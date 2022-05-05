# Hackintosh-OC-Dell-OptiPlex-7060-Micro

* OpenCore 0.8.0
* macOS Monterey 12.3.1 测试正常


## 硬件配置

* 主机：Dell OptiPlex 7060 Micro
* CPU: i9-9900T （7060 Micro默认只支持8代cpu，上9代低压cpu需要刷BIOS）
* 内存: 笔记本内存 DDR4 16G 2666 x2
* SSD：WD Blue SN570 500GB SSD
* Wifi+BT: BCM94360Z4 （4天线，需要再贴2个贴片天线）


## BIOS设置
* General → Advanced Boot Options: ***uncheck***
* System Configuration → SATA Operation: ***AHCI***
* Secure Boot → Secure Boot Enable: ***Disabled***
* Intel® Software Guard Extensions™ → Intel® SGX™ Enable: ***Disabled***
* Virtualization Support → VT for Direct I/O: ***uncheck***

## 首次启动需要进入 modGRUBShell 调整BIOS隐藏设定
* Set Pre-Allocated DVMT to 64M: 
***setup_var 0x8DC 0x02***
* Disable CFG lock: 
***setup_var 0x5BE 0x00***


## 如果你的系统没有IMEI设备，需要通过刷BIOS打开ME

* <code>ioreg|grep IMEI</code> 如果没有任何输出，说明你的机器出厂时被禁用了ME
* 没有IMEI，会让机器从睡眠中唤醒后失去核显加速功能，故障现象包括：打开部分APP界面空白，鼠标转圈。参考： https://github.com/acidanthera/bugtracker/issues/990
* BIOS/7060_Add9thCPU_ME_Enabled.bin 是修改过的BIOS固件，加入了9代cpu支持，开启了Intel ME。


