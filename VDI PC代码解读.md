# 前言:

`zMediaApp `和`zMediaUI `一起构成了Media进程。Media进程是由Citrix插件拉起来的一个进程。在Meida进程代码中，`zMediaUI`主要就是界面UI相关的。底层通信逻辑和audio之类UI不相关的都写到`zMediaApp`里去了

`ZVideoAppVDI` 和`ZVideoUIVDI`这两个是我们client里面处理video用的。Vedio 与Media一样，是一个进程，是由citrix里面的zoomvdi拉起来的。windows那边还要做里面那个客户端，这个就在里面。 但是在vdi里面要改一点代码。所以windows那边加进来就取了这个名字。我们不用管videovdi，这是放在client里

----

# 共性文件:

## dllmain.cpp:

> DLL模块的默认入口点。当Windows加载DLL模块时调用这一函数。系统首先调用全局对象的构造函数，然后调用全局函数 DLLMain。DLLMain函数不仅在将DLL链接加载到进程时被调用，在DLL模块与进程分离时（以及其它时候）也被调用。

## 工程名.cpp

> 定义模块初始化函数`InitModule()`和模块终止函数`TermModule()`

---

# zMediaUI

## 

## ConfImageListMgr：

含有类：

CTextDrawer: 绘制文本

CUserAvatar: 封装用户头像

CmmAvatarList: 管理用户头像列表

CConfImageListMgr: 获取各种图片资源

## DibSection：

含有类CDibSection，封装了图片数据以及与其相关的工具函数。



## draw_button_bundles:

含有类`CDrawButtonBundles`,封装了按钮各种状态(点击、鼠标等)下绘制的函数

## DrawButton

## media_confui_mgr

含有类`MediaConfUIMgr`， 是UI的管理器，成员变量有ICmmMediaConfAPI、MuBase、CmmAvatarList、CConfImageListMgr、MuSettings、MuLayoutMgr、MuCommunicate、QTranslator等。继承自`MediaConfUIMgrInterface`和`ICmmMediaConfUISink`

## meida_confui_module

定义了`mu_communicate `类，继承自`ICmmMessageQueueClient` `ISBUIProvider` `MediaConfUIMgr`， 封装了UI创建的主要逻辑，以及消息的同步异步接收、通知等函数

## mu_base

定义了类：`MediaConfUIMgrInterface` `MuBase` 
`MediaConfUIMgrInterface `封装了一些UI管理器的基本事件纯虚函数

`MuBase`封装了UI管理器中的基本成员变量

## mu_communicate

定义了`MuCommunicate`类，集成自`MuBase` `UiCommunicateBase`。封装了cmd相关的事件函数(参数都是json数据)、以及发送事件到vm的一些函数(会写到数据库)

## mu_dpi_adapter



## mu_layout_mgr

定义了`MuLayoutMgr` 类，继承自`MuBase` ，含有`MuVideoWall` `MuVideoStripe` `MuVideoSinglePortContainer` `MuShareRenderContainer` 等对象，负责容器类视图的创建和布局

## mu_video_wall

定义了`MuVideoWall`类， 继承自`MuVideoMultiPortContainer`，就是我们常说的wall view，是meeting中的顶层容器。


## mu_share_render_container

定义了`MuShareRenderContainer`类，继承自`QQuickView` `VideoPortContainerInterface` `INotifcationHandler` `MuBase` 

## mu_video_multi_port_container

定义了`MuVideoMultiPortContainer`类，继承自`QQuickView` `VideoPortContainerInterface` `MuBase`。 port 的容器视图，内部维护了一个ports数组，可以存放多个port，一个port可以对应一个参会者的界面视图。


## mu_video_single_port_container

定义了`MuVideoMultiPortContainer`类，继承自`QQuickView` `VideoPortContainerInterface` `MuBase`。 port 的容器视图，内部维护了一个port。

## mu_video_port_base

定义了`MuVideoPortBase`类，继承自`VideoPortInterface` `MuBase`，定义了port的基本元素和操作。

## mu_video_port

定义了`MuVideoPort` 类，继承自`MuVideoPortBase` `INotifcationHandler` 



## mu_video_strip

定义了`MuVideoStripe`类，继承自`MuVideoMultiPortContainer`。是一个视图。尚不知是干嘛的


## MuZZHostForAudioMgr

zzhost相关


## MuZZHostHelper

zzhost相关

## PTNotificationCenter

通知相关

## stdafx

头文件定义

## UIUtils



## win_sign_helper

## ZPPicture

## ZPUtf8KeyValuePool

---

# zMediaApp



## targetver.h:

系统版本定义

## media_conf_agent:

含有`MediaConfAgent`类

## media_conf_mgr

## media_module_client

## media_user

## media_user_list

## PowerConfigure

## remote_window_mapper

## stdafx

## system_info_helper


---

# 几个重要的窗口概念：



```c++
    struct ParentWnd {
        CmmInt64 pri_wnd;
        CmmInt64 wall_wnd;
        CmmInt64 stripe_wnd;
        CmmInt64 float_wnd;
        CmmInt64 setting_wnd;
        CmmInt64 main_share_wnd;
        CmmInt64 float_share_wnd;
        ParentWnd() {
            pri_wnd         = 0;
            wall_wnd        = 0;
            stripe_wnd      = 0;
            float_wnd       = 0;
            setting_wnd     = 0;
            main_share_wnd  = 0;
            float_share_wnd = 0;
        }
    };
 ```