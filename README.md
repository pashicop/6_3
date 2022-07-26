# 6_3
## 1
Версия БД: `Server version:         8.0.29 MySQL Community Server - GPL`  
Кол-во записей -- 1: 
```
mysql> select count(*) from orders where price > 300;
+----------+
| count(*) |
+----------+
|        1 |
+----------+
1 row in set (0.01 sec)
```
## 2
```
mysql> select * from INFORMATION_SCHEMA.USER_ATTRIBUTES where user = 'test';
+------+-----------+---------------------------------------+
| USER | HOST      | ATTRIBUTE                             |
+------+-----------+---------------------------------------+
| test | localhost | {"fname": "James", "lname": "PRETTY"} |
+------+-----------+---------------------------------------+
1 row in set (0.01 sec)
```
## 3
```
mysql> SELECT TABLE_NAME, ENGINE FROM information_schema. TABLES where TABLE_SCHEMA = 'test_db';
+------------+--------+
| TABLE_NAME | ENGINE |
+------------+--------+
| orders     | InnoDB |
+------------+--------+
1 row in set (0.00 sec)
```
Время выполнения изменения движка:   
На MyISAM -- 0.02402775  
На InnoDB -- 0.02792750  
## 4
Подключил volume в docker-compose.yml `- ./config2:/etc/mysql/conf.d` с конфигурацией в файле my.cnf:
```
[mysqld]
innodb_flush_log_at_trx_commit = 0
# innodb_file_format = Barracuda
innodb_log_buffer_size = 1M
innodb_buffer_pool_size = 1800M
max_binlog_size = 100M
```
По пункту `Нужна компрессия таблиц для экономии места на диске` как я понял раньше использовалась переменная `innodb_file_format = Barracuda`, но в mysql 8 она была удалена [link на release notes](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-0.html)
 
