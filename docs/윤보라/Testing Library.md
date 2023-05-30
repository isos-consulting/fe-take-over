# 개요

컴포넌트를 테스트할 수 있는 라이브러리입니다. 행위 주도 테스트(Behavior Driven Test)가 대두 되면서 같이 주목 받게 되었습니다. 리액트에서 주로 사용하지만 리액트에서만 사용되는 것은 아닙니다. 테스팅 라이브러리는 jest와 같이 사용되는 경우가 많습니다.

테스팅 라이브러리는 실제 DOM 노드를 사용하여 테스트 한다는 것이 가장 큰 특징입니다. 이는 실제 사용자가 보는 것과 유사한 환경에서 테스트를 한다는 것을 의미합니다. 테스트는 실제 환경과 비슷할 수록 신뢰할 수 있습니다.

테스팅 라이브러리의 특징을 한눈에 정리하면 아래와 같습니다.

## 특징

- **실제 DOM 노드 환경을 사용한다.** 실제 DOM 노드 환경에서 사용 가능한건 react-dom에서 동작하기 때문입니다. 위에서 설명한 대로 사용자가 경험하는 상황과 비슷하게 테스트 케이스를 작성할 수 있습니다.
- **사용자 관점으로 테스트를 진행한다.** 테스팅 라이브러리를 사용할 땐 props나 state값이 변경되는 것에 대한 테스트는 중요하지 않습니다. 사용자가 보는 DOM에 영향을 미치는 가가 중요합니다. 실제 사용자가 보고 행동하는 작업을 테스트할 수 있도록 설계되었기 때문입니다. 이는 사용자 위주로 테스트를 해야 한다는 테스팅 라이브러리의 설계 이념과 잘 맞습니다. 그래서 라이브러리의 기능들을 보면 사용자가 DOM을 사용할 때랑 유사한 방식으로 테스트할 수 있는 기능들이 제공됩니다.

# 기본 개념

테스트를 작성하기 위해 기본적으로 알아야 할 주요 개념들을 정리하였습니다.

## describe

테스트 묶음 단위입니다. 여러 테스트를 묶어서 그룹을 만들 수 있습니다.

## test & it

테스트 단위입니다. 개별 테스트를 수행할 때 사용합니다. test와 it에 기능 및 성능에 대한 차이점은 없습니다.

## render

테스트를 위해 컴포넌트를 DOM에 렌더링할 때 사용하는 함수입니다.

## expect

값을 검증할 때 사용하기 위한 함수입니다.

## getBy~

DOM 요소를 가져오기 위해 사용하는 메서드입니다. 일치하는 요소가 없으면 오류를 반환합니다.

## queryBy~

getBy와 유사합니다. 일치하는 요소가 없으면 null을 반환합니다.

## findBy~

getBy와 유사합니다. 요소가 발견되면 Promise를 반환합니다. 비동기 테스트할 때 사용합니다. 요소가 발견되지 않거나 기본 제한 시간인 1000ms가 초과되면 Promise가 거부됩니다.

## waitFor

특정 시간 동안 기다릴 때 사용합니다. 타임 아웃에 도달할 때까지 콜백을 정해진 숫자 만큼 실행합니다.

## **waitForElementToBeRemoved**

DOM에서 Element가 제거 될 때까지 기다릴 때 사용합니다.

## fireEvent

사용자 액션 함수입니다. DOM에서 이벤트를 발생 시키기 위해 사용합니다. `@testing-library/user-event` 에서 import하여 사용할 수 있습니다.

## createEvent

커스텀 이벤트를 만드는 함수입니다.

## only

테스트를 실행할 때 only()가 있는 테스트 케이스가 있으면 오직 그 케이스만 테스트합니다.

```jsx
test.only("run only", () => {
  // 이 테스트 함수만 실행됨
});

test("not run", () => {
  // 실행 안됨
});
```

## skip

테스트를 실행할 때 skip()가 있는 테스트 케이스는 테스트 대상에서 제외합니다.

```jsx
test.skip("skip", () => {
  // 이 테스트 함수는 제외됨
});

test("run", () => {
  // 실행됨
});
```

<aside>
💡 더 자세한 내용은 아래 링크를 참고하세요.

[About Queries | Testing Library](https://testing-library.com/docs/queries/about)

</aside>

# 환경 구축

CRA 환경으로 리액트 환경을 구축한 경우, 테스팅 라이브러리도 같이 설치됩니다. 여기선 CRA가 아닌 기존 리액트 환경에서 테스트 환경을 구축하는 방법에 대해 기술하겠습니다.

테스트를 하려면 아래에서 환경에 맞게 패키지를 설치해야 합니다. 

## React 환경에서 테스트 환경 구축하기

아래 명시된 패키지를 설치해야 합니다.

- @testing-library/react
- @testing-library/user-event
- @testing-library/jest-dom

<aside>
💡 한번에 설치하기
npm :

```powershell
npm install @testing-library/react @testing-library/user-event @testing-library/jest-dom
```

yarn :

```powershell
yarn add @testing-library/react @testing-library/user-event @testing-library/jest-dom
```

</aside>

이제 xxx.test.js 또는 xxx.test.jsx 파일을 만든 후 테스트를 진행할 수 있습니다.

## Typescript 환경에서 테스트 환경 구축하기

[React 환경에 테스트 환경 구축하기](https://www.notion.so/Testing-Library-c2e0fc72d61c45e0a39b2cb5d6a40bef) 섹션에서 필요한 패키지를 모두 설치한 후 추가로 아래 명시된 패키지를 설치해야 합니다.

- @types/jest

<aside>
💡 설치하기
npm :

```powershell
npm install @types/jest
```

yarn :

```powershell
yarn add @types/jest
```

</aside>

이제 xxx.test.ts 또는 xxx.test.tsx 파일을 만들어 테스트를 수행하면 됩니다.

## 테스트 파일 인식

테스트를 하려면 일반 파일과 테스트 파일을 구분하여 만들어줘야 합니다. 두 파일을 구분하는 방법은 두 가지가 있습니다. 

1. **파일명에 test 붙이기** : 파일명과 확장자 사이에 test를 넣으면 자동으로 테스트 파일로 인식됩니다. (예시: xxx.test.jsx)
2. **`__test__` 폴더 만들기** : 테스트 폴더를 만들어 모아둘 수도 있습니다. `__test__` 이 이름의 폴더가 있으면 하위 파일들을 모두 테스트 파일로 인식합니다.

# 명령어

`npm test` 또는 `yarn test` 를 입력하여 테스트를 시작할 수 있습니다. test 명령어를 수행할 때 특별한 옵션을 붙여서 편리하게 테스트를 수행할 수 있습니다.

## 특정 파일만 테스트하기

경우에 따라 특정 이름을 가진 파일만 테스트를 해야 할 수 있습니다. 

한 가지 파일만 테스트하려면 아래처럼 파일 명을 같이 입력합니다.

```powershell
npm test src/pages/std/factory.test.tsx
```

파일 명으로 패턴을 걸러면 `--`옵션을 사용합니다.

```powershell
npm test -- factory
```

이러면 이름에 factory가 들어간 테스트 파일들을 모두 실행합니다.

아니면 테스트가 실행 중일 때 패턴을 걸 수도 있습니다.

```powershell
Test Suites: 16 passed, 16 total
Tests:       98 passed, 98 total
Snapshots:   0 total
Time:        5.048s
Ran all test suites.

Watch Usage: Press w to show more.
```

이 상황에서 `w`를 눌러 메뉴를 엽니다.

```powershell
Watch Usage
 › Press f to run only failed tests.
 › Press o to only run tests related to changed files.
 › Press q to quit watch mode.
 › Press p to filter by a filename regex pattern.
 › Press t to filter by a test name regex pattern.
 › Press Enter to trigger a test run.
```

여기서 `p`를 누르면 파일 명으로 패턴을 걸 수 있고, `t`를 누르면 테스트 명으로 패턴을 걸 수 있습니다. 로그인 파일만 테스트하겠다고 가정하고 `p`를 눌러보도록 하겠습니다.

```powershell
Pattern Mode Usage
 › Press Esc to exit pattern mode.
 › Press Enter to filter by a filenames regex pattern.

 pattern ›

 Start typing to filter by a filename regex pattern.
```

걸고 싶은 패턴을 입력합니다.

```jsx
Pattern Mode Usage
 › Press Esc to exit pattern mode.
 › Press Enter to filter by a filenames regex pattern.

 pattern › std/factory

 Pattern matches 1 file
 › src/pages/std/factory.test.jsx
```

이렇게 입력하면 std 폴더에 있는 factory라는 이름을 가진 파일들만 테스트를 수행하게 됩니다.

## 감시 기준 정하기

테스트를 할 때 `--watch` 옵션과 `--watchAll` 옵션을 사용할 수 있습니다. `--watch`는 파일에 변경이 발생하면 그 파일만 다시 테스트하는 옵션이고 `--watchAll`는 모든 파일을 테스트하는 옵션입니다. 상황에 맞춰 사용하면 됩니다.

```powershell
npm test --watch
npm test --watchAll
```

# 반복되는 구문 설정하기

테스트를 작성하다 보면 테스트 케이스마다 반복되는 구문이 생길 수 있습니다. 이런 경우 `beforeEach()` 와 `afterEach()`를 사용하면 모든 테스트 케이스를 실행하기 전, 또는 후에 같은 구문을 실행하게 만들 수 있습니다.

**before**

```jsx
test("find all users", () => {
  data.users.push(
    { id: 1, email: "user1@test.com" },
    { id: 2, email: "user2@test.com" },
    { id: 3, email: "user3@test.com" }
  );

  const users = userService.findAll();

  expect(users).toHaveLength(3);
  expect(users).toContainEqual({ id: 1, email: "user1@test.com" });
  expect(users).toContainEqual({ id: 2, email: "user2@test.com" });
  expect(users).toContainEqual({ id: 3, email: "user3@test.com" });
});

test("destory a user", () => {
  data.users.push(
    { id: 1, email: "user1@test.com" },
    { id: 2, email: "user2@test.com" },
    { id: 3, email: "user3@test.com" }
  );

  const id = 3;
  const user = data.users.find((user) => user.id === id);

  userService.destroy(id);

  expect(data.users).toHaveLength(2);
  expect(data.users).not.toContainEqual(user);
});
```

**after**

```jsx
beforeEach(() => {
  data.users.push(
    { id: 1, email: "user1@test.com" },
    { id: 2, email: "user2@test.com" },
    { id: 3, email: "user3@test.com" }
  );
});

test("find all users", () => {
  const users = userService.findAll();

  expect(users).toHaveLength(3);
  expect(users).toContainEqual({ id: 1, email: "user1@test.com" });
  expect(users).toContainEqual({ id: 2, email: "user2@test.com" });
  expect(users).toContainEqual({ id: 3, email: "user3@test.com" });
});

test("destory a user", () => {
  const id = 3;
  const user = data.users.find((user) => user.id === id);

  userService.destroy(id);

  expect(data.users).toHaveLength(2);
  expect(data.users).not.toContainEqual(user);
});
```

# act()를 사용하여 가상DOM에 적용하기

`act()`는 인자 값으로 함수를 받습니다. 해당 함수를 실행시켜 DOM에 적용시킵니다. `act()` 이후에 작성되는 구문들은 이미 DOM에 `act()`의 인자가 실행되었다고 가정하고 작성하게 됩니다.

```jsx
test('테스트', () => {
  act(() => {
    // DOM에 반영하고 싶은 코드들
    // 예. ReactDOM.render(<Counter />, container);
  });
  
	// `DOM에 반영하고 싶은 코드들`이 DOM에 반영되었다고 가정하고 테스트할 코드들...
});
```

# 무료 자습서

[테스팅 개요 - React](https://ko.reactjs.org/docs/testing.html)

[[번역] 초보자를 위한 React 어플리케이션 테스트 심층 가이드 (1)](https://blog.rhostem.com/posts/2020-10-14-beginners-guide-to-testing-react-1)
