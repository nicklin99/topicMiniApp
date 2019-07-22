# 路由

## 路由组件

小程序有 `navigator`组件用于路由导航，在mpvue中只需要这样web a标签写法即可

web
```html
<a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>
```

小程序
```html
<navigator url="/pages/counter/main" class="_a data-v-2959e30b counter">去往Vuex示例页面</navigator>
```

## 路由API

### 安装

 ```js
import Vue from 'vue'
import Router from '../packages/router'
Vue.use(Router)
 ```

> API

### push(path, success?, fail?, complete?)

保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面。使用 wx.navigateBack 可以返回到原页面。

- 参数
    - `path:string` 路由路径
    - `success:function` 接口调用成功的回调函数
    - `fail:function` 接口调用失败的回调函数
    - `complete:function` 接口调用结束的回调函数（调用成功、失败都会执行）

```js
router.push('test?id=1')
```

callNative

```js
wx.navigateTo({
  url: 'test?id=1'
})
```


### replace(path, success?, fail?, complete?)

关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。

- 参数
    - `path:string` 路由路径
    - `success:function` 接口调用成功的回调函数
    - `fail:function` 接口调用失败的回调函数
    - `complete:function` 接口调用结束的回调函数（调用成功、失败都会执行）

```js
router.replace('test?id=1')
```

callNative

```js
wx.redirectTo({
  url: 'test?id=1'
})
```

### back(step=1, success?, fail?, complete?)

关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages() 获取当前的页面栈，决定需要返回几层。

- 参数
    - `step:int` 步数，默认1

```js
router.back()
```

callNative

```js
wx.navigateBack({
    delta: step || 1
})
```

```js
// 注意：调用 navigateTo 跳转时，调用该方法的页面会被加入堆栈，而 redirectTo 方法则不会。见下方示例代码
```

### tab(path, success?, fail?, complete?)

- 参数
    - `path:string` 需要跳转的 tabBar 页面的路径（需在 app.json 的 tabBar 字段定义的页面），路径后不能带参数。
    - `success:function` 接口调用成功的回调函数
    - `fail:function` 接口调用失败的回调函数
    - `complete:function` 接口调用结束的回调函数（调用成功、失败都会执行）

跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

```js
router.tab('/index')
```

callNative

```js
{
  "tabBar": {
    "list": [{
      "pagePath": "index",
      "text": "首页"
    },{
      "pagePath": "other",
      "text": "其他"
    }]
  }
}
wx.switchTab({
  url: '/index'
})
```