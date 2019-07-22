# vant

Vant Weapp 是有赞移动端组件库 Vant 的小程序版本，两者基于相同的视觉规范，提供一致的 API 接口，助力开发者快速搭建小程序应用。

## 集成vant Weapp到mpvue

1. 从git仓库下载

```
yarn add vant-weapp --production
```

2. 将dist内的组件放如src/vant文件夹

webpack.base.config.js CopyWebpackPlugin增加

```js
baseWebpackConfig = merge(baseWebpackConfig, {
    plugins: [
      new CopyWebpackPlugin([
        {
          from: path.resolve(__dirname, '../src/assets/tabbar'),
          to: path.resolve(__dirname, '../dist/wx/assets/tabbar'),
          ignore: ['.*']
        },
        {
          from: path.resolve(__dirname, '../src/vant'),
          to: path.resolve(__dirname, '../dist/wx/vant'),
          ignore: ['.*']
        }
      ])
    ]
  })
```
