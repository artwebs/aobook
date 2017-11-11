### 开放端口
```
firewall-cmd --zone=public --add-port=8099/tcp --permanent   
firewall-cmd --reload
```

### 解锁
```
systemctl unmask firewalld
```

### 查看开放端口
```
firewall-cmd --zone=public --list-ports
```
### ftp安装
```
一、通过yum安装vsftpd
yum install -y vsftpd

二、修改vsftpd的配置文件
vi /etc/vsftpd/vsftpd.conf
修改配置文件如下：
1.不允许匿名访问
anonymous_enable=NO

2.允许使用本地帐户进行FTP用户登录验证
local_enable=YES
3.使用户不能离开主目录
当chroot_list_enable=YES，chroot_local_user=YES时，在/etc/vsftpd.chroot_list文件中列出的用户，可以切换到其他目录；未在文件中列出的用户，不能切换到其他目录。
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
配置文件最后添加
allow_writeable_chroot=YES
要不然会报错
500 OOPS: vsftpd: refusing to run with writable root inside chroot()
如果/etc/vsftpd/chroot_list不存在，则需要创建该文件
vi /etc/vsftpd/chroot_list
:wq直接保存并退出就行。

4.设定支持ASCII模式的上传和下载功能。
ascii_upload_enable=YES
ascii_download_enable=YES
最后 :wq保存修改，重启vsftpd

systemctl restart vsftpd.service
三、新建FTP用户

useradd -d /var/ftp/public_root -g ftp -s /sbin/nologin ftpuser
修改该FTP用户密码

passwd ftpuser
```
### 错误: 无法建立数据连接: ECONNREFUSED - 连接被服务器拒绝
```
解决方式：
更换使用FTP软件连接方式，把被动改为主动，把传输模式改为主动 
```
