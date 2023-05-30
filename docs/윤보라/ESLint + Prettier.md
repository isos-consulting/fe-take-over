# 개요

ESLint는 자바스크립트에서 소스코드를 작성할 때 문법의 오류를 캐치하거나 적절하지 않은 구조에 대한 메시지를 표시해주는 개발 도구입니다. 코드 작성에 대한 규약이 있을 때 ESLint를 사용하면 협업할 때 큰 도움이 될 수 있습니다.

Prettier는 정해진 코드 스타일 가이드라인을 작성할 수 있게 도와주는 도구입니다. prettier를 사용하면 정해진 설정에 맞게 문법 스타일을 자동으로 변경할 수 있습니다.

eslint와 prettier는 세트로 사용되는 경우가 많습니다.

# 기본 개념

## Lint

문법의 오류나 적절하지 못한 구조를 잡아주는 행위

## Linter

lint 동작을 도와주는 도구

## ESLint

자바스크립트에 사용하는 Linter, 과거엔 `JSLint`, `JSHint`, `TSLint`가 사용됐었으나 `ESLint`로 통합되었다.

## Formatter

정해진 코드 스타일 가이드라인(공백, 띄어쓰기, 탭 등등... 텍스트 작성 기준)에 따라 작성된 코드를 변환해주는 도구

## Prettier

Formatter의 종류

# 환경 구축

## 설치하기

lint를 실행하기 위해 `eslint` 패키지를 설치합니다.

**npm** : 

```jsx
npm install eslint
```

**yarn** :

```jsx
yarn add eslint
```

패키지를 설치한다고 lint가 실행되진 않습니다. 워크스페이스에 eslint 플러그인까지 설치해줘야 제대로 동작합니다. react코드를 Visual studio code에서 작업한다고 가정하고 확장프로그램을 설치하겠습니다.

vscode에서 eslint 확장 프로그램을 설치합니다.

[ESLint - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

prettier는 적용하는 방법이 두 가지가 있습니다.

1. **워크스페이스에만 설치한다.**
2. **패키지를 설치해서 .eslintrc에 적용한다.**

1번 방법은 확장 프로그램을 설치하는 것으로 끝납니다.

[Prettier - Code formatter - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

2번 방법은 eslint처럼 `prettier` 패키지를 설치합니다.

**npm** : 

```jsx
npm install prettier
```

**yarn** :

```jsx
yarn add prettier
```

<aside>
💡 eslint와 prettier를 같이 사용하는 경우는 충돌을 방지시켜주는 패키지도 설치해야 합니다.

- **eslint-plugin-prettier** : eslint와 prettier가 충돌될 수 있는 설정들을 비활성화 합니다.
- **eslint-config-prettier** : eslint의 포맷이 아닌 prettier의 포맷 기능을 사용하게 합니다.

**npm** : 

```jsx
npm install eslint-plugin-prettier eslint-config-prettier --save-dev
```

**yarn** :

```jsx
yarn add --save-dev eslint-plugin-prettier eslint-config-prettier --save-dev
```

</aside>

패키지를 설치한 후 .eslintrc에 다음과 같은 설정을 부여합니다.

**.eslintrc**

```jsx
{
  "extends": ["plugin:prettier/recommended"]
}
```

마지막으로 [설정 파일](https://www.notion.so/ESLint-Prettier-2716aa44903b44079c1fbca936f4b791) 섹션을 참고해 .prettierrc 파일을 만들어 설정을 적용합니다.

<aside>
🤔 1, 2번 방법을 모두 사용하면 안되나요?
 - **해도 됩니다.** 그러나 적용되는 우선순위가 다르기 때문에 설정할 때 혼란을 겪을 수 있습니다.

확장 프로그램만 설치된 경우 vscode를 통해서 설정하는 것도, `.prettierrc` 파일을 통해 설정하는 것도 가능합니다. 하지만 `.prettierrc` 파일이 존재하면 vscode 설정은 무시되고 무조건 `.prettierrc`설정만 적용됩니다. 거기에 패키지를 설치한 경우엔 `.prettierrc` 파일이 없으면 동작되지 않기 때문에 이러한 우선순위 차이만 이해한다면 아무런 문제가 되지 않습니다.

</aside>

패키지 설치 + 확장 프로그램 설치까지 맞췄다면 다음은 설정 파일을 다뤄봅시다.

## 설정 파일

각 패키지에 대한 설정은 `.eslintrc` `.prettierrc`에서 이루어집니다.

**.eslintrc**

```json
{
  // 코드 포맷을 prettier로 설정
  "plugins": [
    "prettier"
  ],

  // eslint의 룰을 기본 권장설정으로 설정
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ],

  // 코드를 해석하는 parser에 대한 설정
  "parserOptions": {
    // 자바스크립트 버전, 7은 ECMA2016
    "ecmaVersion": 7,
    // 모듈 export를 위해 import, export를 사용 가능여부를 설정, script는 사용불가
    "sourceType": "script",
    // jsx 허용을 설정, back-end 설정이기 때문에 사용 안함
    "ecmaFeatures": {
      "jsx": false
    }
  },

  // linter가 파일을 분석할 때, 미리 정의된 전역변수에 무엇이 있는지 명시하는 속성
  "env": {
    // 브라우저의 document와 같은 객체 사용 여부
    "browser": false,
    // node.js에서 console과 같은 전역변수 사용 여부
    "node": true
  },
  // ESLint가 무시할 디렉토리, 파일을 설정
  "ignorePatterns": [
    "node_modules/"
  ],

  // ESLint 룰을 설정
  "rules": {
    // prettier에 맞게 룰을 설정
    "prettier/prettier": "error"
  }
}
```

**.prettierrc**
```json
{
  // 객체, 배열 등에서 항상 마지막에 , 를 붙인다.
  "trailingComma": "es5",

  // 들여쓰기 할 때, 기본 폭을 설정한다.
  "tabWidth": 2,

  // 모든 구문에 세미콜론을 붙인다.
  "semi": true,

  // 따옴표는 홑따옴표를 사용한다.
  "singleQuote": true
}
```

<aside>
💡 더 많은 속성을 확인하려면 각 공식 문서를 확인하세요.
  
https://eslint.org/docs/latest/use/configure/
  
https://prettier.io/docs/en/options.html
</aside>
