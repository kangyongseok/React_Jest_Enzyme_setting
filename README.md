# React_Jest_Enzyme_setting
Existing React projects setting for Front Test-code

### **npm install**
```
npm i --save-dev jest jest-css-modules enzyme enzyme-adapter-react-16 babel-jest enzyme-to-json
```

 ```
 jest-css-modules: style.css_name 형태의 css 모듈을 사용하기위해 필요합니다.
 enzyme-adapter-react-16: 뒤에 숫자는 React의 버전숫자와 맞춰야합니다.
 enzyme-to-json: snapshot 을 보여줄때 깔끔하게 정리되어져서 보여지게 해줍니다.
 ```
 

### JEST
[Jest](https://jestjs.io) 는 facebook 에서 만든 javascript 테스트 도구 입니다. 설정없는 테스트환경을 제공하는것이 철학이라 `jest` 만 설치해서 바로 테스트 도구 사용이 가능합니다.  
`CRA` 를 사용했을때에는 자동으로 테스트도구인 jest가 기본내장되어있지만 기존의 프로젝트라면 신규 설치가 필요합니다.

### Enzyme
[Enzyme](https://airbnb.io/enzyme/) 은 React를 위한 테스트 유틸리티로 React 의 Component를 쉽게 출력할 수 있습니다.  
Enzyme 의 API 는 jQuery API 와 유사합니다.


### Setting
```
// package.json
"script": {
....
"test": "NODE_ENV=test jest --watch --verbose", // 변경사항만 감지
"test:all": "NODE_ENV=test jest --watchAll --verbose" // 변경이있을때 항상 전체 실행
}
```
[추가옵션](https://jestjs.io/docs/en/cli.html#coverage)

```
// package.json
"jest": {
  "testEnvironment": "jsdom", // 테스트에 사용될 테스트 환경. Jest의 기본 환경은 jsdom을 통한 브라우저와 유사한 환경 입니다. 
  "snapshotSerializers": [
    "enzyme-to-json/serializer"
  ],
  "setupFilesAfterEnv": [
    // 각 테스트 전에 테스트 프레임 워크를 구성하거나 설정하기 위해 일부 코드를 실행하는 모듈에 대한 경로 목록입니다.
    "<rootDir>/test/setupTests.js"
  ],
  "testPathIgnorePatterns": [
    // 테스트 경로가 패턴 중 하나와 일치하면 건너 뜁니다.
    "<rootDir>/.next/",
    "<rootDir>/node_modules/"
  ],
  "transform": {
    // JavaScript 코드를 컴파일하는데 사용하기위해 명시적으로 정의
    ".*": "babel-jest",
    "^.+\\.js?$": "babel-jest"
  },
  "moduleFileExtensions": [
    // jest 가 왼쪽에서 오른쪽으로 찾는 확장자명
    "js",
    "json"
  ],
  "moduleNameMapper": {
    "\\.(css|less|scss|sss|styl)$": "<rootDir>/node_modules/jest-css-modules",
    "\\.(jpg|ico|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "<rootDir>/test/fileMock.js"
  }
  
}
```

```
// test/fileMock.js
module.exports = 'test-file-stub';
```

```
// test/setupTests.js
import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';
import 'jest-enzyme';

configure({ adapter: new Adapter() });
```


### Jest Test code Func
[자주쓰이는 함수 정리](https://www.daleseo.com/jest-basic/)  
[비동기테스트](https://www.daleseo.com/jest-async/)  
[mocking기법](https://www.daleseo.com/jest-fn-spy-on/)  
[jest cheatsheet](https://devhints.io/jest)  
