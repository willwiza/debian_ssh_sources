# debian_ssh_sources
蔡鹅🪿出品必出炖锅/////个人使用记录，过于详细/////蔡鹅🪿出品必出炖锅
debian13安装后，开启ssh，替换国内源

非容器（lxc：旁路坑过）模式安装debian13并开启ssh
1.运行以下命令配置SSH服务器：
a.root登录
vi /etc/ssh/sshd_config

b.结尾直接添加/修改
PermitRootLogin yes
PasswordAuthentication yes
####:wq保存
或者输入以下命令：
echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config

c.重启 SSH 服务以应用更改：：
/etc/init.d/ssh restart
或者
service ssh resta
####ip addr show #查看ip

2.ssh登录成功
a.先安装sudo
apt install sudo
sudo nano /etc/apt/sources.list
注释掉#这一行，apt update 没报错就忽略
## deb cdrom:[Debian GNU/Linux 13.1.0 _Trixie_ - Official amd64 DVD Binary-1 with firmware 20250906-10:24] trixie Release

3.替换国内源
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
echo > /etc/apt/sources.list  #清空下一步直接复制粘贴，不喜欢可以一个个注释掉
sudo nano /etc/apt/sources.list  #打开粘贴以下阿里云

# 默认注释了源码镜像以提高apt update 速度，如有需要可自行取消注释
deb https://mirrors.aliyun.com/debian/ trixie main contrib non-free non-free-firmware
# deb-src https://mirrors.aliyun.com/debian/ trixie main contrib non-free non-free-firmware

deb https://mirrors.aliyun.com/debian-security/ trixie-security main contrib non-free non-free-firmware
# deb-src https://mirrors.aliyun.com/debian-security/ trixie-security main contrib non-free non-free-firmware

deb https://mirrors.aliyun.com/debian/ trixie-updates main contrib non-free non-free-firmware
# deb-src https://mirrors.aliyun.com/debian/ trixie-updates main contrib non-free non-free-firmware

#粘贴完新的源列表后，保存文件。在 nano 中，按 Ctrl + X，然后按 Y，最后按 Enter 确认。

sudo apt update & sudo apt upgrade -y
