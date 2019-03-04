2018年12月11日22:21:29

远程连接SSH服务器： ssh -l *username* -p *port_num* *IP-adress*

参考链接:

<https://www.cnblogs.com/joshua317/articles/4740881.html>

 

使用服务器上面的jupyter notebook:

<https://www.jianshu.com/p/a9de7a089834>

1 先在服务器上面运行jupyter notebook

2 使用下面的命令 改变映射

ssh -L *local port*:*remote host*:*remote port* *SSH hostname*

ssh -L ***local_jupyter_port***:localhost:***remote_jupyter_port*** ***remote_ip*** -p ***remote_port***  -l ***username***

nohup jupyter notebook &

3 在本地机浏览器里面输入：localhost:4000

 

使用scp下载服务器上面的数据:

scp -P *port* *username*@*server_ip*:*server_file_path* *local_file_path*

http://www.hypexr.org/linux_scp_help.php