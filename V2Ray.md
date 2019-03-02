v2ray linux搭建过程：https://yuan.ga/v2ray-complete-tutorial/

先要自己下载一个core包。然后跟着走就是了。

\#让当前终端走代理

https://blog.csdn.net/jassfuchang/article/details/79550460

export ALL_PROXY=socks5://127.0.0.1:1080

下载东西 使用 curl -O  因为 wget 不支持socks5协议https://www.jb51.net/article/112345.htm 

如果v2ray不好用了，可以查看下是不是配置文件出了问题了