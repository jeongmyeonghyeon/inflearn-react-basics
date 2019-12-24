[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (4)

김민준

2019.12.23



**[ Input 상태 관리하기]**

VSCode Extends

- reactjs code snippet
- [e.target.name] [계산된 속성명(computed property name) 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Object_initializer)

```javascript
handleChange = (e) => {
  this.setState({
    [e.target.name]: e.target.value,
  });
}
```

```javascript
// 계산된 속성명 (ES6)
var i = 0;
var a = {
  ["foo" + ++i]: i,
  ["foo" + ++i]: i,
  ["foo" + ++i]: i
};

console.log(a.foo1); // 1
console.log(a.foo2); // 2
console.log(a.foo3); // 3

var param = 'size';
var config = {
  [param]: 12,
  ["mobile" + param.charAt(0).toUpperCase() + param.slice(1)]: 4
};

console.log(config); // { size: 12, mobileSize: 4 }
```

