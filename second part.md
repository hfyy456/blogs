### CSS/HTML

#### 1.三角形的原理

boder-top, border-left,boder-right,boder-bottom

#### 2.BFC布局规则和nomal flow的区别 和常用触发条件

1.浮动元素是否会计入父级高度

2.触发了bfc的元素不会被浮动元素覆盖

3.margin是否会传递给父级（bfc的子元素margin会撑开父元素的高度）

4.bfc与其相邻上下元素的上下margin不会重叠

常用触发条件

1.position:absolute,fiexd

2.display:inline-block,table-cell、flex

3.overflow不为visible

4.浮动元素



### 计算机网络

#### 1.如何保证UDP的可靠传输？怎么实现？

ARQ，数据链路层错误纠正协议，停止等待ARQ协议和连续ARQ协议

#### 2.osi七层模型及对应的协议



### Javascript

#### 1.js原型&原型链



#### 2.jsonp实现原理

动态创建地创建script标签以发起请求，在src中填写请求的目标路径，并传入查询参数callback也就是回调函数的函数名。

服务器接收到请求时，会根据查询参数callback返回执行回调函数的语句，并在参数传入请求方想要的数据。

请求方接收到响应后就会执行这个语句也就是执行回调函数，这样请求方就能在回调函数中取得想要的数据。

#### 3.this指向

1.直接调用 window

2.构造函数 绑定在实例化的对象

3.箭头函数 与最外层非箭头函数this相同

4.当作属性调用 this指向对最后一个调用函数的对象

5.定时器内this指向  window 

6.优先级 new>call及其他两个函数>属性调用>直接调用 

#### 4.js常见的报错



### Node

#### 1.cluster

主要集成了两个⽅⾯，第⼀集成了 child_process.fork⽅法创建node⼦进程，第⼆集成了根据多核CPU创建⼦进程后，⾃动控制负载均衡。它是node本身的⼀个模块，⽤于多核CPU环境下多进程的负载均衡。cluster模块可创建共享服务器端⼝的⼦进程。 特点： 可以共享tcp连接 ⾃带负载均衡(内置⼀个负载均衡器，采⽤Round-robin算法协调各个worker进程之间的负载) 通过主进程监听端⼝和分发请求，⼦进程负责请求的处理

#### 2.多进程之间通信IPC的原理 句柄传递



#### 3.websocket握手

https://www.jianshu.com/p/8414d2efa087

#### 4.Express和koa2中间件使用的不同

koa2的中间件是通过 `async await` 实现的，中间件执行顺序是“洋葱圈”模型。

express中间件一个接一个的顺序执行, 通常会将 response 响应写在最后一个中间件中

### React

#### 1.纯函数

*一个函数的返回结果只依赖于它的参数，并且在执行过程里面没有副作用，我们就把这个函数叫做纯函数*。这么说肯定比较抽象，我们把它掰开来看：

1. 函数的返回结果只依赖于它的参数。
2. 函数执行过程里面没有副作用。

#### 2.hooks的限制，Effect清理

顺序调用、不能写在条件语句中、纯函数

#### 3.为什么React元素有一个$$typeof属性？

预防xxs

这是个有效的办法，因为JSON不支持 `Symbol` 类型。**所以即使服务器存在用JSON作为文本返回安全漏洞，JSON 里也不包含 `Symbol.for('react.element')`**。React 会检测 `element.$$typeof`，如果元素丢失或者无效，会拒绝处理该元素。

特意用 `Symbol.for()` 的好处是 **Symbols 通用于 iframes 和 workers 等环境中**。因此无论在多奇怪的条件下，这方案也不会影响到应用不同部分传递可信的元素。同样，即使页面上有很多个 React 副本，它们也 「接受」 有效的 `$$typeof` 值。

https://overreacted.io/zh-hans/why-do-react-elements-have-typeof-property/

#### 4.类组件和函数组件的区别和应用场景

https://overreacted.io/zh-hans/how-are-function-components-different-from-classes/

函数组件没有this,没有生命周期，没有状态state,

类组件有this,有生命周期，有状态state。

#### 5.React.memo 

`React.memo` 为[高阶组件](https://zh-hans.reactjs.org/docs/higher-order-components.html)。它与 [`React.PureComponent`](https://zh-hans.reactjs.org/docs/react-api.html#reactpurecomponent) 非常相似，但只适用于函数组件，而不适用 class 组件。

如果你的函数组件在给定相同 props 的情况下渲染相同的结果，那么你可以通过将其包装在 `React.memo` 中调用，以此通过记忆组件渲染结果的方式来提高组件的性能表现。这意味着在这种情况下，React 将跳过渲染组件的操作并直接复用最近一次渲染的结果。

`React.memo` 仅检查 props 变更。如果函数组件被 `React.memo` 包裹，且其实现中拥有 [`useState`](https://zh-hans.reactjs.org/docs/hooks-state.html) 或 [`useContext`](https://zh-hans.reactjs.org/docs/hooks-reference.html#usecontext) 的 Hook，当 context 发生变化时，它仍会重新渲染。

默认情况下其只会对复杂对象做浅层对比，如果你想要控制对比过程，那么请将自定义的比较函数通过第二个参数传入来实现。

#### 6. *高阶组件*

*就是一个函数，传给它一个组件，它返回一个新的组件*。新的组件使用传入的组件作为子组件。

*高阶组件的作用是用于代码复用*，可以把组件之间可复用的代码、逻辑抽离到高阶组件当中。*新的组件和传入的组件通过 `props` 传递信息*。

高阶组件有助于提高我们代码的灵活性，逻辑的复用性。灵活和熟练地掌握高阶组件的用法需要经验的积累还有长时间的思考和练习，如果你觉得本章节的内容无法完全消化和掌握也没有关系，可以先简单了解高阶组件的定义、形式和作用即可。

#### 7.Vue和React diff算法的不同之处

#### 8.用React hooks实现一个倒计时组件，并显示时间。