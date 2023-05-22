# 여덟번째. 클래스

## 8.1 클래스 메서드

#### 타입스크립트는

- 독립 함수(standalone function)을 이해하는 것과 동일한 방식으로 메서드를 이해함

❗ <span style='background-color: #f5b5b6; color:#000'>**독립함수**</span>(standalone function) ?

- 클래스나 객체에 속하지 않고 독립적으로 정의된 함수로,
  전역 범위에 정의되거나 모듈 내에서 직접 정의될 수 있음
- 독립 함수는 일반적으로 모듈화된 코드의 일부로 사용되며, **다른 함수나 객체에 의존하지 않고 자체적으로 작동**
  ![](https://velog.velcdn.com/images/gazero_/post/1a7a1d0b-6eb7-4f4f-b0e0-1c321f0dc6a6/image.png)
- math.ts파일에 add라는 독립함수를 정의하고, main.ts 파일에서 math.ts 파일에 정의된 독립 함수를 임포트하여 사용할 수 있음

#### 본론으로 들어가서,

- 매개변수 타입에 타입이나 기본값을 지정하지 않으면 any 타입을 기본으로 갖음
- 메서드를 호출하려면 허용 가능한 수의 인수가 필요
- 재귀함수가 아니라면 대부분 반환 타입으로 유추 가능
  ![](https://velog.velcdn.com/images/gazero_/post/ca47d1e8-4fab-44d9-915c-431691f08879/image.png)

#### <span style='background-color: #f9a828; color:#000'>**클래스 생성자(constructor)**</span>는 매개변수와 관련하여 전형적인 클래스 메서드처럼 취급

![](https://velog.velcdn.com/images/gazero_/post/04caeb59-a78a-4eb3-a1d8-86b358721a11/image.png)

❗ <span style='background-color: #f5b5b6; color:#000'>**생성자**</span>(constructor) ?

- 타입스크립트에서 클래스 생성자(constructor)는 클래스의 인스턴스를 초기화하는 메서드
- 클래스 생성자는 클래스 내부에 constructor 키워드로 정의
- 생성자는 클래스로부터 객체를 만들 때 자동으로 호출되며, **인스턴스의 초기 상태를 설정하고 클래스 멤버 변수를 초기화하는 역할**
  ![](https://velog.velcdn.com/images/gazero_/post/b95feda1-0904-4bb9-a23b-63e28d87b9ed/image.png)

```
1. 위의 예제에서 Person 클래스는 name과 age라는 두 개의 멤버 변수를 가지고 있음.
2. 생성자는 name과 age라는 두 개의 매개변수를 받아와서 클래스의 멤버 변수를 초기화.
3. 생성자 내부에서 this.name = name;과 this.age = age;와 같은 구문을 사용하여 매개변수의 값을 멤버 변수에 할당
4. 이후에 const person = new Person('John', 25);라는 코드를 통해 Person 클래스의 인스턴스를 생성
5. 생성자에 'John'과 25라는 값을 전달
6. 생성된 객체는 person.introduce()와 같은 메서드를 호출하여 자신의 멤버 변수 값을 사용
```

## 8.2 클래스 속성

- 타입스크립트에서 클래스의 속성을 읽거나 쓰려면 클래스에 명시적으로 선언이 필요
- 클래스 속성은 인터페이스와 동일한 구문을 사용해 선언
- 클래스 속성 이름 뒤에 선택적으로 타입 애너테이션이 붙음
  ![](https://velog.velcdn.com/images/gazero_/post/f0c65604-e51c-4fdc-937b-6dec12c5469f/image.png)
- 타입스크립트는 생성자 내의 할당에 대해서 그 멤버가 클래스에 존재하는 멤버인지 추론하려 시도하지 않음 !
- destination은 string으로 <span style='background-color: #8c0303; color:#fff'>명시적으로 선언</span>되어 있기 때문에 FieldTrip 클래스 인스턴스에 할당되고 접근이 <span style='background-color: #8c0303; color:#fff'>가능</span>
- 클래스가 nonexistent 속성을 <span style='background-color: #8c0303; color:#fff'>명시적으로 선언</span>선언하지 않았기</span> 때문에 생성자에서 this.nonexistent할당은 <span style='background-color: #8c0303; color:#fff'>명시적으로 선언</span>허용하지 않음</span>

### 8.2.1 함수 속성

#### 자바스크립트에서 클래스의 멤버를 호출 가능한 함수로 선언하는 구문 !

1. 메서드 접근방식
   ![](https://velog.velcdn.com/images/gazero_/post/2d226d48-fb72-4eab-b67a-f865aaa3865e/image.png)
2. 함수인 속성을 선언하는 방식

🚫 주의할 점 !

- myProperty의 형식 선언 부분에서 ()은 함수 형식을 나타내는데, 함수 형식을 나타내려면 파라미터와 반환 타입이 필요
  ![](https://velog.velcdn.com/images/gazero_/post/1dd5eb93-eb60-47a6-9959-a503511b9c13/image.png)
- 또 해당 오류는 클래스의 속성(myProperty)이 초기화되지 않았거나 생성자에서 할당되지 않았기 때문에 발생
  ![](https://velog.velcdn.com/images/gazero_/post/e7099216-017b-4904-aff1-1911823f1cfa/image.png)
- 따라서, myProperty 속성을 초기화하기 위해 생성자에서 값을 할당해야 함!
  ![](https://velog.velcdn.com/images/gazero_/post/c1cc8732-45ca-4ec2-9b57-f9723d3a7245/image.png)

![](https://velog.velcdn.com/images/gazero_/post/873417d9-ee9e-49a9-8a4e-28e75d02fcb5/image.png)

- GazeroPropertyParam 클래스는 매개변수 타입이 (input:boolean) => string인 takesParam 속성을 가짐

### 8.2.2 초기화 검사

- 엄격한 컴파일러 설정이 활성화된 상태에서 타입스크립트는 undefined 타입으로 선언된 각 속성이 생성자에서 하당되었는지 확인
- 엄격한 초기화 검사는 클래스 속성에 값을 할당하지 않는 실수를 예방할 수 있음

![](https://velog.velcdn.com/images/gazero_/post/b2a16a8b-4808-4df5-abd4-b6202e2b47dd/image.png)

- GazeroValue 클래스는 unused 속성에 값을 할당하지 않았으며, 이 경우 타입오류로 인식함

![](https://velog.velcdn.com/images/gazero_/post/c12035f5-3402-4f98-a7b0-3b3e8003e675/image.png)
<참고: 위 예시는 엄격한 타입검사가 수행되어 타입오류를 표시한 상태임>

- 엄격한 초기화 검사가 없다면, undefined 값에 접근할 수 없다고 하더라도 클래스 인스턴스는 undefined 값에 접근할 수 있음
- 따라서 엄격한 초기화 검사가 수행되지 않으면 올바르게 컴파일되지만, 런타임시 문제가 발생
  ![](https://velog.velcdn.com/images/gazero_/post/03e0af51-db49-49ca-8700-461605bbb3a7/image.png)

#### 확실하게 할당된 속성

- 의도적으로 할당하지 않는 경우
- 엄격한 초기화 검사를 적용하면 안되는 속성 뒤에는 <span style='background-color: #f9a828; color:#000'>!를 추가</span>해 검사를 비활성화 하게 함
- 이 경우, <span style='background-color: #f9a828; color:#000'>undefined 값이 할당</span>됨
  ![](https://velog.velcdn.com/images/gazero_/post/df3276cd-2f91-4a47-96d7-1cf64fe8446c/image.png)

### 8.2.3 선택적 속성

- 선언된 속성 이름 뒤에 <span style='background-color: #f9a828; color:#000'>?를 추가</span>해 속성을 옵션으로 선언
- <span style='background-color: #f9a828; color:#000'>|undefined를 포함</span>하는 유니언 타입과 거의 동일하게 작동
- 엄격한 초기화 검사는 생성자에서 선택적 속성을 명시적으로 설정하지 않아도 문제가 되지 않음
  ![](https://velog.velcdn.com/images/gazero_/post/cf08253f-883d-4cee-bc90-c33ada57528c/image.png)

❓참고
![](https://velog.velcdn.com/images/gazero_/post/244fd22e-057d-47b7-b0e9-a199cda7b4d8/image.png)

### 8.2.4 읽기 전용 속성

- 속성 이름 앞에 <span style='background-color: #f9a828; color:#000'>readonly 키워드를 추가</span>해 속성을 읽기 전용으로 선언
- readonly로 선언된 속성은 선언된 위치 또는 생성자에서 초깃값만 할당할 수 있음
- 클래스 내의 메서드를 포함한 다른 모든 위치에서 속성을 읽을 수만 있고, 쓸 수 는 없음
  ![](https://velog.velcdn.com/images/gazero_/post/03038b50-f5ea-4348-910e-0440142d824a/image.png)
- 읽기 전용에는 값을 할당할 수 도 없고,
  ![](https://velog.velcdn.com/images/gazero_/post/09039a65-c1c0-4d5b-903d-1007204c29ad/image.png)
- 객체안에 읽기전용으로 선언된 속성은 받아오지 않음

- 클래스 속성은 처음에는 모두 문자열 리터럴로 선언되므로 둘 중 하나를 string으로 확장하기 위해서는 타입 애너테이션이 필요
  ![](https://velog.velcdn.com/images/gazero_/post/8b9cd45f-5f21-4d4e-88df-fde90460b05b/image.png)
  ![](https://velog.velcdn.com/images/gazero_/post/2d518dc1-8b15-436e-944b-ac004f67e04e/image.png)

```
즉, explicit의 타입은 string이라 생성자에서 다른 값을 할당할 수 있게되지만, implicit은 readonly속성에서 bye형식으로 선언되었기 때문에 생성자에서도 다른 값을 할당할 수 없음
```

🚫 주의

- readonly 속성을 사용하면 무조건 값을 할당할 수 없음 !
- readonly 속성을 사용하면, string으로 확장하기 위한 타입 애너테이션을 설정한 경우 생성자(constructor)에서 확장하기 위한 재할당이 가능함
  ![](https://velog.velcdn.com/images/gazero_/post/ab77fba1-265c-4530-abdb-57c5966162c3/image.png)

```js
console.log(quote.explicit);
//Ok
```

## 8.3 타입으로서의 클래스

- 클래스 선언이 런타임 값과 타입 애너테이션에서 사용할 수 있는 타입을 모두 생성한다
  ![](https://velog.velcdn.com/images/gazero_/post/fe052b9f-1f38-4e20-8e3d-2c26dfeab919/image.png)
- Teacher 클래스의 이름은 teacher 변수에 주석을 다는 데 사용
- teacher 변수에는 Teacher 클래스 자체 인스턴스처럼 Teacher 클래스에 할당할 수 있는 값만 할당해야 함

#### 클래스의 동일한 멤버를 모두 포함하는 모든 객체 타입을 클래스에 할당할 수 있는 것으로 간주

![](https://velog.velcdn.com/images/gazero_/post/cb63836f-ec94-404d-8041-b6151a76265a/image.png)

- withSchoolBus는 SchoolBus 타입의 매개변수를 받음
- 매개변수로 SchoolBus 클래스 인스턴스처럼 타입이 () => string[]인 속성을 가진 모든 객체를 할당할 수 있음

## 8.4 클래스와 인터페이스

- 클래스 <span style='background-color: #f9a828; color:#000'>이름 뒤에 implements</span> 키워드와 인터페이스 이름을 추가함으로써 클래스의 해당 인스턴스가 인터페이스를 준수한다고 선언
- 클래스를 각 인터페이스에 할당할 수 있어야 함을 타입스크립트에 나타냄
  ![](https://velog.velcdn.com/images/gazero_/post/d04144f8-3f6d-489c-95b1-5d2c1f7524d6/image.png)
- Student 클래스는 name 속성과 study 메서드를 포함해 Gazero 인터페이스를 올바르게 구현
- Story에는 name, study가 누락되어 있어 타입 오류가 발생

### 8.4.1 다중 인터페이스 구현

- 클래스에 구현된 인터페이스 목록은 인터페이스 <span style='background-color: #f9a828; color:#000'>이름 사이에 쉼표를 넣고</span>, 개수 제한 없이 인터페이스를 사용할 수 있음
  ![](https://velog.velcdn.com/images/gazero_/post/8b5d6283-69f4-4b63-a8d5-109b0c2c46f5/image.png)
- 클래스에서 Gazero를 구현 하려면 name 속성을 가져와야 하고, Garaded를 구현하려면 grade, Reporter를 구현하려면 report속성을 가져와야 함
  ![](https://velog.velcdn.com/images/gazero_/post/4ab9f2dd-e768-404a-88c3-907e0993c19c/image.png)
- Empty 클래스는 각각의 인터페이스 속성을 제대로 구현하지 못했으므로 세가지 타입 오류가 발생
  ![](https://velog.velcdn.com/images/gazero_/post/a0164d7c-f964-4531-bc37-4902835ad7c4/image.png)
- AsNumber클래스, NotAsNumber클래스 모두 두 인터페이스를 제대로 구현하지 못하고 있음
- 두 인터페이스가 매우 다른 객체 형태를 표현하는 경우에는 동일한 클래스로 구현하지 않아야 함 !

## 8.5 클래스 확장

- 다른 클래스를 확장하거나 하위 클래스를 만드는 개념에 타입 검사를 추가
- 기본 클래스에 선언된 메서드나 속성은 하위 클래스에서 사용 가능
  ![](https://velog.velcdn.com/images/gazero_/post/65d5989f-7cbf-4f47-9924-d7051ee130a9/image.png)

### 8.5.1 할당 가능성 확장

- 하위 클래스도 기본 클래스의 멤버를 상속
- 기본 클래스의 인스턴스가 필요한 모든 곳에서 사용
- 기본 클래스에 하위 클래스가 가지고 있는 모든 멤버가 없으면 더 구체적인 하위 클래스가 필요할 때 사용할 수 없음

![](https://velog.velcdn.com/images/gazero_/post/d24ddb10-e6f5-4600-8d19-182a33cefccf/image.png)

- Lesson 클래스가 기본 클래스, OnLine 클래스가 하위 클래스
- 하위 클래스에서 기본 클래스의 멤버를 상속할 때 constructor에서 supuer(멤버, 멤버 ...)형태로 정의
- 파생된 인스턴스는 기본 클래스 또는 하위 클래스를 충족하는 데 사용할 수 있음

❗ 다형성 !

- **타입으로 상위 클래스를 지정하는 것**은 하위 클래스의 인스턴스를 상위 클래스 타입으로 다룰 수 있음을 의미
- 다형성을 활용한 것으로, 하위 클래스의 인스턴스(OnLine)를 상위 클래스 타입(Lesson)으로 할당
- 상위 클래스인 Lesson은 하위 클래스인 OnLine 모든 기능을 갖고 있기 때문
- 이렇게 하면 lesson 변수는 OnLine 인스턴스를 참조할 수 있으며, 해당 인스턴스의 속성과 메서드에 접근할 수 있음

![](https://velog.velcdn.com/images/gazero_/post/c922ad07-d159-419f-ab5d-629612246b1d/image.png)

- 이는 Lesson 클래스의 인스턴스를 Online 타입인 online 변수에 할당하려고 시도하기 때문에 오류발생
- 하위 클래스의 인스턴스를 상위 클래스 타입으로 다루는 것은 가능하지만, 상위 클래스의 인스턴스를 하위 클래스 타입으로 다루는 것은 허용되지 않음
  ![](https://velog.velcdn.com/images/gazero_/post/96530250-56b9-483a-80c5-7939bf10fff3/image.png)
- 타입스크립트에서 하위 클래스의 인스턴스를 상위 클래스 타입에 할당하는 것은 가능
- 인스턴스 할당(subClass = new LabeledPastGrades())을 통해 subClass 변수는 LabeledPastGrades의 인스턴스를 참조할 수 있음

### 8.5.2 재정의된 생성자

- 자체 생성자가 없는 하위 클래스는 암묵적으로 기본 클래스의 생성자를 사용
- 하위 클래스가 자체 생성자를 선언하면 super 키워드를 통해 기본 클래스 생성자를 호출
- 하위 클래스 생성자는 모든 매개변수를 선언 가능
  ![](https://velog.velcdn.com/images/gazero_/post/a6690442-c283-4bd7-84ec-8744994bd3a3/image.png)
- GradeAnnouncer의 생성자를 올바르게 호출하지 않으면 오류 발생

- 자바스크립트에서 하위 클래스의 생성자 this 또는 super에 접근하기 전에 반드시 기본 클래스의 생성자 호출이 필수 !
- 타입스크립트는 super()를 호출하기 전에 this 또는 super에 접근하려고 하면 타입 오류 발생
  ![](https://velog.velcdn.com/images/gazero_/post/84370836-ea96-481e-bd13-f0a11cfddde5/image.png)

### 8.5.3 재정의된 메서드

- 하위 클래스의 메서드가 기본 클래스의 메서드에 할당될 수 있는 한 하위 클래스는 기본클래스와 동일한 이름으로 새 메서드 선언 가능
  ![](https://velog.velcdn.com/images/gazero_/post/e72d086c-4c62-45aa-b776-89323141ffd4/image.png)
- 동일한 속성에 할당할 수 없음

### 8.5.6 재정의된 속성

- 하위 클래서는 새 타입을 기본 클래스의 타입에 할당할 수 있는 한, 동일한 이름으로 기본 클래스 속성을 명시적으로 다시 선언할 수 있음
- 재정의된 메서드와 마찬가지로 하위 클래스는 기본 클래스와 구조적으로 일치해야 함
  ![](https://velog.velcdn.com/images/gazero_/post/940dd6d7-0ea9-4ee9-b9c1-daba4cb5c235/image.png)
- 하위 클래스는 해당 속성을 더 구체적인 하위 집합으로 만들거나 기본 클래스 속성 타입에서 확장되는 타입으로 만듦

![](https://velog.velcdn.com/images/gazero_/post/76a65b67-6c64-4e3e-aef1-bb8c6952f6a3/image.png)

- 속성의 유니언 타입의 <span style='background-color: #f9a828; color:#000'>허용된 값</span> 집합을 확장할 수 없음
- 확장한다면 하위 클래스 속성은 더 이상 기본 클래스 속성 타입에 할당할 수 없음
  ![](https://velog.velcdn.com/images/gazero_/post/76a65b67-6c64-4e3e-aef1-bb8c6952f6a3/image.png)

## 8.6 추상 클래스

- 추상화하려는 클래스 이름과 메서드 앞에 <span style='background-color: #f9a828; color:#000'>abstract</span>키워드를 추가
- 추상화 기본 클래스에서 메서드의 본문을 제공하는 것을 건너뜀
- 인터페이스와 동일한 방식으로 선언됨
  ![](https://velog.velcdn.com/images/gazero_/post/eec6038f-3652-4a77-8216-5d4137826732/image.png)
- School 클래스와 getStudentTypes 메서드는 abstract로 표시됨
- 따라서 PreSchool, Absence는 getStudentTypes를 구현해야 함

#### 추상클래스 직접 인스턴스화

- 구현이 존재한다고 가정할 수 있는 일부 메서드에 대한 정의가 없으면 불가능
- 추상클래스가 아닌 클래스만 인스턴스화 가능
  ![](https://ifh.cc/g/3qGlOD.png)

## 8.7 멤버 접근성

- 자바스크립트에서 클래스 멤버 이름 앞에 #을 추가해 private 클래스 멤버임을 표시
- private 클래스 멤버는 해당 클래스 인스턴스에서만 접근 가능
- 타입스크립트의 클래스 지원은 자바스크립트 # 프라이버시보다 먼저 만들어 졌음
- 타입스크립트는 private 클래스 멤버를 지원함
- 타입 시스템에만 존재하는 클래스 메서드와 속성에 대해 차이가 있을 수 있음
  ![](https://ifh.cc/g/3QxBAm.png)
- SubClass는 public, protected 멤버에만 접근이 가능

#### 접근성 제한자와 readonly

- 명시적 접근성 키워드를 먼저 적고 + readonly를 적어야 함
  ![](https://ifh.cc/g/PLc6y5.png)

### 8.7.1 정적 필드 제한자

- 타입스크립트는 static 키워드를 단독으로 사용하거나, readonly와 접근성 키워드를 먼저 작성하고, 그다음 static, readonly 키워드가 옴

![](https://ifh.cc/g/7T4rX9.png)

- static 클래스 필드에 대해 readonl용와 접근성 제한자를 사용하면,
- 해당 필드가 해당 클래스 외부에서 접근되거나 수정되는 것을 제한하는 데 유용
