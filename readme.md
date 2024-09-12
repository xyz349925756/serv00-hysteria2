

# hysteria2
> [!tip]
>
> 在 serv00 上使用其他协议已经被精准识别到了。现在还有 hysteria2 目前还是用正常。另外分支vless trojan 这些协议每天上午可用，下午网速都被 hysteria2 抢去了，下午基本不能使用。socks5 一样的情况。
> 要使用 vless 选择分支 main 。

## 初始化
初始化服务器： 部署过之前的vless的就这样初始化服务器。【删除端口，网站，端口，证书等】 
```shell
$ wget -q https://github.com/xyz349925756/serv00-hysteria2/raw/hysteria2/initialize_serv00
$ chmod u+x initialize_serv00  # 如果这里又重复的会有后缀 chmod u+x initialize_serv00.1 根据实际情况调整
$ ./initialize_serv00.1;rm initialize_serv00.1
$ ./initialize_serv00
```
> [!note]
>
> 如果是第一次使用一定要打开执行脚本权限 
>
> 在ssh中执行 devil binexec on 
>
> 执行完成关闭 ssh 再使用 ssh 登入服务器


## 使用
```shell
$ git clone -b hysteria2 https://github.com/xyz349925756/serv00-hysteria2.git
$ cd serv00-v2ray ; cp hysteria2 initialize_serv00 smail2 ~ ; cd ; chmod u+x hysteria2 initialize_serv00 smail2
$ ./hysteria2 <换成您的email>
```

## 检查
```shell
$ crontab -l
@reboot nohup /home/<user>/.hysteria2/hysteria server -c /home/<user>/.hysteria2/config.yaml & disown %1
*/30 * * * * . ~/smail2
$ sockstat -l
USER     COMMAND    PID   FD  PROTO  LOCAL ADDRESS         FOREIGN ADDRESS      
<user>   hysteria    7850 4   udp46  *:5554                *:*
```

看到这些信息就表示成功了。下面的了解即可。

对应的 https://user.serv00.net 也有一个简单的web网站。

## 通用URL

```shell
$ cat .hysteria2/url.txt 
 hysteria2:   hysteria2://<user>:<password>@<ip>:<port>/?sni=www.bing.com&alpn=h3&insecure=1#<user>.serv00.net
```
这些已经在脚本中集成了。

就可以查看到URL信息将这个信息粘贴到v2rayN 这些工具中，打开YouTube看下1080P的码流就可以了。不要测速消耗流量了。

## 计划任务
默认脚本中已经添加了两条计划任务
```shell
 "@reboot nohup $HYSTERIA_WORKDIR/hysteria server -c $HYSTERIA_WORKDIR/config.yaml & disown %1" 
 "*/30 * * * * . ~/smail2" 
```
第一条的意思是：当服务器重启时，hysteria2 会自动启动。

第二条的意思是：每30分钟执行一次检查一下sockstat。也就是每个小时的0分钟，30分钟执行一次检查。当发现服务商杀进程的时候，就会发送邮件通知。

## 邮件告警
email 是serv00 自带的。在脚本中修改成自己的 email 告警即可。
有些邮箱收不到，会被认为是骚扰。多换几个邮箱服务商试试。

hysteria2部署脚本中邮箱要填写自己的！！！

# 注意：请勿用于非法业务，否则后果自负！

## 订阅连接 
数量多的可以自己将上面的 url 集中到一个文件中，然后通过这个文件来订阅。

譬如： 我将这些 url 放到 sub.txt 文件中,然后将这个文件放到 ~/domains/<user>.serv00.net/public_html/ 目录下。

订阅连接就是： https://<user>.serv00.net/sub.txt 

自己操作这里不提供订阅链接。


## 排查问题是使用到的命令
```shell
crontab -l    # 查看计划任务是否已经设置成功

kill `sockstat -l|sed "/USER/d"|awk '{print $3}'` 2> /dev/null   # 杀死进程

nohup ~/.hysteria2/hysteria server -c ~/.hysteria2/config.yaml & disown %1   # 手动启动服务

DOMAIN=$(devil www list | sed -e '/Domain/d' -e '/^$/d'|awk -F"." '{ if ($2=="serv00") print $0 }'|awk '{print $1}') # 设置域名

cat .hysteria2/url.txt | mail -s "$DOMAIN server sub" <email>  # 将订阅信息发送到email。
```