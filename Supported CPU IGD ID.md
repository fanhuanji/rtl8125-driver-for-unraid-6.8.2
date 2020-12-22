目前已支持情况如下：

ID为0x9BC5的集显：
未测试

ID为0x9BC8的集显：
I5 10400 已测试

ID为0x9BA8的集显：
G6400（待群友测试） 

ID号在以上列表的可以自己测试（在命令行里输入`lspci | grep VGA`查看后面的四位十六进制数字就是ID号），测试可以的老哥可以联系提供下信息

UHD 610的支持待加入（没有设备没人测试）

使用UHD630 CPU的集成显卡ID如下，（井号前空白的说明爬虫没获取到id，没法办）
```python
0x9BC5 # Intel® Core™ i9-10910 Processor
0x9BC5 # Intel® Core™ i9-10850K Processor
       # Intel® NUC 9 Extreme Laptop Kit - LAPQC71D
       # Intel® NUC 9 Extreme Laptop Kit - LAPQC71C
       # Intel® NUC 9 Extreme Laptop Kit - LAPQC71B
       # Intel® NUC 9 Extreme Laptop Kit - LAPQC71A
0x9BC6 # Intel® Xeon® W-1290TE Processor
0x9BC6 # Intel® Xeon® W-1270TE Processor
0x9BC6 # Intel® Xeon® W-1270E Processor
0x9BE6 # Intel® Xeon® W-1250TE Processor
0x9BE6 # Intel® Xeon® W-1250E Processor
0x9BC8 # Intel® Pentium® Gold G6600 Processor
0x9BC8 # Intel® Pentium® Gold G6500T Processor
0x9BC8 # Intel® Pentium® Gold G6500 Processor
0x9BC5 # Intel® Core™ i9-10900TE Processor
0x9BC5 # Intel® Core™ i9-10900T Processor
0x9BC5 # Intel® Core™ i9-10900K Processor
0x9BC5 # Intel® Core™ i9-10900E Processor
0x9BC5 # Intel® Core™ i9-10900 Processor
0x9BC5 # Intel® Core™ i7-10700TE Processor
0x9BC5 # Intel® Core™ i7-10700K Processor
0x9BC5 # Intel® Core™ i7-10700E Processor
0x9BC5 # Intel® Core™ i7-10700 Processor
0x9BC8 # Intel® Core™ i5-10600T Processor
0x9BC8 # Intel® Core™ i5-10600 Processor
0x9BC8 # Intel® Core™ i5-10500TE Processor
0x9BC8 # Intel® Core™ i5-10500T Processor
0x9BC8 # Intel® Core™ i5-10500E Processor
0x9BC8 # Intel® Core™ i5-10500 Processor
0x9BC8 # Intel® Core™ i5-10400T Processor
0x9BC8 / 0x9BC5 # Intel® Core™ i5-10400 Processor
0x9BC8 # Intel® Core™ i3-10320 Processor
0x9BC8 # Intel® Core™ i3-10300T Processor
0x9BC8 # Intel® Core™ i3-10300 Processor
0x9BC8 # Intel® Core™ i3-10100TE Processor
0x9BC8 # Intel® Core™ i3-10100T Processor
0x9BC8 # Intel® Core™ i3-10100E Processor
0x9BC8 # Intel® Core™ i3-10100 Processor
       # Intel® NUC 9 Pro Kit - NUC9V7QNX
       # Intel® NUC 9 Pro Compute Element - NUC9V7QNB
       # Intel® NUC 9 Extreme Kit - NUC9i9QNX
       # Intel® NUC 9 Extreme Kit - NUC9i7QNX
       # Intel® NUC 9 Extreme Kit - NUC9i5QNX
       # Intel® NUC 9 Extreme Compute Element - NUC9i9QNB
       # Intel® NUC 9 Extreme Compute Element - NUC9i7QNB
       # Intel® NUC 9 Extreme Compute Element - NUC9i5QNB
0x3E98 # Intel® Core™ i9-9900KS Processor
0x3E9A # Intel® Xeon® E-2278GEL Processor
0x3E9A # Intel® Xeon® E-2278GE Processor
0x3E9A # Intel® Xeon® E-2226GE Processor
0x3E9B # Intel® Core™ i7-9850HL Processor
0x3E9B # Intel® Core™ i7-9850HE Processor
0x3E98 # Intel® Core™ i7-9700E Processor
0x3E98 # Intel® Core™ i5-9500TE Processor
0x3E98 # Intel® Core™ i5-9500E Processor
0x3E98 # Intel® Core™ i3-9100TE Processor
0x9BC8 # Intel® Core™ i3-10100 Processor
       # Intel® NUC 9 Pro Kit - NUC9V7QNX
       # Intel® NUC 9 Pro Compute Element - NUC9V7QNB
       # Intel® NUC 9 Extreme Kit - NUC9i9QNX
       # Intel® NUC 9 Extreme Kit - NUC9i7QNX
       # Intel® NUC 9 Extreme Kit - NUC9i5QNX
       # Intel® NUC 9 Extreme Compute Element - NUC9i9QNB
       # Intel® NUC 9 Extreme Compute Element - NUC9i7QNB
       # Intel® NUC 9 Extreme Compute Element - NUC9i5QNB
0x3E98 # Intel® Core™ i9-9900KS Processor
0x3E9A # Intel® Xeon® E-2278GEL Processor
0x3E9A # Intel® Xeon® E-2278GE Processor
0x3E9A # Intel® Xeon® E-2226GE Processor
0x3E9B # Intel® Core™ i7-9850HL Processor
0x3E9B # Intel® Core™ i7-9850HE Processor
0x3E98 # Intel® Core™ i7-9700E Processor
0x3E98 # Intel® Core™ i5-9500TE Processor
0x3E98 # Intel® Core™ i5-9500E Processor
0x3E98 # Intel® Core™ i3-9100TE Processor
0x3E9B # Intel® Core™ i3-9100HL Processor
0x3E98 # Intel® Core™ i3-9100E Processor
0x3E91 # Intel® Pentium® Gold G5620 Processor
0x3E91 # Intel® Pentium® Gold G5600T Processor
0x3E9B # Intel® Core™ i9-9980HK Processor
0x3E9B # Intel® Core™ i9-9880H Processor
0x3E9B # Intel® Core™ i7-9850H Processor
0x3E9B # Intel® Core™ i7-9750H Processor
0x3E98 # Intel® Core™ i7-9700T Processor
0x3E98 # Intel® Core™ i7-9700 Processor
0x3E92 # Intel® Core™ i5-9600T Processor
0x3E92 # Intel® Core™ i5-9600 Processor
0x3E92 # Intel® Core™ i5-9500T Processor
0x3E92 # Intel® Core™ i5-9500 Processor
0x3E92 # Intel® Core™ i5-9400T Processor
0x3E9B # Intel® Core™ i5-9400H Processor
0x3E9B # Intel® Core™ i5-9300H Processor
0x3E91 # Intel® Core™ i3-9350K Processor
0x3E91 # Intel® Core™ i3-9320 Processor
0x3E91 # Intel® Core™ i3-9300T Processor
0x3E91 # Intel® Core™ i3-9300 Processor
0x3E91 # Intel® Core™ i3-9100T Processor
0x3E91 # Intel® Core™ i3-9100 Processor
0X3E98/x92 # Intel® Core™ i5-9400 Processor
0x3E98 # Intel® Core™ i9-9900K Processor
0x3E98 # Intel® Core™ i7-9700K Processor
0x3E98 # Intel® Core™ i5-9600K Processor
0x3E9B # Intel® Core™ i3-8100B Processor
       # Intel® Core™ i3-8100H Processor
0x3E92 # Intel® Core™ i7-8086K Processor
0x3E91 # Intel® Pentium® Gold G5600 Processor
0x3E91 # Intel® Pentium® Gold G5500T Processor
0x3E91 # Intel® Pentium® Gold G5500 Processor
0x3E9B # Intel® Core™ i7-8850H Processor
0x3E9B # Intel® Core™ i7-8750H Processor
0x3E92 # Intel® Core™ i7-8700T Processor
0x3E9B # Intel® Core™ i7-8700B Processor
0x3E91/x92 # Intel® Core™ i3-8100 Processor
```
