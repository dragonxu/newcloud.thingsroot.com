# 采集设备数据

ThingsLink网关作为物联网平台的数据入口，采集目标设备和系统的数据是最基础核心的功能，下面的步骤以采集一个Modbus仿真设备为例，介绍一下如何通过平台为远程的ThingsLink网关安装应用采集目标设备数据的完整过程。

这里我使用Modbus仿真软件Modsim搭配1个配置文件模拟某个设备。Modbus仿真软件的下载和安装使用请参考[“设备/模拟器”](https://help.cloud.thingsroot.com/part-i-basic/zhun-bei/she-bei-mo-ni-qi)一节。

ThingRoot平台中，针对设备的数据采集应用多是一对一的对应关系。因此，使用应用采集目标设备数据时，需要先知道目标设备的厂商、型号等信息，然后再去应用商店中按照厂商，型号等过滤条件去查找对应的应用程序，找到应用程序可能不存在（针对此设备的应用未开发）或多个（多个开发者开发了针对此设备的应用）。找不到目标设备对应的应用时，需要自己开发针对目标设备的应用（需要用户掌握ThingsLink应用开发的相关知识），或者委托平台厂商或第三方开发者开发目标设备的应用。在这里我以一个Modbus仿真设备作为目标设备来举例说明。

目标设备：

| 类型 | Modbus仿真设备 |
| :--- | :--- |
| 设备协议 | ModbusRTU |
| 通讯链路 | RS232 |
| 链路参数 | 默认9600/8/N/1，可配置 |
| 设备信息参数 | 开关量，20个，01功能码，起始地址0 |
|  | 模拟量，10个，03功能码，起始地址 |

对应应用： modbus\_collector（可采集ModbusRTU或ModbusTCP协议的设备数据，应用只支持03功能码0~9寄存器地址和01功能码0~19寄存器地址）

![](../.gitbook/assets/image%20%286%29.png)

测试步骤如下：

1. 启动Modsim32软件。创建2个配置页，配置页1选择01功能码，起始地址1，寄存器长度20，设备地址1，配置页2选择03功能码，起始地址1，寄存器长度10，设备地址1。

![](../.gitbook/assets/image%20%2820%29.png)

2. 将Modsim32软件运行到计算机的某个串口上，本测试中，我将Modsim32软件运行在另外一台Windows 7 的虚拟机上，并为Windows 7 的虚拟机添加了2个串口端口（使用命名的管道方式，服务器端），在freeioe虚拟机上也添加了2个串口端口（使用命名的管道方式，客户端）。

![](../.gitbook/assets/image%20%2823%29.png)

3. freeioe虚拟机的串口1（/dev/ ttyS0）默认已经被openwrt系统所占用，其他程序无法使用，因此在使用freeioe虚拟机通过串口采集外部设备数据时，需要给freeioe虚拟机添加2个串口或更多的串口，真正能让freeioe软件能使用的串口是除了串口1（/dev/ ttyS0）的其他串口。

4. 将Windows 7 的虚拟机中的Modsim32软件运行在串口2上，并设置串口2的参数为9600/8/N/1。

5.  登录ThingRoot平台，在自己的账户下面找到自己的freeioe虚拟网关，点击管理按钮进入网关的应用管理界面。

6.  在应用管理界面中，添加+号增加新的应用，输入关键词“modbus\_collector”进行应用查找。

7. 选择应用“modbus\_collector”查看详情获取安装参数，或者点击安装应用直接安装应用。

8. 在应用安装界面，输入应用实例名称（在目标网关中的运行实例名称，网关内唯一即可）。根据应用说明，将应用配置参数输入到下方的Json编辑框中。modbus\_collector应用可配置采集同一链路上的设备数量，这里定义1个设备（设备的序列号是“1”，设备的Modbus地址是“1”，设备的别名是“设备1”），定义串口的参数，定义链路类型是“serial”，定义子协议是rtu。完成后点击确定将会将此应用modbus\_collector（网关内的实例名称“modbus\_rtu\_test1”）安装到目标网关中并运行起来。

![](../.gitbook/assets/image%20%2814%29.png)

![](../.gitbook/assets/image%20%284%29.png)

接下来，就可以去查看应用是否采集到数据。
