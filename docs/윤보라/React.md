# 개요

React는 SPA(Single Page Application) 특성의 사용자 인터페이스를 개발하기 위한 자바스크립트의 라이브러리입니다. Facebook에서 주도하여 개발되었습니다. React 자체만으로는 프레임워크 기준에 부합하지 않기 때문에 라이브러리라고 불리지만 다른 라이브러리와 함께 사용하기에 효율적입니다. 이렇게 라이브러리와 라이브러리가 결합된 거대한 React 생태계를 프레임워크라고 부릅니다.

React의 특징은 아래와 같습니다.

## 특징

- **여러 요소를 하나의 컴포넌트로 묶어서 관리할 수 있다.** 여러 요소를 묶어 하나의 이름으로 명명하여 사용할 수 있습니다. 작성된 코드를 컴포넌트로 재사용할 수 있다는 특징이 있습니다.
- **단방향 데이터 바인딩 특성을 가진다.** 데이터 방향이 한 방향으로만 흐릅니다. 자식이 부모의 데이터를 변경하려면 state를 사용해야 합니다.
- **가상 돔(Virtual DOM)을 사용하여 렌더링한다.** 가상 돔을 사용하여 속도와 성능을 개선한 방식입니다. (작동원리 섹션 참고)

## 작동 원리

가상 돔을 사용해 실제 DOM에 접근합니다. 렌더링이 발생되면 가상 돔이 이전 상태의 UI를 메모리에 기록한 상태에서 변경이 발생된 부분의 최소 단위 집합 부분만 메모리를 변경합니다. 이러한 동작을 `ReactDOM.render()`가 수행합니다.

<aside>
💡 자세한 내용은 공식 문서의 ‘재조정(Reconciliation)’ 항목을 참고하세요.

[재조정 (Reconciliation) - React](https://ko.reactjs.org/docs/reconciliation.html)

</aside>

# 기본 개념

리액트에서 손꼽히는 주요 개념에 대해 기술하였습니다.

## JSX

자바스크립트 확장 문법입니다. XML과 유사하게 생겼습니다. 주로 react, vue에서 사용합니다.

<aside>
💡 자세한 내용은 공식 문서의 ‘JSX 소개’ 항목을 참고하세요.

[JSX 소개 - React](https://ko.reactjs.org/docs/introducing-jsx.html)

</aside>

## Props

프로퍼티(properties)의 줄임말로, 컴포넌트 객체의 인수 값을 의미합니다. 상위 컴포넌트가 하위 컴포넌트한테 데이터를 전달할 때 사용합니다. props의 값은 변경될 수 없으며(읽기전용), 상위 컴포넌트로부터 받은 값은 state를 통해 변경할 수 있습니다.

<aside>
💡 자세한 내용은 공식 문서의 'Components와 Props’ 항목을 참고하세요.

[Components와 Props - React](https://ko.reactjs.org/docs/components-and-props.html)

</aside>

## State

컴포넌트 내에서 변경된 데이터를 관리하기 위한 상태 값을 의미합니다. props와 다르게 수정이 가능하며, 모든 컴포넌트는 독립적으로 state를 가질 수 있습니다. props와 공통된 점은 렌더링 결과물에 영향을 주는 정보를 가지고 있다는 특징에 있습니다.

<aside>
💡 자세한 내용은 공식 문서의 ‘컴포넌트 State’ 항목을 참고하세요.

[컴포넌트 State - React](https://ko.reactjs.org/docs/faq-state.html)

</aside>

# 상태 관리

상태 값은 웹을 렌더링할 때 영향을 미치는 값을 의미합니다. 상태 관리는 다르게 말하면 `**렌더링을 컨트롤하기 위한 정보들을 관리하는 것**`으로도 볼 수 있습니다. 상태 관리에 신경 쓰지 않으면 불필요한 렌더링이 발생해 성능에 영향을 주거나, 원치 않은 순간에 렌더링에 발생되어 결과를 다르게 보여주는 등의 문제를 초래할 수 있습니다.

웹앱을 구성하다 보면 React에서 기본으로 제공해주는 `useState` `useReducer` `useRef` 만으로는 관리가 복잡해질 수 있습니다. 이런 경우 사용하는 것이 Redux, mobx, 등등의 상태관리 라이브러리입니다. (본 문서에서 상태관리에 대한 라이브러리는 다루지 않습니다.)

React는 단반향 데이터 바인딩이라는 특징을 가지고 있는 만큼 부모가 자식에게 데이터를 전달하는 것은 가능하나, 자식이 부모에게 데이터를 물려줄 수는 없습니다. 이러한 특징에 맞게 주로 거론되는 문제는 전역 상태에 대한 관리 방법입니다.

## 전역 상태 관리

전역 상태를 관리하기 위한 방법으로는 두 가지가 있습니다.

1. React가 제공하는 ContextAPI 사용하기
2. 다른 상태관리 라이브러리 사용하기

본 섹션에선 상태관리 라이브러리에 다루지 않으므로 Context API에 관해서만 설명하겠습니다.

Context API는 React에서 제공해주는 전역 상태 관리 도구입니다. 전역 데이터를 위치 상관 없이 Context라는 공간에 저장해놓고 어디서든 불러와 사용할 수 있습니다.

![Context의 개념 사진](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44fe80fe-67ea-4461-8fb1-65b4ed907c12/Untitled.png)

Context의 개념 사진

최상위(root) 컴포넌트에 provider를 선언해두면 consumer를 사용하여 어디서든 실제 데이터를 사용할 수 있습니다. context는 주로 유저 정보, 테마, 언어를 설정할 때 활용됩니다.

<aside>
💡 Context에 대한 자세한 설명은 공식 문서 ‘Context’ 항목을 참고하세요.

[Context - React](https://ko.reactjs.org/docs/context.html)

</aside>

## 리렌더링 방지

React에선 원치 않은 리렌더링을 방지할 수 있습니다. 리렌더링을 방지하여 원하는 결과를 도출하거나 성능을 개선 시킬 수 있습니다. 리렌더링을 컨트롤 하기 위한 방법은 두 가지가 있습니다.

1. `useMemo` 사용하기
2. `useRef` 사용하기

`useMemo`는 컴포넌트를 기준으로 리렌더링을 관리합니다. props의 값이 변경되지 않았을 때, 동일한 입력이 발생된 경우 렌더링이 되지 않도록 할 수 있습니다.

<aside>
💡 자세한 내용은 아래 링크를 참고하세요.

[React Hooks: useMemo 사용법](https://www.daleseo.com/react-hooks-use-memo/)

</aside>

state를 사용하면 렌더링이 발생합니다. 하지만 렌더링이 발생할 때 값은 유지되면서 렌더링은 발생 시키고 싶지 않을 때가 있습니다. 이럴 때 사용하는 것이 `useRef` 입니다.

`useRef`를 사용해 레퍼런스 값을 사용하면 리렌더링을 발생 시키지 않으면서 값은 유지 시키며 핸들링 할 수 있습니다. 또한 특정 조건에 따라 렌더링이 발생되도록 만들 수도 있습니다.

<aside>
💡 자세한 내용은 아래 링크를 참고하세요.

[React Hooks: useRef 사용법](https://www.daleseo.com/react-hooks-use-ref/)

</aside>

# 훅

함수형 컴포넌트에서 사용할 수 있는 기술입니다. 기존 클래스형 컴포넌트가 가지고 있던 state와 라이프 사이클을 동일하게 구현할 수 있습니다. 컴포넌트 최상단에서만 선언할 수 있다는 특징을 가지고 있습니다.

## 커스텀 훅

상태 로직을 재사용할 때 사용합니다. 평소 많이 사용하는 `useState` `useRef` `useEffect`와 마찬가지로 어디서든 재사용 가능한 직접 만든 훅을 의미합니다.

커스텀 훅을 만드는 방법은 간단합니다. 함수를 만들고 함수 내에서 state를 선언하고, state를 사용할 때 핸들링할 함수를 생성해주면 끝입니다.

예제는 아래 링크를 참고하세요.

[React.js - 커스텀 훅 만들기](https://kyounghwan01.github.io/blog/React/custome-hook/#%E1%84%89%E1%85%A1%E1%86%BC%E1%84%92%E1%85%AA%E1%86%BC)

# 환경 구축

CRA를 사용하면 React 환경 프로젝트를 쉽게 구축할 수 있습니다.

준비물: [node](https://nodejs.org/ko/download/)

1. 프로젝트 이름의 폴더 생성합니다.
2. 명령프롬포트에서 프로젝트 폴더로 이동합니다.
3. 아래 명령어 실행합니다.

```powershell
npx create-react-app [프로젝트명]
```

아래처럼 파일이 생성되면 성공입니다.

![CRA(Create-React-App) 결과](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5f5c168e-babd-44fd-bbd7-d7df490adaa3/Untitled.png)

CRA(Create-React-App) 결과

## 구성

- **node_modules** : 패키지 폴더들이 모여있는 폴더입니다.
- **public** : 웹 서버에서 실행할 index파일이 들어 있습니다.
- **src** : 실제 사용될 리소스 파일이 들어갈 폴더입니다. 기본적으론 App.jsx, index.js, App.css가 있습니다. index.js는 자바스크립트 파일 시작점입니다.
- **package.json** : 프로젝트 이름과 라이센스 정보, 스크립트 명령어 정보와 종속된 패키지 정보가 들어 있습니다.

<aside>
💡 CRA 공식 사이트

[Create React App](https://create-react-app.dev/)

</aside>

# 유의사항

리액트로 작업할 때 유의해야할 사항들을 기재해놓은 섹션입니다.

- **훅은 컴포넌트내 최상위에서 선언할 것.** 훅은 무조건 컴포넌트 내 최상위 위치에서만 선언 가능합니다. 함수 안에 선언이 불가능하므로 사용 시 주의하세요.
- **useState와 useRef를 적절히 섞어서 활용할 것.** state만 사용하면 리렌더링을 관리하기 힘들어집니다. 렌더링을 발생 시키지 않을 거라면 useRef를 사용해서 상태 값을 관리하세요.
- **절대경로를 적용할 땐 신중히 작업할 것.** 설정할 때 뭔가 하나라도 빠지면 컴파일할 때도, import할 때도 예상치 못한 오류를 발생 시킬 확률이 높습니다.
- **side effect안에 setState 넣지 말 것.** 이건 경우에 따라선 넣어야 될 수 있지만 만약 넣더라도 한번 더 생각해보세요. 그게 effect로 상태 값을 변경해야 할 작업일까요? 그 방법 밖에 없다면 side effect가 상태 값을 핸들링 하게 되는 건 그거 하나만 되도록 만드세요. 여러 개의 state가 effect의 영향을 받게 되면 상태 관리가 매우 복잡해질 가능성이 높습니다.

# 무료 자습서

[자습서: React 시작하기 - React](https://ko.reactjs.org/tutorial/tutorial.html)

[기초부터 배우는 React - Part 1](https://berkbach.com/%EA%B8%B0%EC%B4%88%EB%B6%80%ED%84%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-react-js-1531b18f7bb2)

https://github.com/woochanleee/Lets-Share

[초보 리액트 개발자를 위한 팁 13가지](https://sumini.dev/guide/006-tips-for-frontend-beginner/)
