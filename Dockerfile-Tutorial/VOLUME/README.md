# Dockerfile에서 VOLUME 사용하기

## 사용 예시

ex) VOLUME vol1
<br/>
ex) VOLUME ["vol1", "vo12"]

<br/>

## docker run에 대한 결과

ex) VOLUME vo1
<br/>
: 호스트에 자동으로 volume 1개가 생기고(volume 이름은 랜덤으로 생성된다) 컨테이너의 root 경로에 "vol1"이라는 폴더(volume)와 마운트가 된다.

<br/>

## 사용 확장 예시

image1's Dockerfile

```
FROM ubuntu:20.04

VOLUME vol1
```

```
docker -t volume-test .
docker run -it --name volume-image-1 volume-test /bin/bash

// volume-image-1 container 진입
cd vol1
touch test.txt

ctrl+P + ctrl+Q
// container에서 빠져 나온다

docker run -it -volumes-from volume-image-1 --name volume-image-2 ubuntu:20.04 /bin/bash

// volume-image-2 container 진입
cd vol1
```

해당 경로는 이미 마운트가 되어 있어 test.txt 파일이 존재한다.
