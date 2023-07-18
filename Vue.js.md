# Vue.js

## vue.js 是什么

Vue 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://v2.cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

```html
<div id="vue_det">
  <h1>site : {{site}}</h1>
  <h1>url : {{url}}</h1>
  <h1>{{details()}}</h1>
</div>
```

```js
let vm = new Vue({
  el: '#vue_det',
  data: {
    site: "Zero",
    url: "www.baidu.com",
    alexa: "10000"
  },
  methods: {
    details: function() {
      return this.site + " - Hello World";
    }
  }
});
```

- 看起来这跟渲染一个字符串模板非常类似，但是 Vue 在背后做了大量工作。现在数据和 DOM 已经被建立了关联，所有东西都是**响应式的**。

除了文本插值，我们还可以像这样来绑定元素  `attribute`

```html
<div id="vue_det">
  <span v-bind:title="message">
    鼠标停留显示信息
  </span>
</div>
```

```javascript
let vm = new Vue({
  el: '#vue_det',
  data: {
    message: '页面加载于 ' + new Date().toLocaleString()
  }
});
```

- {{...}} 标签的内容将会被替代为对应组件实例中 **message** 属性的值，如果 **message** 属性的值发生了改变，{{...}} 标签内容也会更新。
- 如果不想改变标签的内容，可以通过使用 **v-once** 指令执行一次性地插值，当数据改变时，插值处的内容不会更新。

## 条件与循环

控制切换一个元素是否显示也相当简单：

```html
<div id="app">
  <p v-if="seen">
    现在你看到我了
  </p>
</div>
```

```javascript
var app3 = new Vue({
  el: '#app',
  data: {
    seen: true
  }
})
```

继续在控制台输入 `app3.seen = false`，你会发现之前显示的消息消失了。

还有其它很多指令，每个都有特殊的功能。例如，`v-for` 指令可以绑定数组的数据来渲染一个项目列表：

```
<div id="app">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```

```
var app4 = new Vue({
  el: '#app',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

在控制台里，输入 `app4.todos.push({ text: '新项目' })`，你会发现列表最后添加了一个新项目。

- v-bind 缩写

```javascript
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

- v-on 缩写

```javascript
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

## 处理用户输入

- 为了让用户和你的应用进行交互，我们可以用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：

```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">反转消息</button>
</div>
```

```javascript
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

- 注意在 `reverseMessage` 方法中，我们更新了应用的状态，但没有触碰 DOM——所有的 DOM 操作都由 Vue 来处理，你编写的代码只需要关注逻辑层面即可。
- Vue 还提供了 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定。

```html
<div id="app">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```

```javascript
var app6 = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

## 组件

- 组件（Component）是 Vue.js 最强大的功能之一。
- 组件可以扩展 HTML 元素，封装可重用的代码。

```javascript
<div id="app">
  <runoob></runoob>
</div>

<script>
  // 创建一个Vue 应用
  const app = Vue.createApp({})

  // 定义一个名为 runoob的新全局组件
  app.component('runoob', {
    template: '<h1>自定义组件!</h1>'
  })

  app.mount('#app')
</script>
```

```javascript
<script>
  // 创建一个Vue 应用
  const app = Vue.createApp({})

  // 定义一个名为 button-counter 的新全局组件
  app.component('button-counter', {
    data() {
      return {
        count: 0
      }
    },
    template: `
      <button @click="count++">
        点了 {{ count }} 次！
      </button>`
  })
  app.mount('#app')
</script>
```

###  组件的复用

```javascript
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```

### 局部组件

- 全局注册往往是不够理想的。比如，如果你使用一个像 webpack 这样的构建系统，全局注册所有的组件意味着即便你已经不再使用一个组件了，它仍然会被包含在你最终的构建结果中。这造成了用户下载的 JavaScript 的无谓的增加。
- 在这些情况下，你可以通过一个普通的 JavaScript 对象来定义组件：

```javascript
const ComponentA = {
  /* ... */
}
const ComponentB = {
  /* ... */
}
const ComponentC = {
  /* ... */
}
```

```javascript
<div id="app">
    <runoob-a></runoob-a>
</div>
<script>
var runoobA = {
  template: '<h1>自定义组件!</h1>'
}
 
const app = Vue.createApp({
  components: {
    'runoob-a': runoobA
  }
})
app.mount('#app')
```

### Prop

- prop 是子组件用来接受父组件传递过来的数据的一个自定义属性。
- 父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：

```javascript
<div id="app">
  <site-name title="Google"></site-name>
  <site-name title="Runoob"></site-name>
  <site-name title="Taobao"></site-name>
</div>
 
<script>
const app = Vue.createApp({})
 
app.component('site-name', {
  props: ['title'],
  template: `<h4>{{ title }}</h4>`
})
 
app.mount('#app')
```

### 动态 Prop

- 类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件：

```javascript
<div id="app">
  <site-info
    v-for="site in sites"
    :id="site.id"
    :title="site.title"
  ></site-info>
</div>
 
<script>
const Site = {
  data() {
    return {
      sites: [
        { id: 1, title: 'Google' },
        { id: 2, title: 'Runoob' },
        { id: 3, title: 'Taobao' }
      ]
    }
  }
}
 
const app = Vue.createApp(Site)
 
app.component('site-info', {
  props: ['id','title'],
  template: `<h4>{{ id }} - {{ title }}</h4>`
})
 
app.mount('#app')
```



## 计算属性

计算属性关键词: `computed`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
    <script src="https://cdn.staticfile.org/vue/3.0.5/vue.global.js"></script>
  </head>
  <body>
    <div id="app">
      <p>原始字符串: {{ message }}</p>
      <p>计算后反转字符串: {{ reversedMessage }}</p>
    </div>

    <script>
      const app = {
        data() {
          return {
            message: 'RUNOOB!!'
          }
        },
        computed: {
          // 计算属性的 getter
          reversedMessage: function () {
            // `this` 指向 vm 实例
            return this.message.split('').reverse().join('')
          }
        }
      }

      Vue.createApp(app).mount('#app')
    </script>
  </body>
</html>
```

## 监听属性

`watch`

```html
<div id = "app">
  千米 : <input type = "text" v-model = "kilometers"  @focus="currentlyActiveField = 'kilometers'">
  米 : <input type = "text" v-model = "meters" @focus="currentlyActiveField = 'meters'">
</div>
<p id="info"></p>    
<script>
  const app = {
    data() {
      return {
        kilometers : 0,
        meters:0
      }
    },
    watch : {
      kilometers: function(newValue, oldValue) {
        // 判断是否是当前输入框
        if (this.currentlyActiveField === 'kilometers') {
          this.kilometers = newValue;
          this.meters = newValue * 1000
        }
      },
      meters : function (newValue, oldValue) {
        // 判断是否是当前输入框
        if (this.currentlyActiveField === 'meters') {
          this.kilometers = newValue/ 1000;
          this.meters = newValue;
        }
      }
    }
  }
  vm = Vue.createApp(app).mount('#app')
  vm.$watch('kilometers', function (newValue, oldValue) {
    // 这个回调将在 vm.kilometers 改变后调用
    document.getElementById ("info").innerHTML = "修改前值为: " + oldValue + "，修改后值为: " + newValue;
  })
</script>
```

## 样式绑定

`class` 与 `style` 是 `HTML` 元素的属性，用于设置元素的样式，我们可以用 `v-bind` 来设置样式属性。

`v-bind` 在处理 `class` 和 `style` 时， 表达式除了可以使用字符串之外，还可以是对象或数组。

`v-bind:class` 可以简写为 `:class`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
    <script src="https://unpkg.com/vue@next"></script>
    <style>
      .active {
        width: 100px;
        height: 100px;
        background: green;
      }
    </style>
  </head>
  <body>
    <div id="app">
      <div :class="{ 'active': isActive }"></div>
    </div>

    <script>
      const app = {
        data() {
          return {
            isActive: true
          }
        }
      }

      Vue.createApp(app).mount('#app')
    </script>
  </body>
</html>
```

- 数组语法

```php+HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
    <script src="https://unpkg.com/vue@next"></script>
    <style>
      .static {
        width: 100px;
        height: 100px;
      }
      .active {
        background: green;
      }
      .text-danger {
        background: red;
      }
    </style>
  </head>
  <body>
    <div id="app">
      <div class="static" :class="[activeClass, errorClass]"></div>
    </div>

    <script>
      const app = {
        data() {
          return {
            activeClass: 'active',
            errorClass: 'text-danger'
          }
        }
      }
      Vue.createApp(app).mount('#app')
    </script>
  </body>
</html>
```

