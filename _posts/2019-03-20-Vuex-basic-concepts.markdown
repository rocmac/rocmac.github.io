---
layout: post
title:  Vuex basic concepts
date:   2019-03-20 00:00:00 +0300
categories: Vue
tag: [Vuex, Javascript] # add tag
---

* content
{:toc}


### 需调用 Vue.use(Vuex)

## State
Vuex使用使用单一状态树，用一个对象就包含了全部的应用层级状态

## mapState 辅助函数

```
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```


## Getter

可以使用state，store.getters.*作为参数

```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

### mapGetters附属函数
mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性

```
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```

```
mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```

## Mutation
- 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation
- mutation必须是同步函数

```
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
```

```
store.commit('increment')
```

- 提交payload,payload 可以使一个对象

```
// ...
mutations: {
  increment (state, n) {
    state.count += n
  }
}
```

```
store.commit('increment', 10)
```

## Action
- Action 提交的是 mutation，而不是直接变更状态
- Action 可以包含任意异步操作

```
store.dispatch('increment')
```

```
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```

## Module
Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter

```
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```


