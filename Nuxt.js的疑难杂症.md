# Nuxt.js的疑难杂症

### 前言

在nuxtjs开发中，遇到过的许多问题，其实都是由服务端渲染造成的，现在就来总结一下。

#### document,window等对象找不到

这个问题很简单，就是因为node端（即服务端）没有这些浏览器对象，解决方法如下：

1. 使用<no-ssr>标签来使一些使用这类对象的dom不在服务端渲染，V2.90后使用<client-only>

2. 在nuxt.config.js中配置，以uikit为例

   ```javascript
   {src: ‘~plugins/uikit.js’, ssr: false}, //uikit.js为引入该框架的文件。
   ```

3. 最暴力的解决方法，在head里引入该库的cdn。

#### axios和proxy的使用

因为nuxt本身就有自己封装好的axios和proxy，所以在nuxt.config.js中添加以下就可以激活：

```javascript
 modules: [
    '@nuxtjs/axios',
    '@nuxtjs/proxy',
  ],
  axios: {
    prefix: '/api', //请求前缀
    credentials: true,是否带cookies
    proxy: false，是否使用proxy反向代理
  },
  proxy: {
    '/api/': {
      target: 'http://127.0.0.1:10086/', // 目标接口域名
      changeOrigin: true, // 表示是否跨域
    }
  }
```

#### Vuex、Vue-router根据目录生成的问题。

> 首先官方文档中说明，假设 `pages` 的目录结构如下：
>
> ```javascript
> pages/
> --| user/
> -----| index.vue
> -----| one.vue
> --| index.vue
> ```
>
> 那么，Nuxt.js 自动生成的路由配置如下：
>
> ```javascript
> router: {
>   routes: [
>     {
>       name: 'index',
>       path: '/',
>       component: 'pages/index.vue'
>     },
>     {
>       name: 'user',
>       path: '/user',
>       component: 'pages/user/index.vue'
>     },
>     {
>       name: 'user-one',
>       path: '/user/one',
>       component: 'pages/user/one.vue'
>     }
>   ]
> }
> ```

​	这类嵌套路由也可以这么实现：

```javascript
pages/
--| user/
-----| one.vue
--| index.vue
--| user.vue
```

​	**vuex也用了同样生成的方法，但vuex必须得有index.js作为根模块来暴露其他模块，否则在使用中会获取不到数据，特别是getters。**

```javascript
export const state = () => ({
})
export const getters = {
    userInfo: state => state.user.userInfo,
    isLogin: state => state.user.login
}
export const mutations = {
}
```

#### 暂未解决的问题：

​	1.刷新后通过axios获取的数据在vuex中computed后并不会更新视图

