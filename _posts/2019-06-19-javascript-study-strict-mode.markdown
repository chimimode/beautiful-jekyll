---
layout: post
title:  "[study] javascript의 strict mode란"
date:   2019-06-19 10:01:00 +0900
categories: javascript
tags: [javascript, strict, 자바스크립트, 엄격모드]
comments: true
---
# :: strict mode ::

### ◾️**보통의 javascript코드에 아래와 같은 몇가지 변경을 적용함**

1. javascript의 문법적 허용을 에러로 throwing함
2. 일부 소스코드의 경우 strict mode가 더 빠르게 동작됨
    - javascript엔진의 최적화 작업을 어렵게하는 실수들을 바로잡음으로써 더 빠른 동작
3. ECMAScript 차기버전에 정의될 문법은 금지

### ◾️**strict mode 적용방법**

- 전체 스크립트에 적용
```javascript
    'use strict';
    
    let mode = 'strict mode';
    ..
```
- 함수에 적용
```javascript
    function strict() {
    	'use strict';
    
    	mode = 'strict mode';
    }
    
    strict();
    
    // Uncaught ReferenceError: mode is not defined
    // strict선언의 위치에 따라 함수안에서도 에러발생 여부가 달라질수 있음 (let 선언자 등)
```
- 모듈에 적용
```javascript
    function strict() {
        // 모듈이기때문에 기본적으로 엄격합니다
    }
    export default strict;
    
    // ES6의 모듈은 'use strict'를 선언하지않아도 자동으로 strict mode
```
strict mode와 non-strice mode를 혼용하면 오류가 발생할 수 있음

⚠️<script> 단위로 적용된 strict mode는 다른 소스에(예: 서드파티 라이브러리 등) 영향을 줄 수 있으므로 바람직 하지 않음 

⚠️함수단위의 strict mode는 함수 참조의 경우 오류가 발생할 수 있음

이를 피하기 위해 즉시실행 함수로 감싸서 적용하는 방법이 있음

### ◾️strict mode가 발생시키는 에러

1. var, let, const로 할당하지않은 전역변수
```javascript
    'use strict';
    
    test = 10;
    
    //ReferenceError: x is not defined
```
2. 예약어 변수할당
```javascript
    let undefined = 0;
    let Infinity = 0;
    
    //Uncaught SyntaxError: Identifier 'Infinity' has already been declared
```
3. 쓸 수 없는 프로퍼티에 할당
```javascript
    var obj1 = {};
    Object.defineProperty(obj1, "x", { value: 42, writable: false });
    obj1.x = 9; // TypeError 발생

    var obj2 = { get x() { return 17; } };
    obj2.x = 5; // TypeError 발생
    
    // getter-only 프로퍼티에 할당

    var fixed = {};
    Object.preventExtensions(fixed);
    fixed.newProp = "ohai"; // TypeError 발생
    
    // preventExtensions(새로운 속성추가를 막는 메소드)
```
4. delete 명령어
```javascript
    'use strict';
    
    let test = 1;
    delete test;
    
    // Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
```
5. 함수의 매개변수명이 중복됨
```javascript
    'use strict';
    
    function sum(a, a, b) {
    	return a + b + c;
    }
    
    sum(1, 2, 3);
    
    //Uncaught SyntaxError: Duplicate parameter name not allowed in this context
```
6. with문 사용
```javascript
    'use strict';
    
    let test = 10;
    
    with(obj) {
    	test;
    }
```
7. 일반함수의 this사용
```javascript
    (function () {
      'use strict';
    
      function foo() {
        console.log(this); // undefined
      }
      foo();
    
      function Foo() {
        console.log(this); // Foo
      }
      new Foo();
    }());
    ```
