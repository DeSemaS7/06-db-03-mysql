### Задача 1


\s
Server version:         8.0.24 MySQL Community Server - GPL

mysql> select COUNT(*) from orders where price > 300;

| COUNT(*) |
|----------|
| 1        |

1 row in set (0.00 sec)

### Задача 2



CREATE USER 'test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'test-pass';

ALTER USER 'test'@'localhost' WITH MAX_QUERIES_PER_HOUR 100;

ALTER USER 'test'@'localhost'
  PASSWORD EXPIRE INTERVAL 180 DAY
  FAILED_LOGIN_ATTEMPTS 3;
  
ALTER USER 'test'@'localhost' ATTRIBUTE '{"Surname":"Pretty", "Name":"James"}';

GRANT SELECT ON test_db.* TO 'test'@'localhost';

<br>

mysql> SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';

| USER | HOST      | ATTRIBUTE                              |
|------|-----------|----------------------------------------|
| test | localhost | {"Name": "James", "Surname": "Pretty"} |

1 row in set (0.00 sec)

### Задача 3

SELECT TABLE_NAME, ENGINE FROM information_schema.TABLES where TABLE_SCHEMA = 'test_db';


| TABLE_NAME | ENGINE |
|------------|--------|
| orders     | InnoDB |

1 row in set (0.00 sec)


<br>
SHOW PROFILES;

| Query_ID | Duration   | Query                              |
|----------|------------|------------------------------------|
| 7        | 0.05646300 | ALTER TABLE orders ENGINE = MyISAM |
| 8        | 0.06214275 | ALTER TABLE orders ENGINE = InnoDB |

### Задача 4

[mysqld]
innodb_file_per_table
innodb-compression-level = 9
innodb-flush-method = O_DSYNC
innodb-io-capacity = 2000
innodb-io-capacity-max = 2500
innodb_log_file_size = 100M
innodb_buffer_pool_size = 4G


 
