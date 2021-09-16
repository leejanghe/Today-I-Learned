# AWS배포 과정_데이터베이스

---

# RDS 인스턴스 생성

aws RDS에 들어가서 데이터 베이스를 생성합니다.  

<br />

### 체크사항

1. 엔진 옵션 - MySQL
2. 템플릿 - 프리티어

3. 설정
3-1 db인스턴스 식별자 - 작명  
3-2 마스터 암호 - 꼭 기억하기  

4. 연결옵션에서 "퍼블릭 엑세스 가능" 예 선택하고 밑에 추가 구성에서 데이터베이스 포트를 13306으로 설정합니다.

5. 추가 구성에서 데이터 베이스 옵션에서 초기이름을 test로 적고 데이터베이스 생성을 합니다.

<br />

## ec2 서버 env 파일 변경하기

```
mv .env.example .env
nano .env
```

nano에서 아래 정보를 수정합니다.

```
DATABASE_HOST=엔드포인트 주소
DATABASE_USER=admin
DATABASE_PASSWORD=아까만든 데이터베이스 비번
DATABASE_PORT=13306
```

<br />

## test하기

ec2에서 sudo npm start를 하고 실행이 잘되는지 확인합니다.

![](./image/data.png)