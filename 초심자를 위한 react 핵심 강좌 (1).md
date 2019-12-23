[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (1)

김민준

2019.12.23



```
리액트를 제대로, 쉽고, 재밌게 !
```

**[ 프론트엔드 라이브러리란? ]**

요즘의 웹은... 단순한 웹 페이지가 아닌 **웹 애플리케이션**

UI(User Interface) 를 동적으로 관리하기 위해서는 수 많은 **"상태"** 를 관리해줘야 한다.

다양한 라이브러리/프레임워크...

Angular, React, Vue, ...



**[ Virtual DOM ]**

우리는 지속해서 데이터가 변화하는 대규모 애플리케이션을 구축하기 위해 리액트를 만들었습니다.

기존 라이브러리/프레임워크의 키워드.

- 모델 과 변화 (Mutation)

React: 그냥 Mutation 을 하지 말자. 그 대신에, 데이터가 바뀌면 그냥 뷰를 날려버리고 새로 만들어버리면 어떨까? 

- 더 깊은 이해를 위해서는 브라우저 동작 과정에 대해 아는 것도 좋지만, 아무튼 브라우저는 브라우저상의 변화를 적용시키기 위해서는 다시 그리는 과정을 거쳐야 하고, 이는 변화가 많을 수록 많은 리소스 사용을 야기한다 는 정도의 개념이해 정도만 하고 넘어가도 좋음!

- Real DOM 과 In-memory DOM 의 Diff And... Patch !
- [React and the Virtual DOM](https://www.youtube.com/watch?v=muc2ZF0QIO4&feature=youtu.be)



**[ 리액트를 특별하게 만드는 점 ]**

어마어마한 생태계

- 리액트 생태계의 개발자들 열정 === 2006년 jQuery 때의 열정 ㅋ

사용하는 곳이 많다.

한번 사용하면 좋아하게 된다. (!?)

한마디로 핫함 =ㅅ=)...



**[ 리액트 프로젝트 시작하기 ]**

리액트를 시작하기에 앞서 살펴 볼 2가지 도구

- Webpack
  - bundler... 특정 확장자를 특정 경로에 특정 이름으로 떨굴 수 있음.
  - 프론트 엔드 도구임 !

- babel
  - JavaScript compiler...

웹 에디터: [CodeSandbox](https://codesandbox.io/)



**[ JSX ] **

HTML 같아 보이지만, javascript !

Rules.

- 꼭 닫혀있어야 하는 태그

  - <input type="text" /> 도 마찮가지 !

- 감싸져 있는 엘리먼트

  - Fragment

- JSX 안에 자바스크립트 값 사용하기

  - `{}`

  - const, let, arrow function...

  - 조건부 렌더링

    - 삼항연산자

    ```jsx
    {
    	1 + 1 === 2 
    	? '맞다',
    	: '틀리다'
    }
    ```

    - 브라우저 로드와 동시에 실행하고 싶다. IIFE.

- style
  - HTML 에서의 style은 (style='background-color: white;...') '문자열' 이지만, JSX 에서의 style 은 {} (오브젝트) 이다.
  - camelCase 를 사용한다. background-color → backgroundColor
  - 연산도 가능하다. padding: 5 + 5 + 'px'
  - `class`="App" 가 아니라, `className`="App"

- 주석

  - 기존 `//`,  `/* */` 를 `{}` 로 감싸줘야 한다.

  - JSX 태그 사이에도 작성할 수 있다.

  - ```jsx
    <h1 somethig="anything" // 이렇게 쓰는게 가능해>
    ```



**[ props]**

리액트에서 데이터를 다룰 때 사용하는 개념

props

```jsx
<Child value="value" />
```

- **부모**가 **자식**에게 넘겨주는 값. (엄청 중요해 !!!, 자식입장에서는 읽기전용.)
- static defaultProps = { name: '기본이름' } === MyName.defaultProps = { name: '기본이름' }

※ 클래스 컴포넌트 와 함수형 컴포넌트

- 함수형 컴포넌트 에서는 상단의 `import React, { Component } from 'react';` 에서 `{ Component }` 를 생략해도 된다. 단, React 는 항상 필요한데, JSX 를 render 할 때 사용하기 때문이다.
- [비구조화 할당 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- 함수형 컴포넌트는 state 기능이 없고, LifeCycle 이 빠져있다. 초기 마운트 속도가 아주 미세하게 빠르고, 불필요한 기능은 없으므로 메모리 자원도 덜 사용한다. 그래서 만약에 컴포넌트를 만들 때 단순히 값을 받아와서 보여주기만 하는 용도라면 함수형 컴포넌트를 사용하는 것을 권장... 하지만 컴포넌트를 수도없이 많이 만들게 아니라면, 성능적으로 큰 차이는 없다... 간단한 컴포넌트를 만들 때 편리한 것 정도로 봐도... =ㅅ=)!?...



**[ state ]**

컴포넌트 자신이 처음부터 들고있는 값. 

만약 변화가 필요할 때는 컴포넌트 내장함수 가운데 하나인 `setState()` 를 통해서 값을 설정한다.

- state 정의

- ```jsx
  state = {
  	number: 0
  }
  ```

- state 값 사용

- ```jsx
  { this.sate.number }
  ```

- 핸들러 등록

- ```jsx
  handleIncrease = () => {
  	this.state.number = this.state.number + 1; (x) Nope! 값이 변경됐는지 감지하지를 못한다. re-rendering 을 하지않는다.
      
    this.setState({
      number: this.state.number + 1
    })
  }
  handelDecrease = () => {
    this.setState({
      number: this.state.number + 1
    })
  }
  ```

- JSX 내 이벤트 등록

- ```jsx
  <button onClick={this.handleIncrease}>+</button>
  <button onClick={this.handleDecrease}>-</button>
  ```



※ handleIncrease 와 handleDecrease 를 arrow function 으로 정의한 이유

- 일반함수로 정의한 this 의 경우

- ```jsx
  constructor(props) {
  	super(props);
  	this.handleIncrease = this.handleIncrease.bind(this);
    this.handleDecrease = this.handleDecrease.bind(this);
  }
  ```

  처럼 생성자 함수에 this 를 bind 해야만 컴포넌트 자체를 가리키는 this 를 가질 수 있게되기 때문... arrow function 은 따로 생성자 함수를 따로 정의해주지 않아도 된다.

※ props 는 읽기전용, state 는 변경할 수도 있다는 것 !

