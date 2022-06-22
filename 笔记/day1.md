## [一]. vue-cli 脚手架初始化项目

node + webpack + 淘宝镜像

node_modules 文件夹: 项目依赖文件夹

public 文件夹: 一般放置一些静态资源(图片), 需要注意, 放在 public 文件夹中的静态资源, webpack 进行打包的时候, 会原封不动打包到 dist 文件夹中.

src 文件夹(程序员源代码文件夹):

assets 文件夹: 一般也是放置静态资源(一般放置多个组件共用的静态资源), 需要注意, 放置在 assets 文件夹里面静态资源, 在 webpack 打包的时候, webpack 会把静态资源当做一个模块, 打包 JS 文件里面

components 文件夹: 一般放置的是非路由组件 (全局组件)

App.vue: 唯一的根组件. Vue 当中的组件(.vue)
main.js: 程序入口文件, 也是整个程序当中最先执行的文件

babel.config.js: 配置文件 (babel 相关)

package.json 文件: 认为是项目"身份证", 记录项目叫什么,项目中有那些依赖 项目怎么运行

package-lock.json 文件: 缓存性文件

README.md: 说明性文件

## [二]. 项目的其它配置

2.1 项目运行起来的时候,让游览器自动打开
---package.json
"scripts": {
"serve": "vue-cli-service serve --open",
"build": "vue-cli-service build",
"lint": "vue-cli-service lint"
},

2.2 eslint 校验工具的关闭
---在根目录下, 创建一个 vue.config.js
比如: 声明变量未使用会报错

2.3 src 文件夹简写方式, 配置别名. @
{
"compilerOptions": {
"baseUrl": "./",
"paths": {
"@/_":["src/_"]
}
},
"exclude": ["node_modules", "dist"]
}

## [三]. 项目路由的分析

vue-router
前端所谓路由: kv 键值对
key: URL (地址栏的路由)
value: 相应的路由组件
注意: 项目上中下结构

路由组件:
Home 首页路由组件, Search 路由组件, login 登录路由, Refister 注册路由
非路由组件:
Header [首页, 搜索页]
Footer [在首页, 登录页], 但是在登录页|注册是没有的

## [四]. 完成非路由组件 Header 与 Footer 业务

在项目中, 不在以 HTML + css 为主, 主要搞业务和逻辑
在开发项目的时候:
1: 书写静态页面(HTML + CSS)
2: 拆分组件
3: 获取服务器的数据动态展示
4: 完成相应的动态业务逻辑

注意 1: 创建组件的时候, 组件结构 + 组件的样式 + 图片资源

注意 2: 咱们项目采用的 less 样式, 游览器不识别 less 样式, 需要通过 less less-loader[安装 5 版本的]进行处理 less, 把 less 样式变为 css 样式, 游览器才可以识别

注意 3: 如果项让组件识别 less 样式, 需要在 style 标签的身上加上 lang-less

4.1 使用组件的步骤(非路由组件) -创建或者定义 -引入 -注册 -使用

## [五] 路由组件的搭建

vue-router
在上面分析的时候, 路由组件应该有四个: Home Search Login Register
-components 文件夹: 经常放置的非路由组件(共用全局组件)
-pages|views 文件夹: 经常放置路由组件

5.1 配置路由
项目当中配置的路由一般放置在 router 文件夹中

5.2 总结
路由组件与非路由组件的区别?
1: 路由组件一般放置在 pages|views 文件夹,非路由组件一般放置在 components 文件中
2：路由组件一般需要在 router 文件中进行注册（使用的即为组件的名字）,非路由组件在使用的时候,一般是以标签的形式使用
3: 注册完路由,不管路由组件 非路由组件身上都有$route $router 属性

$route: 一般获取路由信息[路径, query, params等等]
$router: 一般进行编程式导航进行路由跳转[push|replace]

5.3 路由的跳转?
路由的跳转有两种形式:
声明式导航 router-link, 可以进行路由的跳转
编程式导航 push|replace, 可以进行路由的跳转

编程式导航: 声明式导航能做的, 编程式导航都能做
但是编程式导航除了可以进行路由跳转, 还可以做一些其他的业务逻辑

## [六] Footer 组件显示与隐藏

显示或隐藏 v-if|v-show
Footer 组件: 在 Home, Search 显示 Footer 组件
Footer 组件: 在登录,注册时候隐藏

6.1: 我们可以根据组件身上的\$route 获取当前路由的信息,通过路由路径判断 Footer 显示与隐藏
6.2: 配置路由的时候, 可以给路由添加路由元信息[meta], 路由需要配置对象, 它的 key 不能瞎写 乱写 胡写

## [七]路由传参

7.1: 路由跳转有几种方式
比如:A->B
声明式导航: router-link (务必要有 to 属性), 可以实现路由的跳转
编程式导航: 利用的是组件实例的\$router.push|replace 方法,可以实现路由的跳转.(可以书写一些自己的业务逻辑)

8.2: 路由传参, 参数有几种写法?
params 参数:属于路径中的一部分,需要注意,在配置路由的时候,需要占位
query 参数:不属于路径的一部分,类似于 ajax 中的 queryString /home?k=v&kv=,不需要占位

## [八]路由传参相关面试题

1: 路由传递参数(对象写法) path 是可以结合 params 参数一起使用?
不可以

2: 如何指定 params 参数可传不可传?
比如: 配置路由的时候, 占位了(params 参数), 但是路由跳转的时候就不传递
路径会出现问题
http://localhost:8080/#/?k=QWE

http://localhost:8080/#/search?k=QWE

3: params 参数可以传递也可以不传递, 但是如果传递是空串, 如何解决?
4: 路由组件能不能传递 props 数据

## [九]

1: 编程式路由跳转到当前路由(参数不变),多次执行会抛出 NavigationDuplicated 的警告错误?
--路由跳转有两种方式:　声明式导航，　编程式导航
--声明式导航没有这种问题, 因为 vue-router 底层以及处理好了

1.1 为什么编程式导航进行路由跳转的时候,就有这种警告错误?
"vue-router": "^3.5.3" 引入了 promise

1.2 通过给 push 方法传递相应的成功,失败的回调函数,可以捕获当前的错误,可以解决

1.3 这种写法:治标不治本,将来在别的组件当中 push|replace,编程式导航还有类似错误
this.\$router.push({name: 'search', params: { keyword: this.keyword query: { k: this.keyword.toUpperCase() }
},() => {},() => {})

1.4 治本 index.js 中重写 push||replace
this: 当前组件实例(search)
this.$router属性:当前的这个属性,属性值VueRouter类的一个实例,当在入口文件注册路由的时候,给组件添加$router|\$route 属性
push:　 VueRouter 类的一个实例

function VueRouter() {

}
// 原型对象的方法
VueRouter.prototype.push = function() {
// 函数的上下文为 VueRouter 类的一个实例
}
let $router = new VueRouter();
$router.push(xxx)
this.\$router.push()
