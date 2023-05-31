# 사내 웹 서버 구성
![사내 웹 서버 구성도](https://github.com/isos-consulting/feto/assets/49608580/6a1fb528-1886-4241-ba71-1e5775bc40ff)

## 서버 정보
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

![흐름도](https://github.com/isos-consulting/feto/assets/49608580/48a2cc14-03d6-4322-9223-9c8241ca7250)

### Jenkins에 대해서
Jenkins는 개발자가 수정한 소스 코드를 서버에 자동으로 배포하기 위해서 설치한 도구입니다(애플리케이션).
