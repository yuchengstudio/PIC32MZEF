* [1. 概述](#1-概述)
* [2. PHY芯片及硬件接口连接确认](#2-PHY芯片及硬件接口连接确认)  

* [3. 一个工程的基本配置，包括时钟配置，熔丝位配置](#3-一个工程的基本配置，包括时钟配置，熔丝位配置)  
* [4. 简单I/O的配置](#4-简单I/O的配置)  
* [5. 添加定时器驱动](#5-添加定时器驱动)  
* [6. 如何在应用代码中调用驱动](#6-如何在应用代码中调用驱动)  
# 1. 概述 
    本文的目的在于使用Harmony从“0”开始创建一个全新的TCPIP应用。
【说明】本实验基于microchip提供的开发板 Curiosity PIC32MZ EF, 及LAN8740 PHY DB接口板，也完全可以使用自己绘制的硬件。

Curiosity PIC32MZ EF参考文件如下链接
https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/PIC32MZ%20EF%20Curiosity%20user%20guider.pdf
http://ww1.microchip.com/downloads/en/DeviceDoc/70005189A.pdf


# 2. PHY芯片及硬件接口连接确认
```
首先我们都得对自己的硬件有一个充分的了解，在基于 PIC32 的 MAC+PHY 的网络调试
中，我们必须知道：
* MAC 和 PHY 的连接方式： RMII 或者 MII；
* PIC32 这边使用的是默认(R)MII 接口还是备用(R)MII 接口；
* PHY 的具体型号， LAN8740 或者其它；
Microchip 的 Curiosity PIC32 MZ EF 采用的是 RMII 接口并且使用的是默认接口，和 SK 默
认搭配的 PHY 板子使用的就是 LAN8740 PHY DB。
注：
有一个简单的方法判断采用的是 MII 还是 RMII，看数据接口是否只用了 ETXD0~1，如果
是只用 ETXD0~1 那么就是 RMII 接口，否则使用 ETXD0~4 是 MII 接口；
判断是否用的是备用（Alternate） (R)MII 接口，只需要看 PIC32 引脚标注，如果标注为
AETXD#，有 A 前缀那么就用了备用(R)MII 接口，否则为默认(R)MII 接口。
接下来我们就可以用 MHC 一步步的进行配置和创建 TCPIP 项目了：
注：以下 MHC 配置里没有特别标注出来的地方，说明使用的是默认选项。
```
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_001.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_002.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_010.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_012.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_013.png)

# 3. 基于PIC32 Ethernet Starter kit II的 TCPIP TCP client 配置
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_011.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_006.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_006.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_006.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_007.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_008.png)
![image](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/Harmony_TCPIP_009.png)
