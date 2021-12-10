# sort() 함수
배열 요소들을 정렬하기 위해 사용하는 함수입니다.
```javascript
let arr = [1, 2, 3];

arr.sort();
```

## 파라미터
1. `compareFunction` `Optional`
정렬 순서를 정의하는 함수입니다. 생략하면 각 요소의 문자열 변환에 따라 각 문자의 유니 코드 값에 따라 정렬됩니다.
