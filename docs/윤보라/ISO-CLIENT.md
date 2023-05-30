# 프로젝트 개요

본사에서 Visual Basic으로 개발된 MES 프로그램을 WEB 환경에서 구동시키기 위해 ReactJS로 개발한 MES 웹 프로젝트 입니다. 웹 개발과 동시에 기존 MES 프로그램의 프로세스를 표준화하여 표준된 서비스를 제공하기 위한 목적도 가지고 있습니다.

### 서비스 중인 고객사 (작성일 기준)

- 뉴아세아조인트

# 프로젝트 내려받기

프로젝트는 [AWS > CodeCommit](https://ap-northeast-2.console.aws.amazon.com/codesuite/codecommit/repositories/iso-client/browse?region=ap-northeast-2)을 통해 받을 수 있습니다. 프로젝트를 설치할 폴더에서 cmd창을 열고 아래 명령어를 입력하여 프로젝트를 내려 받을 수 있습니다.

```powershell
> git clone https://git-codecommit.ap-northeast-2.amazonaws.com/v1/repos/iso-client
```

<aside>
💡 **유의사항**
본 프로젝트는 [Parcel 번들러](https://ko.parceljs.org/getting_started.html)를 사용하고 있습니다.
프로젝트를 시작하실려면 먼저 parcel 번들러를 설치해주세요.

Yarn:

```
yarn global add parcel-bundler
```

npm:

```
npm install -g parcel-bundler
```

</aside>

# 프로젝트 구조

프로젝트를 내려받은 후 폴더를 열어보시면 다음과 같은 구조를 볼 수 있습니다.

```
**iso-client**
┣━ /public
****┣━ /snippets                         // 스니펫 폴더
┣━ /src
	┣━ /components                     // 컴포넌트 폴더
		┣━ /pages                        // 페이지 폴더
			┣━ /adm
			┣━ /aut
			┣━ /eqm
			┣━ /inv
			┗━ ...
		┣━ /templates                    // 템플릿 폴더
			┣━ /grid-double
			┣━ /grid-single
			┣━ /grid-triple
			┗━ ...
		┗━ /UI                           // UI 폴더
			┣━ /button
			┣━ /button-group
			┣━ /checkbox
			┣━ /checkbox-group
			┣━ /combobox
			┗━ ...
	┣━ /enums                          // 상수 폴더
	┣━ /fonts                          // 폰트 폴더 
	┣━ /functions                      // 공용 함수 폴더
	┣━ /hooks                          // 공용 훅 폴더
	┣━ /images                         // 이미지 리소스 폴더
	┣━ /recoils                        // 전역 훅 폴더
	┣━ /styles                         // 스타일 폴더
	┣━ /typings                        // 확장자 지정 폴더
┣━ .babelrc                          // 바벨 설정 파일
┣━ .env                              // 환경변수 설정 파일
┣━ .gitignore                        // git 예외설정 파일
┣━ .postcssrc                        // postcss 설정 파일
┣━ buildspec.yml                     // AWS build 커맨드 설정 파일
┣━ package.json                      // 패키지 설정 파일
┣━ README.md                         // 프로젝트 설명서
┣━ tsconfig.json                     // typescript 설정 파일
┗━ yarn.lock                         // 패키지 버전 고정 파일
```

### snippets

- 개발 편의성을 위한 커스텀 스니펫을 정의하는 폴더 입니다.
- 스니펫 설정법은 프로젝트 내의 `snippets > readme.txt`를 참고하세요.

### src > components

- 리액트 환경에서 렌더링될 페이지, UI를 모아놓은 폴더입니다.
- templates은 page의 베이스가 되는 마크업 컴포넌트를 모아두는 폴더입니다.

### src > hooks

- 공용 훅을 모아두는 폴더입니다.
- **컴포넌트를 로딩할 때 true/false 값을 관리할 loading.hook.ts 파일만 사용하고 있었으나 로딩한 후 입력해놓은 데이터가 초기화되는 현상 때문에 현재는 authStore를 제외한 나머지 파일은 사용하고 있지 않습니다.**

### .babelrc

- 바벨 플러그인 설정 파일입니다.
- 본 프로젝트에서는 절대 경로 설정을 위해 사용되었습니다.

### .env

- 프로젝트에서 사용할 환경변수를 설정하는 파일입니다.
- 본 프로젝트에서는 온전한 이름으로 환경변수를 사용하고 있지만 상위 버전에서는 REACT_APP_xxx 형식으로 작성하지 않으면 동작하지 않습니다.
- **처음엔 crypto-js를 통해 암호화 또는 복호화할 때 사용하는 secret key를 저장하기 위해 사용하였지만 현재는 production 및 development 환경의 URL 정보를 활용할 때 사용하고 있습니다.**

### buildspec.yml

- AWS Build 환경에서 빌드 시 동작시킬 일련의 커맨드를 작성해놓는 파일입니다.

### tsconfig.json

- 타입스크립트 설정 파일입니다.
- baseUrl, paths(절대경로), 컴파일 빌드 경로, 타입 검사 전략 등을 설정할 수 있습니다.

# 패키지

React 프로젝트의 모든 라이브러리 정보는 package.json 파일을 통해 확인할 수 있습니다.

본 프로젝트에서 사용중인 라이브러리 현황은 아래와 같습니다. (문서 작성일 기준)

```
// 붉은글자 - 필요없으니 삭제해야 될 패키지
// 주황글자 - 활용하진 않으나 필요할순 있는 패키지
{
  ...
  "devDependencies": {
    "@babel/core": "^7.0.0-0",                            // 바벨 구동을 위한 메인 패키지
    "@babel/plugin-transform-react-jsx": "^7.16.7",       // 자동 런타임 반응을 위한 패키지, 자동으로 jsx가 가진 함수를 가져올 수 있습니다.
    "@babel/preset-env": "^7.16.7",                       // 브라우저 지원 설정을 할 수 있는 플러그인을 포함하는 프리셋
    "@babel/preset-react": "^7.16.7",                     // React 관련 플러그인을 포함한 프리셋
    "@babel/preset-typescript": "7.15.0",                 // Typescript 관련 플러그인을 포함한 프리셋
    "@types/crypto-js": "4.0.1",                          // 암호화 및 복호화를 위한 패키지
    "babel-plugin-root-import": "6.6.0",                  // 절대 경로를 지정할 수 있게 해주는 바벨 플러그인 입니다.
    "parcel-bundler": "1.12.5",                           // 컴파일 및 빌드 번들러
    "postcss-modules": "3.2.2",                           // css module을 어디서든 사용하기 위한 패키지
    "typescript": "4.4.4",                                // 타입스크립트 패키지
    "uuid": "8.3.2"                                       // 랜덤한 uuid를 생성해주는 패키지
  },
  "dependencies": {
    "@nivo/bar": "^0.74.0",                               // 막대 그래프 패키지
    "@nivo/core": "^0.74.0",                              // 그래프 구동을 위한 메인 패키지
    "@nivo/line": "^0.74.0",                              // 선형 그래프 패키지
    "@nivo/pie": "^0.74.0",                               // 원형 그래프 패키지
    "@toast-ui/react-grid": "^4.19.4",                    // 데이터 그리드 패키지
    "@types/lodash": "^4.14.177",                         // 개발 유틸 함수를 모은 패키지
    "ant-design": "1.0.0",                                // UI 템플릿 패키지
    "antd": "4.16.1",                                     // UI 템플릿 패키지
    "axios": "0.21.1",                                    // HTTP통신을 위한 패키지
    "axios-progress-bar": "1.2.0",                        // HTTP통신할 때 프로그래스를 화면에 표시하기 위한 패키지 입니다.
    **"components": "0.1.0",                                // ??**
    "crypto-js": "4.0.0",                                 // 암호화 및 복호화를 위한 패키지
    "dayjs": "1.9.8",                                     // 날짜 및 시간 포맷을 다루는 패키지
    "dotenv": "8.2.0",                                    // 런타임 환경변수 설정 패키지
    "exceljs": "4.2.1",                                   // javascript 코딩으로 엑셀 파일을 생성하고 읽을 수 있게 해주는 패키지
    "formik": "2.2.9",                                    // form 태그처럼 input을 그룹으로 관리해주는 패키지
    **"images": "3.2.3",                                    // 이미지 인코더, 디코더 (어디서, 뭘 위해 사용중인지 알수없음)**
    **"rc-picker": "2.5.0",                                 // 달력 입력기? 현재 사용중인 곳 없음**
    "react": "17.0.2",
    "react-dom": "17.0.2",
    "react-router-dom": "5.2.0",
    "react-scripts": "4.0.3",
    **"react-to-print": "2.12.2",                           // 간편한 인쇄 기능 구현할 때 사용하는 패키지**
    **"recoil": "0.3.0",                                    // 전역 상태관리를 위한 패키지**
    "sass": "1.43.2",                                     // .scss를 사용하기 위한 패키지
    "styled-components": "5.2.1"                          // 컴포넌트 자체에 스타일을 입히는 패키지
  },
  ...
}
```

# DataGrid 사용하기

데이터 그리드의 관한 글은 하위 페이지를 참조하세요.

[DataGrid](https://github.com/isos-consulting/fe-take-over/blob/main/docs/%EC%9C%A4%EB%B3%B4%EB%9D%BC/DataGrid.md)

# 문제점

본 섹션에서는 현재 프로젝트가 가진 문제점에 대해 기술되었습니다.

### 집합된 코드

코드가 한 파일에 집합되어 작성된 경우가 많습니다. 이는 보는 사람들로 하여금 가독성을 떨어트리며, 코드의 이해도를 낮추어 버리는 문제가 있습니다. 본 프로젝트에서는 하나로 집합된 코드를 단일 클래스나 함수로 분리시켜 가독성을 올리는 방법이 필요합니다.

### 다양한 방식의 스타일 코드

현재 프로젝트 내에 스타일 코드는 일관성이 많이 떨어집니다. 인라인 방식, css, scss, styledComponent, 이렇게 네 가지 방식으로 나누어져 있습니다. 스타일 방식이 한 프로젝트 내에서 이렇게 다양하게 사용되면 어느정도 규칙이 마련되어 있어야 하는데 현재 그러한 규칙은 존재하지 않습니다.

스타일 방식이 이렇게 다양하게 된 까닭이 나름 있습니다. 최초로 퍼블리싱된 프로젝트에선 styled-components 방식만 사용했었습니다. 그러나, tui-grid, antd 라이브러리 사용으로 인해 styled-components 방식을 사용하기엔 코드의 복잡성이 증가하는 문제가 발생했습니다.

라이브러리의 스타일을 클래스 네임을 써서 변경하는 일을 작업할 때부터 css 클래스 네임 방식을 사용하기 시작했습니다. 그 과정에서 스타일을 변수로 관리하고자 scss를 채택하게 되었고, 작업을 급하게 하다보니 인라인 방식을 사용하게 되어 지금의 다양한 스타일 코드가 탄생하게 되었습니다.

스타일 코드 작성에는 나름의 규칙이 필요합니다. 하지만 지금의 스타일 방식은 매우 중구난방인 상태에 머물러 있습니다. 스타일 코드 작성에 대한 컨벤션이 필요한 상황입니다.

### 중복된 코드

코드를 여기저기 작성하다보면 과거에 작성한 함수에 대해 기억조차 못하는 경우가 흔히 있습니다. 새로운 페이지에서 작업을 할 때 다른 페이지 소스에 이미 있는 함수를 모르고 다시 만드는 경우도 있습니다. 이런 현상을 줄이기 위해서라도 코드 작성에 대한 컨벤션이 필요합니다.

### 과도한 이펙트 사용

이펙트는 매우 유용한 기능입니다. 하지만 과도하게 사용하면 오히려 예기치 못한 오류를 초래할 수 있습니다. 이펙트가 이펙트를 호출하는 상황처럼 체인 현상이 발생하게 되면 원하는 결과가 제대로 나오지 않을 확률이 높습니다.

이펙트는 좋은 기능이지만 사용하기 나름입니다. 본 프로젝트에선 이펙트의 사용이 너무 과합니다. 이펙트는 꼭 사용해야할 경우에만 사용해야하며, 사용하지 않아도 되는 경우에는 사용하지 않는 방향으로 개발을 해야합니다. 이펙트를 과도하게 사용하면 렌더링 관리가 안되기 때문입니다.

렌더링은 성능 문제와 직결됩니다. 과도한 이펙트 사용은 오류와 성능 저하의 원인이 될 수 있습니다.
