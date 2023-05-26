# 아홉번째. 타입 제한자

## 9.1 top 타입

#### top 타입 ?

> 시스템에서 가능한 모든 값을 나타내는 타입

- 모든 다른 타입의 값은 타입이 top인 위치에 제공될 수 있음
- 모든 타입은 top 타입에 할당할 수 있음
- top타입을 사용하면 타입 검사가 매우 유연해짐 따라서 타입 에러를 사전에 발견하기 어려울 수 있음
- 더 구체적이고 명확한 타입을 사용하는 것이 좋음

### 9.1.1 any 다시 보기

- any 타입은 <span style='background-color: #f5b5b6; color:#000'>**모든**</span> 타입의 위치에 제공될 수 있다는 점에서 _top 타입_ 처럼 작동할 수 있음
- any는 타입스크립트가 해당 값에 대한 할당 가능성 또는 멤버에 대해 타입 검사를 수행하지 않도록 명시적으로 지시한다는 문제점이 있음

### 9.1.2 unknown

- 진정한 top타입 = unknown타입
- 모든 객체를 unknown 타입의 위치로 전달할 수 있다는 점에서 any타입과 유사
- unknown타입과 any타입의 차이점은 unknown 타입의 값을 훨씬 더 제한적으로 취급함

```
 1. 타입스크립트는 unknown 타입 값 속성에 직접 접근할 수 없음
 2. unknown 타입은 top 타입이 아닌 타입에는 할당할 수 없음
```

![](https://velog.velcdn.com/images/gazero_/post/b614af78-6e2d-4d49-81e1-caf4d4bac2ce/image.png)

- 따라서, unknown 타입 값의 속성에 접근하려고 시도할 경우 타입오류

#### 그렇다면, unknown타입에 접근하는 방법은 ?

> instanceof나 typeof 또는 타입 어서션을 사용하는 것처럼 타입이 제한된 경우 !

## 9.2 타입 서술어

- 로직을 함수로 감싸면 타입을 좁히기 어려움
  ![](https://velog.velcdn.com/images/gazero_/post/8e361638-18eb-4840-8332-f230e1ea76ed/image.png)
- 첫번째 함수는 value를 받고, 그 값은 number 또는 string인지를 나타내는 boolean 값을 반환
- 하지만 타입스크립트는 boolean 값을 반환한다는 사실만 알 수 있고, 인수의 타입을 좁히기 위함이라는 건 알 수 없음

#### 타입서술어(a.k.a 사용자 정의 타입 가드)

> 인수가 특정 타입인지 여부를 나타내기 위해 boolean 값을 반환하는 함수를 위한 특별한 구문

- 타입 서술어는 매개변수로 전달된 인수가 매개변수의 타입보다 더 구체적인 타입인지 여부를 나타낼 때 사용
- 타입 서술어의 반환 타입은 <span style='background-color: #f5b5b6; color:#000'>매개변수의 이름, is 키워드, 특정 타입</span> 으로 선언할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/e83ab152-244e-4123-b80d-761cb1610b56/image.png)
- isNumberOrString함수에서 반환값 타입을 value is number|string으로 변경하면, 명시적 반환타입을 가질 수 있음
- 따라서 타입스크립트는 value가 number|string인 경우의 코드 블록은 number|string 타입의 값을 가져야 한다고 추론

#### 반면에

- 하지만, number|string이 아닌 경우의 코드 블록은 null|undefined를 가져야 함
  ![](https://velog.velcdn.com/images/gazero_/post/96cc0d4b-cbbd-43ba-80fe-1637a31a5c81/image.png)

- 타입서술어는 boolean 값을 반환하는 것이 아니라 더 구체적인 타입을 나타냄 !
- 타입서술어는 이미 한 인터페이스의 인스턴스로 알려진 객체가 더 구체적인 인터페이스의 인스턴스인지 여부를 검사하는 데 자주 사용함
  ![](https://velog.velcdn.com/images/gazero_/post/d33545da-7766-4e65-8702-6848159c8ce9/image.png)
- 주의 ! 타입 서술어는 false 조건에서 타입을 좁힘
- 따라서 타입 서술어가 입력된 타입 이상을 검사할 수 있음

![](https://velog.velcdn.com/images/gazero_/post/09946e57-2edf-4edb-b793-7d354335f833/image.png)

- isLongString 타입 서술어는 input 매개변수가 undefined 또는 길이가 7보다 작은 string인 경우 false를 반환(그러니깐, 7보다 큰 string은 true)
- 따라서 else 문은 text를 undefined 타입으로 좁힘

## 9.3 타입 연산자

> 기존 타입의 이름만으로 모든 타입을 설명할 수 없음 !

### 9.3.1 keyof

![](https://velog.velcdn.com/images/gazero_/post/f53c5b8a-c85f-4e2e-8dc9-c1b14cf20ddc/image.png)

- 타입 string은 Ratings 인터페이스에서 속성으로 허용되지 않는 값을 허용
- Ratings는 string 키를 허용하는 인덱스 시그니처를 선언하지 않음

#### 다른 옵션은 허용되는 키를 위한 <span style='background-color: #f5b5b6; color:#000'>리터럴 유니언</span> 타입

![](https://velog.velcdn.com/images/gazero_/post/074b403a-8dc6-4008-9503-b6848273c137/image.png)

- 컨테이너 값에 존재하는 키를 적절히 제한해야 함

#### 인터페이스에 무수히 많은 멤버가 있다면?

- 기존에 존재하는 타입을 사용하고, 해당 타입에 허용되는 모든 키의 조합을 반환하는 <span style='background-color: #f5b5b6; color:#000'>keyof</span> 연산자를 제공
- 타입 애너테이션처럼 타입을 사용하는 모든 곳에서 타입 이름 앞에 keyof 연산자를 배치
  ![](https://velog.velcdn.com/images/gazero_/post/60673070-c5bc-4808-8ba2-54e52ae40b51/image.png)
- keyof Ratings = 'audience'|'critic'

### 9.3.2 typeof

- typeof는 제공되는 값의 타입을 반환
  ![](https://velog.velcdn.com/images/gazero_/post/3144d9d4-94cf-4370-a39e-f31e83293d72/image.png)
- adaptation에 original의 객체 형식의 타입이 적용됨
- adaptation은 medium: string, title: string 타입을 갖음

#### keyof typeof

- typeof는 값의 타입을 검색
- keyof는 타입에 허용된 키를 검색
- 타입스크립트는 두 키워드를 연결해 값의 타입에 허용된 키를 간결하게 검색 가능

1. keyof 키 검색가능 !
   ![](https://velog.velcdn.com/images/gazero_/post/b7f9b692-c62e-47bc-aa63-3d9f688c76f2/image.png)
2. typeof 값의 타입을 검색 !
   ![](https://velog.velcdn.com/images/gazero_/post/280b358e-cb07-4fe8-bd6b-8f1c3a3967f5/image.png)

- keyof typeof를 사용해 키가 ratings 값 타입의 키 중 하나여야 함을 나타냄

## 9.4 타입 어서션(a.k.a 타입 캐스트)

> 값의 타입에 대한 타입 시스템의 이해를 재정의하기 위함

- 다른 타입을 의미하는 값의 타입 다음주 <span style='background-color: #f5b5b6; color:#000'>as</span>키워드를 배치
- 타입 시스템은 어서션을 따르고 값을 해당 타입으로 처리함

### 9.4.1 포착된 오류 타입 어서션

- 오류를 처리할 때 유용함
- 코드 영역이 Error클래스의 인스턴스를 발생시킬 거라 틀림없이 확신한다면 타입 어서션을 사용해 포착된 어서션을 오류로 처리할 수 있음

### 9.4.2 non-null 어서션

- null 또는 undefined가 아니라고 간주함
  ![](https://velog.velcdn.com/images/gazero_/post/1a3655b7-95d1-49ea-a6be-e4454c94438a/image.png)
- 아래 두 타입 어서션은 타입이 Date|undefined가 아니라 Date가 된다는 점에서 동일
- non-null 어서션은 값을 반환하거나 존재하지 않는 경우 undefined를 반환하는 Map.get과 API에서 유용

### 9.4.3 타입 어서션 주의 사항

> 타입 어서션은 사용하는 것이 안전하다고 확신할 때만 사용 !

#### 어서션 vs. 선언

- 변수의 타입 애너테이션과 초깃값이 모두 있을 때, 타입 애너테이션에 대한 변수의 초깃값에 대한 할당 가능성 검사를 수행
- 타입 어서션은 타입스크립트에 타입 검사 중 일부를 건너뛰도록 명시적으로 지시

![](https://velog.velcdn.com/images/gazero_/post/2b1ad31d-2c6e-4186-883c-084cb609cad5/image.png)

- Entertainer 타입 애너테이션으로 declared 변수에서 오류를 잡을 수 있었음
  ![](https://velog.velcdn.com/images/gazero_/post/84697d85-a03f-4966-80ff-18d65ecc1f00/image.png)
- 하지만, 타입 어서션 때문에 asserted 변수에 대해 오류를 잡을 수 없었음

#### 어서션 할당 가능성

- 타입스크립트는 타입 중 하나가 다른 타입에 할당 가능한 경우에만 두 타입 간의 타입 어서션을 허용
- 서로 관련없는 두 타입 사이에 타입 어서션이 있는 경우 타입 오류를 감지
  ![](https://velog.velcdn.com/images/gazero_/post/c1a1f7b9-843e-468c-94cc-aca4badac89b/image.png)
- 원시 타입이 전혀 관련이 없기 때문에 원시 타입에서 다른 원시 타입으로 전환은 불가

#### 그래도 완전 관련 없는 타입으로 전환하고 싶다면 ? 이중 타입 어서션 !

- 먼저 값을 any 혹은 top 타입으로 전환하고 결과를 관련 없는 타입으로 전환
- 그렇지만 안쓰는게 좋음

## 9.5 const 어서션

> const 어션은 배열, 원시 타입, 값, 별칭 등 모든 값을 상수로 취급해야 함을 나태는 데 사용

- <span style='background-color: #f5b5b6; color:#000'>as const</span>는 수신하는 모든 타입에 세가지 규칙을 적용

```
1. 배열은 가변 배열이 아니라 읽기 전용 튜플로 취급
2. 리터럴은 일반적인 원시 타입과 동등하지 않고 리터럴로 취급
3. 객체의 속성을 읽기 전용으로 간주
```

### 9.5.1 리터럴에서 원시 타입으로

- 더 구체적으로 쓸 수 있음 !
  ![](https://velog.velcdn.com/images/gazero_/post/e6f630f9-8432-4eb2-92a1-44e3fa8da178/image.png)
  ![](https://velog.velcdn.com/images/gazero_/post/73ef7af5-0c08-4236-bf97-1403152c72de/image.png)
- string 보다 더 구체적인 "M" 타입으로 !
  ![](https://velog.velcdn.com/images/gazero_/post/9c5af898-8dfa-4953-81bd-8153f95a7325/image.png)
- 해당 코드의 타입이 값을 더 구체적으로 추론할 수 있음

### 9.5.2 읽기 전용 객체

- as const를 사용해 값 리터럴을 어서션하면 유추된 타입이 가능한 한 구체적으로 전환
- 모든 멤버 속성은 readonly가 됨
- 리터럴은 일반적인 원시 타입 대신 고유한 리터럴 타입으로 간주
- 배열은 읽기 전용 튜플이 됨
- 값 리터럴에 const 어서션을 적용하면 해당 값 리터럴이 변경되지 않고 모든 멤버에 동일한 const 어서션 로직이 재귀적으로 적용
