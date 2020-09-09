## 组件化

### antd

#### 按需加载

```js
// 按需引入
import { Button } from 'antd';
import "antd/dist/antd.css"
// 配置按需导入：
// 方案一
// 安装react-app-rewired取代react-scripts，可以扩展webpack的配置
// npm install react-app-rewired customize-cra babel-plugin-import -D
// 编写配置文件config-overrides.js，参考同名文件
// 用来参考的，本项目已eject，未使用
const { override, fixBabelImports, addDecoratorsLegacy } = require("customize-cra");

// override生成webpack配置对象
module.exports = override(
  fixBabelImports("import", { // antd按需加载
    libraryName: "antd",
    libraryDirectory: "es",
    style: "css"
  }),
  addDecoratorsLegacy() // 配置装饰器
);
// 修改scripts，使用react-app-rewired取代react-scripts

// 方案二（本项目使用）
// npm run eject 
// 修改配置文件
```

#### 配置装饰器

#### Form

getFieldDecorator：装饰器工厂，得到一个装饰器，设置校验规则，监听事件

### 组件设计

#### 表单组件

##### 设计思路

通过高阶组件实现数据收集，校验，提交等特性

传递包装好书接管输入事件，统一管理表单数据

传递一个校验函数

##### 实现

克隆

#### 弹窗组件

##### portal

16.0 传送门

##### unstable_renderSubtreeIntoContainer

16.0之前

#### 树形组件

#### 组件优化

##### shouldComponentUpdate

判断是否变化

##### PureComponet

纯展示型组件可以使用，浅对比。使用时注意对象（可以直接展开而不使用对象赋值，否则对比不起作用）

##### React.memo

16.6之后，让函数式组件也拥有Pure Component的功能，是一个高阶组件

##### Immutable.js

不可变

## 全家桶

### Redux

js应用的状态容器，保证程序的行为一致性且易于测试

**安装**

对比vuex没有action，Reducer相当于mutation

#### reducer

一个函数，初始化state，定义state修改规则

通过dispatch一个action提交数据修改

强制更新：`this.forcrUpdate()`

**原生**

createStore 创建

reducer 初始化，修改状态

getState 获取状态

dispatch 提交变更

subscribe 订阅变更

#### react-redux

Provider

为后代组件提供store

connect

装饰器工厂函数，为组件提供数据和变更方法

参数1:mapStateToProps方法

参数2:mapDispatchToProps方法，可以简化为一个对象

#### 异步

redux只支持同步，异步任务需要中间件，比如redux-thunk和redux-logger

安装

applyMiddleware

#### 优化

store模块

#### reducer原理实现

store

中间件

异步

#### react-redux原理实现

### Router4

 react-router-dom

一切皆组件

#### 匹配

#### 传参

####  嵌套

#### 404

#### 路由守卫

#### 原理实现

### 最佳实践

#### 异步方案redux-saga

管理副作用

**使用**

创建清单

创建中间件

运行saga监听

#### 数据流方案dva

基于redux和redux-saga

类似vuex

#### 应用框架umi

**环境准备**

首先得有 [node](https://nodejs.org/en/)，并确保 node 版本是 10.13 或以上。（mac 下推荐使用 [nvm](https://github.com/creationix/nvm) 来管理 node 版本）

```bash
$ node -v
v10.13.0
```

推荐使用 yarn 管理 npm 依赖，并[使用国内源](https://github.com/yiminghe/tyarn)（阿里用户使用内网源）。

```bash
# 国内源
$ npm i yarn tyarn -g
# 后面文档里的 yarn 换成 tyarn
$ tyarn -v
```

```
# 创建目录
$ mkdir myapp && cd myapp

# 安装依赖
$ yarn add umi

# 创建页面
$ npx umi g page index --typescript --less

# 启动开发
$ npx umi dev
```

或者[通过脚手架快速上手](https://umijs.org/zh-CN/docs/getting-started)。

**脚手架**

先找个地方建个空目录。

```bash
$ mkdir myapp && cd myapp
```

通过官方工具创建项目，

```bash
$ yarn create @umijs/umi-app
```

**安装依赖**

```bash
$ yarn
```

**开始**

基于dva

结构

`npx umi g page index //生成首页，路由`

`npx umi g page user/'$id' // 动态路由`

`npx umi g layout ./users // 生成布局`

umi/router提供路由器

##### 404页面

`npx umi g page 404`

##### 布局页

约定 src/layouts/index.js 为全局路由，返回一个 React 组件，通过 props.children 渲染子组件。

创建layouts/index

##### 扩展路由

使用文件中第一个块注释，要符合yaml语法

实现路由守卫

##### 引入dva

安装umi-plugin-react

创建配置文件.umirc.js，配置插件，也可以添加自定义路由

创建models

使用connect映射

mock

loading

#### 项目

重定向注释

安装ant-design-pro