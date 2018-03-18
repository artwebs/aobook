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

### Bind to port 2211 on 0.0.0.0 failed: Permission denied.
```
semanage port -a -t ssh_port_t -p tcp 9481
```

### Fastdfs安装
```
cd /data
git clone https://github.com/happyfish100/libfastcommon.git
git clone https://github.com/happyfish100/fastdfs.git
yum install gcc git-core net-tools
cd libfastcommon/
./make.sh && ./make.sh install
cd ../fastdfs
./make.sh && ./make.sh install
mkdir -p /data/fdfs_tracker
mkdir -p /data/fdfs_storage

cd /etc/fdfs
cp storage.conf.sample storage.conf
cp tracker.conf.sample tracker.conf
vi tracker.conf

    #绑定IP
    bind_addr=
    #端口
    port=22122
    #连接超时时间
    connect_timeout=30
    #日志数据路径
    base_path=/data/fdfs_tracker
    #上传文件时选择group的方法
    #0:轮询，1:指定组，2:选择剩余空间最大
    store_lookup=2
    #如果上面的配置是1，那么这里必须指定组名
    store_group=group2
    #上传文件时选择server的方法
    #0:轮询，1:按IP地址排序，2:通过权重排序
    store_server=0
    #storage上预留空间
    reserved_storage_space = 10%

vi storage.conf

    #storage server所属组名
    group_name=group1
    #绑定IP
    bind_addr=
    #storage server的端口
    port=23000
    #连接超时时间
    connect_timeout=30
    #日志数据路径
    base_path=/data/fdfs_storage/base
    #storage path的个数
    store_path_count=2
    #根据store_path_count的值，就要有storage0到storage(N-1)个
    store_path0=/data/fdfs_storage/storage0
    store_path1=/data/fdfs_storage/storage1
    #跟踪服务器
    tracker_server=192.168.1.222:22122
    tracker_server=192.168.1.233:22122

mkdir -p /data/fdfs_storage/base
mkdir -p /data/fdfs_storage/storage0

firewall-cmd --zone=public --add-port=22122/tcp --permanent
firewall-cmd --zone=public --add-port=23000/tcp --permanent
firewall-cmd --reload

/etc/init.d/fdfs_trackerd start
/etc/init.d/fdfs_storaged start
yum install net-tools.x86_64
netstat -nltp
cd /etc/fdfs
cp client.conf.sample client.conf
vi client.conf

    #存放日志目录
    base_path=/data/client
    #跟踪服务器
    tracker_server=192.168.1.222:22122
    tracker_server=192.168.1.233:22122

mkdir -p /data/client
echo "12345678" >> /data/1.txt
fdfs_upload_file /etc/fdfs/client.conf /data/1.txt
fdfs_download_file /etc/fdfs/client.conf group1/M00/00/00/wKgB3li3a2mAejYPAAAADok0NhY177.txtgroup1/M00/00/00/wKgAIFpoGYyANDUkAAAACZ-6mU0851.txt


fdfs_monitor /etc/fdfs/client.conf
git clone https://github.com/happyfish100/fastdfs-nginx-module.git

yum install zlib-devel openssl-devel gcc-c++
useradd -s /sbin/nologin -M nginx

cd pcre-8.41
./configure --prefix=/data/pcre
make && make install

cd nginx-1.13.8
./configure --prefix=/data/nginx  --with-pcre=/data/pcre-8.41  --user=nginx  --group=nginx  --with-http_ssl_module  --with-http_realip_module  --with-http_stub_status_module  --add-module=/data/fastdfs-nginx-module/src
make && make install

cd /data/fastdfs-nginx-module/src
cp mod_fastdfs.conf /etc/fdfs/

cd /data/fastdfs/conf
cp anti-steal.jpg http.conf mime.types /etc/fdfs/

vi /data/nginx/conf/nginx.conf

    server {
    listen 80;
    server_name localhost;

    location ~ /group[0-9]/M00 {
        ngx_fastdfs_module;
    }
  }

vi /etc/fdfs/mod_fastdfs.conf
    #日志目录
    base_path=/tmp
    #跟踪服务器
    tracker_server=192.168.1.222:22122
    tracker_server=192.168.1.233:22122
    #url中是否有group名称
    url_have_group_name = true
    #storage path的个数
    store_path_count=2
    #根据store_path_count的值，就要有storage0到storage(N-1)个
    store_path0=/data/fdfs_storage/storage0
    store_path1=/data/fdfs_storage/storage1

firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload

/data/nginx/sbin/nginx
fdfs_upload_file /etc/fdfs/client.conf /data/1.txt
http://192.168.0.32/group1/M00/00/00/wKgAIFpoK22ATIy4AAAACZ-6mU0739.txt


/etc/init.d/fdfs_trackerd stop
/etc/init.d/fdfs_storaged stop

```

### 修改启动内核
```
cat /boot/grub2/grub.cfg |grep menuentry
grub2-set-default 'CentOS Linux (3.10.0-693.el7.x86_64) 7 (Core)'
grub2-editenv list
```

### 修改主机名
```
hostnamectl set-hostname xxx
```

[安装包搜索](http://rpm.pbone.net/)
