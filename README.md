# joins_and_unions

Microsoft Windows [Version 10.0.22621.2070]
(c) Microsoft Corporation. All rights reserved.

C:\Users\lagad>cd/

C:\>cd xampp\mysql\bin

C:\xampp\mysql\bin>mysql.exe -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.4.28-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| phpmyadmin         |
| student            |
| test               |
+--------------------+
6 rows in set (0.001 sec)

MariaDB [(none)]> use student;
Database changed
MariaDB [student]> show tables;
+-------------------+
| Tables_in_student |
+-------------------+
| customer_info     |
| data              |
| event_a           |
| event_b           |
| info              |
| sales             |
+-------------------+
6 rows in set (0.001 sec)

MariaDB [student]> desc event_a;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| surname | varchar(10) | YES  |     | NULL    |       |
| city    | varchar(20) | YES  |     | NULL    |       |
| phone   | int(50)     | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
3 rows in set (0.005 sec)

MariaDB [student]> select * from event_a;
+------------+-----------+------------+
| surname    | city      | phone      |
+------------+-----------+------------+
| kurangi    | darsi     | 2147483647 |
| ajmeera    | guntur    | 2147483647 |
| lagadapati | vinukonda | 2147483647 |
+------------+-----------+------------+
3 rows in set (0.000 sec)

MariaDB [student]> select * from event_b;
+---------+----------+------------+
| surname | city     | phone      |
+---------+----------+------------+
| susan   | jersey   |   50855548 |
| miller  | hamilton |   71355589 |
| larry   | norway   |  617558693 |
| kuarngi | darsi    | 2147483647 |
+---------+----------+------------+
4 rows in set (0.000 sec)

MariaDB [student]> insert into event_b values('king','dehradun',8973489);
Query OK, 1 row affected (0.005 sec)

MariaDB [student]> select * from event_b;
+---------+----------+------------+
| surname | city     | phone      |
+---------+----------+------------+
| susan   | jersey   |   50855548 |
| miller  | hamilton |   71355589 |
| larry   | norway   |  617558693 |
| kuarngi | darsi    | 2147483647 |
| king    | dehradun |    8973489 |
+---------+----------+------------+
5 rows in set (0.000 sec)

MariaDB [student]> delete from event_b where phone=2147483647;
Query OK, 1 row affected (0.005 sec)


MariaDB [student]> select * from event_a;
+------------+-----------+------------+
| surname    | city      | phone      |
+------------+-----------+------------+
| kurangi    | darsi     | 2147483647 |
| ajmeera    | guntur    | 2147483647 |
| lagadapati | vinukonda | 2147483647 |
| king       | dehradun  |    8973489 |
+------------+-----------+------------+
4 rows in set (0.000 sec)

MariaDB [student]> select * from event_b;
+---------+----------+-----------+
| surname | city     | phone     |
+---------+----------+-----------+
| susan   | jersey   |  50855548 |
| miller  | hamilton |  71355589 |
| larry   | norway   | 617558693 |
| king    | dehradun |   8973489 |
+---------+----------+-----------+
4 rows in set (0.000 sec)

MariaDB [student]> select * from event_a union select * from event_b;
+------------+-----------+------------+
| surname    | city      | phone      |
+------------+-----------+------------+
| kurangi    | darsi     | 2147483647 |
| ajmeera    | guntur    | 2147483647 |
| lagadapati | vinukonda | 2147483647 |
| king       | dehradun  |    8973489 |
| susan      | jersey    |   50855548 |
| miller     | hamilton  |   71355589 |
| larry      | norway    |  617558693 |
+------------+-----------+------------+
7 rows in set (0.000 sec)

MariaDB [student]> select * from event_a where event_a.surname in (select event_b.surname from event_b);
+---------+----------+---------+
| surname | city     | phone   |
+---------+----------+---------+
| king    | dehradun | 8973489 |
+---------+----------+---------+
1 row in set (0.003 sec)

MariaDB [student]> select * from event_a where event_a.phone in (select event_b.phone from event_b);
+---------+----------+---------+
| surname | city     | phone   |
+---------+----------+---------+
| king    | dehradun | 8973489 |
+---------+----------+---------+
1 row in set (0.001 sec)

MariaDB [student]> CREATE TABLE Customer (cust_id INT, cust_name VARCHAR(20), contact_name VARCHAR(20), city  VARCHAR(10), telephone VARCHAR(10));
Query OK, 0 rows affected (0.019 sec)                                                                                          
MariaDB [student]> insert into customer values(101, "Oliver", "Joy", "New York", 2016776708), (102,"George", "George", "Chicago" , "209761700"), (103,"Harry", "Harry", "Texas" , "2097617866"), (104,"Jack", "Noah", "California", "2097627999");
Query OK, 4 rows affected (0.005 sec)
Records: 4  Duplicates: 0  Warnings: 0

MariaDB [student]> select * from Customer;
+---------+-----------+--------------+------------+------------+
| cust_id | cust_name | contact_name | city       | telephone  |
+---------+-----------+--------------+------------+------------+
|     101 | Oliver    | Joy          | New York   | 2016776708 |
|     102 | George    | George       | Chicago    | 209761700  |
|     103 | Harry     | Harry        | Texas      | 2097617866 |
|     104 | Jack      | Noah         | California | 2097627999 |
+---------+-----------+--------------+------------+------------+
4 rows in set (0.000 sec)

MariaDB [student]> CREATE TABLE Orders (cust_id INT, order_id INT, order_date varchar(20), shipper_id varchar(20));
Query OK, 0 rows affected (0.023 sec)

MariaDB [student]> INSERT INTO Orders VALUES (101, 4501, '12/03/1997', 'A111' ), (102, 4502, '13/03/1997', 'A112'), (103, 4503, '14/03/1997', 'A113'), (105, 4505, '16/03/1997', 'A115'), (106, 4506, '17/03/1997', 'A116');
Query OK, 5 rows affected (0.009 sec)
Records: 5  Duplicates: 0  Warnings: 0

MariaDB [student]> select * from orders;
+---------+----------+------------+------------+
| cust_id | order_id | order_date | shipper_id |
+---------+----------+------------+------------+
|     101 |     4501 | 12/03/1997 | A111       |
|     102 |     4502 | 13/03/1997 | A112       |
|     103 |     4503 | 14/03/1997 | A113       |
|     105 |     4505 | 16/03/1997 | A115       |
|     106 |     4506 | 17/03/1997 | A116       |
+---------+----------+------------+------------+
5 rows in set (0.000 sec)

MariaDB [student]> select cust.cust_id,cust.cust_name,cust.contact_name,cust.city,cust.telephone,ord.order_id,ord.shipper_id from customer as cust inner join orders as ord on cust.cust_id = ord.cust_id;
+---------+-----------+--------------+----------+------------+----------+------------+
| cust_id | cust_name | contact_name | city     | telephone  | order_id | shipper_id |
+---------+-----------+--------------+----------+------------+----------+------------+
|     101 | Oliver    | Joy          | New York | 2016776708 |     4501 | A111       |
|     102 | George    | George       | Chicago  | 209761700  |     4502 | A112       |
|     103 | Harry     | Harry        | Texas    | 2097617866 |     4503 | A113       |
+---------+-----------+--------------+----------+------------+----------+------------+
3 rows in set (0.002 sec)

MariaDB [student]> select cust.cust_id,cust.cust_name,cust.contact_name,cust.city,cust.telephone,ord.order_id,ord.shipper_id from customer as cust right join orders as ord on cust.cust_id = ord.cust_id;
+---------+-----------+--------------+----------+------------+----------+------------+
| cust_id | cust_name | contact_name | city     | telephone  | order_id | shipper_id |
+---------+-----------+--------------+----------+------------+----------+------------+
|     101 | Oliver    | Joy          | New York | 2016776708 |     4501 | A111       |
|     102 | George    | George       | Chicago  | 209761700  |     4502 | A112       |
|     103 | Harry     | Harry        | Texas    | 2097617866 |     4503 | A113       |
|    NULL | NULL      | NULL         | NULL     | NULL       |     4505 | A115       |
|    NULL | NULL      | NULL         | NULL     | NULL       |     4506 | A116       |
+---------+-----------+--------------+----------+------------+----------+------------+
5 rows in set (0.001 sec)

MariaDB [student]> select cust.cust_id,cust.cust_name,cust.contact_name,cust.city,cust.telephone,ord.order_id,ord.shipper_id from customer as cust left join orders as ord on cust.cust_id = ord.cust_id;
+---------+-----------+--------------+------------+------------+----------+------------+
| cust_id | cust_name | contact_name | city       | telephone  | order_id | shipper_id |
+---------+-----------+--------------+------------+------------+----------+------------+
|     101 | Oliver    | Joy          | New York   | 2016776708 |     4501 | A111       |
|     102 | George    | George       | Chicago    | 209761700  |     4502 | A112       |
|     103 | Harry     | Harry        | Texas      | 2097617866 |     4503 | A113       |
|     104 | Jack      | Noah         | California | 2097627999 |     NULL | NULL       |
+---------+-----------+--------------+------------+------------+----------+------------+
4 rows in set (0.001 sec)

MariaDB [student]> select cust.cust_id,cust.cust_name,cust.contact_name,cust.city,cust.telephone,ord.order_id,ord.shipper_id from customer as cust left join orders as ord on cust.cust_id = ord.cust_id union select cust.cust_id,cust.cust_name,cust.contact_name,cust.city,cust.telephone,ord.order_id,ord.shipper_id from customer as cust right join orders as ord on cust.cust_id = ord.cust_id;
+---------+-----------+--------------+------------+------------+----------+------------+
| cust_id | cust_name | contact_name | city       | telephone  | order_id | shipper_id |
+---------+-----------+--------------+------------+------------+----------+------------+
|     101 | Oliver    | Joy          | New York   | 2016776708 |     4501 | A111       |
|     102 | George    | George       | Chicago    | 209761700  |     4502 | A112       |
|     103 | Harry     | Harry        | Texas      | 2097617866 |     4503 | A113       |
|     104 | Jack      | Noah         | California | 2097627999 |     NULL | NULL       |
|    NULL | NULL      | NULL         | NULL       | NULL       |     4505 | A115       |
|    NULL | NULL      | NULL         | NULL       | NULL       |     4506 | A116       |
+---------+-----------+--------------+------------+------------+----------+------------+
6 rows in set (0.001 sec)

MariaDB [student]> show tables;
+-------------------+
| Tables_in_student |
+-------------------+
| customer          |
| customer_info     |
| data              |
| event_a           |
| event_b           |
| info              |
| orders            |
| sales             |
+-------------------+
8 rows in set (0.001 sec)

MariaDB [student]> create table employee(Name varchar(20), Age int, City varchar(20), Salary int);
Query OK, 0 rows affected (0.027 sec)

MariaDB [student]> insert into employee values('ravi',15,'chennai',56000),('Sara', 30, 'California', 67000), ('Allen', 29, 'New York', 45000), ('John',45, 'Texas', 55000);
Query OK, 4 rows affected (0.009 sec)
Records: 4  Duplicates: 0  Warnings: 0

MariaDB [student]> select * from employee;
+-------+------+------------+--------+
| Name  | Age  | City       | Salary |
+-------+------+------------+--------+
| ravi  |   15 | chennai    |  56000 |
| Sara  |   30 | California |  67000 |
| Allen |   29 | New York   |  45000 |
| John  |   45 | Texas      |  55000 |
+-------+------+------------+--------+
4 rows in set (0.000 sec)

MariaDB [student]> insert into employee values('Sai',15,'chennai',56000);
Query OK, 1 row affected (0.006 sec)

MariaDB [student]> select * from employee;
+-------+------+------------+--------+
| Name  | Age  | City       | Salary |
+-------+------+------------+--------+
| ravi  |   15 | chennai    |  56000 |
| Sara  |   30 | California |  67000 |
| Allen |   29 | New York   |  45000 |
| John  |   45 | Texas      |  55000 |
| Sai   |   15 | chennai    |  56000 |
+-------+------+------------+--------+
5 rows in set (0.000 sec)

MariaDB [student]> SELECT DISTINCT b.Name, b.Age, b.City, b.Salary FROM employee AS a, employee AS b WHERE a.City = b.City   and a.Salary > 50000;
+------+------+------------+--------+
| Name | Age  | City       | Salary |
+------+------+------------+--------+
| ravi |   15 | chennai    |  56000 |
| Sara |   30 | California |  67000 |
| John |   45 | Texas      |  55000 |
| Sai  |   15 | chennai    |  56000 |
+------+------+------------+--------+
4 rows in set (0.001 sec)

MariaDB [student]> SELECT DISTINCT b.Name, b.Age, b.City, b.Salary FROM employee AS a, employee AS b WHERE a.City = b.City   and a.Salary > 60000;
+------+------+------------+--------+
| Name | Age  | City       | Salary |
+------+------+------------+--------+
| Sara |   30 | California |  67000 |
+------+------+------------+--------+
1 row in set (0.001 sec)
