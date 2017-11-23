# Django Blog Application

## 소개
해당 샘플 앱은 도커로 (nginx / backend / frontend) 이미지 및 컨테이너가 자동 생성 됩니다.
설치를 완료하면 다음과 같이 도커 이미지와 컨테이너를 확인 할 수 있습니다.

## 데이터 베이스 초기 설정
- default DatabaseName: blog
```
$ create database blog;
```

## 애플리케이션 서버 띄우기 - 도커 활용
- 코드 받기
```
$ git clone git@github.com:whatapdev/python-django-blog.git
```

- docker-compose 실행(foregrdoun로 동작함)
```
$ docker-compose up
```

- docker compose가 실행 되지 않는다면?
```
하단 참조
```

- docker container 실행(새로운 탭)
```
$ docker exec -i -t backend /bin/bash
```

- 데이터 베이스 설정 변경
```
파일: ~/django-blog/backend/backend/settings.py
에서 다음 데이터 베이스 설정을 변경한다.
        'HOST': 'DB Server IP',
        'NAME': 'blog',
        'PASSWORD': 'pass'

ex)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': '127.0.0.1',
        'NAME': 'blog',
        'USER': 'root',
        'PASSWORD': 'pass'
    },
}
```

- 데이터 베이스 마이그레이트
```
$ python3.5 manage.py migrate
```

- 기본 사용자 생성
```
$ python3.5 manage.py createsuperuser
```

- 도메인 설정
```
파일: /etc/hosts
에 다음 내용을 추가한다.


[FRONT_END_SERVER_IP]    api.[FRONT_END_SERVER_IP]

예)
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost

210.122.2.85    api.210.122.2.85

```

- 웹 접속(브라우저에서 확인)
```
http://[FRONT_END_SERVER_IP]/
```

- 와탭 에이전트 실
```
whatap agent를 미리 설정 해 두었습니다.
WHATAP_HOME: /home/blog/backend/whatap

다음 위치에서 설정 내용을 확인 할 수 있습니다.
파일: /etc/supervisor/conf.d/supervisor.conf

수집서버 주소와 라이센스 키를 변경하고자 하는 경우 다음 파일을 변경하세요.
파일: /home/blog/backend/whatap/whatap.conf
```

## 도커 이미지 및 컨테이너 확인
- docker 이미지 확인
```
$ docker images
```

- docker 컨테이너 확인
```
$ docker ps -a
```

## 도커 파이썬 환경
- python version: 3.5

## 데이터 베이스 환경
- postgresq versionl: 9.3.17
```
$ psql --version
```

## 문제 해결

### docker compose가 실행 되지 않는다면?

#### 설치
```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
#### 권한
```
$ sudo chmod +x /usr/local/bin/docker-compose
```
#### 버전 확인
```
$ docker-compose --version
```




## 참고
해당 애플리케이션은 다음을 참고 하였습니다
https://github.com/raymestalez/django-react-blog

