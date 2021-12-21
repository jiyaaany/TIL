# 클로저
```javascript
function helper(func) {
  func();
}

funtion outer() {
  const a = 123;
  const b = 'hello';
  
  function inner() {
    console.log(a, b);
  }
  
  helper(inner);
}
```

위 코드는 이렇게 바꿔쓸 수 있다.
```javascript
function helper(func, a, b) {
  func(a, b);
}

function inner() {
  console.log(a, b);
}

funtion outer() {
  const a = 123;
  const b = 'hello';
  
  helper(inner, a, b);
}
```
중간에 상수 `a`, `b`를 넘기는 부분이 추가되었는데 클로저를 쓰면 이 부분을 생략할 수 있어서 편하다. 이 예시에서는 `inner` 함수를 처리하는 함수가 3개 밖에 없지만 실제로는 한 함수에서 여러 함수를 호출할 수 있기 때문에 인자를 추가해야하는 함수 개수가 기하급수적으로 늘어나게 된다. 그럴 때 클로저를 쓰면 모든 게 생략되어 깔끔해진다.
