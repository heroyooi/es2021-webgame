# ES2021 자바스크립트 강좌

## 참고 링크

- [강좌 영상](https://www.youtube.com/watch?v=2yGhb-z8VTQ&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt)
- [강좌 저장소](https://github.com/ZeroCho/es2021-webgame)

- [듣던 강좌 5-7](https://www.youtube.com/watch?v=H6EQPhMgHkM&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt&index=54)

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
