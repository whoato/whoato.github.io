---
published: false
layout: post
author: me
title: 키비 빌드 환경 설정
category:
  - Kivy
---
# Kivy Android Build 환경 구성

## Ubuntu 20.04로 진행

~build를 위한 피나는 노력~

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
```

## Anaconda 설치

[install](https://www.anaconda.com/products/individual)<br>
[hash](https://docs.anaconda.com/anaconda/install/hashes/all/)

linux installer를 설치한 후 데이터 무결성 확인
```
$ sha256sum <sh파일이름>.sh
// hash 값이 같은지 확인
$ bash <sh파일이름>.sh
// 모두 yes
$ source ~/.bashrc
$ conda info
```

## buildozer 설치

[링크 참조](https://buildozer.readthedocs.io/en/latest/installation.html)

#### add the following line at the end of your ~/.bashrc file

```
$ gedit ~/.bashrc
```

맨 마지막 줄에 export PATH=$PATH:~/.local/bin/ 추가

## Conda 가상환경 설정

### 가상환경 생성

최신버전 python으로 진행하지 말 것.

높은 확률로 다음과 같은 에러를 뿜어냄

```
failed with initial frozen solve. Retrying with flexible solve.
```

최신버전 python은 dependency 문제가 생길 수 있다.

따라서 한단계 낮은 버전의 새 환경을 생성해 진행해야 한다.

```
$ conda create -n <env_name> python=3.7
$ conda activate <env_name>
(<env_name>) $
```

### kivy 설치

```
(<env_name>) $ conda install -c conda-forge kivy
```

### opencv 설치

```
(<env_name>) $ conda install -c conda-forge opencv
```

### tensorflow 설치

```
(<env_name>) $ conda install -c conda-forge tensorflow
```

이렇게 하면 또 frozen 에러를 뿜어낸다

개같은거

키비도 빌도저처럼 가상환경 밖에 설치해야 하나봄

### etc - Conda 가상환경 삭제 

```
$ conda remove -n <env_name> --all
```


[다른 방법](https://www.youtube.com/watch?v=Pi510YawopE)
[또 다른 방법](https://noel-embedded.tistory.com/914)
