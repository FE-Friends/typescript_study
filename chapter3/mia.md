![](https://velog.velcdn.com/images/gyeongmi_lee/post/72982431-64f7-4546-8932-13ca170fca53/image.png)

#### 사전에 알아두면 좋을 기본 타입

```
/* ts의 문자열, 숫자, 배열 기본타입*/
// js 문자열 선언
var str = 'hello';
// ts 문자열 선언
let str2: string = 'hello';
const num: number = 2;
// ts 배열 선언
let arr: Array<number> = [1,2,3]; // arr에는 배열(A는 대문자여야함), 그 안에는 숫자만 들어갈 수 있다.
let arr2:Array<string> = ["a",2]; // 이러면 에러다
// 배열 리터럴 사용해서 선언
let items: number[] = [1,2,3];

// ts 튜플(tuple)
let address: [string,number] = ['gangnam', 12] // 요런식으로 배열의 규칙까지 정해주는것, 요소의 타입과 개수가 고정된 배열을 표현할 수 있음

// ts 객체
let obj: object = {};
let person:object = {
    name: 'gyoengmi',
    age:100
} // 위에서 지정한대로만하면 어떤 속성이든지 상관 x , 객체이기만 하면된다

// 하지만
let person2:{name: string, age: number} = {
    name:"gyoengmi",
    age:100
} // 이런식으로 타입을 지정해두면 무조건 속성이 있어야만 오류를 안낸다!

// 진위값
let show:boolean = true;
```

# 3. 유니언과 리터럴

- 유니언 : 값에 허용된 타입을 두개 이상의 가능한 타입으로 확장하는 것
- 내로잉 : 값에 허용된 타입이 하나 이상의 가능한 타입이 되지 않도록 좁히는 것

## 3.1 유니언 타입

```
let mathmatician = Math.random() > 0.5 ? undefined : "a";
// 값이 어떤것이냐에 따라 달라질수 있다
```

![](https://velog.velcdn.com/images/gyeongmi_lee/post/7fc95062-d4c2-4666-a446-593b0301dad9/image.png)
'이거 혹은 저거' 같은 타입 => `유니언` 이라고 한다.

- 타입스크립트는 `|` 를 사용해 유니언 타입을 나타낸다.

### 3.1.1 유니언 타입 선언이 언제 필요해!

=> 변수 초깃값이 존재하더라도 `명시적(분명한) 타입 애너테이션` 제공하는것이 필요할때!

> 유니언 타입의 순서는 중요하지 않다.

### 3.1.2 유니언 속성

- ✔ 값이 유니언 타입일때 타입스크립트는 `모든 타입에 존재하는 속성`에만 접근가능.

```
let physicist = Math.random() > 0.5 ? "Marie Curie" : 84;
physicist.toString(); // OK, number와 string 모두 사용가능
physicist.toUpperCase();
// Error: Property 'toUpperCase' does not exist on type 'string | number'
```

=> 근데 만약 내가 유니언 타입으로 정의된 타입들 중 하나의 속성만 사용하고 싶다면! => `내로잉` 과정을 사용해야함

## 3.2 내로잉

#### 내로잉

- 타입의 범위를 좁히는 과정
- 값이 이전에 유추된 것보다 더 구체적 타입임을 유추하는것

#### 타입검사

- 이때 타입을 좁히는 데 사용할 수 있는 논리적 검사

## 내로잉을 하는 방법들💨

### 3.2.1 값 할당을 통한 내로잉

```
let admiral: number | string = "grace";
// 📌admiral이 string이므로 narrowing 한것
admiral.toUpperCase(); // OK: String

admiral = 23;
// 📌admiral이 number이므로 narrowing 한것
admiral.toFixed(); // OK
```

### 3.2.2 조건 검사를 통한 내로잉

- if문으로 변수값 좁히는 방법

```
let scientist = Math.random() > 0.5
	? "Frank"
	: 51;

if(scientist === "Frank") {
	scientist.toupperCase(); // OK
}

scientist.toupperCase(); // 📌Error 유니언타입 두가지 다 만족해야함
```

### 3.2.3 typeof 검사를 통한 내로잉

- `typeof`연산자 사용하여 타입 좁히기 = 실용적 방법!

```
let something = Math.random() > 0.5 ? "leekoby" : 1;

// type이 number 일 때로 타입 좁히기
if (typeof something === 'number') {
    something.toFixed();
}
// type이 string 일 때로 타입 좁히기
if (typeof something === 'string') {
    something.toUpperCase();
}


// ! 를 사용한 논리 부정과 else 문도 가능
// type이 number 일 때로 타입 좁히기
if (!(typeof something === 'number')) {
    something.toUpperCase();
} else something.toFixed();
// type이 string 일 때로 타입 좁히기

// 삼항연산자도 사용가능
typeof something === "string" ? something.toUpperCase():something.toFixed()

// ❌ Error : Property 'toUpperCase' does not exist on type 'number'.
something.toUpperCase();
```

## 3.3 리터럴 타입

- 리터럴타입: 좀 더 구체적인 버전의 원시타입(원시타입 값 중 어떤것이 아닌 `특정 원싯값`으로 알려진 타입!)

```
let name = "mia"; // 📌이 변수의 타입은 string이 아닌 "mia" 다
```

- 원시 타입에는 무한한 수의 리터럴 타입이 있다.
  > boolean: true | false
  > number: 0 | 1 | 2 | 3 | 0.1 | 0.2 | …
  > string : “” | “a” | “b” | “ab” | “adkdfo” | …

### 3.3.1 리터럴 할당 가능성

- 동일한 원시타입이어도, 서로 다른 리터럴 타입은 할당할 수 없다

```
let name: "mia" = "mia"; // type이 "mia", 할당한값도 "mia"
something = "you"; // 📌 Error: Type '"you"' is not assignable to type '"mia"'.
```

- 리터럴 타입은 원시값에 할당 가능 ⭕
- 원시값은 리터럴 타입에 할당 불가 ❌

## 3.4 엄격한 null 검사

- 자바스크립트는 타입이 필요한 위치에 `null값`을 허용한다!
  (= 이를 십억달러의 실수라고 부르기도 한다, 이때문에 수많은 오류, 취약성 및 시스템 충돌이 발생했기 때문)

#### strictNullChecks 활성화하는 방법

![](https://velog.velcdn.com/images/gyeongmi_lee/post/336aeb84-7ccd-4318-b6f5-3e2af69b3333/image.png)

```
// ❌ strictNullChecks
let name: string;
console.log(name.length); // No error, but runtime error

// ⭕ With strictNullChecks
let name: string | null;
console.log(name.length); // Error: Object is possibly 'null'.

```

### 3.4.2 참 검사를 통한 내로잉

- 자바스크립트에서 false, 0, -0, "", null, undefined, NaN 등 `falsy`로 정의된 값을 제외한 모든 값은 참이다
  => 이를 이용해서 검사할 수 있음!

```
let okk = Math.random() > 0.5
    ? "mia"
    : undefined; //undefined는 falsy값

if(okk){
    sth.toUpperCase(); //✅
}
okk.toUpperCase();
// ❌ Error : okk' is possibly 'undefined'.
```

> => `&&`와 `?` 또한 가능하지만 이의 단점으로는

1. 참 여부 확인 회의 다른 기능 제공하지 않음
2. falsy값이 ""라면 빈문자열인지, undefined인지 알수 없음

### 3.4.3 초기값이 없는 변수

- 자바스크립트에서 초기값이 없는 변수는 `undefined`가 된다
- 타입스크립트에서 할당하지 않은 (초기값 없는) 변수 사용하려고 하면 => 오류 발생

```
let sth: string;
sth.length;
// ❌ Error : Variable 'sth' is used before being assigned.


let someth: string | undefined;
// 변수 타입에 undefined가 포함되어있는 경우에는 오류 보고 안됨

someth?.length; //✅

someth = "leekoby";
someth.length; // ✅
```

## 3.5 타입 별칭

#### 타입별칭

- 재사용하는 타입에 더 쉬운 이름을 할당하는것
- 사용 방법
  > type 새로운이름 = 타입
  > => pascalCase로 작성

```
type sth = string | name;
let something: sth = "mia";

type sth2 = boolean | number | string | null | undefined;
let first: sth2;
let second: sth2;
let third: sth2;
// ⭕ 훨씬 간단한 형태!

console.log(sth2);
//❌ Error : 'sth' only refers to a type,
but is being used as a value here.
```

=> 타입별칭은 자바스크립트엔 없다!
=> 컴파일되지 않는다!

### 3.5.2 타입 별칭 결합

- 타입 별칭은 다른 타입 별칭을 참조할 수 있다!

```
type Id = number | string;
type Idmaybe = Id | undefined | null
// IdMaybe의 타입은 number | string | undefined | null
```
