注：此方法已因RustDesk在中国地区停止服务而失效。

参考：[https://www.oschina.net/news/291123](https://www.oschina.net/news/291123)

---

以下内容建立在我前些日子获取了一台阿里云ECS服务器的基础上，服务器的获取参考了CC98论坛上的 [这个帖子](https://www.cc98.org/topic/5739105) （浙江大学校网打开）。尝试探索这个功能也是受这个帖子的指点。具体配置主要按照从B站发现的 [教程](https://www.mintimate.cn/2023/08/27/guideToHostRustDesk/) 进行。

### 下载服务端

到[RustDesk Server的GitHub发布地址](https://github.com/rustdesk/rustdesk-server/releases)，选择合适版本，复制对应链接，到服务器上使用wget下载解压：`wget <链接>` ，例如我的是`wget https://github.com/rustdesk/rustdesk-server/releases/download/1.1.10-3/rustdesk-server-linux-amd64.zip`

使用unzip解压：`unzip <rustdesk-server-（略）.zip>`，例如我的是`unzip unzip rustdesk-server-linux-amd64.zip`，我最开始还没有unzip，则先运行`apt-get install zip`下载zip和unzip。我下载的版本看起来比较老了，可能是apt源的问题。

重命名：`mv <解压后文件夹名> RustDesk`，我的是 `mv amd64 RustDesk`

### 使用screen运行

安装screen：`sudo apt install screen`

然后报错：`<用户名> is not in the sudoers file.This incident will be reported.`于是我参考了CSDN上[这篇文章](https://blog.csdn.net/qq_23327993/article/details/122063031)的3.1部分，先`exit`以下切换回root用户，手动修改了现有用户的权限，详情不表。

解决报错并重新安装后，切换到上面自定义的用户，切到RustDesk文件夹，先运行RustDesk的hbbs：
```shell
screen -R myHbbs

./hbbs
```
然后按`Ctrl+a`和`d`返回主终端，运行RustDesk的hbbr：
```shell
screen -R myHbbr

./hbbr
```

然后按`Ctrl+a`和`d`返回主终端。

如果运行`screen -ls`可以看到两个sockets正在运行，就没问题了。

这时`ls`一下，可以看到`RustDesk`目录下有一个`.pub`公钥文件。通过`cat <文件名.pub>`显示`.pub`公钥文件，然后手动复制。

### 配置本地客户端

到 [RustDesk客户端的GitHub发布地址](https://github.com/rustdesk/rustdesk/releases) 寻找本地主机对应的安装包，我下的是Windows的。打开后，我点击了左侧的「安装」按钮，但不点应该也行。

点击左侧ID处竖直三点图标，找到「网络」配置，ID服务器和中继服务器我都填的是服务器的公网IP，Key填上一步手动复制的`.pub`公钥文件的内容，注意以`=`结尾，然后点击「应用」。

然后发现客户端右侧左下角提示`未就绪，请检查网络设置`，重新看了一遍最上面提到的参考教程，发现可能是端口配置问题。于是参考了[这篇文章](https://developer.aliyun.com/article/1209367)，开放了TCP的21115/21119（即从21115到21119之间的5个端口）和UDP的21116，客户端立刻就转为`就绪`了。

还是到客户端的发布地址，找到了Andriod的安装包，通过USB线将手机与电脑连接，选择「传输文件」，然后在电脑上下好`.apk`安装包传过去（我喜欢传到Download目录下面的Weixin文件夹里面），在手机上打开文件管理器，在对应位置找到安装包安装，安装完成打开后同样进行「网络」配置，步骤同上。

!!! warning "重要警告"
    以下步骤很可能赋予控制端屏幕录制和控制输入的权限，极易造成个人信息泄露和财产损失，如对方是陌生人，请不要继续进行。

### 测试使用

两端都显示`就绪`后，在任一端输入对方ID，点击「连接」即可。权限设置仅需按照弹窗指示操作即可。



