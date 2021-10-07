# Composition API란?
컴포지션 API는 컴포넌트의 로직을 유연하게 구성할 수 있도록 하는 함수 기반의 API이다.

기존 Vue2 버전에선 `mixin`을 통해 컴포넌트 로직을 어느 정도 재사용할 수 있었지만, 오버라이딩 문제나 다중 `mixin`을 상속한다면 컴포넌트 관리가 어려워진다는 등 아쉬운 점이 있었다. 무엇보다 싱글 파일 컴포넌트에 로직을 구현하다보면 가독성이 떨어지고 복잡해지는 문제가 있다.

```javascript
<template>
    <div>
        <h1>{{ countWithUnit }}</h1>
        <button @click="increase">Increase</button>
        <button @click="decrease">Decrease</button>
    </div>
</template>

<script>
export default {
    data () {
        return {
            count: 0
        }
    },
    computed: {
        countWithUnit () {
            return this.count + ' 입니다.'
        }
    },
    methods: {
        increase () {
            ++this.count
        },
        decrease () {
            --this.count
        }
    }
}
</script>
```

위 코드는 간단한 카운터 컴포넌트이다. 카운터의 값을 저장하는 `count`와 값을 조작하기 위한 `increase`, `decrease` 메소드, `{count} 입니다.`의 형식의 데이터를 제공하는 `computed`함수 `countWithUnit`이 있다.  
모두 같은 기능을 위한 코드임에도 불구하고 여기 저기 흩어져있는 모습을 볼 수 있다. 카운터 컴포넌트는 작고 복잡하지 않아 직관적이라 느껴질 수 있지만, 규모가 커지고 로직이 많아질 수록 흩어져 보기 어려울 수 있다. 이 외에도, 하나만 존재하는 생명주기에 많은 코드가 응집되는 여러 문제가 있을 수 있다.  
직관적인 확인이 어렵고 재사용성이 떨어진다는 문제를 해결하기 위해 탄생한 것이 **컴포지션(Composition) API** 이다. 위 코드를 컴포지션 API를 사용하여 변경하면 아래와 같다.
```javascript
<template>
    <div>
        <h1>{{ countWithUnit }}</h1>
        <button @click="increase">Increase</button>
        <button @click="decrease">Decrease</button>
    </div>
</template>

<script>
import { ref, computed } from '@vue/composition-api'

const useCount = () => {
    const count = ref(0)
    const countWithUnit = computed(() => count.value + ' 입니다.')

    const increase = () => ++count.value
    const decrease = () => --count.value

    return { countWithUnit, increase, decrease }
}

export default {
    setup () {
        const { countWithUnit, increase, decrease } = countWithUnit()

        return {
            countWithUnit,
            increase,
            decrease
        }
    }
}
</script>
```
카운터 기능에 대한 값과 로직이 `useCount` 함수 내에 모두 모이게 되고, 이후 컴포넌트에 다양한 기능이 생겨도 목적에 맞는 것끼리 모듈화하여 기존의 단점을 보완할 수 있다.

`setup` 훅은 컴포지션 API를 사용하기 위한 진입점. 즉, 초기화 지점이다. 기존 생명주기의 `beforeCreate` 이전에 `setup`이 호출된다. 컴포지션 API를 사용하는 경우 `beforeCreate`, `created` 대신 `setup`을 사용하면 된다.

# 반응형 데이터
반응형 데이터는 값이 변경됨에 따라 이를 감지하고 해당 값에 종속된 작업(Side Effect)가 수행된다. 컴포지션 API에서는 **2가지 유형(reactive, ref)**의 변경 가능한 반응형 데이터를 만들 수 있다.

## `reactive`
첫 번째는 `reactive`이다. 
- 오직 객체만 받을 수 있다.
- 인자로 받은 객체와 **완전히 동일한 프록시 객체를 반환**한다.
- `reactive`를 통해 생성된 객체는 모두 **깊은(Deep) 감지**를 수행하기 때문에 객체가 중첩된 상황에서도 반응형 데이터를 쉽게 조작하고 처리할 수 있다.

`reactive`로 생성한 값은 프록시 객체라고 했지만 ES6에 추가된 프록시와는 **다르다.** ES6의 프록시 객체는 원본 데이터와 별도의 프록시 객체를 생성하지만 `reactive`로 생성한 프록시 객체는 원본 객체와 **완전히 동일**하다.

## `ref`
두 번째는 `ref`이다.  
- 객체를 포함하여 모든 원시파입(Primitive) 값을 포함한 여러가지 타입의 값을 받을 수 있다.
- `ref` 객체의 `value` 속성을 통해 접근할 수 있으며 변경할 때도 `value` 속성에 접근하여 조작해야 한다.
(+ 템플릿에 표시할 때는 `value` 속성 없이 사용)

## `reactive`와 `ref`?
`ref` 객체는 원본 값을 `value`라는 속성에 담아두고 변경을 감시하는 객체, `reactive`는 원본 객체 자체에 변경을 감지하는 옵저버를 추가하여 그대로 반환한 값이다.

## `isRef`, `toRefs`
컴포지션 API에는 단순 반응형 데이터 뿐만 아니라 어떤 유형의 값인지 확인하기 위한 `isRef`, `reactive` 값을 `ref` 값으로 변환하는 `toRefs`가 존재한다.

```javascript
import { reactive } from '@vue/composition-api'

const useMousePosition = () => {
    const pos = reacitve({ x: 0, y: 0 })
    return pos
}

export default {
    setup () {
        const { x, y } = useMousePosition()

        return {
            x,
            y
        }
    }
}
```
좌표와 같이 묶여있는 데이터의 경우 `reactive` 객체 값을 생성해서 사용합니다. 하지만 `reactive` 객체를 구조 분해하여 재할당 할 경우 **반응형으로 동작하지 않습니다.** 이러한 문제를 해결하기 위해 `toRefs`가 존재합니다.
```javascript
import { reactive, toRefs } from '@vue/composition-api'

const useMousePosition = () => {
    const pos = reacitve({ x: 0, y: 0 })
    return toRefs(pos)
}

export default {
    setup () {
        const { x, y } = useMousePosition()

        return {
            x,
            y
        }
    }
}
```
위와 같이 `reactive`를 `toRefs`를 통해 `ref` 값으로 반환하면 구조 분해 할당을 수행해도 반응형이 그대로 유지됩니다.

# computed
계산된 속성(computed) 또한 컴포지션 API를 통해 간단히 사용 가능하다.

```javascript
<template>
    <div>
        <h1>{{ value2x }}</h1>
    </div>
</template>

<script>
import { ref, computed } from '@vue/composition-api'

export default {
    setup () {
        const myValue = ref(10)
        const value2x = computed(() => myValue * 2)

        return {
            value2x
        }
    }
}
</script>
```

# watch
변경 감시(watch)도 컴포지션 API를 통해 간단히 사용할 수 있으며, Vue 2와 동일한 옵션을 사용할 수 있다. (deep, immediate)
```javascript
import { ref, watch } from '@vue/composition-api'

const useUserList = () => {
    const userList = ref([
        { id: 1, name: 'tom' },
        { id: 2, name: 'jessieca' },
        { id: 3, name: 'daniel' }
    ])

    watch(userList, (newVal, oldVal) => {

    }, { deep: true })

    return { userList }
}

export default {
    setup () {
        const { userList } = useUserList()

        setInterval(() => {
            userList.value[0].name += '!'
        }, 3000)
    }
}
```
watch의 첫번째 인자의 값이 변경될 경우 **두번째 인자로 전달된 콜백을 실행**한다. 세 번째 인자로 `deep`, `immediate` 옵션을 활성화할 수 있다.

# 생명 주기(Life Cycle)
```javascript
// Vue 2
export default {
    mounted () {

    },
    updated () {

    },
    destroyed () {

    }
}
// composition
import {
    onMounted,
    onUpdated,
    onUnmounted
} from '@vue/composition-api'

export default {
    setup () {
        onMounted(() => {

        })
        onUpdated(() => {
            
        })
        onUnMounted(() => {
            
        })
    }
}
```
기존에는 컴포넌트 당 하나의 생명 주기를 사용했지만 컴포지션 API를 사용하면 여러개로 나누어 사용할 수 있다.
```javascript
import { onMounted } from '@vue/composition-api'

const first = () => {
    onMounted(() => {

    })
}

const second = () => {
    onMounted(() => {

    })
}

const thired = () => {
    onMounted(() => {

    })
}

export default {
    setup () {
        first()
        second()
        third()
    }
}
```

# 마치며
> 참고 아티클  
https://v3.ko.vuejs.org/api/composition-api.html#setup  
https://geundung.dev/102#recentComments

> 추후 확인  
https://composition-api.nuxtjs.org/