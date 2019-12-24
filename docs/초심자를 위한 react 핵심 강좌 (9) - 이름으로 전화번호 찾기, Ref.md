[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (8)

김민준

2019.12.24



**[이름으로 전화번호 찾기]**

```jsx
state = {
	[
		...
	],
	keyword: '',
}

(...)

handleChange = (e) => {
  this.setState({
    keyword: e.target.value,
  })
}

(...)

<PhoneInfoList 
    data={this.state.information.filter(
    				info => info.name.indexOf(this.state.keyword) > -1
    )} // =ㅁ=)...
    onRemove={this.handleRemove}
    onUpdate={this.handleUpdate}
/>
```



**[ DOM 에 접근 Ref ]**

방법은 두 가지...

```jsx
input = null;

(...)
 
<Child
	ref={ref => this.input = ref }
/>

(...)

this.input.focus();
```

```jsx
input = React.createRef();

(...)

<Child
	ref={this.ref}
/>

(...)

this.input.current.focus();
```

Ref 는...

focus 를 준다던지

특정 DOM 의 크기를 가져와야 한다던지

scroll 의 위치를 가져와야 한다던지...

**DOM에 직접적으로 접근이 꼭 필요할 때**



추가적으로 외부라이브러리와 연동할 때...

d3.js, Chartist.js, ... 특정 DOM 에 그리도록 설정... canvas, video 관련 라이브러.... 등