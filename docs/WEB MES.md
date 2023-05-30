# 용도
웹 브라우저에서 동작하는 스마트 팩토리 MES 애플리케이션

## 애플리케이션 개발 주요 라이브러리 구성
- React
- Antd
- Chartjs
- formik
- tui-grid

## 애플리케이션 이슈 목록
이 프로젝트의 이슈는 시간이 지남에 따라 많은 변경이 있었음(`jira → notion → github`)
- [jira](https://iwork.atlassian.net/jira/software/projects/IC/boards)
- [notion](https://www.notion.so/199a4f2a831e4bfea0dc93ac80455ea3)
- [github](https://github.com/isos-consulting/WEB-MES-CLIENT/issues)
- [excel](https://github.com/isos-consulting/feto/files/11596635/20230410_WEB_MES.xlsx)

### 최근 다룰 이슈
- react typescript 의존성 설치한 후 발생하는 타입 에러 수정해야 함
- CUD API를 요청하는 공통 함수를 사용하지 않는 방법을(`saveGridData → MESService`) 적용 중임
- `template`화면의(1레벨 그리드, 2레벨 그리드, 3레벨 그리드...등) 커스터마이즈를 유연하게 할 수 있어야 함

### 기타
![화면별 데이터 그리드 개수를 정리함](https://github.com/isos-consulting/feto/assets/49608580/ea66357d-006a-4964-987c-71054a3b3f87)

