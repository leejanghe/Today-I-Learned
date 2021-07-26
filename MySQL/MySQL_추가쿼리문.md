## MySQL 추가쿼리문(알게된 내용)

스프린트 4,5 내용을 공부하면서 알게된 내용을 정리하였습니다.

---

## FOREIGN KEY() REFERENCES '연결테이블'(아이디)

이 쿼리문은 KEY옆에 소괄호에 현테이블 안에 있는 연결할 아이디와 REFERENCES에 있는 연결할 테이블의 아이디를 연결해줍니다.(스키마)

```
CREATE TABLE `user`(
    `id` int PRIMARY KEY AUTO_INCREMENT,
    ...생략
);

CREATE TABLE `content`(
    `id` int PRIMARY KEY AUTO_INCREMENT,
    ...생략
    `userId` int,
    FOREIGN KEY(`uesrId`) REFERENCES `user`(`id`)
);
```

<br />

## INNER JOIN 이어쓰기

INNER JOIN문은 연속으로 쓸수있으며 다양하게 관계를 맺을수 있습니다.

```
select title, body, created_at from content
    -> inner join content_category on content.id=content_category.contentId
    -> inner join category on content_category.categoryId=category.id
    -> where category.name='soccer';

    +-----------+--------------------------------+---------------------+
| title     | body                           | created_at          |
+-----------+--------------------------------+---------------------+
| soccer    | There are two heart in my body | 2021-07-26 15:23:51 |
| My Father | IS BOOM BOOM CHA               | 2021-07-26 15:23:51 |
+-----------+--------------------------------+---------------------+
2 rows in set (0.00 sec)
```

<br />

## 현 필드 이름 AS 변경할 필드 이름 

현 필드이름을 바꿔서 출력하고 싶으면 AS를 사용해서 대신할 필드 이름을 작성하면 됩니다.

```
select count(content.id) as ContentCount from content
    -> inner join user on user.id=content.userId
    -> where user.name='duRiCha';
+--------------+
| ContentCount |
+--------------+
|            1 |
+--------------+
1 row in set (0.00 sec)
```

count를 ContentCount 필드네임으로 대체합니다.

<br />


