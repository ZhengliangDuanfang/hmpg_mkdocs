# Linux使用笔记

感觉Linux相关指令用得越来越多了，在这里记录一下。

## SSH连接服务器

在终端（我用的是Windows 11上的PowerShell）输入指令以连接服务器：

`ssh <服务器默认用户名，我设为root>@<公ip> -i <密钥对的地址>`

然后报错，告诉我`Permissions for ‘xxx‘ are too open.`

解决办法参见了CSDN上 [这个博客](https://blog.csdn.net/u010571709/article/details/121990664) ，这个博客中未予以指示的步骤均点击`确定`即可。

## 在服务器上创建新用户

终端输入指令`sudo useradd -m <用户名>`创建新用户；

之后输入指令`sudo passwd <用户名>`设置该用户的用户密码；

重启SSH服务：`sudo systemctl restart sshd`

切换到刚才设置的用户：`sudo su - mintimate`

## rsync复制文件

```shell
rsync -avz --progress -e "ssh -i /path/to/key/key.pem" /origin/dir/ <用户名>@<公ip>:/destination/dir/
```

