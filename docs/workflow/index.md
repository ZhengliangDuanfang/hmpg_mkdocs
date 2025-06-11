# 工作流记录


目前使用的操作系统是 Windows 11 专业版，以及附带的WSL2 Ubuntu 22.04。

## 系统

- 截屏指令：`Win + Shift + S`
- 切换应用：`Alt + Tab`

### 键盘代替鼠标操作

[https://mcmw.abilitynet.org.uk/how-to-use-your-keyboard-to-control-the-mouse-pointer-in-windows-11](https://mcmw.abilitynet.org.uk/how-to-use-your-keyboard-to-control-the-mouse-pointer-in-windows-11)

### 直角引号输入

[https://www.zhihu.com/question/19755746/answer/2652118371?utm_id=0](https://www.zhihu.com/question/19755746/answer/2652118371?utm_id=0) 个人采用的是方法二

## Chrome

### 插件清单

- [Vimium](https://vimium.github.io/) 浏览器的Vim插件
- [GitZip for GitHub](https://gitzip.org/) 下载GitHub仓库中的部分内容
- [沉浸式翻译](https://immersivetranslate.com/zh-Hans/)
- Zotero Connector
- [TamperMonkey](https://www.tampermonkey.net/)
- Lazuli 选课辅助

## Typora

[https://github.com/Delppine1024/TGreen/blob/master/README-CN.md](https://github.com/Delppine1024/TGreen/blob/master/README-CN.md) 

- 使用方法：替换`{Install_Location}/resources/app.asar`。
    - 对于1.7.6版本，可以查看[本站备份](../assets/asar-v1.7.6-windows-x64.zip)。
- 为图片指定自动存储路径：文件->偏好设置->图像->插入图片时

## PDF

- [Zotero 6](https://www.zotero.org/download/)
    - [直接下载链接](https://www.zotero.org/download/client/dl?channel=release&platform=win32&version=6.0.36)
    - [Zotero PDF Translate](https://zotero.yuque.com/staff-gkhviy/pdf-trans)
- ABBYY：用于竖排文字识别。
    - [https://www.cc98.org/topic/5360319](https://www.cc98.org/topic/5360319)
    - [https://pan.baidu.com/s/1vvk_h9mN04oMxNjNojs0qQ](https://pan.baidu.com/s/1vvk_h9mN04oMxNjNojs0qQ) 密码 1111
- SumatraPDF：PDF阅读器
    - [https://www.sumatrapdfreader.org/free-pdf-reader](https://www.sumatrapdfreader.org/free-pdf-reader)
- pdfarranger：PDF编辑器
    - [https://github.com/pdfarranger/pdfarranger](https://github.com/pdfarranger/pdfarranger)

## 视频

- [PotPlayer](https://potplayer.daum.net/)：播放器
- [ffmpeg](https://www.ffmpeg.org/)：视频处理
    - [中文教程](https://wklchris.github.io/blog/FFmpeg/index.html)
- [OBS Studio](https://obsproject.com/)：录屏

## 其他

- 7-Zip：解压
- FileZilla Client：FTP客户端
- uTorrent：做种
- Geek Uninstaller：卸载软件
- Everything：文件搜索
- WinMerge：文本比较
    - 发现也可以用VSCode：`code --diff <file1> <file2>`
- 语雀：笔记

## 不常用的软件

### Solidworks

[https://getintopc.com/softwares/solidworks-2022-free-download-6999973/?id=001996334662](https://getintopc.com/softwares/solidworks-2022-free-download-6999973/?id=001996334662)

### Minecraft

从[这个地方](https://www.mcnav.net/)找到了PCL2，Java是按引导自动下的。其实最开始用的是HMCL，但是似乎由于MCBBS那里发生了一些事情无法下载，才转战的。

### 植物大战僵尸

[http://lonelystar.org/download.htm](http://lonelystar.org/download.htm) 似乎只能用HTTP访问，不支持HTTPS。

## 目前所能使用GPU的环境

```shell
conda create -n <name> python=3.9 -y
conda activate <name>
pip install torch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 --index-url https://download.pytorch.org/whl/cu121
# 这个版本conda install后，numpy版本与torch版本不兼容，导致无法使用
```