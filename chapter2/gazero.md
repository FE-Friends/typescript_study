# 두번째. 타입 시스템

## 2.1 타입의 종류

### 타입은 무엇인가?

> _형태 (a.k.a typeof)_

자바스트립트에서 다루는 값의 형태. 즉, 값에 존재하는 속성과 메서드

#### 🔔 타입스크립트의 기본 원시타입

```
null; //null
undefined; //undefined
true; //bollean
"Louise"; //string
1337; //number
1337n //bigint
Symbol("Franklin"); //symbol
```

👍 ts특 ) 마우스 오버하면 변수 타입을 보여줌

![마우스 오버로 문자열 변수의 타입을 보여줄 수 있음](https://velog.velcdn.com/images/gazero_/post/77524e1b-5fcf-40d8-af33-48521026a4b6/image.png)

### 2.1.1 타입시스템

> 프로그래밍 언어가 프로그램에서 가질 수 있는 타입을 이해하는 방법에 대한 규칙 집합

![](https://velog.velcdn.com/images/gazero_/post/d926f4fb-52ec-4798-a805-e336843d5169/image.png)

### 2.1.2 오류 종류(구문오류 and 타입오류)

#### 구문오류

> 타입스크립트가 자바스크립트로 변환되는 것을 차단한 경우

#### 타입오류

> 타입 검사기에 따라 일치하지 않는 것이 감지된 경우

타입 오류가 있음에도 불구하고, 자바스크립트 코드를 출력 할 수 있음
하지만, 코드가 원하는 대로 실행되지 않을 가능성이 있음을 타입 오류로 알려줌
<br>
<br>
ex. 타입스크립트
![타입스크립트](https://velog.velcdn.com/images/gazero_/post/f3a7d3b7-afc5-4018-9f53-2355c283bb0b/image.png)
ex. 자바스크립트
![자바스트립트](https://velog.velcdn.com/images/gazero_/post/63f9db73-1168-4484-8e11-cf5151090372/image.png)

## 2.2 할당 가능성

> 변수의 초깃값을 읽고, 해당변수가 허용되는 타입을 결정
> <br>
> 나중에 해당 변수에 새로운 값이 할당되면, 새롭게 할당된 값의 타입이 변수의 타입과 동일한 지 확인<br> > _"전달된 값이 예상된 타입으로 할당 가능한지 여부를 확인하는 것 !"_

#### case 1. 변수에 동일한 타입의 다른 값이 할당될 때

ex. String -> String (문제 없음)

#### case 2. 변수에 다른 타입의 값이 할당될 때

ex. String -> boolean 🔔 오류 발생 !

## 2.3 타입 애너테이션

> 초깃값을 할당하지 않고도 변수의 타입을 선언할 수 있는 구문

#### case 3. 변수에 타입스크립트가 읽어야 할 초깃값이 없는 경우

타입스크립트는 나중에 사용할 변수의 초기 타입을 파악하려고 시도 하지 않음
<br>
기본적으로 변수를 암묵적인 any타입으로 간주
![](https://velog.velcdn.com/images/gazero_/post/67fbc921-9d8b-4204-b7f5-78718f5a4c88/image.png)

![](https://velog.velcdn.com/images/gazero_/post/bc052151-6175-4367-a7d7-81faf423031f/image.png)

any 변수인 gazero에 처음에 문자열(Ga young)이 할당
![](https://velog.velcdn.com/images/gazero_/post/acc15614-de52-4605-8abb-e32ae8f085f8/image.png)
그 다음 number타입으로 진화

### 🔔 따라서 이를 위해 타입 애너테이션을 사용 !

![](https://velog.velcdn.com/images/gazero_/post/45d0e0de-9e79-4f02-b656-fbec8f6c00e5/image.png)
![](https://velog.velcdn.com/images/gazero_/post/be8903a4-bfb2-4a23-810d-1cd2ff42a9fd/image.png)

> 변수에 타입 애너테이션으로 정의한 타입 외의 값을 할당하면 타입 오류가 발생

<br>

## 2.4 타입 형태

<br>

> 각각 타입에 알맞는 속성에 접근만을 허락함

- string 타입에서 .length는 수행가능 하지만, .push는 허용되지 않음
