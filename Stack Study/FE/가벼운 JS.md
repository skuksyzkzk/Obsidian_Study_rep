### js공부 

타입

# 기본형 
> 기존값 수정이 아니라 새로운값을 만들어 내는 것 수정시 
> 또한 메모리에 저장이 아니라 그냥 그 값을 저장한다고 생각하면 된다 .

# 참조형 
>저장시 해당 값의 메모리 주소를 저장한다. 
>배열을 저장하면 메모리 주소가 저장되는 것 
>메모리안에 있는 배열의 내용이 수정이 그래서 되는 것 

```js
const arr = ['1','2'];
arr.push('3');// 에러 발생하지 않는다 
```

Boolean 
비어있는 문자열 null,undefined,숫자 0은 false로 간주 

## null
> null은 확실하게 비어있음을 표현하기 위한 것 undefined하곤 다르다 

Undefined 
할당되지않는 값 접근시 언디파인드로 뜬다

Null
의도적으로 변수에 값이 없다는 것을 명시할 경우 사용 

Var 이걸로 변수 선언 

### 객체타입
키와 값으로 이루어져있다.
var obj = { a: 1,b : 2} 

### 배열,객체
#### map()
>map((item)=> {})
>기존 배열을 변환하는게 아니라 새로운 배열을 반환한다.
>item에 접근해서 여러가지 가능한 것 

> 또한 자바스크립트 객체를 반환할수도 있다 

```js
const edit = hobbies.map((item) => ({text : item}));
```

자바스크립트 객체를 변환 시킬 때는 ()괄호로 감싸야한다.
#### .findIndex()
> findIndex( (item) => { }) 중괄호 안에 조건식이 true 인 인덱스를 반환한다 item에는 배열의 원소 하나 씩 매칭 

배열 
- var arr = [];
- length다 가능 길이
- typeof 하면 object로 나온다 
- var arr = New Array(1,2); 하면 1과 2가 들어간채로 배열 생성된다.
- 요소의 추가와 삭제 
- 1. delete arr[1];이렇게하면 삭제되고 그 빈자리는 유지가 된다.
- 2. arr.splice(3,1); 이거는 인덱스 3번째 자리부터 1개의 데이터를 삭제 이러면 빈자리 없이 아예 사라짐 

객체 
``` 
var person = {
		name:"김성엽",
		gender: 'male',
}
```
- 객체를 생성할 때 var person = new Object();
- 이렇게 생성하고 추가할경우에 person['area'] = 'Seoul';이렇게 추가가능 또한 
- for문으로 출력 하고자 할 경우에는 
```
for (var prop in person) {
	console.log(prop +','+person[prop]);
}
```
- 이렇게 하게되면 prop에는 key값인 name,gender,area가 들어가게 된다.뭔지알잖아 

---

### 연산자

단항 산술 연산자 

```
var x = 5, result = 0; 

result = x++;
console.log(result,x)//5,6 x를 쓰고 그 다음 x를 더한다 
result = ++x;
//7,7 먼저 더한 값을 x에 넣고 그 값을 result에 대입하기에 같아지는 것 
```

문자열 연결 연산자 

'1'+2 = '12' , '1'+'2' = '12 ' 문자열이 있으면 더했을 때 둘다 무조건 문자열 

#### 비교 연산자 

5 == '5' true 
5 === '5' false  === 는 값뿐만 아니라 타입도 같아야  true

#### 삼항 조건 연산자

> 조건식 ? 조건식이 true일때 반환값 : 조건식이 false일때 반환값 

``` 
var x = 4;
var result = x % 2 ? '짝' : '홀';
//당연히 짝이 반환된다 true이기 때문에 
```


---
### 블록문

```
{
 var foo = 10;
}
```

### 조건문

#### if else 문

```
if(num > 0) {

}
else if (num >1) {

}
else {

}
```

#### Switch 문도 존재함 

### 반복문 

``` 
for (var i=0;i<2;i++){
	//참일 경우 실행문 
}

while ( count <3 ){

}
```

### let & const  VS var 

var는 구시대
- 블록스코프가 없고 함수 스코프 아니면 전역 스코프 이다.
- 블록 기준으로 스코프가 안생기기 때문에 블록 밖에서도 접근이 가능하다.
- 또한 중복 선언이 가능하다.

```
var a = 1;
var a = 2;
console.log(a);// 2가 출력된다 이렇게 중복선언이 가능.
```
const 는 상수 재정의 안된다
let 
- 이 녀석은 중복 선언이 안되고, 블록스코프도 가능하다.
- 기본은 const쓰기 

### 스코프 

```
{
var b = 1 ;
let c = 2;
}

console.log(b);//1 함수스코프 변수는 블록 밖에서도 접근 가능하다 
console.log(c);//error 왜냐고? let은 블록스코프 변수가능해서 블록 밖에서 접근이 안돼요.

```

### 호이스팅 

그냥 선언 단계가 최상위로 끌어올려지냐 아니냐의 차이 
``` 
console.log(a);
var a = 5; // 이렇게 해도 a는 출력이 된다 이게 바로 호이스팅이 발생하는 것 let은 안된다.
```


### 신기한 거 
```
var car = '포르쉐';
console.log(this.car); //출력 포르쉐

let car2 = '벤리';
console.log(this.car2);//출력 안된다 undefined 

console.log(window.car); //출력 포르쉐 
console.log(window.car2);//출력 undefined 

```

> [!tip] var는 전역 객체의 속성으로 등록되어서 브라우저 환경에서 window 객체 속성이 된다. this도 비슷한 맥락인 것 같다. 신기하게 var가 더 편리해보이긴하는데 현재는 let과 const 사용 권장한다고 한다.

---

### 함수 

기본 함수 
```
var a = 
function(b,c) {
	//
}
```

#### 화살표 함수 
```js
let c = (a,b) => {
//
}

let d = (a,b,c) => a*b*c; //위에 리턴 생략해도 한줄이면 저렇게 가능 
let e = a => a+10 ;//파라메터 하나면 괄호도 없어도 되고 리턴도 한줄이면 이렇게 그대로 즉 return a+10 을 쓰면 오히려 안된다 .
let func = () => 1+2;//파라메터가 없으면 빈 괄호로 나타냄 이렇게 많이 사용 
```
이렇게 function안쓰고 간결해졌다. 숙지하자 

### 클래스

```
class Animal {
	constructor(name){
		this.name = name;
	}
	getName(){
		return this.name;
	}
}
// 이렇게 extends로 상속도 가능 super은 자바하고 똑같음
class Lions extends Animal {
	constructor(name){
		super(name);
		this.type = "lion";
	}
}

let lion = new Lions("king");


```

### 템플릿 문자열 

새로도입된 리터럴 이거 많이 쓰긴한다

```
let a =1;
let b =2;

let str = `${a'더하기 ${b}는 ${a+b'다`;
//str 출력하면 1더하기 2는 3이다 이렇게 출력 

console.log ( `a
b
c`);//이렇게하면 계행문자 없어도 알아서 계행된다 `둘다 이거 사용 백틱`
```

### 디스트럭처링
> 배열의 객체 분해 및 생성 
> 
```js
let arr = [1,2,3,4];
let [a,b,c,d] = arr; //1,2,3,4가 차례대로 들어감 
```
이러면 a에는 1 이들어가게 되고 그뒤는234가 순서대로 들어간다 

```js
const {name : userName,age} = {name: "MAX",age: 26};
```
객체를 분해할 경우에는 {} 중괄호를 사용하고 이름 또한 객체의 key값과 일치시켜야 가져올수있다 .  만약에 별칭을 사용하고 싶으면 : 을 사용하면 사용할수있다.

---

### Spread 연산자

기존 배열이나 객체의 전체 또는 일부를 빠르게 복사한다 
>... 이렇게 사용 

```
let result = (a,b) => a+b;
let data = [1,2];

result(...data);//하면 3 이 리턴되는 것 ...이게 spread 연산자 

const a = [..."abcde"];
console.log(a); //해보면 ['a','b','c','d','e'] 이렇게 출력된다


```

### Rest 연산자

spread와 동일하게 쓰는데 나머지 부분 쓰는 거
나머지가 크기도모르고 몇개인지도 모를 때 유용하게 쓰일 수있다.
``` 
function test(a,b,...arr) {
	console.log(arr);
}

test(1,2,3,4,5);// 이러면 나머지 3,4,5가 출력되는것 
```

### for of 루프 

배열이나 문자열에서 사용 
```
let list = [1,2,3,4];

for (let v of list) {
	console.log(v);//1,2,3,4
}

for (let a of "hello"){
	//하나씩 출력가능 
	
}

//또한 DOM에서도 사용가능하다 

<ul>
	<li>a 
	<li>b
	<li>c
</ul>

const nodes = document.querySelectorAll("li");
// querySelectorAll하면 그냥 id class name 에 상관없이 다 가져와서 노드리스트로 반환하는것 
for (const node of nodes){
	console.log(node.textContent);
	//이렇게 출력가능 
}

//Object

const animals = {

	lion : '사자',
	age : 3
};

const key = Object.key(animals);//객체의 속성들을 순회할수있는 열거할수있는 배열로 반환 
// 이러면 lion,age 이렇게 나오는 거

	for (let k of key){
		console.log(key,animals[key]);하면 원하는 것을 나오게 할 수있다는것.
	}


```

---

### 콜백함수와 익명함수

#### 콜백함수란 어떤 함수에 인자로 전달되어서 어떤 함수의 내부에서 실행되는 함수 

#### 익명함수란 콜백함수를 보통 인자로 전달시 익명함수 형태로 전달한다 일회용처럼 쓰려고 그러는 것 

```
getHuman(function(){
	console.log('나는 인간이다 ')
})

setTimeout(function(){
	console.log("살고싶다");
},3000); //이렇게 타이머나 인터벌에서 콜백함수를 익명함수 형태로 전달 많이한다.
```

# ==Promise & Async-Await 

네트워크 전송 시 어느 정도 기다려야 할 때 자주 사용된다.
> Sync vs Async 
> Sync는 순서대로 task가 끝나면 다음  task 
> Async는 순서 상관없이 동시 실행 

>[!info] Promise
> 비동기 작업을 처리하는 객체
> ### resolve 
> - 정상적인 결과의 값을 반환 (이행)
> ### reject 
> - 정상적이지 않았던 값을 반환(거부)
> ## 상태 
> - 대기 (pending) :  비동기 작업을 처리하는 중 
> - 이행 (fulfiled) : 비동기 작업이 정상적으로 처리 된 경우
> -  거부( rejected ) : 비동기 작업이 정상적으로 처리 되지 않은 경우 
> ## 메소드 
> - then() : 이행 되었을 때
> - cathc() : 거부 되었을 때 
> - fianlly() : 이행 거부 둘다 안되어도 기본으로 실행 

```
const myPromise = new Promise((resolve,reject)=> {|

    setTimeout(()=>{

        const text = prompt("hello 입력해서 선물 받기");

        if (text === "hello") {

            resolve("gift");

        }

        else {

            reject("error 거부됨 ");

        }

    },3000

    )

})

  

myPromise.then((result) => {

    console.log('result :',result);

})

.catch( (err)=> {

    console.log ("erre", err);

})
```

> [!info] ## Async - Await 
> 콜백함수와 프로미스의 단점을 보완하여 개발자가 읽기 좋은 코드로 작성할 수 있게 도와준다.
> 

```
async function 함수명() {
  await 비동기_처리_메서드_명();
}

```
>먼저 함수의 앞에 `async` 라는 예약어를 붙입니다. 그러고 나서 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 `await`를 붙입니다. 여기서 주의하셔야 할 점은 비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 `await`가 의도한 대로 동작합니다.

> [!warning] Promise 객체를 반환하기 때문에 Try Catch문을 써주는 게 좋다 오류 컨트롤

## Try Catch 오류 컨트롤

A to Z 강의 진행하면서 오류를 많이 마주했다.
aysnc 함수 안에서 try catch를 많이 사용하면서 
catch(error)이거에 대해서 궁금해서 찿아보았다.

## [에러 객체](https://ko.javascript.info/try-catch#ref-1020)

에러가 발생하면 자바스크립트는 에러 상세내용이 담긴 객체를 생성합니다. 그 후, `catch` 블록에 이 객체를 인수로 전달합니다.

내장 에러 전체와 에러 객체는 두 가지 주요 프로퍼티를 가집니다.

`name`

에러 이름. 정의되지 않은 변수 때문에 발생한 에러라면 `"ReferenceError"`가 이름이 됩니다.

`message`

에러 상세 내용을 담고 있는 문자 메시지

표준은 아니지만, `name`과 `message` 이외에 대부분의 호스트 환경에서 지원하는 프로퍼티도 있습니다. `stack`은 가장 널리 사용되는 비표준 프로퍼티 중 하나입니다.

`stack`

현재 호출 스택. 에러를 유발한 중첩 호출들의 순서 정보를 가진 문자열로 디버깅 목적으로 사용됩니다.





### JSON 메소드 

#### JSON.stringify() 
- js값이나 객체를 JSON문자열로 변환한다. 
#### JSON.parse()
- json문자열의 구문을 분석하고 객체나 js값으로 생성한다 

```
const user = '{"name":"김성엽"}'; //json문자열 형태 
const data = JSON.parse(user);
//data.name --> 이게 김성엽나오는것 
```


---

## 문법 구조 분해 할당

#### 문법의 구조를 분해해서 할당한다!! 

2가지 경우 

1. 객체(Object) 일 경우
	```
		let person  = {
			name : "kim"
		};
		const {name} = person;
		// 기존에는 const name = person.name; 이렇게 해야 했었는데 이걸 간편화 시킨 것 
	```
2. 배열 (arr) 일 경우
	```
		let arr = [1,2];
		let [first,second] = arr;
		// 기존의 경우 let first = arr[0]; 이렇게 가져와야 했다.
	```


# prompt 

``` 
const a = prompt("값을 입력하세요"); <====== 여기서 JS가 실행을 멈춰있음 

console.log(a);
```

prompt를 사용하면 prompt에서 JS가 실행을 멈추고 prompt 값을 입력할 때까지 기다린다 그러나 이것은 매우 구시대적인 방법이다 왜냐하면 스타일을 아무것도 건들 수 없기 때문에 


# type 변화 

parseInt()  : 스트링을 숫자로 변화 숫자가 아닌 스트링을 하면 NaN이 뜬다
	NaN = Not a Number 
	isNan() : NaN이면 true 반환 


# import export

## export 
```javascript
export const api_key = "12345";

import { api_key } from "./test";
```

이렇게 변수를 export해서 다른 파일에서 사용이 가능하다 

> import { } from 파일경로 

### export default 
각  파일별로 하나의 default export가 존재한다.
파일에서 export하는 기본값이 된다.
변수를 못쓰고 값으로만 가능 

```javascript
export default "12354";
import api_key from "./test";

console.log(api_key);
```

export default 할 경우 이름이 없으므로 import {}중괄호가 아니라 사용자가 이름을 지정해줘야 한다 .  

> 하나의 값이나 함수만 export 할 경우에 좋다 하나밖에없을때 

### 여러개를 export 하고 import 할 경우 
```javascript
export default "12345";

export const api_key = "KSYZKZK";

export const hello ="hello";

import * as utill from "./test.js";

console.log(utill.api_key);

console.log(utill.hello);

console.log(utill.default);
```

> import * as 사용자 지정 이름 from 상대경로 ;

이런식으로 * 한뒤 as 뒤부분에 사용자가 설정한 이름을 쓰면 export 한 모든 것을 사용 가능하다 

객체를 만들어서 사용하는 방법이다 

#### as 키워드 
임포트 할 경우에도 만약에 이름이 맘에 안들면 
> 기존이름 as 내가원하는 이름 

으로 내가 원하는 이름으로 변경하여서 사용이 가능하다 



# Math.Random()

> Math.random() * 3 

이렇게 사용하면 0 부터 3사이의 숫자들이 출력된다 
소수점으로 출력되기 때문에 보통 
Math.floor(Math.random() * 3 ) 이렇게 해서 0 1 2 가 생성되게 한다 .

# ... Rest Property 
나머지 속성 

함수의 마지막 매개변수 앞에 "`...`"(세 개의 U+002E FULL STOP 문자)를 붙이면 (사용자가 제공한) 모든 후속 매개변수를 [표준 JavaScript 배열](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)에 넣도록 지정합니다. 마지막 매개변수만 나머지 매개변수로 설정할 수 있습니다.