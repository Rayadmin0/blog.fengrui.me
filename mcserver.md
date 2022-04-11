# Minecraft我的世界云服务器搭建教程

## 一、购买服务器

(熟练的朋友萌请跳过这里）
首先我们先去al云或者tx云买个服务器，有学生优惠的话一年才120，当然最低配的单核2G（实测纯净服同时在线10个人无压力）

这里以al云为例演示，首先 在搜索栏搜索学生优惠，点进去会是这样

![图片1](https://img-blog.csdnimg.cn/2020012912023819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nsb3VkMTIwOQ==,size_16,color_FFFFFF,t_70 "aly1")

然后我买的是这个，一年120，平均一个月10块，很划算。1000G的流量够够的用，5M带宽网速快一点当然好，环境就选了宝塔linux面板

![图片1](https://img-blog.csdnimg.cn/20200129120433658.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nsb3VkMTIwOQ==,size_16,color_FFFFFF,t_70 "aly2")

## 二、云服务器配置

购买之后，就可以进入控制台查看你的服务器

![图片1](https://img-blog.csdnimg.cn/20200129120746571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nsb3VkMTIwOQ==,size_16,color_FFFFFF,t_70"aly3")

使用ssh工具连接服务器，以前已经讲过了，[ssh教程](https://fengrui.me/#/ssh)。

远程连接后开始写linux代码。

获取op权限
输入以下代码
`sudo su root`

装Java
输入以下代码
`sudo yum install java-1.8.0-openjdk`

然后就去下一个MC服务端；（用最简单的纯净服演示）
可以去MCBBS官网下，记住要下载服务端
server.jar这样的文件
这里我直接发代码进行下载
`sudo wget https://launcher.mojang.com/v1/objects/3737db93722a9e39eeada7c27e7aca28b144ffa7/server.jar`

下载完毕后输入
`pwd`
可以找到当前目录 应该是/home/admin

## 三、打开一个端口
输入以下代码
`firewall-cmd --zone=public --add-port=25565/tcp --permanent`

（默认是25565）
然后重启firewall
`firewall-cmd --reload`
查看端口状态
`firewall-cmd --zone= public --query-port=25565/tcp`

查看端口状态
添加防火墙规则，给25565端口打开

## 四、配置开启Minecraft服务器
输入代码运行服务端
`sudo java -Xms512m -Xmx1024m -jar /home/admin/server.jar nogui`
解释一下，Xms是最小分配内存，Xmx是最大，然后是路径和文件，nogui是不启动图形用户界面。）

这里会报错，是因为还没有同意用户协议
输入代码
`vi eula.txt`
接下来按 i 进入编辑模式，找到eula=false更改为eula=true
然后按 Esc
再按 ：（也就是shift+；）进入指令模式，输入wq回车保存并退出vim

然后重新启动服务端
`sudo java -Xms512m -Xmx1024m -jar /home/admin/server.jar nogui`

## 就能快乐的和小伙伴玩耍了！

