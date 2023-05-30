# 프로젝트 개요

웹 프로젝트 개발 편의성과 표준화된 컴포넌트 개발 추진을 위해 생성된 프로젝트 입니다. 다른 웹 프로젝트에서 해당 프로젝트의 UI를 import 받아 사용할 수 있도록 만들었습니다.

본 프로젝트는 antd 패키지를 기반으로 만들어졌습니다.

# 프로젝트 내려받기

프로젝트는 [AWS > CodeCommit](https://ap-northeast-2.console.aws.amazon.com/codesuite/codecommit/repositories/isos-client/browse?region=ap-northeast-2)을 통해 받을 수 있습니다. 프로젝트를 설치할 폴더에서 cmd창을 열고 아래 명령어를 입력하여 프로젝트를 내려 받을 수 있습니다.

```powershell
> git clone https://git-codecommit.ap-northeast-2.amazonaws.com/v1/repos/isos-client
```

<aside>
💡 **유의사항**
본 프로젝트는 Code Artifact를 사용하여 패키지를 관리하고 있습니다.
프로젝트를 실행하실려면 접근 토큰이 필요합니다. 토큰을 아래 명령어를 통해 발급 받으실 수 있습니다.

Window : 

```powershell
for /f %i in ('aws codeartifact get-authorization-token --domain isos --domain-owner 557471975685 --query authorizationToken --output text') do set CODEARTIFACT_AUTH_TOKEN=%i
```

Linux : 

```powershell
export CODEARTIFACT_AUTH_TOKEN=`aws codeartifact get-authorization-token --domain isos --domain-owner 557471975685 --query authorizationToken --output text`
```

</aside>

<aside>
🤔 토큰을 환경변수에 설정했더라도 권한 관련 오류가 발생한다면 aws configure를 통해 aws에 접속할 계정을 로컬에 등록하지 않았기 때문일 수 있습니다.
aws에 코드커밋, 코드아티팩트에 권한을 가진 계정 정보를 aws configure 명령을 통해 등록하고 다시 시도해보세요.

❗ aws configure를 설정하는 방법은 aws 관련 문서를 참조하세요.

</aside>

<aside>
📢 간혹 타 프로젝트에서 .npmrc 파일이 없음에도 isos-ui 프로젝트처럼 토큰을 요구하는 경우가 발생할 수 있습니다.
이 현상은 npm, yarn을 통해 패키지를 설치하는 행위를 했을 때 자동으로 user폴더에 rc파일을 생성해주기 때문에 발생합니다.

![Untitled](https://github.com/isos-consulting/fe-take-over/assets/49608580/6aeadadd-aaee-4565-86a5-11454afb0fc3)

프로젝트에 있는 .npmrc 정보를 복사해 사용자 폴더에 파일을 생성하고 npm 또는 yarn 명령어가 실행될 때마다 해당 rc파일이 실행됩니다.

**사용자 폴더에 있는 rc파일을 제거하면 일시적으로 토큰 오류를 없앨 수 있습니다.**

</aside>

# 프로젝트 구조

프로젝트를 내려받은 후 폴더를 열어보시면 다음과 같은 구조를 볼 수 있습니다.

```
**iso-client**
┣━ /.storybook
  ┣━ main.js
  ┣━ manager.js
  ┗━ preview.js
****┣━ /.vscode                          // vscode 설정 공유 폴더
┣━ /public
┣━ /src
	┣━ /components                     // 컴포넌트 폴더
		┣━ /breadcrumb                   
		┣━ /button
		┣━ /card
		┣━ /checkbox
		┣━ /checkbox-group
		┗━ ...
	┣━ /fonts                          // 폰트 폴더 
	┣━ /images                         // 이미지 리소스 폴더
	┣━ /utils                          // 공용 함수 폴더
┣━ .eslintignore                     // eslint 검사 제외 설정 파일
┣━ .eslintrc                         // eslint 설정 파일
┣━ .gitignore                        // git 예외 설정 파일
┣━ .npmignore                        // npm 예외 설정 파일
┣━ .npmrc                            // npm 설정 파일
┣━ .prettierrc                       // prettier 플러그인 설정 파일
┣━ buildspec.yml                     // AWS build 커맨드 설정 파일
┣━ package.json                      // 패키지 설정 파일
┣━ README.md                         // 프로젝트 설명서
┣━ rollup.config.js                  // rollup 번들러 설정 파일
┣━ tsconfig.json                     // typescript 설정 파일
┗━ yarn.lock                         // 패키지 버전 고정 파일
```

### .storybook

- [storybook](https://storybook.js.org/)에 관한 여러 설정을 할 수 있는 파일이 모여있는 폴더입니다.
- main.js에서는 플러그인과 웹팩에 관한 설정을 할 수 있습니다.
- manager.js에서는 애드온을 활용해 테마 색상을 변경할 수 있습니다.
- preview.js에서는 미리보기가 되는 영역의 렌더링 방식을 변경할 수 있습니다. 스타일을 해당 파일에서 설정하면 미리보기 영역의 스타일이 해당 스타일로 적용되게 됩니다.

### src > components

- 리액트 환경에서 렌더링될 UI를 모아놓은 폴더입니다.

### src > utils

- 개발할 때 유용하게 사용될 수 있는 함수들을 모아놓은 폴더입니다..

### .eslintrc

- [eslint](https://eslint.org/) 설정 파일입니다.
- eslint는 코드를 작성할 때 문법의 오류를 지적해주는 역할을 수행합니다.

### .npmrc

- npm 관련 설정 파일입니다.
- AWS의 코드 아티팩트를 통해 npm을 연동시켰기 때문에 해당 registry 주소와 권한 토큰을 설정하는 파일로 사용하고 있습니다.

### .prettierrc

- [prettier](https://prettier.io/) 설정 파일입니다.
- prettier는 정해진 규칙을 위반한 스크립트의 오류를 지적해주고 고쳐주는 플러그인 입니다.
- 쌍따옴표 vs 홀따옴표, 세미콜론 있음 vs 없음, 탭 2칸 vs 4칸 등의 룰을 만들어 설정할 수 있습니다.

### buildspec.yml

- AWS Build 환경에서 빌드 시 동작시킬 일련의 커맨드를 작성해놓는 파일입니다.

### rollup.config.js

- [rollup](https://rollupjs.org/guide/en/) 번들러 관한 설정 파일입니다.
- 롤업은 빠르고 적은 용량의 결과물을 빌드할 수 있는 툴입니다. 무엇보다 **es모듈로 빌드할 수 있어 라이브러리나 패키지를 작업하는데 유용합니다.** (webpack은 commonJS 형식으로만 빌드할 수 있습니다.)

### tsconfig.json

- 타입스크립트 설정 파일입니다.
- baseUrl, paths(절대경로), 컴파일 빌드 경로, 타입 검사 전략 등을 설정할 수 있습니다.

# 패키지

React 프로젝트의 모든 라이브러리 정보는 package.json 파일을 통해 확인할 수 있습니다.

본 프로젝트에서 사용중인 라이브러리 현황은 아래와 같습니다. (문서 작성일 기준)

```
// 붉은글자 - 필요없으니 삭제해야 될 패키지
// 주황글자 - 활용하진 않으나 필요할순 있는 패키지
...
"devDependencies": {
  "@rollup/plugin-alias": "^3.1.9",                     // rollup alias 설정 패키지 (빌드할 때 절대경로를 인식시키기 위해 사용되었습니다.)
  "@rollup/plugin-commonjs": "^21.0.1",                 // commonjs 모듈을 es6로 변환하기 위한 rollup 플러그인
  "@rollup/plugin-json": "^4.1.0",                      // json 파일을 es6 모듈로 변환하기 위한 rollup 플러그인
  "@rollup/plugin-node-resolve": "^13.1.3",             // 타사 모듈을 사용하기 위해 모듈을 찾아주는 rollup 플러그인
  "@storybook/addon-actions": "^6.4.14",                // storybook에서 핸들러가 수신한 데이터를 표시하기 위한 플러그인
  "@storybook/addon-essentials": "^6.4.14",             // storybook addon 개발팀에서 선별한 애드온을 모아둔 종합 애드온 패키지
  "@storybook/addon-links": "^6.4.14",                  // storybook의 탐색 링크를 구성할 수 있는 패키지
  "@storybook/builder-webpack5": "^6.4.14",             // 6이상 버전의 storybook을 실행시키기 위해 필요한 webpack5 패키지
  "@storybook/manager-webpack5": "^6.4.14",             // 6이상 버전의 storybook을 실행시키기 위해 필요한 webpack5 패키지
  "@storybook/node-logger": "^6.4.14",                  // 로깅을 수행해주는 storybook 플러그인
  "@storybook/preset-create-react-app": "^4.0.0",       // storybook에서 리액트에 관한 사전 설정을 해주는 플러그인
  "@storybook/react": "^6.4.14",                        // storybook에서 리액트 환경을 구동 시키기 위한 패키지
  "@types/lodash": "^4.14.178",                         // 개발시 편리한 util함수를 모아둔 패키지
  "eslint-config-prettier": "^8.3.0",                   // prettier와 충돌이 발생할 수 있는 규칙을 꺼두는 패키지
  "eslint-plugin-prettier": "^4.0.0",                   // prettier를 eslint의 규칙으로 실행하게 해주는 패키지 (eslint-config-prettier와 같이 사용해야 효과를 올바르게 볼 수 있습니다.)
  "prettier": "^2.5.1",                                 // 코드를 아름답게 정리해주는 코드 포맷터
  "prettier-plugin-style-order": "^0.2.2",              // 속성 선언을 아름답게 정리해주는 prettier 플러그인
  "rollup": "^2.66.1",                                  // 빠르고 가볍게 빌드해주는 패키지
  **"rollup-plugin-peer-deps-external": "^2.2.4",         // peerDependencies로 설치된 패키지를 import할 수 있게 해주는 플러그인**
  "rollup-plugin-postcss": "^4.0.2",                    // rollup에서 postcss가 원만히 통합될 수 있도록 해주는 플러그인
  "rollup-plugin-typescript2": "^0.31.1",               // typescript 구문을 컴파일러가 인식할 수 있게 해주는 패키지 (rollup-plugin-typescript의 오류를 고쳐서 새로 개선된 버전이 rollup-plugin-typescript2입니다.)
  "tsconfig-paths-webpack-plugin": "^3.5.2",            // tsconfig.json의 paths 설정을 webpack으로 설정할 수 있게 하는 패키지
  "typescript-plugin-css-modules": "^3.4.0",            // css모듈을 typescript 환경에서 사용할 수 있게 해주는 패키지
  "webpack": "^5.67.0"                                  // CRA 기본 컴파일러
},
"dependencies": {
  "@ant-design/icons": "^4.7.0",                        // 이미지 아이콘 패키지
  "@testing-library/jest-dom": "^5.14.1",               // testing library jest-dom 플러그인
  "@testing-library/react": "^12.0.0",                  // testing library react 플러그인
  "@testing-library/user-event": "^13.2.1",             // testing library 사용자 관점 이벤트 플러그인
  "@types/jest": "^27.0.1",                             // test코드 작성할 때 필요한 jest 플러그인
  "@types/node": "^16.7.13",                            
  "@types/react": "^17.0.20",                           
  "@types/react-dom": "^17.0.9",
  "antd": "^4.18.5",                                    // UI 패키지
  "antd-dayjs-webpack-plugin": "^1.0.6",                // antd 패키지의 날짜 포맷을 moment에서 dayjs로 호환되게 변경해줄 수 있는 플러그인
  "dayjs": "^1.10.7",                                   // 저용량 날짜 포맷터
  "react": "^17.0.2",
  "react-dom": "^17.0.2",
  "react-scripts": "^5.0.0",
  "typescript": "^4.4.2",
  "web-vitals": "^2.1.0"                                // 성능 체크용 라이브러리 (CRA 기본 패키지)
},
...
```

# 다른 프로젝트에서 패키지 설치하기

타 프로젝트에서 해당 프로젝트의 UI를 사용하기 위해선 설치하기전에 사전 작업을 해야 합니다. 본 섹션에선 **[프로젝트 내려받기](https://github.com/isos-consulting/fe-take-over/assets/49608580/6aeadadd-aaee-4565-86a5-11454afb0fc3)** 섹션을 통해 이미 계정 설정을 마친 상태라고 가정하고 진행하겠습니다.
isos-ui 패키지가 설치될 프로젝트 root폴더에 .npmrc를 파일을 생성하고 아래의 내용을 삽입하여 저장합니다.

```
registry=https://isos-557471975685.d.codeartifact.ap-northeast-1.amazonaws.com/npm/isos-ui/
//isos-557471975685.d.codeartifact.ap-northeast-1.amazonaws.com/npm/isos-ui/:always-auth=true
//isos-557471975685.d.codeartifact.ap-northeast-1.amazonaws.com/npm/isos-ui/:_authToken=${CODEARTIFACT_AUTH_TOKEN}
```

.npmrc 파일을 생성하였다면 아래 명령어를 참고해 패키지를 설치해봅시다.

Npm : 

```powershell
npm install @isos/isos-ui
```

Yarn : 

```powershell
yarn add @isos/isos-ui
```

설치를 마쳤다면 이제 미리 만들어진 컴포넌트를 import하여 사용할 수 있습니다.

# 패키지 업데이트 방법 (publish)

기본적으로 패키지를 업데이트 하려면 프로젝트 내의 package.json에서 version을 수정한 후 아래 명령어를 수행하면 됩니다.

```powershell
> npm publish
```

하지만 isos-ui 프로젝트는 AWS에 **파이프라인**이 설정되어 있기 때문에 push를 수행하면 빌드부터 퍼블리시까지 자동으로 수행하므로 따로 퍼블리시를 하는 것보단 리포지토리와 퍼블리시의 동기를 맞추기위해 git push를 하는 것이 좋습니다.

# 패키지 버전을 삭제하는 방법

패키지 버전을 잘못 등록한 경우가 발생할 수 있습니다. 이럴땐 AWS 코드 아티팩트에 접속한 후 isos-ui 리포지토리에 들어갑니다. 패키지 검색창에 `@isos/isos-ui` 를 입력한 후 상세 정보에 들어가면 퍼블리시된 버전 이력을 확인할 수 있습니다.

삭제할 버전을 선택한 후 삭제 버튼을 누르면 됩니다.

![Untitled](https://github.com/isos-consulting/fe-take-over/assets/49608580/3216480c-2760-48ce-8369-3212b44f9b07)

# 프로젝트 유의사항

본 섹션에서는 UI를 만들 때 유의해야하는 항목에 대해 설명합니다. 본 프로젝트는 공용 UI를 제공하는 앱이기 때문에 아래 사항을 숙지한 후 작업에 임하도록 합니다.

### UI를 추가하기 전에 신중하게 고민해보기

isos-ui는 타 프로젝트에서도 사용되는 공용 프로젝트이기 때문에 팀원들과 먼저 상의를 마친 후에 작업을 진행해야 합니다. 상의할 때 중복된 컴포넌트가 이미 있는지, 정말 필요한 UI인지, 공용으로 제공해도 되는 UI인지, 여러 측면에서 살펴보는 것이 좋습니다.

### 변경점이 생기면 공유하기

프로젝트에 변경점이 생겼다면 해당 프로젝트를 사용중인 모든 사람들에게 내용을 공유하는 것이 좋습니다. 프로젝트를 수정해야 한다면 내용 공유를 먼저 진행한 후 작업에 들어가도록 합시다.

# 문제점

본 프로젝트의 문제점을 정리한 섹션입니다. 해당 프로젝트에서 발견된 오류 사항을 모아봤습니다.

### 유틸 함수가 export되고 있습니다.

현재 ISOS-UTIL 패키지가 따로 운영되고 있지 않기 때문에 util함수는 각 프로젝트 마다 가지고 있는 상황입니다. 타 프로젝트들도 각자의 유틸 함수를 가지고 있기 때문에 본 프로젝트에서 사용하는 유틸 함수는 export되지 못 하도록 설정해야 합니다.

![패키지 내부의 유틸 함수를 사용하자 발생한 오류 사진](https://github.com/isos-consulting/fe-take-over/assets/49608580/6f948f83-07d5-400f-8562-f1d07a1baaf4)

패키지 내부의 유틸 함수를 사용하자 발생한 오류 사진

### yarn test 명령어를 실행하면 에러가 발생합니다.

타 프로젝트에서 isos-ui 패키지를 설치하고 yarn test를 수행하면 다음과 같은 Card 컴포넌트 관련 에러가 발생하여 테스트를 수행할 수 없습니다.

![yarn test를 실행하자 발생한 오류 사진](https://github.com/isos-consulting/fe-take-over/assets/49608580/691c665c-000b-4674-8d78-fc0f32f9cd59)

yarn test를 실행하자 발생한 오류 사진
