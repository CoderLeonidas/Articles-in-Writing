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

CUserAvatar: 绘制用户头像

CmmAvatarList: 管理用户头像列表

CConfImageListMgr: 获取各种图片资源

## DibSection：

含有类CDibSection，封装了图片数据以及与其相关的工具函数。



## draw_button_bundles:

含有类`CDrawButtonBundles`,封装了按钮各种状态(点击、鼠标等)下绘制的函数l

## DrawButton

## media_confui_mgr

## meida_confui_module

## mu_base

## mu_communicate

## mu_dpi_adapter

## mu_layout_mgr

## mu_share_render_container

## mu_video_multi_port_container

## mu_video_port

## mu_video_port_base

## mu_video_single_port_container

## mu_video_strip

## mu_video_wall

## MuZZHostForAudioMgr

## MuZZHostHelper

## PTNotificationCenter

## stdafx

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


