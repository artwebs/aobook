### oralce docker 安装
```
unzip docker-images-master.zip
cd docker-images-master/OracleDatabase
mv linuxx64_12201_database.zip  12.2.0.1/
./buildDockerImage.sh -v 12.2.0.1 -e
docker run  -i -t  --name  oracle --net shadownet --ip 172.18.0.15  -p 1521:1521 -p 5500:5500 -v /data/dockerData/oracle:/data oracle/database:12.2.0.1-ee

docker exec -ti oracle sqlplus sys@orclcdb as sysdba
管理数据库：docker exec -ti oracle bash

```

### oracle 创建表空及用户
```
show pdbs;

create tablespace kh_data
logging
datafile '/data/kh_data.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

create temporary tablespace kh_temp
tempfile '/data/kh_temp.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

alter session set container=ORCLPDB1

create tablespace kh_data
logging
datafile '/data/pdb1/kh_data.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

create temporary tablespace kh_temp
tempfile '/data/pdb1/kh_temp.dbf'
size 50m  
autoextend on  
next 50m maxsize 20480m  
extent management local;

create user c##kh identified by kh   default tablespace kh_data;  

grant connect,resource to c##kh container=all;

```

### 解决docker root权限问题
```
docker exec -u 0 -it oralce bash
```

### 授权
```
ALTER USER 用户名 QUOTA UNLIMITED ON 表空间;
grant imp_full_database to 用户;
Grant Create Table, Create View, Select Any table, Create sequence, Create trigger,
  Create procedure, Create role, Grant any privilege, Drop any role, Create public synonym,
  Drop public synonym to 用户;
```

### 数据导入
```
NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
imp 用户名/密码@实例 file=文件 DESTROY=y full=y ignore=y  commit=y
```
