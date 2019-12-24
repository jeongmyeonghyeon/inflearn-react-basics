[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (6)

김민준

2019.12.24



**[ 배열 렌더링 하기 ]**

[map](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - JavaScript 배열 내장함수

```javascript
const numbers = [1,2,3,4,5];
// arrow func, 인자 1개 일때 () 생략. 
// 함수가 한줄 일 때 return 및 {} (scope) 생략.
const squared = numbers.map( n => n * n );
// const squared = numbers.map( (n) => { return n * n } );

console.log(squared); // [1, 4, 9, 16, 25]
```



**[ 배열 렌더링, key ]**

[key.](https://reactjs.org/docs/lists-and-keys.html#keys) 배열의 CRUD 를 효율적으로 하기위해 사용되는 값.

키가 없는 경우 (인덱스가 키로 사용되고 있음)

- a,b,c,d → a,b,z,c,d
  - a,b,c→z,d→c,+d (아 몰라 그림 안그려 ㅠㅠ 나만 이해하면 되 !!!)
- a,b,z,c,d → b,z,c,d
  - a→b, b→z, z→c, c→d

하지만, id 가 있으면 해당 아이디의 고유성을 바탕으로 수정, 삭제 만 하면 된다.