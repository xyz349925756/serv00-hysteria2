> [!tip]
>
> 使用本脚本部署 vless + tcp +tls , vless + ws + tls , trojan + tcp +tls 。由于中途需要使用到serv00 提供的自动更新证书服务，因此需要输入一次 ssh 密码[可以粘贴]，部署成功后  https://域名/panel.html 是单条 URL ， https://域名/sub.txt 是订阅地址。





# 前置

## 开启脚本执行权限

![image-20240731092717967](./.readme.assets/image-20240731092717967.png)



## DNS准备

https://www.cloudns.net/

申请很简单，不介绍了。

创建域点击这里的添加记录

![image-20240801214959474](./.readme.assets/image-20240801214959474.png)

![image-20240801215142149](./.readme.assets/image-20240801215142149.png)

等待这里是这个状态图标的时候就说明已经生效了。

![image-20240801215200563](./.readme.assets/image-20240801215200563.png)

> [!important]
>
> 如何查看serv00 vps 地址？
>
> 1.进入serv00 发给你的邮件找到  **Domains and subdomains:**   这里有一个自带的域名。
>
> 2.打开 运行输入 cmd (或者使用powershell) 输入 ping 域名 .(https://xxx.serv00.net/.)
>
> 命令输入  ping xxx.serv00.net   返回的信息中找到中括号内的 IP地址 就是你的A记录IP地址。
>
> 3.如果不会，脚本运行输入你的域名，会提示你当前服务器的IP地址。



## 下载脚本







