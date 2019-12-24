[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (5)

김민준

2019.12.24



**[ 배열에 데이터 삽입하기 ]**

**자식 컴포넌트가 부모한테 값 전달하기**

개요

- 부모컴포넌트에 handleCreate 메소드를 만들고

```jsx
// Parent.js
handleCreate = (data) => {
	...
}
```

- 이 메소드를 우리가 만든 자식컴포넌트한테 props(onCreate) 로 전달해주고

```jsx
// Parent.js
<Child onCreate={this.handleCreate} />
```

- 자식컴포넌트에서 이 props(onCreate) 로 전달한 함수를 호출시켜서

```jsx
// Child.js
handleSubmit = (e) => {
	e.preventDefault(); // submit 이벤트로 인한 브라우저 새로고침 방지
	this.props.onCreate({
		...
	}) // 부모컴포넌트로 부터 전달받은 메소드 호출
}

...

<form onSubmit={this.handleSubmit}> 
	...
</form>
```

- 이 데이터값이 부모컴포넌트에 들어가게끔 하면 된다.

```jsx
// Parent.js
state = {
	information: [],
}

handleCreate = (data) => {
	this.state.information.push(data); // (X)
	this.setState({
    information: this.state.information,
  });	// (X)
  // 리액트에서는 "불변성"을 꼭 유지해야 한다.
  // 값을 수정하게 될 때, 컴포넌트 내장함수인 setState() 를 사용해야 하고
  // 내부에 있는 객체나 배열을 바꿀 때는 "기존의 배열이나 객체를 수정하지 않고" 그것을 기반으로 새로운 객체, 배열을 만들어서 값을 주입해주어야 한다.
  
  // 위와 같은 이유로 배열내장함수 concat 을 사용해줘야 한다.
  // concat: 기존배열을 변경하지 않는다. 추가된 새로운 배열을 반환한다.
  this.setState({
    information: this.state.information.concat(data),
  });
}
```

※ 불변성은 [순환참조](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_Management) 와 연관이 있는 것 같아 보인다. ( 체크[ ] )

※  JSX 에서 Object 값을 확인할 때는 JSON.stringify 를 사용해야 오류가 나지 않는다. (에러 메세지: 오브젝트는 유효하지 않은 react child 블라블라...)

- 그렇게 정리된 Parent.js 의 handleCreate 메소드

```jsx
// Parent.js
id = 0; // 컴포넌트로 만들 때 (!) key 값으로 사용.

state = {
	information: [],
}

handleCreate = (data) => {
	const information = this.state;

  // 방법 1
	this.setState(this.state.information.concat({
		...data,
		id: id++,
	}))
	
  // 또는
  
  // 방법 2
  this.setState(Object.assign({}, data, {
  	id: id++,
  }))
}
```

※ [Spread syntax](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

※ [Object.assign()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)



부모컴포넌트 메소드 → 자식컴포넌트에게 props 로 전달 → 자식컴포넌트에서 전달받은 props 호출 (this.props.전달한props 이름) → 부모컴포넌트의 메소드가 호출되면서 부모컴포넌트의 state 에 담아준다.



불변성 이해하기. 순환참조와 연관성 확인하기.

그 해결을 위한 방법이 Spread syntax, Object.assign() 인게 맞는지 확인하기.

👉🏻 "초심자를 위한 react 핵심 강좌 (8) - shouldComponentUpdate 를 통한 최적화, 불변성을 왜 유지 하는가?" 에 나옴...

