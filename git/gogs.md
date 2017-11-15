### 安装
* 基础安装及包下载
```
apt-get update  
apt-get install mysql-server  
apt-get install wget  
wget https://dl.gogs.io/0.11.29/linux_amd64.zip  
apt-get install zip  
unzip linux_amd64.zip  
mkdir gogs-repositories  
```
* 数据库配置
```
service mysql start  
mysql -u root -h localhost
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '******' WITH GRANT OPTION;
flush privileges;
```
* 其他配置
```
cd gogs  
mkdir custom
cd custom
mkdir conf
cd conf
vi app.ini
```
写入信息配置
```
APP_NAME = 名称
RUN_USER = git
RUN_MODE = prod

[server]
HTTP_PORT = 80
PROTOCOL = https
ROOT_URL = https://*******.com/
CERT_FILE = custom/https/cert.pem
KEY_FILE = custom/https/key.pem
DOMAIN =******.com
DISABLE_SSH = false
SSH_PORT = 22
OFFLINE_MODE = false
START_SSH_SERVER = true
LANDING_PAGE = explore

[database]
DB_TYPE = mysql
HOST = localhost:3306
NAME = gogsdb
USER = root
PASSWD = *******
SSL_MODE = disable
PATH = data/gogs.db

[repository]
ROOT = /data/gogs-repositories

[mailer]
ENABLED = false

[service]
REGISTER_EMAIL_CONFIRM = false
ENABLE_NOTIFY_MAIL = false
DISABLE_REGISTRATION = false
ENABLE_CAPTCHA = true
REQUIRE_SIGNIN_VIEW = false

[picture]
DISABLE_GRAVATAR = false

[session]
PROVIDER = file

[log]
MODE = file
LEVEL = Info

[security]
INSTALL_LOCK = true
SECRET_KEY = ***********
```
```
cd ../
mkdir https
cd https
/data/gogs/gogs cert -ca=true -duration=8760h0m0s -host=****.com
```
```
apt-get install openssh-server openssh-client  
apt-get install git-core  
apt-get install python-setuptools  
adduser --system --shell /bin/bash --disabled-password --group git
vi /etc/passwd
```
```
git:x:108:109::/home/git:/bin/bash
```
修改为
```
git:x:0:0::/home/git:/bin/bash
```
```
su git
cd /data/gogs
./gogs web &
```
