* [1. 概述](#1-概述)
* [2. 如何建立一个空的工程，及如何启动Harmony](#2-如何建立一个空的工程，及如何启动Harmony)  
* [3. 一个工程的基本配置，包括时钟配置，熔丝位配置](#3-一个工程的基本配置，包括时钟配置，熔丝位配置)  


# 1. 概述 
```
    本文的目的在于使用Harmony从“0”开始创建一个全新的应用工程，比如产生一个LED 500ms闪烁应用程序。
【说明】本实验基于microchip提供的开发板 Curiosity PIC32MZ EF, 也完全可以使用自己绘制的硬件。
```
    

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
 | 7 | ![images](https://github.com/yuchengstudio/PIC32MZEF/blob/master/APP_note/pictures/harmony_start_010.jpg) | 回到配置树窗口，器件配置的DEVCFG0中的 ICE\ICD Comm channel select(ICESEL)非常关键，必须根据实际原理选择相应的编程口，否则编程器无法正确连接芯片。curiosity 的板子默认是ICS_PGx1 所以这里不用做更改。 |
 
 






