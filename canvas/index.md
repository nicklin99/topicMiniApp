# 画布

### 生成图片

模板

```html
<template>
  <div class="full">
    <canvas style="width: 750px; height: 1206px;" canvas-id="shareShopCanvas"></canvas>
  </div>
</template>
```

组件,获取画布上下文

```js
export default {
    mounted(){
        var context = wx.createCanvasContext('shareShopCanvas')
    
        context.setStrokeStyle("#00ff00")
        context.setLineWidth(5)
        context.rect(0, 0, 200, 200)
        context.stroke()
        context.setStrokeStyle("#ff0000")
        context.setLineWidth(2)
        context.moveTo(160, 100)
        context.arc(100, 100, 60, 0, 2 * Math.PI, true)
        context.moveTo(140, 100)
        context.arc(100, 100, 40, 0, Math.PI, false)
        context.moveTo(85, 80)
        context.arc(80, 80, 5, 0, 2 * Math.PI, true)
        context.moveTo(125, 80)
        context.arc(120, 80, 5, 0, 2 * Math.PI, true)
        context.stroke()
        context.draw()
    }
}
```

### 圆形头像

```js
const img = {
    x: 44,
    y: 49,
    w: 110,
    h: 110
}
const tempPath = ''
ctx.save()
ctx.beginPath()
ctx.setStrokeStyle('white')
// ctx.setFillStyle('transparent') // 该方法一定要注释掉，否则安卓无法生成圆角头像
const offset = img.w / 2
ctx.arc(img.x + offset, img.y + offset, offset, 0, Math.PI * 2, false)
ctx.fill()
ctx.stroke()
ctx.clip()
ctx.drawImage(tempPath, img.x, img.y, img.w, img.h)
ctx.closePath()
ctx.restore()
```

### 圆形

```js

```


### 方形


### 图片




### 字体

设置字体大小

```js
ctx.setFontSize(43)
```

设置文本颜色

```js
ctx.setFillStyle('#fff')
```

设置文本垂直对齐

```js
ctx.setTextBaseline('top')
```

设置文本

- 参数
  - `text:string` 文本
  - `x:int` x坐标
  - `y:int` y坐标

```js
ctx.fillText(nickname, 174, 62)
```

设置文本斜体

```js
ctx.setTransform(1, 0, -0.1, 1, 0, 0)
```
