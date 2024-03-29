## 这是什么?  
&nbsp; &nbsp; 这是一个关于厌倦了在windows界面写嵌入式代码的人的关于嵌入式的些许总结。或许还会有一些使用终端编译的例子。
***

# 理论部分
## 基础平台
1. **arm32**
2. **arm64**
<br>&nbsp; &nbsp; 从我的观点来看，嵌入式使用的硬件与电脑相对。与PC端经常见到的英特尔不同，arm公司才是嵌入式的king。在2011年之前，ARMv7架构用的比较多，也就是比较熟悉的32位；在ARMv8架构发布后，出现了从32位到64位的转变。  
&nbsp; &nbsp; 也就是说,一般大家都说的开发嵌入式，说的比较多的就是开发ARMv7架构的内核，体现在arduino、stm32、espidf、luatOS等等这些。而至于64位的ARMv8以上的架构，有一个单独的名字“arch64”，比如linux、raspberryOS、Harmony（也就是熟知的鸿蒙系统）。
## 编译链
1. **armgcc**
2. **x86_64-gcc**
3. **arduino cli**  
&nbsp; &nbsp; 这里举三个例子。如果你之前用keil开发过stm32，那么你就应该比较熟悉里面的AC5编译器。当你辛辛苦苦写完代码后，你会很高兴地按下“build”编译按钮，虽然你不知道发生了什么，看着一串代码出现，然后再点击“Download”下载按钮，就可以把程序下载到你的板子里面了。这里面，keil充当了IDE（集成开发环境，Integrated Development Environment）的作用，隐藏了内部的armgcc编译器，直接给你提供了结果。
&nbsp; &nbsp; 相反，如果你使用交叉编译链，比如说“arm-none-linux-gnueabihf”,你想要在你的x86_64架构的电脑上编译在ARMv7架构（也就是32位架构）上能跑的程序，那你就必须得使用交叉编译链，特别是当你想要在ubuntu20.04（一种linux的发行版）上开发stm32时，你必然会接触到如何用一行行代码而不是仅仅一个按钮来编译你的程序。当然，实际上armgcc也是交叉编译链的一种。
&nbsp; &nbsp; 当然，如果你目前还听不懂这些，也没关系，arduino你应该接触过吧？arduino cli严格来说应该不算编译链（实际上这也太扯了），我把他们三者并列仅仅是为了更清楚地说明从windows开发环境到linux开发环境的一个缓冲。你习惯了keil编译？没关系!这里有“arm-none-linux-gnueabihf”。能够让你编译的更加透彻、爽快。你习惯了arduino IDE？不如来试试arduino CLI！它说到底只不过是arduino IDE的命令行版本，是IDE的内核，是一种纯粹的关于指令的快乐。

## 硬件物理层的知识
&nbsp; &nbsp; 这里我想要借用一下OSI的网络模型，大家都知道要想把小电影发到朋友的电脑上，需要有硬件设备，要有光纤，然后对方最好还安装了微信、QQ或者是网盘。最后你小手轻轻一点，文件就“biu--”的一下发送出去了，然后对方也只要点一下就能接受文件。对于软件控制硬件的嵌入式部分同样是如此，如果你想要点一下小车上的按钮，就能够让小车“biu--”一下出发，同时还能在屏幕显示好看的画面，让8W的小喇叭开始唱歌，让红外传感器开始工作…………这也是同样的道理，在这个过程中，起作用的不是网络和光纤，而是各种硬件和协议。
***
1. **IIC**
2. **SPI**
3. **IIS**
4. **CAN**
5. **TIM**
6. **USART/UART**
7. **RS485/RS422**
8. USB

## 软件驱动层的知识
&nbsp; &nbsp; 在这里，其实我没啥想说的，主要是如何编写代码使用我刚才说的那些硬件物理层的“通道”，实际上这就是在说明一个问题——如何用程序去控制程序的引脚，也就是GPIO。实际上，GPIO一共有八种模式：四种输入模式，两种输入模式，两种复用模式。
***
1. GPIO的八种模式
2. 如何更好地利用库
3. 如何做库移植
