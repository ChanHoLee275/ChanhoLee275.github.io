---
layout: post
title: Summary of ReactJS
tags: [frontend]
categories: frontend
---
React에서는 렌더링을 하는 로직과 UI 로직( 이벤트 처리, 시간에 따라 state 변화, 화면에 표시하기 위해 데이터가 준비되는 방식 등 )이 연결된다.

React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 컴포넌트라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리한다.

# JSX

Javascirpt를 확장한 문법으로 JSX의 React 엘리먼트를 생성한다.
JSX는 XML과 유사하게 태그를 작성한다. 또한 그 문법은 html과 유사하며, 이를 참고하여 작성하면 원하는 내용을 만들 수 있다.

JSX는 아래의 특징을 갖는다.
1. JSX에 표현식이 포함될 수 있다.

    아래의 코드처럼 변수로 선언한 내용을 JSX를 작성할 때, 중괄호를 활용하여 그 안에 넣으면 그 내용을 사용할 수 있다. 이는 함수에도 마찬가지로 적용이 되는 내용이다. 
    ~~~ js
    const user = "Lee";
    const age = () => 23;
    const element =(
    <div>
        <h1> Hello World! My name is { user }</h1>
        <h2>My Old is { age() }</h2>
    </div>);
    ReactDOM.render(
        element, document.getElementById('root'),
    )
    ~~~
1. JSX는 표현식이다.

    JSX 표현식은 객체로 인식된다.

    if문과 for문 while문 등 다양한 구문에 사용을 할 수 있고, 변수에 할당하고, 인자로 받아드리고, 함수로부터 반환을 할 수 있다.

    ~~~ js
    const sayHello => (user) user ? <h1> Hello, {user}!</h1> : <h1> Hello, Stranger!</h1>;
    ~~~

1. JSX 속성 정의
    html의 태그 속성을 정의하는 것처럼, JSX 또한, 이를 정의할 수 있다. 
    
    하지만 javascript에서 이미 사용하고 있는 내용의 경우 (ex. class) 이름이 다르므로, 이를 확인하여 사용해야 한다.

    속성을 정의할 때, 직접 정의하는 경우 따옴표를 사용하여 입력을 하고 변수를 활용하는 경우 중괄호를 사용한다.
    ~~~ js
    const element1 = <div className = "post"> shopping </div>;
    const element2 = <img src={url}></img>;
    ~~~
1. JSX로 자식 정의

    태그가 비어있다면 XML처럼 />를 이용하여 바로 닫아주는 것이 좋다.
    
    ~~~js
    const element2 = <img src={url} />;
    ~~~

    태그는 자식을 포함할 수 있다.
    ~~~js
    const element =(
    <div>
        <h1> Hello World! My name is { user }</h1>
        <h2>My Old is { age() }</h2>
    </div>);
    ~~~

# 엘리먼트 렌더링

**엘리먼트는 React 앱의 가장 작은 단위이다.**

엘리먼트는 화면에 표시할 내용을 기술한다.

React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트한다.

## DOM에 엘리먼트 렌더링하기

html 파일에 <div>가 있다고 가정한다.

이 안에 들어가는 모든 엘리먼트를 React DOM이 관리한다고 하면, 이를 루트 DOM 노드라고 부른다.

React로 구현된 어플리케이션은 하나의 루트 DOM 노드가 있다.

React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 ReactDOM.render()로 전달하면 된다.

~~~js
const user = "Lee";
const age = () => 23;
const element =(
<div>
    <h1> Hello World! My name is { user }</h1>
    <h2>My Old is { age() }</h2>
</div>);
ReactDOM.render(
    element, document.getElementById('root'),
)
~~~

## 렌더링 된 엘리먼트 업데이트하기

React 엘리먼트는 불변객체이다. 엘리먼트는 한 번 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없다. 

엘리먼트는 지속적으로 변화하는 UI 중 특정 시점의 상태를 보여주는 것이다.

따라서 엘리먼트가 바뀔 때마다, 새롭게 엘리먼트를 렌더링하는 것이 필요하다.

~~~js
let count = 0;
const tick = () => {
    
    const element =(
    <div>
        <h1> Hello World! My name is { user }</h1>
        <h2>Now Time is { count }</h2>
    </div>);
    count += 1;
    ReactDOM.render(element,document.getElementById('root'));
}

setInterval(tick,1000);
~~~

React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 필요한 경우에만 DOM을 업데이트한다.

특정 시점에 UI가 어떻게 보일지 고민하는 접근법은 시간의 변화에 따라 UI가 어떻게 변화할지 고민하는 것보다 더 많은 수의 버그를 없앨 수 있다.

# Component와 Props
# State와 생명주기
# 이벤트 처리하기
# 조건부 렌더링
# 리스트와 Key
# 폼
# State 끌어올리기
# 합성 vs 상속
