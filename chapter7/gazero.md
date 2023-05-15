# 일곱번째. 인터페이스

## 인터페이스란?

> 연관된 이름으로 객체 형태를 설명하는 또 다른 방법

- 별칭으로 된 객체 타입과 여러면에서 유사
- 일반적으로 더 읽기 쉬운 오류 메시지
- 더 빠른 컴파일러 성능
- 클래스와의 더 나은 상호 운용성을 위해 선호됨

## 7.1 타입 별칭 vs. 인터페이스

![](https://velog.velcdn.com/images/gazero_/post/aac3cf8c-a054-4b15-87bc-b54a55562d8f/image.png)

### 공통점

- 할당 가능성 검사와 오류메시지는 거의 동일

### 차이점

- 인터페이스는 속성 증가를 위해 병합 할 수 있음
- 인터페이스는 클래스가 선언된 구조의 타입을 확인하는데 사용
- 인터페이스에서 타입스크립트 타입 검사기가 더 빨리 작동(인터페이스는 타입 별칭이 하는 것처럼 새로운 객체 리터럴의 동적인 복사 붙여넣기보다 내부적으로 더 쉽게 캐시할 수 있는 명명된 타입을 선언)
- 인터페이스는 이름 없는 객체 리터럴의 별칭이 아닌 이름 있는 객체로 간주(어려운 특이 케이스에서 나타나는 오류 메시지를 좀 더 쉽게 읽을 수 있음)

### **_결과적으로_**

- 인터페이스는 사용하는 것이 좋음
- 타입 별칭의 유니언 타입과 같은 기능이 필요할 때까지는 인터페이스를 사용해라 !

## 7.2 속성 타입

### 7.2.1 선택적 속성

- 객체 타입과 마찬가지로 모든 객체가 필수적으로 인터페이스 속성을 가질 필요는 없음
- 타입 애너테이션 : 앞에 ?를 사용해 인터페이스의 속성이 선택적 속성임을 나타낼 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/58c9ec61-ee7e-446b-bbf5-869783c4e3f9/image.png)
- gazero 인터페이스를 사용하는 객체애 선택적 속성은 제공되거나(string으로 혹은 undefined로 제공) 생략할 수 있음

### 7.2.2 읽기 전용 속성

#### 언제쓸까?

- 인터페이스에 정의된 객체의 속성을 재할당하지 못하도록 인터페이스 사용자를 차단하고 싶을때
- 속성 이름 앞에 readonly키워드를 추가해 다른 값으로 설정될 수 없음을 나타냄
- readonly 제한자는 타입 시스켐에만 존재 & 인터페이스에서만 사용
- readonly속성은 평소대로 읽을 수 있지만, 새로운 값으로 재할당하지 못함
  ![](https://velog.velcdn.com/images/gazero_/post/5503f28f-b4a2-42d2-9bce-2f8b67ee7c2c/image.png)
- Gazero 인터페이스의 name 속성에 접근하면 string을 반환
- name에 새로운 값을 할당하면 오류 발생

#### writeable 쓰기 가능한 속성으로는 사용할 수 없을까? 있음 !

![](https://velog.velcdn.com/images/gazero_/post/082c10aa-dccb-4004-828e-516448023019/image.png)

- name 속성의 부모 객체는 함수 내부에서 name으로 명시적으로 사용되지 않았기 때문에 함수 밖에서 속성을 수정할 수 있음
- 따라서, 쓰기 가능한 속성을 readonly 속성에 할당할 수 있음
- gazerous는 Gazero를 사용할 수 있음
- 즉, 쓰기 가능한 속성은 readonly 속성이 필요한 모든 위치에서 읽을 수 있음

cf. gazerous의 더 구체적인 버전인 Gazero를 읽음
![](https://velog.velcdn.com/images/gazero_/post/e7fc986e-68d8-4b0b-bdb1-47e7359f7cdb/image.png)

- 명시적 타입 애너테이션인 :Gazeo로 변수 gazerous를 선언하면 타입스크립트 name 속성이 readonly라고 가르킴
  ![](https://velog.velcdn.com/images/gazero_/post/e7dda409-6653-4f2b-a59b-0307e49546d2/image.png)

### 7.2.3 함수와 메서드

#### 인터페이스 멤버를 함수로 선언하는 방법

- 메서드 구문

인터페이스 멤버를

```js
 member(): void
```

와 같이 객체의 멤버로 호출되는 함수로 선언

- 속성 구문
  인터페이스 멤버를

```js
member: () => void
```

와 같이 독립 함수와 동일하게 선언

![](https://velog.velcdn.com/images/gazero_/post/22485fe7-119e-41e2-920f-1332771f7e00/image.png)

- method와 property 멤버는 둘 다 매개변수 없이 호출되어 string타입을 반환

#### 선택적 속성사용

![](https://velog.velcdn.com/images/gazero_/post/dd2269f0-f0ab-4435-aee2-d42fee2b3f14/image.png)

- string 타입으로 반환되거나
- 정의되지 않을 수 있음을 의미
- 정의되지 않을 수 있는 개체는 호출할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/f8324ba8-64fd-4c6e-bb19-0ba93ab280c2/image.png)
- 메서드는 readonly로 선언할 수 없지만 속성은 가능

### 7.2.4 호출 시그니처

- 인터페이스와 객체 타입은 호출 시그니처로 선언할 수 있음
- 호출 시그니처는 함수처럼 호출하는 방식에 대한 타입 시스템
- 호출 시그니처가 선언한 방식으로 호출되는 값만 인터페이스에 할당할 수 있음
- 즉, 할당 가능한 매개변수와 반환 타입을 가진 함수임
- 형식: 함수타입과 비슷하지만 콜론 대신 화살표로 표시
  ![](https://velog.velcdn.com/images/gazero_/post/39301183-3057-466f-95aa-1aad7e679897/image.png)
  ![](https://velog.velcdn.com/images/gazero_/post/e41fa921-646b-4616-8355-31d29820c2f6/image.png)
- 사용자 정의 속성을 추가로 갖는 함수를 설명하는 데 사용
- 타입스크립트는 함수 선언에 추가된 속성을 해당 함수 선언의 타입에 추가하는 것으로 인식

#### 인터페이스 할당의 문제

![](https://velog.velcdn.com/images/gazero_/post/ca0b3254-2140-4798-b4a0-88ea60dafb79/image.png)

### 7.2.5 인덱스 시그니처

- 인덱스 시그니처 구문을 제공해 인터페이스의 객체가 임의의 키를 받고, 해당 키 아래의 특정 타입을 반환할 수 있음을 나타냄
- 인덱스 시그니처는 일반 속성 정의와 유사하지만 키 다음에 타입이 있고 {[i: string]: ...}과 같이 배열의 대괄호를 갖음
  ![](https://velog.velcdn.com/images/gazero_/post/a4f06242-ea3b-47c0-a27f-de9648e23ef4/image.png)
- GazeroFunctionCount 인터페이스는 number 값을 갖는 모든 string키를 허용하는 것으로 선언
- 이런 타입의 객체는 값이 number면 string키가 아닌 그 어떤 키도 바인딩 할 수 없음
- 인덱스 시그니처는 객체에 값을 할당할 때 편리함
- 하지만 타입 안정성을 완벽하게 보장하지 않음
- 인덱스 시그니처는 객체가 어떤 속성에 접근하든 값을 반환해야 함
  ![](https://velog.velcdn.com/images/gazero_/post/6fa21613-1d9c-428c-96e5-2176076945a9/image.png)

```
1. WordGazero 인터페이스는 Date 값을 갖는 모든 string 키를 허용하는 것으로 선언
2. 객체는 값이 Date면 string키가 아닌 그 어떤 키도 바인딩 할 수 없음
3. gazeroDate 값은 Date 타입으로 Gayoung을 안전하게 반환하지만
4. 타입스크립트는 Beloved가 정의되지 않았음에도 불구하고 정의되었다고 생각하도록 속임
```

- 따라서 키/값 쌍을 저장하려고 하는데 키를 미리 알 수 없다면 Map을 사용하는 것이 안전
- get 메서드는 항상 키가 존재하지 않음을 나타내기 위해 |undefined 타입을 반환

#### 속성과 인덱스 시그니처 혼합

- 인터페이스는 명시적으로 명명된 속성과 포괄적인 용도의 string 인덱스 시그니처를 한 번에 포함할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/8cdb5f3f-d27d-4444-a6db-4aa6e2d2025a/image.png)
- 인덱스시그니처: interface Gazero는 모든 속성을 number타입으로 선언 + 속성: Gayoung 속성이 존재해야 함
  ![](https://velog.velcdn.com/images/gazero_/post/1b989332-9684-4322-8bcc-a3c5409949c6/image.png)
- 또한, 속성 값의 초깃값을 지정해두면 Gazero를 사용하는 모든 객체의 Gayoung 속성은 반드시 지정해둔 값을 사용해야 함

#### 숫자 인덱스 시그니처

- 인덱스 시그니처는 키로 string 대신 number 타입을 사용할 수 있지만, 명명된 속성은 그 타입을 포괄적인 용도의 string 인덱스 시그니처의 타입으로 할당할 수 있어야 함
  ![](https://velog.velcdn.com/images/gazero_/post/48f0ab52-f480-4845-ac15-e2ff804cee1b/image.png)
- Gazero 인터페이스는 string을 string|undefined에 할당할 수 있지만, GazeroMore 인터페이스는 string|undefined를 string에 할당할 수 없음

### 7.2.6 중첩 인터페이스

- 인터페이스 타입도 자체 인터페이스 타입 혹은 객체 타입을 속성으로 가질 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/e232bb88-aeab-45bb-8a7b-54f29be6bdad/image.png)
- Gazero 인터페이스는 인라인 객체 타입인 author 속성과 Setting 인터페이스인 setting속성을 포함

## 7.3 인터페이스 확장

> 서로 형태가 비슷한 여러 개의 인터페이스를 갖게 될 수 있음

- 타입스크립트는 인터페이스가 다른 인터페이스의 모든 멤버를 복사해서 선언할 수 잇는 확장된 인터페이스를 허용
- 확장할 인터페이스의 이름 뒤에 extends 키워드를 추가해서 다른 인터페이스를 확장한 인터페이스라는 걸 표시
- 파생 인터페이스를 준수하는 모든 객체가 기본 인터페이스의 모든 멤버도 가져야 한다는 것을 타입스크립트에 알려줌
  ![](https://velog.velcdn.com/images/gazero_/post/e52a19e8-ef8f-47e6-9541-b92dec1d17dd/image.png)
- Fine 인터페이스는 Gazero를 확장하므로 객체는 최소한 Fine의 year와 Gazero의 name 멤버가 모두 존재해야 함

### 7.3.1 재정의된 속성

- 파생 인터페이스는 다른 타입으로 속성을 다시 선언해 기본 인터페이스의 속성을 재정의 하거나 대체할 수 있음
- 속성을 재선언하는 대부분의 파생 인터페이스는 해당 속성을 유니언 타입의 더 구체적인 하위 집합으로 만들거나 속성을 기본 인터페이스의 타입에서 확장된 타입으로 만들기 위해 사용
  ![](https://velog.velcdn.com/images/gazero_/post/5222f6af-b875-48f6-8add-4980378c65c6/image.png)
- GazeroNull 타입은 GazeroNonNull에서 null을 허용하지 않도록 재설정됨
- GazeroNumeric의 name에는 number|string이 허용되지 않음(number|string은 string|null에 할당할 수 없기 때문)

### 7.3.2 다중 인터페이스 확장

- 인터페이스는 여러 개의 다른 인터페이스를 확장해서 선언할 수 있음
- 파생 인터페이스 이름에 있는 extends 키워드 뒤에 쉼표로 인터페이스 이름을 구분해 사용함
  ![](https://velog.velcdn.com/images/gazero_/post/ef9365ba-080a-491a-9eff-29755dbdb90a/image.png)

## 7.4 인터페이스 병합

- 인터페이스의 중요한 특징 ! <span style='background-color: #DAB4B8; color:#000'>"병합"</span>
- 두 개의 인터페이스가 동일한 이름으로 동일한 스코프에 선언된 경우, 선언된 모든 필드를 포함하는 더 큰 인터페이스가 코드에 추가
  ![](https://velog.velcdn.com/images/gazero_/post/cb2f8a52-b573-4b0f-8bf9-2fcb91382b97/image.png)
- 인터페이스 병합은 자주 사용되지 않음(코드를 이해하기가 어려워 질 수 있음)
- 하지만, window 내장된 전역 인터페이스를 보강하는데 유리함

```js
interface Window {
  environment: string;
}

window.environment;
//string 타입으로 !
```

### 7.4.1 이름이 충돌되는 멤버

- 병합된 인터페이스는 타입이 다른 동일한 이름의 속성을 여러 번 선언 불가
- 속성이 이미 인터페이스에 선언되어 있다면, 추후 병합된 인터페이스에서도 동일한 타입을 사용해야 함
  ![](https://velog.velcdn.com/images/gazero_/post/1558b861-ae9d-4bf1-a164-bb566e07de5b/image.png)
- 하지만 동일한 이름과 다른 시그니처를 가진 <span style='background-color: #DAB4B8; color:#000'>메서드</span>는 정의할 수 있음 = 함수 오버로드 발생
  ![](https://velog.velcdn.com/images/gazero_/post/631f15a2-c887-4865-88ff-9b067e033e83/image.png)
