## MySQL_part1_Quiz 풀기

기본적인 개념을 숙지한 상태라면 퀴즈는 그렇게 어렵지 않았습니다. 그나마 유용한 쿼리문을 정리하였습니다.

---

![](./image/sqlqz.png)

<br />

---

### Question 9_ LIKE

With SQL, how do you select all the records from a table named "Persons" where the value of the column "FirstName" starts with an "a"?

```
SELECT * FROM Persons WHERE FirstName LIKE 'a%'  
```

여기서 LIKE 'a%'의미는 FirstName이 a로 시작되는 모든 Persons을 선택하는 것입니다.

<br />

### Question 11_ AND

With SQL, how do you select all the records from a table named "Persons" where the "FirstName" is "Peter" and the "LastName" is "Jackson"?

```
SELECT * FROM Persons WHERE FirstName='Peter' AND LastName='Jackson'  
```

AND연산자는 a and b a,b둘다 해당하는 값 즉 성이 'Peter' 이고 이름이 'Jackson' 인 Persons 테이블에서 전체를 선택합니다.

<br />

### Question 12_ between and

With SQL, how do you select all the records from a table named "Persons" where the "LastName" is alphabetically between (and including) "Hansen" and "Pettersen"?

```
SELECT * FROM Persons WHERE LastName BETWEEN 'Hansen' AND 'Pettersen'  
```

between  A and B 는 A와 B사이에 있는 값을 의미합니다. 즉 'Hansen'와 'Pettersen' 사이에 있는 LastName을 Persons로 부터 전체 선택하라는 뜻입니다. 위에 And와 헷갈리면 안됩니다.

<br />

### Question 13_ DISTINCT

Which SQL statement is used to return only different values?

```
SELECT DISTINCT
```

DISTINCT는 중복을 막아주고 고유의 값을 출력합니다. 예를들어 1.미국 2.한국 3.중국 4.한국 5.미국 이라는 값이 있을 때 SELECT DISTINCT 사용하면 1.미국 2.한국 3.중국 값이 출력됩니다.

<br />

## Question 15_ ORDER BY  DESC 
With SQL, how can you return all the records from a table named "Persons" sorted descending by "FirstName"?

```
SELECT * FROM Persons ORDER BY FirstName DESC  
```

ORDER BY는 순서라고 생각하면 되고 DESC는 내림차순입니다. 즉 Persons테이블에서 FirstName 내림차순으로 전체 선택한다는 뜻입니다.

<br />

## Question 17_ INSERT INTO ...()VALUES()

With SQL, how can you insert "Olsen" as the "LastName" in the "Persons" table?

```
INSERT INTO Persons (LastName) VALUES ('Olsen')  
```

INSERT INTO VALUES문은 내용을 삽입할수 있게 도와줍니다. Persons테이블에 있는 LastName필드에 "Olsen" 작성하라는 뜻입니다.

<br />

## Question 18_ UPDATE SET WHERE

How can you change "Hansen" into "Nilsen" in the "LastName" column in the Persons table?

```
UPDATE Persons SET LastName='Nilsen' WHERE LastName='Hansen'  
```

UPDATE와 INSERT INTO 전혀 다른 개념입니다. UPDATE는 수정 개념으로 이해하면 됩니다. 즉 Persons테이블에 성을 'Hansen'에서 'Nilsen'으로 수정한다는 뜻입니다.

<br />

## Question 20_ COUNT

With SQL, how can you return the number of records in the "Persons" table?

```
SELECT COUNT(*) FROM Persons  
```

Persons테이블의 전체(목록) 수를 세줍니다 COUNT 말고도 SUM, AVG도 확인하면 좋습니다!

<br />

