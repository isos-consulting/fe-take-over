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
#### 현재 인공지능 정확도 조회
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
#### 현재 인공 지능 정확도 필드
[현재 인공지능 정확도 조회 API 요청](#현재-인공지능-정확도-조회)하여 값을(% 단위) 표시함
#### 조회 폼
|한글명|영문명|기본값|데이터타입|
| --- | --- | --- | --- |
|시작일|lastDate|오늘 -7일|"YYYY-MM-DD"|
|종료일|currendDate|오늘|"YYYY-MM-DD"|
|품목명|prodNm|""|문자열|
|로트번호|lotNo|""|문자열|
#### 메인 화면 데이터 그리드
|한글명|영문명|데이터 정렬|
| --- | --- | --- |
|검사일자|reg_date|가운데 정렬|
|제품명|prod_nm|왼쪽 정렬|
|폭|width|가운데 정렬|
|길이|length|가운데 정렬|
|두께|tickness|가운데 정렬|
|LOT|lot_no|왼쪽 정렬|
|cut no|cut_no|왼쪽 정렬|
|릴|reel_no|왼쪽 정렬|
|순번|seq|가운데 정렬|
|비전검사기 검출수량|total_cnt|가운데 정렬|
|AI예측 이물수량|ng_cnt|가운데 정렬|
|0~100|first_degree|가운데 정렬|
|100~200|sescond_degree|가운데 정렬|
|200~300|third_degree|가운데 정렬|
|300~400|fourth_degree|가운데 정렬|
|400↑|fifth_degree|가운데 정렬|
#### 모달 데이터 그리드
|한글명|영문명|데이터 정렬|특징|
| --- | --- | --- | --- |
|검사일자|reg_date|왼쪽 정렬||
|제품명|prod_nm|왼쪽 정렬||
|폭|width|가운데 정렬||
|길이|length|가운데 정렬||
|두께|tickness|가운데 정렬||
|LOT|lot_no|왼쪽 정렬||
|cut no|cut_no|왼쪽 정렬||
|릴|reel_no|왼쪽 정렬||
|사진|file|가운데 정렬|화면에 사진이 보여야 됨|
|AI 예측|analysis_result|가운데 정렬||
|Area|area|가운데 정렬||
|이물종류|reject_type_nm|가운데 정렬||
|확률(%)|probability|가운데 정렬||
|정답|real_result|가운데 정렬|LOV로 데이터 수정할 수 있음 `[{UI 텍스트: 양품, 값: true}, UI 텍스트: 이물, 값: false]`|

### 이벤트를 구성
#### 화면을 처음 접속했을 때
1. [현재 인공지능 정확도 조회 API 요청](#현재-인공지능-정확도-조회)
2. 현재 인공지능 정확도 필드에 API 응답 데이터 할당
#### 조회 버튼을 클릭했을 때
1. [메인 데이터 그리드 조회 API 요청](#메인-화면-데이터-그리드-조회)
2. 메인 데이터 그리드에 API 응답 데이터 할당
3. [현재 인공지능 정확도 조회 API 요청](#현재-인공지능-정확도-조회)
4. 현재 인공지능 정확도 필드에 API 응답 데이터 할당
#### 분석 버튼을 클릭했을 때
1. [분석 데이터 조회 API 요청](#분석-조회)
2. 종료일 필드의 값을 오늘로 변경
3. 분석여부 값을 true로 변경
#### 학습 버튼을 클릭했을 때
1. [학습 검사 조회 API 요청](#학습-검사-조회)
2. [학습 조회 API 요청](#학습-조회)
3. 학습 조회 API 응답 메시지 출력
#### 메인 데이터 그리드에서 행을 더블클릭했을 때
1. [모달 화면 데이터 조회 API 요청](#모달-화면-데이터-그리드-조회)
2. API 응답 데이터 파싱
```
  2-1. alaysis_result값을 문자열로 파싱 `["양품", "이물"]`
  2-2. real_result 값을 문자열로 파싱 `["true", "false"]`
```  
2. 모달 데이터 그리드에 파싱한 데이터를 할당
3. 모달 출력
#### 저장 버튼을 클릭했을 때
1. 모달 데이터 그리드 변경 데이터 추출
2. 추출 데이터 파싱
```
  2-1. alaysis_result값을 boolean으로 파싱 `[true, false]`
  2-2. reel_result값을 문자열로 파싱 `[true, false]`
```
3. [모달 화면 데이터 수정 API 요청](#모달-화면-데이터-그리드-수정)
4. [현재 인공지능 정확도 조회 API 요청](#현재-인공지능-정확도-조회)
5. 현재 인공지능 정확도 필드에 API 응답 데이터 할당
6. [모달 화면 데이터 조회 API 요청](#모달-화면-데이터-그리드-조회)
7. API 응답 데이터 파싱
```
  7-1. alaysis_result값을 문자열로 파싱 `["양품", "이물"]`
  7-2. real_result 값을 문자열로 파싱 `["true", "false"]`
```  
8. 모달 데이터 그리드에 파싱한 데이터를 할당
#### 취소 버튼을 클릭했을 때
1. 모달 닫기
#### API 요청이 실패했을 때
1. 화면에 API 실패 메시지를 출력
