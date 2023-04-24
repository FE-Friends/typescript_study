### 또 까먹은 js파일 console로 찍는법

https://velog.io/@akwnsldj1/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8Javascript-%ED%99%95%EC%9E%A5%EC%9E%90-.js%ED%8C%8C%EC%9D%BC%EC%97%90%EC%84%9C-%EC%BD%98%EC%86%94%EC%B0%BD-%EC%B6%9C%EB%A0%A5%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95

![](https://velog.velcdn.com/images/gyeongmi_lee/post/c4488d22-8d30-4d0c-b8d2-741f8d4ac6f9/image.png)

> 자바스크립트의 힘은 유연함에서 나온다! 유연함 조심!

=> 타입스크립트는

1. 코드가 작동하는 방식을 이해하고
2. 오류가 있는 부분을 알려주는 타입 검사기의 역할을 한다!
   (지난 1장에서 살펴봄 ~)

## 그니까 그거 어케하는건데

## 2.1 타입의 종류

```
let singer = "ME!";
```

- 마우스 오버하면 string타입이라고 알려줌!

- 타입 : 자바스크립트에서 다루는 `값의 형태`에 대한 설명
  (여기서 형태란, 값에 존재하는 속성과 메서드 그리고 내장되어있는 typeof 연산자가 설명하는것을 의~미~)

### 일곱가지의 원시타입

1. null
2. undefined
3. boolean
4. string
5. number
6. bigint
7. symbol

### 2.1.1 타입 시스템

- 타입 시스템 ❓: 프로그래밍 언어가 프로그램에서 가질 수 있는 타입을 이해하는 방법에 대한 규칙 집합

=> 어케 작동하냐면요!

- 코드를 읽고 존재하는 모든 타입과 값을 이해한다
- 각 값이 초기 선언에서 가질 수 있는 타입을 확인
- 각 값이 추후 코드에서 어떻게 사용될 수 있는 지 모든 방법을 확인
- 값의 사용법이 타입과 일치하지 않으면 사용자에게 오류 표시!

### 2.1.2 오류 종류

- 구문 오류 : 타입스크립트 => 자바스크립트로 변환되는 것을 차단한 경우

```
let let wat;
// Error: ',' expected.
```

- 타입 오류 : 타입 검사기에 따라 일치하지 않는것이 감지된 경우

```
console.blub("Notiong");
// Error: Property 'blub' does not exist on type 'Console'.
```

## 2.2 할당 가능성

- 타입스크립트는 변수의 초깃값을 읽고 해당 변수가 허용되는 타입을 결정한다.
  ex. 첨 string => 재할당 string 문제 안되지만,
  string => boolean은 안된단 소리

- 즉, 전달된 값이 예상된 타입으로 할당 가능한지 여부를 `할당 가능성`이라고 함

```
let lastName = "mia";
lastName = true;
// Error : type "boolean" is not assignable to type "string".
```

## 2.3 타입 애너테이션

- 초깃값이 없는 경우라면 타입 애너테이션을 이용해 타입 지정가능.

- 초기값을 유추할 수 없는 변수는 `진화하는 any`라고 부른다

```
let myName: string;
myName = "mia";
myName = 22; // Error : "number"은 "string" 형식에 할당 할 수 없다.
```

- 타입스크립트는 초깃값을 할당하지않고도 변수의 타입을 선언할 수 있는 구문인 `type annotation`을 제공!

- 타입애너테이션은 타입스크립트에만 존재하며, 런타임 코드에도 영향 주지 않고 유효한 자바스크립트 구문도 아님!

- 명시적 타입정의(타입 애너테이션)는 타입스크립트가 자체적으로 수집할 수 없을때만 사용하는것이 좋다.

## 2.4 타입 형태

- 타입스크립트는 해당 변수의 타입에 사용하려는 `속성이 존재하는지`도 확인한다.

```
let rapper = "Queen";
rapper.length; // OK

rapper.push('!');
// Error: Property 'push' does not exist on type 'string'
```

### 2.4.1 모듈

- ECMA 스크립트 2015에서는 import, export 구문을 표준화하기위해 `모듈`이 추가됨!
- `모듈` : export 또는 import가 있는 파일
- `스크립트` : 모듈이 아닌 모든 파일!

=> 모듈은 전역 스코프가 아닌 자체 스코프 내에서 실행됨!
(즉 모듈 내에서 선언된 변수, 함수, 클래스 등은 export 양식중 하나를 사용하여 명시적으로 export하지 않는 한 모듈 외부에서 보이지 앟음)

- 즉 export한 변수, 함수, 클래스, 인터페이스 등을 사용하기 위해서는 import양식중 하나를 사용하여 import 해야함!

![](https://velog.velcdn.com/images/gyeongmi_lee/post/6d311e32-14dd-43c1-a03e-e180694c8f59/image.png)

```
import {value} from "./values";
export const doubled = value * 2;
```

1. 모듈 : 한 모듈에서 다른 파일에 선언된 변수와 동일한 이름으로 선언된 변수는 다른 파일의 변수를 가져오지 않는 한 이름 충돌로 간주하지 않는다!

```
// a.ts
export const myName = "Lee";


// b.ts
expoprt const myName = "Lee";

// c.ts
import { myName } from "./a";
console.log(myName);
```

2. 스크립트 : 파일이 스크립트라면 해당 파일을 전역 스코프로 간주하므로! 모든 스크립트가 파일의 내용에 접근 가능이다. 즉, 스크립트 파일에 선언된 변수는 다른 스크립트 파일에 선언된 동일 이름 가질 수 없다!!

```
// a.ts
const myName = "Lee"
// Error : Cannot redeclare blok-scoped varible "myName".

// b.ts
const myName = "Lee";
// Error : Cannot redeclare block-scoped varible "myName".

// a.ts && b.ts
const myName = "Lee";
export {};
```
