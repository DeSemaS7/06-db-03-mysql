# 06-db-03-mysql



docker run -e MYSQL_ROOT_PASSWORD=mysql -v /tmp/mysql:/var/lib/mysql -p 3306:3306 -d mysql:8

mysql> create database test_db;

mysqldump -p test_db < /var/lib/mysql/test_dump.sql
\s
Server version:         8.0.24 MySQL Community Server - GPL


mysql> select * from orders where price > 300;
+----+----------------+-------+
| id | title          | price |
+----+----------------+-------+
|  2 | My little pony |   500 |
+----+----------------+-------+
1 row in set (0.00 sec)


_______________________________________________________________________________


CREATE USER 'test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'test-pass';

ALTER USER 'test'@'localhost' WITH MAX_QUERIES_PER_HOUR 100;

ALTER USER 'test'@'localhost'
  PASSWORD EXPIRE INTERVAL 180 DAY
  FAILED_LOGIN_ATTEMPTS 3;
  
ALTER USER 'test'@'localhost' ATTRIBUTE '{"Surname":"Pretty", "Name":"James"}';

GRANT SELECT ON test_db.* TO 'test'@'localhost';

SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';



mysql> SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';
+------+-----------+----------------------------------------+
| USER | HOST      | ATTRIBUTE                              |
+------+-----------+----------------------------------------+
| test | localhost | {"Name": "James", "Surname": "Pretty"} |
+------+-----------+----------------------------------------+
1 row in set (0.00 sec)

_______________________________________________________________________________



SELECT TABLE_NAME, ENGINE FROM information_schema.TABLES where TABLE_SCHEMA = 'test_db';


ALTER TABLE orders ENGINE = MyISAM;

SHOW PROFILES;

ALTER TABLE orders ENGINE = InnoDB;

  Query_ID | Duration   | Query
  
 7 | 0.05646300 | ALTER TABLE orders ENGINE = MyISAM
 10 | 0.06214275 | ALTER TABLE orders ENGINE = InnoDB
 
_______________________________________________________________________________
 
