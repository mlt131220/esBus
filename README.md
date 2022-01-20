# esBus

一个简单好用的事件发布订阅类；

<br/>

# Installation

```typescript
npm install esBus -S
```

<br/>

# Use（Vue3为例）

```typescript
import { createApp } from 'vue'
import App from './App.vue'
import EsBus from 'esBus'
```

### main.ts中注册实例

```typescript
const app = createApp(App);

const $bus = EsBus.getInstance();`
app.provide("$bus",bus);

app.mount('#app');
```

### 组件中使用

```typescript
const $bus = inject("$bus");

/** 订阅、注册事件 bus() */
//窗口改变大小监听
$bus.bus("windowResize");

/** 添加事件 add() */
// 窗口大小改变响应
$bus.add("windowResize", () => {
  console.log("窗口大小改变");
})
$bus.add("windowResize", () => {
  alert("窗口大小改变第二个事件");
})

/** 发布、触发事件 dispatch() */
const onWindowResize = () => {
  $bus.dispatch("windowResize");
}
window.addEventListener('resize', onWindowResize, false)

/** 移除订阅 remove() */
$bus.remove("windowResize")
```

<br/>

# Hint

- 未注册订阅的监听事件会放入暂存器中，在注册后自动添加至改订阅。通俗解释就是在未执行`$bus.bus("windowResize")`前执行了`$bus.add("windowResize",()=>{})`，则add()的事件会放入暂存器中，在bus()时自动添加；
