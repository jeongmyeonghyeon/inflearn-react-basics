[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (8)

김민준

2019.12.24



**[shouldComponentUpdate 를 통한 최적화. 불변성을 왜 유지하는가?]**

**component update 하게 될 때 성능최적화는 어떻게 하게 되는지**

```jsx
// Child.js
shouldComponentUpdate(nextProps, nextState) {
    if ( this.state !== nextState ) {	// 현재 컴포넌트의 state 가 변경될 state 와 다른지.
        return true; // true - 다르면 render
    }
    return this.props.info !== nextProps.info; // 현재 컴포넌트의 props 와 넘겨받은 props 가 다른지. true - 다르면 render
}
```



**state 값을 변경할 때 불변성을 왜 유지해야 하는지**

리액트에서는 setState() 를 하고 re-render 되도록 설정이 되어있어 다음의 코드는 안됨...

```jsx
this.state.information.push({ ...data, id: this.id++ });
```

다음과 같이 강제로 실행시킬 수는 있으나,

```jsx
this.state.information.push({ ...data, id: this.id++ });
this.setState({
	information: this.state.information,
})
```

다음과 같은 문제가 생김.

```jsx
const array = [1,2,3];
const anotherArray = array;

array === anotherArray;	// true. 두 변수 모두 같은 배열을 가리키고 있다.
```

```jsx
const object = { a: 1, b: 2 };
const anotherObject = object;

object.c = 3;
console.log(anotherObject) // { a: 1, b: 2, c: 3 }

object === anotherObject // true.
```

이와 같은 상황이 발생하면 shouldComponentUpdate 에서 로직을 구현할 때 굉장히 어려워짐...



하지만, 불변성을 유지할 경우

Array

```jsx
const array = [0,1,2];
const anotherArray = [...array, 3];
const anotherArray2 = array.concat(4);

array	// [0,1,2]
anotherArray // [0,1,2,3]
anotherArray2 // [0,1,2,4]

array !== anotherArray // true.
array === anotherArray2 // false.
```

Object

```jsx
const object = { a: 1, b: 2 };
const anotherObject = { ...object, c:3 };

object !== anotherObject	// true.

anotherObject // { a: 1, b: 2, c: 3 }
object // { a: 1, b: 2 }
```



깊은 복사에 유용한 라이브러리들... (nestedObject...)

- [Immutable.js](https://immutable-js.github.io/immutable-js/)

- [immer](https://github.com/immerjs/immer)

