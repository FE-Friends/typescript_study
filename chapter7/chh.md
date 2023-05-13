## 7. 인터페이스(interface)

연관된 이름으로 객체 형태를 설명하는 또 다른 방법입니다.

-   타입 별칭과 유사하지만 더 읽기 쉬운 오류 메시지, 더 빠른 컴파일러 성능, 클래스와의 더 나은 상호 운용성을 위해 선호됩니다.

<br>

## 7.1 타입 별칭 vs 인터페이스

![1](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/b5b7dddb-5833-4076-8779-4363d2ce22d8)

두 구문은 거의 같습니다.

<br>

### 타입 별칭과 인터페이스의 차이점

1. 인터페이스는 **속성 증가**를 위해 **병합** 할 수 있습니다. <br>
   → 내장된 전역 인터페이스 또는 npm 패키지와 같은 외부 코드를 사용할 때 유용 합니다.

2. 인터페이스는 클래스가 선언된 구조의 타입을 확인하는데 사용할 수 있습니다.

3. 인터페이스에서 타입스크립트 **타입 검사기가 더 빨리 작동** 합니다. <br>
   → 내부적으로 더 쉽게 캐시할 수 있는 명명된 타입을 선언하기 때문.

4. 인터페이스는 이름 있는(명명된) 객체로 간주되므로 오류 메시지를 좀 더 쉽게 읽을 수 있습니다.

<br>

## 7.2 속성 타입

### 7.2.1 선택적 속성

객체 타입과 마찬가지로 모든 객체가 필수적으로 인터페이스 속성을 가질 필요는 없습니다.

-   타입 애너테이션 앞 `:` 에 **?** 를 사용해 인터페이스의 속성이 선택적 속성임을 나타낼 수 있습니다.

![2](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/ef7fa908-92ff-4d82-8a01-0701d9ae7479)

<br>

Book 인터페이스는 필수 속성 pages와 선택적 속성 author를 갖습니다.

-   Book 인터페이스를 사용하는 객체에 필수 속성만 제공된다면 선택적 속성은 제공되거나 생략할 수 있습니다.

<br>

### 7.2.2 읽기 전용 속성

경우에 따라 인터페이스에 정의된 객체의 속성을 **재할당**하지 못하도록 인터페이스 사용자를 차단하고 싶습니다.

-   `readonly` 키워드를 추가해 다른 값으로 설정 될 수 없음을 나타냅니다.
-   위의 속성은 읽을 수는 있지만 **새로운 값으로 재할당하지 못합니다.**
-   단지 타입 검사기를 사용해 개발 중에 그 속성이 수정되지 못하도록 보호하는 역할 입니다.

![3](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/a01e1ad3-2d3b-4bf4-905b-0da089bfcea3)

<br>

### 7.2.3 함수와 메서드

타입스크립트에서는 인터페이스 멤버를 함수로 선언하는 두 가지 방법을 제공합니다.

-   메서드 구문 : member(): void와 같이 **객체의 멤버로 호출되는 함수**로 선언
-   속성 구문 : member: () => void와 같이 **독립 함수**와 동일하게 선언

또한 `?:`를 사용해서 선택적 속성을 나타낼 수 있습니다.

![4](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/525c1554-e0c2-430a-9661-1dd030399bbc)

<br>

### 7.2.4 호출 시그니처

호출 시그니처는 값을 **함수처럼 호출하는 방식**에 대한 타입 시스템의 설명입니다.

-   호출 시그니처로 **선언한 방식으로 호출되는 값만 인터페이스에 할당** 할 수 있습니다.
-   즉, 할당 가능한 매개변수와 반환 타입을 가진 함수 입니다.
-   함수와 비슷하지만 콜론(:) 대신 **화살표(=>)** 로 표시 합니다.

![5](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/09d9628c-fb8a-4da6-80f2-a02b312be86a)

<br>

호출 시그니처는 사용자 정의 속성을 추가로 갖는 함수를 설명하는데 사용 할 수 있습니다.

![6](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/1d2f7cf0-dec6-4963-860a-ef54398e2597)

keepsTrackOfCalls 함수 선언에는 number 타입인 counter 속성이 주어져 <br>
FunctionWithCount 인터페이스에 할당 할 수 있습니다.

-   따라서 FunctionWithCount 타입의 hasCallCount 인수에 할당 할 수 있습니다.
-   마지막 함수에는 count 속성이 주어지지 않아서 오류가 발생 합니다.

<br>

### 7.2.5 인덱스 시그니처

인터페이스 개체가 임의의 키를 받고, 해당 키 아래의 특정 타입을 반환 할 수 있음을 나타냅니다.

-   자바스크립트 객체 속성 조희는 암묵적으로 **키를 문자열로 반환**하기 때문에 <br> 인터페이스의 객체는 문자열 키와 함께 가장 일반적으로 사용 됩니다.
-   인덱스 시그니처는 일반 속성 정의와 유사하지만 키 다음에 타입이 있고 `[i: string]:` 같이 배열의 대괄호를 가집니다.

![7](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/b5a03d3a-b3ea-4b75-8212-4ee02eb7c572)

<br>

### 속성과 인덱스 시그니처 혼합

인터페이스는 명시적으로 명명된 속성과 **포괄적인 용도**의 string 인덱스 시그니처를 한번에 포함할 수 있습니다.

-   HistoricalNovels 는 모든 속성을 number 타입으로 선언했고 추가적으로 Oroonoko 속성이 존재해야 합니다.

![8](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/6aed5d1f-0c2a-407a-a88c-91360e77b955)

<br>

예시의 ChapterStarts는 perfect 속성은 0으로, 다른 모든 속성은 <br> 더 일반적인 number를 갖도록 선언합니다.

-   즉, ChapterStarts를 사용하는 모든 객체의 perfect 속성은 반드시 0이어야 합니다.

![9](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/3823f6fb-6792-4da2-8d05-2f40b3ea2874)

<br>

### 숫자 인덱스 시그니처

자바스크립트가 암묵적으로 객체 속성 조회 키를 문자열로 반환하지만 때로는 객체의 키로 숫자만 허용하는 것이 바람직할 수 있습니다.

-   키로 string 대신 **number 타입**을 사용할 수 있지만
-   명명된 속성은 포괄적인 용도의 **string 인덱스 시그니처의 타입으로 할당할 수 있어야 합니다.**

![10](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/cf106cc3-24ff-4dfa-a9ce-fe836f79ab84)

위의 에러의 이유는 MoreNarrowNumbers 인터페이스는 string을 `string | undefined`에 할당할 수 있지만
MoreNarrowStrings 인터페이스는 **string 에 할당할 수 없습니다.** (2번째 이유)

<br>

### 7.2.6 중첩 인터페이스

객체 타입이 다른 객체 타입의 속성으로 중첩될 수 있는 것처럼

-   인터페이스 타입도 자체 인터페이스 타입 혹인 객체 타입을 속성으로 가질 수 있습니다.

![11](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/3f07cc41-c75e-4bd2-8725-522fb933ae3e)

<br>

## 7.3 인터페이스 확장

때로는 서로 형태가 비슷한 여러 개의 인터페이스를 가지게 됩니다. <br>
에를 들어, 다른 인터페이스의 모든 멤버를 포함하고 거기에 몇 개의 멤버가 <br> 추가된 인터페이스인 경우 입니다.

타입스크립트는 인터페이스가 다른 인터페이스의 모든 멤버를 복사해서 선언할 수 있는

-   **확장(extend)** 인터페이스를 허용합니다.
-   확장할 인터페이스 이름 뒤에 **extends** 키워드를 추가해서 사용합니다.

다음 예시의 Novella 인터페이스는 Writing을 확장하므로 객체는 최소한 **Novella**의 `pages`와 **Writing**의 `title` 멤버가 모두 있어야 합니다.

![12](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/d227529b-cf49-4fa5-95eb-0a793cc4b098)

<br>

### 7.3.1 재정의된 속성

파생된 인터페이스는 다른 타입으로 속성을 다시 선언해 기본 인터페이스의 속성을 <br> **재정의**하거나 **대체** 할 수 있습니다.

-   WithNullableName 타입은 WithNonNullableName에서 null을 허용하지 않도록 <br> 다시 설정됩니다.
-   그러나 WithNumericName의 name에는 `number | string` 허용되지 않습니다
-   number | string 은 `string | null` 에 할당할 수 없기 때문입니다.

![13](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/47920128-7d1c-4185-8844-bcf22f099082)

<br>

### 7.3.2 다중 인터페이스 확장

타입스크립트의 인터페이스는 **여러 개의 다른 인터페이스**를 확장해서 선언할 수 있습니다.

-   파생 인터페이스 이름에 있는 `extends` 키워드 뒤에 **쉼표**로 인터페이스 이름을 구분해 사용하면 됩니다.

![14](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/5a913620-aa39-462a-9990-9515329e5597)

<br>

## 7.4 인터페이스 병합

인터페이스의 중요한 특징 중 하나는 서로 병합하는 능력 입니다.

-   두 개의 인터페이스가 `동일한 이름`으로 `동일한 스코프`에 선언된 경우
-   선언된 모든 필드를 포함하는 더 큰 인터페이스가 코드에 추가됩니다.

다음 코드는 fromFirst 와 fromSecond라는 두 개의 속성을 갖는 Merged 인터페이스를 선언합니다.

![15](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/3cd3c4cf-cb61-4b1f-ba7e-4d37cb39cec0)

### ⚠️ 일반적인 개발에서는 병합을 자주 사용하지는 않습니다.

인터페이스가 여러 곳에 선언되면 코드를 이해하기 어려워지므로 가능하면 인터페이스 병합을 사용하지 않는 것이 좋습니다.

<br>

✅ 하지만 외부 패키지 또는 내장 전역 인터페이스 보강하는데는 유용함

![16](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/123959a9-69d1-4948-9fc5-d9a0ea99f17d)

<br>

### 7.4.1 이름이 충돌되는 멤버

병합된 인터페이스는 타입이 다른 동일한 이름의 속성을 여러 번 선언할 수 없습니다.

-   속성이 이미 인터페이스에 선언되어 있다면
-   나중에 병합된 인터페이스에도 동일한 타입을 사용해야 합니다.

![17](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/ff55f001-7d73-4e90-b7a6-70b0754615a9)
