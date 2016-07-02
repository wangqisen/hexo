title: "Agent技术介绍"
date: 2015-12-24 20:00:17
categories: Agent,JADE
tags: [Java,Agent,JADE]
---
最近因为课程的关系，开始接触到Agent技术，翻译过来就是智能体技术。这个概念其实是想要把计算机硬件相关的部分通过抽象隐藏起来，将各个计算资源抽象为所谓的智能体。Agent不仅仅只是具有各种行为特征，来完成各种任务。而且可以在不同的网络节点进行迁移，以完成所需要的需求。参考官方文档，做了一个售书系统的demo，其中，卖家通过向经理询问来查找当前的卖家，然后与所有卖家进行沟通，选择价格最低的卖家进行交易。
## Agent运行环境和搭建过程
Agent技术的实现方案有多种，其中一种叫做JADE。JADE本身提供了Agent智能体的运行环境和生命周期管理，行为特征，迁移等等各种特性，同时还提供了一个方便开发者的可视化界面。想要将JADE运行起来，就需要配置CLASSPATH，将JADE相关的几个jar包加入到CLASSPATH中，然后使用命令行就可以启动JADE了。
例如，如果是windows系统，在我的电脑的环境变量中，在CLASSPATH这一项添加所需的jar包就可以了。如果是linux系统，需要编辑配置文件/etc/profile:
``` bash
sudo vim /etc/profile
```
在配置文件/etc/profile中添加CLASSPATH所需的所有jar包。
```bash
CLASSPATH=.:/libs/jade.jar:/libs/jadeTools.jar:/libs/iiop.jar:/libs/commons-codec-1.3.jar:/libs/http.jar
```
然后，更新配置。
```bash
source /etc/profile
```
最后，在命令行里启动就可以看到JADE启动了。
```bash
java jade.Boot -gui 
```
## 售书系统的运行

买家对应的Agent智能体是BookBuyerAgent,卖家对应的只能体是BookSellerAgent,经理则是BookManagerAgent。相关代码可以到github上查阅。

在命令行里输入：
```bash
java jade.Boot -gui s1:BookSellerAgent s2:BookSellerAgent m:BookManagerAgent "b1:BookBuyerAgent(book_name)"
```
就可以启动这些智能体了。其中，买家需要提供一个购书的书名的参数。

## 一些观点

Agent技术其实是比较古老的一个概念了。应该说，非常适用于像并行计算这样的场景下应用。特别是其提供的迁移，旅行这样的功能和消息传递机制，都是进行并行计算非常恰当的一些特征。而象JADE这样的产品并没有得到广泛的推广使用，应该也是跟其思想过于繁杂，与Map/Reduce这样的热门计算框架比较起来，多了许多并不需要的东西，同时，也缺乏相关的监控，冗余，故障修复工具的支持，只能作为一个概念来进行参考。

