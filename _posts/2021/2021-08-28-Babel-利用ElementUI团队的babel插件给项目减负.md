---
layout: post
title: 利用ElementUI团队的Babel插件给项目减负
date: 2021-08-28 13:27:40 +08:00
categories: [Webpack,Babel]
---

## 利用ElementUI团队的Babel插件给项目减负

目前在后台项目中，最常使用的ui库就是饿了么团队出品的ElementUI，而最开始使用只是全局全量引入，这样做虽然很方便，但是首次加载的时候，加载速度影响有点大，特别网络不好和在移动端影响更明显。

#### 未做特别处理，直接全局引入

在 `main.js` 中，

```javascript
import 'element-ui/lib/theme-chalk/index.css'
import Element from 'element-ui'

Vue.use(Element)
```

<img src="./img/vue-config1.png" alt="1" style="zoom: 33%;" />

未做其它配置，打包后单文件特别大，即使gzip压缩后也有249KB。

接下来按照官方团队推荐修改为按需加载。

#### 添加依赖项

```bash
npm install babel-plugin-component -D
```

因为不需要运行时使用，所以加上 `-D` 参数。

然后在babel.config.js文件中的plugins属性数组中，加入配置项：(没有文件则新建一个)

```js
[
    'component',
    {
        libraryName: 'element-ui',
        styleLibraryName: 'theme-chalk'
    }
]
```

我的这个文件全部配置为：

```js
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset'
  ],
  plugins: [
    [
      'component',
      {
        libraryName: 'element-ui',
        styleLibraryName: 'theme-chalk'
      }
    ]
  ]
}

```

接下来将 `main.js` 文件中的引入ElementUI的代码修改一下：

```js
// 删除这两行
// import Element from 'element-ui'
// Vue.use(Element)
// 添加
import './components/element-ui/registry.js'

// registry.js内容为
import Vue from 'vue'
import {
  Row,
  Col,
  Button,
  Select,
  Option,
  Form,
  FormItem,
  Input,
  InputNumber,
  DatePicker,
  Menu,
  Submenu,
  MenuItem,
  Card,
  Message,
  Notification,
  Dialog,
  Pagination,
  Table,
  TableColumn,
  MessageBox,
  Loading, Tooltip, Popconfirm
} from 'element-ui'

const components = [Row, Col, Button, Select, Option, Form, FormItem, Input, InputNumber, DatePicker, Menu, Submenu, MenuItem, Card, Dialog, Pagination, Table, TableColumn, Tooltip, Popconfirm]

components.forEach(comp => {
  Vue.component(comp.name, comp)
})
Vue.directive('loading', Loading)
Vue.prototype.$message = Message
Vue.prototype.$notify = Notification
Vue.prototype.$loading = Loading.service
Vue.prototype.$alert = MessageBox.alert
Vue.prototype.$confirm = MessageBox.confirm
// 写上项目中用到的全部el组件
```

接下来再次打包

<img src="./img/vue-config2.png" alt="2" style="zoom:33%;" />

最大的js文件gzip压缩后体积为159KB，但是还是有点大了

#### 切割打包后js文件

利用webpack的 `optimization.splitChunks` 分割vue和elementui

在vue.config配置中修改一下：

```js
configureWebpack: config => {
    config.devtool = isPro ? 'cheap-module-source-map' : 'cheap-module-eval-source-map'
    Object.assign(config.optimization.splitChunks.cacheGroups, {
        element: { // 分离组件库
            name: true, // name 为true会自动命名
            test: /[\\/]node_modules[\\/](element-ui)[\\/]/,
            priority: 10,
            chunks: 'initial'
        },
        vue: { // 分离vue全家桶
            name: true,
            test: /[\\/]vue(.+?)[\\/]/,
            priority: 5,
            chunks: 'initial'
        }
    })
}
```

再次打包

<img src="./img/vue-config3.png" alt="3" style="zoom:33%;" />

gzip压缩后最大文件仅86kb

也可以将vue忽略，使用cdn的方式引入到项目
