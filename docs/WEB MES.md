# 용도
웹 브라우저에서 동작하는 스마트 팩토리 MES 애플리케이션

## 애플리케이션 개발 주요 라이브러리 구성
`❗ 웹 클라이언트 프로그램 개발을 하기 위해서 아래 라이브러리의 사용법을 숙지 해주세요.`
- react
- antd
- chartjs
- formik
- tui-grid
- typescript

## 애플리케이션 이슈 목록
이 프로젝트의 이슈는 시간이 지남에 따라 많은 변경이 있었음(`jira → notion → (github + excel)`)
- [jira](https://iwork.atlassian.net/jira/software/projects/IC/boards)
- [notion](https://www.notion.so/199a4f2a831e4bfea0dc93ac80455ea3)
- [github](https://github.com/isos-consulting/WEB-MES-CLIENT/issues)
- [excel](https://github.com/isos-consulting/feto/files/11596635/20230410_WEB_MES.xlsx)

### 최근 다룰 이슈
- react typescript 의존성 설치한 후 발생하는 타입 에러 수정해야 함
- CUD API를 요청하는 공통 함수를 사용하지 않는 방법을(`saveGridData → MESService`) 적용 중임
- `template`화면의(1레벨 그리드, 2레벨 그리드, 3레벨 그리드...등) 커스터마이즈를 유연하게 할 수 있어야 함

### 앞으로 남은 과제
- 사용성 개선
  - 품목 데이터 2만 건을 조회했을 때 속도가 너무 느림, 최적화(조회 조건 혹은 캐싱 같은) 적용이 필요함
  - 데이터 그리드에서 CRUD 행위가 발생했을 때 사용자가 선택한 포커스를 유지할 수 있어야함
  - 매뉴얼 추가 해야함
  - 품목의 라우팅 등록, 수입 검사, 창고의 불량창고 등록 같은 필수 조건에 대한 설정을 편리하게 바꿔야함(`나는 챗 봇 같은 시스템을 이용해서 데이터 변경 API 처리까지 해주는게 좋다고 생각함`)
  - 데이터 생성, 수정을 처리하기 위한 모달창을 없애고 한 화면에서 처리할 수 있어야함
  - 관리자는 많은 동시에 많은 화면을 다뤄야 할 일이 있기 때문에 화면 전환이 아닌 탭을 추가하는 방식으로 처리할 수 있어야함

### 기타
![화면별 데이터 그리드 개수를 정리함1](https://github.com/isos-consulting/feto/assets/49608580/ad81300f-d97d-4240-a4c5-a7fd694bed2c)
![화면별 데이터 그리드 개수를 정리함2](https://github.com/isos-consulting/feto/assets/49608580/ea66357d-006a-4964-987c-71054a3b3f87)

