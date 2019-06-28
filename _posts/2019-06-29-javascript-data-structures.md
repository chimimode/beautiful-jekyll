---
layout: post
title: "원시타입(primitive), 참조타입(reference)"
subtitle: "javascript의 자료형"
date:   2019-06-29 09:01:00 +0900
categories: javascript
tags: [javascript, data structure]
comments: true
---

javascript가 가지고있는 내장 자료형(타입)은 두 가지로 나뉩니다.  
타입은 원시타입과 참조타입의 두 가지가 있습니다.  

🔹원시타입
- Boolean
- Null
- Undefiend
- Number
- String
- Symbol(ECMAScript 6)

🔹참조타입
- Object
- Array
- Date
- Function
- (표준이 될..수도?)Map, Set, TypedArrays

**원시타입**은 변경이 불가능한 값 입니다. 이 뜻은 변수에 값을 할당하면 그 값이 메모리에 고정된다는 것을 의미합니다.  
아래의 코드를 보면 어떤 내용인지 확인이 가능합니다.
```
    let a = 1;
    let b = a; // a값을 b에 대입하면 a의 값인 1 이 b에 복사됩니다.
    
    console.log(a); // 1
    console.log(b); // 1
    
    b = 2;
    
    console.log(a); //1
    console.log(b); //2
    
    // b에 새로운 값을 할당하면 b의 데이터는 즉시 바뀌고 a와는 관련없이 2로 변경됩니다.
```

**참조타입**은 원시타입과는 다르게 고정된 값이 아닌 참조를 가지고 있으며 몇가지 속성은 제거, 추가, 초기화가 가능합니다. 이는 사용자가 원하는 형태의 데이터구조를 만들 수 있다는것을 의미합니다.  
아래의 코드를 보면 어떤 내용인지 확인이 가능합니다.
```
    let obj = {name: 'lee'};
    let obj2 = obj; // obj2에 먼저 선언한 obj를 할당합니다.
    
    console.log(obj); // {name: 'lee'}
    console.log(obj2); // {name: 'lee'}
    
    obj2.name = 'kim';
    
    console.log(obj); // {name: 'kim'}
    console.log(obj2); // {name: 'kim'}
    
    // obj2의 name에 접근하여 값을바꾸면 원시타입과는 다르게 obj의 값도 함께 변합니다.
    // 이는 obj2에 할당한 obj가 참조를 가진 Object이기 때문입니다.
    
    obj.drink = 'water'; // obj를 선언할 당히 없던 drink를 추가합니다.
    
    console.log(obj2.drink); // 'water'
    
    // obj에 drink를 추가했지만 obj2도 obj를 참조하고 있으므로 drink를 공유합니다.
```