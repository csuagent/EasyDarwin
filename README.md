# EasyDarwin开源流媒体平台 #

**EasyDarwin**是由国内开源流媒体团队开发和维护的一款开源流媒体平台框架，从2012年12月创建并发展至今，从原有的单服务的流媒体服务器形式，扩展成现在的云平台架构的开源项目，更好地帮助广大流媒体开发者和创业型企业快速构建流媒体服务平台，更快、更简单地实现最新的移动互联网(安卓、IOS、微信)流媒体直播与点播的需求，尤其是安防行业与互联网行业的衔接；

## 云平台结构 ##

目前EasyDarwin流媒体平台整套解决方案包括有：**EasyCMS**(中心管理服务)，**EasyDarwin**(流媒体服务)，**EasyCamera**(开源流媒体摄像机)、**EasyPlayer**（开源流媒体播放器）、以及周边众多工具库([**EasyHLS**](https://github.com/EasyDarwin/EasyHLS "EasyHLS") / [**EasyRTMP**](https://github.com/EasyDarwin/EasyRTMP "EasyRTMP") / [**EasyRTSPClient**](https://github.com/EasyDarwin/EasyRTSPClient "EasyRTSPClient") / [**EasyPusher**](https://github.com/EasyDarwin/EasyPusher "EasyPusher") / [**EasyAACEncoder**](https://github.com/EasyDarwin/EasyAACEncoder "EasyAACEncoder"))，后续也将继续扩展的录像、回放等多种服务和工具集，各个功能单元既可以独立使用于项目，又可以整体使用，形成一个完整、简单、易用、高效的流媒体解决方案：

1. **EasyCMS** 开源的设备接入与管理服务，支持多设备、多客户端接入，能非常快速地帮助大家实现稳定的设备接入服务，可以根据自己的需求进行服务功能拆分（例如用户接入服务与设备接入服务拆分等），具体见[https://github.com/EasyDarwin/EasyDarwin/tree/master/EasyCMS](https://github.com/EasyDarwin/EasyDarwin/tree/master/EasyCMS)；

1. **EasyDarwin** 核心流媒体服务！开源流媒体服务，高效、稳定、可靠、功能齐全，支持RTSP/HLS/HTTP流媒体协议，支持安防行业需要的摄像机流媒体转发功能、支持互联网行业需要的多平台(WEB、Android、IOS)点播（Mp4）、直播（H264/MJPEG/MPEG4、AAC/PCMA/PCMU/G726）功能，支持标准WebService接口调用，具体接口调用方法和流程见：[https://github.com/EasyDarwin/EasyDarwin](https://github.com/EasyDarwin/EasyDarwin)；

1. **EasyCamera** 设备端（摄像机、移动设备、桌面程序）对接EasyDarwin平台的方案，跨平台，支持Windows、Linux、ARM，其中EasyDarwin摄像机是我们定制的一款摄像机硬件与EasyDarwin平台进行对接的方案，摄像机采用海思3518E方案，支持RTSP、Onvif、WEB管理、配套SDK工具，作为开发和演示硬件工具，我们提供了全套完备的程序和文档，既可以用于流媒体学习，又可以用于方案移植参考，更可以直接用于项目中，购买参考设备可以在：[https://easydarwin.taobao.com/](https://easydarwin.taobao.com/ "EasyDarwin")，用户可以将摄像机定制的部分替换成自己摄像机的硬件SDK，具体接入方法见[https://github.com/EasyDarwin/EasyCamera](https://github.com/EasyDarwin/EasyCamera)；

1. **EasyPlayer** RTSP流媒体播放客户端，目前只支持Windows桌面版本，后续将陆续支持Android、IOS版本，详细方案见[https://github.com/EasyDarwin/EasyPlayer](https://github.com/EasyDarwin/EasyPlayer)；


## 基本流程 ##
![](http://www.easydarwin.org/skin/easydarwin/images/architecture20150825.png)


## 直播流程 ##

<pre>

          +---------+         +----------+        +------------+        +------------+
          +  Client +         +  EasyCMS +        + EasyCamera +        + EasyDarwin +
          +---|-----+         +----|-----+        +----|-------+        +------|-----+
    +---------+--------------------+-------------------+-----------------------+---------+
    |         |                    |<-Register Online--+                       |         |
    +---------+--------------------+-------------------+-----------------------+---------+
    |         +--Get Device List-->|                   |                       |         |
    |         |                    |                   |                       |         |
    |         |<-Device List Json--|                   |                       |         |
    +---------+--------------------+-------------------+-----------------------+---------+
    |         |                    |                   |                       |         |
    |         +-Get Device Stream->|                   |                       |         |
    |         |    (Device SN)     |                   |                       |         |
    |         |                    +--request stream-->|                       |         |
    |         |                    | (EasyDarwin Addr) |                       |         |
    |         |                    |                   +---RTSP Stream Push--->|         |
    |         |                    |                   +====RTP Streaming=====>|         |
    |         |                    |                   |                       |         |
    |         |                    |<---Streaming OK---+                       |         |
    |         |<--live stream url--+                   |                       |         |
    |         |                    |                   |                       |         |
    |         +-------------------HTTP or RTSP Streaming---------------------->|         |
    |         |                    |                   |                       |         |
    +---------+--------------------+-------------------+-----------------------+---------+

</pre>

## EasyDarwin部署视频广场 ##


### 
- 部署EasyCMS接入服务器 
###
按照文档[《EasyCMS编译部署文档》](http://doc.easydarwin.org/EasyCMS/README/ "EasyCMS编译部署文档")编译、配置并部署EasyCMS；


### 
- 部署EasyDarwin流媒体服务器 


按照文档[《EasyDarwin编译部署文档》](http://doc.easydarwin.org/EasyDarwin/README/#_1 "EasyDarwin编译部署文档")编译、配置并部署EasyDarwin；

### 
- 部署EasyCamera设备端 


按照文档[《EasyCamera编译部署文档》](http://doc.easydarwin.org/EasyCamera/README/#_1 "EasyCamera编译部署文档")编译、配置并部署EasyCamera；

### 
- 整体串联 

**列表页**：js调用EasyCMS获取设备列表接口，html展示在线设备列表（[可参考EasyDarwin视频广场页面](http://www.easydarwin.org/article/video/ "EasyDarwin视频广场")）；

**播放页**：html播放页面用调用ckplayer等m3u8播放器（[可参考EasyDarwin视频播放页面](http://www.easydarwin.org/article/play/ "EasyDarwin视频播放")）；


## 获取更多信息 ##

邮件：[support@easydarwin.org](mailto:support@easydarwin.org) 

WEB：[www.EasyDarwin.org](http://www.easydarwin.org)

QQ交流群：288214068

Copyright &copy; EasyDarwin.org 2012-2015

![EasyDarwin](http://www.easydarwin.org/skin/easydarwin/images/wx_qrcode.jpg)