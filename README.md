# RealTimeOnRaspberryPi
关于树莓派实时时钟遇到的问题
实时时钟设置参考链接
http://www.raspberrypi-spy.co.uk/2015/05/adding-a-ds3231-real-time-clock-to-the-raspberry-pi/
http://blog.csdn.net/huayucong/article/details/50061025

遇到问题：
开机运行指令
sudo echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device
导致硬件时钟重置成与树莓派系统时钟一样的初始值
树莓派开机启动时间为1979年1月1日
硬件时钟被重置为这个时间并且为不可读变量

解决办法
系统软件有bug，运行
sudo apt-get –y –f --fix-missing  upgrade

对系统软件进行重新更新就可解决问题
