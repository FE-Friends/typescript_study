## 8.클래스

들어가기 전에 잠깐 복습할 겸 클래스에 대해 짧게 보고 넘어가겠습니다.

<br>

### 자바스크립트에서 클래스란 ?

클래스는 객체를 생성하기 위한 템플릿이며, 해당 클래스로부터 생성된 개별 객체는 <br>
클래스에 정의된 **속성**과 **메서드**를 상속 받습니다.

<br>

### 클래스를 정의하는 방법

`class` 키워드를 사용하며, 클래스 이름은 대문자로 시작하는 것이 관례입니다.

![1](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/92694a27-78a5-492d-b310-5def1cd22a79)

위 예제에서 MyClass는 클래스로 정의되었습니다.

-   constructor라는 특별한 메서드는 객체를 초기화하는 역할을 합니다.
-   `name` 속성을 인자로 받아 객체의 **속성**으로 설정합니다.
-   `sayHello`는 MyClass 클래스의 **메서드**로 정의되었습니다.
-   이 메서드는 console.log를 통해 name 속성과 함께 인사말을 출력합니다.

클래스를 기반으로 객체를 생성하기 위해서는 `new 키워드`를 사용해야 합니다. <br> 위 예제에서 myObject는 MyClass의 인스턴스로 생성된 객체입니다

이제 클래스에 대한 타입스크립트에 대해 알아보겠습니다.

<br>

## 8.1 클래스 메서드

타입스크립트는 독립 함수를 이해하는 것과 동일한 방식으로 **메서드**를 이해합니다.

> 자바스크립트에서 '메서드'는 객체에 속한 함수를 가리킵니다.

<br>

매개변수 타입에 타입이나 기본 값을 지정하지 않은 경우

-   `any` 타입을 기본으로 가집니다.

![2](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/71654079-029d-4af6-8940-77ef21780fcd)

<br>

## 8.2 클래스 속성

타입스크립트에서 클래스의 속성을 읽거나 쓰려면 **명시적으로 선언**해야 합니다.

-   클래스 속성 이름 뒤에는 선택적으로 **타입 애너테이션**이 붙습니다.
-   인스턴스에 존재하지 않는 멤버에 접근하려고 시도하면 타입 오류가 발생 합니다.

![3](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/6b9143df-ac77-497a-afe2-a9182e904e63)

-   destination은 string 타입으로 명시적 선언되어 있어 FieldTrip 클래스 인스턴스에 <br> 할당되고 접근할 수 있습니다.

<br>

### 8.2.1 함수 속성

자바스크립트는 클래스의 멤버를 호출 가능한 삼수로 선언하는 두 가지 구문이 있습니다.

앞서 `myFunction(){}`과 같이 멤버 이름 뒤에 괄호를 붙이는 메서드 접근 방식을 살펴 봤습니다.

-   메서드 접근 방식은 함수를 클래스 프로토타입에 할당하므로
-   모든 클래스 인스턴스는 동일한 함수 정의를 사용합니다.

다음 WithMethod 클래스는 모든 인스턴스가 참조할 수 있는 myMethod 메서드를 선언합니다.

![4](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/45684abc-b588-45aa-adf4-9a186189a07f)

<br>

값이 함수인 속성을 선언하는 방법도 있습니다.

-   클래스의 인스턴스 당 새로운 함수가 생성되며
-   항상 클래스 인스턴스를 가리켜야 하는 화살표 함수에서 `this` 스코프를 사용하면 <br> 새로운 함수를 생성하는 시간과 메모리 비용 측면에서 유용할 수 있습니다.

다음 WithProperty 클래스는 이름이 myProperty인 단일 속성을 포함하여 <br> 각 클래스 인스턴스에 대해 다시 생성되는 `() => void` 타입 입니다.

![5](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/a67f42d2-49bc-4c32-84f6-0fc3ca2c50e6)

<br>

### 8.2.2 초기화 검사

엄격한 컴파일러 설정이 활성화된 상태에서 타입스크립트는 `undefined` 타입으로 선언된 각 속성이 <br>
생성자에서 할당 되었는지를 확인 합니다.

![6](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/7a20e6ec-7852-42e6-8613-d929205b789d)

에러를 수정하려면 아래와 같이 `unused` 필드에 초기 값을 할당하거나 생성자에서 값을 할당해야 합니다.

![7](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/22ba1423-d841-4221-9a95-f34b3c4dbb86)

<br>

### 확실하게 할당된 속성

엄격한 초기화 검사가 유용한 경우가 대부분이지만, 클래스 생성자 다음에 <br>
클래스 속성을 의도적으로 할당하지 않는 경우가 있을 수도 있습니다.

-   초기화 검사를 하고 싶지 않은 경우 `!` 를 추가해 검사를 비활성화하도록 설정 합니다.
-   이렇게 되면 속성이 처음 사용되기 전 `undefined` 값이 할당됩니다.

![8](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/4d35077f-17f7-44fc-b6e4-88e10038dd88)

<br>

### 8.2.3 선택적 속성

선언된 속성 이름 뒤에 `?` 를 추가해 속성을 옵션으로 선언 합니다.

-   선택적 속성은 ` | undefined` 를 포함하는 유니언 타입과 거의 동일하게 작동 합니다.

![9](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/6238421e-14b6-4c4e-accf-993c895b8dde)

<br>

#### 8.2.4 읽기 전용 속성

`readonly` 키워드를 추가해 속성을 읽기 전용으로 선언합니다.

-   타입 시스템에만 존재하며 자바스크립트로 컴파일 할 때 삭제됩니다.
-   **1. 선언된 위치** 또는 **2. 생성자**에서 초기값만 할당 할 수 있습니다.

![10](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/7aebc75b-5ae8-423b-a105-24f55323b9e4)

<br>

## 8.3 타입으로서의 클래스

타입 시스템에서 클래스는 클래스 선언이

1. 런타임 값(클래스 자체)과
2. 타입 애너테이션에서 사용할 수 있는 타입을 모두 생성 합니다.

해당 클래스의 인스턴스가 아니더라도 모든 멤버와 메서드를 갖고 있다면 할당할 수 있습니다.

-   타입스크립트의 구조적 타이핑으로 선언되는 방식이 아니라
-   객체의 형태만을 고려하기 때문

![11](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/efadedbd-8d23-4583-a5be-f765bf5b9fa9)

<br>

## 8.4 클래스와 인터페이스

클래스 이름 뒤에 `implements` 키워드와 인터페이스 이름을 추가함으로써

-   클래스의 해당 인스턴스가 인터페이스를 준수한다고 선언할 수 있습니다.

![12](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/38e65e70-b6ef-4339-8690-9bf9c94d85d5)

-   Student 클래스는 name 속성과 study 메서드를 포함해 <br> Learner 인터페이스를 올바르게 구현 했지만
-   Slaker에는 study가 누락되어 타입 오류가 발생합니다.

<br>

### 8.4.1 다중 인터페이스 구현

`implements` 뒤에 `,`를 이용해서 개수 제한 없이 인터페이스를 등록할 수 있습니다.

-   해당 클래스는 등록된 모든 인터페이스를 준수해야 합니다.

![13](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/2de8498e-0c8a-41ff-bd64-1cdd8bde8aa9)

-   Empty 클래스는 Graded와 Reporter 인터페이스를 제대로 구현하지 못했으므로 두 가지 타입오류가 발생 합니다.

> 만약 인터페이스끼리 중복된 부분이 있고 두 인터페이스가 매우 다른 객체 형태를 표현하는 경우 해당 클래스는 정의할 수 없습니다.

<br>

## 8.5 클래스 확장

다른 클래스를 확장하거나 하위 클래스를 만드는 자바스크립트 개념에 타입 검사를 추가합니다.

![14](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/2b9cca62-8bb0-40f7-90dd-cc02728f8e56)

<br>

### 8.5.1 할당 가능성 확장

하위 클래스에서 기본 클래스의 멤버나 메서드를 사용할 수 있습니다.

![15](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/890b002a-913a-4315-8409-0afa3ba1ccd9)

구조적 타이핑에 따라 기본 클래스의 타입이 **하위 클래스의 모든 맴버가 동일하게 존재하는 경우** 기본 클래스의 인스턴스를 하위 클래스 대신 사용할 수 있습니다.

<br>

### 8.5.2 재정의된 생성자

하위 클래스는 자체 생성자를 정의할 필요가 없습니다.

-   자체 생성자가 없는 하위 생성자는 암묵적으로 기본 클래스의 생성자를 사용합니다.
-   자바스크립트에서 하위 클래스가 자체 생성자를 선언하면 `super` 키워드를 통해 기본 클래스 생성자를 호출해야 합니다.

![16](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/14bf5feb-f7ba-4dae-aad7-ffb513edc3c2)

Brand 클래스는 super 생성자를 호출하고 color 매개변수를 전달하여 Colors 클래스의 생성자를 적절하게 재정의합니다.

<br>

### 8.5.3 재정의된 메서드 (Overriding)

하위 클래스는 기본 클래스의 메서드를 재정의 할 수 있습니다.

-   기본 클래스를 사용하는 모든 곳에 하위 클래스를 사용할 수 있으므로
-   새 메서드의 기본 타입도 기본 메서드 대신 사용할 수 있어야 합니다.

![17](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/e68d87e9-e7b2-4361-9652-cabbe758b8f7)

Colors 클래스에는 색상을 설명하는 문자열을 반환하는 getColorInfo() 메서드가 있습니다.

-   Brand 클래스는 Colors를 확장하고 반환된 문자열에 브랜드 정보를 포함하는 자체 구현으로 getColorInfo() 메서드를 재정의합니다.
-   이제 Brand 클래스의 인스턴스를 만들고 getColorInfo() 메서드를 호출하면
-   Colors 클래스 대신 Brand 클래스에서 재정의된 메서드가 호출됩니다.

<br>

### 8.5.4 재정의된 속성

속성을 다시 선언하는 대부분의 하위 클래스는 해당 속성을

-   유니언 타입의 더 구체적인 하위 집합으로 만들거나
-   기본 클래스 속성 타입에서 확장되는 타입으로 만듭니다.

![18](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/488ca528-ad10-47ec-89c2-603c147c05e2)

<br>

## 8.6 추상 클래스

일부 메서드의 구현을 하지 않고, 대신 하위 클래스가 해당 메서드를 제공할 것을 예상하여<br>
기본 클래스를 만드는 방법이 유용할 수 있습니다.

-   추상화하려는 클래스 이름과 메서드 앞에 `abstract` 키워드를 추가합니다.
-   이러한 추상화 메서드 선언은 추상화 기본 클래스에서 메서드의 본문을 제공하는 것을 건너뛰고
-   대신 인터페이스와 동일한 방식으로 선언됩니다.

![19](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/b2871cf9-2845-41a4-b7f6-fc4251ea9343)

<br>

## 8.7 멤버 접근성

타입스크립에는 접근 제한자가 존재 합니다.

자바스크립트에도 `#`이라는 private한 접근 제한자가 존재하지만 <br> private와 #은 비슷한 역할을 하지만 미묘한 차이가 존재 합니다.

-   `#`은 컴파일 후에도 사라지지 않는 자바스크립트 고유의 문법
-   `private`은 컴파일 후에 사라지는 타입스크립트 고유의 문법

<br>

접근 제한자 설명

-   `public` : 어디서나 누구나 접근 가능
-   `protected` : 클래스 내부 또는 하위 클래스에서만 접근 가능
-   `private` : 클래스 내부에서만 접근 가능

![20](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/6933bd53-30f6-4cd7-9be3-2643571ddd7c)

<br>

### 8.7.1 정적 필드 제한자

자바스크립트는 `static` 키워드를 사용해 **클래스 자체에 멤버를 선언** 합니다. <br>
타입스크립트는 `static` 키워드를 단독으로 사용하거나 `readonly`와 접근성 키워드를 함께 사용할 수 있습니다.

-   함께 사용할 경우 `접근성 키워드 > static > readonly` 키워드가 옵니다.
-   static 클래스 필드에 대해 readonly와 접근성 제한자를 사용하면 해당 클래스 외부에서 접근되거나 수정되는 것을 제한하는데 유용

![21](https://github.com/Choi-HyunHo/hyunho-gatsby-blog/assets/87301268/89a15105-c903-47ae-a56d-a75ebaa68017)
