# Project_dev #.1

---

## 1. 오늘 내가 한 일

SR 계획 세우기, 기능 todolist 구체화 하기, 계획 스케줄표 만들기

<br />

## 2. 내일 내가 할 일

환경셋팅후 팀원들 레포 제공, 전반적인 SR계획 마무리, 팀룰 설정, wiki정리 


<br />

## 3. 숙지 내용

![](./img/git.png)

<br />

![](./img/flow.png)

<br />

내일 배포를 하기 위해서 팀원들에게 레포를 전달해야 한다. 그전에 UpStream에서 포크가 아닌 클론을 받고 데브 브런치를 하나 생성하고 거기 안에서 서버와 클라 폴더를 만들어서 필요한 환경 셋팅을 다하고 다시 UpStream에다 Merge하는 작업을 하면 된다. 이 작업이 완료가 되면 팀원들에게 공지해서 포크 받을수 있도록 해야하고! 추가적으로 무조건 데브 브런치 기반으로 피쳐브런치에서 기능 구현을 하면 될것 같다. 그리고 머지할 경우는 무조건 팀원들에게 공유를 해야 하는것도 잊지 않아야 겠다!

<br />

## 4. Project Git Flow

### 1. 부여된 레포를 깃 클론을 한다 (포크 금지)

### 2. 클론한 폴더에 들어가서 초기화 작업을 한다.

```
echo "# Moa-Link" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/codestates/Moa-Link.git
git push -u origin master
```

<br />

### 3. 레포가 잘만들어 졌는지 확인 후 dev 브런치 만들기

```
git switch -c dev
```

<br />

### 4. dev브런치에서 클라, 서버만들고 환경셋팅 하기

```
npm create-react-app client
cd client 하고 설치하기
```

서버는 폴더 하나 만들어서 파일하나 만들고 시작

```
cd server
npm init
```

세팅 다하고 깃이그노어 설정 및 env파일 미리 만들기

<br />

### 5. 환경셋팅 끝나면 레포에 푸쉬하기

```
git switch dev
git add .
git commit -m "Start Project"
git push -u origin dev
```

<br />

### 6. 팀원 초대하고 포크해서 개별 프로젝트 진행

주의 할점!! 마스터 브런치가 아닌 데브 브런치로 진행

<br />

## 5. 느낌..

많은걸 하려고 하는것 보단 여태 배운 내용을 복습한다라는 생각으로 기본에 충실 할 수 있도록 해야 겠다. 분명히 시간안에 완벽에 가깝게 구현하기에는 다소 무리가 있다...개발을 하다보면 무수한 시행착오가 있을 것이다...어떻게 극복할지 막막하지만 시행착오를 겪으면서 성장하는 계기가 되었으면 한다!! 개발자가 되기 위한 과정이니 천천히 할 수 있는것부터 진행해보자!