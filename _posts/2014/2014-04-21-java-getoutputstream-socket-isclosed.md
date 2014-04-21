---
layout: post
title: "Android Java socket异常"
description: ""
category: java, android
tags: [java, android, socket, 网络]
---

## 问题

最近在做Android上连接打印机的项目，遇到一个问题：`socket`正常连接后，在调用`socket`的`getOutputStream`时抛出异常提示:
> java.net.SocketException: Socket is closed

一开始，我很诧异，这个异常就很奇怪，明明前面的`socket`也正常创建连接且没有关闭，为什么到这就变成已关闭呢？查了半天，终于在[SO](http://stackoverflow.com/questions/8890303/behavior-of-java-sockets-when-closing-output-stream)上找到问题根源：原来我在使用`Writer`对象就关闭了它，这就引起`OutputStream`的关闭，进而引起`socket`的关闭，从而就出错了：
> Writer.close()  --> OutputStream.close() -->  Socket.close()

连锁反应啊！

还有另外一个问题：
> 创建完`socket`后，在某个代码分支，我忘了关闭`socket`了

从而在一定程度上也造成了`socket`连接的问题。

## 解决方法

知道问题根源，就可以想办法解决了，那就是创建一个`Writer`的成员变量，其在发送完数据后`flush`一下，无需马上关闭，等程序退出再关闭就可以了。解决`socket`连接问题，就可以正常打印了。

## 反思

总的来说，就是
> 细节是魔鬼，一知半解很危险！

- 不要想当然的以为某些自己未接触过的东西很困难或很简单，接触过后才能有了解，才好作出评判；
- 从网上找某个功能的实现，一定要充分了解代码的上下文及其实现原理，切不可复制粘贴罢了；
- 打好基础，才能盖高楼，天才也是“一万小时”的积累的，警惕好高骛远。