# React Start

## 리액트 컴포넌트의 정의와 규칙

리액트는 자바스크립트 기반의 라이브러리이며, 가장 큰 특징은 UI **컴포넌트** 단위로 구성한다는 점입니다.
컴포넌트는 고유한 로직과 모양을 가진 재사용 가능한 UI요소로, 마크업을 반환하는 자바스크립트 함수입니다.

```jsx
function Profile() {
    return (
        <h2>{name}</h2>
        <img src="./ProfileImage" alt="프로필 이미지"/>
    )
}

// 화살표 함수 방식도 쓰일 수 있다.
const Profile = () => {
    return (
        <h2>{name}</h2>
        <img src="./ProfileImage" alt="프로필 이미지"/>
    )
}
```

컴포넌트에서는 항상 **대문자**로 시작해야하며 HTML태그는 소문자로 시작해야한다.

```jsx
// HTML 태그인 img 태그가 호출됩니다.
function Profile() = {
    return <img />
}

// 컴포넌트인 Img 컴포넌트가 호출됩니다.
function Profile() = {
    return <Img />
}
```

<br />

## JSX 문법의 엄격함과 표현식

리액트에서는 UI 로직과 렌더링 로직이 밀접하게 연결되어 있어 JSX라는 문법을 사용합니다.
JSX는 일반 HTML보다 엄격하여 `<br />`처럼 닫는 태그가 필수적입니다. 또한 중괄호 `{}`를 사용하면 그 안에 변수나 함수 호출 등 모든 유효한 자바스크립트 표현식을 삽입할 수 있어 동적인 UI 생성이 가능해집니다.

```jsx
function formatName(user) {
  return user.firstName + " " + user.lastName;
}

const user = {
  firstName: "Harper",
  lastName: "Perez",
};

const element = <h1>Hello, {formatName(user)}!</h1>;
```

> 컴파일이 끝나며, JSX 표현식이 정규 자바스크립트 함수 호출이 되고 자바스크립트 객체로 인식이 됩니다.

즉, JSX를 `if` 구문 및 `for` loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있습니다.

### JSX 속성 정의

어트리뷰트에 `""`를 이용해 문자열 리터럴을 정의할 수 있고, 중괄호를 사용하여 어트리뷰트에 자바스크립트 표현식을 삽입할 수 있습니다.

```jsx
const element = <a href="https://www.reactjs.org"> link </a>;

const element = <img src={user.avatarUrl}></img>;
```

`""` 또는 `{}`중 하나만 사용해야하며, 동일한 어트리뷰트에 두 가지를 동시에 사용하면 안됩니다.

> JSX는 HTML보다는 자바스크립트에 가깝기 때문에, React DOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용합니다.

## JSX 반환 규칙

JSX를 작성할 때 가장 빈번하게 발생하는 에러 중 하나는 여러 개의 태그를 평행하게 반환하려 할 때입니다. 기술적으로 JSX는 컴파일 후 자바스크립트 객체를 변환되는데, 자바스크립트 함수는 한 번에 하나의 객체만 반환할 수 있기 때문에 반드시 최상위를 하나의 태그로 감싸야 합니다.

```jsx
// 부모 태그를 감싸주지 않으면 error가 발생합니다.
const AddProfile = () => {
    <Profile />
    <AddButton />
};
// <div></div>, <></>로 감싸주어야 error가 발생하지 않습니다.
const AddProfile = () => {
  <>
    <Profile />
    <AddButton />
  </>;
};
```

### 왜 하나만 반환해야할까?

React는 자바스크립트를 기반으로한 프레임 워크입니다. 자바스크립트에서 함수는 단 하나의 값만 반환할 수 있기에 여러 개의 객체를 동시에 `return`할 수 없습니다.

## JSX의 보안 특성 (XSS 방지)

리액트 DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 문자열로 변환하는 이스케이프(Escape) 처리를 수행합니다. 이 과정을 통해 애플리케이션에 명시적으로 작성되지 않은 외부 스크립트가 실행되는 것을 차단하며, 결과적으로 XSS(cross-site-scripting) 공격으로부터 사용자를 보호합니다.
