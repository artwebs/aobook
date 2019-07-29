### 压缩文件
```
tar -cjvf   openwrt171207.etc.tar.bz2 openwrt-trunk
```

### fastndf
```
libfastcommon-1.0.35
```
### 配置磁盘共享
```
vi /etc/exports 
exportfs -r
service rpcbind start
service nfs start
root rpcinfo -p localhost
root showmount -e localhost
  ```
