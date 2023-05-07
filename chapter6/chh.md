## 6. 배열

-   자바스크립트의 배열은 매우 유연하고 내부에 모든 타입의 값을 혼합해서 저장할 수 있습니다.
-   **타입스크립트는 초기 배열 데이터 타입을 확인하고, 해당 데이터 타입에서만 작동하도록 제한 합니다.**

<br>

### 자바스크립트에서

![1](https://user-images.githubusercontent.com/87301268/236661207-f7dde31a-e197-4d61-a046-3e8acdb237af.png)

<br>

### 타입스크립트에서

다음 예제는 warrios 배열이 **초기에 string 타입의 값을 포함**한다는 것을 알고 있으므로 <br>
이후 `string 타입의 값 추가는 허용`하지만 **다른 데이터 타입 추가는 허용하지 않습니다.**

![2](https://user-images.githubusercontent.com/87301268/236661351-812ff06c-7389-43ab-a23f-536476dd14ec.png)

<br>

## 6.1 배열 타입

다른 변수 선언과 마찬가지로 배열을 저장하기 위한 변수는 초기값이 필요하지 않습니다.

-   변수는 `undefined` 으로 시작해서 나중에 배열 값을 받을 수 있습니다.
-   배열에 대한 타입 애너테이션은 배열의 요소 타입 다음에 `[]` 사용 합니다.

![3](https://user-images.githubusercontent.com/87301268/236661555-ea75142e-02bf-4bd0-a838-b2f043c79352.png)

<br>

### 6.1.1 배열과 함수 타입

-   배열 타입은 함수 타입에 무엇이 있는지를 구별하는 괄호가 필요한 구문 컨테이너의 예시 입니다.
-   괄호는 애너테이션의 어느 부분이 `함수 반환 부분`이고 어느 부분이 `배열 타입 묶음`인지 나타내기 위해 사용

![4](https://user-images.githubusercontent.com/87301268/236661802-8289f1c1-8794-4c79-a0e1-579b2b9ed59d.png)

<br>

### 6.1.2 유니언 타입 배열

배열의 각 요소가 여러 선택 타입 중 하나일 수 있음을 나타낼 때 사용 합니다.

-   애너테이션의 `어느 부분이 배열의 콘텐츠`이고 `어느 부분이 유니언 타입 묶음`인지 나타내기 위해 **괄호**를 사용 할 수 있습니다.

![5](https://user-images.githubusercontent.com/87301268/236662114-68c01f0d-5c2f-482b-b112-85d54c28077a.png)

<br>

다음 예시는 `string` 값과 `undefined` 값을 모두 가지므로 `(string | undefined)[]` 타입 입니다.

![6](https://user-images.githubusercontent.com/87301268/236662219-b0c3a84d-e438-4b5b-b147-37052f124f5c.png)

<br>

### 6.1.3 any 배열의 진화

초기에 빈 배열로 설정된 변수에서 타입 애너테이션을 포함하지 않으면 <br> 타입스크립트는 배열을 `any[]`로 취급 합니다.

![7](https://user-images.githubusercontent.com/87301268/236662315-e73131e5-ed3b-4ed9-b181-c748a89fe8eb.png)

<br>

### 6.1.4 다차원 배열

2차원 배열 또는 배열의 배열은 두 개의 `[](대괄호)`를 갖습니다.

-   3차원은 세개의 [ ], 4차원은 네개의 [ ] 가 있습니다.

![8](https://user-images.githubusercontent.com/87301268/236662456-ed0b20b1-082a-48a0-81cb-1697fe6b9176.png)

-   arr 배열은 number[][] 타입이고 (number[])[]로 나타낼 수 있습니다.

<br>

## 6.2 배열 멤버

타입스크립트는 배열의 멤버를 찾아서 해당 배열의 타입 요소를 되돌려주는 인덱스 기반 접근 방식을 이해하는 언어

![9](https://user-images.githubusercontent.com/87301268/236662726-0a7f8dd7-793b-4324-867a-0d3a7f09c40b.png)

-   defenders 배열은 string[] 타입이므로 defender는 string 타입 입니다.
-   soldierOrDates 는 (string | Data)[] 타입이므로 soldierOrDate 변수는 string | Date 타입 입니다.

<br>

### 6.2.1 주의사항: 불안정한 멤버

타입스크립트의 타입 시스템은 기술적으로 불안정하다고 알려져 있습니다.

대부분 올바른 타입을 얻을 수 있지만, 때로는 값 타입에 대한 타입 시스템의 이해가 올바르지 않습니다.

배열은 타입 시스템에서 불안정한 소스 입니다.

-   타입스크립트는 모든 배열의 멤버에 대한 접근이 해당 배열의 멤버를 반환한다고 가정하지만
-   자바스크립트는 배열의 길이보다 큰 인덱스로 배열 요소 접근 시 undefined 를 반환 합니다.

<br>

![10](https://user-images.githubusercontent.com/87301268/236663003-363eb58f-f1a8-471c-a430-f9a0df31f04e.png)

-   런타임 시 `Cannot read property 'length' of undefined` 를 유추 할 수 있지만
-   타입스크립트에서는 **검색된 배열의 멤버가 존재하는지 의도적으로 확인하지 않습니다.**

<br>

## 6.3 스프레드와 나머지 매개변수

### 6.3.1 스프레드

spread operator를 사용해 배열을 결합 합니다.

-   타입스크립트는 입력된 배열 중 하나의 값이 결과 배열에 포함될 것임을 이해 합니다.
-   입력된 배열이 동일한 타입이라면 출력 배열도 동일한 타입 입니다.
-   서로 다른 타입의 두 배열을 함께 스프레드해 새 배열을 생성하면 <br> 새 배열은 두 개의 타입 중 어느 하나의 요소인 유니언 타입 배열로 이해 됩니다.

![11](https://user-images.githubusercontent.com/87301268/236663954-3c9843f7-03f6-4de8-9e90-b9fa5e4aa9fb.png)

<br>

### 6.3.2 나머지 매개변수 스프레드

나머지 매개변수를 위한 인수로 사용되는 배열은 **나머지 매개변수와 동일한 배열 타입을 가져야 합니다.**

나머지 매개변수로 string 값만 받는다면 string[] 타입 배열을 스프레드하는 것은 허용되지만 <br> number[]는 허용되지 않습니다.

![12](https://user-images.githubusercontent.com/87301268/236664403-80405567-d8a8-4c24-b05c-a8a903712d6d.png)

<br>

## 6.4 튜플

자바스크립트 배열은 이론상 **어떤 크기**라도 될 수 있습니다.

-   하지만 때로는 `튜플`이라고 하는 **고정된 크기의 배열**을 사용하는 것이 유용 합니다.
-   튜플은 각 인덱스에 알려진 특정 타입을 가집니다.
-   튜플 타입을 선언하는 구문은 배열 리터럴 처럼 보이지만 값 대신 타입을 적습니다.

![13](https://user-images.githubusercontent.com/87301268/236664897-0e9e6f8b-bb1f-4027-885a-29dfd87d0ce7.png)

<br>

### 6.4.1 튜플 할당 가능성

가변 길이의 배열 타입은 튜플 타입에 할당할 수 없습니다.

-   길이가 서로 다른 튜플은 서로 할당할 수 없습니다.
-   `[boolean, number]` 가 있는 것을 볼 수 있지만, 타입스크립트는 더 일반적인 <br> `(boolena | number)[]` 로 유추 합니다.

![14](https://user-images.githubusercontent.com/87301268/236665206-0eb2496b-100f-4f81-b012-77ec824c395c.png)

<br>

다음 tupleTwoExtra 는 정확히 두 개의 멤버를 가져야 하므로 tupleThree가 올바른 멤버로 시작하더라도
세 번째 멤버는 tupleTwoExtra에 할당 할 수 없습니다.

![15](https://user-images.githubusercontent.com/87301268/236665784-34a5b6bc-2749-4926-88b0-064869af7035.png)

<br>

### 나머지 매개변수로서의 튜플

나머지 매개 변수 튜플을 사용하고 싶다면 여러 번 함수를 호출하는 인수 목록을 배열에 저장해 함께 사용 가능 합니다.

trios는 튜플 배열이고, 각 튜플은 두 번째 멤버로 또 튜플을 가집니다.

-   `trios.forEach(trio => logTrio(...trio))` 는 각 ...trio가 logTrio의 매개변수 타입과 일치하므로 안전한 것으로 알려지고
-   `trio.forEach(logTrio)` 는 첫 번째 매개변수로 타입이 string인 [string, [number, boolean]] 전체를 전달하려고 시도하기 때문에 할당할 수 없습니다.

![16](https://user-images.githubusercontent.com/87301268/236666157-269c3b5d-b1e0-4883-b6a0-c72565c4f05d.png)

<br>

### 6.4.2 튜플 추론

### 명시적 튜플 타입

함수가 튜플 타입을 반환한다고 선언되고, 배열 리터럴을 반환한다면 튜플로 간주 합니다.

![17](https://user-images.githubusercontent.com/87301268/236666521-7fda1491-93d6-4254-a6b3-8a2ae931e2aa.png)

-   firstCharAndSize 함수는 `string` 과 `number`인 튜플을 반환한다고 명시되어 있습니다.

<br>

### const 어서션

위와 같은 작업은 코드 변경에 따라 작성이 번거로울 수 있습니다. <br>
그 대안으로 타입스크립트는 값 뒤에 넣을 수 있는 const 어셔션인 `as const` 연산자를 제공 합니다.

-   const 어셔션은 타입스크립트에 타입을 유추할 때 **읽기 전용이 가능한 값 형식**을 사용하도록 지시
-   배열 리터럴 뒤 as const가 배치되면 **배열이 튜플로 처리되어야 함을 나타냅니다.**
-   const 어서션은 튜플로 전환을 넘어서 **읽기 전용**, **값 수정이 예상 되는 곳에서 사용할 수 없음**을 나타냅니다.

![18](https://user-images.githubusercontent.com/87301268/236666868-cde7e6ae-2813-4d72-b199-26da36f9b490.png)

![19](https://user-images.githubusercontent.com/87301268/236667194-d13c3ac0-7ac6-4050-a327-42a13f12cbe2.png)

<br>

### 명시적 튜플 타입의 예시를 as const 으로

![20](https://user-images.githubusercontent.com/87301268/236667254-0322e91a-52be-4221-ac5d-264ae491be98.png)
