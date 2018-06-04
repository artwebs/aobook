### 解决 CentOS7 容器 Failed to get D-Bus connection: Operation not permitted
```
curl -fsSL https://get.docker.com/ | sh

docker network create --subnet=172.18.0.0/16 shadownet

chcon -Rt svirt_sandbox_file_t /data



docker run -d -e "container=docker" --privileged=true -v /sys/fs/cgroup:/sys/fs/cgroup --name centos7 centos /usr/sbin/init  
docker exec -it ab49ca003950 /bin/bash 
```
