# Zoom Mac team 开发笔记

# 1 ftp相关

## 1.1 拿包地址

>  Note: 访问ftp推荐使用`File Zilla`，安装前让IT人员关闭`SOPHOS`，否则可能无法正常打开app

ftp 地址如下：

```
Protocol: SFTP (Secure FTP)
Port: 22 (standard SFTP port)
IP: 10.10.32.140
Your username: 你自己的公司用户名(如我叫 Leonidas.Luo )
Your password: 给你分配的密码，可以自行修改
```

FTP账户可以找以下同事申请：
`Jie Jiang \ Bonnie Yang \ Evan Zhu \ Raul Zhang`

## 1.2 ftp Mac 包的路径

`/BuildPackage/client/client_46x_ep/mac/client_46x_ep_4.6.15628.0102.zoom.mac_en_222737_xcode10`


其中，`client_46x_ep`是git分支的名字，如果分支叫做`ep`，则将其换成`ep`

![](https://tva1.sinaimg.cn/large/006tNbRwly1gajh4jo5w6j30ra0f7gns.jpg)

# 2 开发工程相关
## 2.1 需要的仓库

通常需要下载以下仓库代码：

 - vendors
 - thirdparties
 - common
 - client

其中，我们对`client`的关注多一些。

## 2.2 xcode工程文件路径

`/Users/YourName/YourRepoPath/ep_new/client/src/framework/common/SaasbeeMainboard/mac/SaasBeeMainboard.xcodeproj`

其中：

- YourName: 是你的电脑用户名
- YourRepoPath: 是你放仓库的路径
- ep_new: 是一个分支名，可替换为其他分支

## 2.3 scheme

工程中的scheme非常多，如图：

![](https://tva1.sinaimg.cn/large/006tNbRwly1gajhe68wkrj30in1j1aef.jpg)

如需让工程跑起来，看到client，则选择`Zoom_UI`

## 2.4 换包

更新或切换各个仓库分支代码后，需要进行换包，否则工程会run不起来。换包过程如下：

### 2.4.1 将所有仓库切换为同一分支

以`client_46x_ep`为例

![](https://i.loli.net/2020/01/03/Ksm5xchgAaV1Snz.png)

### 2.4.2 在ftp上找到相应的需要替换的包:
在此我简称为`Sip包`和`libs`。
同样以`client_46x_ep`分支为例，我们需要在ftp上找到最新的mac包，如圖：

![](https://i.loli.net/2020/01/03/mvrWNgKeqMu19HL.png)

打開目錄，找到Sip包和libs：

- zoom_4.6.15628.0102_Sip.pkg
- mac_libs_4.6.15628.0102.zip

如圖：

![](https://i.loli.net/2020/01/03/ErpbPeFDUnqgmZy.jpg)

將2者下載下來。

### 2.4.3  使用工具進行換包

工具為Geno開發的`DevHelper`，強大如斯。

換包界面如下：

![](https://i.loli.net/2020/01/03/jm7wvyfcHNiRIus.jpg)

在截圖頂部的輸入框中，設置好換包的路徑，路徑為你倉庫中的app release路徑。

然後按工具的提示直接將2個包drag進來即可。

> 注意： 务必保证这2个包的版本是新的，如果仓库更新了，而没有使用更新后的包，则会有很多错误。 
> 
> ![](https://tva1.sinaimg.cn/large/006tNbRwly1gamxhyfxrvj30rs06xjt0.jpg)
> 
> 此时就可以试试替换上最新的包

### 2.5 编译相关

xcode的构建系统

务必在菜单`File`-`Project setting`里选择`Legacy Build System`：

![](https://tva1.sinaimg.cn/large/006tNbRwly1gamx1p63hzj30w80qswh7.jpg)

否则会出现很多错误，如：

```
Showing Recent Messages
:-1: Unable to resolve build file: XCBCore.BuildFile (namedReferencesCannotBeResolved) (in target 'zoom.us')
```















