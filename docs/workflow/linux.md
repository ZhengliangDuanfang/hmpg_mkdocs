# Linux使用笔记

感觉Linux相关指令用得越来越多了，在这里记录一下。

## SSH连接服务器

### 使用密钥

在终端（我用的是Windows 11上的PowerShell）输入指令以连接服务器：

`ssh <用户名，如root>@<公ip> -i <密钥对的地址>`

然后报错，告诉我`Permissions for ‘xxx‘ are too open.`

解决办法：

- 参见了CSDN上 [这个博客](https://blog.csdn.net/u010571709/article/details/121990664) ，这个博客中未予以指示的步骤均点击`确定`即可。
- 或者在Windows PowerShell中依次输入：
    
    ```shell
    icacls <密钥路径> /inheritance:r
    icacls <密钥路径> /grant:r "<用户名>:(R,W)"
    ```

### 使用密码

`ssh <用户名>@<公ip> -p <端口号> -P <密码>`

## 在服务器上创建新用户

终端输入指令`sudo useradd -m <用户名>`创建新用户；

之后输入指令`sudo passwd <用户名>`设置该用户的用户密码；

重启SSH服务：`sudo systemctl restart sshd`

切换到刚才设置的用户：`sudo su - mintimate`

## rsync复制文件

```shell
rsync -avz --progress -e "ssh -i /path/to/key/key.pem" /origin/dir/ <用户名>@<公ip>:/destination/dir/
```

## zip与unzip

压缩单个文件：`zip <压缩后的文件名> <要压缩的文件名>`，如`zip test.zip test.txt`

压缩整个目录：`zip -r <压缩后的文件名> <要压缩的目录名>`

解压缩到特定目录：`unzip <压缩文件名> -d <目标目录>`，如`unzip test.zip -d /path/to/destination`

## 复制、移动、重命名

复制：`cp <源文件或目录> <目标目录>`，如`cp test.txt /path/to/destination`

复制整个目录：`cp -r <源目录> <目标目录>`

移动：`mv <源文件或目录> <目标目录>`，如`mv test.txt /path/to/destination`

重命名：`mv <源文件或目录> <目标文件或目录>`，如`mv test.txt test2.txt`

## tmux

tmux用于将session与命令行界面分离，使得我们在退出命令行之后，程序能继续在后台运行。详见 [https://www.ruanyifeng.com/blog/2019/10/tmux.html](https://www.ruanyifeng.com/blog/2019/10/tmux.html)，此处描述最简单的操作。

新建一个会话：`tmux new -s <会话名>`

列出当前机器上运行的所有会话：`tmux ls`

进入会话：`tmux attach -t <会话名>`

退出会话，但会话中未完成的指令在后台继续运行：Windows按`Ctrl+b d`

删除会话：`tmux kill-session -t <会话名>`