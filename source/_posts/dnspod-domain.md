title: 拥有自己的域名邮箱
date: 2016-12-28 15:39:13
tags: [dns]
---
```
不知道什么时候出现逼格这个词了，所以能作为程序员也要有自己的逼格，今天我们就来搞一下域名
邮箱，不然老用@qq.com多low啊
```

<!--more-->

### 准备工作
* 你要有qq邮箱（嘿嘿）
* 你要有域名
* 你用过dnspod吧（没有自行脑补）
> 这东西就是用来域名解析的，狗爹自己的域名解析有时候会被墙，所以呢，就有了这个东西

---

### 开始 step by step
* 打开这个地址[QQ域名邮箱](http://domain.mail.qq.com/)
* 点击创建域名邮箱
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-1.png)
* NEXT 填写域名
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-2.png)
* NEXT 选择域名提供商
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-3.png)
* NEXT(请验证域名的所有权并设置MX记录),这里dns加上三条解析记录，下面是我的，这里可能会弹出<font color="red">记录冲突</font>，没有问题，继续就可以了
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-4.png)
* 提交验证，这样就生成了域名邮箱
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-5.png)
* 但是现在你要怎么发送邮件给你自己来测试呢，这里就要注意上面步骤里面标红的成员，所以
需要添加成员
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-6.png)
* 添加成员成功后，就可以发送邮件给你的域名邮箱了，其实接收方还是你的@qq.com，只不过
现在它换了个名字
![示例](http://7u2q5h.com1.z0.glb.clouddn.com/image/domain/domain-7.png)
