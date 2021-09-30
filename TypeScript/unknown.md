[TypeScript](https://www.typescriptlang.org/) 3 버전부터 `unknown` 타입이 추가되었다.

### `any` 타입
TypeScript에서 `any`는 어떤 타입이든 할당 받을 수 있는 타입이다. 

### `unknown` 타이
`unknown` 타입도 마찬가지로 어떤 타입이든 할당될 수 있다. 차이점은 다른 타입으로 선언된 변수에 선언될 수 없다는 것이다. (`any` 타입 제외)
```javascript
let foo: unknown

let bar: any = foo // OK
let str: string = foo // Error
let num: number = foo // Error
let flag: boolean = foo // Error
let obj: object = foo // Error
```
`unknown` 타입은 **알려지지 않은 타입**으로 프로퍼트에 접근하거나 메서드를 호출하는 것이 불가능하다. 또한, 인스턴스 생성도 불가능하다.
```javascript
let foo: unknown

foo.bar // Error
foo.trigger() // Error
new foo() // Error
```

