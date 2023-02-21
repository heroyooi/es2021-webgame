# ES2021 자바스크립트 강좌

## 참고 링크

- [강좌 영상](https://www.youtube.com/watch?v=2yGhb-z8VTQ&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt)
- [강좌 저장소](https://github.com/ZeroCho/es2021-webgame)
- [듣던 강좌 7-6](https://www.youtube.com/watch?v=-DWk1Bt-03Q&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt&index=67)

## 자바스크립트 강좌 4. 계산기 

### 함수 중복 제거하기

```js
document.querySelector('#num-0').addEventListener('click', () => {
  if (operator) { // 비어있지 않다
    numTwo += '0';
  } else { // 비어있다
    numOne += '0';
  }
  $result.value += number;
});
document.querySelector('#num-1').addEventListener('click', () => {
  if (operator) { // 비어있지 않다
    numTwo += '1';
  } else { // 비어있다
    numOne += '1';
  }
  $result.value += number;
});
document.querySelector('#num-2').addEventListener('click', () => {
  if (operator) { // 비어있지 않다
    numTwo += '2';
  } else { // 비어있다
    numOne += '2';
  }
  $result.value += number;
});
```

```js
const onClickNumber = (number) => (event) => {
  if (operator) { // 비어있지 않다
    numTwo += number;
  } else { // 비어있다
    numOne += number;
  }
  $result.value += number;
}; // 고차 함수 (high order function)

document.querySelector('#num-0').addEventListener('click', onClickNumber('0'));
document.querySelector('#num-1').addEventListener('click', onClickNumber('1'));
document.querySelector('#num-2').addEventListener('click', onClickNumber('2'));
```
- 매개 변수 event는 브라우저가 넣어준다.
- 고차 함수로 함수간의 중복을 제거할 수 있다.

```js
const onClickNumber = (event) => {
  if (operator) { // 비어있지 않다
    numTwo += event.target.textContent;
  } else { // 비어있다
    numOne += event.target.textContent;
  }
  $result.value += event.target.textContent;
}; // 고차 함수 (high order function)

document.querySelector('#num-0').addEventListener('click', onClickNumber);
document.querySelector('#num-1').addEventListener('click', onClickNumber);
document.querySelector('#num-2').addEventListener('click', onClickNumber);
```
- textContent를 활용하면 고차 함수를 쓰지 않아도 된다.

- -, *, /는 문자열을 숫자로 바꿔준다.

## 자바스크립트 강좌 5. 숫자야구

- 순서도도 알고리즘이다.
- 중복되지 않게 4개의 숫자를 뽑아야한다.

|:--|:--|
|Math.random()|0 <= x < 1|
|Math.random() * 9|0 <= x < 9|
|Math.random() * 9 + 1|1 <= x < 10|
|Math.floor(Math.random() * 9 + 1)|x = {1, 2, 3, 4, 5, 6, 7, 8, 9}|

```js
if (new Set(input).size !== 4) { // 중복된 숫자가 있는가
  return alert('중복되지 않게 입력해 주세요.');
}
```
- **new Set**에 넣은 것은 중복이 제거가 된다. 위 input에 '3144'를 넣으면 {'3', '1', '4'}가 된다.
- **new Set**은 중복이 없는 배열이라고 생각하면 된다.
- 알아서 중복을 제거해주는 배열이 **new Set**이고, length가 아닌 size를 쓴다.

```html
<input required type="text" minlength="4" maxlength="4" pattern="^(?!.*(.).*\1)\d{4}$" />
```
- [정규표현식 공부 사이트](https://github.com/ziishaned/learn-regex)

<br /><br />

### join vs split

1. join: 배열을 문자열로 바꾸는 메서드
```js
const answer = [3, 1, 4, 6];
answer.join(); // [3, 1, 4, 6] -> '3,1,4,6'
answer.join(''); // [3, 1, 4, 6] -> '3146'
answer.join(':'); // [3, 1, 4, 6] -> '3:1:4:6'
```
- join 메서드는 **join(',')**가 기본값이다.
- join 메서드에 인자를 넘기지 않으면 ,를 기준으로 합치게 된다.

<br /><br />

2. split: 문자열을 배열로 바꾸는 메서드
```js
'3146'.split(); // ["3146"]
'3146'.split(''); // ["3", "1", "4", "6"]
```

<br /><br />

### indexOf vs includes

```js
'2345'.indexOf(3) === 1;
'2345'.indexOf(6) === -1;
['2', '3', '4', '5'].indexOf('5') === 3;
['2', '3', '4', '5'].indexOf(5) === -1; // 요소의 자료형까지 같아야 함
'2345'.includes(3) === true;
['2', '3', '4', '5'].includes(5) === false;
```
- indexOf는 원하는 값이 들어있다면 해당 인덱스를 알려주고, 들어 있지 않다면 -1를 반환한다.
- includes는 직관적으로 true/false 를 반환한다.
- includes보다 indexOf가 좀 더 구체적으로 알려준다. 활용 가능성이 높음

<br /><br />

### document.createElement vs document.createTextNode

- 각각 태그와 텍스트를 만드는 메서드이다. 단 다른 태그에 append나 appendChild 하기 전까지는 화면에 보이지 않는다.

<br /><br />

### appendChild vs append

```js
const message = document.createTextNode(`패배! 정답은 ${answer.join('')}`);
$logs.appendChild(message);
```
- appendChild는 append로 개선되었다.

<br /><br />

```js
$logs.append(`${value}: ${strike} 스트라이크 ${ball} 볼`, document.createElement('br'));
```
- appendChild로는 하나만 넣을 수 있고, append를 사용하면 여러 개를 동시에 넣을 수 있다.
- append로 문자열은 createTextNode 할 필요없이 바로 넣으면 되고, 태그랑 함께 넣을 수 있다.
- append는 여러개 동시 추가 가능


### forEach, map, fill

```js
const answer = [3, 1, 4, 6];
const value = '3214';
let strike = 0;
let ball = 0;
answer.forEach((element, i) => {
  const index = value.indexOf(element);
  if (index > -1) { // 일치하는 숫자 발견
    if (index === i) { // 자릿수도 같음
      strike += 1;
    } else { // 숫자만 같음
      ball += 1;
    }
  }
});
```

- forEach, map은 배열에 대한 반복문이 된다.

```js
const array = [1, 2, 3, 4];
for (let i = 0; i < 4; i++) {
  result.push(array[i] * 2);
}
console.log(result); // [2, 4, 6, 8]
```

```js
array.map((element, i) => {
  return element * 2;
});

```
## 자바스크립트 강좌 6. 로또

- 실제로 코딩한 순서와 다르게 동작하는 코드를 **비동기 코드**라고 한다.
- 이벤트 리스너가 대표적인 비동기 코드이다.


### splice vs slice

```js
const array = [1, 2, 3, 4, 5];
array.splice(2, 1); // [3]
array // [1, 2, 4, 5]

const array2 = [1, 2, 3, 4, 5];
array2.splice(2, 1, 9);
array2 // [1, 2, 9, 4, 5];
```
- **splice(start, ?deleteCount, ...items)** : 처음 인덱스, 갯수, 추가할 아이템
- splice는 배열에서 빼낸 값이 리턴값으로 들어있다.
- splice는 원본 배열이 변한다.

```js
const array = [3, 2, 9, 7, 5, 8, 6, 4, 1];
array.slice(); // [3, 2, 9, 7, 5, 8, 6, 4, 1]
array.slice(0, 3); // [3, 2, 9]
array.slice(3, 5); // [7, 5]
array.slice(4, -1); // [5, 8, 6, 4]
array.slice(4); // => array.slice(4, 0); // [5, 8, 6, 4, 1]
array.slice(-5, -1); // [5, 8, 6, 4]
```
- **slice(?start, ?end)** : 처음 인덱스와 끝 인덱스, 끝 인덱스는 포함하지 않는다.
- end의 -1은 마지막 인자를 뜻한다.
- 두번째 인자를 생략하면 0이 된다.
- start에 -5를 적으면 뒤에서부터 다섯번째가 처음 인덱스가 된다.
  - 배열이 값이 많아서 뒤에서부터 숫자를 셀 때 좋다.
- slice는 원본 배열이 변하지 않는다. map도 원본 배열은 변하지 않는다.

- 원본이 변하지 않는 배열 메서드 : **slice, map**
- 원본이 변하는 배열 메서드 : **splice, sort**

### sort

```js
const array = [3, 2, 9, 7, 5, 8, 6, 4, 1];
array.sort((a, b) => {
  return a - b; // 오름차순
  // return b - a; // 내림차순
}) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
array // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
- sort는 원본 배열이 변한다.

- sort 메서드를 사용하면 원본이 변하기 때문에, sort 메서드 앞에 slice를 사용하면 원본을 유지할 수 있게 된다.
```js
const array = [3, 2, 9, 7, 5, 8, 6, 4, 1];
array.slice().sort((a, b) => a - b); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
array // [3, 2, 9, 7, 5, 8, 6, 4, 1]
array.slice().sort((a, b) => b - a); // [9, 8, 7, 6, 5, 4, 3, 2, 1]
array // [3, 2, 9, 7, 5, 8, 6, 4, 1]
```

- sort가 숫자만 정렬을 하는 것은 아니다. 문자나 날짜도 정렬할 수 있다.

```js
const arr = ['apple', 'orange', 'grape', 'banana', 'kiwi'];
arr.slice().sort((a, b) => a[0].charCodeAt() - b[0].charCodeAt());
// ['apple', 'banana', 'grape', 'kiwi', 'orange'] // 오름차순
arr.slice().sort((a, b) => b[0].charCodeAt() - a[0].charCodeAt()); // 내림차순
// ['orange', 'kiwi', 'grape', 'banana', 'apple']
arr.slice().sort((a, b) => a.localeCompare(b)) // 사전순 - 오름차순
// ['apple', 'banana', 'grape', 'kiwi', 'orange']
arr.slice().sort((a, b) => b.localeCompare(a)) // 사전순 - 내림차순
// ['orange', 'kiwi', 'grape', 'banana', 'apple']
[new Date(2020, 0, 1), new Date(2021, 0, 1)].sort((a, b) => a - b);
```

```js
Array(45).fill().map((v, i) => i + 1);
```
- 45개의 인자를 갖고있는 배열을 만들어준다.
- fill()로 모두 undefined으로 만들어준 map을 통해서 다음 1부터 45까지 넣어줌


### 클로저

- 변수는 스코프(scope, 범위)라는 것을 가집니다. var는 함수 스코프를 가지고, let은 블록 스코프를 가집니다.
```js
if (true) {
  var a = 1;
}
console.log(a); // 1
```
- a는 함수 스코프를 가지기에 콘솔에서 a에 접근 가능하다.

```js
if (true) {
  let a = 1;
}
console.log(a); // a is not defined
```
- 하지만 let은 블록 스코프라서 a에 접근할 수 없다.

```js
for (var i = 0; i < 6; i++) {
  setTimeout(function(){
    console.log(winBalls[i], i);
  }, (i + 1) * 1000);
}
```
- for문 안에 var를 사용할 경우 기대와 다른 결과를 만나게 된다.
- var 스코프와 함수 클로저가 조합된 복잡한 문제이다.
- 함수 스코프를 갖고 있는 var와 비동기가 만나면 클로저 문제가 발생한다.
- 그래서 이를 클로저를 통해서 해결하게 된다.

```js
for (var i = 0; i < 6; i++) {
  function(j) {
    setTimeout(function(){
      console.log(winBalls[j], j);
    }, (i + 1) * 1000);
  }(i);
}
```
- 함수와 함수 바깥에 있는 변수를, 함수와 함수 안에 있는 변수 j로 만들어줌으로써 문제를 해결하게 된다.
- **클로저**는 함수와 외부 변수와의 관계이다.

- [실행 컨텍스트](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)

### 공 색칠하기

```js
function colorize(number, $tag) {
  if (number < 10) {
    $tag.style.backgroundColor = 'red';
    $tag.style.color = 'white';
  } else if (number < 20) {
    $tag.style.backgroundColor = 'orange';
  } else if (number < 30) {
    $tag.style.backgroundColor = 'yellow';
  } else if (number < 40) {
    $tag.style.backgroundColor = 'blue';
    $tag.style.color = 'white';
  } else {
    $tag.style.backgroundColor = 'green';
    $tag.style.color = 'white';
  }
}
const drawBall = (number, $parent) => {
  const $ball = document.createElement('div');
  $ball.className = 'ball';
  colorize(number, $ball);
  $ball.textContent = number;
  $parent.appendChild($ball);
}
```

## 자바스크립트 강좌 7. 가위바위보

```js
const changeComputerHand = () => {
  if (computerChoice === 'scissors') { // 가위면
    computerChoice = 'rock';
  } else if (computerChoice === 'rock') { // 바위
    computerChoice = 'paper';
  } else if (computerChoice === 'paper') { // 보
    computerChoice = 'scissors';
  }
  $computer.style.background = `url(${IMG_URL}) ${rspX[computerChoice]} 0`;
  $computer.style.backgroundSize = 'auto 200px';
}
setInterval(changeComputerHand, 50);
```
- setInterval은 다음과 같이 setTimeout으로 바꿀 수 있다.
```js
const changeComputerHand = () => {
  if (computerChoice === 'scissors') { // 가위면
    computerChoice = 'rock';
  } else if (computerChoice === 'rock') { // 바위
    computerChoice = 'paper';
  } else if (computerChoice === 'paper') { // 보
    computerChoice = 'scissors';
  }
  $computer.style.background = `url(${IMG_URL}) ${rspX[computerChoice]} 0`;
  $computer.style.backgroundSize = 'auto 200px';
  setTimeout(changeComputerHand, 50);
}
setTimeout(changeComputerHand, 50);
```
- 함수가 자기를 다시 호출하면 재귀 함수, 재귀 setTimeout으로 setInterval과 같은 효과를 구현할 수 있음
- setTimeout은 시간이 정확하지 않을 수 있다. setInterval도 마찬가지이다. 정확한 시간을 보장하지는 않는다. 그래도 setInterval은 간격을 보장하려고 노력한다. setTimeout은 간격을 보장하지 않는다.


```js
let intervalId = setInterval(changeComputerHand, 50);

const clickButton = () => {
  clearInterval(intervalId);
  // 점수 계산 및 화면 표시
  setTimeout(() => {
    // clearInterval(intervalId); // 실행 시간이 다르다.
    intervalId = setInterval(changeComputerHand, 50);
  }, 1000);
}

$rock.addEventListener('click', clickButton);
$scissors.addEventListener('click', clickButton);
$paper.addEventListener('click', clickButton);
```

- 예전 타이머로 지금 타이머를 취소할 순 없기 때문에 타이머를 만들 때마다 변수에 저장을 해줘야 한다.
- 버튼을 연달아 클릭 시 가위바위보가 더 빠르게 움직이는 버그가 발생한다.
- 버튼을 여러번 클릭하면 setTimeout의 타이머가 여러번 등록이 된다.

<hr />

- 버그의 원인
- clickButton 5번 호출, 인터벌 1번, 2번, 3번, 4번, 5번(얘만 inetervalId)
- 그 다음에 버튼을 클릭하면 5번만 취소
- 그래서 setTimeout 구문 안에 **clearInterval(intervalId);** 를 넣어준다.

- 또는 다음과 같이 **removeEventListener**를 사용해서 버튼을 아예 클릭이 되지 않도록 하면 된다.
```js
const clickButton = () => {
  clearInterval(intervalId);
  $rock.removeEventListener('click', clickButton);
  $scissors.removeEventListener('click', clickButton);
  $paper.removeEventListener('click', clickButton);
  // 점수 계산 및 화면 표시
  setTimeout(() => {
    clearInterval(intervalId);
    intervalId = setInterval(changeComputerHand, 50);
    $rock.addEventListener('click', clickButton);
    $scissors.addEventListener('click', clickButton);
    $paper.addEventListener('click', clickButton);
  }, 1000);
}
$rock.addEventListener('click', clickButton);
$scissors.addEventListener('click', clickButton);
$paper.addEventListener('click', clickButton);
```

- 하지만 removeEventListener는 다음과 같이 예외로 동작을 할 때가 있다.
```js
const fun = (값) => () => {
  console.log('고차함수입니다', 값);
}
fun(1) === fun(1) // false
태그.addEventListener('click', fun(1));
태그.removeEventListener('click', fun(1)); // 같지 않기 때문에 클릭 이벤트가 지워지지 않는다.

{} === {} // false
(() => {}) === (() => {}) // false
```

- 비교하는 객체를 같게 만들어주려면 변수에 담아주면 된다.
```js
const a = {};
const b = a;
a === b; // true

const fun = (값) => () => {
  console.log('고차함수입니다', 값);
}
const fun1 = fun(1);
fun1 === fun1; // true

태그.addEventListener('click', fun1);
태그.removeEventListener('click', fun1); // 같기 때문에 클릭 이벤트가 지워진다.
```

<hr />

- 조건문에서 or로 연결되는 경우 includes나 indexOf로 다음과 같이 줄여줄 수 있다.
```js
if (diff === '고양이' || diff === '사자' || diff === '강아지' || diff === '거북이') {}
if (['고양이', '사자', '강아지', '거북이'].includes(diff)) {}
if (['고양이', '사자', '강아지', '거북이'].indexOf(diff) > -1) {}

// if (diff === 2 || diff === -1) {
if ([2, -1].includes(diff)) {
  console.log('승리');
// } else if (diff === -2 || diff === 1) {
} else if ([-2, 1].includes(diff)) {
  console.log('패배');
// } else if (diff === 0) {
} else {
  console.log('무승부');
}
```