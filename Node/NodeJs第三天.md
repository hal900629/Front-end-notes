[TOC]

# NodeJs第三天

## 1. 反馈与复习

### 反馈

- 希望老师再推荐一些前端学习的书籍，谢谢！
  - 《JavaScript 高级编程》第3班
  - 学习，解决问题
  - 书本可以更好的系统的整理学过的内容，了解一些细节
  - 《JavaScript 语言精粹》
- seo的资料，嘿嘿
  - 网站运营 SEO
  - SEO 运营专员
  - 百度、Google、搜狗、
- 老师，软件版本的升级是以什么作为理论支持的，为什么跳跃间隙可以这么大？还有，看上了老师的电子图书馆，瞬间好爱学习呀，真的！
  - 软件开发版本里面涉及到软件工程学： 
  - x.x.x
    - 0.0.1
    - 0.0.2
    - 1.1.5
    - 1.9.2
    - 2（新增功能比较多，甚至可能去除了某些功能）.5(加入了新功能).0（修复bug，提升性能）
    - 大版本
    - 一般是这些客户端软件、技术框架开发者比较理解的多
    - 做网站很少涉及到版本的概念，网站的目的就是快
- art-template里面用的语法是jQuery吗， each什么的 我晕了 each,forEach, 遍历的全混了
  - art-template 和 jQuery 一毛钱关系都没有
  - each 是 art-template 的模板语法，专属的
  - {{each 数组}}
  - <li>{{ $value }}</li>
  - {{/each}} 这是 art-template 模板引擎支持的语法，只能在模板字符串中使用
  - $.each(数组, function)
  - $('div').each(function) 一般用于遍历 jQuery 选择器选择到的伪数组实例对象
  - forEach 是 EcmaScript 5 中的一个数组遍历函数，是 JavaScript 原生支持的遍历方法 可以遍历任何可以被遍历的成员
  - jQuery 的 each 方法和 forEach 几乎一致
  - 由于 forEach 是 EcmaScript 5 中的，所以低版本浏览器不支持
- 每一次的复习贼重要 老师很不错 我喜欢
- 在以后的工作中 用到node.js的地方多吗？ 在留言本的案例中 点击发表留言跳转页面的路径是url路径 和之前写的页面跳转写的文件路径还是有点分不清。
  - 技多不压身
  - Node 对于前端来讲是进阶高级前端开发工程师必备的技能
  - 屌丝最容易逆袭的职业
  - 见得东西多了你就不怕了
  - 为所欲为
- 如果从a中调用b中的数据，又从b中调用a中的数据，执行a代码，为什么把b中的执行完后才会执行a，而不是在b调用a的时候a中的代码继续执行
  - a 加载了 b
    - 执行 b 中的代码
    - 同时得到 b 中导出的接口对象：`exports`
    - 执行 b 的过程中发现 b 也在 require a
    - b 就会反过来执行 a
    - a 中又加载 b
    - b 又反过来加载 a
    - 这就是循环加载
    - 如果你一旦出现了这种情况，说明你的思路有问题。
    - jQuery.js （可能不可能出现 jQuery 依赖了 main）
    - main.js 依赖了 jQuery
    - 这个问题是矛盾。
  - b 中也加载了 a
  - 网页中所有的路径其实都是 url 路径，不是文件路径

### 复习

#### 网站开发模型

- 黑盒子、哑巴
- 写代码让它变得更智能
- 按照你设计好的套路供用户使用

#### 在 Node 中使用 art-template 模板引擎

- 安装
- 加载
- `template.render()`

#### 客户端渲染和服务端渲染的区别

- 最少两次请求，发起 ajax 在客户端使用模板引擎渲染
- 客户端拿到的就是服务端已经渲染好的

- 处理留言本案例首页数据列表渲染展示
- 处理留言本案例发表留言功能
  - 路径
  - 设计好的请求路径
  - $GET 直接或查询字符串数据
  - Node 中需要咱们自己动手来解析
    - url.parse()
  - /pinglun?name=jack&message=hello
  - split('?')
  - name=jack&message=hello
  - split('&')
  - name=jack message=hello
  - forEach()
  - name=jack.split('=')
  - 0 key
  - 1 value

####  掌握如何解析请求路径中的查询字符串

- `url.parse()`

#### 如何在 Node 中实现服务器重定向

- `header('location')`
  - 301 永久重定向 浏览器会记住
    - a.com b.com
    - a 浏览器不会请求 a 了
    - 直接去跳到 b 了
    - 案例：[新浪](www.sina.com)
  - 302 临时重定向 浏览器不记忆
    - a.com b.com
    - a.com 还会请求 a
    - a 告诉浏览器你往 b

- Node 中的 Console（REPL）使用
  - 主要是用来测试Node中的一些API的

## 2. 模块系统

### 2.1 三种模块

- **核心模块**
- **第三方模块**
- **自己写的模块**

### 2.2 模块引入与导出的方式

> **模块的引入`require`两个作用**
>
> **1. 执行模块**
>
> **2. 引入模块到处对象`exports`**

```javascript
var fs = require('fs');
```

> **模块导出的方式`exports`分两种情况：**

 1. **多文件导出**

```javascript
function add() {
    console.log('hahah')
}
var str = 'hello';
exports.add = add;
exports.str = str;
```

 2. **单文件导出**

```javascript
function add() {
    console.log('hahah')
}
module.exports = add;
//这种情况下面的会覆盖前面的。
```

### 2.3 模块原理

> **个人总结：模块中在代码的最后会有一句隐藏的代码`return module.exports`,但是作者为了添加导出方法的简单又加了一句`exports = module.exports `,这就要注意了，`module.exports`与`exports`都指向的是同一个对象，但是最后返回的是`module.exports`,这点要牢记**

> **这里定义了两个模块`foo.js`与`main.js`**

```javascript
//main.js文件
var fooExports = require('./foo')

console.log(fooExports)


// 如果你实在分不清楚 exports 和 module.exports
// 你可以选择忘记 exports
// 而只使用 module.exports 也没问题
// 
// module.exports.xxx = xxx
// moudle.exports = {}
```

```javascript
//foo.js文件
// 在 Node 中，每个模块内部都有一个自己的 module 对象
// 该 module 对象中，有一个成员叫：exports 也是一个对象
// 也就是说如果你需要对外导出成员，只需要把导出的成员挂载到 module.exports 中

// 我们发现，每次导出接口成员的时候都通过 module.exports.xxx = xxx 的方式很麻烦，点儿的太多了
// 所以，Node 为了简化你的操作，专门提供了一个变量：exports 等于 module.exports

// var module = {
//   exports: {
//     foo: 'bar',
//     add: function
//   }
// }

// 也就是说在模块中还有这么一句代码
// var exports = module.exports

// module.exports.foo = 'bar'

// module.exports.add = function (x, y) {
//   return x + y
// }

// 两者一致，那就说明，我可以使用任意一方来导出内部成员
// console.log(exports === module.exports)

// exports.foo = 'bar'
// module.exports.add = function (x, y) {
//   return x + y
// }

// 当一个模块需要导出单个成员的时候
// 直接给 exports 赋值是不管用的

// exports.a = 123

// exports = {}
// exports.foo = 'bar'

// module.exports.b = 456

// 给 exports 赋值会断开和 module.exports 之间的引用
// 同理，给 module.exports 重新赋值也会断开

// 这里导致 exports !== module.exports
// module.exports = {
//   foo: 'bar'
// }

// // 但是这里又重新建立两者的引用关系
// exports = module.exports

// exports.foo = 'hello'

// {foo: bar}
exports.foo = 'bar'


// {foo: bar, a: 123}
module.exports.a = 123

// exports !== module.exports
// 最终 return 的是 module.exports
// 所以无论你 exports 中的成员是什么都没用
exports = {
  a: 456
}

// {foo: 'haha', a: 123}
module.exports.foo = 'haha'

// 没关系，混淆你的
exports.c = 456

// 重新建立了和 module.exports 之间的引用关系了
exports = module.exports

// 由于在上面建立了引用关系，所以这里是生效的
// {foo: 'haha', a: 789}
exports.a = 789

// 前面再牛逼，在这里都全部推翻了，重新赋值
// 最终得到的是 Function
module.exports = function () {
  console.log('hello')
}

// 真正去使用的时候：
//    导出多个成员：exports.xxx = xxx
//    导出多个成员也可以：module.exports = {
//                        }
//    导出单个成员：module.exports


// 谁来 require 我，谁就得到 module.exports
// 默认在代码的最后有一句：
// 一定要记住，最后 return 的是 module.exports
// 不是 exports
// 所以你给 exports 重新赋值不管用，
// return module.exports
```

### 2.4 模块加载规则

> **模块查找机制**
>
> - 优先从缓存加载
> - 核心模块
> - 路径形式的文件模块
> - 第三方模块(拿art-template这个模块来举例)
>   - node_modules/art-template/
>   - node_modules/art-template/package.json
>   - node_modules/art-template/package.json main
>   - index.js 备选项
>   - 进入上一级目录找 node_modules
>   - 按照这个规则依次往上找，直到磁盘根目录还找不到，最后报错：Can not find moudle xxx
> - **一个项目有且仅有一个 node_modules 而且是存放到项目的根目录**

```javascript
// 如果是非路径形式的模块标识
// 路径形式的模块：
//  ./ 当前目录，不可省略
//  ../ 上一级目录，不可省略
//  /xxx 几乎不用
//  d:/a/foo.js 几乎不用
//  首位的 / 在这里表示的是当前文件模块所属磁盘根路径
//  .js 后缀名可以省略
// require('./foo.js')

// 核心模块的本质也是文件
// 核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了
// require('fs')
// require('http')

// 第三方模块
// 凡是第三方模块都必须通过 npm 来下载
// 使用的时候就可以通过 require('包名') 的方式来进行加载才可以使用
// 不可能有任何一个第三方包和核心模块的名字是一样的
// 既不是核心模块、也不是路径形式的模块
//    先找到当前文件所处目录中的 node_modules 目录
//    node_modules/art-template
//    node_modules/art-template/package.json 文件
//    node_modules/art-template/package.json 文件中的 main 属性
//    main 属性中就记录了 art-template 的入口模块
//    然后加载使用这个第三方包
//    实际上最终加载的还是文件

//    如果 package.json 文件不存在或者 main 指定的入口模块是也没有
//    则 node 会自动找该目录下的 index.js
//    也就是说 index.js 会作为一个默认备选项
//    
//    如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找
//    如果上一级还没有，则继续往上上一级查找
//    。。。
//    如果直到当前磁盘根目录还找不到，最后报错：
//      can not find module xxx
// var template = require('art-template')
// 
// 注意：我们一个项目有且只有一个 node_modules，放在项目根目录中，这样的话项目中所有的子目录中的代码都可以加载到第三方包
// 不会出现有多个 node_modules
// 模块查找机制
//    优先从缓存加载
//    核心模块
//    路径形式的文件模块
//    第三方模块
//      node_modules/art-template/
//      node_modules/art-template/package.json
//      node_modules/art-template/package.json main
//      index.js 备选项
//      进入上一级目录找 node_modules
//      按照这个规则依次往上找，直到磁盘根目录还找不到，最后报错：Can not find moudle xxx
//    一个项目有且仅有一个 node_modules 而且是存放到项目的根目录

require('a')
```

### 2.5 Package.json

> **建议每一个项目都有一个`Package.json`文件（类似产品的说明书），里面包含了项目的有关信息。**

```javascript
{
  "name": "demo",
  "version": "0.0.1",
  "description": "练习专用",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "练习"
  ],
  "author": "zhanghao",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.3.1"
  }
}
```

> **对于`package.json`文件，我们可以通过`npm init`来初始化出来**

```shell
package name: (新建文件夹) demo //项目名字
version: (1.0.0) 0.0.1  //版本号
description: 练习专用   //项目描述
entry point: (index.js) main.js //项目的入口模块
test command: //项目启动时脚本命令
git repository: //如果你有 Git 地址，可以将这个项目放到你的 Git 仓库里
keywords: 练习 //关键词
author: zhanghao //作者叫啥
license: (ISC) //项目要发行的时候需要的证书，平时玩玩忽略它
```

> **`npm install --save jquery`加上`--save`之后就可以将加载的第三方包，保存到`package.json`文件当中了，如果项目当中的`node-modules`不慎删除了，但是`package.json`还在，那直接运行`npm install`所有的包就都回来了**

