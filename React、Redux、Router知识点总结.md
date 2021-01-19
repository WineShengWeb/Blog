# React、Redux、Router 知识总结

### React 基础知识点

#### React 概述

> React 是 facebook 于 2013 年 5 月开源的一个用于构建用户界面的 MVC 版 JS 框架，是 Facebook 的内部项目，用来架设 Instagram 的网站，其要解决的问题是构建数据不断变化的大型应用；
> MVC：Model(数据层)，View(视图层)，Controller(控制层)；
> 核心是组件，使用组件提高了代码的复用率，降低测试的难度和代码的复杂度；
> 核心思想：通过数据的改变来影响视图的渲染(数据驱动)。
> React 16 和 17 使用上的区别，模块中只使用到了 JSX 时，17 不需要在引入 React，16 还需要引入 React

#### React 特点

-   <b>声明式设计:</b> React 采用声明范式，可以轻松描述应用。
-   <b>高效:</b> React 通过对 DOM 的模拟，最大限度地减少与 DOM 的交互。
-   <b>灵活:</b> React 可以与已知的库或框架很好地配合。
-   <b>JSX:</b> JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。
-   <b>组件:</b> 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。
-   <b>单向响应的数据流:</b> React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

#### React 安装

-   CDN 引入:

```javascript
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<!-- 生产环境中不建议使用 -->
<script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
```

-   npm 安装:

```bash
npm install -g create-react-app
```

-   yarn 安装:

```bash
yarn global add create-react-app
```

#### 使用 React

```npm
create-react-app <项目名称>
cd <项目名称>
npm start
```

#### 项目目录

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js  项目的入口文件
    logo.svg
```

#### React 组件

React 组件分两种，一种是类组件，一种函数组件，在 React 16.7 之前 函数组件只能依赖父级进行更新。

-   类组件:
    1. 类组件必须继承自 Component
    2. 组件名首字母必须大写
    3. 类组件中必须有一个 render 方法，该方法的返回值，是当前组件要构建的视图
    4. 在组件中，有一个 state 属性，该属性中保存的是组件可变的数据，当 state 更新时，会引起 组件更新，从而改变视图
-   函数式组件：
    1. 函数的名称就是组件的名称
    2. 函数的返回值就是组件要渲染的内容
-   事件：
    1. react 中添加事件类似于 JS 的行间事件
    2. 事件名是驼峰命名
    3. 注意事件处理函数的 this 指向 undefined
       将 this 指向 组件实例:
        - 箭头函数
        - bind
-   更新状态：
    1. 在组件中要更新状态，需要调用实例的 setState 方法
    2. setState 本身接收一个参数是 对象的数据，该对象中，是更新后的 state

#### JSX 语法

JSX: react 的一个语法糖，JavaScript + XML 支持在 JS 中，扩展 XML 的语法

注意事项：

-   JSX 并不是字符串
-   JSX 是一个值，所以 JSX 中，必须有一个顶层（唯一）父级
    -   如果父级我们并不希望，在 DOM 中展示出来，可以使用 `Fragment` 组件或空标签`<></>`
-   JSX 区分大小写，标签要全部小写，组件的首字母要大写
-   JSX 标签必须闭合
-   SX 不是 html，很多属性在编写时不一样
    -   className
    -   style
-   列表渲染时，必须有 key 值

#### props 和 state

-   props 是一个父组件传递给子组件的数据流，这个数据流可以一直传递到子孙组件。而 state 代表的是一个组件内部自身的状态

    1. prop 用于定义外部接口，state 用于记录内部状态；
    2. prop 的赋值在外部世界使用组件时，state 的赋值在组件内部；
    3. 组件不应该改变 prop 的值，而 state 存在的目的就是让组件来改变的；

-   props 与 state 的区别：
    1.  state 的主要作用是用于组件保存、控制、修改*自己*的可变状态，在组件内部进行初始化，也可以在组件内部进行修改，但是组件外部不能修改组件的 state
    2.  props 的主要作用是让使用该组件的父组件可以传入参数来配置该组件，它是外部传进来的配置参数，组件内部无法控制也无法修改
    3.  state 和 props 都可以决定组件的外观和显示状态。通常，props 做为不变数据或者初始化数据传递给组件，可变状态使用 state

#### 注释

-   注释需要写在花括号中
    -   在标签内部的注释需要花括号
    -   在标签外的的注释不能使用花括号

例如：

```js
ReactDOM.render(
    /*注释 */
    {/* 注释 */}
    <h1>Hello World {/*注释*/}</h1>,
    document.getElementById("example")
);
```

#### state 和 setState

-   setState(updater, [callback])
    -   updater: 更新数据 FUNCTION/OBJECT
    -   callback: 更新成功后的回调 FUNCTION
    -   异步: react 通常会集齐一批需要更新的组件，然后一次性更新来保证渲染的性能
    -   浅合并 Objecr.assign()，通过 setState 修改状态时，只需要传入要修改的 state 即可，setState 会帮助我们进行浅合并，将 修改 sttae 合并入 组件的 state 中。
    -   调用 setState 之后，会触发生命周期，重新渲染组件

#### 组件通信

-   组件间通信
    在 React.js 中，数据是从上自下流动（传递）的，也就是一个父组件可以把它的 state / props 通过 props 传递给它的子组件，但是子组件不能修改 props - React.js 是单向数据流，如果子组件需要修改父组件状态（数据），是通过回调函数方式来完成的。
    -   父级向子级通信
        把数据添加子组件的属性中，然后子组件中从 props 属性中，获取父级传递过来的数据
    -   子级向父级通信
        在父级中定义相关的数据操作方法(或其他回调), 把该方法传递给子级，在子级中调用该方法父级传递消息

#### React 生命周期

生命周期，16.3 之前，16.3, 16.4 及之后

-   mount 挂载阶段--- 组件从初始化到真实渲染到 DOM 中（组件创建-->把组件创建的虚拟 DOM，生成真实 DOM，添加到我们的 DOM 树中）：
    -   constructor 组件初始化
    -   static getDerivedStateFromProps(props)
        -   注意 this 问题
    -   render
    -   componentDidMount -- 处理副作用(请求)
-   update 更新阶段 --从 setState 之后组件开始更新，一直完成对真实的 DOM 节点更新(组件重新渲染)：
    -   static getDerivedStateFromProps(props, state)
    -   shouldComponentUpdate() -- 判断是否更新
    -   render()
    -   getSnapshotBeforeUpdate()
    -   componentDidUpdate() -- 处理副作用(请求)
-   unmount 卸载阶段
    -   componentWillUnmount -- 删除添加在全局的一些信息或操作

#### keys 的作用

> keys 是 react 用于追踪列表元素被修改，添加或移除的标识，我们需要保证元素的 key 在同级元素的唯一性，react 的 diff 算法会根据 key 的值来判断该元素是新创建的还是移动的元素，减少不必要的渲染，增加性能

#### refs 的作用

> refs 是 react 提供给我们的安全访问 dom 元素或者某个组件的实例化的句柄，我们可以为元素添加 ref 属性然后再回调函数中接受该元素在 dom 树种的句柄，该值会作为回调函数的第一个参数返回

#### 受控组件与 非受控组件的区别

> 受控组件（Controlled Component）代指那些交由 React 控制并且所有的表单数据统一存放的组件；非受控组件（Uncontrolled Component）则是由 DOM 存放表单数据，并非存放在 React 组件中。

#### React 组件 API（主要是以下 7 个方法）

-   设置状态：setState
-   替换状态：replaceState
-   设置属性：setProps
-   替换属性：replaceProps
-   强制更新：forceUpdate
-   获取 DOM 节点：findDOMNode
-   判断组件挂载状态：isMounted

### React hooks 基础知识点总结

#### React hooks(钩子)

React hooks 是 React 16.8 中的新增功能。它们使您无需编写类即可使用状态和其他 React 功能

##### 常用 hook

-   hooks 使用注意事项：
    1. hooks 要保障其调用顺序，所以必须在最外层使用(不能 if、for、子函数……等)
    2. hooks 只能在 react 函数中调用
-   useState  
     `const [state, setState] = useState(initialState);`
    let [状态,修改该状态的方法] = useState(初始值); 1. 在同一个组件中可以使用 useState 定义多个状态 2. 注意 useState 返回的 setState 方法，不会进行对象合并 3. 注意 useState 返回的 setState 方法同样是异步方法
-   useEffect
    类组件
    componentDidMount、componentDidUpdate 和 componentWillUnmount
    需要清除的副作用
-   useRef
    用户关联原生 DOM 节点，或者用来记录组件更新前的一些数据

##### React Hooks 优势

-   简化组件逻辑
-   复用状态逻辑
-   无需使用类组件编写

##### Hook 使用规则

-   只在 React 函数中调用 Hook
    -   React 函数组件中
    -   React 自定义 Hook 中
-   只在最顶层使用 Hook

##### useEffect 执行顺序

-   组件挂载阶段：
    1. 执行 useEffect 将 effect 函数存入队列
    2. 挂载完成之后，执行 effect 函数队列，并获取返回函数存入队列
-   组件更新阶段：
    1. 执行 useEffect 将 effect 函数存入队列
    2. 更新完成之后，先将返回函数队列执行: 在执行时会观察该 effect 是否有依赖参数，无依赖数据，直接执行，有依赖则追踪依赖是否改变，改变才执行，不变则不执行
    3. 执行新的 effect 函数存入队列: 在执行时会观察该 effect 是否有依赖参数，无依赖数据，直接执行，有依赖则追踪依赖是否改变，改变才执行，不变则不执行
-   卸载阶段：
    1. 将返回函数队列执行

useEffect 执行顺序：

```javascript
import { useEffect, useState } from "react";

function App() {
    const [count, setCount] = useState(0);
    const [name, setName] = useState("a");
    useEffect(() => {
        console.log("effect-1");
        return () => {
            console.log("effect 返还函数 - 1");
        };
    });
    useEffect(() => {
        console.log("effect-2");
        return () => {
            console.log("effect 返还函数 - 2");
        };
    }, []);
    useEffect(() => {
        console.log("effect-3");
        return () => {
            console.log("effect 返还函数 - 3");
        };
    }, [count]);
    console.log("render");
    return (
        <div>
            <p>{count}</p>
            <button
                onClick={() => {
                    setCount(count + 1);
                }}
            >
                递增
            </button>
            <p>{name}</p>
            <button
                onClick={() => {
                    setName(name + 1);
                }}
            >
                递增
            </button>
        </div>
    );
}
export default App;
```

### React Router 基础知识总结

#### react-router 路由的理解

react-router 是 react 的一个插件库，专门用来实现一个 SPA 应用，基于 react 的项目基本都会用到这个库。

react-router-dom 是应用程序中路由的库。 React 库中没有路由功能，需要单独安装 react-router-dom。

react-router-dom 提供两个路由器 BrowserRouter 和 HashRoauter。前者基于 url 的 pathname 段，后者基于 hash 段。

**SPA 理解**

SPA 指单页 Web 应用（single page web application，SPA），整个应用只有一个完整的页面（入口页面），点击页面中的链接不会刷新页面, 本身也不会向服务器发请求，当点击路由链接时, 只会做页面的局部更新，数据都需要通过 ajax 请求获取, 并在前端异步展现。

**优点：**

-   有更好的用户体验（减少请求和渲染和页面跳转产生的等待与空白），页面切换快
-   重前端，数据和页面内容由异步请求（AJAX）+ DOM 操作来完成，前端处理更多的业务逻辑

**缺点：**

-   首次进入处理慢
-   不利于 SEO

#### SPA 的页面切换机制

虽然 SPA 的内容都是在一个页面通过 JavaScript 动态处理的，但是还是需要根据需求在不同的情况下分内容展示，如果仅仅只是依靠 JavaScript 内部机制去判断，逻辑会变得过于复杂，通过把 JavaScript 与 URL 进行结合的方式：JavaScript 根据 URL 的变化，来处理不同的逻辑，交互过程中只需要改变 URL 即可。这样把不同 URL 与 JavaScript 对应的逻辑进行关联的方式就是路由，其本质上与后端路由的思想是一样的。

#### 路由的理解

-   路由：根据不同的 url 规则，给用户展示不同的视图(页面)。

**路由的分类**

-   后端路由：
    1. 注册路由: router.get(path, function(req, res))
    2. 当 node 接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据
-   前端路由
    1. 注册路由:
    2. 当浏览器的 hash 变为#about 时, 当前路由组件就会变为 About 组件

#### 前端路由

前端路由只是改变了 URL 或 URL 中的某一部分，但一定不会直接发送请求，可以认为仅仅只是改变了浏览器地址栏上的 URL 而已，JavaScript 通过各种手段处理这种 URL 的变化，然后通过 DOM 操作动态的改变当前页面的结构

-   URL 的变化不会直接发送 HTTP 请求
-   业务逻辑由前端 JavaScript 来完成

#### 基本使用

安装：

```bash
npm install react-router-dom --save
```

使用：

```javascript
import { BrowserRouter, Route, Link, Redirect } from "react-router-dom";

class MyRouter extends React.Component {
    render() {
        return (
            <BrowserRouter>
                {" "}
                <Link to="/">router1</Link> &nbsp;&nbsp; <Link to="/router2">
                    router2
                </Link> &nbsp;&nbsp; <Link to="/router3">router3</Link> &nbsp;&nbsp;{" "}
                <hr /> <Redirect exact from="/" to="/router1" />
                <Route path="/router1" component={router1}></Route>
                <Route path="/router2" component={router2}></Route>
                <Route path="/router3" component={router3}></Route>
            </BrowserRouter>
        );
    }
}
```

#### 路由跳转

**1、用 link 跳转：**

```javascript
import { BrowserRouter, Route, Link, Redirect } from "react-router-dom";

class MyRouter extends React.Component {
    render() {
        return (
            <BrowserRouter>
                {" "}
                <Link to="/">router1</Link> &nbsp;&nbsp; <Link to="/router2">
                    router2
                </Link> &nbsp;&nbsp; <Link to="/router3">router3</Link> &nbsp;&nbsp;{" "}
                <hr /> <Redirect exact from="/" to="/router1" />
                <Route path="/router1" component={router1}></Route>
                <Route path="/router2" component={router2}></Route>
                <Route path="/router3" component={router3}></Route>
            </BrowserRouter>
        );
    }
}
```

**2、编程式导航**

-   路由组件可以直接从 this.props.history 上拿到 history
-   非路由组件无法直接拿到 history，需要配合 withRouter

```javascript
this.props.history.push(url);
this.props.history.go(-1);
```

#### 路由传参

1、params 传参

```javascript
<Route path='/path/:name' component={Path}/>
<link to="/path/123">xxx</Link>

this.props.history.push({pathname:"/path/" + name});
// 读取参数用:this.props.match.params.name
```

2、query 传参

```js
<Route path='/query' component={Query}/>
<Link to={{ pathname : '/query' , query : { name : 'sunny' }}}></Link>

this.props.history.push({pathname:"/query",query: { name : 'sunny' }});
// 读取参数用:this.props.location.query.name
```

3、state 传参

```js
<Route path='/sort ' component={Sort}/>
<Link to={{ pathname : '/sort ' , state : { name : 'sunny' }}}></Link>

this.props.history.push({pathname:"/sort ",state : { name : 'sunny' }});
// 读取参数用: this.props.location.query.state
```

4、search 传参

```js
<Route path='/web/search ' component={Search}/>
<link to="web/search?id=12121212">xxx</Link>

this.props.history.push({pathname:`/web/search?id ${row.id}`});
// 读取参数用: this.props.location.searchs
```

#### Redux 基础知识点总结

-   Redux 是一个独立的 JavaScript 状态管理库，不依赖于任何其他库，提供可预测化的状态管理。
-   文档：https://www.redux.org.cn/

#### 安装 Redux

```bash
# npm 安装
npm i redux
# yarn 安装
yarn add redux
```

#### 核心概念

理解 Redux 核心几个概念与它们之间的关系

-   state 状态
-   reducer 纯函数 - 提供修改状态的方法
-   store 仓库 - 管理状态
    -   dispatch: ƒ dispatch(action) 发起一个 action
        -   调用 dispatch 之后，dispatch 会将通知 store 执行 reducer，并将 action 传递给 reducer
        -   dispatch 是同步方法
    -   getState: ƒ getState() 获取状态
    -   replaceReducer: ƒ replaceReducer(nextReducer)
    -   subscribe: ƒ subscribe(listener)
-   action 动作 - 对 state 的修改动作
    -   action 就是一个 JS 的普通对象
    -   action 必须有一个 type 属性，type 属性中，描述了要对 state 做何种修改
    -   潜规则：action 的 type 必须大写

#### Redux 三大原则

##### 单一数据源

**整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。**

```js
console.log(store.getState())

/* 输出
{
  visibilityFilter: 'SHOW_ALL',
  todos: [
    {
      text: 'Consider using Redux',
      completed: true,
    },
    {
      text: 'Keep all state in a single tree',
      completed: false
    }
  ]
}
*／
```

##### State 是只读的

**唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。**

```js
store.dispatch({
    type: "COMPLETE_TODO",
    index: 1,
});

store.dispatch({
    type: "SET_VISIBILITY_FILTER",
    filter: "SHOW_COMPLETED",
});
```

##### 使用纯函数来执行修改

**为了描述 action 如何改变 state tree ，你需要编写 reducers。**

-   纯函数
    1. 相同的输入永远返回相同的输出
    2. 不修改函数的输入值
    3. 不依赖外部环境状态
    4. 无任何副作用

使用纯函数的好处：

-   便于测试
-   有利重构

```js
function visibilityFilter(state = "SHOW_ALL", action) {
    switch (action.type) {
        case "SET_VISIBILITY_FILTER":
            return action.filter;
        default:
            return state;
    }
}

function todos(state = [], action) {
    switch (action.type) {
        case "ADD_TODO":
            return [
                ...state,
                {
                    text: action.text,
                    completed: false,
                },
            ];
        case "COMPLETE_TODO":
            return state.map((todo, index) => {
                if (index === action.index) {
                    return Object.assign({}, todo, {
                        completed: true,
                    });
                }
                return todo;
            });
        default:
            return state;
    }
}

import { combineReducers, createStore } from "redux";
let reducer = combineReducers({ visibilityFilter, todos });
let store = createStore(reducer);
```

#### action 对象

我们对 state 的修改是通过 reducer 纯函数来进行的，同时通过传入的 action 来执行具体的操作，action 是一个对象

-   type 属性 : 表示要进行操作的动作类型，增删改查……
-   payload 属性 : 操作 state 的同时传入的数据

但是这里需要注意的是，我们不直接去调用 Reducer 函数，而是通过 Store 对象提供的 dispatch 方法来调用

#### Store 对象

为了对 state，Reducer，action 进行统一管理和维护，我们需要创建一个 Store 对象

#### redux API

-   createStore(reducer, [preloadedState], enhancer);
    -   reducer (Function): 接收两个参数，分别是当前的 state 树和要处理的 action，返回新的 state 树。
    -   [preloadedState] (any): 初始时的 state。 在同构应用中，你可以决定是否把服务端传来的 state 后传给它，或者从之前保存的用户会话中恢复一个传给它。如果你使用 combineReducers 创建 - reducer，它必须是一个普通对象，与传入的 keys 保持同样的结构。否则，你可以自由传入任何 reducer 可理解的内容。
    -   enhancer (Function): Store enhancer 是一个组合 store creator 的高阶函数，返回一个新的强化过的 store creator。这与 middleware 相似，它也允许你通过复合函数改变 store 接口。
    -   返回值 (Store): 保存了应用所有 state 的对象。改变 state 的惟一方法是 dispatch action。你也可以 subscribe 监听 state 的变化，然后更新 UI。
-   reducer
    -   reducer(state,action)
-   Store

    -   getState()
    -   dispatch(action)
    -   subscribe(listener)
    -   replaceReducer(nextReducer)

-   combineReducers(reducers)
    将 reducer 函数拆分成多个单独的函数，拆分后的每个函数负责独立管理 state 的一部分

-   applyMiddleware(...middlewares) 中间件

#### react-redux

Redux 官方提供的 React 绑定库。 具有高效且灵活的特性。

安装：

```bash
npm install --save react-redux
```

-   Provider

Provider：将 redux 创建好的 store 传递给整个项目的其他组件，在项目中，哪个组件需要使用，就接收 store 的方法，会使用 或 修改 state

```js
<Provider store={store}>
    <App />
</Provider>
```

-   connect 方法

    1、方法声明：

    ```js
    connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options]);
    ```

    2、作用：
    连接 react 组件与 redux store

    3、书写位置：
    一般写在“与布局相关的组件中”

    4、原理：
    connect 之所以会成功，是因为 Provider 组件：首先，在原应用组件上包裹一层，使原来整个应用成为 Provider 的子组件；其次，接收 Redux 的 store 作为 props，通过 context 对象传递给子孙组件上的 connect。connect 真正连接 Redux 和 React，它包在我们的容器组件的外一层，它接收上面 Provider 提供的 store 里面的 state 和 dispatch，传给一个构造函数，返回一个对象，以属性形式传给我们的容器组件。

-   connect() -- 高阶函数:传入数据，返回一个函数
-   useDispatch 获取 dispatch
-   useStore 获取 store
-   useSelector 获取 state
