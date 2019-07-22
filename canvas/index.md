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
// ctx.setFillStyle('transparent') // 该方法一定要注释掉，否则安卓无法生成圆角头像
const offset = img.w / 2
ctx.arc(img.x + offset, img.y + offset, offset, 0, Math.PI * 2, false)
ctx.clip()
ctx.drawImage(tempPath, img.x, img.y, img.w, img.h)
ctx.restore()
```

### 圆形填充或描边

#### arc(number x, number y, number r, number sAngle, number eAngle, boolean counterclockwise)

- 参数
  - `x:int` 圆心的 x 坐标
  - `y:int` 圆心的 y 坐标
  - `r:int` 圆的半径
  - `sAngle:int` 起始弧度，单位弧度（在3点钟方向）
  - `eAngle:int` 终止弧度
  - `counterclockwise:int` 弧度的方向是否是逆时针

```js
const img = {
    x: 44,
    y: 49,
    w: 110,
    h: 110
}
ctx.save()
ctx.beginPath()
const offset = img.w / 2
ctx.arc(img.x + offset, img.y + offset, offset, 0, Math.PI * 2, false)
ctx.setFillStyle('white') // 填充颜色
ctx.setStrokeStyle('white') // 描边颜色, 不描边去掉这行代码
ctx.closePath()
ctx.fill() // 填充
ctx.stroke() //描边，不描边去掉这行代码
ctx.restore()
```

### 方形

#### rect(number x, number y, number width, number height)

- 参数
  - `x:int` 矩形路径左上角的横坐标
  - `y:int` 矩形路径左上角的纵坐标
  - `width:int` 矩形路径的宽度
  - `height:int` 矩形路径的高度

```js
ctx.rect(10, 10, 100, 30)
ctx.setFillStyle('yellow')
ctx.fill()
```


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
