## [交易页面]

用户登录了才可以获取用户信息, 不登陆没办法获取到

动态展示服务器数据

业务:　　一个排他 + 数组 find 方法

## [提交订单&&支付]

1. 支付的静态组件
2. 点击提交订单的按钮的时候,还需要向服务器发起一次请求[把支付一些信息传递给服务器]---用 this.\$API 方法
3. 从今天开始,项目不在用 vuex

4. 获取支付信息(用 this.\$API 方法)
   --别再生命周期函数中使用 async---原因: 会把同步变异步

5. elementUI 使用 + 按需引入
   --已经学过的组件库
   React/Vue: antd[PC] antd-mobile[移动端]
   Vue: ElementUI[PC] vant[移动端]
   elementUI 按需引入, 配置文件按需引入, 项目需要重启的

6. 二维码生成 qrcode

7. 点击[生成二维码 + 弹出框(也要判断) + 定时器(发请求 + await 判断是否支付成功 + 成功路由跳转)]

## [个人中心]

1. 子路由组件
2. 我的订单--渲染--合并单元格
3. 分页器

## [导航守卫]

1. 全局守卫
   未登录不能去哪?
   --trade, pay, paysuccess, center------>login

2. 路由独享守卫
   ----找交易路由
   --只有从购物车界面才能跳转到交易页面(创建订单)
   --只有从交易页面(创建订单)才能跳转到支付页面
   --只有从支付页面才能跳转到支付成功页面

3. 图片懒加载----用的插件
   nprogress
   qrcode
   vue-lazyload
   https://www.npmjs.com/package/vue-lazyload

4. 自定义插件----解释

5. 表单验证---vee-validate 插件--了解即可
   -----使用方法: 参考 validate.js 模块

6. 路由懒加载---(守卫, 滚动行为, 路由元信息, 懒加载)

7. 打包上线
   项由打包后，代码都是经过压缩加密的，如果运行时报错，编出的错误信息无法准确得知是哪里的代码报错。
   有了 map 就可以像未加密的代码一样，准确输出是哪一行有错，
   所以该文件如果项目不需要是可以去除掉
   vue.config.js 配黑
   productionSourceMap:false

8. 购买云服务器
   --阿里云, 腾讯云
   --设置安全组,让服务器一些端口号打开
   --利用 xshell 工具登录服务器
   ----linux
   cd /
   ls 查看 root-家目录---------cd root
   root 目录下: mkdir 文件名字
   pwd 查看绝对路径
