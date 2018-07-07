* [1. 概述](#1-概述)
* [2. 如何建立一个空的工程，及如何启动Harmony](#2-如何建立一个空的工程，及如何启动Harmony)  
* [3. 一个工程的基本配置，包括时钟配置，熔丝位配置](#3-一个工程的基本配置，包括时钟配置，熔丝位配置)  
* [4. 简单I/O的配置](#4-简单I/O的配置)  
* [5. 添加定时器驱动](#5-添加定时器驱动)  
* [6. 如何在应用代码中调用驱动](#6-如何在应用代码中调用驱动)  
# 1. 概述 
```
    本文的目的在于使用Harmony从“0”开始创建一个全新的应用工程，比如产生一个LED 500ms闪烁应用程序。
【说明】本实验基于microchip提供的开发板 Curiosity PIC32MZ EF, 也完全可以使用自己绘制的硬件。
```
    Curiosity PIC32MZ EF参考文件如下链接
https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/PIC32MZ%20EF%20Curiosity%20user%20guider.pdf
    
    

# 2.如何建立一个空的工程，及如何启动Harmony
 | 步骤 | 图示 | 说明 |
 | - | :----- | :-- | 
 | 1 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_001.jpg) | 在MPLAB X IDE环境下创建32-bit MPLAB Harmony Project的工程 | 
 | 2 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_002.jpg) | 请根据图示说明进行相应的选择，选择完后点击“finish”按键，会自动产生一个harmony配置环境，参考步骤3. | 
 | 3 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_003.jpg) | Harmony配置的工作主要在配置区域完成，对不同应用的需求，有相应的配置。后续步骤会根据此章节要完成LED闪烁的功能做相应的harmony配置。 |


# 3.一个工程的基本配置，包括时钟配置，熔丝位配置

 | 步骤 | 图示 | 说明 |
 | - | :------- | :- | 
 | 1 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_004.jpg) | 此图是PIC32MZ内部时钟的分布图，可以做灵活配置，产生不同的时钟应用，以下的步骤只是比较常用的配置模式之一 | 
 | 2 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_005.jpg) | 选择系统时钟源，如红线标注，FNOSC选择SPLL, 系统时钟源就会由SPLL（系统锁相环）提供主时钟 | 
 | 3 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_006.jpg) | POSCMOD选EC,表示选择外部晶体，Primary Oscillator 选择框里应该填写相应外部振荡器的频率，点击auto-Caculate可以进行PLL时钟自动计算，如步骤4所示，在这里可以自定义SPLL输出的时钟。 |
 | 4 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_007.jpg) |  |
 | 5 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_008.jpg) | 参照以上步骤，一个简单的带系统锁相环的系统时钟就配置好了，点击保存按钮，系统会保证相关配置信息。 |
 | 6 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_009.jpg) | 点击“code”按钮，就会自动生成代码，但到目前为止，我们没有产生任何实际的应用，生成的代码看不出任何应用效果。 |
 | 7 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_010.jpg) | 回到配置树窗口，器件配置的DEVCFG0中的 ICE\ICD Comm channel select(ICESEL)非常关键，必须根据实际原理选择相应的编程口，否则编程器无法正确连接芯片。curiosity 的板子默认是ICS_PGx2 所以这里需要做更改。 |
 
 


# 4.简单I/O的配置

 | 步骤 | 图示 | 说明 |
 | - | :----- | :- | 
 | 0 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_011.jpg) | 图形化管脚配置器的启动（请参考图中 “MPLAB Harmony Graphical Pin Manager”）章节相关内容。 | 
 | 1 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_013.jpg) | 在配置树窗口中选择“Pin Diagram窗口”。 | 
 | 2 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_014.jpg) | | 
 |   |1.找到C1RX功能脚，可以看到该功能脚可以配置在RE6，RC4，RC6，RB3，RB0，RD15的PIN口。 2.一旦我选定了RC4作为C1RX口，可以看见功能脚其他的映射PIN口就变灰色，也就是说该功能脚不能再映射到其他PIN口了，同时,RC4也不能作为其他功能脚的映射，而且RC4这时已经自动更名为C1RX. 【备注 Pin Table窗口是用以配置外设功能脚的，如果只是为了设置一个普通的I/O线，不需要在此设置，可以关注步骤3】
 | 3 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_020.jpg) ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_016.jpg)|  | 
 | 4 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_018.jpg) | 保持| 
 | 5 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_019.jpg) | 点击代码生成| 
 
# 5.添加定时器驱动
 | 步骤 | 图示 | 说明 |
 | - | :----- | :- | 
 |0|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_021.jpg)|在原有的项目工程上启动Harmony,在“配置树”中找到“timer”,路径为“MPLAB Harmony & Application Configuration” ——>Harmony Framework Configuration ——> System Servics ——> Timer|
 |1|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_022.jpg)|保存配置，并启动Generate Project,这里我们可以选择“Prompt merge for All Differences” 这样我们可以清晰得看清楚新产生的代码会做哪些细节更改。|
 |2|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_023.jpg)||
 |3|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_024.jpg)||


# 6.如何在应用代码中调用驱动
 参考链接：
 http://blog.163.com/yucheng_studio/blog/getBlog.do?bid=fks_084066083086085065084083095069072084087075081086082067083084
 
 |说明|
 |-|
 |通过以上步骤，我们已经建立了基本的软件框架，同时添加了I/O口的配置，点亮了LED1，而且我们还添加了Timer的定时器服务驱动，接下来要实现如何把他们串联起来实现，LED灯闪烁的应用代码。|
 
 | 步骤 | 图示 | 说明 |
 | - | :----- | :- | 
 |0|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_025.jpg)|要完成我们最终的应用代码，我们只要修改LED_FLASH.h, LED_FLASH.c相关的修改。注意LED_FLASH这个名字是可以在harmony配置树下修改的。|
 |1|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_026.jpg)|在状态机的枚举结构体中添加应用程序的“状态”，状态的定义根据应用程序的实际执行情况定义。在LED_Flash应用中无非就两个这状态：1.延时启动。2.延时完成【这个时候启动LED翻转】|
 |2|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_027.jpg)|枚举类型的定义会在LED_FLASH.c中进行。|
 |3|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_028.jpg)|LED_FLASH工程主循环的状态机机制，及在相应状态下都需要添加什么工作。|
 |备注|源文件参考：https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/LED_FLASH%E5%B7%A5%E7%A8%8B%E4%B8%BB%E5%BE%AA%E7%8E%AF%E7%8A%B6%E6%80%81%E6%9C%BA%E5%88%87%E6%8D%A2%E6%B5%81%E7%A8%8B.vsdx||
 |4|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_029.jpg)|添加定时器的句柄变量，最好按照自动生成的代码原有的位置格式添加相关数据|
 |5|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_030.jpg)|句柄数据类型的定义在相关模块的.h文件下可以找到，这个很重要，以后使用句柄的时候都可以找到相应的数据类型|
 |6|程序初始化流程||
 |6.1|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_031.jpg)|初始化从main.c函数开始，这里不需要用户做任何工作|
 |6.2|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_032.jpg)|初始化的主函数在system_init.c这个文件里，这里包含了系统所有的初始化工作，包括harmony自动生成的，以及应用程序初始化的接口函数LED_FLASH_Initialize（），同样，在这里我们也不需要做任何工作|
 |6.3|![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_033.jpg)|这里是应用程序初始化的执行函数，需要根据应用需求更改，其中状态机的初始化系统已经自动完成“led_flashData.state = LED_FLASH_STATE_INIT;”，用户根据应用的需要添加其他初始化，比如这里的sysTMRHandle = SYS_TMR_HANDLE_INVALID|
