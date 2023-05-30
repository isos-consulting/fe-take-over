`본 문서는 스토리북 6버전을 기준으로 작성되었습니다.`

# 개요

스토리북은 UI 컴포넌트를 독립적으로 구현하고 테스트 할 수 있는 도구입니다. 개발된 UI를 보여주는 문서로 사용되기도 합니다. 프로젝트가 복잡하다면 스토리북을 사용하여 구성요소를 분리하는 방법도 도움 됩니다.
![Untitled](https://github.com/isos-consulting/feto/assets/49608580/e4f80b6f-5c51-42a9-a3b6-9013adbc660d)

## 특징

- **고립된 환경에서 컴포넌트를 작업할 수 있습니다.** 스토리북의 가장 큰 장점이기도 합니다. 컴포넌트를 분리된 작업 환경에서 비즈니스 로직, 데이터에 신경쓰지 않고 집중적으로 개발할 수 있습니다.
- **케이스별로 컴포넌트를 명시할 수 있습니다.** 하나의 컴포넌트가 특정 상황일 때 렌더링될 모습이 다르다면 이를 명시해야할 필요가 있을 수 있습니다. 스토리북은 하나의 컴포넌트를 여러 케이스로 나눈 메뉴를 구성하여 보여줄 수 있습니다.
- **UI의 변경점을 시각적으로 확인할 수 있습니다.** 본래 프로젝트에서 UI를 확인하려면 UI를 사용중인 페이지에서 확인하거나 따로 UI페이지를 만드는 작업을 거쳐, 별도의 작업을 통해 눈으로 확인해야 했지만 스토리북을 실행하면 UI만 바로 확인할 수 있기 때문에 즉각적으로 확인이 가능하다는 장점이 있습니다.
- **단위 테스트를 할 수 있습니다.** 컴포넌트 별로 따로 속성을 건드려보기도 하고 이벤트를 확인하기도 하며 테스트를 할 수 있기 때문에 컴포넌트에 대한 단위 테스트를 할 때 유용하게 사용할 수 있습니다.
- **매뉴얼로 사용할 수 있습니다.** 스토리북을 작성하는 것 그 자체만으로 매뉴얼로 활용할 수 있습니다. 프로젝트에서 사용하는 컴포넌트들을 명시하는 문서의 역할을 하기도 합니다.

# 환경 구축

스토리북 환경을 구축하기 위해선 어떤 패키지와 별도의 작업이 필요한지 알아봅시다. 스토리북을 구축하려면 기존 React 프로젝트가 이미 만들어진 상태에서 추가를 해주어야 합니다. CRA를 통해 구축한 환경에서 스토리북을 추가하는 방법과 별도의 다른 방법으로 구성한 React 프로젝트에서 추가하는 방법으로 나누어 설명하도록 하겠습니다.

## npx 명령어로 스토리북 환경 구축하기

가장 편한 방법입니다. CRA로 구축한 환경에서 스토리북 환경을 추가하려면 아래 명령어를 실행하면 됩니다.

```powershell
npx sb init
```

명령어를 실행하면 스토리북을 구성하기 위한 패키지와 폴더, js파일을 프로젝트에 추가합니다. 성공적으로 마무리되면 새로운 폴더가 생기게 됩니다. ([구성](https://www.notion.so/Storybook-6a882a93c1894183ad2586df709668f1) 섹션 참고)

`package.json`을 열어보면 `scripts` 항목에 새로운 명령어로 `storybook`이 추가되어 있습니다. 해당 명령어를 실행하여 스토리북이 정상적으로 작동되는지 확인할 수 있습니다.

**npm** : 

```powershell
npm run storybook
```

**yarn** : 

```powershell
yarn storybook
```

## 수동으로 스토리북 환경 구축하기

npx sb init 명령어를 통해서 스토리북 환경을 한번에 구축할 수 있긴 하지만 특별한 상황이라면 명령어가 제대로 수행되지 않을 수 있습니다. 이럴땐 수동으로 필요한 패키지를 설치하고 설정을 마쳐주면 해결할 수 있습니다.

스토리북이 구동되려면 아래에 명시된 패키지들이 필요합니다.

- @storybook/addon-actions
- @storybook/addon-essentials
- @storybook/addon-interactions
- @storybook/addon-links
- @storybook/builder-webpack5
- @storybook/manager-webpack5
- @storybook/node-logger
- @storybook/preset-create-react-app
- @storybook/react
- @storybook/testing-library
- webpack 5버전

<aside>
💡 한번에 설치하기
npm :

```powershell
npm install @storybook/addon-actions @storybook/addon-essentials @storybook/addon-interactions @storybook/addon-links @storybook/builder-webpack5 @storybook/manager-webpack5 @storybook/node-logger @storybook/preset-create-react-app @storybook/react @storybook/testing-library webpack@5
```

yarn : 

```powershell
yarn add @storybook/addon-actions @storybook/addon-essentials @storybook/addon-interactions @storybook/addon-links @storybook/builder-webpack5 @storybook/manager-webpack5 @storybook/node-logger @storybook/preset-create-react-app @storybook/react @storybook/testing-library webpack@5
```

</aside>

다음은 필요한 구성 파일을 만들어줍시다. 프로젝트 폴더 최상단 위치에 `.storybook`이라는 이름으로 폴더를 하나 생성합니다.

생성한 폴더 안에 `main.js` 파일과 `preview.js` 파일을 생성하고 아래에 내용을 삽입합니다.

.storybook > **main.js**

```jsx
module.exports = {
  "stories": [
    "../src/**/*.stories.mdx",
    "../src/**/*.stories.@(js|jsx|ts|tsx)"
  ],
  "addons": [
    "@storybook/addon-links",
    "@storybook/addon-essentials",
    "@storybook/addon-interactions",
    "@storybook/preset-create-react-app"
  ],
  "framework": "@storybook/react",
  "core": {
    "builder": "@storybook/builder-webpack5"
  }
}
```

.storybook > **preview.js**

```jsx
export const parameters = {
  actions: { argTypesRegex: "^on[A-Z].*" },
  controls: {
    matchers: {
      color: /(background|color)$/i,
      date: /Date$/,
    },
  },
}
```

스토리북이 실행되기 위해 `package.json`에서 아래 내용을 추가합니다.

**package.json**

```json
// ...
"eslintConfig": {
  // ...
  "overrides": [
    {
      "files": [
        "**/*.stories.*"
      ],
      "rules": {
        "import/no-anonymous-default-export": "off"
      }
    }
  ]
},
// ...
"scripts": {
	//...
	"storybook": "start-storybook -p 6006 -s public",
}
```

컴포넌트 파일을 임시로 추가한 후 스토리북을 실행하여 정상적으로 출력되는지 확인합니다.

**Button.css**

```jsx
.custom-button-large {
	width: 256;
}
.custom-button-medium {
	width: 164;
}
.custom-button-small {
	width: 75;
}
```

**Button.jsx**

```jsx
import React from 'react';
import 'Button.css';

export const ButtonComponent = ({ ...props }) => {
    const { text, size, onClick } = props;
    const sizeStyle = useMemo(() => {
			return `custom-button-${size}`
		}, [size]);

    return (
        <button className={sizeStyle} onClick={onClick}>
	        {text}
        </button>
    );
}
```

**Button.stories.jsx**

```jsx
import React from 'react';
import { ButtonComponent } from '../component/UI/ButtonComponent'

export default {
  title: 'UI/ButtonComponent',
  component: ButtonComponent,
  argTypes: {
    text: { control: 'text' },
    size: { control: 'text' },
    onClick: { control: '' },
  },
};

const Template = (args) => <ButtonComponent {...args} />;

export const Primary = Template.bind({});
Primary.args = {
  text: 'text',
  size: 'small',
  onClick: '',
};
```

**npm** : 

```powershell
npm run storybook
```

**yarn** : 

```powershell
yarn storybook
```

## 구성

환경 구축을 마무리하면 보통 아래의 사진 같은 환경으로 구성됩니다.

![Untitled](https://github.com/isos-consulting/feto/assets/49608580/08b86f6c-ed47-4ac7-aa95-3feb064e2d5e)

항목을 하나씩 살펴보겠습니다.

- **.storybook** : 스토리북을 사용할 때 필요한 플러그인을 설정하거나 테마를 변경하는 작업을 하는 설정 파일로 구성된 폴더입니다.
- **stories** : 샘플 컴포넌트 파일과 스토리 파일로 구성된 폴더입니다. 해당 폴더는 지워도 문제 없습니다.
- **main.js** : stories파일 색인을 결정하거나 플러그인을 설정할 수 있는 설정 파일입니다.
- **preview.js** : 스토리가 렌더링되는 방식을 제어하는 설정 파일입니다. `decorators` `parameters` `globalTypes` 에 대해 정의 할 수 있습니다.

<aside>
💡 더 다양한 구성에 대한 공식문서의 ‘****Configure Storybook****’ 항목을 참고하세요.

[Configure Storybook](https://storybook.js.org/docs/react/configure/overview)

</aside>

## 스토리 파일 인식

test파일처럼 스토리북도 실행될 때 특정 파일들만 색인한 후 실행됩니다. 파일명과 확장자 사이에 `stories`를 붙이면 스토리를 파일로 인식되어 실행됩니다. (예시: xxx.stories.jsx)

# 메뉴 구성하기

메뉴는 `title`에 의해 구성됩니다. `/` 기호를 사용하여 카테고리를 구성할 수 있습니다.

**Button.stories.jsx**

```jsx
// ...

export default {
  title: 'UI/ButtonComponent',
  component: ButtonComponent,
  argTypes: {
    text: { control: 'text' },
    size: { control: 'text' },
    onClick: { control: '' },
  },
};

// ...
```

위 예시는 사이드바에 UI라는 섹션 안에 ButtonComponent 메뉴가 생성되는 예제입니다.

# 테마 설정하기

스토리북 테마를 변경하는 가장 빠른 방법은 애드온을 사용하여 테마 패키지를 설치하는 것입니다. 먼저 아래 명시된 패키지를 설치합니다.

- @storybook/addons
- @storybook/theming

<aside>
💡 한번에 설치하기

**npm** : 

```powershell
npm install @storybook/addons @storybook/theming
```

**yarn** :

```powershell
yarn add @storybook/addons @storybook/theming
```

</aside>

설치가 끝나면 .storybook >  `manager.js` 파일을 생성하고 아래처럼 내용을 삽입합니다.

**manager.js**

```jsx
import { addons } from '@storybook/addons';
import { themes } from '@storybook/theming';

addons.setConfig({
  theme: themes.dark,
});
```

추가적으로 docs 영역에도 동일한 테마를 적용하려면 .storybook > `preview.js` 아래 내용을 삽입하면 됩니다.

**preview.js**

```jsx
import { themes } from '@storybook/theming';

export const parameters = {
	// ...
  docs: {
    theme: themes.dark,
  },
};
```

<aside>
💡 테마를 직접 만들려면 공식문서의 ‘****Create a theme quickstart****’ 항목을 참고하세요.

[Theming](https://storybook.js.org/docs/react/configure/theming#create-a-theme-quickstart)

</aside>

# 무료 자습서

[How to write stories](https://storybook.js.org/docs/react/writing-stories/introduction)

# 이슈 해결

스토리북을 사용하면서 생길 수 있는 문제에 대한 해결책을 제시해주는 섹션입니다. 미리보기에서 필요한 항목을 찾아가면 됩니다. 

## 스토리북 환경에서 스타일이 적용되지 않습니다.

기껏 적용해놓은 스타일이 일반 런타임 환경에서는 되는데 스토리북에서는 안될 수 있습니다. 이런 상황은 보통 루트 index파일에서 스타일을 import했기 때문에 런타임에서만 적용되는 문제일 수 있습니다. 스토리북 환경에서 루트 index파일은 실행되지 않기 때문에 스토리북이 실행되는 파일에서 스타일을 import해야 합니다.

1. .storybook > preview.js 파일을 엽니다.
2. 아래처럼 적용할 스타일 파일을 import합니다.
    
    ```jsx
    import '../src/xxx.css';
    
    export const parameters = {
      ...
    }
    ```
    
3. 스토리북을 실행하여 제대로 적용됐는지 확인합니다.

## webpack5에 대한 오류가 발생합니다.

<aside>
📢 이 문제는 최신 버전에서 이미 해결된 항목일 수 있습니다.

</aside>

프로젝트에 따로 webpack 패키지가 설치된 경우 storybook 6버전에서 사용하는 웹팩 버전과 충돌하여 이러한 오류가 발생할 수 있습니다. 스토리북이 업데이트를 하면 해결될 수 있는 문제지만 자체적으로 해결할 수 있는 방법에 대해 작성했습니다.

먼저 webpack버전이 5이상인지 확인합니다. 5미만이라면 5버전으로 업그레이드 해야 합니다.

업그레이드를 마치면 아래에 명시된 패키지를 설치합니다.

- @storybook/builder-webpack5
- @storybook/manager-webpack5

<aside>
💡 한번에 설치하기
**npm** :

```powershell
npm install @storybook/builder-webpack5 @storybook/manager-webpack5
```

**yarn** : 

```powershell
yarn add @storybook/builder-webpack5 @storybook/manager-webpack5
```

</aside>

메인 파일에 아래 내용을 추가합니다.

**main.js**

```jsx
module.exports = {
	// ...
	"core": {
    "builder": "webpack5"
  }
}
```

실행한 후 동일한 오류가 발생하는지 확인합니다.
