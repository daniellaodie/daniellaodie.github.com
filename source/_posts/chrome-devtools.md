title: chrome_devtools
date: 2017-03-19 17:01:14
tags: [前端, protocol]
---
```
DevTools 我们天天在用，然而你真正了解它么，未必
```

<!--more-->

### 了解
* DevTools 的源码就在[Google的blink项目](https://chromium.googlesource.com/chromium/blink.git/+/master/Source/devtools/)中，高度的开放。目前这么多丰富的功能，正是 Google 和其社区的共同贡献。同时它的 License 也不拒绝任何的二次开发。
* DevTools 仅仅是简单的由 HTML、JavaScript、CSS、Images 组成的，本质上就是一个 WebApp，纯粹的前端应用。当你去了解、修改它时，你不需要理解 C++ 和任何编译的知识。
* 事实上Devtools是一个充分模块化的JavaScript网页应用。它的每个功能你都可以去扩展（仅需要了解 JavaScript）。

---

### 初探
* 开启调试命令： chrome --remote-debugging-port=9222
```
i) 请确认关闭所有chrome页签
ii) 把chrome 加入到你的 path 中（环境变量）
```
* 你可以访问 http://localhost:9222/ 获取devtools列表，点击可进入debug界面，是不是很熟悉。然后你可以继续ctrl+shift+i 调试这个debug界面，network里面可以看到socket通信，当鼠标与debug界面发生交互，那么socket会不断的有消息发出、接收。
    - devtools 列表
    ![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/devtools/devtools_rd_list.png)
    - 点击查看上图其中的一个devtool
    ![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/devtools/devtools_rd_ws.png)
    - 你也可以访问 http://localhost:9222/json 提供json数据列表
    ![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/devtools/devtools_rd_jsonl.png)
* 使用json列表里面其中之一的 webSocketDebuggerUrl 来构建自己的websocket通讯，获取我们的数据
    - 这里需要注意，devtools的ws只支持单信道，所以同一时刻只能有一个连接
    - 直接上代码，使用h5的websocket连接
    ```
    var ws = new WebSocket("ws://localhost:9222/devtools/page/1e799774-96de-405f-bc3d-5f63daccc03b");

    ws.onopen = function (e) {

        console.log('Connection to server opened');
        var msg1 = {
            id: 1,
            method: "Network.enable",
            params: {}
        }

        ws.send(JSON.stringify(msg1));
    }
    ws.onmessage = function(e){
        console.log("accept server's data");
        console.log(e.data);
    }
    ```
    - 这里的消息格式要注意，同时你也可以用nodejs进行模拟，推荐ws模块
    - 根据我们发送的信息，我们就可以获得我们需要的数据，数据有了，各种问题的分析就可以迎刃而解了。具体的应用场景后面在讨论。
