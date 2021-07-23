# MySQL_기본 문법정리 #2 READ UPDATE DELETE

---

# SELECT 기본 문법

## SELECT * from 테이블이름

문법정리#1에 이어서 SELECT * 는 전체 정보를 선택해서 가져올수 있습니다.

```
mysql> select * from user;
+----+---------+-------------+---------------------+--------+-----------+
| id | title   | description | created             | author | profile   |
+----+---------+-------------+---------------------+--------+-----------+
|  1 | joy     | coding      | 2021-07-23 01:03:26 | jangh  | developer |
|  2 | happy   | coco        | 2021-07-23 01:05:18 | teemo  | developer |
|  3 | art     | cat         | 2021-07-23 01:46:20 | toto   | md        |
|  4 | love    | opa         | 2021-07-23 01:47:40 | puma   | teacher   |
|  5 | fashion | sexy        | 2021-07-23 01:49:15 | dior   | designer  |
+----+---------+-------------+---------------------+--------+-----------+
5 rows in set (0.00 sec)
```

<br />

## SELECT (원하는 Field) from 테이블이름

SELECT에서 원하는 값만 정보를 불러올수 있습니다. 예를들어 description과 profile을 제외한 field를 가져오려면 아래와 같습니다.

```
mysql> select id,title,created,author from user;
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  1 | joy     | 2021-07-23 01:03:26 | jangh  |
|  2 | happy   | 2021-07-23 01:05:18 | teemo  |
|  3 | art     | 2021-07-23 01:46:20 | toto   |
|  4 | love    | 2021-07-23 01:47:40 | puma   |
|  5 | fashion | 2021-07-23 01:49:15 | dior   |
+----+---------+---------------------+--------+
5 rows in set (0.00 sec)
```

<br />

## SELECT (원하는 Field) from 테이블이름 WHERE FIELD='해당정보'

추가적으로 WHERE옆에 field = '해당정보'를 입력하면 해당정보에 대한 세부적인 내용을 출력할수 있습니다. 예를들어 field는 title이고 title에서 'happy'라는 정보를 출력하고 싶을떄 아래와 같습니다.

```
mysql> select id,title,created,author from user where title='happy';
+----+-------+---------------------+--------+
| id | title | created             | author |
+----+-------+---------------------+--------+
|  2 | happy | 2021-07-23 01:05:18 | teemo  |
+----+-------+---------------------+--------+
1 row in set (0.00 sec)
```

<br />

## SELECT (원하는 Field) from 테이블이름 ORDER BY 기준(숫자,아이디) DESC;

OREDER BY id DESC;는 id값을 기준으로 정렬순서를 역전시킬수 있습니다(내림차순)

```
mysql> select id,title,created,author from user order by id desc;
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | fashion | 2021-07-23 01:49:15 | dior   |
|  4 | love    | 2021-07-23 01:47:40 | puma   |
|  3 | art     | 2021-07-23 01:46:20 | toto   |
|  2 | happy   | 2021-07-23 01:05:18 | teemo  |
|  1 | joy     | 2021-07-23 01:03:26 | jangh  |
+----+---------+---------------------+--------+
5 rows in set (0.00 sec)
```

만약에 여기서 내림차순 기준으로 3개의 데이터만 볼수있게 제한을 걸고 싶으면 옆에 `LIMIT 3;`을 입력하면 됩니다. (광범위한 데이터를 제한 걸어서 효율적으로 관리할수 있습니다.)

```
mysql> select id,title,created,author from user order by id desc limit 3;
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | fashion | 2021-07-23 01:49:15 | dior   |
|  4 | love    | 2021-07-23 01:47:40 | puma   |
|  3 | art     | 2021-07-23 01:46:20 | toto   |
+----+---------+---------------------+--------+
3 rows in set (0.00 sec)
```

<br />

## UPDATE 테이블 SET (원하는 Field) WHERE (아이디값)

UPDATE를 통해 해당 아이디에 있는 Field값을 수정할수 있습니다. 주의할점은 where문을 꼭!! 기입하기

```
mysql> update user set title='mysql',author='kakao' where id=2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from user;
+----+---------+-------------+---------------------+--------+-----------+
| id | title   | description | created             | author | profile   |
+----+---------+-------------+---------------------+--------+-----------+
|  1 | joy     | coding      | 2021-07-23 01:03:26 | jangh  | developer |
|  2 | mysql   | coco        | 2021-07-23 01:05:18 | kakao  | developer |
|  3 | art     | cat         | 2021-07-23 01:46:20 | toto   | md        |
|  4 | love    | opa         | 2021-07-23 01:47:40 | puma   | teacher   |
|  5 | fashion | sexy        | 2021-07-23 01:49:15 | dior   | designer  |
+----+---------+-------------+---------------------+--------+-----------+
5 rows in set (0.00 sec)
```

<br />

## DELETE from 테이블 WHERE (삭제하고싶은값)

delete는 from ... where 은 원치않은 값을 삭제할수 있습니다. 만약 위에 있는 테이블에서 id값이 3인 정보를 삭제하고 싶으면 아래와 같습니다.

```
mysql> delete from user where id=3;
Query OK, 1 row affected (0.00 sec)

mysql> select * from user;
+----+---------+-------------+---------------------+--------+-----------+
| id | title   | description | created             | author | profile   |
+----+---------+-------------+---------------------+--------+-----------+
|  1 | joy     | coding      | 2021-07-23 01:03:26 | jangh  | developer |
|  2 | mysql   | coco        | 2021-07-23 01:05:18 | kakao  | developer |
|  4 | love    | opa         | 2021-07-23 01:47:40 | puma   | teacher   |
|  5 | fashion | sexy        | 2021-07-23 01:49:15 | dior   | designer  |
+----+---------+-------------+---------------------+--------+-----------+
4 rows in set (0.00 sec)
```