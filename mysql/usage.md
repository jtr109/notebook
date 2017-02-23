# MySQL 基础操作

## 1 登录

`$ mysql -h localhost -P port -u username -p`

## 2 操作 database

- 显示所有 database

  `mysql> SHOW DATABASES;`

- 创建 database

  `mysql> CREATE DATABASE db_name;`
  
- 删除 database

  `mysql> DROP {DATABASE | SCHEMA} [IF EXISTS] db_name`
  
- 重命名 database

  `mysql> RENAME TABLE old_db.table TO new_db.table;`
  
- 进入 database

  `mysql> USE db_name;`


## 3 操作 table

- 显示所有 table

  ```
  msyql> SHOW TABLES;
  ```

- 创建 table

  ```
  mysql> CREATE TABLE Shohin
  (shohin_id      CHAR(4)       NOT NULL,
   shohin_mei     VARCHAR(100)  NOT NULL,
   shohin_bunrui  VARCHAR(32)   NOT NULL,
   hanbai_tanka   INTERGER,
   shiire_tanka   INTERGER,
   torokubi       DATE,
   PRIMARY KEY    (shohin_id));
  ```

- 删除 table

  ```
  mysql> DROP TABLE Shohin;
  ```
  
- 修改 table

  添加列
  
  ```
  mysql> ALTER TABLE <tablename> ADD COLUMN <column>;
  ```

## 4 操作数据

- 查询

  ```
  SELECT <col_name>, ...
    FROM <table_name>
   WHERE <condition>;
  ```
  
- 插入

  ```
  INSERT INTO <table_name> (col1, col2, col3, ...) VALUES (val1, val2, val3, ...);
  ```
  
- 删除

  ```
  DELETE FROM <table_name>
   WHERE <condition>;
  ```
  
- 修改

  ```
  UPDATE <table_name>
     SET <col_name> = <expression>
   WHERE <condition>;
  ```
  
