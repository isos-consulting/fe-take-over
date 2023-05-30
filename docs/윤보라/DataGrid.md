iso-client에서 데이터를 핸들링하기 위해서는 DataGrid 사용 방법에 대해 알 필요가 있습니다. 사용 방법을 배우기 전에 먼저 구조와 흐름부터 살펴봅시다.

# DataGrid 구조 이해하기

본 프로젝트의 데이터 그리드는 TOAST UI에서 제공하는 [tui-grid](https://ui.toast.com/tui-grid) 패키지를 통해 개발되었습니다. 데이터 그리드 사용법을 이해하려면 먼저 tui-grid를 이해해야 합니다.

[Grid](https://ui.toast.com/tui-grid)

iso-client 프로젝트의 데이터 그리드는 아래와 같은 절차로 컴포넌트가 구성되어 있습니다.

1. 커스텀 프로퍼티 전달
2. 커스텀 프로퍼티를 tui-grid 데이터 타입에 맞게 가공
3. tui-grid 프로퍼티 전달

개발 편의성과 상황에 따라 필요한 속성에 의하여 프로퍼티 타입이 커스텀으로 정의되어 있습니다.

tui-grid의 기존 프로퍼티를 살펴보면 현 프로젝트의 데이터 그리드 프로퍼티와 차이점이 있다는 걸 알 수 있습니다. 2번에서 언급된대로 커스텀된 프로퍼티를 재가공하는 과정만 알면 신규 프로퍼티를 추가할 수도, 기존 프로퍼티를 수정할 수 있습니다.

재가공되고 있는 커스텀 프로퍼티는 아래와 같습니다.

- [columns](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)
- [header](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)
- [columnOptions](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)
- [summary](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)
- [data](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)
- [기본 액션](https://www.notion.so/DataGrid-e4ad24d5e3734c76b181a642eaaf12f3)

자세한 내용은 아래에서 하나씩 살펴보도록 하겠습니다.

## columns

columns 속성은 다음 기능에 대한 가공 작업을 수행합니다.

### 필수 값 지정

- `requiredField` 기본 값은 `false`입니다.
- 컬럼을 필수 값으로 지정하면 컬럼 이름 앞에 별모양(*)이 붙습니다.

### 정렬 기능 설정

- `sortable` 기본 값은 `true`입니다.

### 컬럼 너비 변경 허용 설정

- `resizable` 기본 값은 `true`입니다.

### 포맷에 따라 렌더러 유형 지정

- `format` 값에 따라 렌더링 타입이 변경됩니다.

### 포맷에 따라 에디터 유형 지정

- `format` 값에 따라 에디터 타입이 변경됩니다.

### 포맷에 따라 필터 유형 지정

- `format` 값에 따라 필터 타입이 변경됩니다.
- 필터는 기본적으로 초기화 버튼이 있습니다.
- 날짜 포맷의 경우 format 값으로 ‘yyyy-MM-dd’ 값이 삽입됩니다.

### 수정 허용 설정

- `editable` 기본 값은 `false`입니다.

### 컬럼 숨김 설정

- `hidden` 기본 값은 `false`입니다.

### 수정 허용 조건 처리

- `editableCondition` 속성을 사용해 입력 활성화를 동적인 조건에 따라 처리할 수 있습니다.

### 비활성화 조건 처리

- `disableCondition` 속성을 사용해 비활성화를 동적인 조건에 따라 처리할 수 있습니다.

### 기본 컬럼 추가 (_edit, 등록일시, 등록자, 수정일시, 수정자)

- `_edit` 컬럼은 신규추가(C), 수정(U), 삭제(D)를 분류하는 역할을 하며 `hidden` 속성으로 감춰져 있어 화면에 표시되지 않습니다.

## header

header 속성은 다음과 같은 작업을 수행합니다.

### 기본 높이 사이즈 조정

- `height` 기본 값은 30으로 고정됩니다.
- `complexColumns` 속성을 사용하는 경우 한정으로 60으로 고정합니다.

## columnOptions

columnOptions 속성은 다음 기능에 대한 가공 작업을 수행합니다.

### 그리드 모드에 따라 컬럼 고정 옵션 지정

- 그리드 모드가 `create` `update` 라면 기본 값으로 무조건 `frozenCount` 옵션을 삽입하여 첫번째 컬럼을 고정시킵니다. 첫번째 컬럼은 `신규`, `수정`, `삭제` 를 표시하는 상태 컬럼입니다.
- columnOptions 속성이 없으면 자동으로 아래와 같이 설정합니다.
    
    ```jsx
    {
    	frozenCount: 1,
    	frozenBorderWidth: 2
    }
    ```
    
- columnOptions에 `frozenCount` 값이 있는 경우 해당 값에 +1를 추가합니다. frozenCount는 0부터 숫자를 세기 때문입니다.

## summary

summary 속성은 다음 기능에 대한 가공 작업을 수행합니다.

### 기본 높이 지정

- 기본 높이는 `rowHeight` 값과 동일하게 설정됩니다. (`rowHeight` 기본 값 `35`)

### 기본 위치 지정

- `position` 기본 값은 `bottom`입니다.

### 컬럼 값 연산

- 같은 컬럼의 셀 값들을 모두 합산하거나 평균을 내는 등의 연산 작업을 합니다.

## data

data 속성은 다음 기능에 대한 가공 작업을 수행합니다.

### 클래스명 삽입

- `editable`, `gridMode`, `popupable` 속성에 따라 클래스 네임을 삽입하여 스타일을 변경합니다.

### 기본 셀 값 삽입

- `defaultValue` 속성을 통해 셀의 기본 값을 설정할 수 있습니다.

## 기본 액션

다음과 같은 함수들로 기본적인 액션을 동작시킵니다.

- 1행에 행 추가 `onPrepentRow`
- 행 추가 `onAppendRow`
- 행 취소 `onCancelRow`
- 클릭 `onClick`
- 더블 클릭 `onDblClick`
- 값 수정 후 이벤트 `onAfterChange`
- 헤더 영역의 체크박스 체크 `onCheck`
- 헤더 영역의 체크박스 전부 체크 `onCheckAll`
- 헤더 영역의 체크박스 전부 해제 `onUncheckAll`
- 단일 항목 선택 `onSelect`
- 단일 항목 선택 해제 `onUnselect`
- 다중 항목 선택 `onMultiSelect`
- 멀티팝업 행 추가 `onAddPopupRow`
- 팝업 불러오기 `onLoadPopup`
- 키보드 입력 처리 `onKeyDown`
- 필터 전처리 `onBeforeFilter`
- 필터 초기화 처리 `onBeforeUnfilter`

# DataGrid 커스텀 하기

개발을 하다보면 기능을 새로 만들거나 수정해야하는 경우가 발생할 수 있습니다. 본 섹션에서는 데이터 그리드를 어떻게 커스텀하여 사용할 수 있는지에 대해 정리해드립니다.

- 살펴보기
    
    [새로운 액션 추가하기](https://www.notion.so/46416816ceb245cfabca604964c35f63) 
    
    [새로운 포맷 추가하기](https://www.notion.so/3a68c667a5d747d0bd0c3287dfdbd7af) 
    
    [셀 디스플레이 형식 변경하기](https://www.notion.so/84d3b4527979478cb013b087c1939f93) 
    
    [신규 입력기 추가하기](https://www.notion.so/c099f534fffa47f89affdbfb0769d51a) 
    

## 새로운 액션 추가하기

액션을 추가하려면 tui_grid에서 제공하는 프로퍼티에 인자 값을 넣어주는 방법도 있지만 레퍼런스를 활용해서 이벤트를 추가해주는 방법도 있습니다. 본 섹션에서는 후자의 경우를 가정한 설명을 해보려고 합니다.

### on / off 메소드 사용하기

tui-grid는 on, off 메소드를 사용해서 이벤트를 추가하거나 삭제할 수 있습니다. 추가할 수 있는 이벤트의 종류는 흔히보는 click, dblClick 같은 것들도 있지만 라이브러리에서 자체적으로 추가한 이벤트도 존재합니다. afterChange, filter, unfilter 등이 그런 것들이죠.

이벤트를 추가하려면 먼저 레퍼런스에 접근하여 인스턴스를 불러와야 합니다. tui-grid에서는 레퍼런스를 통해 getInstance() 메소드를 제공합니다.

```jsx
const gridRef = useRef();

gridRef.current.getInstacne();

return <DataGrid ref={gridRef} />;
```

getInstance() 내부에 ‘on’, ‘off’ 메소드를 사용해서 이벤트를 추가하거나 삭제할 수 있습니다.

```jsx
const { on, off } = gridRef.current.getInstacne();

// 이벤트 리스너 추가
on('afterChange', (ev) => {
	console.log('값이 수정되었음');
});

//이벤트 리스너 제거
off('afterChange'); 
```

`on` 메소드 첫번째 인자는 이벤트 이름, 두번째 인자는 이벤트 발생 시 실행될 함수입니다. 이벤트는 여러 번 등록할 수 있습니다.

`off` 메소드는 첫번째 인자 값만 넘겨주면 해당 이벤트 이름으로 추가했던 모든 이벤트를 제거합니다. function을 넘겨주면 해당 function에 대한 이벤트만 제거합니다.

callback 함수에서는 각 이벤트 이름에 따라 다양한 형식의 프로퍼티를 받을 수 있습니다. 이벤트 이름마다 프로퍼티가 다르지만 공통적으론 그리드의 인스턴스를 받을 수 있다는 점입니다.

그리드의 인스턴스로는 현재 데이터나 컬럼 데이터, 각종 함수 등을 쓸 수 있습니다. tui-grid 공식 문서의 ****[INSTANCE METHODS](https://nhn.github.io/tui.grid/latest/Grid#activateFocus)** 항목을 보고 찾아서 사용할 수 있습니다.

```jsx
const { on, off } = gridRef.current.getInstacne();

// 이벤트 리스너 추가
on('afterChange', (ev) => {
	const { columnName, rowKey, instance } = ev;
 	console.log(`${rowKey}, ${columnName}의 값이 수정되었음`);
	console.log('지금 데이터의 값 보기', instance.store.data.rawData);
	// 인스턴스 함수 사용!
	console.log('값 가져오기', instance.getValue(rowKey, columnName));
});

//이벤트 리스너 제거
off('afterChange'); 
```

## 새로운 포맷 추가하기

현재 사용하는 ‘text’, ‘number’, ‘combo’, ‘check’... 말고도 새로운 포맷을 추가해야할 수 있습니다. 본 섹션에서는 새로운 포맷을 추가하는 절차를 나열하여 설명합니다.

본 예제에선 ‘slide’ 라는 이름의 포맷을 추가시켜 슬라이드 바를 활용해 숫자 값을 입력하는 코드를 작성하였습니다.

### 타입 추가하기

먼저, 새로운 포맷의 타입 유형을 추가해야 합니다. 타입은 `datagrid.ui.type.ts`에서 추가할 수 있습니다. 예정대로 ‘slide’ 유형의 타입을 임시로 추가하겠습니다.

```jsx
format?: 'text' | 'number' | 'date' | 'datetime' | 'time' | 'check' | 'radio' | 'combo' | 'popup' | 'button' | 'tag' | 'file' | 'slide';
```

### 포맷 case 추가하기

타입을 추가했으니 실질적으로 속성에 대한 처리 로직을 추가해야합니다. 실제로 포맷 인자를 받게되면 해당 처리는 `datagrid.ui.tsx` 내의 `columns` 변수에서 처리하게 됩니다.

columns의 useMemo 함수를 들여다보면 각 format에 따라 switch-case를 작성하는 구간이 있습니다. 비슷한 위치에 case를 새로 작성해보겠습니다.

포맷을 추가할 때 렌더러가 텍스트가 아닌 새로운 컴포넌트로 표시되어야 하는지, 입력방식은 어떤지에 대해 생각을 먼저 정리한 후 진행하면 좋습니다. 슬라이드는 렌더러도 입력기도 슬라이드 형태로 보여지고 입력되는 방식으로 진행해보도록 하겠습니다.

<aside>
💡 렌더러(renderer)는 셀 값의 표현 형식
에디터(editor)는 셀 값을 입력하는 방식

</aside>

렌더러를 변경하려면 column내의 속성인 renderer속성을, 에디터를 변경하려면 editor속성을 사용해야 합니다. 상단에서 반복문의 콜백 파라메터로 `el` 변수를 사용해 속성 값을 지정하도록 작업되어 있으니 이를 활용해봅시다.

```jsx
case 'slide': 
	el['renderer'] = {
		type: 클래스의 이름,
		options: {
			// 넘겨줄 옵션 값
		}
	}
	el['editor'] = {
		type: 클래스의 이름,
		options: {
			// 넘겨줄 옵션 값
		}
	}
	break;
```

기존에 없는 형식의 렌더러와 에디터를 추가하려면 클래스가 필요합니다. 클래스를 사용하여 컴포넌트를 만든 후 type속성에 넣어주면 해당 클래스 컴포넌트를 셀에 렌더링하게 됩니다.

options라는 속성을 활용해 필요한 값을 받아서 활용할 수 있습니다.

**셀 디스플레이 형식 변경하기** 섹션을 통해 renderer를 추가하는 방법을, **신규 입력기 추가하기** 섹션을 통해 editor를 추가하는 방법에 대해 배울수 있습니다.

## 셀 디스플레이 형식 변경하기

먼저 슬라이드 클래스를 작성한 후 이를 적용해봅시다.

클래스의 내부 함수로 `getElement()`를 사용할 수 있습니다. `getElement()`는 셀에 반환될 엘리먼트를 출력할 때 사용됩니다.

```jsx
class DataGridSlideRenderer {
	constructor(props) {
  }

  getElement() {
  }
}
```

`constructor()` 는 클래스가 생성될 때 실행되므로 초기 값을 설정하는 작업과 사용될 document를 생성하는 작업에 대해 작성하면 좋습니다.

지금 작성하는 컴포넌트는 렌더러이므로 입력이 발생되지 않도록 `disabled`를 `true`로 설정했습니다.

셀 값을 엘리먼트에 적용하려면 props의 value 프로퍼티를 받아서 element에 넣어주면 됩니다.

```jsx
class DataGridSlideRenderer {
	constructor(props) {
    const el = document.createElement('input');

    el.type = 'range';
    el.disabled = true;

    this.el = el;
		this.el.value = String(props.value);
  }

  getElement() {
		return this.el;
  }
}
```

추가적으로 옵션 값에 대한 처리까지 작성해준 후 포맷 case에 적용까지 해주면 완성입니다.

**datagrid-slide.ui.tsx**

```jsx
class DataGridSlideRenderer {
	constructor(props) {
    const el = document.createElement('input');
		const { min, max } = props.columnInfo.renderer.options;

    el.type = 'range';
    el.min = String(min);
    el.max = String(max);
    el.disabled = true;

    this.el = el;
		this.el.value = String(props.value);
  }

  getElement() {
		return this.el;
  }
}
```

**datagrid.ui.tsx**

```jsx
case 'slide': 
	el['renderer'] = {
		type: DataGridSlideRenderer,
		options: {
			min: 1,
			max: 100
		}
	}
	break;
```

## 신규 입력기 추가하기

에디터도 렌더러와 동일한 방식으로 클래스를 만든 후 포맷 case에 추가해주면 됩니다. 유의해야할 점은 기존 값이 입력기에 들어가야 되는 것과 새로 입력한 값이 렌더러에 적용돼야 한다는 점입니다.

editor 클래스는 `getElement()` 뿐만 아니라 `getValue()`, `mounted()` 메소드가 사용됩니다.

`getValue()`는 새로 입력된 값을 불러오는 역할을 담당하며, `mounted()`는 에디터가 렌더링된 후 자동으로 실행되는 이펙트 같은 역할을 담당합니다.

`getValue()` 를 통해 값을 가공하여 적용하거나, `mounted()` 를 사용해 editor가 렌더링될 때 포커스를 자동으로 맞추도록 설정할 수 있습니다.

**datagrid-slide.ui.tsx**

```jsx
class DataGridSlideEditor {
	constructor(props) {
    const el = document.createElement('input');
		const { min, max } = props.columnInfo.renderer.options;

    el.type = 'range';
    el.min = String(min);
    el.max = String(max);

    this.el = el;
  }

  getElement() {
		return this.el;
  }

	getValue() {
		return this.el.value;
	}

	mounted() {
    this.el.focus();
  }
}
```

**datagrid.ui.tsx**

```jsx
case 'slide': 
	el['editor'] = {
		type: DataGridSlideEditor,
		options: {
			min: 1,
			max: 100
		}
	}
	break;
```
