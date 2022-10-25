mysql> create database NewMovies;
Query OK, 1 row affected (0.01 sec)

mysql> use NewMovies;
Database changed
mysql> create table moviesInTheatreNow(Title varchar(30) NOT NULL DEFAULT '',
-> Runtime int(10) unsigned NOT NULL DEFAULT 0,
-> Genre varchar(30) NOT NULL DEFAULT '',
-> IMDB_Score decimal(2,1) NOT NULL DEFAULT 9.9,
-> Rating char(5) NOT NULL DEFAULT '',
-> PRIMARY KEY (Title)
-> );
Query OK, 0 rows affected, 1 warning (0.06 sec)

mysql> describe moviesInTheatreNow;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| Title      | varchar(30)  | NO   | PRI |         |       |
| Runtime    | int unsigned | NO   |     | 0       |       |
| Genre      | varchar(30)  | NO   |     |         |       |
| IMDB_Score | decimal(2,1) | NO   |     | 9.9     |       |
| Rating     | char(5)      | NO   |     |         |       |
+------------+--------------+------+-----+---------+-------+
5 rows in set (0.01 sec)

mysql> INSERT INTO moviesInTheatreNow(Title, Runtime, Genre, IMDB_Score, Rating)
-> VALUES('Howard The Duck', 110, 'Sci-Fi', 4.6, 'PG'),
-> ('Lavalantula', 83, 'Horror', 4.7, 'TV-14'),
-> ('Starship Troopers', 129, 'Sci-Fi', 7.2, 'PG-13'),
-> ('Waltz With Bashir', 90, 'Documentary', 8.0, 'R'),
-> ('Spaceballs', 96, 'Comedy', 7.1, 'PG'),
-> ('Monsters Inc.', 92, 'Animation', 8.1, 'G');
Query OK, 6 rows affected (0.02 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM moviesInTheatreNow;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard The Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
+-------------------+---------+-------------+------------+--------+
6 rows in set (0.00 sec)

mysql> INSERT INTO moviesInTheatreNow(Title, Runtime, Genre, IMDB_Score, Rating)
-> VALUES('Scott Pilgrim Vs The World', 112, 'Comedy/Action', 7.5, 'PG-13');
Query OK, 1 row affected (0.01 sec)
mysql> INSERT INTO moviesInTheatreNow(Title, Runtime, Genre, IMDB_Score, Rating)
-> VALUES('Howls Moving Castle', 119, 'Animation', 9.0, 'PG');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM moviesInTheatreNow;
+----------------------------+---------+---------------+------------+--------+
| Title                      | Runtime | Genre         | IMDB_Score | Rating |
+----------------------------+---------+---------------+------------+--------+
| Howard The Duck            |     110 | Sci-Fi        |        4.6 | PG     |
| Howls Moving Castle        |     119 | Animation     |        9.0 | PG     |
| Lavalantula                |      83 | Horror        |        4.7 | TV-14  |
| Monsters Inc.              |      92 | Animation     |        8.1 | G      |
| Scott Pilgrim Vs The World |     112 | Comedy/Action |        7.5 | PG-13  |
| Spaceballs                 |      96 | Comedy        |        7.1 | PG     |
| Starship Troopers          |     129 | Sci-Fi        |        7.2 | PG-13  |
| Waltz With Bashir          |      90 | Documentary   |        8.0 | R      |
+----------------------------+---------+---------------+------------+--------+
8 rows in set (0.00 sec)

mysql> SELECT * FROM moviesInTheatreNow WHERE Genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| Title             | Runtime | Genre  | IMDB_Score | Rating |
+-------------------+---------+--------+------------+--------+
| Howard The Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
+-------------------+---------+--------+------------+--------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM moviesInTheatreNow WHERE IMDB_Score >6.5;
+----------------------------+---------+---------------+------------+--------+
| Title                      | Runtime | Genre         | IMDB_Score | Rating |
+----------------------------+---------+---------------+------------+--------+
| Howls Moving Castle        |     119 | Animation     |        9.0 | PG     |
| Monsters Inc.              |      92 | Animation     |        8.1 | G      |
| Scott Pilgrim Vs The World |     112 | Comedy/Action |        7.5 | PG-13  |
| Spaceballs                 |      96 | Comedy        |        7.1 | PG     |
| Starship Troopers          |     129 | Sci-Fi        |        7.2 | PG-13  |
| Waltz With Bashir          |      90 | Documentary   |        8.0 | R      |
+----------------------------+---------+---------------+------------+--------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM moviesInTheatreNow WHERE Runtime <100 AND RATING = 'G' OR Rating = 'PG';
+---------------------+---------+-----------+------------+--------+
| Title               | Runtime | Genre     | IMDB_Score | Rating |
+---------------------+---------+-----------+------------+--------+
| Howard The Duck     |     110 | Sci-Fi    |        4.6 | PG     |
| Howls Moving Castle |     119 | Animation |        9.0 | PG     |
| Monsters Inc.       |      92 | Animation |        8.1 | G      |
| Spaceballs          |      96 | Comedy    |        7.1 | PG     |
+---------------------+---------+-----------+------------+--------+
4 rows in set, 6 warnings (0.00 sec)

mysql> SELECT AVG(Runtime),Genre FROM moviesInTheatreNow WHERE IMDB_Score <7.5 GROUP BY Genre;
+--------------+--------+
| AVG(Runtime) | Genre  |
+--------------+--------+
|     119.5000 | Sci-Fi |
|      83.0000 | Horror |
|      96.0000 | Comedy |
+--------------+--------+

UPDATE moviesInTheatreNow
-> SET Rating = 'R'
-> WHERE Title = 'Starship Troopers';
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM moviesInTheatreNow;
+----------------------------+---------+---------------+------------+--------+
| Title                      | Runtime | Genre         | IMDB_Score | Rating |
+----------------------------+---------+---------------+------------+--------+
| Howard The Duck            |     110 | Sci-Fi        |        4.6 | PG     |
| Howls Moving Castle        |     119 | Animation     |        9.0 | PG     |
| Lavalantula                |      83 | Horror        |        4.7 | TV-14  |
| Monsters Inc.              |      92 | Animation     |        8.1 | G      |
| Scott Pilgrim Vs The World |     112 | Comedy/Action |        7.5 | PG-13  |
| Spaceballs                 |      96 | Comedy        |        7.1 | PG     |
| Starship Troopers          |     129 | Sci-Fi        |        7.2 | R      |
| Waltz With Bashir          |      90 | Documentary   |        8.0 | R      |
+----------------------------+---------+---------------+------------+--------+
8 rows in set (0.00 sec)


ALTER TABLE moviesInTheatreNow
-> ADD COLUMN ID int(10) unsigned NOT NULL DEFAULT 0;
Query OK, 0 rows affected, 1 warning (0.03 sec)

mysql> UPDATE moviesInTheatreNow
-> SET ID = '1'
-> WHERE Title = 'Howard The Duck';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '2'
-> WHERE Title = 'Lavalantula';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '3'
-> WHERE Title = 'Starship Troopers';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '4'
-> WHERE Title = 'Waltz With Bashir';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '5'
-> WHERE Title = 'Spaceballs';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '6'
-> WHERE Title = 'Monsters Inc.';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '7'
-> WHERE Title = 'Scott Pilgrim Vs The World';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE moviesInTheatreNow
-> SET ID = '8'
-> WHERE Title = 'Howls Moving Castle';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM moviesInTheatreNow;
+----------------------------+---------+---------------+------------+--------+----+
| Title                      | Runtime | Genre         | IMDB_Score | Rating | ID |
+----------------------------+---------+---------------+------------+--------+----+
| Howard The Duck            |     110 | Sci-Fi        |        4.6 | PG     |  1 |
| Howls Moving Castle        |     119 | Animation     |        9.0 | PG     |  8 |
| Lavalantula                |      83 | Horror        |        4.7 | TV-14  |  2 |
| Monsters Inc.              |      92 | Animation     |        8.1 | G      |  6 |
| Scott Pilgrim Vs The World |     112 | Comedy/Action |        7.5 | PG-13  |  7 |
| Spaceballs                 |      96 | Comedy        |        7.1 | PG     |  5 |
| Starship Troopers          |     129 | Sci-Fi        |        7.2 | R      |  3 |
| Waltz With Bashir          |      90 | Documentary   |        8.0 | R      |  4 |
+----------------------------+---------+---------------+------------+--------+----+
8 rows in set (0.00 sec)

mysql> SELECT ID,Rating FROM moviesInTheatreNow WHERE Genre = 'Horror' OR Genre = 'Documentary';
+----+--------+
| ID | Rating |
+----+--------+
|  2 | TV-14  |
|  4 | R      |
+----+--------+
2 rows in set (0.00 sec)

mysql> SELECT MIN(IMDB_Score) FROM moviesInTheatreNOW;
+-----------------+
| MIN(IMDB_Score) |
+-----------------+
|             4.6 |
+-----------------+
1 row in set (0.01 sec)

mysql> SELECT MAX(IMDB_Score) FROM moviesInTheatreNOW;
+-----------------+
| MAX(IMDB_Score) |
+-----------------+
|             9.0 |
+-----------------+
1 row in set (0.00 sec)

mysql> SELECT AVG(IMDB_Score) FROM moviesInTheatreNOW;
+-----------------+
| AVG(IMDB_Score) |
+-----------------+
|         7.02500 |
+-----------------+
1 row in set (0.00 sec)

SELECT MAX(IMDB_Score), AVG(IMDB_Score), MIN(IMDB_Score) FROM moviesInTheatreNow GROUP BY Rating HAVING COUNT(*)>1;
+-----------------+-----------------+-----------------+
| MAX(IMDB_Score) | AVG(IMDB_Score) | MIN(IMDB_Score) |
+-----------------+-----------------+-----------------+
|             9.0 |         6.90000 |             4.6 |
|             7.5 |         7.35000 |             7.2 |
+-----------------+-----------------+-----------------+
2 rows in set (0.00 sec)

mysql> DELETE FROM moviesInTheatreNow WHERE Rating = 'R';
Query OK, 2 rows affected (0.01 sec)

mysql> SELECT * FROM moviesInTheatreNow;
+----------------------------+---------+---------------+------------+--------+
| Title                      | Runtime | Genre         | IMDB_Score | Rating |
+----------------------------+---------+---------------+------------+--------+
| Howard The Duck            |     110 | Sci-Fi        |        4.6 | PG     |
| Howls Moving Castle        |     119 | Animation     |        9.0 | PG     |
| Lavalantula                |      83 | Horror        |        4.7 | TV-14  |
| Monsters Inc.              |      92 | Animation     |        8.1 | G      |
| Scott Pilgrim Vs The World |     112 | Comedy/Action |        7.5 | PG-13  |
| Spaceballs                 |      96 | Comedy        |        7.1 | PG     |
| Starship Troopers          |     129 | Sci-Fi        |        7.2 | PG-13  |
+----------------------------+---------+---------------+------------+--------+
7 rows in set (0.00 sec)

mysql> drop table moviesInTheatreNow;
Query OK, 0 rows affected (0.02 sec)

mysql> drop database NewMovies;
Query OK, 0 rows affected (0.02 sec)