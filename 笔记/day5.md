## [登录与注册页面]

登录与注册功能(还有 git), 必须要会的技能

## [一]. 登陆与注册的静态组件----中用到 icons.png

assets 文件夹: 一般也是放置静态资源(一般放置多个组件共用的静态资源),
注:在样式文件夹也可以使用@符号[src 别名],切记在在前面加上 ~

--登陆与注册业务中的表单验证先不处理[最后一天统一处理]---简单

## [二] 注册的业务

(1). 点击验证码发送请求,

(2). 点击注册发送请求(服务器存储数据), 跳转到登录页面

## [三] 登录的业务

(1)注册----通过数据库存储用户信息(名字、密码)

(2)登录(带着用户信息)的时候---有-登录成功的时候，后台为了区分你这个用户是谁--服务器下发 token[令牌：唯一标识符]
盘录接口，做的不完美，一般登录成功服务器会下发 token,前台持久化存储 token,[带着 token 找服务器要用户信息进行展示]

(3) token 令牌
注意: vuex 仓库存储 数据(token)------------- 不是持久化的

(4)登录过后首页用户信息的展示

4.1 当用户注册成功， 用户登录【用户名+密码】向服务器发送请求（组件派发 action:userLogin）,登录成功获取到 token, 存储到仓库当中（非持久化的），路由跳转到 home 首页。
4.2 因此在首页当中（mounted）派发 action(getUserInfo)获取用户信息，以及动态展示 header 组件内容。
4.3 一刷新 home 首页，获取不到用户信息（token, vuex 非持久化存储）
4.4 持久化存储 token
4.5 存在的问题----------(导航守卫解决)
--------问题 1. 多个组件展示用户信息需要在每一个组件的 mouted 中触发 this.\$store.dispatch('getUserInfo')------不行-----放在 app 里面也不行，解决不了第一次登录的问题
--------问题 2. 用户已经登录了，就不应该会在登录页 && 没登陆，不能去购物车

(5)退出登录
退出登录需要做的事情

1. 需要发请求，通知服务器退出登录【清除一些数据，token]
2. 清除项目当中的数据【uesrInfo, token]
   -----退出后返回首页，所以派发 action 需要成功与失败的结果

(6) 导航守卫
导航: 表示路由正在发生改变。
守卫: 符合条件让跳转

1. 全局守卫: 所有的 全要排查---相当于 [大门]守卫
   ---项目当中,只要发生路由的变化,守卫就能监听到.

2. 路由独享守卫: 相当于 相应的[皇帝,妃子...]路上守卫

3. 组件内守卫: 相当于[皇帝门口]的守卫

----问题: 用户已经登录了，就不应该会在登录页

(7)统一登录的账号?
13700000000 111111
