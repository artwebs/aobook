### 安装
```
docker pull kalilinux/kali-linux-docker   
docker run -t -i kalilinux/kali-linux-docker /bin/bash  
apt-get update && apt-get install metasploit-framework  
```
### 安装vm-tools
```
apt -y full-upgrade
apt -y install open-vm-tools-desktop fuse
reboot
```

### metasploit-framework 安装
```
apt-get install postgresql
su - postgres -c "psql"
alter user postgres with password 'xxxxxx';
\q
apt-get install metasploit-framework
msfconsole
db_connect postgres:xxxxxx@127.0.0.1/msfbook
db_status
db_rebuild_cache
```

### 解决metasploit-framework 安装后启动异常问题
```
cd /var
touch swap.img
chmod 600 swap.img
dd if=/dev/zero of=/var/swap.img bs=1024k count=1000
mkswap /var/swap.img
swapon swap.img
free
```
