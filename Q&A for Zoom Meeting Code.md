# Q&A for Zoom Meeting Code

常见方法:

- + (void)initXXX; 创建管理器
- + (void)uninitXXX; 销毁管理器，释放资源
- - (void)initUI;: 创建UI
- - (void)cleanup;: 释放资源
- - (void)relayoutUI;: UI布局
- - (void)onConfReady; 准备工作
- - (void)receiveEvent:(NSEvent*)inEvent: 接受事件
- - (void)toggleFullScreen;

> 使窗口进入或退出全屏模式；如果应用程序支持全屏，则应将菜单项添加到“视图”菜单中，并以toggleFullScreen：作为操作，将nil作为目标。

-  - (void)windowWillEnterFullScreen;
-  - (void)windowDidEnterFullScreen;
-  - (void)windowWillExitFullScreen;
-  - (void)windowDidExitFullScreen;
-  - (void)switchMinimalVideoAction;
-  - (void)forceUpdateAllVideos:(ZMVideoUpdateStrategy)strategy;
-  - (void)forceUpdateVideo:(ZMVideoUpdateStrategy)strategy userID:(ZMUserID)inUserID
-  - (void)destroyAllRenders;
-  - (void)screenResolutionDidChanged;
-  - (void) windowWillResize: (NSWindow*) sender toSize: (NSSize) frameSize;
-  - (void) windowDidResize;
-  - (void)startSendingShare;
-  - (void)stopSendingShare;
-  - (void)updateDualMonitorStatusChanged;
-  - (void)updateDualMonitorStatusChanged;
-  - (void)resetTopic;



## 1 Class files and their functions

### 1 ZPConfUIMgr

管理大部分mgr，接口封装

- ZMThumbnailMgr: Thumbnail 相关
- ZPConfSendingSharingController
- ZPConfLayoutMgr
- ZMMeetingViewMenuMgr
- ZMUserMeetingPreferences
- ZMMeetingDisplayStyleHelper
- ZMAuxUIMgr
- ZMMainUIMgr
- ZPAlertManager
- ZMConfStyleHelper
- ZMAudioMgr
- ZMRecordMgr
- ZMSilentModeHelper
- ZMQAUIMgr
- ZMAirHostMgr
- ZMNotificationCenter
- ZPConfChatMgr
- ZMShareMgr
- ZMBreakoutSessionMgr
- ZMClosedCaptionMgr
- ZMPinVideoMgr
- ZMFitBarMgr
- ZMShortcuts
- ZMAttentionTrackMgr
- ZMLiveStreamMgr
- ZMStatusBarMenuMgr
- ZMDialInPadMgr
- ZMEventMonitorMgr
- ZMCompanionMgr
- ZMInterpretationMgr
- ZMBandWidthLimitMgr
- ZMMergeMgr
- ZMConfReactionsMgr



---
## Q:

### 1
Q: weakself marco define with `__block`

```c++
#ifndef WEAK_SELF
#define WEAK_SELF __block __typeof(&*self)weakSelf = self;
#endif
```

A: 


### 2 类文件前缀“ZM”和“ZP”有何区别？何为"ZP"？

---