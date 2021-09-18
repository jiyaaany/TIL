## `styled-components`의 `ThemeProvider`
- 스타일 코드의 일관성을 유지할 수 있다.
- 중복되는 스타일의 재사용이 가능하다.
- 스타일 코드를 쉽게 파악할 수 있다.

## `ThemeProvider`
`Contenxt API`를 사용해 모든 리액트 컴포넌트에게 `theme` 속성을 사용할 수 있도록 전달한다.

### 기본적인 사용
```javascript
const theme = {
    color: gray;
    // .. 등 사용자 정의 theme
}

render(
    <ThemeProvider theme={theme}>
        <App />
    </ThemeProvider>
)
```
보통 렌더 트리의 최상단에 위치하기 때문에 하위 모든 컴포넌트에서 `theme`를 사용할 수 있다.

### Function Themes
객체가 아닌 함수 형태로도 `theme`를 지정할 수 있다.

```javascript
const theme = {
  fg: "palevioletred",
  bg: "white"
};

// This theme swaps `fg` and `bg`
const invertTheme = ({ fg, bg }) => ({
  fg: bg,
  bg: fg
});

render(
  <ThemeProvider theme={theme}>
    <div>
      <Button>Default Theme</Button>

      <ThemeProvider theme={invertTheme}>
        <Button>Inverted Theme</Button>
      </ThemeProvider>
    </div>
  </ThemeProvider>
);
```

> [참고]
>
> https://wonit.tistory.com/366
