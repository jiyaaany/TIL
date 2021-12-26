# `first-child`와 `first-of-type`
CSS에서 `first-child` 속성을 사용했더니 이런 오류를 발생시킨다.
![image](https://user-images.githubusercontent.com/43168524/147406746-63e1629a-b3a6-4b18-9a6f-d49208ac2d6a.png)

```
The pseudo class ":first-child" is potentially unsafe when doing server-side rendering. Try changing it to ":first-of-type".
```

`first-child`: 같은 레벨의 요소 중 첫 번째
`first-of-type`: 같은 레벨의 같은 태그 요소 중 첫 번째

`first-child`는 잠재적으로 안전하지 않을 수 있기 때문에 `first-of-type`을 사용하는 것이 좋다.

