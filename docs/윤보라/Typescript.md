# 개요

Typescript는 javascript에 타입을 부여한 언어입니다. 마이크로소프트에서 개발되었습니다. 목적에 맞지 않는 타입의 변수나 함수에 에러를 발생 시켜 런타임 중에 발생될 수 있는 오류를 사전에 차단하는 역할을 합니다. 타입 스크립트로 짜여진 코드는 컴파일 후 다시 자바스크립트 언어로 변환됩니다. 때문에 기존 자바스크립트 코드도 같이 사용 가능합니다.

## 특징

- **정적 타입의 컴파일 언어다.** 자바스크립트는 인터프리터 언어기 때문에 실행을 한 후 직접 사용해보기 전까진 오류를 알 수 없는 경우가 많습니다. 반면 타입스크립트는 컴파일러가 오류를 잡아주는 차이점이 있습니다.
- **자바스크립트의 슈퍼셋이다.** 타입스크립트는 자바스크립트의 확장 언어입니다. js에서 ts로 변환해 컴파일하여 실행할 수 있습니다.
- **객체 지향 프로그래밍 지원한다.** ES6문법을 지원하여 객체 지향 코딩을 할 수 있는 패턴들을 제공합니다. `class` `interface` `instance` `module` 등등..

# 기본 개념

타입스크립트에는 interface와 type을 작성할 수 있습니다. interface와 type의 기능은 유사하지만 몇 가지 차이점이 있습니다.

## interface와 type의 차이점

- **type은 이름을 중복해서 사용할 수 없지만 interface는 가능하다.** interface는 선언적으로 확장이 가능하지만 type은 불가능하기 때문입니다.
- **interface는 객체만 사용 가능하다.** type처럼 리터럴 타입(string, boolean 등)을 정의할 수 없습니다.
- **interface는 computed value(계산된 값)를 사용할 수 없다.** type에선 가능하지만 interface는 불가능합니다. 이는 아래 예시를 통해 확인할 수 있습니다.
    
    ```jsx
    type names = 'firstName' | 'lastName'
    
    type NameTypes = {
      [key in names]: string
    }
    
    const yc: NameTypes = { firstName: 'hi', lastName: 'yc' }
    
    interface NameInterface {
      // error
      [key in names]: string
    }
    ```
    

## 제네릭

한 가지 타입이 아닌 여러가지 타입에서 동작하는 컴포넌트를 생성할 때 사용합니다. 타입을 함수의 파라메터처럼 사용하는 것이 특징입니다.

```tsx
function getText<T>(text: T): T {
  return text;
}
```

위의 예시는 파라메터와 반환 타입이 같으며, 함수를 호출할 때 타입을 정의할 수 있습니다.

```tsx
const value:number = getText<number>('강낭콩'); // error
const value:number = getText<number>(123); // true
const value:boolean = getText<string>('해바라기'); // error
const value:string = getText<string>('해바라기'); // true
```

이처럼 여러 타입으로 동작하는 함수를 정의할 때 사용하는 것이 제네릭입니다.

<aside>
💡 제네릭에 대한 자세한 설명은 아래 링크를 참고하세요.

[제네릭 | 타입스크립트 핸드북](https://joshua1988.github.io/ts/guide/generics.html#%EC%A0%9C%EB%84%A4%EB%A6%AD-generics-%EC%9D%98-%EC%82%AC%EC%A0%84%EC%A0%81-%EC%A0%95%EC%9D%98)

</aside>

# 환경 구축

처음 프로젝트를 시작하는 단계에서 구축하는 방법은 CRA할 때 타입스크립트 옵션을 사용하는 방법이 있습니다.

1. 프로젝트명으로 폴더를 생성합니다.
2. 폴더 안에서 아래 명령어를 실행합니다.

```powershell
npx create-react-app [프로젝트명] --template typescript
```

아래와 같이 구성이 완료되면 성공입니다.

![CRA(Create-React-App) + typescript 명령 후 완료된 사진](https://github.com/isos-consulting/feto/assets/49608580/18d85a91-3789-4e64-b14f-74926ac72fef)

CRA(Create-React-App) + typescript 명령 후 완료된 사진

기존 리액트와 다른 점은 App파일이 tsx로 만들어졌다는 점, tsconfig.json 이라는 새로운 설정 파일이 추가되었다는 점이 있습니다.

## 구성

- **ts, tsx파일** 타입스크립트의 확장자 파일입니다. (js→ts, jsx→tsx)
- **tsconfig.json** 타입스크립트 설정 파일입니다. 이곳에서 타입 체크 범위를 설정과 기타 path, es문법 타입 등을 설정할 수 있습니다.

## React에서 Typescript로 마이그레이션

기존 React 프로젝트에서 Typescript로 마이그레이션 하기 위한 방법이 있습니다.

우선 아래에 명시된 목록의 패키지들을 설치해줍니다.

- **typescript** : 타입스크립트를 사용하기 위해 필요한 필수 패키지
- **@types/node** : typescript 2.x부터 필수로 설치해야 하는 패키지입니다. node에서 타입스크립트를 사용할 때 필요한 유형이 정의되어 있습니다.
- **@types/react** : react의 유형이 정의된 패키지
- **@types/react-dom** : react-dom의 유형이 정의된 패키지
- **@types/jest** : jest를 사용중인 경우에만 설치합니다.

<aside>
💡 한번에 설치하기

npm : 

```powershell
npm install typescript @types/node @types/react @types/react-dom @types/jest
```

yarn : 

```powershell
yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

</aside>

설치를 마쳤다면 마지막으로 `index.js` 파일을 `index.tsx`로 변경한 후 `npm start` 혹은 `yarn start` 실행하면 자동적으로 tsconfig.json 파일이 프로젝트 폴더에 생기면서 프로그램이 실행됩니다.

# tsconfig

타입스크립트 관련 설정을 할 수 있는 파일입니다. 주로 타입 체크 범위를 설정하거나 컴파일 옵션, js허용, 컴파일 시 자바스크립트 문법 설정 등을 할 수 있습니다.

## compilerOptions

컴파일 관련 설정을 하는 옵션입니다. 먼저 빌드와 관련된 주요 설정들이 있습니다.

- **target** : 자바스크립트로 컴파일할 때 어떤 버전의 자바스크립트 언어로 변경할지 선택하는 옵션입니다. (es5, es6 등등)
- **module** : import를 사용할 때 어떤 문법을 사용할지 결정하는 옵션입니다. `commonjs`는 require를 사용하고 `es2015`, `esnext`는 import를 사용합니다.
- **allowJs** : ts에서 js파일 import를 허용할 건지 설정합니다.
- **checkJs** : js파일에서 에러 체크를 할 것인지 설정합니다.
- **jsx** : tsx파일을 어떤 방식으로 컴파일 할 것인지 설정합니다. `preserve` `react` `react-native`
- **declaration** : 컴파일 후 .d.ts 파일을 자동으로 생성할 것인지 설정합니다.
- **outFile** : 단일 파일로 빌드할 때 사용할 파일 명을 설정합니다.
- **outDir** : js파일 빌드 폴더 위치를 설정합니다.
- **rootDir** : 루트 폴더 위치 설정 (경로를 변경하면 outDir에서 설정한 경로가 영향을 받습니다.)
- **removeComments** : 컴파일 시 주석을 소스에 포함 시키지 않습니다.
- **files** : 원하는 파일만 실행되게 설정합니다.
- **isolatedModules** : 각 파일들을 별도 모듈로 변환할지 설정합니다.
- **esModuleInterop** : import할 때 es6모듈에서 commonjs방식의 import를 허용할 지 설정합니다.

다음은 에러 체크에 관한 설정입니다.

- **strict** : 엄격모드 설정. strict와 관련된 모드를 전부 허용합니다.
- **noImplicitAny** : any 타입을 금지하는 설정입니다.
- **strictNullChecks** : null, undefiend 값 참조를 방지합니다.
- **strictFunctionTypes** : 함수의 파라메터 타입 체크를 강하게 합니다.
- **strictPropertyInitialization** : 클래스 값 초기화 할 때 타입을 엄격하게 합니다. (constructor)
- **noImplicitThis** : this가 any 타입일 경우 에러를 반환합니다.
- **alwaysStrict** : react의 strict 모드를 언제나 허용합니다.
- **noUnusedLocals** : 사용하지 않은 지역변수에 대한 오류를 보고합니다.
- **noUnusedParameters** : 사용하지 않은 파라메터에 대한 오류를 보고합니다.
- **noImplicitReturns** : 함수에 return이 없으면 오류를 보고합니다.
- **noFallthroughCasesInSwitch** : switch-case를 사용할 때 발생할 수 있는 오류에 대해 보고합니다.

<aside>
💡 더 많은 설정을 확인하려면 아래 링크를 참고하세요.

[TSConfig Reference - Docs on every TSConfig option](https://www.typescriptlang.org/tsconfig)

</aside>

# 무료 자습서

[1. 타입스크립트 연습](https://react.vlpt.us/using-typescript/01-practice.html)

[한눈에 보는 타입스크립트(updated)](https://heropy.blog/2020/01/27/typescript/)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

[Introduction](https://radlohead.gitbook.io/typescript-deep-dive/)

[올해 버려야 할 타입스크립트 나쁜 버릇 10가지](https://ui.toast.com/weekly-pick/ko_20210217)
