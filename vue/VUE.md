## VUE3

### 创建Vue实例

<!-- 通过 createApp 来创建新的应用实例。传入 createApp的组件叫做根组件。应用实例必须调用.mount()才能被渲染出来。 -->

```js
import { createApp } from 'vue'
import App from './app.vue'
import router from './router'

const app = createApp(App)
// 表示将id为app的节点挂在到vue上。
app.mount('#app')
// 通过.config可以做一些应用级的配置
app.config.errorHandler = (err) => {
  /* 处理错误 */
}
// 注册组件（一次注册一个组件）
app.component('hello', 'hello')
// 注册插件（带install方法的对象或将被用作install方法的函数）
app.use(router)
```

### 数据绑定

<!-- 数据绑定的形式是文本插值，使用双大括号，值会动态更新 -->

```html
<template>
  <span>Message: {{ msg }}</span>
  <!-- 双大括号是纯文本，v-html支持插入html并保留样式，请谨慎使用v-html -->
  <span v-html="msg"></span>
</template>
```

### attribute（属性）绑定

<!-- attributed绑定：使用v-bind:，简写为: -->

```html
<template>
  <!-- 如果dId为null或undefined时,attribute(id)将从渲染元素上移除 -->
  <div v-bind:id="dId"></div>
  <div :id="dId"></div>

  <!-- attribute的名称与绑定的值相同时，可以简化语法 -->
  <div :id="id"></div>
  <div :id></div>

  <!-- 动态绑定多个值 const objectOfAttrs = { id: 'container', class: 'wrapper' } -->
  <div v-bind="objectOfAttrs"></div>

  <!-- 使用JavaScript表达式 -->
  <div :id="`list-${id}`"></div>
  <span>Message: {{ msg + 1 }}</span>
</template>
```

### 事件绑定

<!-- 事件绑定：使用v-on:,简写为@ -->

```html
<template>
  <!-- 基本用法 -->
  <a v-on:click="doSomething"> ... </a>
  <a @click="doSomething"> ... </a>

  <!-- 内联事件处理器 const count = ref(0) -->
  <button @click="count++">Add 1</button>
  <!-- 方法事件处理器 function greet(event) { alert(event.target.tagName) } -->
  <button @click="greet">Greet</button>

  <!-- 参数 function say(message) { alert(message) } -->
  <button @click="say('bye')">Say bye</button>

  <!-- 事件修饰符 -->
  <!-- 单击事件将停止传递 -->
  <a @click.stop="doThis"></a>
  <!-- 提交事件将不再重新加载页面 -->
  <form @submit.prevent="onSubmit"></form>
  <!-- 修饰语可以使用链式书写 -->
  <a @click.stop.prevent="doThat"></a>
  <!-- 也可以只有修饰符 -->
  <form @submit.prevent></form>
  <!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
  <!-- 例如：事件处理器不来自子元素 -->
  <div @click.self="doThat">...</div>
  <!-- 添加事件监听器时，使用 `capture` 捕获模式 -->
  <!-- 例如：指向内部元素的事件，在被内部元素处理前，先被外部处理 -->
  <div @click.capture="doThis">...</div>
  <!-- 点击事件最多被触发一次 -->
  <a @click.once="doThis"></a>
  <!-- 滚动事件的默认行为 (scrolling) 将立即发生而非等待 `onScroll` 完成 -->
  <!-- 以防其中包含 `event.preventDefault()` -->
  <div @scroll.passive="onScroll">...</div>

  <!-- // 按键修饰符 -->
  <!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
  <input @keyup.enter="submit" />
</template>
```

### 动态参数

```html
<!-- attributeName值为 "href"，那么这个绑定就等价于 v-bind:href。 -->
<a v-bind:[attributeName]="url"> ... </a>
<!-- 简写为 -->
<a :[attributeName]="url">...</a>

<!-- // eventName值为 "focus"，那么这个绑定就等价于 v-on:focus。 -->
<a v-on:[eventName]="doSomething"> ... </a>
<a @[eventName]="doSomething"> ... </a>
```

### v-for v-if v-show

```html
<template>
  <!-- v-if v-else v-else-if -->
  <div v-if="seen">v-if的使用</div>
  <div v-else-if="seen2">v-else-if的使用</div>
  <div v-else>v-else的使用</div>

  <!-- <template>是一个不可见的包装器元素,不会被渲染出来 -->
  <!-- v-if 只能控制一个元素,如果同时控制多个父元素使用<template> -->
  <template v-if="seen">
    <div>hello</div>
    <div>world</div>
  </template>

  <!-- v-show -->
  <div v-show="seen">v-show的使用</div>

  <!-- v-for -->
  <!-- key为每个元素提供一个唯一的值,应该始终设置 -->
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
  <li v-for="(item, index) in items" :key="index">{{ index }} - {{ item.message }}</li>

  <!-- 遍历对象所有属性,遍历顺序基于该对象调用Object.keys()的返回值决定 -->
  <!-- const myObj = reactive(title: 'MyObject', author: 'Jane', time: '2024-05-14') -->
  <li v-for="(value, key, index) in myObj">{{ key }} + {{ value }}</li>

  <!-- v-for接受一个整数值, n是从1开始而非0 -->
  <div v-for="n in 10">{{ n }}</div>

  <!-- v-if和v-show的区别 -->
  <!-- v-if是真正的条件渲染,条件满足则渲染元素不满足则不渲染; v-show不管条件如何都会渲染元素,只有条件满足时才会显示. -->
  <!-- 如果频繁切换使用v-show,否则使用v-if-->
  <!-- v-show不能在<template>上使用,因为<template>不会被渲染上 -->

  <!-- v-if和v-for同时使用 -->
  <!-- v-if优先级比v-for更高,会优先判断v-if条件,v-if无法使用v-for的属性值,下面这种写法是错误的 -->
  <li v-for="todo in todos" v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
  <!-- 可以在外包装一层<template>,在使用v-for -->
  <template v-for="todo in todos">
    <li v-if="!todo.isComplete">
      {{ todo.name }}
    </li>
  </template>
</template>
```

### 响应式声明

```html
<!-- 响应式声明:ref() 和 reactive() -->

<!-- ref() -->
<!-- 类似flutter中的 var name = ''.obs; name.value = 'hello' -->
<script>
var name = ref('')
name.value = 'Tom'

const obj = ref({ nested: { count: 0 }, arr: ['foo', 'bar'] })
obj.value.nested.count++
</script>
<!-- 在模板中使用时不用加.value,因为在模板中会自动解包 -->
<template>
  <div>{{ name }}</div>
</template>

<!-- reactive -->
<script>
const state = reactive({ count: 0 })
state.count++
</script>

<!-- ref 和 reactive的区别 -->
<!-- ref和reactive都可以跟踪数据变化,并在UI上实时显示 -->
<!-- ref可以接受基础数据和对象作为参数, reactive只能接受对象作为参数 -->
<script>
const isSuccess = ref(false) // 有效
const isSuccess = reactive(false) // 无效

const json = ref({name : ''}) // 有效
const json = reactive(name : '') // 有效
</script>
<!-- ref通过.value访问,reactive可以直接访问 -->
<script>
const json1 = ref({name : ''}) // 有效
const json2 = reactive(name : '') // 有效

json1.value.name = 'Tom'
json2.name = 'Tom'
</script>
<!-- ref可以替换整个实例对象,reactive不可以 -->
<!-- ref创建的实例具有深层次响应性,reactive创建的实例不具有深层次响应性 -->
<script>
const state = reactive({ count: 0 })

// 解构，count后续的改变不会影响state
let { count } = state
count++

//该函数传入的是一个普通的数字,无法追踪state.count的变化，必须传入整个对象来保持响应性。
callSomeFunction(state.count)
</script>

<!-- 优先使用ref() -->
```

### 计算属性

```html
<!-- 为什么要用计算属性? -->
<!-- 模板中可以直接使用表达式，但是只能进行简单的操作，而且大量使用表达式会使模板变得臃肿 -->
<script>
const author = reactive({
  name: 'John',
  books: ['Vue 2 - Advanced Guide', 'Vue 3 - Basic Guide', 'Vue 4 - TheMystery']
})
</script>
<template>
  <span>{{ author.books.length > 0 ? 'No' : 'Yes' }}</span>
</template>

<!-- 计算属性的返回值是一个ref()实例 -->
<script>
cosnt booksIsEmpty = computed(() => {
    return author.books.length > 0 ? No : Yes
})

// 计算属性默认是只读的，可以通过setter让其可写，但应尽量不要这样操作
const firstName = ref('john')
const lastName = ref('Doe')
const fullName = computed({
    get() {
        return firstName.value + lastName.value
    }
    set(value) {
        [firstName.value, lastName.value] = value.split(' ')
    }
})
</script>

<!-- 计算属性和方法的区别 -->
<!-- 计算属性和方法的结果是相同的，但是计算属性的值会被缓存，一个计算属性只有在其响应式依赖变化时才会重新计算，而方法则是每次都要计算 -->
```

### class与style

```html
<!-- style的使用方式同class相同，这里只介绍class -->

<script>
const isActive = ref(true)
const hasError = ref(false)
const classObject = reactive({ active: true, 'text-danger': false })
const classObject2 = computed(() => ({ active: isActive.value, 'text-danger': hasError.value }))
const activeClass = ref('active')
const errorClass = ref('text-danger')
</script>

<template>
  <!-- class支持动态绑定， class与:class 可同时存在 -->
  <div class="static" :class="{ active: isActive, 'text-danger': hasError }">Hello</div>

  <!-- 直接绑定对象 -->
  <div :class="classObject"></div>

  <!-- 绑定计算属性 -->
  <div :class="classObject2"></div>

  <!-- 使用数组渲染多个class -->
  <div :class="[activeClass, errorClass]"></div>

  <!-- 数组中有条件渲染某个class -->
  <div :class="[isActive ? activeClass : '', errorClass]"></div>
  <div :class="[{ activeClass: isActive }, errorClass]"></div>
</template>
```

### 表单输入绑定

```html
<template>
  <input v-model="message" placeholder="edit me" />
  <textarea v-model="message" placeholder="add multiple lines"></textarea>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <input type="radio" id="one" value="One" v-model="picked" />
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
  </select>
</template>
```

### 生命周期

```html
<script>
// setup(组合式API)
// beforeCreated
// 初始化选项式API
// created
// beforeMount
// mounted
// beforeUpdate
// updated
// beforeUnmount
// unmounted
// 常用的时onMounted，onUpdated，onUnmounted
</script>
```

### watch

```html
<!-- watch 监听状态变化,并执行一些操作 -->
<template>
  <p>
    Ask a yes/no question:
    <input v-model="question" :disabled="loading" />
  </p>
  <p>{{ answer }}</p>
</template>

<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

// watch的第一个参数时数据源(ref(包括计算属性),响应式对象,getter函数,多个数据源组成的数组等)
// 这里监听question 的变化
watch(
  question,
  async (newQuestion, oldQuestion) => {
    if (newQuestion.includes('?')) {
      loading.value = true
      answer.value = 'Thinking...'
      try {
        const res = await fetch('https://yesno.wtf/api')
        answer.value = (await res.json()).answer
      } catch (error) {
        answer.value = 'Error! Could not reach the API. ' + error
      } finally {
        loading.value = false
      }
    }
  },
  // watch 是被动的,仅当数据源发生变化时才会执行, 可以通过immediate立即执行一次回调
  { immediate: true },
  // once 表示只监听一次
  { once: true }
)

// watch需要传入监听的数据源,可以使用watchEffect进行优化
// watchEffect只会监听回调中用到的属性
watchEffect(async () => {
  // todoId 的值发生变化后,重新请求接口
  const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${todoId.value}`)
  data.value = await response.json()
})
</script>
```

### 访问DOM元素

```html
<!-- 使用一个特殊的 attribute ref -->
<template>
  <input ref="input" />
</template>

<script setup>
import { ref, onMounted } from 'vue'

// 声明一个 ref 来存放该元素的引用
// 必须和模板里的 ref 同名
const input = ref(null)

onMounted(() => {
  input.value.focus()
})
</script>
```

### 切换组件

```html
<template>
  <!-- 在两个组件间来回切换,如tab -->
  <!-- 使用is 来在多个组件间切换时，被切换的组件会被卸载掉，可以通过<keepAlive>让其保持活跃 -->
  <Myconponent :is="tabs[currentTab]"></Myconponent>
</template>
```

### 组件注册

```html
<!-- 
全局注册：当前vue应用中都可使用
import MyComponent from './App.vue'

// 参数1：组件的名字 参数2：组件的实现
app.component('MyComponent', MyComponent)
-->

<!-- 局部注册： -->
<!-- 在使用 <script setup> 的单文件组件中，导入的组件可以直接在模板中使用，无需注册： -->
<script setup>
import ComponentA from './ComponentA.vue'
</script>

<template>
  <ComponentA />
</template>
```

### Props

```html
<!-- Props的数据传递是单项的，从父组件传到子组件，不能在子组件中修改props的值 -->
<!-- 在使用<script setup> 的单文件组件中，props 可以使用 defineProps() 宏来声明： -->
<script setup>
const props = defineProps({ title: String, likes: Number })
console.log(props.title)
</script>

<template>
  <!-- 静态传值和动态传值 -->
  <BlogPost title="My journey with Vue" />
  <BlogPost :title="post.title" />
</template>

<!-- 将对象的所有属性作为props传入，可以使用没有参数的v-bind  -->
<script>
const post = { id: 1, title: 'My Journey with Vue' }
</script>
<template>
  <BlogPost v-bind="post" />
  // 等价与
  <BlogPost :id="post.id" :title="post.title" />
</template>

<!-- props的一些使用 -->
<script>
// 可以对传入的props的值进行校验
defineProps({
  // 基础类型检查 // （给出 `null` 和 `undefined`值则会跳过任何类型检查）
  propA: Number,
  // 多种可能的类型
  propB: [String, Number],
  // 必传，且为String 类型
  propC: { type: String, required: true },
  // 必传但可为空的字符串
  propD: { type: [String, null], required: true },
  // Number 类型的默认值
  propE: { type: Number, default: 100 },
  //对象类型的默认值
  propF: {
    type: Object,
    // 对象或数组的默认值 // 必须从一个工厂函数返回。
    //该函数接收组件所接收到的原始 prop 作为参数。
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  //自定义类型校验函数
  // 在 3.4+ 中完整的 props 作为第二个参数传入
  propG: {
    validator(value, props) {
      // The value must match one of these strings
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // 函数类型的默认值
  propH: {
    type: Function,
    // 不像对象或数组的默认，这不是一个
    //工厂函数。这会是一个用来作为默认值的函数
    default() {
      return 'Default function'
    }
  }
})
</script>
```

### emit

```html
<!-- 通过$emit由子组件向父组件传递消息 -->

<!-- 1. 父组件通过v-on来监听事件 -->
<MyComponent @some-event="callback" />

<!-- 子组件通过$emit来触发自定义事件，这样父组件的callback就会收到消息 -->
<!-- MyComponent -->
<button @click="$emit('someEvent')">Click Me</button>
<!-- 可以带参数值 -->
<button @click="$emit('someEvent'， 1)">Click Me</button>


<!-- 还可以参考props的方式将父组件的事件传递过来 -->
<script setup>
const emit = defineEmits(['inFocus', 'submit'])
function buttonClick() {
  emit('submit')
}
//同理可以为emit添加校验
</script>
```

19. 组件的v-model

```html
<!-- Child.vue -->
<!-- 子组件中定义一个defineModel() -->
<script setup>
// defineModel返回值是一个ref
const model = defineModel()
function update() {
  model.value++
}
</script>
<template>
  <div>Parent bound v-model is: {{ model }}</div>
</template>

<!-- Parent.vue -->
<!-- 父组件可以用 v-model 绑定一个ref() 对象 -->
<Child v-model="countModel" />

<!-- 子组件的 model.value 和父组件的 countModel的值同步，并且一起更新 -->
```

20. <slot>

```html
<!-- 如何向子组件传递模板片段并展示？ -->

// 父组件
<FancyButton>
  Click me! <!-- 插槽内容 -->
</FancyButton>

<!-- FancyButton -->
<button class="fancy-btn">
  <slot></slot> <!-- 插槽出口 -->
</button>

<!-- 最终展现的结果 -->
<button class="fancy-btn">Click me!</button>

<!-- 插槽的内容不局限于文本，可以是任何合法的模板内容（可以有多个元素，甚至组件） -->
<!-- 如果组件中有多个插槽<slot>，需要为他们命名，以区分开来 -->
<!-- BaseLayout -->
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

<!-- 父组件，v-solt可以缩写为# -->
<BaseLayout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <template #default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</BaseLayout>

<!-- 条件插槽，可以根据插槽的名字来渲染不同的样式 -->
<template>
  <div class="card">
    <div v-if="$slots.header" class="card-header">
      <slot name="header" />
    </div>

    <div v-if="$slots.default" class="card-content">
      <slot />
    </div>

    <div v-if="$slots.footer" class="card-footer">
      <slot name="footer" />
    </div>
  </div>
</template>

<!-- 插槽正常是无法访问子组件的状态的，但是可以参考props那样给插槽传递attributes： -->
<!-- <MyComponent> 的模板 -->
<div>
  <slot :text="greetingMessage" :count="1"></slot>
</div>

<MyComponent v-slot="slotProps">
  {{ slotProps.text }} {{ slotProps.count }}
</MyComponent>

```

21. 依赖注入

通常情况下从父组件向子组件传递数据用props即可，但是如果中间有多层级嵌套的组件，用props传递起来就很麻烦了。

通过Provide和Inject来解决这个问题

```html
<script setup>
import { provide } from 'vue'
// 提供数据provide可以多次调用provide，来提供不同的值，除了在组件中使用也可以在整个app使用 app.provide()
provide(/* 注入名 */ 'message', /* 值 */ 'hello!')
</script>

<!-- 接受上传提供的数据 -->
<script setup>
import { inject } from 'vue'

const message = inject('message')
</script>

<!-- 如果传递的值是一个ref数据，并且要对其进行修改，可以将修改数据的方法一起传递过去 -->

<!-- 在供给组件内 -->
<script setup>
import { provide, ref } from 'vue'

const location = ref('North Pole')
function updateLocation() {
  location.value = 'South Pole'
}

provide('location', {
  location,
  updateLocation
})
</script>

<!-- 在后代组件 -->
<script setup>
import { inject } from 'vue'

const { location, updateLocation } = inject('location')
</script>

<template>
  <button @click="updateLocation">{{ location }}</button>
</template>

<!-- 如果要只读，不能修改可以使用readonly -->
<script setup>
import { ref, provide, readonly } from 'vue'

const count = ref(0)
provide('read-only-count', readonly(count))
</script>
```
