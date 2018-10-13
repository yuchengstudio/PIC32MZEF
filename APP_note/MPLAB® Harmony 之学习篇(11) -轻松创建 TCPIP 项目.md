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
