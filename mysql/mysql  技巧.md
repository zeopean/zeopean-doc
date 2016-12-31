
#### myisam 碎片清理
```
optimize table table_name;

```
#### 查看数据表引擎
```
show create table table_name;

```
#### mysql蠕虫复制
```
INSERT into insert_table_name(field_1,field_2,...) select field_1,field_2,... from copy_table_name; 

```
#### mysql查看表结构
```
desc table_name;

```