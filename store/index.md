# 存储

每个微信小程序都可以有自己的本地缓存，可以通过 wx.setStorage/wx.setStorageSync、wx.getStorage/wx.getStorageSync、wx.clearStorage/wx.clearStorageSync，wx.removeStorage/wx.removeStorageSync 对本地缓存进行读写和清理。

同一个微信用户，同一个小程序 storage 上限为 10MB。storage 以用户维度隔离，同一台设备上，A 用户无法读取到 B 用户的数据。

注意： 如果用户储存空间不足，我们会清空最近最久未使用的小程序的本地缓存。我们不建议将关键信息全部存在 storage，以防储存空间不足或用户换设备的情况。

已对同步存储做了封装,查看 <a href="#/extend?id=storage">存储API</a>

## 用户信息

### state

```js
{
    njb:{
        user: false,    // 接口返回的用户信息，主要包含 userid、openid
        wxuser: false,  // 微信用户信息
        token: ''   // 登录令牌
    }
}
```


### 读取用户数据

用户信息对象查看 `/common/wetch/auth`接口

```js
this.$store.state.njb.user
```

### 读取微信用户数据

用户信息对象查看微信小程序文档 <a href="https://developers.weixin.qq.com/miniprogram/dev/api/open-api/user-info/UserInfo.html" target="_blank">userInfo</a>

```js
this.$store.state.njb.wxuser
```

### 获取当前userId

```js
import storage from '@/packages/storage'
storage.getItem('userId')
```

### 缓存

| key              | 类型   | 说明                      |
| ---------------- | ------ | ------------------------- |
| userId | string | 当前用户id |

## 日常任务

### state

```js
const state = {
  // 连续签到
  signIn: {
    value: 0, // 连续签到次数
    list: [], // 7天
    today: false, // 今天是否签到
    todayIndex: '',
    todayPoint: 0
  }
}
```

### 缓存 

| key      | 类型     | 说明             | 示例                                                 |
| -------- | -------- | ---------------- | ---------------------------------------------------- |
| zuanjing | `object` | 最近一次钻井记录 | {"t":1542679524125,"y":2018,"m":10,"d":20,"index":1} |
| saodi    | `object` | 最近一次扫地记录 | {"y":2018,"m":11,"d":20} 扫地成功记录的年月日

## 分享

### 缓存

| key              | 类型   | 说明                      |
| ---------------- | ------ | ------------------------- |
| shareBankPreview | string | 分享银行海报图片临时路径 |
