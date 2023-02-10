# ES2021 자바스크립트 강좌

## 참고 링크

- [강좌 영상](https://www.youtube.com/watch?v=2yGhb-z8VTQ&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt)
- [강좌 저장소](https://github.com/ZeroCho/es2021-webgame)
- [듣던 강좌 6-5. 블록, 함수 스코프, 클로저 문제](https://www.youtube.com/watch?v=Qh9Ad6TmGc0&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt&index=60)

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
