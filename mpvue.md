# mpvue

## 编译 build

了解mpvue编译

1. mpvue-loader, template部分编译走的`mpvue-loader`修改的编译方法，不走 file-loader,url-loader
2. style编译使用`vue-style-complier`编译，这块和vue是一样的

### mpvue-loader

mpvue-loader作用类似vue-loader,将vue文件编译，`template`,`script`,`style`分别一一编译

mpvue-loader做了一些修改，`package.json`删除`mpvue`依赖,重新安装从git修改过的包

```bash
npm i https://github.com/nicklin99/mpvue-loader  -D
```

#### 静态图片与文件URL处理

> `img`组件变异规则

1. `src`文件路径第一个字符是`.`,直接使用转为`/${图片路径}`
2. `src`是`/static`开头，publicPath为 `process.env.staticPublicPath`

> css背景图片

1. `src`文件路径第一个字符是`.`,直接使用转为`/${图片路径}`，走`file-loader` publicPath


#### 已知问题

1. 无法绑定动态方法，必须通过data传入