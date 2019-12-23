[인프런] 누구든지 하는 리액트: 초심자를 위한 react 핵심 강좌 (3)

김민준

2019.12.23



**[ 필요한 도구 설치하기 ]**

**node.js LTS**

- webpack, babel 사용을 위해 필요하다.
- **nvm** 사용 권장 !
- npm 대신 **yarn**
  - yarn ? 조금 개선된 버전의 npm. 더 나은 속도. 더 나은 캐싱 시스템.
  - 인터넷이 빠른 우리나라에서는 크게 체감하기 힘듬... 해외, 느린 인터넷, 낮은 사양의 컴퓨터에서는 체감됨... 

**VSCode**

**git**



**[ Create react app ]**

리액트 프로젝트 생성을 쉽게 해주는 Command. [Link](https://github.com/facebook/create-react-app)

※ boilerplate 👀 (설명 중 나온 용어)

```
$ npx react-create-app project-name
```

`react-create-app` 로 만든 리액트 프로젝트는 `node_modules/react-script` 에 webpack, babel 설정이 담겨있다.

설정파일을 꺼내 보기 위해서는...?

```
$ yarn eject
```

- 한번 하고나면 되돌릴 수 없음...

