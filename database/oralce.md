### oralce docker 安装
```
unzip docker-images-master.zip
cd docker-images-master/OracleDatabase
mv linuxx64_12201_database.zip  12.2.0.1/
./buildDockerImage.sh -v 12.2.0.1 -e
docker run  -i -t  --name  oracle --net shadownet --ip 172.18.0.15  -p 1521:1521 -p 5500:5500 -v /data/dockerData/oracle:/data oracle/database:12.2.0.1-ee

```

### oracle 创建表空及用户
```
show pdbs;

create tablespace fz_data
logging
datafile '/data/fz_data.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

create temporary tablespace fz_temp
tempfile '/data/fz_temp.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

alter session set container=ORCLPDB1

create tablespace fz_data
logging
datafile '/data/pdb1/fz_data.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;

create temporary tablespace fz_temp
tempfile '/data/pdb1/fz_temp.dbf'
size 50m  
autoextend on  
next 50m maxsize 20480m  
extent management local;

create user c##fz identified by xxxxxx   
default tablespace fz_data;  

grant connect,resource to c##fz container=all;

```

### 解决docker root权限问题
```
docker exec -u 0 -it oralce bash
```
