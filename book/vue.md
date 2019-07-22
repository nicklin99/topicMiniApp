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

###  不支持

1. 过滤器
2. 不支持部分复杂的 JavaScript 渲染表达式
3. 不支持 纯-HTML
4. class、style直接绑定数据对象，字符串可以