# 유건호 202130418

# 4월 3일
* Props 사용법
    * JSX에서는 Key-value쌍으로 props를 구성합니다.

    * profile 컴포넌트로 name,introduction,viewCount Props를 전달한다.
    * jsx에서는 중괄호를 사용하면 js 코드를 넣을 수 있다.
    * jsx를 사용하지 않는 경우 props의 전달 방법은 createElement()함수를 사용하는 것이다.
    
* 컴포넌트 종류
    * 리액트 초기 버전을 사용할 때는 클래스형 컴포넌트를 주로 사용함
    * 이후 HOOK이라는 개념이 나오면서 최근에는 함수형 컴포넌트를 주로 사용함.
    * 예전에 작성된 코드나 문서들이 클래스형 컴포넌트를 사용하고 있기 때문에
    * 클래스형 컴포넌트와 컴포넌트의 생명주기에 관해서도 공부해둬야 한다.
* 함수형 컴포넌트
    * welcome 컴포넌트는 props를 받아, 받은 props중 name키의 값을 "안녕"뒤에 넣어 변환함.


* 클래스형 컴포넌트
    * Welcome컴포넌트는 React.Component로 부터 상속받아 선언함

* 컴포넌트 이름 짓기
    * 이름은 항상 대문자로 시작
    * 왜냐하면 리액트는 소문자로 시작하는 컴포넌트를 DOM 태그로 인식하기 때문에
    * 컴포넌트 파일 이름과 컴포넌트 이름은 같아야함

* 컴포넌트 렌더링
    * 렌더링의 과정은 다음 코드와 같다.

    ```js
        function Welcome(props){
            return <h1>안녕, (props.name)</h1>
        }
        const element = <Welcome name = "인제" />
        ReactDOM.render(
            element,
            document.getElementById(`root`)
        );
    ```
* 컴포넌트 합성
    * 컴포넌트 합성은 여러개의 컴포넌트를 합쳐서 하나의 컴포넌트를 만드는 것
    * 이랙트에서는 컴포넌트 안에 또 다른 컴포넌트를 사용할 수 있기 때문에, 복잡한 화면을 여러 개의 컴포넌트로 나누어 구현할 수 있다.
     ```js
        app.js
        import logo from './logo.svg';
        import './App.css';

        import Welcome from './chapter_03/Welcome';
        import Clock from './chapter_03/Clock';

        function App() {
        return (
            <div className="App">
            <header className="App-header">
                <img src={logo} className="App-logo" alt="logo"/>
                <p>
                Edit <code>src/App.js</code> and save to reload.
                </p>
                <a
                className="App-link"
                href="https://reactjs.org"
                target="_blank"
                rel="noopener noreferrer"
                >
                Learn React
                </a>
            </header>
            <Welcome name="홍길동"/>
            <Welcome name="이순신"/>
            <Welcome name="강감찬"/>
            <Clock/>
            </div>
        );
        }

        export default App;

                
                -----------
        Welcome.jsx

        export default function Welcome(props){
            return (
            <>
            <h1>안녕, {props.name}</h1>
            </>
            )

        }


     ```
* 컴포넌트 추출
    * 복잡한 컴포넌트를 쪼개서 여러 개의 컴포넌트로 나눌 수 있다.
    * 큰 컴포넌트에서 일부를 추출해서 새로운 컴포넌트를 만드는 것이다.
    * 실무에서 처음부터 1개의 컴포넌트에 하나의 기능만 사용하도록 설계하는 것이 좋다.

    * comment는 댓글 표시 컴포넌트다.
    * 내부에는 이미지, 이름, 댓글과 작성일이 포함되어 있다.
    
## state
* state란?
    * state는 리액트 컴포넌트의 상태를 의미함
    * 상태의 의미는 정상인지 비정상인지가 아니라 컴포넌트의 데이터를 의미함
    * 정확히는 컴포넌트의 변경 가능한 데이터를 의미함
    * state가 변하면 다시 렌더링이 되기 때문에 렌더링과 관련된 값만 state에 포함시켜야함.
* state의 특징
    * 리액트 만의 특별한 형태가 아닌 단지 자바스크립트의 객체일 뿐

    * 함수형 에서는 useState()라는 함수 사용
    * state는 변경은 가능하지만 직접 수정해서는 안됨
    * 불가능 하다고 생각하는 것이 좋음
    * state를 변경하고자 할땐 setstate() 함수를 사용함
* 생명주기에 대해 알아보기
    * 생명주기는 컴포넌트의 생성 시점, 사용 시점, 종료 시점을 나타내는 것
    * constructor가 실행되면서 컴포넌트가 생성됨
    * 생성 직후 componentDidMount() 함수가 호출됨
    * 컴포넌트가 소멸하기 전까지 여러 번 렌더링 함.
    * 렌더링은 props,setState(),forceUpdate()에 의한 상태가 변경되면 이루어짐
    * 그리고 렌더링이 끝나면 componentDinUpdat() 함수가 호출됨
    * 마지막으로 컴포넌트가 언마운트 되면 compomentWillUnmount() 함수가 호출됨

# 3월 27일 
## JSX 
* JSX의 역할
    * JSX는 javaScript와 XML을 합친 것이다.
    * JSX는 내부적으로 XML/HTML코드를 자바스크립트로 변환함
    * REACT가 createElement함수를 사용하여 자동으로 자바스크립트로 변환해 줌
    * 만일 JS로 작업할 경우 직접 createElement함수를 사용해야 함
    * JSX는 기독성을 높여 주는 역할을 해준다.
***

*   JSX 장점
    * 코드가 간결해짐
    * 가독성이 향상됨
    * Injection Attack이라 불리는 해킹 방법을 방어함으로써 보안이 강화됨
 class를 사용한 모습
```js
    import React from "react";

    class Hello extends React.Component{
        render(){
               return(
                <h1>Hello</h1>
            )
        }
    }

    export default Hello;
```
```js
    
    export default function Hello(){
        return(
            <h1>Hellow</h1>
        )
    }
    //더 간결해짐
```
*   JSX 사용법
    *   모든 자바스크립트 문법을 지원함
    *   자바스크립트 문법에 XML과 HTML을 섞어서 사용함
    ```js
    const name = 'AAA';
        const element = <h1>안녕, {name}</h1>;
        ReactDOM.render(
            element,
            document.getElementById('root')
            );
    ```
    * 만일 HTML이나 XML에 자바스크립트 코드를 사용하고싶으면 ( )를 사용함
        자바스크립트를 사용하고싶으면 { }를 사용함
    ***
    *   Book.jsx
    ```js
        import React from "react";
        export default function Book(props){
            return(
        <div>
            <h1>{`이 책의 이름은 ${props.name}입니다.`}</h1>
            <h2>{`이 책은 총 ${props.numOfPage}페이지로 이뤄져 있습니다.`}</h2>
        </div>
        );
    }
    ```
    *   Library.jsx
    ```js
    import React from "react";
    import Book from "./Book";

    export default function Library(){
        return (
        <div>
            <Book name="처음만난 파이썬" numOfPage={300} />
            <Book name="처음 만난 AWS" numOfPage={400} />
            <Book name="처음 만난 리액트" numOfPage={500}/>

        </div>
        );
    }
    ```
    *   index.js
    ```js
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import './index.css';
    import App from './App';
    import reportWebVitals from './reportWebVitals';
    import Library from './chapter_03/Library';
    import Library from './chapter_03/Library';
    import Book from './chapter_03/Book';
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
     <React.StrictMode>
        <Library>
     </React.StrictMode>
    );

    // If you want to start measuring performance in your app, pass a function
    // to log results (for example: reportWebVitals(console.log))
    // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
    reportWebVitals();

    ```
* 엘리먼트의 정의
    * 엘리먼트는 리액트 앱을 구성하는 요소를 의미함
    * 공식페이지에는 "엘리먼트는 리액트 앱의 가장 작은 빌딩 블록들"이라고 설명하고 있음
    * 웹사이트의 경우 DOM 엘리먼트이며,HTML 요소를 의미함

* 리액트 엘리먼트와 DOM엘리먼트의 차이
    * 리액트 엘리먼트는 Virtual DOM의 형태를 취하고 있음
    * DOM 엘리먼트는 페이지의 모든 정보를 갖고 있어 무겁움
    * 반면 리액트 엘리먼트는 변화한 부분만 갖고 있어 가벼움

* 엘리먼트의 생김새
    * 리액트 엘리먼트는 자바스크립트 객체의 형태로 존재함
    * 컴포넌트(Buttob 등),송성(color 등) 및 내부의 모든 children을 포함하는 일반 js 객채
    * 이 객채는 마음대로 변경할 수 없는 불변성을 갖고 있음

    * 내부적으로 자바스크립트 객체를 만드는 역할을 하는 함수는 createElement() 다.
    
* 엘리먼트 특징
    * 리액트 엘리먼트의 가장 큰 특징은 불변성이다.
        즉, 한 번 생성된 엘리먼트의 children이나 송성을 바꿀 수 없다.

* 엘리먼트 렌더링하기
    * 일레먼트를 렌더링 하기 위해 다음과 같은 코드가 필요함
        ```js
            const element = <h1>안녕 리액트</h1>
            ReactDOM.render(element, document.getElementById('root'));
        ```
        * render()함수를 사용함
            
* 렌더링된 엘리먼트 업데이트
    ```js
        import React from "react";
        export default function Clock(props){
            return(
                <div>
                <h1>안녕, 리액트</h1>
                <h2>현재 시간 : {new Date().toLocaleTimeString()}</h2>
                </div>
            );
        }
    ```
## 컴포넌트와 Props

* 컴포넌트
    * 컴포넌트 구조라는 것은 작은 컴포넌트가 모여 큰 컴포넌트를 구성하고, 다시 이런 컴포넌트들이 모여 전체 페이지를 구성한다는 것을 의미한다.
    * 컴포넌트 재사용이 가능하기 때문에 전체 코드의 양을 줄일 수 있어 개발 시간과 유지 보수 빙ㅅㅇㄷㅎ 줄일 수 있다.
    * 컴포넌트는 자바스크립트 함수와 입력과 출력이 있다는 면에서 유사함
    * 다만 입력은 Props가 담당하고, 출력은 리액트 엘리먼트의 형태로 출력됨
    * 엘리먼트를 필요한 만큼 만들어 사용한다는 면에서 객체 지향의 개념과 비슷함

* Props
    * props는 prop(property: 속성,특성)의 준말
    * 이 props가 바로 컴포넌트의 속성이다
    * 컴포넌트에 어떤 속성, props를 넣느냐에 따라서 속성이 다른 엘리먼트가 출력됨
    * props는 컴포넌트에 전달 할 다양한 정보를 담고 있는 자바스크립트 객체다
    * 에어비앤비의 예도 마찬가지
* Props의 특징
    * 읽기 전용이다. 변경할 수 없다는 의미
    * 속성이 다른 엘리먼트를 생성하려면 새로운 props를 컴포넌트에 전달해야됨

* pure함수 vs Impure 함수
    * pure함수는 인수로 받은 정보가 함수 내부에서도 변하지 않는 함수
    * Impure함수는 인수로 받은 정보가 함수 내부에서 변하는 함수  
* 리액트 공식 문서에는 컴포넌트의 특징을 다음과 같이 설명함
    * 모든 리액트 컴포넌트는 그들의 props에 관해서는 Pure함수 간은 역할을 해야 한다.
    * 다시말해 모든 리액트 컴포넌트는 props를 직접 바꿀 수 없고, 같은 props에 대해서는 항상 같은 결과를 보여준다
# 3월 20일
## 1장 리액트 소개
```rudy 
    React : 사용자 인터페이스를 만들기 위한 자바스크립트 라이브러리
``` 
-> 웹 및 앱 유저 인터페이스를 위한 라이브러리
react.dev
리액트의 프레임워크 -> Next.js
리액트 개념
복잡한 사이트를 쉽고 빠르게 만들고 , 관리하기 위해 만들어진 것이 리액트다
다른 표현으로는 spa(single page application)를 쉽고 빠르게 만들 수 있도록 해주는 도구
웹 전체가 바뀌는 방식이 동기식이고
변환부분만 출력하는게 비동기식 이다. 
그렇기 때문에 비동기식이 더 빠르다.

## 1-1 리액트 장점
 렌더링 속도와 업데이트가 빠르다. 이것을 가능하게 만드는 것은 Virtual DOM 때문이다.
 DOM(Document Object Model)이란 xml, HTML 문서의 각 항목을 계층으로 표현하여 생성,변형 삭제할 수 있도록돕는 인터페이스
 DOM 조작이 비효율적이고 느려서 고안된 방법이 Virtual DOM 이다.
 DOM은 동기식, Virtual DOM 비동기식이다.
 2 컴포넌트 기반 구조
     리액트의 모든 페이지는 컴포넌트로 구성됨
     하나의 컴포넌트는 다른 여러 개의 컴포넌트의 조합으로 구성할 수 있다.
     그래서 리액트로 개발하다 보면 레고 블록을 조립하는 것 처럼 컴포넌트를 조합해서 웹사이트를 개발함
 재사용성이 뛰어남
 ComponentName.js
 같은 이름으로 쓴다(ComponentName) 
 function componentName(){   }
 메타(구 페이스북)에서 오픈소스 프로젝트로 관리하고 있어 계속 발전중
 
 활발한 지식 공유 & 커뮤니티
 모바일 앱 개발 가능
 리액트 네이티브라는 모바일 환경 ui프레임워크를 사용하면 크로스 플랫폼모바일 앱 개발이 가능함
## 1-2 리액트 단점
* 방대한 학습량
    * 자바스크립트를 공부한 경우 빠르게 학습 가능함

* 높은 상태 관리 복잡도
    * state, component life cycle 등의 개념이 있지만 그리 어렵지 않음


## 2.리액트 시작하기
    부트스트랩
        CDN이라 프레임워크관리하는 서버에서 링크만 가져와서 사용가능하게 만드는 것

## 3월 13일 강의
