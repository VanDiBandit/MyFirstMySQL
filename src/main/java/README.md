mysql> show tables;
+----------------------+
| Tables_in_homework12 |
+----------------------+
| movies               |
+----------------------+
1 row in set (0.01 sec)

mysql> describe movies;
+----------+--------------+------+-----+---------+----------------+
| Field    | Type         | Null | Key | Default | Extra          |
+----------+--------------+------+-----+---------+----------------+
| id       | int unsigned | NO   | PRI | NULL    | auto_increment |
| title    | varchar(20)  | NO   |     |         |                |
| genre    | varchar(100) | NO   |     |         |                |
| duration | int unsigned | NO   |     | 0       |                |
+----------+--------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)

mysql> SELECT * FROM movies;
+----+---------------+-----------+----------+
| id | title         | genre     | duration |
+----+---------------+-----------+----------+
|  1 | Metropolis    | Sci-Fi    |      153 |
|  2 | Nosferatu     | Horror    |       94 |
|  3 | The Kid       | Comedy    |       68 |
|  4 | The Gold Rush | Adventure |       95 |
+----+---------------+-----------+----------+
4 rows in set (0.00 sec)