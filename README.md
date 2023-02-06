# ES2021 자바스크립트 강좌

## 참고 링크

- [강좌 영상](https://www.youtube.com/watch?v=2yGhb-z8VTQ&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt)
- [강좌 저장소](https://github.com/ZeroCho/es2021-webgame)

- [듣던 강좌 5-3. 무작위로 숫자 네 개 뽑기](https://www.youtube.com/watch?v=yIbL-mgML1A&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt&index=50)

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

|||
|:--|:--|
|Math.random()|0 <= x < 1|
|Math.random() * 9|0 <= x < 9|
|Math.random() * 9 + 1|1 <= x < 10|
|Math.floor(Math.random() * 9 + 1)|x = {1, 2, 3, 4, 5, 6, 7, 8, 9}|