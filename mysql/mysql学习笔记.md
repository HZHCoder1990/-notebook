#### MySQL学习笔记

学习资源来自B站: [老杜带你学mysql](https://www.bilibili.com/medialist/play/ml1575900633/BV1Vy4y1z7EX?oid=800230080&otype=2)

- MySQL的启动与停止

  1.启动MySQL: 在系统偏好设置启动MYSQL服务

  2.在终端输入以下命令进入登录(需要输入密码)MySQL环境

  ```ruby
  mysql -uroot -p
  ```

  3.退出MySQL环境

  ```ruby
  exit
  ```

- MySQL常用命令

  查看MySQL有哪些数据库(以分号结尾)

  ```mysql
  SHOW DATABASES;
  ```

  清屏

  ```mysql
  SYSTEM CLEAR;
  ```

  创建数据库

  ```mysql
  CREATE DATABASE TEST(数据库名称); 
  ```

  使用某一个数据库

  ```mysql
  USE TEST(数据库名称);
  ```

  查看某个数据库中表的情况(前提是切换到了某个数据库)

  ```mysql
  SHOW TABLES;
  ```

- SQL语句的分类

  **DQL**: 数据查询语句(凡是带有select关键字的都是查询语句) data query language 譬如: select ...

  **DML**:数据操作语句(凡是对表中的数据进行增删改的都是DML) 譬如: insert、delete、update

  **DDL**:数据定义语句(凡是带有create、drop、alter都是DDL) DDL主要操作的是表的结构，不是表中的数据

  create: 创建

  drop:删除

  alter: 修改

  **TCL**:事务控制语言 包括:事务提交(commit)、事务回滚(rollback)

  **DCL**:数据控制语言 譬如:授权(grant)、撤销权限(revoke)...

- 导入数据库到MySQL

  ```mysql
  mysql> source /Users/huangzhihao/Desktop/工具+源码+资料/document/bjpowernode.sql
  ```

  注意语句后面没有*分号*!

- 查看表中的数据

  ```mysql
  SELECT * FROM emp(表名);
  ```

- 查看表的结构

  ```mysql
  DESC 表名;
  ```

- 查看MySQL版本号

  ```mysql
  SELECT VERSION();
  ```

- 查看当前使用的是哪一个数据库

  ```mysql
  SELECT DATABASE();
  ```

  注意:MySQL是不见分号不执行! 

  终止一条MySQL语句的执行: \c

  ```mysql
  mysql> show
      -> \c  # 退出当前语句
  mysql>
  ```

  SQL是不区分大小写的: 

  #### 简单查询

  1.查询一个字段(已经选中某一个数据库了)

  ```mysql
  # SELECT 字段名 FROM 表名;
  SELECT JOB FROM EMP;  # 这里JOB => job EMP => emp 都行
  ```

  2.查询多个字段

  ```mysql
  # SELECT 字段名1,字段名2,... FROM 表名;
  SELECT JOB,SAL FROM EMP;
  ```

  3.查询所有字段

  ```mysql
  # 使用通配符 ’*‘ 即可 => 但是效率比较低
  SELECT * FROM EMP;
  ```

  4.给查询的字段起别名

  ```mysql
  +-----------+---------+
  | JOB       | SAL     |
  +-----------+---------+
  | CLERK     |  800.00 |
  | SALESMAN  | 1600.00 |
  | SALESMAN  | 1250.00 |
  | MANAGER   | 2975.00 |
  | SALESMAN  | 1250.00 |
  | MANAGER   | 2850.00 |
  | MANAGER   | 2450.00 |
  | ANALYST   | 3000.00 |
  | PRESIDENT | 5000.00 |
  | SALESMAN  | 1500.00 |
  | CLERK     | 1100.00 |
  | CLERK     |  950.00 |
  | ANALYST   | 3000.00 |
  | CLERK     | 1300.00 |
  +-----------+---------+
  
  # 给SAL起一个别名 只是显示结果修改了，原表不变
  SELECT JOB,SAL AS MONEY FROM EMP;
  
  # 结果
  +-----------+---------+
  | JOB       | MONEY   |
  +-----------+---------+
  | CLERK     |  800.00 |
  | SALESMAN  | 1600.00 |
  | SALESMAN  | 1250.00 |
  | MANAGER   | 2975.00 |
  | SALESMAN  | 1250.00 |
  | MANAGER   | 2850.00 |
  | MANAGER   | 2450.00 |
  | ANALYST   | 3000.00 |
  | PRESIDENT | 5000.00 |
  | SALESMAN  | 1500.00 |
  | CLERK     | 1100.00 |
  | CLERK     |  950.00 |
  | ANALYST   | 3000.00 |
  | CLERK     | 1300.00 |
  +-----------+---------+
  ```

  

  

