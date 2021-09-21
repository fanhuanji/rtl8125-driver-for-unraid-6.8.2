
## 基本工作

以当时版本为例
首先，为了编译内核驱动，我们需要内核源代码，可以在目标系统上通过`uname -srm`先获取到目标系统内核版本，，
例如获取到：
```
root@unraid:~# uname -srm
Linux 4.19.98-Unraid x86_64
```


知道内核版本后，切到事先准备好的其他linux系统(比如ubuntu server 20.04)，下载源码。`wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.19.98.tar.xz`

切换到root shell。(`su root`或`sudo -i`)，，安装编译打包用的软件包，`build-essential bison flex libssl-dev libelf-dev libelf-dev`(debian系用apt install)，（可能不全，后面如果提示缺什么命令的话找下命令装下），，

定位到刚下载的源码压缩包，然后解压到usr/src目录，`tar -C /usr/src/ -xf linux-4.19.98.tar.xz`。
为了方便操作（系统里也会有其他源码目录，比如ubuntu里的linux-headers-5.4.0-***），建立符号链接，将usr/src/linux连接到解压出的源码目录，`ln -sf /usr/src/linux-4.19.98 /usr/src/linux`。

由于unraid里有许多lime团队针对其nas需求而定制的功能，对内核做了修改，而下载到的原版内核没有这些修改，所以我们需要从unraid系统里提出来这些修改。这时回到我们的unraid机器，将`/usr/src/linux-4.19.98-Unraid`目录打包(切进去，`tar zcvf linux-4.19.98-Unraid.tar.gz .[!.]* *`，特别注意目录里应该有个`.config`文件，要一并打包进去（一会解压的时候也检查下），不然一会make的时候会缺失配置)，，

将打包得到的`linux-4.19.98-Unraid.tar.gz`拷贝到ubuntu，将其内容解压到`/usr/src/linux-4.19.98`目录，然后切换到源码目录`cd /usr/src/linux`，使用`find . -type f -iname '*.patch' -print0|xargs -n1 -0 patch -p 1 -i`将补丁应用到源码中。

过程中没有出问题的化，这里已经成功应用了，接下来依次键入
```
# 使用原先配置准备编译环境
make oldconfig
# 准备编译内核modules（驱动）的环境
make -j10 modules_prepare
# 编译bzImage（内核映像） 编译驱动模块
make -j10 bzImage; make -j10; make -j10 modules
```

以上三行成功执行的话，我们就得到了内核与相配套的驱动包了，（没修改过的驱动包，修改的地方见下面，这一步只是确保之前的步骤没问题）。

执行`make modules_install`将编译好的驱动包拷贝到系统目录，然后使用`mksquashfs /lib/modules/4.19.98-Unraid/ bzmodules -keep-as-directory -noappend`对驱动包进行打包，得到bzmodules文件。
找到`/usr/src/linux/arch/x86/boot/bzImage`，有了bzImage与bzmodules文件，我们便可以尝试替换unraid的u盘上的文件了（记得备份u盘上的那俩文件），替换文件时记得将bzImage与bzmodules文件内容修改成新编译出的文件的哈希（注意不要修改文件结构换行符、文本编码之类的，哈希方法为sha256，可以用unraid自带的`sha256sum`命令计算文件哈希值），，
然后便可以尝试开机看是否能正常启动了，如果机器能够正常启动并使用，证明前面所作的操作没有问题，可以继续编译一些树外的内核模块了，，


## 修改并编译树外驱动
以树外编译rtl8125的驱动为例
首先去Realtek官网下载驱动源码包，下载后解压。然后通过`make -C /usr/src/linux/ M=/home/你解压路径/r8125-9.005.01/src modules`编译，编译后可以得到`r8125.ko`文件，有需求的可选择对该文件清理下无用的符号信息以缩减大小`objcopy --strip-debug r8125.ko`。

此时可以将r8125.ko文件拷贝到unraid机器上进行测试，参考`insmod`，`rmmod`，`modprobe`等命令使用，测试驱动可以正常使能目标设备后，可以选择将驱动打包进bzmodules包中。在这里简单说下修改squashfs的方法，，

首先，切到一个干净的目录，并将bzmodules文件放到当前目录，将要打包的驱动文件放到当前目录，依次执行
```
# 创建挂接点文件夹
mkdir fm
# 将squashfs挂接到指定挂接点
sudo mount bzmodules ./fm/
# 创建临时工作目录
mkdir to
mkdir temp
mkdir fin
# 使用overlay fs挂接，指定上下层文件系统与工作目录
sudo mount -t overlay -o lowerdir=./fm,upperdir=./to,workdir=./temp overlay ./fin
```
挂载好后，便可以将要做的修改做到fin中，如
```
# 要将ko文件先打包（牙膏集显驱动）
xz -z ./i915.ko
# 然后拷贝进挂载的fin目录中
sudo cp ./i915.ko.xz ./fin/5.5.8-Unraid/kernel/drivers/gpu/drm/i915/
# 同理对待 （r8125网卡驱动）
xz -z ./r8125.ko
sudo cp ./r8125.ko.xz ./fin/5.5.8-Unraid/kernel/drivers/net/ethernet/realtek/
```
拷贝好后，执行
```
# 重新打包squashfs，起名为bzmodulesnew
mksquashfs ./fin/ bzmodulesnew
# 取消挂载并删除临时文件夹
sudo umount ./fin
sudo umount ./fm/
sudo rm -rf ./fm ./fin ./to ./temp
```
到这里，就完成了驱动包的修改，取出bzmodulesnew，改名成bzmodules，覆盖u盘文件，尝试启动unraid，如果一切顺利，系统会加载上你新编译出的驱动，可以在系统里输入`lsmod`查看当前装载的驱动，可通过`dmesg`查看系统启动时驱动加载时的输出，，



ps:当时笔记里有这么一行，时间太久，忘了是不是必须的了，如果在编译树外模块的时候提示找不到symvers，可以试下这条命令，执行`make modules_install`后应该就会有左边的文件，，
```
sudo cp /lib/modules/4.19.98-Unraid/build/Module.symvers /usr/src/linux-4.19.98/
```

pps:QAQ有问题大佬们请轻喷，也谢谢给指出问题，，
