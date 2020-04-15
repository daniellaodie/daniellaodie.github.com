title: TCP协议标志 
date: 2019-10-18 18:27:12
tags: [编程, protocol]
---
```
TCP(Transmission Control Protocol)传输控制协议是网络编程重要的基础，
TCP的连接建立和连接关闭，都是通过请求－响应的模式完成的。
```

<!--more-->

### TCP 6种标志(flags)
1. SYN(synchronous建立联机)
2. ACK(acknowledgement 确认)
3. PSH(push传送) 
4. FIN(finish结束) 
5. RST(reset重置)
6. URG(urgent紧急)

---   

### TCP 三次握手

| 客户端(状态）| 建立连接（三次握手）         | 服务端（状态） |
| -----------  | ----                         | ----           |
| CLOSED       |                              | LISTEN         |
|              | SYN seq=0 ==》               |                |
| SYN_SENT     |                              |                |
|              | 《== SYN ACK ack=1,seq=0     |                |
|              |                              | SYN_RCVD       |
|              | ACK ack=1,seq=1 ==》         |                |
| ESTABLISHED  |                              | ESTABLISHED    |

* 第一次握手：主机A发送位码为SYN＝1，随机产生seq number=1234567的数据包到服务器，主机B由SYN=1知道，A要求建立联机；**报文：SYN，seq number=1234567**
* 第二次握手：主机B收到请求后要确认联机信息，向A发送ack number=主机A的seq+1(12345671)；**报文：SYN=1，ACK=1，seq number=1234567, ack number=12345671**
*  第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1，以及位码ACK是否为1，若正确，主机A会再发送ack number=(12345671)，ACK=1，主机B收到后确认seq值与ack=1则连接建立成功；**报文：ACK=1，seq number=12345671，ack number=12345671**  
* 计算规则
```
seq 为序列号
ack 为应答码
seq = 对方上次的ack；（首次发送时seq为系统随机生成）
ack = 对方的seq+1（无数据传输时） 或者 seq+L（报文数据的长度L）
```

---

### TCP 四次挥手

| 客户端(状态）| 断开连接                          | 服务端（状态）|
|----          | ----                              | ----          |
|              |FIN ACK ack=120，seq=100 ==》      |               |
| FIN_WAIT_1   |                                   |               |
|              | 《== ACK ack=101,seq=120          |               |
| FIN_WAIT_2   |                                   | CLOSE_WAIT    |
|              | 《== FIN ACK ack=101,seq=120      |               |
|              |                                   | LAST_ACK      |
|              |  ACK ack=121,seq=101 ==》         |               |
| TIME_WAIT    |                                   |   CLOSE       |

* 第一次挥手：客户端向服务器发送一个FIN报文段，将设置seq为100和ack为120，;此时，客户端进入 FIN_WAIT_1状态,这表示客户端没有数据要发送服务器了，请求关闭连接;
* 第二次挥手：服务器收到了客户端发送的FIN报文段，向客户端回一个ACK报文段，ack设置为101，seq设置为120;服务器进入了CLOSE_WAIT状态，客户端收到服务器返回的ACK报文后，进入FIN_WAIT_2状态;
* 第三次挥手：服务器会观察自己是否还有数据没有发送给客户端，如果有，先把数据发送给客户端，再发送FIN报文；如果没有，那么服务器直接发送FIN报文给客户端。请求关闭连接，同时服务器进入LAST_ACK状态;
* 第四次挥手：客户端收到服务器发送的FIN报文段，向服务器发送ACK报文段，将seq设置为101，将ack设置为121，然后客户端进入TIME_WAIT状态;服务器收到客户端的ACK报文段以后，就关闭连接;此时，客户端等待2MSL后依然没有收到回复，则证明Server端已正常关闭，客户端也可以关闭连接了。    
* 为什么是2MSL而不是MSL？
```
为什么等待2MSL，从TIME_WAIT到CLOSE？

 在Client发送出最后的ACK回复，但该ACK可能丢失。Server如果没有收到ACK，将不断重
 复发送FIN片段。所以Client不能立即关闭，它必须确认Server接收到了该ACK。Client会
 在发送出ACK之后进入到TIME_WAIT状态。Client会设置一个计时器，等待2MSL的时间。如
 果在该时间内再次收到FIN，那么Client会重发ACK并再次等待2MSL。所谓的2MSL是两倍的
 MSL(Maximum Segment Lifetime)。MSL指一个片段在网络中最大的存活时间，2MSL就是一
 个发送和一个回复所需的最大时间。如果直到2MSL，Client都没有再次收到FIN，那么
 Client推断ACK已经被成功接收，则结束TCP连接。
```
* 服务器保持了大量CLOSE_WAIT状态
```
简单来说CLOSE_WAIT数目过大是由于被动关闭连接处理不当导致的
```
* 服务器保持了大量TIME_WAIT状态 
```
有时候，如果我们换个角度去看问题，往往能得到四两拨千斤的效果。前面提到的例子：
客户端向服务端发起HTTP请求，服务端响应后主动关闭连接，于 是TIME_WAIT便留在了服
务端。这里的关键在于主动关闭连接的是服务端！在关闭TCP连接的时候，先出手的一方注
定逃不开TIME_WAIT的宿 命，套用一句歌词：把我的悲伤留给自己，你的美丽让你带走。
如果客户端可控的话，那么在服务端打开KeepAlive，尽可能不让服务端主动关闭连接，而
让客户端主动关闭连接，如此一来问题便迎刃而解了。
```
