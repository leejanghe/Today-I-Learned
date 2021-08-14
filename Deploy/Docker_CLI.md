# Docker CLI

---

## 도커 이미지 구분

도커 이미지를 읽을때 레지스트리, 레포지토리, 태그로 구성되어 있습니다.

```
레지스트리/레포지토리:테그
```

1. 레지스트리 (Registry)
- 도커 이미지를 관리하는 공간입니다.
- 특별히 다른 것으 지정하지 않는다면, 도크 허브를 기본 레지스트리로 설정합니다.
- 레지스트리는 Docker Hub, Private Docker Hub, 회사 내부용 레지스트리 등으로 나뉠 수 있습니다.

2. 레포지토리 (Repository)
- 레지스트리 내에 도커 이미지가 저장되는 공간입니다.
- 이미지 이름이 사용되기도 합니다.
- 깃헙의 레포지토리와 유사합니다

3. 태그(Tag)
- 같은 이미지라고 할지라도 버전 별로 안의 내용이 다를수 있습니다.
- 해당 이미지를 설명하는 버전 정보를 주로 입력합니다.
- 특별히 다른 것을 지정하지 않는다면 `latest`태그를 붙인 이미지를 가져옵니다.

---

# Docker 명령어

## 이미지 가져오기

```
$ docker image pull docker/whalesay:latest
```

{image} pull : 레지스트리에서 이미지 혹은 레포지토리를 가져옵니다(pull)

<br />

## 이미지 조회 및 용량 확인

```
$ docker image ls
```

이미지를 조회 할수 있습니다.

<br />

## 이미지 삭제

```
$ docker image rm docker/whalesay
```

<br />

## 컨테이너 실행

```
$ docker container run --name 컨테이너_이름 docker/whalesay:latest cowsay boo
```

`docker container run`는 컨테이너를 실행할수 있습니다.

<br />

## 컨테이너 리스트 조회

```
$ docker container ps -a
```

{container} ps : 컨테이너의 리스트를 출력합니다.  
-a : Default 로는 실행되는 컨테이너지만 종료된 컨테이너를 포함하여 모든 컨테이너를 출력합니다.

<br />

## 컨테이너 삭제

```
$ docker container rm 컨테이너_이름
```

{container} rm : 컨테이너를 지칭해서 삭제합니다. 컨테이너를 명시할 때는 ps 명령을 통해 확인할 수 있는 NAMES 혹은 CONTAINER ID 를 사용합니다.

<br />

## 컨테이너 종료

container는 ctrl + c 로 종료할 수 있습니다.


---

## 정리

```js
// 도커 이미지 목록을 확인한다.
sudo docker images // 또는 sudo docker image ls 

// Option1 : 컨테이너 삭제 후 도커 이미지 삭제
sudo docker ps -a
sudo docker stop 컨테이너ID // 실행 중이라면 컨테이너 실행을 중지시킨다.
sudo docker rm 컨테이너ID 
sudo docker rmi 이미지ID

// Option2 : 컨테이너 상관없이 도커 이미지 삭제 
sudo docker rmi -f 이미지ID
```