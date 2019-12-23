[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (2)

김민준

2019.12.23



**[ LifeCycle API ]**

크게,

나타날 때 (Mounting): **컴포넌트**가 브라우저 상에 나타난다는 것.

업데이트 될 때 (Updating): props 나 state 가 변경됐을 때.

사라질 때 (Unmounting): 컴포넌트가 브라우저에서 사라질 때.

- v16.3

![v16.3](https://jistol.github.io/assets/img/frontend/react-lifecycle-methods/1.jpeg)

constructor, getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate, (React updates DOM and refs), componentDidMount, componentDidUpdate, componentWillUnmount... **모두 함수다 !**

- **constructor**: 컴포넌트가 브라우저에 처음 나타나게 될 때, 만들어지는 과정에서 가장 먼저 실행되는 함수. 

  - 컴포넌트의 state 를 초기설정 할 때

- **getDerivedStateFromProps**

  - props 로 받은값을 state 에 그대로 동기화 시키고 싶을 때
  - Mounting 과정에서도 실행되고, props 가 변경됐을 때도 실행된다.
    - **shouldComponentUpdate (중요)**
      - porps 나 state 가 변경됐을 때, virtualDOM 에도 rendering 을 할지/말지 결정하는 함수.
      - 컴포넌트가 업데이트 되는 성능을 최적화 하고 싶을 때 사용한다.
        - : 컴포넌트는 기본적으로 부모컴포넌트가 re-redering 될 때 그 부모컴포넌트의 자식컴포넌트까지 render 가 실행되도록 되어있다. 하지만 이 과정이 불필요해질 때가 있다. render 는 virtualDOM 에 그리는데 (그 후 realDOM 과 diff, patch...) 이 virtualDOM 에 그리는 것 조차 아끼고 싶을 때...
        - true, false 반환으로 render 가 되거나 멈추거나.
        - 따로 선언해서 사용하지 않으면 기본적으로 `return true`

- ```javascript
  static getDerivedStateFromProps(nextProps, prevState) {
    // nextProps: 다음으로 받아 올 props 값
    // prevState: 업데이트 되기 전의 상태
    if (prevState.value !== nextProps.value) {
      return {
        value: nextProps.value
      }
    }
    return null; // 변경없음
  }
  ```

  ```javascript
  shouldComponentUpdate(nextProps, nextState) {
  	if ( nextProps.value === 10 ) return false;
  	return true;
  }
  // 인 경우 nextProps.value 이 10 일 때 rendering 이 스킵된다.
  ```

  

- **render**: 어떤 DOM 을 만들게 될지, 내부에 있는 태그들에는 어떤 값을 전달해주게 될지 등을 정의

  - **getSnapshotBeforeUpdate**

    - 렌더링을 한 다음에 브라우저에 반영되기 바로 직전에 호출되는 함수.
    - 스크롤의 위치, 해당 DOM 의 크기 를 사전에 가져오고 싶을 때
    - 업데이트 되기 직전의 DOM 상태를 return 해서 componentDidUpdate 에서 받아올 수 있음.

    ```javascript
    getSnapshotBeforeUpdate(prevProps, prevState) {
    	// prevProps, prevState - 이전 props 와 이전 상태를 확인할 수 있다.
      if ( prevState.array !== this.state.array ) {
        const {
          scrollTop, scrollHeight
        } = this.list;
        
        return {
          scrollTop, scrollHeight
        };
      }
    }
    
    componentDidUpdate(prevProps, prevState, snapshot) {...}
    // componentDidUpdate 에서 snapshot 으로 받아올 수 있다.
    ```

    

- **componentDidMount**

  - 외부라이브러리. 예로 D3.js, chartist-js, masonry 와 같은 차트라이브러리를 사용하게 될 때, 특정 DOM 에 차트를 그려주세요~ 식의 코드 작성시
  - 데이터 (api, ajax, GraphQL) 요청 시
  - DOM 관련된 작업: 이벤트 리스너 등록, 스크롤 설정, 크기 읽어오기 등
  - 만든 컴포넌트가 브라우저에 **나타난 시점**에 **어떤 작업**을 하겠다 !

- **componentDidUpdate**

  - 위 과정을 마치고 컴포넌트가 업데이트 된 후에 실행되는 함수.
  - 기존 state 와 현재 state 가 다를 때, 어떤 작업을 하겠다 !

- ```javascript
  componentDidUpdate(prevProps, prevState, snapshot) {
    // prevProps, prevState: 업데이트 되기 전의 값.
    if ( prevProps.value !== this.props.value ) {
      console.log("value 값이 바뀌었다!", this.props.value);
    }
  }
  ```

- **componentWillUnmount**
  - 이벤트 리스너를 제거하거나 할 때...

- **componentDidCatch**

  - 컴포넌트에 에러 발생

- ```jsx
  this.state = {
    error: false
  }
  
  componentDidCatch(error, info) {
  	this.setState({
  		error: true
  	});
    // API 를 통해 서버로 오류 내용 날리기
  }
  
  render() {
    if (this.state.error) {
        return (
      		<div>error!</div>
  		  )
    }
  }
  ```

  - error 가 발생할 수 있는 컴포넌트의 부모컴포넌트 에서 작성해야 한다.





※ 좌측의 설명 (한번 읽어보고 대략적인 이해만 하고 패스!)

- 렌더 단계 (Render Phase): 순수(!)하고 사이드 이펙트가 없다. 리액트에 의해 보류, 중단 또는 재작성될 수 있다. (Pure and has no side effects. May be puased, aborted or restated by React.)
- 커밋 이전 단계 (Pre-Commit Phase): DOM 을 읽을 수 있다. (Can read the DOM.)
- 커밋 단계 (Commit Phase): DOM 으로 작업(조작?) 가능. 사이드 이펙트를 실행하고 업데이트를 스케쥴링 할 수 있다. (Can work with DOM, run side effects. schedule updates.)

※ 참조 v16.4

![v16.4](https://jistol.github.io/assets/img/frontend/react-lifecycle-methods/2.png)

※ componentWillMount 라는 애가 있었는데 사라짐... 

※ componentWillRecevieProps 라는 애가 있었는데 사라짐... getDerivedStateFromProps 와 대응... 하지만 사용방법이 다름. (객체를 리턴하는 방식 `return { value: nextProps.value }`)

※ componentWillUpdate 도 사라짐...

※ [누구든지 하는 리액트 문서 - LifeCycle API](https://react-anyone.vlpt.us/05.html)

※ 개념만 훑기...