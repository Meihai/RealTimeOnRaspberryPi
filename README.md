# RealTimeOnRaspberryPi
关于树莓派实时时钟遇到的问题
实时时钟设置参考链接
http://www.raspberrypi-spy.co.uk/2015/05/adding-a-ds3231-real-time-clock-to-the-raspberry-pi/
http://blog.csdn.net/huayucong/article/details/50061025
http://henson.github.io/post/raspiclock/
http://www.elevendroids.com/2012/12/setting-up-hardware-rtc-in-raspbian/
https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=67364

遇到问题：
开机运行指令
sudo echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device
导致硬件时钟重置成与树莓派系统时钟一样的初始值
树莓派开机启动时间为1970年1月1日
硬件时钟被重置为这个时间并且为不可读变量

解决办法
系统软件有bug，运行
sudo apt-get –y –-force-yes --fix-missing  upgrade

对系统软件进行重新更新就可解决问题，但后来在另一个树莓派上运行该指令以后结果发现不行
再对树莓派的实时时钟设置进行了解
由于树莓派内部并没有实时时钟，因此树莓派有一个fake-hwclock，它会保存系统最后一次关机的时间放在
/etc/fake-hwclock.data文件中，并且默认为格林威治时间
要想显示为本地时间，可以把 /sbin/fake-hwclock文件中的这一行
"date -u '+%Y-%m-%d %H:%M:%S' > $FILE"
改为
"date '+%Y-%m-%d %H:%M:%S' > $FILE"
即可.原因是"-u"会将时间转换为UTC时间
