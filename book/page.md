### 新建页面

新建user页面，在pages新建目录user,新建`main.js`,新建`index.vue`

main.js

```js
import Vue from 'vue'
import App from './index'
import store from '@/store'
const app = new Vue({
  ...App,
  store
})

```

index.vue,和vue单文件组件一样,再`app.json`pages数组中注册，重新运行npm run dev

### 下拉刷新监听处理

1.配置开启下拉刷新监听
`main.json`

```js
 "backgroundTextStyle": "dark", // 刷新文本颜色  dark、light 默认light
 "backgroundColor": "#c8e6ff",  // 页面背景色，默认白色
```
2. 注册下拉刷新监听处理函数,刷新完关闭下拉刷新
```js
onPullDownRefresh () {
    console.log('callback.onPullDownRefresh')
    this.$store.dispatch('refreshUser').then(() => {
      wx.stopPullDownRefresh()
    })
  },
```

### 页面转发分享监听处理

1. 注册转发分享监听处理函数

```js
onShareAppMessage (options) {
    const pid = this.$store.getters.isCurrUserShop ? this.$store.state.njb.user.id : 0
    console.log('onShare.pid', pid)
    return {
      title: '好玩停不下来',
      path: '/pages/index/main?pid=' + pid,
      imageUrl: ''
    }
  },
```

2. 配置后会显示转发按钮，可以通过 `wx.hideShareMenu({})`隐藏转发按钮，如果又想显示 `wx.showShareMenu()`显示转发
3. `wx.updateShareMenu`更新转发属性
4. `wx.getShareInfo` 获取转发详细信息
5. 3,4用法有点复杂，这里不做深入
