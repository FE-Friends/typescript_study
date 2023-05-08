# 여섯번째. 배열

> 자바스크립트에서 배열은 <span style='background-color: #DAB4B8; color:#000'>**내부에 모든 타입의 값을 혼합해서 저장**</span>할 수 있음

- 매우 유연함
- 배열을 읽을 때 혼란을 줄 수 있음
- 프로그램에 문제가 될 만한 오류가 발생할 수 있음

> 타입스크립트는 초기 <span style='background-color: #DAB4B8; color:#000'>**데이터 타입을 기억하고, 해당 데이터 타입에서만 작동하도록 제한**</span>

![](https://velog.velcdn.com/images/gazero_/post/d1400245-41a2-4b23-b8bf-77c5e96f8ee7/image.png)

## 6.1 배열 타입

- 베열을 저장하기 위한 변수는 초깃값이 필요하지 않음
- undefined로 시작해서 나중에 배열 값을 받을 수 있음
- 배열에 대한 타입 애너테이션 <span style='background-color: #8c0303; color:#fff'>**배열의 요소 타입**</span> 다음에 [] 가 와야함

```js
let array: number[];
```

### 6.1.1 배열과 함수 타입

```js
let oneString: () => string[];
```

타입은 string 배열을 반환하는 <span style='background-color: #7fbcff; color:#000'>**함수**</span>

```js
let twoString: (() => string)[];
```

타입은 string 타입을 반환하는 함수 <span style='background-color: #7fbcff; color:#000'>**배열**</span>

### 6.1.2 유니언 타입 배열

- 배열의 각 요소가 여러 선택 타입 중 하나일 수 있음을 나타낼 때 사용
- 유니언 배열 타입에서 소괄호의 위치

**string 또는 number 타입의 배열**

```js
let gazero1: string | number[];
```

= 그러니깐, 변수 gazero1은 string타입 이거나, number타입의 배열임
그렇기 때문에 gazero1에 배열형태가 오는 경우에는 number값만 배열 안에 들어갈 수 있음 !

**각각 number배열 그리고 string배열**

```js
let gazero2: (string | number)[];
```

= 따라서, gazero2가 배열로 쓰일 경우 배열 안의 값은 string타입 이거나 number타입임

![](https://velog.velcdn.com/images/gazero_/post/35697c0a-9a5b-4dbb-bad7-35f77809a7a6/image.png)

- gazero 배열 안에는 string 타입과 undefined 타입임을 유추할 수 있음

### 6.1.3 any 배열의 진화

- 초기 빈배열로 설정된 변수에서 타입 애너테이션을 포함하지 않으면, any[]로 취급
- 이 경우 잠재적으로 잘못된 값 추가를 허용해 타입스크립트의 타입 검사기가 갖는 이점을 부분적으로 무력화할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/fbe69e9b-64eb-4eeb-b783-351b1e35eb72/image.png)
- 주의할 점 : 초기 any[] 타입이 string[], (number|string)[] 타입으로 변화하는 것이 아니라 ! 해당 타입 요소가 포함되는 것을 허용하는 것임

### 6.1.4 다차원 배열

```js
let gazero: number[][];

gazero = [
  [1, 2, 3],
  [2, 3, 4],
  [3, 4, 5],
];
```

- 이는 gazero는 number타입 배열을 배열형태로 가진다
- 즉, 배열 내에 value값이 number타입 배열을 갖는 배열

## 6.2 배열 멤버

> 타입스크립트는 해당 배열의 타입 요소를 되돌려주는 전형적인 인덱스 기반 접근 방식을 이해

![](https://velog.velcdn.com/images/gazero_/post/4fd96a59-4e76-429b-a41b-350210351e35/image.png)

- gazero의 타입이 정해지는 방법? gazeros 타입에 기반하여 정해짐
  ![](https://velog.velcdn.com/images/gazero_/post/b9159ffc-0519-455a-8ef8-c14a973b84ee/image.png)
- gazeros의 배열 값의 타입을 (number|string)[]로 했을때, gazero의 값은 number이거나, string으로 추론할 수 있음
- 그렇다면, 애너테이션 괄호를 무시하는 것인가? 아님. 왜냐하면 gazero는 gazeros의 배열 **속성 값**에 접근하고 있기 때문임

### 6.2.1 주의 사항: 불안정한 멤버

- 타입스크립트에서 배열은 타입 시스템에서 불안정한 소스
- 기본적으로 타입스크립트는 모든 배열의 멤버에 대한 접근이 해당 배열의 멤버를 반환하지만, 자바스크립트에서는 배열의 길이보다 큰 인덱스로 배열 요소에 접근하면 undefined를 제공
- 하지만, 타입스크립트에서는 undefined로 취급되지 않음
  ![](https://velog.velcdn.com/images/gazero_/post/17c1b8fd-f9f3-4858-a1f9-fbee80b33d8b/image.png)
- elements[9999]를 undefined가 아닌, string 타입으로 간주함

## 6.3 스프레드와 나머지 매개변수

### 6.3.1 스프레드

- 스프레드 연산자를 사용해 배열을 결합
- 입력된 배열 중 하나의 값이 결과 배열에 포함
  ![](https://velog.velcdn.com/images/gazero_/post/48d29c50-178f-494a-ae3c-71e7fd23bada/image.png)
- gazeroJoin 배열에는 gazero의 string타입과 gazeros의 number타입 값을 모두 포함

### 6.3.2 나머지 매개변수 스프레드

![](https://velog.velcdn.com/images/gazero_/post/8188f444-00d0-4001-b02d-c0b759caeebe/image.png)

- gazero함수는 첫번째 인자로 string타입의 greeting 매개변수와, 두번째 인자로 스프레드 string타입의 배열인 names 매개변수를 가진다
- 따라서 첫번째 인자에는 string타입, 두번째 인자에도 string타입 값만 받음

## 6.4 튜플

> 튜플(tuple)이란? 고정된 크기의 배열

![](https://velog.velcdn.com/images/gazero_/post/89a2f4af-2370-4c59-b1bb-e6a827d4c65b/image.png)

- 고정적으로 배열 인덱스 값에 타입을 고정할 수 있음
- [0]번째 값은 number 타입
- [1]번째 값을 string 타입 값을 고정
- 따라서 해당 자리에 고정된 타입 값이 할당되지 않을 경우 오류

#### 구조분해할당도 가능

![](https://velog.velcdn.com/images/gazero_/post/7b6e1a51-a313-4dec-88c6-ba5da39f61bc/image.png)
![](https://velog.velcdn.com/images/gazero_/post/9cfcf40c-f6ef-4e76-8617-306b89c133c6/image.png)

- 할당된 타입에 따라 타입을 할당할 수 있음

### 6.4.1 튜플 할당 가능성

- 튜플 타입은 가변 길이의 배열 타입보다 더 구체적으로 처리
- 가변 길이의 배열 타입은 튜플 타입에 할당할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/4f2f6c4b-ad70-4fe7-b67c-f8d30866b2e9/image.png)
- 즉, 튜플 타입(고정된 크기의 배열)에 가변 길이 배열 타입은 할당할 수 없음

```js
const gazeroLoose = [false, 123];
```

- 튜플도 아님
- 구조분해 할당도 아님
- 그저 gazeroLoose는 boolean 혹은 number 타입을 할당하는 배열일 뿐
- const gazeroLoose: (boolean | number)[] 임

```js
const gazeroTupleLoose: [boolean, number] = gazeroLoose;
//오류
```

- 그렇기 때문에 (boolean | number)[]는 [boolean, number] 타입에 할당될 수 없음
- (boolean | number)[]는 boolean이거나 number이지만 [boolean,number]는 고정된 튜플된 값임

![](https://velog.velcdn.com/images/gazero_/post/1be5f6c9-ce1f-4bcf-9494-bd0ee2cf7085/image.png)

- 또한, 튜플로 할당된 배열의 갯수에 따라 타입 할당이 가능함
- 즉, tupleThree의 배열 값 갯수는 3개 이므로, 오로지 2개의 배열 값이 필요한 tupleTwoExtra에 할당할 수 없음

#### 나머지 매개변수로서의 튜플

- 튜플은 구체적인 길이와 요소 타입 정보를 가지는 배열로 간주됨
- 따라서 함수에 전달할 인수를 저장하는 데 특히 유용
- 타입스크립트는 ...나머지 매개변수로 전달된 튜플에 정확한 타입 검사를 제공
  ![](https://velog.velcdn.com/images/gazero_/post/e6181579-d8e8-4ae3-b7ea-71cbfc482023/image.png)

### 6.4.2 튜플추론

- 배열이 변수의 초깃값 또는 **함수에 대한 반환값**으로 사용되는 경우, 고정된 크기의 튜플이 아니라 유연한 크기의 배열로 가정함
  ![](https://velog.velcdn.com/images/gazero_/post/f07b040b-e8cf-4632-8800-d2bea506bb14/image.png)

#### 명시적 튜플 타입

- 튜플 타입도 타입 애너테이션에 사용할 수 있음
- 함수가 튜플 타입을 반환한다고 선언되고, 배열 리터럴을 반환한다면 해당 배열 리터럴은
- 일반적인 가변 길이의 배열 대신 튜플로 간주

**반환타입이 명백하게 명시**

```js
function first(input: string): [string, number] {
  return [input[0], input.length]
}

일때,

const [firstChar, size] = first("gazero");

에서 firstChar 타입은 string이고, size는 number타입
```

#### const 어서션

- 타입스크립트 값 뒤에 넣을 수 있는 const 어서션인 as const연산자를 제공
- const 어서션은 타입스크립트에 타입을 유추할 때 읽기 전용이 가능한 값 형식을 사용하도록 지시
- as const는 값이 변경될 수 있는 변수에 할당할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/06e32a1b-15a1-40ae-8086-352ddf05929b/image.png)
- 즉, 변경가능한 pairAlsoGazeo: [number, string]에 [1157, "To"] as const는 할당할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/55efa5c4-1bda-482a-b01e-1278d7c460c0/image.png)
- 이것은 배열안에 값을 할당하는 경우에도 마찬가지임
- 읽기 전용 배열 값을 반환하는 경우, 이는 사용하는 코드에 해당 큐플에서 값을 찾는 것에만 관심을 둠
