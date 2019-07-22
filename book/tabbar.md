## 配置

##### 底部导航

app.json

```js
"tabBar": {
    "color":"#ffffff",
    "selectedColor":"#ffffff",
    "backgroundColor": "#494971",
    "list": [
      {
        "pagePath": "pages/index/main",
        "iconPath":"static/home/icon-02.png",
        "selectedIconPath":"static/home/icon-01.png",
        
        "text": "银行首页"
      },
      {
        "pagePath": "pages/activity/main",
        "iconPath":"static/home/icon-03.png",
        "selectedIconPath":"static/home/icon-04.png",
        "text": "今日活动"
      },
      {
        "pagePath": "pages/product/main",
        "iconPath":"static/home/icon-05.png",
        "selectedIconPath":"static/home/icon-06.png",
        "text": "产品中心"
      },
      {
        "pagePath": "pages/mywelfare/main",
        "iconPath":"static/home/icon-07.png",
        "selectedIconPath":"static/home/icon-08.png",
        "text": "我的福利"
      }
    ]
  }
```

## 页面

结构 `pages/{page}/main.js`，`{page}`小程序页面名称


### 生命周期

1. created 初始化组件
2. onLoad  页面首次加载时触发
3. onShow  页面可见，比如返回到页面，刚打开页面
4. onReady  页面初次渲染完成时触发。一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
5. mounted 首次dom绑定
6. onHide 页面不可见，比如打开新页面，关闭页面

> 总结

1. 接口调用如果想每次打开都刷新，可以使用 onShow
2. 首次打开可以用 created 后都可以
3. 需要获取路由参数，onLoad开始才可以获取
4. 如果需要 UI交互，从 onReady开始
### 新建页面

新建user页面，在pages新建目录user,新建`main.js`,新建`index.vue`

main.js

```js
import Vue from 'vue'
import NJBANK from '@/njb'
import App from './index'
import store from '@/store'
const app = new Vue({
  ...App,
  store
})

NJBANK(app)
```

index.vue,和vue单文件组件一样,再`app.json`pages数组中注册，重新运行npm run dev

### 加载流程

1. 导入 vue 
2. 导入页面入口组件
3. 导入南京银行包 
4. 导入store，store务必要在南京银行包后
5. 初始化Vue对象并渲染

> 1,2,5为必须步骤，其他可选

### assets

存放本地的资源文件

```html

```

### static

存放的网络资源文件

```html

```

## css

微信小程序使用 wxss
<a href="https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html" target="_blank">wxss文档</a>

##### 背景图片说明

> 默认小图片会直接转 dataURL字符串，稍大图片无法使用本地图片无法使用，使用网络地址或用`image`组件
，说明：https://developers.weixin.qq.com/miniprogram/dev/qa.html

##### 用法

因为设计稿都是 750px，比如 一个图片是 116* 116px, 再小程序直接写 px 即可，因为 1px = 1rpx，写px，会自动编译出rpx

```css
.user {
  display: flex;
  flex-direction: row;
  align-items: center;
  &-avatar{
  width: 116px;
  height: 116px;
  margin: 20px;
  border-radius: 50%;
  }
}
```

## 事件

### 事件列表

```js
{
    click: 'tap',
    touchstart: 'touchstart',
    touchmove: 'touchmove',
    touchcancel: 'touchcancel',
    touchend: 'touchend',
    tap: 'tap',
    longtap: 'longtap',
    input: 'input',
    change: 'change',
    submit: 'submit',
    blur: 'blur',
    focus: 'focus',
    reset: 'reset',
    confirm: 'confirm',
    columnchange: 'columnchange',
    linechange: 'linechange',
    error: 'error',
    scrolltoupper: 'scrolltoupper',
    scrolltolower: 'scrolltolower',
    scroll: 'scroll'
}

```
在 input 和 textarea 中 change 事件会被转为 blur 事件。

### 修饰符

- .stop 的使用会阻止冒泡，但是同时绑定了一个非冒泡事件，会导致该元素上的 catchEventName 失效！
- 其他不支持


#### 用法

- 阻止冒泡遮罩层滑动引起页面滑动

```html
<div @touchmove.stop></div>
```

## 表单

### 支持

todo

### 不支持

todo


## 模板语法

### class

```html
<p :class="{ active: isActive }">111</p>
<p class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }">222</p>
<p class="static" :class="[activeClass, errorClass]">333</p>
<p class="static" v-bind:class="[isActive ? activeClass : '', errorClass]">444</p>
<p class="static" v-bind:class="[{ active: isActive }, errorClass]">555</p>
```

### style

```html
<p v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">666</p>
<p v-bind:style="[{ color: activeColor, fontSize: fontSize + 'px' }]">777</p>
```



###  不支持

1. 过滤器
2. 不支持部分复杂的 JavaScript 渲染表达式
3. 不支持 纯-HTML
4. class、style直接绑定数据对象，字符串可以

## 自定义vue组件

除了高级组件，其他都支持


#### 不支持

- `动态组件`
- `异步组件`
- `keep-alive`
- `transition`

## 小程序组件

todo

## webview

### 分享

```js

onShareAppMessage (options) {
    const currUrl = parseUrl(options.webViewUrl, {
      pid: this.getSharePid(),
      userid: null,
      fromShare: 'h5'
    })

    this.shareInfo.sharePath = '/pages/activity/webview/main?url=' + encodeURIComponent(currUrl) + '&pid=' + this.getSharePid()

    console.log('share.options', options)
    console.log('share.data', this.shareInfo)
    console.log('share.webview.url', currUrl)

    return {
      title: this.shareInfo.shareTitle,
      path: this.shareInfo.sharePath,
      imageUrl: this.shareInfo.shareimageUrl
    }
  },
```

### 监听处理h5 postMessage


```html
<web-view :src="webviewlink" @message="onH5Message"></web-view>
```

```js
onH5Message (e) {
      const {data} = e.mp.detail
      console.log('onH5Message', data)
      if (data && data[0] === 'backMyShop') {
        this.$store.commit('backMyShop')
      }
    }
```