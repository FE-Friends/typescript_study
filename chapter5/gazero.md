# 다섯번째. 함수

## 5.1 함수 매개변수

### 명시적 타입 정보가 선언되지 않는다면?<span style='background-color: #DAB4B8; color:#000'>**any**</span> !

![](https://velog.velcdn.com/images/gazero_/post/c1b9bfcb-a753-41db-8c5a-2db68b31dbb1/image.png)

매개변수(song)에 명시적으로 타입 정보를 입력하지 않으면, 타입스크립트가 이를 <span style='background-color: #DAB4B8; color:#000'>any타입</span>으로 간주

매개변수에 애너테이션<span style='background-color: #DAB4B8; color:#000'>**( : string)**</span>으로 타입을 선언해주면 ?
![](https://velog.velcdn.com/images/gazero_/post/d89c6388-36d1-466f-83dd-a330eaa832d4/image.png)

### 5.1.1 필수 매개변수

#### 타입스크립트에서는 함수에 선언된 모든 매개변수가 모두 **필수**라고 가정

- 그러니깐, 인수는 매개변수의 갯수와 일치해야 함 !
  ![](https://velog.velcdn.com/images/gazero_/post/81c41665-bcbd-42de-aa74-2265e61cd236/image.png)
- 따라서, 예를 들어 2개의 매개변수를 전달하는 경우, 2개의 인수를 받아와야 하며, 더 적거나 더 많이 가져와서는 안 됨 !

### 5.1.2 선택적 매개변수

#### 타입스크립트에서 선택적 객체 타입 속성과 유사<span style='background-color: #DAB4B8; color:#000'> **?**</span>를 추가하면 선택적임을 의미

- 선택적 매개변수에는 항상 |undefined가 유니언 타입으로 추가되어 있음
  ![](https://velog.velcdn.com/images/gazero_/post/60154505-a959-42a3-a4ab-76b570a51852/image.png)
- 즉, 선택적 매개변수로 선언될 경우 필수항목이 아니므로 인수를 비워놔도 되고, 혹은 undefined으로 처리해도 상관없음 !

#### 만약, 선택적 매개변수가 아닌 매개변수 타입에 <span style='background-color: #DAB4B8; color:#000'>undefined</span>를 주는 경우?

- 선택이 아닌 필수 ! 따라서 undefined라도 반드시 써줘야 함

#### <span style='background-color: #DAB4B8; color:#000'>매개변수:string | undefined</span>의 경우에도 마찬가지 !

- string이든, undefined이든 인수는 필수 값임
  ![](https://velog.velcdn.com/images/gazero_/post/9a64ec33-a997-414e-a867-a1075ca5c7ab/image.png)

#### 선택적 매개변수의 위치는? 항상 <span style='background-color: #DAB4B8; color:#000'>마지막</span>에 위치해야 함

![](https://velog.velcdn.com/images/gazero_/post/83fe46ab-0396-4bc3-a7d7-4bdd26493be1/image.png)

### 5.1.3 기본 매개변수

- 자바스크립트에서 선택적 매개변수를 선언할 때, = 와 값이 포함된 기본값을 제공할 수 있음
- 타입스크립트에 함묵적으로 함수 내부에 |undefined 유니언 타입이 추가됨
- 매개변수에 기본값이 있고, 타입 애너테이션이 없는 경우
  ![](https://velog.velcdn.com/images/gazero_/post/cbaa899f-7f41-4c0b-86f0-73f5f2232297/image.png)
- 타입스크립트는 해당 기본값을 기반으로 매개변수 타입을 유추
- 즉, 위 예시 코드에서는 rating은 number타입으로 유추
- 결과적으로 매개변수에 기본 값으로 타입을 "유추"가능한 경우 선택적 매개변수로 취급되어 함수를 호출하는 코드에서 선택적 유추된 타입 | undefined가 됨
  ![](https://velog.velcdn.com/images/gazero_/post/205f5cc3-82e0-465e-aeb5-ba51172ecd82/image.png)

### 5.1.4 나머지 매개변수

#### 스프레드 연산자

- 함수 선언의 마지막 매개변수에 위치
- 해당 매개변수에서 시작해 함수에 전달된 나무저 인수가 모두 단일 배열에 저장되어야 함을 의미
  ![](https://velog.velcdn.com/images/gazero_/post/fb48c025-e770-4a0d-9a0b-687f00b00b37/image.png)

## 5.2 반환 타입

### 함수에 다른 값을 가진 반환문을 포함하고 있다면, 반환 타입을 조합으로 유추

- 반환되는 값의 타입을 유추하는 기능
- 매개변수의 타입과 별개 ! 매개변수의 타입이 변화하는 것이 아님 !!
  ![](https://velog.velcdn.com/images/gazero_/post/f5ad8706-13fa-4e3a-b8bb-a2e536fb08a7/image.png)

### 5.2.1 명시적 반환 타입

> 함수의 반환 타입을 명시적으로 선언하지 않는 것이 좋음! 하지만, 명시적으로 선언하는 방식이 유용한 경우가 있음

- 가능한 반환값이 많은 함수가 항상 동일한 타입의 값을 반환하도록 강제
- 타입스크립트는 재귀 함수의 반환 타입을 통해 타입의 유추하는 것을 거부
- 수백 개 이상의 타입스크립트 파일이 있는 매우 큰 프로젝트에서 타입스크립트 타입 검사 속도를 높일 수 있음

#### 반환 타입을 명시적으로 선언하는 방법 !

- 매개변음 <span style='background-color: #DAB4B8; color:#000'>목록이 끝나는 ) 다음에</span> 배치
- 함수 선언의 경우 <span style='background-color: #DAB4B8; color:#000'> { 앞에 </span> 배치
- 화살표 함수의 경우 <span style='background-color: #DAB4B8; color:#000'> => 앞에 </span> 배치
  ![](https://velog.velcdn.com/images/gazero_/post/8043220b-f151-41b7-a929-a61e978b561d/image.png)

## 5.3 함수 타입

> 함수 타입 구문은 화살표 함수와 유사하지만 함수 본문 대신 타입이 있음

![](https://velog.velcdn.com/images/gazero_/post/3df5c1bf-dafe-4561-af99-d366e26806b4/image.png)

- gazero변수 타입은 매개변수가 없고, string타입을 반환하는 함수이며,

![](https://velog.velcdn.com/images/gazero_/post/74b3ad54-7944-4d30-b89a-1f844ff7c641/image.png)

- gazero변수는 필수인 string[] 매개변수, 선택적인 number타입의 매개변수 및 number값을 반환하는 함수음

### 함수 타입은 콜백 매개변수(=함수로 호출되는 매개변수)를 설명하는 데 자주 사용

![](https://velog.velcdn.com/images/gazero_/post/8c09851d-b756-424b-b3ec-47b9c03d2efb/image.png)

### ❗**참고** 에러메세지

- 첫 번째 들여쓰기: 두함수 타입을 출력함
- 두번째 들여쓰기: 일치하지 않는 부분을 지정
- 세번째 들여쓰기: 일치하지 않는 부분에 대한 정확한 할당 가능성 오류를 출력

### 5.3.1 함수 타입 괄호

- 함수 타입은 다른 타입이 사용되는 모든 곳에 배치할 수 있음(유니언 타입도 포함)
- 유니언 타입의 애너테이션에서 함수 반환 위치를 나타내거나 유니언 타입을 감싸는 부분을 표시할 때 괄호를 사용

```js
let gazero1: () => string | undefined;
```

- 반환되는 타입은 항상 보장됨. string타입이거나, undefined이거나

```js
let gazero2: (() => string) | undefined;
```

- 반환될수도 있고, 아닐수도 있음 하지만 반환값이 존재하는 경우 string타입으로 반환됨

### 5.3.2 매개변수 타입 추론

- 타입스크립트는 선언된 타입의 위치에 제공된 함수의 매개변수 타입을 유추할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/ff74e18a-d959-47a7-8681-9042831a5879/image.png)

- 함수를 매개변수로 갖는 함수에 인수로 전달된 함수는 해당 매개변수 타입도 잘 유추할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/2b676123-71dc-4cd7-af61-c321409368c7/image.png)

### 5.3.3 함수 타입 별칭

![](https://velog.velcdn.com/images/gazero_/post/a62a88d1-7b23-48b3-8db8-5a39616dc4aa/image.png)

## 5.4 그 외 반환 타입

### 5.4.1 void 반환 타입

#### 일부 함수는 어떤 값도 반환하지 않음

- return 문이 없는 함수이거나 값을 반환하지 않는 return문을 가진 함수일 경우
- 타입스크립트는 void 키워드를 사용해 반환 값이 없는 함수의 반환 타입을 확인할 수 있음

#### 반환 타입이 void인 함수는 값을 반환하지 않을 수 있음

![](https://velog.velcdn.com/images/gazero_/post/ce97632a-af3e-4a7f-aecd-74ee8066c1c8/image.png)

- 반환 타입이 void인 함수는 값을 반환하지 않을 수 있음
- gazero함수는 void를 반환하도록 선언되었으므로 값 반환을 허용하지 않음
- 또한, 함수 타입을 선언할 때 void를 사용하면 함수에서 반환되는 모든 값은 무시됨
- 자바스크립트 함수는 실제값이 반환되지 않으면 기본적으로 undefined를 반환하지만 void는 undefined과 동일하지 않음
- void는 반환 타입이 무시된다는 것이며, undefined는 반환되는 리터럴 값임
  ![](https://velog.velcdn.com/images/gazero_/post/1b63cb81-2723-435a-9983-71e4aac4c57f/image.png)
  ![](https://velog.velcdn.com/images/gazero_/post/076df5ca-fb37-4bc8-8d73-2fc5fe264a07/image.png)

- 따라서, undefined를 포함하는 대신 void 타입의 값을 할당하려고 하면 타입 오류가 발생

### 5.4.2 never 반환 타입

- 일부 함수는 값을 반환하지 않으며, 반환할 생각도 전혀 없음
- never 반환 함수는 항상 오류를 발생시키거나 무한 루프를 실행
- 함수가 절대 반환하지 않도록 의도하려면 : never 타입 애너테이션을 추가해 <span style='background-color: #DAB4B8; color:#000'>해당 함수를 호출할 후 모든 코드가 실행되지 않도록</span> 할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/be0243e2-fb57-436b-8398-757e632fbbb3/image.png)

## 5.5 함수 오버로드

#### 오버로드 시그니처(overload signature)

- 선택적 매개변수와 나머지 매개변수만으로 표현할 수 없는 매우 다른 매개변수들로 호출되는 현상
- 오버로드된 함수 호출에 대해 구문 오류를 생성할지 여부를 결정할 때 함수의 오버로드 시그니처만 확인
  ![](https://velog.velcdn.com/images/gazero_/post/227b6e77-fb23-4316-8438-ceeb7005e1b5/image.png)

#### 구현 시그니처(implementation signature)

- 하나의 최종 구현 시그니처와 그 함수의 본문 앞에 서로 다른 버전의 함수 이름, 매개변수, 반환 타입을 여러 번 선언
- 구현 시그니처는 함수의 내부 로직에서만 사용
  ![](https://velog.velcdn.com/images/gazero_/post/8bc21543-30f9-4f40-af5d-3e681297e6b6/image.png)

### 5.5.1 호출 시그니처 호환성

- 함수의 오버로드 시그니처에 있는 반환 타입과 각 매개변수는 구현 시그니처에 있는 동일한 인덱스의 매개변수에 할당할 수 있어야 함
- 구현 시그니처는 모든 오버로드 시그니처와 호환되어야 함
  ![](https://velog.velcdn.com/images/gazero_/post/14773ac2-9f3d-4437-b130-1ce7ad740bed/image.png)
- 따라서, 함수의 오버로드 시그니처에 있는 반환 타입과 매개변수는 구현 시그니처에 있는 동일한 인덱스의 매개변수에 할당할 수 있어야 오버로드 시그니처와 구현 시그니처가 호환이 가능해짐!
