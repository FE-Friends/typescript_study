# 네번째. 객체

## 4.1 객체 타입

> ### 객체 리터럴의 형태

```js
const gazero = {...} 형태의 구문
```

> ### 속성값에 접근하는 방법

```js
gazero.멤버 혹은 gazero['멤버']
```

따라서, gazero객체 리터럴 안에 객체의 <span style='background-color: #DAB4B8; color:#000'>속성명</span>이 존재하는 경우 해당 방법으로 해당 <span style='background-color: #DAB4B8; color:#000'>속성값</span>에 접근이 가능 !

![](https://velog.velcdn.com/images/gazero_/post/1c865cc5-fe27-4558-ae98-451e12469f5c/image.png)

### 4.1.1 객체 타입 선언

- 명시적 선언(유추하는 방법도 괜찮긴 함)
- 별도의 객체 형태를 설명하는 방법
- 객체 타입과 객체 리터럴은 다름 !
  ![](https://velog.velcdn.com/images/gazero_/post/bc0a29f8-558b-46da-87d7-181d6033c513/image.png)

### 4.1.2 별칭 객체 타입

- 객체 타입을 미리 별칭에 할당 !
- 이전에 chapter3에서 다뤘던 타입별칭과 유사한 개념
  ![](https://velog.velcdn.com/images/gazero_/post/600b903b-9e9e-436b-b207-fce3c2ee634d/image.png)
- 미리 gazero(별칭)에 타입꾸러미(객체 타입)를 만들어 놓고, 해당 꾸러미를 사용하고자 하는 변수에 할당 후 사용 ! 이후 사용 방법은 (4.1.1 객체 타입 선언과 동일

## 4.2 구조적 타입화

- 구조적으로 타입화(structurally typed): 타입을 충족하는 모든 값을 해당 타입의 값으로 사용
- 매개변수나 변수가 특정 객체 타입으로 선언되면 타입스크립트에 어떤 객체를 사용하든 해당 속성이 있어야 함

![](https://velog.velcdn.com/images/gazero_/post/ef9873a3-5777-4ef7-91b6-bd0527eb3b1b/image.png)

- gazeroFirstName, gazeroLastName은 각각 string 타입의 firstName, lastName을 타입 선언
- gazero에 firstName, lastName이 명시적으로 선언되어 있지 않더라도 각각 <span style='background-color: #DAB4B8; color:#000'>선언된 변수를 모두 제공</span> 받을 수 있음

### 4.2.1 사용 검사

- 객체 타입으로 애너테이션된 위치에 값을 제공할 때, 값을 해당 객체 타입에 할당할 수 있는지 확인
- 할당하는 값에는함<span style='background-color: #DAB4B8; color:#000'>객체 타입의 필수 속성</span>이 있어야 함

![](https://velog.velcdn.com/images/gazero_/post/6622f3ab-b413-408a-aa77-2daa618adfa0/image.png)

- 그러니깐, FirstAndLastNames(타입 별칭) 안에 만들어둔 <span style='background-color: #DAB4B8; color:#000'>속성(first, last)은 반드시 할당하는 값</span>에 있어야 함, 만들어둔 속성에 해당하는 <span style='background-color: #DAB4B8; color:#000'>타입</span>도 일치해야 함

### 4.2.2 초과 속성 검사

- 변수가 객체 타입으로 선언되고, 🚫 초깃값에 객체 타입에서 정의된 것보다 많은 필드가 있다면 오류발생 !
  ![](https://velog.velcdn.com/images/gazero_/post/a01b2766-d74e-4269-97c5-93035490bfb3/image.png)

### 4.2.3 중첩된 객체 타입

#### <span style='background-color: #CFDC84; color:#000'>**방법 1.**</span>

![](https://velog.velcdn.com/images/gazero_/post/f52c3f65-c280-47ee-b411-6654f0419404/image.png)

#### <span style='background-color: #CFDC84; color:#000'>**방법 2.**</span>

- 중첩된 객체 타입을 별도 별칭객체 타입으로 추출해서 할당하는 방법도 가능

![](https://velog.velcdn.com/images/gazero_/post/3487eeaf-d45b-4dd3-81cf-b13a1b8a18d4/image.png)

#### <span style='background-color: #CFDC84; color:#000'>**추출방법**</span>

![](https://velog.velcdn.com/images/gazero_/post/8ef6f4db-5043-4762-baca-8ad123e272b0/image.png)

### 4.2.4 선택적 속성

- 타입 속성 애너테이션에서 : 앞에 ? 를 추가하면 선택적 속성임을 나타낼 수 있음
- 따라서, ?가 추가된 속성은 필수적적인 속성이 아님 !
  ![](https://velog.velcdn.com/images/gazero_/post/395c12b4-666f-46ee-a4af-5ed4be7210a2/image.png)
- 즉, ?가 추가된 name은 필수 속성이 아님 !

❗<span style='background-color: #CFDC84; color:#000'>**undefined**</span>로 대체 할 수 없을까?

> 결론 ! <span style='background-color: #DAB4B8; color:#000'>대체할 수 없음</span>
> 결국 그 값이 undefined라고 하더라도 반드시 존재해야 함

## 4.3 객체 타입 유니언

- 속성이 조금 다른, 하나 이상의 서로 다른 객체 타입이 될 수 있는 타입을 설명할 수 있어야 함
- 속성값을 기반으로 해당 객체 타입 간에 타입을 좁혀야 할 수 있음

### 4.3.1 유추된 객체 타입 유니언

- 변수에 여러 객체 타입 중 하나가 될 수 있는 초깃값이 주어지면 타입스크립트는 해당 타입을 객체 타입 유니언으로 유추
- 유니언 타입은 가능한 각 객체 타입을 구성하고 있는 요소를 모두 가질 수 있음
- 객체 타입에 정의된 각각의 가능한 속성은 객체 타입의 구성 요소로 주어짐
  ![](https://velog.velcdn.com/images/gazero_/post/5ca7f8de-0a03-46aa-a47c-24e250e05806/image.png)

### 4.3.2 명시된 객체 타입 유니언

- 객체 타입의 조합을 명시
  ![](https://velog.velcdn.com/images/gazero_/post/058f1186-3213-47d1-a1cb-896d7d9a3684/image.png)
- Gazero 형식에는 pages와 rhymes속성은 항상 필수적으로 존재하는 사항이 아니므로, Gazero타입을 할당한 변수 gazero에서는 조건에 해당하는 경우를 제외하고, 해당 속성에 접근할 수 없음

### 4.3.3 객체 타입 내로잉

- 코드에서 객체의 형태를 확인하고 타입 내로잉이 객체에 적용됨
  ![](https://velog.velcdn.com/images/gazero_/post/d3e0bfda-9e8c-410e-b84c-2205b3fece17/image.png)
- 각각 조건에 따라 gazero는 GazeroPages로 좁혀지거나, GazeroRhymes로 좁혀짐

### 4.3.4 판별된 유니언

- 판별된 유니언(discriminated union): 객체의 속성이 객체의 형태를 나타내도록 하는 것
- 판별값: 객체 타입을 가리키는 속성
  ![](https://velog.velcdn.com/images/gazero_/post/0edb21f4-378a-404e-bc37-b4e4663ba5cf/image.png)
- gazero.type이 pages면 타입 스크립트는 gazero를 GazeroPages로 유추
- 내로잉 없이는 값에 존재하는 속성을 보장할 수 없음

## 4.4 교차 타입

- 교차타입(interaction type)을 사용해 여러 타입을 동시에 사용
- 여러 기존 객체 타입을 별칭 객체 타입으로 결합해 새로운 타입을 생성
  ![](https://velog.velcdn.com/images/gazero_/post/e80c2bb4-841e-4ef2-ad57-09ca11731377/image.png)
- Gazero 타입은 항상 GazeroArt와 GazeroWriting타입 속성을 모두 가진다.
  <br>

**_tip. 유니언 타입과 결합도 가능_**
![](https://velog.velcdn.com/images/gazero_/post/2de589a7-c4b5-4d04-a377-3983fb8d2a62/image.png)

- GoodGazero는 반드시 author속성을 가지며, type속성으로 판별된 유니언 타입임
  ![](https://velog.velcdn.com/images/gazero_/post/3a83136d-14b1-45de-bb01-c93a9744fd5d/image.png)
- type 속성으로 판별되었으므로 다른 타입의 속성을 사용할 수 없음

### 4.4.1 교차 타입의 위험성

- 혼동하기 쉽기 때문에, 가능한 한 간결하게 코드를 유지할 필요가 있음

#### <span style='background-color: #CFDC84; color:#000'>**긴 할당 가능성 오류**</span>

- 타입을 일련의 별칭으로 된 객체 타입으로 분할하면 좋음
  ![](https://velog.velcdn.com/images/gazero_/post/493751a6-0f54-4480-8b44-d7e89667ddc2/image.png)

#### <span style='background-color: #CFDC84; color:#000'>**never**</span>

- 원시 타입의 값은 동시에 여러 타입이 될 수 없음 따라서 교차 타입의 구성 요소로 함께 결합할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/d58e3b35-8d63-4dc8-9ae9-a172028b7e86/image.png)
- never타입이 됨
- never타입은 bottom / empty 타입으로 값을 가질 수 없고, 참고할 수 없음 따라서 어떠한 타입을 제공할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/236d2259-cd22-4ca0-9e47-2af03c145e2a/image.png)
