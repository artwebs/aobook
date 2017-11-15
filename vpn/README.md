### 解决 缺少kernel-headers依赖
```
yum install kernel-headers-$(uname -r) kernel-devel-$( uname -r) -y   
登录 http://rpm.pbone.net/ 搜索相关缺少的包
```
