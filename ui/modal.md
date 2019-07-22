
## modal

显示一个确定、取消选择弹窗

callNative

```js
wx.showModal({
  title: '提示',
  content: '这是一个模态弹窗',
  success (res) {
    if (res.confirm) {
      console.log('用户点击确定')
    } else if (res.cancel) {
      console.log('用户点击取消')
    }
  }
})
```

> API

### $modal(title,content, options)

- 参数
    - `title:string` 标题
    - `content:string` 内容
    - `options:object` 可选
        - `showCancel:boolean` 可选，是否显示取消按钮
        - `confirmText:string` 可选，确认按钮的文字，最多 4 个字符	
        - `cancelText:string` 可选，取消按钮的文字，最多 4 个字符
        - `cancelColor:string` 可选，取消按钮的文字颜色，必须是 16 进制格式的颜色字符串
        - `confirmColor:string` 可选，确认按钮的文字颜色，必须是 16 进制格式的颜色字符串
        - `fail:function` 可选，接口调用失败的回调函数
        - `complete:function` 接口调用结束的回调函数（调用成功、失败都会执行）
```js
this.$modal('去开启我的银行么？', '您需要开启您的个人银行才能使用该功能').then(() => {
    this.$router.push('/other/openbank')
})
```