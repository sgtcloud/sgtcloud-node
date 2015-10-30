

# Socket支持

主要做实时类游戏，比如大厅游戏，和聊天室

## 服务端
服务端选用[netty-socketio](https://github.com/mrniko/netty-socketio)
这个组合比较活跃，netty框架很成熟，但操作比较复杂，结合socketio就变的简单易用，而且对现有大厅游戏模式封装的比较好，自带命名空间和房间概念
大厅游戏现在常见的有两种模式
1. 大厅+固定room，房间是运营人员在后台配置好，玩家不能自己创建，如：QQ斗地主
2. 大厅+自动room，房间由玩家自己创建，这种模式的游戏比较多，大部分竞技游戏如：CF、炫舞...以及很多卡牌游戏三国杀
不管哪种模式，大厅是固定死的

不足的地方 是netty+socket.io没有官方支持，而且网上现有资料太少

## 服务端socket支持设计
默认socket的根路径不可用，每个app的访问路径问`ws://host:port/{appid}/{NameSpace}`,appid为每个app的唯一标识，namespace为自定义。

### ~~NameSpace定义~~ 

~~只需要配置注解`@SgtSocketServer`即可，属性包含：~~
* ~~`ns`，必填，命名空间名称，即{NameSpace}所需值~~

### 内置事件
* 频道内群发消息`mass`
* 发送一对一消息`message`
* 创建房间`createRoom`
* 进入房间`joinRoom`
* 退出房间`leaveRoom`
* 房间内群发`roomMass`

### 消息格式定义
* 消息内容`message`
* 房间ID`roomId`
* 目标角色的socket sessionID `targetId`



## 客户端
h5中使用Websocket做交互，前端框架工具选择[socketio](http://www.socket.io)，[github资料](https://github.com/socketio/socket.io-client)

客户端默认不加载websocket模块，需要调用模块初始化方法以动态加载模块并初始化
### 客户端接口
* `SgtApi.socket.ceate(spaceName)`创建一个socketio对象，并初始化socket模块加载socketio库,同时建立socket连接,参数为命名空间，参数可为空，默认建立服务器保留的命名空间连接(以`{appid}`命名)。接口返回socketio的对象，可以调用socketio原始的api

