# 유건호 202130418

# 5월 22일
### 리스트와 키
- 리스트는 자바스크립트의 변수나 객체를 하나의 변수로 묶어놓은 것

- map() 2를 곱한 후 doubled라는 배열에 다시 넣는 코드
``` js
const doubled = numbers.map((number)=> number*2)
```

```js numberList.jsx
export default function NumberList(){
    const numbers = [1,2,3,4,5]

    const todos = [
        {id: 1, name:"홍길동1"},
        {id: 2, name:"홍길동2"},
        {id: 3, name:"홍길동3"},
        {id: 4, name:"홍길동4"},
        {id: 5, name:"홍길동5"},
    ]
    const listItems = numbers.map((numbers)=>
        <li key={numbers.toString()}>{numbers}</li>
    )
    const todoItems = todos.map((todo)=>
        <li key={todo.id}>{todo.name}</li>
    )
    const indexItems =  todos.map((todo,index)=>
        <li key={index}>{todo.name}</li>
    )
    return(
        <>
            <ul>{listItems}</ul>
            <ul>{todoItems}</ul>
            <ul>{indexItems}</ul>
        </>
    )
}

```
- 키 : 리스트에서 아이템을 구별하기 위한 고유한 문자열
- 이 키는 리스트에서 어떤 아이템 변경,추가 또는 제거되었는지 구분하기 위해 사용함
- 키는 같은 리스트에 있는 엘리먼트 사이에서만 고유한 값이면 된다.

### 폼
- 폼은 일반적으로 사용자로부터 입력을 받기위한 양식에서 많이 사용됨
### 제어 컴포넌트
- 제어 컴포넌트는 사용자가 입력한 값에 접근하고 제어할 수 있도록 해주는 컴포넌트다

```js NameForm.jsx
import { useState } from "react";

export default function NameForm(){
    const [value,setValue] = useState('')
    
    const handleChange = (e) => {setValue(e.target.value)}
    const handleSubmit = (e) => {alert('입력한 이름: '+value)
    e.preventDefault()
}
return(
    <form onSubmit={handleSubmit}>
        <label>
            이름:
            <input type="text" value={value} onChange={handleChange}/>
            <button type="submit">제출</button>
        </label>
    </form>
)
}
```
- textarea : 텍스트박스 안 글씨
```js RequestForm.jsx
import { useState } from "react";

export default function RequestForm(){
    const [value,setValue] = useState('요청사항을 입력하세요.')

    const handleChange = (e) => {setValue(e.target.value)}
    const handleSubmit = (e) => {alert('요청사항: '+value)
        e.preventDefault()
    }
    return(
        <form onSubmit={handleSubmit}>
            <label>
                요청사항:
                <textarea value={value} onChange={handleChange}/>
                <button type="submit">제출</button>
            </label>
        </form>
    )
}

```
```js RequestForm.jsx(select)
import { useState } from "react";

export default function RequestForm(){
    const [value,setValue] = useState('요청사항을 입력하세요.')

    const handleChange = (e) => {setValue(e.target.value)}
    const handleSubmit = (e) => {alert('요청사항: '+value)
        e.preventDefault()
    }
    return(
        <form onSubmit={handleSubmit}>
            <label>
                요청사항:
                <select value={value} onChange={handleChange}>
                    <option value = "사과">사과</option>
                    <option value = "바나나">바나나</option>
                    <option value = "오렌지">오렌지</option>
                </select>
                <input type="file"/>
                <button type="submit">제출</button>
                
            </label>

        </form>
    )
}

```
- select 태그도 textarea와 동일함
- file input 태그는 그 값이 읽기 전용이기 떄문에 리액트에서는 비제어 컴포넌트가 된다.
# 5월 8일
### 이벤트
```js
    import { useState } from "react"

export default function Toggle(props){
    const [isToggleOn,setIsToggleOn] = useState(true)

    const handleClick = () =>{
        setIsToggleOn ((isToggleOn) => !isToggleOn)
    } 

    return(
        <button onClick={handleClick}>
            {isToggleOn ? '커짐':'꺼짐'}
        </button>
    )
}
```
### Arguments 전달하기
- 함수를 정의할 때는 파라미터 혹은 매개변수, 함수를 사용할때는 아귀먼트 혹은 인수라고 부른다
- 이벤트 핸들러에 매개변수를 전달해야 하는 경우도 많다.

- 260 page

```jsx
    export default function MyButton(props){
        const handleClickDelete = (id,e) => {
         console.log(id,e.target)
        }
        return(
            <button onClick = {(e) => handleClickDelete(1,e)}>삭제하기</button>
        )
    }
```
### 조건부 렌더링
- 렌더링해야 될 컴포넌트를 변수처럼 사용하는 방법이 엘리먼트 변수다.
- 277~278 page
```js LoginControl.jsx
    import { useState } from "react";
    import Greeting from "./Greeting";

    export default function LoginControl(props){
        const [isLoggedIn,setIsLoggedIn] = useState(false)

        const handleLoginClick = () => {setIsLoggedIn(true)}

        const handleLogoutClick = () => {setIsLoggedIn(false)}

        //엘리먼트 변수
        let button;
        if(isLoggedIn){
            button = <LogoutButton onClick={handleLogoutClick}/>
        }else{
            button = <LoginButton onClick={handleLoginClick}/>
        }
        return(
            <>
                <Greeting isLoggedIn={isLoggedIn}/>
                {button}
            </>
        )
    }

    function LoginButton(props){
        return(
            <button onClick={props.onClick}>로그인</button>
        )
    }
    function LogoutButton(props){
        return(
            <button onClick={props.onClick}>로그아웃</button>
        )
    }

```

```js Greeting.jsx
    export default function Greeting(props){
    if(props.isLoggedIn){
        return <p>안녕하세요. 반갑습니다.</p>
    }else{
        return <p>로그인 하세요!</p>
    }
}
```


### 인라인 조건
- 인라인 if
    - if문을 직접 사용하지 않고 , 동일한 효과를 내기 위해 && 논리 연산자를 사용함
    - && 는 and연자로 모든 조건이 참일때만 참이 된다.
    - 첫 조건이 거짓이면 두번째 조건은 판단할 필요가 없다. 단축평가
    - 판단하지않고 그대로 결과값을 리턴함

- 인라인 if - else
    - 상향 연산자를 사용함 조건식? 참일 경우 : 거짓일 경우
    - 문자열이나 엘리먼트를 넣어 사용할 수도 있다.
### 컴포넌트 렌더링 막기
- 컴포넌트를 렌더링하고 싶지 않으때 null을 리턴한다.
``` js
    function WarningBanner(props){
        if(!props.warning){
            return null;
        }
        return(
            <div>경고</div>
        )
    }
```

```js MainPage.jsx
    import { useState } from "react"
import WarningBanner from "./WarningBanner"
export default function MainPage(props){
    const [showWarning,setShowWarning] = useState(false)

    const handleToggleClick = () => {
        setShowWarning(prevShowWarning => !prevShowWarning)

    }

    return(
        <>
            <WarningBanner warning = {showWarning}/>
            <button onClick={handleToggleClick}>
                {showWarning ? '감추기' : '보이기'}
            </button>
        </>
    )
}
```
``` js WarningBanner.jsx
export default function WarningBanner(props){
    if(!props.warning){
        return null
    }
    return(
        <div>경고!</div>
    )
} 
```

```js Toolbar.jsx
import LandingPage from "./LandingPage"
export default function Toolbar(props){
    const {isLoggedIn,onClickLogin,onClickLogout} = props

    return(
        <div>
            {isLoggedIn && <span>환영합니다.</span>}
            {isLoggedIn
                ? <button onClick={onClickLogout}>로그아웃</button>
                : <button onClick={onClickLogin}>로그인</button>
                 
            }
        </div>
    )
}
```

```js LandingPage.jsx
import { useState } from "react";
import Toolbar from "./Toolbar";
export default function LandingPage(props){
    const [isLoggedIn,setIsLoggedIn] = useState(false)

    const onClickLogin = () => {
        setIsLoggedIn(true)
    }
    const onClickLogout = () => {
        setIsLoggedIn(false)
    }
    return(
        <div>
            <Toolbar
            isLoggedIn = {isLoggedIn}
            onClickLogin = {onClickLogin}
            onClickLogout = {onClickLogout}
            />
            <div>소풀과 함께하는 리액트 공부!</div>
        </div>
    )
}
```
# 5월 1일
### 훅의 규칙
- 무조건 최상위 레벨에서만 호출해야 한다.
  - 반복묵이나 조건문 또는 중첩된 함수들 안에서 훅을 호출하면 안됨
  - 이 규칙에 따라서 혹은 컴포넌트가 렌더링 될 때마다 같은 순서로 호출되어야 한다.
- 함수형 컴포넌트에서만 훅을 호출해야 한다
  - 그렇기 때문에 자바스크립트 함수에서 훅을 호출하면 안됨
  - 훅은 함수형 컴포넌트 혹은 직접 만든 커스텀 훅에서만 호출 가능함


#### 커스텀 훅
- userStatus를 이용해 온라인인지 아닌지를 나타내는 코드
```jsx userStatus.jsx
    import { useEffect,useState } from "react"

    export default function UserStatus(props){
        const [isOnline, setIsOnline] = useState(null)

        useEffect(()=>{
            function handleStatusChange(status){
                setIsOnline(status.isOnline)
            }
            serverAPI.subscribeUserStatus(props.user.id,handleStatusChange)
            return () => {
                serverAPI.unsubscribeUserStatus(props.user.id,handleStatusChange)
            }
        })
        if(isOnline === null){
            return '대기중...'
        }
        return isOnline?'온라인':'오프라인'
    }

```
- 온라인이면 이름을 초록색 오프라인이면 검은색으로 나타내는 코드
```jsx  UserListItem.jsx
    import { useEffect,useState } from "react"

    export default function UserListItem (props){
        const [isOnline, setIsOnline] = useState(null)

        useEffect(()=>{
            function handleStatusChange(status){
                setIsOnline(status.isOnline)
            }
            serverAPI.subscribeUserStatus(props.user.id,handleStatusChange)
            return () => {
                serverAPI.unsubscribeUserStatus(props.user.id,handleStatusChange)
            }
        })
    
        return (
            <li style={{ color: isOnline ? 'green' : 'black'}}>
                {props.user.name}
            </li>
        )
    }
```  
- use로 시작하는 훅을 만들고 내부에서 다른 훅을 호출하면됨

```jsx UserStatus.jsx
import { useEffect,useState } from "react"
import useUserStatus from "./useUserStatus"

export default function UserStatus(props){
    const isOnline=useUserStatus[props.user.id]

   
    if(isOnline === null){
        return '대기중...'
    }
    return isOnline?'온라인':'오프라인'
}
```
```jsx useUserStatus.jsx
    import { useEffect,useState } from "react"

    export default function useUserStatus(userId){
        const [isOnline, setIsOnline] = useState(null)

        useEffect(()=>{
            function handleStatusChange(status){
                setIsOnline(status.isOnline)
            }
            serverAPI.subscribeUserStatus(userId,handleStatusChange)
            return () => {
                serverAPI.unsubscribeUserStatus(userId,handleStatusChange)
            }
        })

    }
```
```jsx UserListItem.jsx
    import { useEffect,useState } from "react"
    import useUserStatus from "./useUserStatus"

    export default function UserListItem (props){
        const isOnline = useUserStatus(props.user.id)

    
        return (
            <li style={{ color: isOnline ? 'green' : 'black'}}>
                {props.user.name}
            </li>
        )
    }

```
```jsx useCounter.jsx 
    import { useState } from "react";

    export default function (initialValue){
        const [count,setCount] = useState(initialValue)

        const increaseCount = () => setCount((count) => count + 1)
        const decreaseCount = () => setCount((count) => Math.max(count-1,0))

        return [count,increaseCount,decreaseCount]

    }

```
```jsx Accommodate.jsx
import { useState,useEffect } from "react";
import useCounter from "./useCounter";

const MAX_CAPACITY = 10

export default function Accommodate(props){
    const [isFull,setIsFull] = useState(false)
    const [count,increaseCount,decreaseCount] = useCounter(0)
    
    useEffect(()=>{
        console.log("======================")
        console.log("useEffect() is called.")
        console.log(`isFull: ${isFull}`)
    })

    useEffect(() =>{
        setIsFull(count >= MAX_CAPACITY)
        console.log(`Current count value ${count}`)
    },[count])
    return(
        <div>
            <p>{`총 ${count}명 수용했습니다`}</p>
            <button onClick={increaseCount} disabled={isFull}>입장</button>
            <button onClick={decreaseCount}>퇴장</button>
            {isFull && <p style={{color:'red'}}>정원이 가득 찼습니다.</p>}
        </div>
    )
}

```
### 이벤트 처리하기
- DOM에서 클릭 이벤트를 처리하는 방식 
```js
<button onClick="activate()">
```
- React에서 클릭 이벤트를 처리하는 방식
```jsx
<button onClick={activate}>
``` 
# 4월 17일
npm start
### 훅(Hook)
* 클래스 컴포s넌트에서 생성자에 state를 정의하고, setState()함수를 통해 state를 업데이트한다
* 예전에 사용하던 함수형 컴포넌트는 별도로 state를 정의하거나, 컴포넌트의 생명주기에 맞춰서 어떤 코드가 실행되도록 할 수 없다.
* 함수형 컴포넌트 state나 생명주기 함수의 기능을 사용하게 해주기 위해 추가된 기능이 바로 훅이다
* 함수형 컴포넌트도 훅을 사용하여 클래스형 컴포넌트의 기능을 모두 동일하게 구현할 수 있게 되었다.
* hook이란 `state와 생명주기 기능에 갈고리를 걸어 원하는 시점에 정해진 함수를 실행되도록 만든 함수`를 의미한다.
* 훅의 이름은 모두 `use`로 시작함
* 사용자 정의 훅(custom hook)을 만둘 수 있으며, 이 경우에 이름은 자유롭게 할 수 있으나 `use`로 시작할 것을 권장함

### useState
* useState는 함수형 컴포넌트에서 state를 사용하기 위한 훅이다.
* 다음 예제는 버튼을 클릭할 때마다 카운트가 증가하는 함수형 컴포넌트다.
* 하지만 증가

```jsx
import { useState } from "react"
export default function Counter(props){
// let count = 0
    const [count,setCount]= useState(0)
    return(
    <>
    <p>총 {count}</p>
    <button onClick={()=> setCount(count+1)}>
            클릭
    </button>
        
    </>
    )
}
```

### useEffect
* useState와 함께 가장 많이 사용하는 훅
* 이 함수는 사이트 이팩트를 수행하기 위한 것
* 영어로 side efect는 부작용(부수적인 작용)을 의미함.
* 예를 들면 서버에서 데이터를 받아오거나 수동으로 DOM을 변경하는 등의 작업을 의미함
* 이 작업을 이팩트라고 부르는 이유는 이 작업들이 다른 컴포넌트에 영향을 미칠 수 있으며, 렌더링 중에는 작업을 완료할 수 없기 떄문이다. 렌더링이 끝난 이후 실행되어야 하는 작업들이다.
* 컴포넌트의 생명주기 함수와 같은 기능을 하나로 통합한 기능을 제공한다.

* useEfect()함수는 다음과 같이 사용한다
* 첫번째 파라미터는 이팩트 함수가 들어가고, 두 번째 파라미터로는 의존성 배열이 들어간다
```jsx
    useEffect(이팩트함수 , 의존성배열)
```
* 의존성 배열은 이팩트가 의존하고 있는 배열로, 배열 안에 있는 변수 중에 하나라도 값이 변경되었을 때 이팩트 함수가 실행됨
* 이팩트 함수는 처음 컴포넌트가 렌더링 된 이후, 그리고 재 렌더링 이후에 실행됨
* 만약 이팩트 함수가 마운트와 언마운트 될때만 한번씩 실행되게 하고 싶으면 빈 배열을 넣으면 됨
이 경우 props나 state에 있는 어떤 값에도 의존하지 않기 때문에 여러번 실행되지 않는다.

```jsx
import { useEffect, useState } from "react"

export default function Counter(props){
    // let count = 0
    const [count,setCount]= useState(0)

    useEffect(()=>{
        document.title = `총 ${count}번 클릭했습니다.`
    })

    return(
        <>
            <p>총 {count}</p>
            <button onClick={()=> setCount(count+1)}>
                클릭
            </button>
            
        </>
    )
}
```

### userMemo
* useMemo() 혹은 Memoized value를 리턴하는 훅
* 이전 계산값을 갖고 있기 때문에 연산량이 많은 작업의 반복을 피할 수 있다.
* 이 혹은 렌더링이 얼마나 일어나는 동안 실행된다
* 따라서 렌더링이 일어나는 동안 실행돼서는 안될 작업을 넣으면 안된다.
* 예를 들면 useEffect에서 실행되어야 할 사이트 이팩트 같은 것을 말한다.
------
* 다음 코드와 같이 의존성 배열을 넣지 않을 경우, 렌더링이 일어날 때마다 매번 함수가 실향됨
* 따라서 의존성 배열을 넣지 않는 것은 의미가 없다.
* 만약 빈 배열을 넣게 되면 컴포넌트 마운트 시에만 함수가 실행된다
```js
    const memoizedValue = useMemo(
        () => computeExpensivaValue(a,b)
    );
```

### useCallback
* useCallback()혹은 useMemo()와 유사한 역할을 한다
* 차이점은 값이 아닌 함수를 반환한다는 점이다.
* 의존성 배열을 파라미터로 받는것은 useMemo와 비슷함
### useRef
* useRef() 혹은 래퍼런스를 사용하기 위한 훅
* 래퍼런스란 특정 컴포넌트에 접근할 수 있는 객체를 의미함
```const refContainer = useRef(초깃값);```
***
### FocusButton.jsx 
```js 
import { useRef } from "react";

export default function FocusButton(props){
    const inputElem = useRef(null)

    const onButtonClock = () => {
        inputElem.current.focus()
    }
    return(
        <>
            <input ref={inputElem} type="text"/>
            <button onClick={onButtonClock}>Focus th input</button>
        </>
    )
}
```
---
### MeasureEx.jsx
```js
    import { useCallback, useState } from "react";

    export default function MeasureEx(props){
    const[height, setHeight]= useState(0)
    const measuerRef = useCallback(node => {
        if(node != null){
            setHeight(node.getBoundingClientRect().height)
        
        
        }
    },[])
    return(
        <>
            <h1 ref={measuerRef}>안녕, 리액트</h1>
            <h2>위 헤더의 높이는 {Math.round(height)}px 입니다.</h2>
        </>
    )
}
```

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
