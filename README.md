一键脚本安装shadowsocks/shadowsocksR/V2Ray + 开启bbr
---

一键脚本搭建shadowsocks/shadowsocksR/V2Ray + 设置开启自启动 + 升级内核&开启bbr加速。

## 教程如何访问
[flyzy小站](https://www.flyzy2005.com) DNS污染了，国内无法访问。

如果还在墙内，可以参考[flyzy小站最新访问方式与镜像网站地址](https://flyzyblog.com/way-to-flyzy2005/)访问教程，科学上网吧！

## 支持系统
CentOS 6+

Debian 7+

Ubuntu 12+

## 使用教程
一键搭建ss/ssr：[一键脚本搭建shadowsocks+开启bbr](https://www.flyzy2005.com/fan-qiang/shadowsocks/install-shadowsocks-in-one-command/)

一键搭建V2Ray：[一键脚本搭建V2Ray+配置与优化](https://www.flyzy2005.com/v2ray/how-to-build-v2ray/)




一键搭建SS/搭建SSR服务
注意，shadowsocks/shadowsocksR这两个只需要搭建一个就可以了！！！！SS与SSR之间的比较一直是各有各的说法，王婆卖瓜自卖自夸。我用的是SS，因为SS的iOS版本比较容易下载，并且被没有觉得ss容易被探查到~

一键搭建shadowsocks
连上购买的VPS后（以Xshell为例），你将看到如下图所示的界面：

连接Xshell结果

如红框中所示，root@vult（root@ubuntu）说明已经连接成功了，之后你只需要在绿色光标处直接复制以下代码并回车就可以了（直接复制即可，如每段代码下方截图中所示）。

1.下载一键搭建ss脚本文件（直接在绿色光标处复制该行命令回车即可，只需要执行一次，卸载ss后也不需要重新下载）

git clone https://github.com/flyzy2005/ss-fly
下载脚本

如果提示bash: git: command not found，则先安装git（你如果不知道自己是哪个系统，那就全部执行一次，然后再执行上面的那个下载命令）：

Centos系统执行这个： yum -y install git
Ubuntu/Debian系统执行这个： apt-get -y install git

2.运行搭建ss脚本代码

ss-fly/ss-fly.sh -i flyzy2005.com 1024
其中flyzy2005.com换成你要设置的shadowsocks的密码即可（这个flyzy2005.com就是你ss的密码了，是需要填在客户端的密码那一栏的），密码随便设置，最好只包含字母+数字，一些特殊字符可能会导致冲突。而第二个参数1024是端口号，也可以不加，不加默认是1024~（举个例子，脚本命令可以是ss-fly/ss-fly.sh -i qwerasd，也可以是ss-fly/ss-fly.sh -i qwerasd 8585，后者指定了服务器端口为8585，前者则是默认的端口号1024，两个命令设置的ss密码都是qwerasd）：

ss安装

界面如下就表示一键搭建ss成功了：

ssr安装成功

注：如果需要改密码或者改端口，只需要重新再执行一次搭建ss脚本代码就可以了，或者修改/etc/shadowsocks.json这个配置文件（如何修改在公众号回复vim编辑器使用）。

3.相关ss操作

修改配置文件：vim /etc/shadowsocks.json
停止ss服务：ssserver -c /etc/shadowsocks.json -d stop
启动ss服务：ssserver -c /etc/shadowsocks.json -d start
重启ss服务：ssserver -c /etc/shadowsocks.json -d restart

4.卸载ss服务

ss-fly/ss-fly.sh -uninstall
 
一键搭建shadowsocksR
再次提醒，如果安装了SS，就不需要再安装SSR了，如果要改装SSR，请按照上一部分内容的教程先卸载SS！！！

1.下载一键搭建ssr脚本（只需要执行一次，卸载ssr后也不需要重新执行）

git clone https://github.com/flyzy2005/ss-fly，此步骤与一键搭建ss一致，就是clone一键脚本代码。

2.运行搭建ssr脚本代码

ss-fly/ss-fly.sh -ssr
ssr脚本安装

3.输入对应的参数

执行完上述的脚本代码后，会进入到输入参数的界面，包括服务器端口，密码，加密方式，协议，混淆。可以直接输入回车选择默认值，也可以输入相应的值选择对应的选项：

ssr脚本参数

全部选择结束后，会看到如下界面，就说明搭建ssr成功了：

Congratulations, ShadowsocksR server install completed!
Your Server IP        :你的服务器ip
Your Server Port      :你的端口
Your Password         :你的密码
Your Protocol         :你的协议
Your obfs             :你的混淆
Your Encryption Method:your_encryption_method
 
Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!

4.相关操作ssr命令

启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
 
配置文件路径：/etc/shadowsocks.json
日志文件路径：/var/log/shadowsocks.log
代码安装目录：/usr/local/shadowsocks

5.卸载ssr服务

./shadowsocksR.sh uninstall
 

一键开启BBR加速
BBR是Google开源的一套内核加速算法，可以让你搭建的shadowsocks/shadowsocksR速度上一个台阶，本一键搭建ss/ssr脚本支持一键升级最新版本的内核并开启BBR加速。

BBR支持4.9以上的，如果低于这个版本则会自动下载最新内容版本的内核后开启BBR加速并重启，如果高于4.9以上则自动开启BBR加速，执行如下脚本命令即可自动开启BBR加速：

ss-fly/ss-fly.sh -bbr

装完后需要重启系统，输入y即可立即重启，或者之后输入reboot命令重启。

判断BBR加速有没有开启成功。输入以下命令：


sysctl net.ipv4.tcp_available_congestion_control

如果返回值为：

net.ipv4.tcp_available_congestion_control = bbr cubic reno
只要后面有bbr，则说明已经开启成功了。

 

客户端搭建shadowsocks/shadowsockR
客户端搭建ss代理
各种客户端版本下载地址：各版本shadowsocks客户端下载地址 (打不开参考flyzy小站最新镜像网站地址或者访问https://files.flyzy2005.cn）

以Windows为例（shadowsocks电脑版（windows）客户端配置教程）：

shadowsocks客户端配置

在状态栏右击shadowsocks，勾选开机启动和启动系统代理，在系统代理模式中选择PAC模式，服务器->编辑服务器，一键安装shadowsocks的脚本默认服务器端口是1024，加密方式是aes-256-cfb，密码是你设置的密码，ip是你自己的VPS ip，保存即可~

PAC模式是指国内可以访问的站点直接访问，不能直接访问的再走shadowsocks代理~

OK！一键脚本搭建shadowsocks完毕！享受科学冲浪吧！

 

客户端搭建ssr代理
各种客户端版本下载地址：各版本SS客户端&SSR客户端官方下载地址 (打不开参考flyzy小站最新镜像网站地址或者访问https://files.flyzy2005.cn）

以Windows为例：

ssr客户端配置

在状态栏右击shadowsocksR，在系统代理模式中选择PAC模式，再左击两次状态栏的图标打开编辑服务器界面，如上图所示，按照自己的服务器配置填充内容，保存即可~

PAC模式是指国内可以访问的站点直接访问，不能直接访问的再走shadowsocksR代理~

OK！一键脚本搭建shadowsocksR完毕！享受科学冲浪吧！
