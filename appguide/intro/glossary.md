---

# 名词解释


### FreeIOE  

物联网智能网关框架。 [项目地址](http://freeioe.org)


### 应用

基于FreeIOE框架开发的物联网应用,可用于：数据采集、平台连接、设备维护、边缘计算等等


### 云平台(冬笋云)

由冬笋科技开发的物联网设备管理维护平台，并提供FreeIOE应用中心等功能。 [地址](http://cloud.thingsroot.com)


### 设备

代指FreeIOE智能网关联接的自动化设备，如PLC,CNC,电表,UPS等等

* 输入项  
	设备从传感器或本机获取的数值
* 输出项  
	用于输出到驱动器的数值或本机配置
* 控制项  
	驱使设备执行特定动作的指令


### 报文

代指通讯链路中的二进制数据流，以协议封包为单位。


### COV(变化传输)

为避免传输未变化的数据，从而浪费通讯带宽和平台服务器计算资源，而设计的数据变化传输的算法逻辑。开启该功能后，可以过滤并未变化（或未超越某个变化幅度）的数据。

* TTL: 生命周期，未变化数据的生命周期，设定该参数可使未变化数据在超越一定时间后失效，并上送当前值。
* 周期上送: 为节省设备通讯资源，打包一定时间内要上送的数据，执行压缩后上送的算法逻辑。


### 扩展

为FreeIOE应用提供基础功能的扩展包，分为:

* Lua扩展模块
* 平台相关的二进制程序/库
* 资源文件


### Skynet

FreeIOE的基础框架，为C语言开发的Actor模式的Lua服务框架


### 应用配置

以JSON为存储格式的FreeIOE应用配置信息，方便用户进行应用运行参数调整


### 设备模板

为了方便用户快速定制设备数据采集集合的配置文件（多为csv格式）。多用于非模型协议的设备数据采集应用(如Modbus)，和选择性数据采集应用。


### 设备事件

由FreeIOE或者FreeIOE应用产生的异常事件信息，用于通知异常数据、错误状态、信息记录等。


### 设备序列号

设备（包括FreeIOE智能网关设备)的唯一设备序号。一般由厂商内置到设备，或者应用根据某种规则生成的平台(全球)唯一序号。


### TODO:
