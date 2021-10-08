# Project_dev #.3 (10/8)

---

## 1. 오늘 내가 한 일

깃 플로우 구축, 프로젝트 클라이언트 헤더 및 라우터 정리 완료

<br />

## 2. 내일 내가 할 일

렌딩페이지 파트1,2,3,4,5 footer, 로그인,페이지


<br />

## 3. 숙지 내용 및 알게 된 내용

오늘 pr과정에서 뻘짓을 하다 멘탈이 나갈뻔했다.. 아직 어색해서 나만의 깃 플로우 사전을 만들 필요가 있다고 느꼇다

<br />

### 3.1 Dev브런치 기반으로 작업할 브런치를 만들어 줍니다.

앞에 팀장이 한 일을 생략하고 팀원들이 할 일들

```
git switch -c local/landing-header
```

<br />

### 3.2 작업한 브런치에서 할 일을 완료하면 본인 깃 저장소에 푸쉬를 합니다.

```
git add .
git commit
git push origin local/landing-header
```

<br />

### 3.3 본인 레포에 들어와 작업한 브런치를 Upstream Dev브랜치로 P/R 하기.

본인 레포에 가면 P/R을 할 수 있는 노란색 창이 뜹니다. 그거 누르고 요청만 하기 (머지는 팀장이)

<br />

### 3.4 팀 내 코드 리뷰 후 작업 내역을 Merge 합니다.

<br />

### 3.5 P/R후 본인이 작업했던 브런치를 본인 데브와 병합 합니다.

```
git switch dev
git merge local/landing-header
git push origin dev
```

<br />

### 3.6 Merge 된 내역으로 본인 로컬 최신화합니다.

(리무트 설정이 안된 경우까지 생각해서) 

```
git remote -v
git remote add {작명} https://github.com/codestates/Moa-Link.git
git remote -v
git pull {작명} dev
git push origin dev
```

1~6 반복 작업 합니다.

<br />

## 4. 느낌..

SR기획 단계에서 너무 많이 힘을 뻇고 너무 정신 없었다... 그래도 아직 피드백이 남았지만 조금은 후련하다... 이제 코드에 집중 할 수 있는 시간이 생겻다! 내일부터 엄청 달려야 겠다!! 멘탈 다시 잡고 시작해야겠다!!