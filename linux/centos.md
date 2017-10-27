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
