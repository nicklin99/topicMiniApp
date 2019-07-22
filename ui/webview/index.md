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