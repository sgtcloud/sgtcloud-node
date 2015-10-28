

# Socket支持

主要做实时类游戏，比如大厅游戏，和聊天室

## 服务端
服务端选用[netty-socketio](https://github.com/mrniko/netty-socketio)
这个组合比较活跃，netty框架很成熟，但操作比较复杂，结合socketio就变的简单易用，而且对现有大厅游戏模式封装的比较好，自带命名空间和房间概念
大厅游戏现在常见的有两种模式
1、大厅+固定room，房间是运营人员在后台配置好，玩家不能自己创建，如：QQ斗地主
2、大厅+自动room，房间由玩家自己创建，这种模式的游戏比较多，大部分竞技游戏如：CF、炫舞...以及很多卡牌游戏三国杀
不管哪种模式，大厅是固定死的

不足的地方 是netty+socket.io没有官方支持，而且网上现有资料太少

## 服务端socket支持设计
默认socket的根路径不可用，每个app的访问路径问`ws://host:port/{appid}/{NameSpace}`,appid为每个app的唯一标识，namespace为自定义。

### NameSpace定义
只需要配置注解`@SgtSocketServer`即可，属性包含：
* `ns`，必填，命名空间名称，即{NameSpace}所需值 





## 客户端
h5中使用Websocket做交互，前端框架工具选择[socketio](http://www.socket.io)，[github资料](https://github.com/socketio/socket.io-client)
