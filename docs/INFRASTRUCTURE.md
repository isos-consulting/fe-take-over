# 사내 웹 서버 구성
![사내 웹 서버 구성도](https://github.com/isos-consulting/feto/assets/49608580/a48b3c94-12ad-4242-82c5-d17e81d0d9b6)

## 서버 정보
모든 서버는 동일한 운영체제 버전(ubuntu18.04_amd64)을 사용합니다.

`❗ 서버의 자세한 접속 정보는 사내에 있는 데스크탑 케이스에 붙어있는(종이로 작성한) 내용을 확인해주세요`

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
1. 개발자가 최신 소스 코드를 Git 시스템(AWS CodeCommit, Github)에 업로드
2. Jenkins가 최신 소스 코드를 감지
3. 웹 서버(iso-client, DMS 등)에 소스 코드를 다운로드하고 프로그램을 빌드하여 배포

![흐름도](https://github.com/isos-consulting/feto/assets/49608580/006f2121-32bf-4e9a-aa34-a6e3b171df2e)

### Jenkins에 대해서
Jenkins는 개발자가 수정한 소스 코드를 서버에 자동으로 배포하기 위해 사용하는 도구입니다(애플리케이션).

```
❗ 이 문서에서는 Jenkins로 파이프라인을 추가하거나 새로운 자동 빌드를 설정하는 방법에 대해서는 설명하지 않습니다.
단지 기존에 설정한 빌드에 대해서만 다루겠습니다.
```

로그인에 성공한 후 Jenkins의 첫 화면입니다.
![first page](https://github.com/isos-consulting/feto/assets/49608580/316e8f15-11ac-40e4-b38e-f542cfb34c79)

1. Item을 선택합니다.
2. 해당 Item 페이지로 이동합니다.

![items](https://github.com/isos-consulting/feto/assets/49608580/cb95fe3b-f571-4a9a-894d-68e4aefe6925)

3. 구성을 클릭합니다.

![tabs](https://github.com/isos-consulting/feto/assets/49608580/04570e75-8f2e-4b30-970d-89e5d51c13c9)

4. 소스 코드 관리에서 자동 배포를 위한 소스 코드 저장소 정보를 확인합니다.

`❗ 정보 유출을 피하기 위해 저장소 정보는 제외되었습니다`

![SCM](https://github.com/isos-consulting/feto/assets/49608580/dd66f5ce-f9d3-4ddd-a9ec-5b4c158459fa)

5. 빌드 유발 > "Poll SCM"을 확인합니다.
6. Schedule 입력 값은 저장소에서 5분 간격으로 변경 사항을 확인합니다.

![polling](https://github.com/isos-consulting/feto/assets/49608580/c85eff08-655d-4080-8a46-9182f6abce5d)

7. 빌드 환경 > "Provide Node & npm bin/ folder to PATH"에서 NodeJS 설치 버전을 확인합니다.

![build environment](https://github.com/isos-consulting/feto/assets/49608580/42097c9a-2b0f-469c-87cb-f315477e74ff)

8. Build Steps > Execute Shell > command의 입력 값은 최신 소스 코드를 빌드하고 웹 서버에 자동으로 배포하는 명령어입니다.

`❗ 정보 유출을 피하기 위해 command 코드는 제외되었습니다`

![commands](https://github.com/isos-consulting/feto/assets/49608580/2489ddf6-ae82-4043-93cf-f412e3e828e8)

9. 빌드 후 조치 > Discord Notifier > Webhook URL의 입력 값은 빌드 결과를 `Discord` 애플리케이션에 알림으로 보내기 위한 URL입니다.

`❗ 정보 유출을 피하기 위해 Webhook URL은 제외되었습니다`

![discord webhook](https://github.com/isos-consulting/feto/assets/49608580/73691952-67d9-4fb2-9c80-6720fcf97176)

#### 빌드를 수행할 서버의 접속 상태 확인
1. Jenkins 관리 탭을 클릭합니다.

![tabs](https://github.com/isos-consulting/feto/assets/49608580/e3e40222-927e-46a2-af4c-1f1dd429db20)

2. 노드 관리를 클릭합니다.

![node management](https://github.com/isos-consulting/feto/assets/49608580/5edf8c93-5738-4c9d-b5e1-f2c6bda4322d)

3. 연결된 서버 목록에서 접속 상태를 확인합니다.

![node list](https://github.com/isos-consulting/feto/assets/49608580/cf4c4e37-041a-4d76-98a5-4ee44133c9d8)

4. 서버 연결이 끊어진 경우 해당 서버를 선택한 후 나타나는 명령어를 원격 서버에서 실행합니다.
   - 원격 서버에 SSH 또는 Seetrol을 사용하여 접속합니다.

`❗ 아래 이미지는 정상적으로 연결된 상태를 나타냅니다.`

![node](https://github.com/isos-consulting/feto/assets/49608580/596c8a17-fb47-4f74-a541-b9612c63f4da)

#### 자동 배포가 적용되지 않는 경우 확인 사항
- 빌드 스크립트(`Build Steps > Execute Shell > command`) 실행 중에 문제가 발생했는지 확인합니다.
- 노드 관리에서 서버의 접속 상태를 확인합니다.
