# vue 面试题汇总

**1、active-class 是哪个组件的属性？嵌套路由怎么定义**

　　(1)、active-class 是 vue-router 模块的 router-link 组件的属性
　　(2)、使用 children 定义嵌套路由

**2、怎么定义 vue-router 的动态路由? 怎么获取传过来的值**

　　在 router 目录下的 index.js 文件中，对 path 属性加上 /:id。

　　使用 router 对象的 params.id 获取

**3、vue-router 有哪几种导航钩子?**

　　三种，

　　(1)、全局导航钩子

　　　　router.beforeEach(to, from, next), 

　　　　router.beforeResolve(to, from, next), 

　　　　router.afterEach(to, from ,next)

　　(2)、组件内钩子
　　　　
　　　　beforeRouteEnter, beforeRouteUpdate, beforeRouteLeave

　　(3)、单独路由独享组件

　　　　beforeEnter

**4、v-model 是什么？怎么使用？ vue中标签怎么绑定事件**

　　v-model 可以实现双向绑定，

　　绑定事件：<input @click="doLog" />

**5、axios 是什么？怎么使用？描述使用它实现登录功能的流程**

　　axios 是请求后台资源的模块。 npm i axios -S

　　如果发送的是跨域请求，需在配置文件中 config/index.js 进行配置

**6、vuex 是什么？怎么使用？哪种功能场景使用它**

　　vuex 是专门为 vue 开发的数据状态管理模式。组件之间数据状态共享

　　使用场景：音乐播放、登录状态、购物车

	// 新建 store.js
	import vue from 'vue'
	import vuex form 'vuex'
	vue.use(vuex)
	export default new vuex.store({
		//...code
	})
	 
	//main.js
	import store from './store'
	...

**7、mvvm 框架是什么？它和其他框架(jquery) 的区别是什么？哪些场景适合**

　　mvvm 是 model + view + viewmodel 框架，通过 viewmodel 连接数据模型model 和 view

　　区别：vue 是数据驱动，通过数据来显示视图层而不是节点操用

　　场景：数据操作比较多的场景，更加快捷

**8、自定义指令(v-check, v-focus) 的方法有哪些? 它有哪些钩子函数? 还有哪些钩子函数参数**

　　全局定义指令：在 vue 对象的 directive 方法里面有两个参数, 一个是指令名称, 另一个是函数。

　　组件内定义指令：directives

　　钩子函数: bind(绑定事件出发)、inserted(节点插入时候触发)、update(组件内相关更新)

　　钩子函数参数： el、binding

**9、说出至少 4 种 vue 当中的指令和它的用法**

　　v-if(判断是否隐藏)、v-for(把数据遍历出来)、v-bind(绑定属性)、v-model(实现双向绑定)

**10、vue-router 是什么?它有哪些组件**

　　vue-router 是 vue 的路由插件,

　　组件：router-link router-view

**11、vue 的双向绑定的原理是什么**

　　vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

　　具体步骤：

　　第一步：需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 
这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

　　第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

　　第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:

　　1、在自身实例化时往属性订阅器(dep)里面添加自己

　　2、自身必须有一个update()方法

　　3、待属性变动dep.notice()通知时，能调用自身的 update() 方法，并触发Compile中绑定的回调，则功成身退。

　　第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

**12、请详细说下你对vue生命周期的理解**

　　总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

　　**创建前/后** 

　　在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。

　　在created阶段，vue实例的数据对象data有了，$el还没有。

　　**载入前/后**

　　在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。

　　在mounted阶段，vue实例挂载完成，data.message成功渲染。

　　**更新前/后**

　　当data变化时，会触发beforeUpdate和updated方法。

　　**销毁前/后**

　　在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在

## vuex 面试题 ##

**1、有哪几种属性**

　　有 5 种，分别是 state、getter、mutation、action、module

**2、vuex 的 store 特性是什么**

　　(1) vuex 就是一个仓库，仓库里放了很多对象。其中 state 就是数据源存放地，对应于一般 vue 对象里面的 data

　　(2) state 里面存放的数据是响应式的，vue 组件从 store 读取数据，若是 store 中的数据发生改变，依赖这相数据的组件也会发生更新

　　(3) 它通过 mapState 把全局的 state 和 getters 映射到当前组件的 computed 计算属性

**3、 vuex 的 getter 特性是什么**

　　(1) getter 可以对 state 进行计算操作，它就是 store 的计算属性

　　(2) 虽然在组件内也可以做计算属性，但是 getters 可以在多给件之间复用

　　(3) 如果一个状态只在一个组件内使用，是可以不用 getters

**4、vuex 的 mutation 特性是什么**

　　action 类似于 muation, 不同在于：action 提交的是 mutation,而不是直接变更状态

　　action 可以包含任意异步操作

**5、vue 中 ajax 请求代码应该写在组件的methods中还是vuex 的action中**

　　如果请求来的数据不是要被其他组件公用，仅仅在请求的组件内使用，就不需要放入 vuex 的 state 里

　　如果被其他地方复用，请将请求放入 action 里，方便复用，并包装成 promise 返回

**5、不用 vuex 会带来什么问题**

　　可维护性会下降，你要修改数据，你得维护3个地方

　　可读性下降，因为一个组件里的数据，你根本就看不出来是从哪里来的

　　增加耦合，大量的上传派发，会让耦合性大大的增加，本来Vue用Component就是为了减少耦合，现在这么用，和组件化的初衷相背

## 生命周期面试题 ##

**1、什么是 vue 生命周期**

　　vue 实例从创建到销毁的过程就是生命周期。

　　也就是从开始创建、初始化数据、编译模板、挂在 dom -> 渲染、更新 -> 渲染、写在等一系列过程

**2、vue生命周期的作用是什么**

　　生命周期中有多个事件钩子，让我们在控制整个 vue 实例的过程时更容易形成好的逻辑

**3、vue生命周期总共有几个阶段**

　　8个阶段：创建前/后、载入前/后、更新前/后、销毁前/后

**4、第一次页面加载会触发哪几个钩子**

　　第一次加载会触发 beforeCreate、created、beforeMount、mounted

**5、DOM 渲染在哪个周期中就已经完成**

　　mounted

**6、简述每个周期具体适合哪些场景**

　　生命周期钩子的一些使用方法： 

　　beforecreate : 可以在这加个loading事件，在加载实例时触发 

　　created : 初始化完成时的事件写在这里，如在这结束loading事件，异步请求也适宜在这里调用 

　　mounted : 挂载元素，获取到DOM节点 updated : 如果对数据统一处理，在这里写上相应函数

　　beforeDestroy : 可以做一个确认停止事件的确认框 nextTick : 更新数据后立即操作dom

# Vue

### 1 对于MVVM的理解

> `MVVM` 是 `Model-View-ViewModel` 的缩写

- `Model` 代表数据模型，也可以在`Model`中定义数据修改和操作的业务逻辑。
- `View` 代表`UI` 组件，它负责将数据模型转化成`UI` 展现出来。
- `ViewModel` 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 `Model`的对象，连接`Model`和`View`

> - 在`MVVM`架构下，`View `和 `Model` 之间并没有直接的联系，而是通过`ViewModel`进行交互，`Model `和 `ViewModel` 之间的交互是双向的， 因此`View` 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到`View` 上。
> - `ViewModel` 通过双向数据绑定把 `View` 层和 `Model `层连接了起来，而`View `和 `Model` 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM，不需要关注数据状态的同步问题，复杂的数据状态维护完全由 `MVVM` 来统一管理

### 2 请详细说下你对vue生命周期的理解

> 答：总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后

- 创建前/后： 在`beforeCreate`阶段，`vue`实例的挂载元素`el`和数据对象`data`都为`undefined`，还未初始化。在`created`阶段，`vue`实例的数据对象`data`有了，el还没有
- 载入前/后：在`beforeMount`阶段，`vue`实例的`$el`和`data`都初始化了，但还是挂载之前为虚拟的`dom`节点，`data.message`还未替换。在`mounted`阶段，`vue`实例挂载完成，`data.message`成功渲染。
- 更新前/后：当`data`变化时，会触发`beforeUpdate`和`updated`方法
- 销毁前/后：在执行`destroy`方法后，对`data`的改变不会再触发周期函数，说明此时`vue`实例已经解除了事件监听以及和`dom`的绑定，但是`dom`结构依然存在

**什么是vue生命周期？**

- 答： Vue 实例从创建到销毁的过程，就是生命周期。从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、销毁等一系列过程，称之为 Vue 的生命周期。

**vue生命周期的作用是什么？**

- 答：它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。

**vue生命周期总共有几个阶段？**

- 答：它可以总共分为`8`个阶段：创建前/后、载入前/后、更新前/后、销毁前/销毁后。

**第一次页面加载会触发哪几个钩子？**

- 答：会触发下面这几个`beforeCreate`、`created`、`beforeMount`、`mounted` 。

**DOM 渲染在哪个周期中就已经完成？**

- 答：`DOM` 渲染在 `mounted` 中就已经完成了

### 3 Vue实现数据双向绑定的原理：Object.defineProperty()

- `vue`实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过 `Object.defineProperty()` 来劫持各个属性的`setter`，`getter`，在数据变动时发布消息给订阅者，触发相应监听回调。当把一个普通 `Javascript` 对象传给 Vue 实例来作为它的 `data` 选项时，Vue 将遍历它的属性，用 `Object.defineProperty()` 将它们转为 `getter/setter`。用户看不到 `getter/setter`，但是在内部它们让 `Vue `追踪依赖，在属性被访问和修改时通知变化。
- vue的数据双向绑定 将`MVVM`作为数据绑定的入口，整合`Observer`，`Compile`和`Watcher`三者，通过`Observer`来监听自己的`model`的数据变化，通过`Compile`来解析编译模板指令（`vue`中是用来解析 `{{}}`），最终利用`watcher`搭起`observer`和`Compile`之间的通信桥梁，达到数据变化 —>视图更新；视图交互变化（`input`）—>数据`model`变更双向绑定效果。

### 4 Vue组件间的参数传递

**父组件与子组件传值**

> 父组件传给子组件：子组件通过`props`方法接受数据；

- 子组件传给父组件： `$emit` 方法传递参数

**非父子组件间的数据传递，兄弟组件传值**

> `eventBus`，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适（虽然也有不少人推荐直接用`VUEX`，具体来说看需求）

### 5 Vue的路由实现：hash模式 和 history模式

- `hash`模式：在浏览器中符号`“#”`，#以及#后面的字符称之为`hash`，用 `window.location.hash` 读取。特点：`hash`虽然在`URL`中，但不被包括在`HTTP`请求中；用来指导浏览器动作，对服务端安全无用，`hash`不会重加载页面。
- `history`模式：h`istory`采用`HTML5`的新特性；且提供了两个新方法： `pushState()`， `replaceState()`可以对浏览器历史记录栈进行修改，以及`popState`事件的监听到状态变更

### 5 vue路由的钩子函数

> 首页可以控制导航跳转，`beforeEach`，`afterEach`等，一般用于页面`title`的修改。一些需要登录才能调整页面的重定向功能。

- `beforeEach`主要有3个参数`to`，`from`，`next`。
- `to`：`route`即将进入的目标路由对象。
- `from`：`route`当前导航正要离开的路由。
- `next`：`function`一定要调用该方法`resolve`这个钩子。执行效果依赖n`ext`方法的调用参数。可以控制网页的跳转

### 6 vuex是什么？怎么使用？哪种功能场景使用它？

- 只用来读取的状态集中放在`store`中； 改变状态的方式是提交`mutations`，这是个同步的事物； 异步逻辑应该封装在`action`中。
- 在`main.js`引入`store`，注入。新建了一个目录`store`，`… export`
- **场景有**：单页应用中，组件之间的状态、音乐播放、登录状态、加入购物车

![vuex](https://upload-images.jianshu.io/upload_images/1480597-ad276e57b4a6e555.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- `state`：`Vuex` 使用单一状态树,即每个应用将仅仅包含一个`store` 实例，但单一状态树和模块化并不冲突。存放的数据状态，不可以直接修改里面的数据。
- `mutations`：`mutations`定义的方法动态修改`Vuex` 的 `store` 中的状态或数据
- `getters`：类似`vue`的计算属性，主要用来过滤一些数据。
- `action`：`actions`可以理解为通过将`mutations`里面处里数据的方法变成可异步的处理数据的方法，简单的说就是异步操作数据。`view` 层通过 `store.dispath` 来分发 `action`

![image.png](https://upload-images.jianshu.io/upload_images/1480597-0db932c9f1a54213.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> `modules`：项目特别复杂的时候，可以让每一个模块拥有自己的`state`、`mutation`、`action`、`getters`，使得结构非常清晰，方便管理

![image.png](https://upload-images.jianshu.io/upload_images/1480597-d8897c808f913010.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 7 v-if 和 v-show 区别

- 答：`v-if`按照条件是否渲染，`v-show`是`display`的`block`或`none`；

### 8 `$route`和`$router`的区别

- `$route`是“路由信息对象”，包括`path`，`params`，`hash`，`query`，`fullPath`，`matched`，`name`等路由信息参数。
- 而`$router`是“路由实例”对象包括了路由的跳转方法，钩子函数等

### 9 如何让CSS只在当前组件中起作用?

> 将当前组件的`<style>`修改为`<style scoped>`

### 10 `<keep-alive></keep-alive>`的作用是什么?

- `<keep-alive></keep-alive>` 包裹动态组件时，会缓存不活动的组件实例,主要用于保留组件状态或避免重新渲染

> 比如有一个列表和一个详情，那么用户就会经常执行打开详情=>返回列表=>打开详情…这样的话列表和详情都是一个频率很高的页面，那么就可以对列表组件使用`<keep-alive></keep-alive>`进行缓存，这样用户每次返回列表的时候，都能从缓存中快速渲染，而不是重新渲染

### 11 指令v-el的作用是什么?

> 提供一个在页面上已存在的 `DOM `元素作为 `Vue `实例的挂载目标.可以是 CSS 选择器，也可以是一个 `HTMLElement` 实例,

### 12 在Vue中使用插件的步骤

- 采用`ES6`的`import ... from ...`语法或`CommonJS`的`require()`方法引入插件
- 使用全局方法`Vue.use( plugin )`使用插件,可以传入一个选项对象`Vue.use(MyPlugin, { someOption: true })`

### 13 请列举出3个Vue中常用的生命周期钩子函数?

- `created`: 实例已经创建完成之后调用,在这一步,实例已经完成数据观测, 属性和方法的运算, `watch/event`事件回调. 然而, 挂载阶段还没有开始, `$el`属性目前还不可见
- `mounted`: `el`被新创建的 `vm.$el` 替换，并挂载到实例上去之后调用该钩子。如果 `root` 实例挂载了一个文档内元素，当 `mounted `被调用时 `vm.$el` 也在文档内。
- `activated`: `keep-alive`组件激活时调用

### 14 vue-cli 工程技术集合介绍

**问题一：构建的 vue-cli 工程都到了哪些技术，它们的作用分别是什么？**

- `vue.js`：`vue-cli`工程的核心，主要特点是 双向数据绑定 和 组件系统。
- `vue-router`：`vue`官方推荐使用的路由框架。
- `vuex`：专为 `Vue.js` 应用项目开发的状态管理器，主要用于维护`vue`组件间共用的一些 变量 和 方法。
- `axios`（ 或者 `fetch` 、`ajax` ）：用于发起 `GET` 、或 `POST` 等 `http`请求，基于 `Promise` 设计。
- `vuex`等：一个专为`vue`设计的移动端`UI`组件库。
- 创建一个`emit.js`文件，用于`vue`事件机制的管理。
- `webpack`：模块加载和`vue-cli`工程打包器。

**问题二：vue-cli 工程常用的 npm 命令有哪些？**

- 下载 `node_modules` 资源包的命令：

```
npm install
```

- 启动 `vue-cli` 开发环境的 npm命令：

```
npm run dev
```

- `vue-cli` 生成 生产环境部署资源 的 `npm`命令：

```
npm run build
```

- 用于查看 `vue-cli` 生产环境部署资源文件大小的 `npm`命令：

```
npm run build --report
```

> 在浏览器上自动弹出一个 展示 `vue-cli` 工程打包后 `app.js`、`manifest.js`、`vendor.js` 文件里面所包含代码的页面。可以具此优化 `vue-cli` 生产环境部署的静态资源，提升 页面 的加载速度

### 15 NextTick

> `nextTick `可以让我们在下次 DOM 更新循环结束之后执行延迟回调，用于获得更新后的 `DOM`

### 16 vue的优点是什么？

- 低耦合。视图（`View`）可以独立于`Model`变化和修改，一个`ViewModel`可以绑定到不同的`"View"`上，当View变化的时候Model可以不变，当`Model`变化的时候`View`也可以不变
- 可重用性。你可以把一些视图逻辑放在一个`ViewModel`里面，让很多`view`重用这段视图逻辑
- 可测试。界面素来是比较难于测试的，而现在测试可以针对`ViewModel`来写


### 17 路由之间跳转？

**声明式（标签跳转）**

```
<router-link :to="index">
```

**编程式（ js跳转）**

```
router.push('index')
```

### 18 实现 Vue SSR

![](http://7xq6al.com1.z0.glb.clouddn.com/vue-ssr.jpg)

**其基本实现原理**

- `app.js` 作为客户端与服务端的公用入口，导出 `Vue` 根实例，供客户端 `entry` 与服务端 `entry` 使用。客户端 `entry` 主要作用挂载到 `DOM` 上，服务端 `entry` 除了创建和返回实例，还进行路由匹配与数据预获取。
- `webpack` 为客服端打包一个 `Client Bundle` ，为服务端打包一个 `Server Bundle` 。
- 服务器接收请求时，会根据 `url`，加载相应组件，获取和解析异步数据，创建一个读取 `Server Bundle` 的 `BundleRenderer`，然后生成 `html` 发送给客户端。
- 客户端混合，客户端收到从服务端传来的 `DOM` 与自己的生成的 DOM 进行对比，把不相同的 `DOM` 激活，使其可以能够响应后续变化，这个过程称为客户端激活 。为确保混合成功，客户端与服务器端需要共享同一套数据。在服务端，可以在渲染之前获取数据，填充到 `stroe` 里，这样，在客户端挂载到 `DOM` 之前，可以直接从 `store `里取数据。首屏的动态数据通过 `window.__INITIAL_STATE__ `发送到客户端

> `Vue SSR` 的实现，主要就是把 `Vue` 的组件输出成一个完整 `HTML`, `vue-server-renderer` 就是干这事的

- `Vue SSR `需要做的事多点（输出完整 HTML），除了` complier -> vnode`，还需如数据获取填充至 `HTML`、客户端混合（`hydration`）、缓存等等。
相比于其他模板引擎（`ejs`, `jade` 等），最终要实现的目的是一样的，性能上可能要差点

### 19 Vue 组件 data 为什么必须是函数

- 每个组件都是 `Vue` 的实例。
- 组件共享 `data` 属性，当 `data` 的值是同一个引用类型的值时，改变其中一个会影响其他

### 20 Vue computed 实现

- 建立与其他属性（如：`data`、 `Store`）的联系；
- 属性改变后，通知计算属性重新计算

> 实现时，主要如下

- 初始化 `data`， 使用 `Object.defineProperty` 把这些属性全部转为 `getter/setter`。
- 初始化 `computed`, 遍历 `computed` 里的每个属性，每个 `computed` 属性都是一个 `watch` 实例。每个属性提供的函数作为属性的 `getter`，使用 `Object.defineProperty` 转化。
- `Object.defineProperty getter` 依赖收集。用于依赖发生变化时，触发属性重新计算。
- 若出现当前 `computed` 计算属性嵌套其他 `computed` 计算属性时，先进行其他的依赖收集


### 21 Vue complier 实现

- 模板解析这种事，本质是将数据转化为一段 `html` ，最开始出现在后端，经过各种处理吐给前端。随着各种 `mv*` 的兴起，模板解析交由前端处理。
- 总的来说，`Vue complier` 是将 `template` 转化成一个 `render` 字符串。

> 可以简单理解成以下步骤：

- `parse` 过程，将 `template` 利用正则转化成` AST` 抽象语法树。
- `optimize` 过程，标记静态节点，后 `diff` 过程跳过静态节点，提升性能。
- `generate` 过程，生成 `render` 字符串

### 22 怎么快速定位哪个组件出现性能问题

> 用 `timeline` 工具。 大意是通过 `timeline` 来查看每个函数的调用时常，定位出哪个函数的问题，从而能判断哪个组件出了问题



