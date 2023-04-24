### 4.1 객체 타입


- {...} 구문으로 객체 리터럴 생성 ⇒ value.멤버 or value['멤버'] 구문으로 값의 속성에 접근


null과 undefined를 제외한 모든 값은 그 값에 대한 실제 타입의 멤버 집합을 가짐


### 4.1.1 객체 타입 선언


- 객체 타입을 명시적으로 선언하기


```typescript
let poetLater: {
	born: number;
    name: string;
};

poetLater = {
	born: 1935,
    name: "Mary Oliver",
}
```


### 4.1.2 별칭 객체 타입


- 객체 타입에 타입 별칭을 할당해 사용하기


```typescript
type Poet = {
	born: number;
    name: string;
};

let poetLater: Poet;

poetLater = {
	born: 1935,
    name: "Sara Teasdale",
};
```


### 4.2 구조적 타이핑


- 정적 시스템이 타입을 검사하는 경우


- 구조적 타입화: 타입을 충족하는 모든 값을 해당 타입의 값으로 사용할 수 있음 → 매개변수나 변수가 특정 객체 타입으로 선언되면 타입 스크립트에 어떤 객체를 사용하든 **해당 속성이 있어야 함**


↔ 자바스크립트는 **덕 타입**으로 런타임에서 사용될 때까지 **객체 타입을 검사하지 않음**


### 4.2.1 사용 검사


- 할당하는 값에는 객체 타입의 필수 속성이 있어야 함 → **모든 속성이 없는 경우** 객체 사용 불가


```typescript
type FirstAndLastNames = {
	first: string;
    last: string;
};

const hasBoth: FirstAndLastNames = { // Ok
	first: "Sarojini",
    last: "Naidu",
};

const hasOnlyOne: FirstAndLastNames = { // Error
	first: "Sappho"
}
```


- 타입이 일치하지 않는 경우에도 오류 발생


### 4.2.2 초과 속성 검사


- 초깃값에 객체 타입에서 정의된 것보다 많은 필드가 존재하는 경우 타입 오류 발생


```typescript
type Poet = {
	born: number;
    name: string;
};

const poetMatch: Poet = { // Ok
	born: 1928,
    name: "Maya Angelou"
};

const extraProperty: Poet = { // Error
	activity: "walking",
    born: 1935,
    name: "Mary Oliver"
};
```


### 4.2.3 중첩된 객체 타입


- 객체 타입은 중첩된 객체 타입을 나타낼 수 있음

```typescript
type Poem = {
	author: {
    	firstName: string;
        lastName: string;
    };
    name: string;
};

const poemMatch: Poem = { // Ok
	author: {
    	firstName: "Sylvia",
        lastName: "Plath",
    },
    name: "Lady Lazarus",
};

const poemMismatch: Poem = { // Error
	author: {
    	name: "Sylvia Plath",
    };
    name: "Tulips",
};
```

- 타입 작성 시 자체 별칭 객체 타입으로 추출하는 방법


```typescript
type Author = {
	firstName: string;
    lastName: string;
};

type Poem = {
	author: Author;
    name: string;
};

const poemMismatch: Poem = { // Error
	author: {
    	name: "Sylvia Plath",
    },
    name: "Tulips",
};
```


### 4.2.4 선택적 속성 ( ?: )


- 선택적 속성은 제공하거나 생략할 수 있음


```typescript
type Book = {
    author?: string;
    pages: number;
};

const ok: Book = {
    author: "Rita Dove",
    pages: 80,
};

const missing1: Book = { // Ok
    pages: 80,
};

const missing2: Book = { // Error
    author: "Rita Dove"
};
```


### 4.3 객체 타입 유니언


### 4.3.1 유추된 객체 타입 유니언


- 변수에 여러 객체 타입 중 하나가 될 수 있는 초깃값이 주어지면 해당 타입을 객체 타입 유니언으로 유추하고, 가능한 각 객체 타입을 구성하고 있는 요소를 모두 가질 수 있음


```typescript
const poem = Math.random() > 0.5
	? { name: "The Double Image", pages: 7 }
    : { name: "Her Kind", rhymes: true };
    
 // 타입: { name: string; pages: number; rhymes?: undefined; }
 //     | { name: string; pages?: undefined; rhymes: boolean; }
 
 poem.name; // string
 poem.pages; // number | undefined
 poem.rhymes; // boolean | undefined
```


### 4.3.2 명시된 객체 타입 유니언


- 객체 타입의 조합을 명시하면 객체 타입을 명확히 정의해 더 많이 제어할 수 있음 → 모든 유니언 타입에 존재하는 속성에 대한 접근만 허용함


```typescript
type PoemWithPages = {
	 name: string;
     pages: number;
};

type PoemWithRhymes = {
	name: string;
    rhymes: boolean;
};

type Poem = PoemWithPages | PoemWithRhymes;

const poem: Poem = Math.random() > 0.5
	? { name: "The Double Image", pages: 7 }
    : { name: "Her Kind", rhymes: true };
    
poem.name; // Ok
poem.pages; // Error
```


**⇒ 잠재적으로 존재하지 않는 객체의 멤버에 대한 접근을 제한해 코드의 안전을 지킴**


### 4.3.3 객체 타입 내로잉


- 코드에서 객체의 형태를 확인하고 타입 내로잉이 객체에 적용됨


```typescript
if ("pages" in poem) {
	poem.pages; // poem은 PoemWithPages로 좁혀짐
} else {
	poem.rhymes; // poem은 PoemWithRhymes로 좁혀짐
}
```


### 4.3.4 판별된 유니언


- 판별된 유니언: 객체의 속성이 객체의 형태를 나타내도록 하는 형태

- 판별값: 객체의 타입을 가리키는 속성


**→ 판별 속성을 사용해 타입 내로잉을 수행함**


```typescript
type PoemWithPages = {
	 name: string;
     pages: number;
     type: 'pages';
};

type PoemWithRhymes = {
	name: string;
    rhymes: boolean;
    type: 'rhymes';
};

type poem = Poem = PoemWithPages | PoemWithRhymes;

const poem: Poem = Math.random() > 0.5
	? { name: "The Double Image", pages: 7, type: "pages" }
    : { name: "Her Kind", rhymes: true, type: ""rhymes };
    
if (poem.type === "pages") {
	console.log('It's got pages: ${poem.pages}');
} else {
	console.log('It's rhymes: ${poem.rhymes}');
}

poem.type; // 'pages' | 'rhymes'

poem.pages; // Error
```


### 4.4 교차 타입( & )


- 여러 기존 객체 타입을 별칭 객체 타입으로 **결합**해 새로운 타입을 생성


```typescript
type Artwork = {
	genre: string;
    name: string;
};

type Writing = {
	pages: number;
    name: string;
};

type WrittenArt = Artwork & Writing; // { genre: string; name: string; pages: number; }
```


### 4.4.1 교차 타입의 위험성


- 가능한 코드를 간결하게 유지해 혼동 방지가 필요함


① 긴 할당 가능성 오류: 타입이 복잡할 수록 타입 검사기의 메시지를 이해하기 어려워짐

② never: 두 개의 원시타입을 함께 시도했을 경우 → bottom 타입 or empty 타입 = 불가능한 상태

> bottom 타입: 값을 가질 수 없고 참조할 수 없는 타입