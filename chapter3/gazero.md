# 세번째, 유니언과 리터럴

### _"타입스크립트에서 해당 값을 바탕으로 추론을 수행하는 핵심 개념 !"_

- 코드 정보에 입각한 추론을 해내는 개념 <span style='background-color: #F9EEB6; color:#000'>유니언과 내로잉</span>

#### 유니언(union) ?

> 값에 허용된 타입을 <span style='background-color: #DAB4B8; color:#000'>두 개</span> 이상의 가능한 타입으로 <span style='background-color: #DAB4B8; color:#000'>확장</span>하는 것

#### 그리고 내로잉(narrowing) ?

> 값에 허용된 타입을 <span style='background-color: #DAB4B8; color:#000'>한 개</span> 이상의 가능한 타입이 되지 않도록 <span style='background-color: #DAB4B8; color:#000'>좁히는</span>것

</br>

## 3.1 유니언 타입

### <span style='background-color: #CFDC84; color:#000'>**유니언**</span>이란? (자세히...)

정확히 어떤 타입인지 모르지만 두 개 이상의 옵션 중 하나라는 것을 잠재적으로 인식하고 코드를 처리하는 개념
</br>
🔎 참고1. 코드에서는 "|" 이런 수직선으로 두 개 이상의 타입을 구분해서 보여줌

![](https://velog.velcdn.com/images/gazero_/post/416de184-4634-4940-b3a4-f20f1b1a6a6a/image.png)
그러니깐, 변수 frontendDeveloper의 타입은 <span style='background-color: #DAB4B8; color:#000'>undefined|(이거나)string</span>일 수 있다 !

### 3.1.1 유니언 타입 선언

#### 🤓유니언 타입, 그러면 언제쓰나요?

> 변수의 **초깃값이 있더**라도, 변수에 대한도 **명시적 타입 애너테이션**을 제공하는 것이 유용할 때 사용 !

### 3.1.2 유니언 속성

❗ 값이 유니언 타입일 떼, 유니언으로 선언한 모든 가능한 타입에 존재하는 멤버 속성에만 접근 가능(유니언 외 타입에 접근하려면? 타입 검사 오류 발생 !)
![](https://velog.velcdn.com/images/gazero_/post/12c28f97-b778-4cd2-b7e5-45f68291f889/image.png)정리하자면, 유니언으로 선언한 모든 타입에 가능한 속성이어야 접근 가능 !

## 3.2 내로잉

> 유니언 타입으로 정의된 여러 타입 중 하나의 타입으로 된 값의 속성을 사용하기 위해 구체적인 타입 중 하나라는 것을 알리는 과정 !

- 타입가드(type guard) ? 타입을 좁히는데 사용할 수 있는 논리적 검사

### 3.2.1 값 할당을 통한 내로잉

![](https://velog.velcdn.com/images/gazero_/post/f91f9bd1-5e58-4912-9f6d-e4a2e68f3664/image.png)

- 값 할당을 통해 string타입으로 타입을 좁힘(내로잉 시킴)

### 3.2.2 조건 검사를 통한 내로잉

![](https://velog.velcdn.com/images/gazero_/post/81f19b6b-1b57-4e5b-a239-41f1a5c49645/image.png)

### 3.2.3 typeof 검사를 통한 내로잉

![](https://velog.velcdn.com/images/gazero_/post/e25b7a33-3553-4b22-8dcf-447ccaadd0b2/image.png)

- 조건 검사를 통한 내로잉 방식과 형태가 유사

## 3.3 리터럴 타입

- 구체적인 버전의 원시타입
- 변수를 <span style='background-color: #DAB4B8; color:#000'>const</span>로 선언하고, 직접 <span style='background-color: #DAB4B8; color:#000'>리터럴 값을 할당</span>하면, 할당된 리터럴 값으로 유추

<br>
🔎 참고2. const로 선언하지 않는다면(= let으로 선언? let frontend: string으로 표시), 다시 변수 값에 할당을 해주면 동일한 효과 !

![](https://velog.velcdn.com/images/gazero_/post/688528b2-00af-4d91-9890-d3c20293caf8/image.png)

- frontend 변수 타입은 "string 타입" 임
- 하지만, "Gazero"라는 특별한 값이기도 함
- 따라서, frontend의 타입은 더 구체적인 "Gazero"임
- 즉, 특정 원싯값으로 알려진 타입이 <span style='background-color: #CFDC84; color:#000'>**리터럴 타입**</span>(하나의 문자열 "Gazero"만 나타냄)

### 3.3.1 리터럴 할당 가능성

- number, string 등 서로 다른 원시타입은 서로 할당되지 못한다.
- 이처럼, 0과 1이 동일한 원시타입이더라도 서로 다른 리터럴 타입은 할당할 수 없음
- 그러니깐, 리터럴 타입으로 string값인 "Gazero"를 선언하면서 할당했다면? 같은 string타입이라고 하더라도, "gayoung"을 할당할 수 없음 !

## 3.4 엄격한 null 검사

### 3.4.1 십억 달러의 실수

> 다른 타입이 필요한 위치에서 null 값을 사용하도록 허용하는 많은 타입 시스템을 가리키는 업계 용어

- 엄격한 null 검사 옵션 (StrictNullChecks)
- StrictNullChecks를 비활성화하면 코드의 모든 <span style='background-color: #CFDC84; color:#000'> 타입에 | null | undefined를 추가</span>해야 모든 변수가 null 또는 undefined를 할당할 수 있다.
- 🚫 StrictNullChecks 옵션을 false로 설정하더라도, 타입이 완벽하다고 간주 될 수 없음 !! 엄격한 null 검사가 활성화되면 잠재적인 충돌을 확인 가능
  ![](https://velog.velcdn.com/images/gazero_/post/804d39be-a92a-4d13-929e-a2a21de454e1/image.png)

### 3.4.2 참 검사를 통한 내로잉

- 자바스크립트에서 falsy로 정의된 값을 제외한 모든 값은 모두 참 !

```js
falsy로 정의된 값

false
0
-0
0n
""
null
undefined
NaN
```

- 타입스크립트는 <span style='background-color: #CFDC84; color:#000'>truthy</span>로 확인된 일부에 한해서 타입을 좁힐 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/42ed0726-8c93-4468-b090-956c35a17000/image.png)

### 3.4.3 초깃값이 없는 변수

- 자바스크립트에서 초깃값이 없는 변수는 기본적으로 "undefined"
- <span style='background-color: #CFDC84; color:#000'>undefined를 포함하지 않는</span> 타입으로 변수를 선언하고, 값을 할당하지 않은 상태에서 사용하려고 한다면?
  🚫 <span style='background-color: #DAB4B8; color:#000'>오류발생 </span>
  ![](https://velog.velcdn.com/images/gazero_/post/e0c06b84-1182-4cef-ba4f-75938c50ba99/image.png)

## 3.5 타입 별칭

- 반복하기 불편한 긴 형태의 유니언 타입을 위해 타입별칭(type alias)를 만들 수 있음

```js
type 새로운이름 = 타입;
```

![](https://velog.velcdn.com/images/gazero_/post/c57e1013-2e78-4179-b290-2c063d74f642/image.png)

### 3.5.1 타입 별칭은 자바스크립트가 아닙니다.

- 🚫 타입별칭은 순전히 타입 시스템에만 존재

### 3.5.2 타입 별칭 결합

- 가능 !
- 유니언 타입인 타입 별칭 내에 또 다른 유니언 타입인 타입 별칭을 포함하고 있다면, 다른 타입 별칭을 참조하는 것이 유용 !
  ![](https://velog.velcdn.com/images/gazero_/post/a2d3f71d-1310-4fc3-a694-2ca31983b3b6/image.png)
