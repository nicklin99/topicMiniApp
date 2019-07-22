# 微信小程序API

## 剪切板

用途：复制券码
<a href="https://developers.weixin.qq.com/miniprogram/dev/api/device/clipboard/wx.setClipboardData.html" target="_blank">查看剪贴板文档</a>

```示例代码
wx.setClipboardData({
  data: 'data',
  success (res) {
    wx.getClipboardData({
      success (res) {
        console.log(res.data) // data
      }
    })
  }
})
```
## 收货地址
用途：我的奖品调微信收货地址
<a href="https://developers.weixin.qq.com/miniprogram/dev/api/open-api/address/wx.chooseAddress.html" target="_blank">查看收货地址文档</a>

- 支持版本 >= 1.1.0
- 调用前需要 用户授权 scope.address


```示例代码
wx.getSetting({
    success (res) {
        console.log(res)
        if (!res.authSetting['scope.address']) {
            wx.authorize({
                scope: 'scope.address',
                success () {
                    // 用户已经同意小程序使用获取地址功能，后续调用 wx.chooseAddress 接口不会弹窗询问
                    wx.chooseAddress({
                        success (res) {
                            console.log(res.userName)
                            console.log(res.postalCode)
                            console.log(res.provinceName)
                            console.log(res.cityName)
                            console.log(res.countyName)
                            console.log(res.detailInfo)
                            console.log(res.nationalCode)
                            console.log(res.telNumber)
                        }
                    })
                }
            })
        }
    })
```
