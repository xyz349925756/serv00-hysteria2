

# hysteria2


初始化服务器： 部署过之前的vless的就这样初始化服务器。【删除端口，网站，端口，证书等】 
```shell
$ ./initialize_serv00
```


```shell
$ git clone -b hysteria2 https://github.com/xyz349925756/serv00-v2ray.git
$ cd serv00-v2ray ; cp hysteria2 initialize_serv00 smail2 ~ ; cd ; chmod u+x hysteria2 initialize_serv00 smail2
$ ./hysteria2 wang@cloudb.pub
```

检查
```shell
$ crontab -l
@reboot nohup /home/<user>/.hysteria2/hysteria server -c /home/<user>/.hysteria2/config.yaml & disown %1
*/30 * * * * . ~/smail2
$ sockstat -l
USER     COMMAND    PID   FD  PROTO  LOCAL ADDRESS         FOREIGN ADDRESS      
<user>   hysteria    7850 4   udp46  *:5554                *:*
```


看到这些信息就表示成功了。

对应的 https://<user>.serv00.net 也有一个简单的web网站。

```shell
$ cat .hysteria2/url.txt 
 hysteria2:   hysteria2://cdeb46@85.194.243.117:5xx/?sni=www.bing.com&alpn=h3&insecure=1#<user>.serv00.net
```
就可以查看到URL信息将这个信息粘贴到v2rayN 这些工具中，打开YouTube看下1080P的码流就可以了。不要测速消耗流量流量了。


