[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (7)

김민준

2019.12.24



**[ 데이터 제거 ]**

어렵진 않지만, 불변성을 유지하면서 작업을 해줘야 하기 때문에 기존과 다르다.

데이터 제거

- [.slice](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

```javascript
const numbers = [1,2,3,4,5];
numbers.slice(0, 3);	// [1,2,3]
numbers.slice(1, 4);	// [2,3,4]

// 잘라 붙여서 [1,2,4,5] 만들고 싶을 때
numbers.slice(0,2).concat(numbers.slice(3,5));	// [1,2,4,5]

// 3 자리에 10을 넣어 [1,2,10,4,5] 를 만들고 싶을 때, Spread syntax 를 함께 사용하면, 
[
	...numbers.slice(0,2),
	10,
	...numbers.slice(3,5)
]
// [1,2,10,4,5]
```

- [.filter](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

```javascript
const numbers = [1,2,3,4,5];

numbers.filter(n => n > 3); // [4,5]

numbers.filter(n => n !== 3); // [1,2,4,5]

numbers	// [1,2,3,4,5] 그대로 유지.. 불변성 유지...
```



리액트에서의 사용은 

부모에게 데이터 전달과 비슷...

- 부모컴포넌트에 삭제메소드 만들고

- 자식컴포넌트에 props 로 전달하고 (만약 자손컴포넌트 까지 있으면 거기까지 전달해서) 거기에서 부모컴포넌트 삭제메소드를 호출...

- 부모컴포넌트의 삭제메소드는 자신의 state 를 바꿈.



**[ 데이터 수정 ]**

- .slice

- .map

```jsx
// Parent.js
handleUpdate = (id, data) => {
  const { information } = this.state; // 결국 부모컴포넌트의 데이터를 수정하기 위한 과정.. 수정할 state 를 가져오고...
  this.setState({
    information: information.map(
    	info => {
        if (info.id === id) {
          return {
            id,
            ...data,
          }
        }
        return info; // 이렇게 짜면, 자식컴포넌트에서 넘겨받은 id 에 해당하는 배열의 오브젝트만 변경하여 반환. 그 값이 setState 를 통해 변한다.
      }
    )
  })
}

...

<Child 
  ... 
  onUpdate={this.handleUpdate} 
  ...
/>
```

```jsx
// Child.js
state = {
  editing: false,	// 1. false 면 수정정보 입력란이 화면에 표시, true 로 toggle 됨. 2. 로직중에 props 로 받은 부모컴포넌트의 onUpdate 호출. false 로 toggle.
  name: '',
  phone: '',
}

handleChange = (e) => {	// input 입력시 각각의 값이 현재컴포넌트 state 에 update 될 수 있도록...
  this.setState({
    [e.target.name]: e.target.value,
  })
}

handleToggleEdit = () => {
  const { info, onUpdate } = this.props;
  
  if (this.state.editing) {
    onUpdate(info.id, {
      name: this.state.name,
      phone: this.state.phone,
    })
  } else {
    // 첫 실행시 editing: false 기본값으로 기존 값(props 로 받음)을 input value 에 사용할 수 있도록 setState.
    this.setState({
      name: info.name,
      phone: info.phone,
    })
  }
  
  this.setState({
    editing: !this.state.editing,
  })
}
```

