### 安装
```
apt-get update
cd /data
cd redis-4.0.7
apt-get install gcc make
make test MALLOC=libc
make install
cd utils
./install_server.sh
cd /etc
vi redis-server
apt-get install vim
vi redis-server
service redis-server restart
cd /etc/init.d
mv redis_6379 redis-server
service redis-server restart
```
