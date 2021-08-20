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

Component는 프로그램의 함수와 유사하며, props라는 임의의 입력을 받은 후, 화면에 어떻게 표기되는지를 나타내는 엘리먼트를 반환

## 함수 컴포넌트와 클래스 컴포넌트

1. 함수 컴포넌트

    엘리먼트를 반환하는 함수를 작성하여 컴포넌트를 표현하는 것.

    데이터를 가진 **하나의 props**를 객체 인자로 받은 후, React 엘리먼트를 반환하면 유효한 컴포넌트이다.

    ~~~js
    const welcomeFunction = (props) => <h1>Hello, {props.name}</h1>;
    ~~~

1. 클래스 컴포넌트

    사전에 정의된 컴포넌트 클래스를 상속을 하여 새로운 컴포넌트 클래스를 만드는 방식

    ~~~js
    class welcome extends React.Component{
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
    }
    ~~~

## 컴포넌트 렌더링

React 엘리먼트는 사용자 정의 컴포넌트로 나타낼 수 있다.

~~~ js
const element = <Welcome name="Sara" />;
~~~

사용자 정의 컴포넌트로 작성한 엘리먼트의 경우, JSX의 attribute와 자식을 해당 컴포넌트에 단일 객체로 전달한다.

이 객체를 props라고 한다.

~~~ js
const Welcome = (props) => <h1>Hello, { props.name } </h1>;
const element = <Welcome name="Sara" />;
ReactDOM.render(
    element,
    document.getElementById('root');
)
~~~

위의 코드는 다음과 같은 순서로 렌더링이 된다.

1. ```<Welcome name="Sara" />``` 엘리먼트로  ReactDOM.render() 호출
1. React는 {name: 'Sara'}를 props로 하여 Welcome 컴포넌트를 호출
1. Welcome 컴포넌트는 결과적으로 ```<h1>Hello, Sara</h1>``` 엘리먼트를 반환
1. ReactDOM은 ```<h1>Hello, Sara</h1>``` 엘리먼트와 일치하도록 DOM을 업데이트

> 컴포넌트의 이름은 항상 대문자로 시작한다.\
> React는 소문자로 시작하는 컴포넌트를 DOM 태그로 처리합니다.\
> 예를 들어 ```<div />```는 HTML div 태그를 나타내지만, ```<Welcome />```은 컴포넌트를 나타내며 범위 안에 Welcome이 있어야 합니다.

## 컴포넌트 합성

컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있다.

모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있다.

즉 버튼, 폼, 다이얼로그, 화면 등의 모든 것들이 컴포넌트로 표현할 수 있다.

~~~js
const Welcome = (props) => <h1>Hello, {props.name}</h1>;

const App = () =>(
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
~~~

## props는 읽기 전용

함수 컴포넌트나 클래스 컴포넌트 모드 컴포넌트 자체 props를 수정할 수 없다.

> **모든 React 컴포넌트는 자신의 props를 다룰 때, 반드시 순수 함수처럼 동작해야 한다.**

# State와 생명주기

컴포넌트를 완전히 재사용하고 캡슐화하는 방법.

~~~js
const Clock = (props) => (
    <div>
        <h1> Hello World! </h1>
        <h2> It is {props.date.toLocaleTimeString()}. </h2>
    </div>
);

const tick = () => ReactDOM.render(
    <Clock date={new Date()}/>,
    document.getElementById('root')
);

setInterval(tick,1000);
~~~

위의 코드에서 바꿔야 할 사항은 Clock이 타이머를 설정하고 매초 UI를 업데이트 하는 것이 Clock의 구현 사항이다.

따라서 Clock 컴포넌트에 ```state```를 추가한다.

## 함수에서 클래스로 변환

1. React.Component를 확장하는 동일한 이름의 ES6 class 생성
1. render()라고 불리는 빈 메서드를 추가
1. 함수의 내용을 render() 메서드 안으로 옮김.
1. render() 내용 안에 있는 props를 this.props로 변경
1. 남아있는 빈 함수 선언을 삭제

~~~js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
~~~

render 메서드는 업데이트가 발생할 때마다 호출되지만, 같은 DOM 노드로 ```<Clock />```을 렌더링하는 경우 Clock 클래스의 단일 인스턴스만 사용됩니다. 

이것은 로컬 state와 생명주기 메서드와 같은 부가적인 기능을 사용할 수 있게 해줍니다.

## 클래스에 로컬 state 추가

1. render() 메서드 안에 있는 this.props.date를 this.state.date로 변경
1. this.state를 정의하는 class constructor 작성
1. ```<Clock/>``` 요소에서 date prop를 삭제

위의 과정을 거치면 아래와 같이 코드가 리팩토링된다.
~~~js
class Clock extends React.Component {
  
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
~~~

## 생명주기 메서드를 클래스에 추가하기

많은 컴포넌트가 있는 어플리케이션에서 컴포넌트가 삭제될 때, 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요하다.

클래스 컴포넌트가 DOM에 렌더링 될 때, 특정 기능을 설정하는 것을 React에서 **마운트**라고 한다.

클래스 컴포넌트에 의해 생성된 DOM을 삭제할 때, 특정 기능의 설정을 해제하는 것을 **언마운트**라고 한다.

컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트되거나 언마운트 될 때, 일부 코드를 작동할 수 있다.

~~~js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
~~~

1. ```<Clock />```가 ReactDOM.render()로 전달되었을 때, React는 Clock 컴포넌트의 constructor를 호출
1. React는 Clock 컴포넌트의 render() 메서드를 호출. 이를 통해 화면에 표시되어야 할 내용을 알게 되고, 그 다음 React는 이 내용을 통해 렌더링 출력값을 일치시키기 위해 DOM을 업데이트 한다.
1. Clock 출력값이 DOM에 삽입되면, React는 componentDidMount() 생명주기 메서드를 호출.
1. 매초마다 setState()를 통해서 state를 변경하고, 이를 통해서 React는 render()를 호출하여 렌더링 출력값은 업데이트된 시각을 포함한다. React는 이에 따라 DOM을 업데이트 한다.
1. Clock 컴포넌트가 DOM에서 삭제된 적이 있다면, React는 componentWillUnmount()를 통해 타이머를 멈춘다.

## state 사용법
1. 직접 state를 수정하지 않는다.

    constructor에서 this.state를 정한 다음, 항상 setState()를 활용해 수정을 해야 한다.

1. state의 업데이트는 비동기적일 수 있다.

    React는 성능을 위해 여러 setState() 호출을 단일 업데이트로 한꺼번에 처리할 수 있다.

    this.props와 this.state가 비동기적으로 업데이트될 수 있기 때문에 state를 계산할 때, 해당 값에 의존적이면 안된다.

    ~~~js
    
    //wrong example
    
    this.setState({
        counter: this.state.counter + this.props.increment,
    });

    // Correct

    this.setState((state,props) => ({
        counter: state.counter + props.increment,
    }));
    ~~~

1. state의 업데이트는 병합된다.

    setState()를 호출할 때, React는 제공한 객체를 현재 state로 변경한다.

    만약 A와 B라는 property가 객체에 있을 때, A의 변경은 B에 영향을 주지 않고 B의 변경은 A의 변경에 영향을 주지 않는다.

    하지만 각각 최신의 내용으로 업데이트 된다.

## 데이터는 아래로 흐른다.

state는 로컬 또는 캡슐화라고 불린다. state가 소유하고 있는 컴포넌트 이외에는 어떠한 컴포넌트에도 접근할 수 없다.

컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있다.

일반적으로 이를 하향식(top-down) 또는 단방향식 데이터 흐름이라고 한다. 

모든 state는 항상 특정한 컴포넌트가 소유하고 있으며 그 state로부터 파생된 UI 또는 데이터는 오직 트리구조에서 자신의 아래에 있는 컴포넌트에만 영향을 미친다.

# 이벤트 처리하기

React 엘리먼트에서 이벤트를 처리하는 방식은 DOM 엘리먼트에서 이벤트를 처리하는 방식과 유사하다.

- React의 이벤트는 캐멀 케이스를 사용
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달
    ~~~js
    const element = <button onClick={activateLasers}> Activate Lasers </button>;
    ~~~
- false를 반환해도 기본 동작을 방지할 수 없음. 반드시 preventDefault를 명시적으로 호출해야 됨.
    ~~~js
    function Form() {

        function handleSubmit(e) {
            e.preventDefault(); // 기본 동작 방지
            console.log('You clicked submit.');
        }

        return (
            <form onSubmit={handleSubmit}>
            <button type="submit">Submit</button>
            </form>
        );
    }
    ~~~
- DOM 엘리먼트가 생성된 후, 리스너를 추가하기 위해 addEventListener를 호출하지 않고 엘리먼트가 처음 렌더링될 때 리스터를 제공해야 한다.
    
    bind를 활용하여 EventListener를 추가한다.
    ~~~js
    class Toggle extends React.Component {
        constructor(props) {
            super(props);
            this.state = {isToggleOn: true};

            // 콜백에서 `this`가 작동하려면 아래와 같이 바인딩 해주어야 합니다.
            this.handleClick = this.handleClick.bind(this);
        }

        handleClick() {
            this.setState(prevState => ({
            isToggleOn: !prevState.isToggleOn
            }));
        }

        render() {
            return (
            <button onClick={this.handleClick}>
                {this.state.isToggleOn ? 'ON' : 'OFF'}
            </button>
            );
        }
    }

    ReactDOM.render(
    <Toggle />,
    document.getElementById('root')
    );
    ~~~

    퍼블릭 클래스 필드 문법을 사용하면, 클래스 필드를 활용하여 콜백을 올바르게 바인딩 할 수 있다.
    ~~~ js
    class LoggingButton extends React.Component {
        // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
        // 주의: 이 문법은 *실험적인* 문법입니다.
        handleClick = () => {
            console.log('this is:', this);
        }

        render() {
            return (
            <button onClick={this.handleClick}>
                Click me
            </button>
            );
    }
    ~~~
    콜백 함수에 화살표 함수를 활용하여 작성이 가능하다.
    ~~~js
    class LoggingButton extends React.Component {
        handleClick() {
            console.log('this is:', this);
        }

        render() {
            // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
            return (
            <button onClick={() => this.handleClick()}>
                Click me
            </button>
            );
        }
    }
    ~~~
- 이벤트 핸들러에 인자 전달하기

    루프 내부에서는 이벤트 핸들러에 추가적인 매개변수를 전달하는 것이 일반적입니다. 예를 들어, id가 행의 ID일 경우 다음 코드가 모두 작동합니다.

    ~~~js
    <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
    <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
    ~~~

    위 두 줄은 동등하며 각각 화살표 함수와 Function.prototype.bind를 사용합니다.

    두 경우 모두 React 이벤트를 나타내는 e 인자가 ID 뒤에 두 번째 인자로 전달됩니다. 화살표 함수를 사용하면 명시적으로 인자를 전달해야 하지만 bind를 사용할 경우 추가 인자가 자동으로 전달됩니다.


# 조건부 렌더링
# 리스트와 Key
# 폼
# State 끌어올리기
# 합성 vs 상속
