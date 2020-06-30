## HTML&CSS：

### BFC

1. 独立的容器，容器里面的子元素不会影响到外面的元素，反之亦然
2. BFC会将浮动元素计入高度

### 创建BFC

1. float
2. postion不为static或者relative
3. display:inline-block、flex、table-cell等

## JavaScript

#### 继承

#### 原型链

#### this指向

1. 函数内部使用，用来指代当前的运行环境
2. Function中this永远指向最后调用它的那个对象。
3. 构造函数里的this指向新创建的类实例
4. 箭头函数的this始终指向函数定义时的this，而非执行时。

#### 设计模式

#### call, apply, bind

#### new实现

#### 防抖节流

#### let, var, const 区别

1. let、const在相同作用域内不允许重复声明变量
2. const是常量，不能改变
3. let和const是块级作用域，只在{}内有效
4. let会引起暂时性死区

#### 暂时性死区

当程序的控制流程在新的作用域（module function 或 block 作用域）进行实例化时，在此作用域中用let/const声明的变量会先在作用域中被创建出来，但因此时还未进行词法绑定，所以是不能被访问的，如果访问就会抛出错误。因此，在这运行流程进入作用域创建变量，到变量可以被访问之间的这一段时间，就称之为暂时死区。

#### event loop；

1. Event Loop执行一次，从task队列中拉出一个task执行
2. Event Loop检查microtask队列是否为空，依次执行直至清空队列
3. task主要包含：setTimeout、setInterval、setImmediate、I/O、UI交互事件
4. microtask主要包含：Promise、process.nextTick、MutaionObserver

#### promise实现

#### promise并行执行和顺序执行

顺序：递归调用、await/async
并行: promise.all()

#### async/await的优缺点

1. 可以一定程度解决Promise的then过多的问题
2. 表达式相比generator/yeild清晰
3. 一个await被reject会导致后面的无法执行

#### 闭包

#### 垃圾回收和内存泄漏

#### 数组方法

#### 数组乱序

#### 数组扁平化

事件委托、事件监听、事件模型

## Vue:

#### vue数据双向绑定原理

#### vue computed原理

#### computed和watch的区别

#### vue编译器结构图、生命周期、vue组件通信

#### mvvm模式、mvc模式理解

#### vue dom diff

#### vuex

#### vue-router

## 网络

#### 浏览从输入网址到回车发生了什么

#### 前端安全（CSRF、XSS）

#### 前端跨域

#### 浏览器缓存、cookie, session, token, localstorage, sessionstorage

#### TCP连接(三次握手, 四次挥手)

#### 性能相关

#### 图片优化的方式

#### 500 张图片，如何实现预加载优化

#### 懒加载具体实现

#### 减少http请求的方式

#### webpack如何配置大型项目
