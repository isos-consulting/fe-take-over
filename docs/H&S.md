# 서버가 꺼졌을 때 해야할 행위
1. Seetrol을 이용하여 고객사 PC에 접속합니다.(`[H&S]GatheringPC`)
2. 파일 탐색기를 실행합니다.
3. nginx 프로그램이 설치된 경로로(`C:\Program Files\nginx\1.22.0`) 이동합니다.
4. 파일 탐색기에서 nginx.exe 프로그램을 마우스로 더블클릭해서 실행합니다.
5. 웹 브라우저에서 화면이 나타나는지 확인합니다.
6. 서버가 실행되지 않을 경우 서비스를 재시작합니다.

![nginx설치경로](https://github.com/isos-consulting/feto/assets/49608580/cc13dafa-2381-482d-b028-e3cd2f3dd50d)

## 프로그램 소스코드 저장소 경로
"사내 SVN 저장소 URL"은 회사 내부에서 사용하는 SVN 주소 유출을 피하기 위해서 가짜 이름을 사용했습니다.

`svn://{사내SVN 저장소 URL}/에이치엔스하이테크/VISION_IMG_AI_HSHIGHTECH`

## 개발 라이브러리 주요 목록
화면(웹 클라이언트) 개발을 하기 위해서 "*" 표시된 라이브러리의 사용을 알아야합니다.
- react*
- tui-grid*
- axios*
- chartjs

## 고객사에 대한 정보
고객사의 사업 제품은 ACF 필름입니다.

### ACF 필름
기판과 반도체 사이에 들어가는 필름입니다.

#### 제품의 양품 판정 검사 목록
- 접착력
- 접속저항
- 필름저항
- 인장강도
- 절연저항

#### 품질 검사 작업 흐름
1. 검사실에 있는 기계가 제품을 검사한 후 불량 이미지를(사진) 내보냄
2. 작업자가 USB에 이미지 파일을 내려받음
3. 사무실에 있는 관리자에게 USB를 전달함
4. 이미지를 다시 보면서 불량 확인

#### 공정
1. Mix(원재료 배합)
2. Coater(롤로 말려있는 필름을 펴면서 도포)
3. Precutting(+ Aging, 오븐에 필름을 숙성)
4. Sliting(필름을 매우 얇게 자름)

![공정 사진](https://github.com/isos-consulting/feto/assets/49608580/250ac3ea-2365-4aac-b82e-34a0e24ee7a4)

#### 추가 정보
- 품질 때문에 필름의 부분만 검사를 실시함(품명, LOT 번호, 컷 번호, 릴 번호)
- 이미지 검사를 AI가 처리한 후 양품과 불량 판정을 하는 일
- 애플리케이션의 페이지 기능 구성
  - 분석: 검사 폴더의 이미지를 AI로 판별함(현황 분석: USB를 관리자에게 전달하려면 건물 2층에서 3층으로 이동해야하는데, 작업자는 방진복을 환복해야하는 낭비가 발생한다)
  - 조회: 이미 분석된 이미지의 결과를 확인(조회 기간의 영향을 받음)
  - 학습: 사진 결과를 판별하는 알고리즘을 적용

## 애플리케이션 정보
`❗ 만약 웹 애플리케이션을 Visual Basic이나 다른 언어로 작성할 경우 아래 내용을 참고해주세요.`

### API 목록
#### Accuracy 조회
```
{
  URL: http://{API서버URL}/vision-analysis/accuracy,
  METHOD: GET
}
```
#### 메인 화면 데이터 그리드 조회
```
{
  URL: http://{API서버URL}/vision-analysis/result-total
  METHOD: GET
  QUERYSTRING: {
    start_date: 입력폼 lastDate 데이터("YYYY-MM-DD"),
    end_date: 입력폼 currendDate 데이터("YYYY-MM-DD"),
    prod_nm: 입력폼 prodNm이 ""이면(공백 문자열) null, 아니면 입력폼 prodNm값,
    lot_no: 입력폼 lotNo이 ""이면(공백 문자열) null, 아니면 입력폼 lotNo값
    
  }
}
```
#### 분석 조회
```
{
  URL: http://{API서버URL}/vision-analysis/execute,
  METHOD: GET,
  QUERYSTRING: {
    start_date: 입력폼 lastDate 데이터("YYYY-MM-DD"),
    end_date: 입력폼 currendDate 데이터("YYYY-MM-DD")
  }
}
```
#### 분석 검사 조회
```
{
  URL: http://{API서버URL}/vision-analysis-check/execute,
  METHOD: GET,
}
```
#### 학습 검사 조회
```
{
  URL: http://{API서버URL}/learning-check/vision,
  METHOD: GET,
}
```
#### 학습 조회
```
{
  URL: http://{API서버URL}/learning/vision,
  METHOD: GET,
}
```
#### 모달 화면 데이터 그리드 조회
```
{
  URL: http://{API서버URL}/vision-analysis/result-detail,
  METHOD: GET,
  QUERYSTRING: {
    reg_date: 사용자가 선택한 메인 데이터 그리드 행의 reg_date,
    log_no: 사용자가 선택한 메인 데이터 그리드 행의 lot_no,
    cut_no: 사용자가 선택한 메인 데이터 그리드 행의 cut_no,
    reel_no: 사용자가 선택한 메인 데이터 그리드 행의 reel_no,
    seq: 사용자가 선택한 메인 데이터 그리드 행의 seq,
  }
}
```
#### 모달 화면 데이터 그리드 수정
```
{
  URL: http://{API서버URL}/vision-analysis/real-result,
  METHOD: PATCH,
  BODY: [{
    idx: 변경 모달 데이터 그리드 행의 idx,
    reel_result: 변경 모달 데이터 그리드 행의 reel_result가 "true"면(문자열) true(boolean), 아니면 false(boolean),
    file_path: 변경 모달 데이터 그리드 행의 file_path,
    file_nm: 변경 모달 데이터 그리드 행의 file_nm,
    analysis_result: 변경 모달 데이터 그리드 행의 analysis_result가 "양품"이면(문자열) true(boolean), 아니면 false(boolean)
  } x 모달 데이터 그리드에서 변경 수만큼 반복 ]
}
```

### 화면 구성
#### 조회 폼
|한글명|영문명|기본값|데이터타입|
| --- | --- | --- | --- |
|시작일|lastDate|오늘 -7일|"YYYY-MM-DD"|
|종료일|currendDate|오늘|"YYYY-MM-DD"|
|품목명|prodNm|""|문자열|
|로트번호|lotNo|""|문자열|

#### 데이터 그리드


## 왜 이렇게 설명이 부족하냐면..
저는 프로젝트 담당자가 아니었습니다.

전임자의 인수인계 문서를 전달받은 적도 없습니다.

단지 화면 개발 능력이 있기 때문에 어느 순간 이슈처리를 했을 뿐입니다.

어느정도 발생 할 수있는 문제를 해결할 수 있기를 바라며 작성했습니다. 자료의 내용 부족해서 미안합니다..
