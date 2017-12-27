### 常用命令
```
GRANT ALL PRIVILEGES ON *.* TO 'user'@'192.168.42.%' IDENTIFIED BY 'xxxxx' WITH GRANT OPTION;
flush privileges;
```

### 动态列（Dynamic Columns）
```
1、表结构
create table assets (
  item_name varchar(32) primary key, -- A common attribute for all items
  dynamic_cols  blob  -- Dynamic columns will be stored here
);

2、插入JSON格式数据
INSERT INTO assets values ('MariaDB T-shirt', COLUMN_CREATE('color', 'blue', 'size', 'XL'));
insert into assets values ('Thinkpad Laptop', COLUMN_CREATE('color', 'black', 'price', 500));

3、获取全部Key-Value
select item_name, COLUMN_JSON(dynamic_cols) from assets;

4、S获取全部Key（键）
SELECT item_name, column_list(dynamic_cols) FROM assets;

5、获取Key（键）color的Value（值）
SELECT item_name, COLUMN_GET(dynamic_cols, 'color' as char) AS color FROM assets;

6、删除一个Key-Value：
UPDATE assets SET dynamic_cols=COLUMN_DELETE(dynamic_cols, 'price') WHERE COLUMN_GET(dynamic_cols, 'color' as char)=‘black‘;

7、增加一个Key-Value：
 UPDATE assets SET dynamic_cols=COLUMN_ADD(dynamic_cols, 'warranty', '3 years') WHERE item_name=‘Thinkpad Laptop‘;

8、更改一个Key-Value：
UPDATE assets SET dynamic_cols=COLUMN_ADD(dynamic_cols,'color', 'white') WHERE COLUMN_GET(dynamic_cols, 'color' as char)='black';
```
