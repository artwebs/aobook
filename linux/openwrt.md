###
```
package/base-files/files/etc/config/system
config system
        option hostname goldsunny
        option timezone CST-8
        option zonename Asia/Shanghai

config timeserver ntp
        list server     0.openwrt.pool.ntp.org
        list server     1.openwrt.pool.ntp.org
        list server     2.openwrt.pool.ntp.org
        list server     3.openwrt.pool.ntp.org
        option enabled 1
        option enable_server 0
```

###
```
ntpd -n -d -p cn.ntp.org.cn

ntpd -n -d -p ntp1.aliyun.com

编译的时候确保勾选Base system  --->base-file包，然后把/etc/crontabs/root这个文件放在源代码的files/etc/crontab下面并重新编译固件

https://zoublog.com/compile-customized-openwrt/
```
