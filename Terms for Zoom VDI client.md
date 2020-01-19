# Terms for Zoom VDI client

zVideoUI

zVideoApp

- Conf 
- AudioSesscionMgr
- VideoSesscionMgr
- ShareSesscionMgr


MCM: 设备驱动、渲染等。在VDI项目中，MCM和SDK从VM移动到了Thin CLient。SDK用于ThinCLien直接和MMR通信，MCM用于直接利用终端设备进行采集、编解码等。（将所有外设相关的操作放在终端处理）。VM中其实有个虚拟的MCM，也是由audio_director、video_director、share_director组成，用于和上层VideoApp进行通信，同时通过ICA通道与ThinCLient的MCM进行通信。关于SDK中的cmd session和share session是放在VM端的。如果share session放在client端，会导致share app时，只能share citrix的整个窗口，而没法share VM里某个app的窗口。因此client端的SDK 只有video session 和 audio session。

- audio_director
- video_director
- share_director

Nydus

Viper
 
Codec

cmd

Qos: （Quality of Service，服务质量）指一个网络能够利用各种基础技术，为指定的网络通信提供更好的服务能力，是网络的一种安全机制， 是用来解决网络延迟和阻塞等问题的一种技术。

MMR

cptHost

cptShare

ZoomMedia: 是一个进程，由Zoom Plug-in dll 创建

zMediaApp

zMediaUI


Zoom Plug-in dll: 运行在Citrix Receriver中的Zoom 插件，负责和Cirtix Server通过ICA虚拟通道进行通信。另外创建一个ZoomMedia进程。主要起中转和桥梁的作用。
Meeting Process: 普通客户端或者VM中Zoom 客户端的进程
Media Process: 由Zoom Plug-in dll 创建的一个进程，负责thin client 设备的采集，video、audio session的上下行， meeting 的真实逻辑基本跑在这个进程中。

SDK: 网络相关的链接

- cmd session
- audio session
- video session
- share session



log是vdi lcient很重要一块。


分辨率 
帧率



[Virtual Channel SDK](https://www.citrix.com.cn/community/citrix-developer/xenapp-xendesktop/virtual-channel-sdk.html)


Citrix虚拟通道是双向的可靠连接，用于在最终用户设备上的Citrix主机（XenApp或XenDesktop）和Citrix Receiver之间交换通用数据包数据。例如：声音，图形，客户端驱动器映射和打印只是Citrix编写的一些虚拟通道。

Citrix虚拟通道软件开发套件（VCSDK）使软件工程师可以编写主机端应用程序和Citrix Receiver端驱动程序，以使用Citrix ICA协议支持其他虚拟通道。主机端虚拟通道应用程序在XenApp或XenDesktop上运行，虚拟通道的客户端部分在Citrix Receiver所在的本地设备上运行。该SDK支持为Citrix Receiver的Win32，Linux和Mac OSX版本编写新的虚拟通道。有关支持的客户端版本的详细信息，请参见随附的文档。