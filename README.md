
![PCI device ID](https://github.com/fanhuanji/rtl8125-driver-for-unraid-6.8.2/raw/main/res/20201222184421.png)

# rtl8125-driver-for-unraid-6.8.2

1. Open your unraid usb drive.
2. Rename old "bzmodules" to "bzmodulesold", "bzmodules.sha256" to "bzmodulesold.sha256" (optional, just for backup)
3. Copy "bzmodules" and "bzmodules.sha256" to your device.
4. Enjoy!

Tested on MSI B460M MORTAR(Onboard NIC:RTL8125)

Source code from:https://www.realtek.com/en/component/zoo/category/network-interface-controllers-10-100-1000m-gigabit-ethernet-pci-express-software


If it works, and you appreciate this, please give it a star.


下载bzmodules与bzmodules.sha256，放到U盘里即可（最好记得备份原来的文件）
在MSI B460M MORTAR(迫击炮)(板载:RTL8125)测试无问题

驱动源代码来源：https://www.realtek.com/en/component/zoo/category/network-interface-controllers-10-100-1000m-gigabit-ethernet-pci-express-software

如果能用的话给颗星星吧QAQ，，

# 添加十袋核显驱动 Intel 10th Gen IGD

支持情况看[这个](https://github.com/fanhuanji/rtl8125-driver-for-unraid-6.8.2/blob/main/Supported%20CPU%20IGD%20ID.md)文件，

~添加中，还未想好怎么生成支持所有十代CPU的驱动（有空了几分钟就能弄明白的事情，稍安勿躁）~

注意，目前上传的文件只测试了**I5 10400（id号为0x9BC8的，应该是硅脂U）**

手上有十袋处理器的盆友可以试下，但**不保证一定能成功**，成功了的去置顶Issue里说下支持情况，Emby什么的硬解配置别来问我自己查去。

如果能用的话给颗星星吧QAQ，，


(~另附不替换文件的方法，但未测试是否可行：~

~把r8125.ko放到u盘根目录，修改u盘/config/go文件，底下添加下面两行，理论上可行，但是没试过~，网友测试不行，已删除，谢谢@Samuel-Chia


另外，测试正常工作后插上Winyao的I350T4四口网卡之后可能有问题（我插卡后原eth0板载网卡变成了eth4，重新调整下命名顺序后可能还需要在go文件里追加一行`dhcpcd`才能正常工作，原因未知），总之配置好后就不要随便折腾PCIe相关配置了，改了某些设置后开机无法获取地址的话，关机，重启试试，还不行重新执行上面的覆盖操作再开机应该就会好（原因未知，命名覆盖的文件没被修改过）
）


# How to build by yourself 自己编译驱动（TODO）

等有时间了简要写写，to be done


![Emby硬解无问题](https://github.com/fanhuanji/rtl8125-driver-for-unraid-6.8.2/raw/main/res/20201222165854.png)
