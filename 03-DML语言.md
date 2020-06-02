### DML

数据操作语言

insert update delete

#### 1、插入语句

```mysql
insert into 表名(列名)

values();
```

- 插入的值的类型要和列的类型一致。
- 不可以为null的列必须插入值。
- 列的顺序可以变，但是要一一对应。
- 列数和值的数目必须一致
- 省略列名，默认就是所有列
- 支持插入多行
- 支持子查询

```mysql
insert into 表名
set 列名=值，列名=值，。。。。
```

#### 2、修改语句

- 修改单表记录

  - ```mysql
    UPDATE 表名
    SET 列=新值,列=新值......
    WHERE 筛选条件
    ```

- 修改多表记录

  - ```mysql
    #sq92语法
    UPDATE 表1 别名,表2 别名
    SET 列=值,...
    WHERE 连接条件
    AND 筛选条件
    
    #sql99语法
    UPDATE 表1 别名
    INNER|LEFT|RIGHT JOIN 表1 别名
    ON 连接条件
    SET 列=值,....
    WHERE 筛选条件
    ```

  - ```mysql
    #修改张无忌的女朋友手机号为114
    update boys bo
    inner join beauty b 
    on bo.id=b.boyfriend_id
    set b.phone=114
    where bo.boyName='张无忌'
    
    #修改没有男朋友的女神的男朋友编号都为2
    update boys bo
    right join beauty b on bo.`id`=b.`boyfriend_id`
    set b.`boyfriend_id`=2
    where bo.`id` is null;
    ```

3、删除语句

```mysql
DELETE FROM table_name  WHERE 筛选条件
truncate table table_name 删除整个表
```

```mysql
#sql92
DELETE 别名（表1b表2或者都加）
FROM 表1 别名，表2 别名
WHERE 连接条件
AND 筛选条件

#sql99
DELETE 表1 的别名，表2的别名
FROM 表1 别名
INNER|LEFT|RIGHT JOIN 表2 别名 ON 连接条件
WHERE 筛选条件

#多表的删除 删除张无忌的女朋友的信息
DELETE b
FROM beauty b
INNER JOIN boys bo 
ON b.boyfriend_id=bo.id
WHERE bo.boyName='张无忌'
SELECT * FROM beauty;
```

- 假如删除的表中有自增长列
  - 用delete删除之后，再插入数据，自增长的列从断点开始
  - 用truncate 删除，再插入数据，从1开始。
  - truncate 删除不能回滚，delete 删除可以回滚