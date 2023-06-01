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

### 사내 프로그램 배포 흐름
개발자가 최신 소스 코드를 Git 시스템에(AWS CodeCommit, Github) 업로드 → Jenkins가 최신 소스 코드를 인식 → 웹 서버에(iso-client, DMS 등) 소스 코드 다운로드 실행 프로그램 빌드 명령 실행
![흐름도](https://github.com/isos-consulting/feto/assets/49608580/006f2121-32bf-4e9a-aa34-a6e3b171df2e)

### Jenkins에 대해서
Jenkins는 개발자가 수정한 소스 코드를 서버에 자동으로 배포하기 위해서 사용하는 도구입니다.(애플리케이션)

```
❗ 이 문서에는 Jenkins로 파이프라인을 추가하는 방법이나 새로운 자동 빌드를 설정하는 방법에 대해서 설명하지 않습니다.
단지 기존에 만들었던 빌드 설정에 대해서만 다룹니다.
```

로그인을 성공하고 난 후 Jenkins의 첫 화면입니다.
![first page](https://github.com/isos-consulting/feto/assets/49608580/316e8f15-11ac-40e4-b38e-f542cfb34c79)

1. Item을 선택합니다.
2. Item에 대한 페이지로 이동합니다.

![items](https://github.com/isos-consulting/feto/assets/49608580/cb95fe3b-f571-4a9a-894d-68e4aefe6925)

3. 구성을 클릭합니다

![tabs](https://github.com/isos-consulting/feto/assets/49608580/04570e75-8f2e-4b30-970d-89e5d51c13c9)

4. 소스 코드 관리에서 자동 배포를 하기 위한 소스 코드 저장소 정보를 확인합니다.
`❗ 정보 유출을 피하기 위해 저장소 정보는 올리지 않았습니다`

![SCM](https://github.com/isos-consulting/feto/assets/49608580/dd66f5ce-f9d3-4ddd-a9ec-5b4c158459fa)

5. 빌드 유발 > "Poll SCM"을 확인합니다.
6. Schedule 입력 값은 저장소에 5분 간격으로 변경사항이 있는지 확인합니다.

![polling](https://github.com/isos-consulting/feto/assets/49608580/c85eff08-655d-4080-8a46-9182f6abce5d)

7. 빌드 환경 > Provide Node & npm bin/ folder to PATH에서 NodeJS 설치 버전을 확인합니다

![build environment](https://github.com/isos-consulting/feto/assets/49608580/42097c9a-2b0f-469c-87cb-f315477e74ff)

8. Build Steps > Execute Shell > command의 입력 값은 최신 소스 코드를 빌드하고 웹 서버에 자동으로 배포하는 명령어 입니다.
`❗ 정보 유출을 피하기 위해 command 코드는 올리지 않았습니다`

![commands](https://github.com/isos-consulting/feto/assets/49608580/2489ddf6-ae82-4043-93cf-f412e3e828e8)

9. 빌드 후 조치 > Discord Notifier > Webhook URL의 입력 값은 빌드 결과를 `discord` 애플리케이션에 알림을 줍니다.
`❗ 정보 유출을 피하기 위해 Webhook URL은 올리지 않았습니다`

![image](https://github.com/isos-consulting/feto/assets/49608580/73691952-67d9-4fb2-9c80-6720fcf97176)
