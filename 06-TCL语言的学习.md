### TCL

事务控制语言

事务:

一个或一组sql语句组成一个执行单元，这个执行单元要么全部执行，要么全部不执行。

innodb 支持事务，myisam ,memory 不支持事务

1、事务的ACID属性

- 原子性:最小，不可分割的工作单位。

- 一致性:从一个状态到另外一个一致性状态。
- 隔离性:一个事务的执行不能被其他事务干扰
- 持久性：一个事务一旦被提交，它对数据库中数据的改变就是永久性的。

#### 1、事务的创建

隐式事务：事务没有明显的开始和结束。

显式事务:事务具有明显的开始和结束

- 开启事务
  - set commit =0;
  - start transaction;可选的
- 编写事务中的sql语句
- 结束事务
  - 提交事务
  - 回滚事务

#### 2、数据库的隔离级别

对于同时运行的多个事务，当这些事务访问数据库中相同的数据时，如果没有采用必要的隔离机制，就会导致各种并发问题。

![Problem](C:/Users/JC/Desktop/秋招/NoteBook/03-DataBase/Mysql/images/problem.png)

隔离级别

- 可以通过seletc @@tx_isolation 查看当前的隔离级别。

- 设置当前隔离级别 set session transaction isolation level read uncommitted 

- 设置数据库系统的全局的隔离级别

  - ```mysql
    set global transaction isolation levelread commited;
    ```

  - ![](C:/Users/JC/Desktop/秋招/NoteBook/03-DataBase/Mysql/images/le.png)

- savepoint 回滚的时候只回滚到保存点。

- delete 数据之后可以回滚。

- truncate 数据之后不能回滚。