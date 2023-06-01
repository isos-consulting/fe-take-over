# 사내 웹 서버 구성
![사내 웹 서버 구성도](https://github.com/isos-consulting/feto/assets/49608580/a48b3c94-12ad-4242-82c5-d17e81d0d9b6)

## 서버 정보
모든 서버는 같은 운영체제 버전을(`ubuntu18.04_amd64`) 사용 중임
``` json
[
   {
      "name":"dms-server",
      "username":"isos",
      "ip":"191.1.70.192",
      "용도":"문서관리 시스템 개발 확인용 웹서버",
      "웹 서버 포트":8080
   },
   {
      "name":"isos-server",
      "username":"isos-server",
      "ip":"191.1.70.205",
      "용도":"웹 MES API 서버 + DB 서버(Postgresql, Redis)",
      "API 서버 포트":3004
   },
   {
      "name":"iso-client",
      "username":"isos-server",
      "ip":"191.1.70.232",
      "용도":"웹 MES 클라이언트 서버",
      "포트":3000
   },
   {
      "name":"jenkins",
      "username":"isos-server",
      "ip":"191.1.70.215",
      "용도":"CI/CD 서버",
      "웹 서버 포트":8080
   }
]
```

### 사내 프로그램 배포 흐름
개발자가 최신 소스 코드를 Git 시스템에(AWS CodeCommit, Github) 업로드 → Jenkins가 최신 소스 코드를 인식 → 웹 서버에(iso-client, DMS 등) 소스 코드 다운로드 실행 프로그램 빌드 명령 실행
![흐름도](https://github.com/isos-consulting/feto/assets/49608580/006f2121-32bf-4e9a-aa34-a6e3b171df2e)

### Jenkins에 대해서
Jenkins는 개발자가 수정한 소스 코드를 서버에 자동으로 배포하기 위해서 사용하는 도구입니다(애플리케이션).

### 설치된 소프트웨어 목록
#### dms-server
- apache-tomcat-8.5.87
- jdk1.8.0_202
- mysql-server_5.7.41
#### isos-server
- postgresql-13
- redis-server
- nodejs-20.0.0
#### iso-client
- nodejs-18.12.1
#### jenkins
- jenkins
- java-11.0.19
