# 2018年5月20日11:39:21

昨晚CUDA8.0+Theano.7.0+Ubuntu16.04安装成功，这里记录一下：
1首先要做的是：安装nvidia驱动降低GCC的版本
1.1驱动的下载与安装：
1.1.1在deepin下面的安装（安装之后会自动屏蔽nouveau）：
参考链接： https://blog.csdn.net/liaodong2010/article/details/71482304
直接用显卡驱动管理安装驱动：使用prime方案完全使用闭源驱动
注意需要在安装 nvidia-smi 不然虽然显卡安装成功了却不能nvidia-smi，命令是：
sudo apt-get update
sudo apt-get install nvidia-smi
注意点：需要安装nvidia-opencl-dev和libcudart9.1这两个包，否则会提示说cuda deriver insufficent的问题
参考链接：https://bbs.deepin.org/forum.php?mod=viewthread&tid=169539&extra=&from=singlemessage


1.1.2下载驱动
在官网上面查看应该安装的驱动的版本，下载最新的.run文件：https://www.nvidia.com/Download/index.aspx?lang=en-us
1.1.3安装驱动：
重启电脑进入tty1
查看注意点的信息
关闭图形界面：sudo service lightdm stop 或者是 gdm stop
进入驱动的下载目录
赋予安装文件可执行权限：sudo chmod +x NVIDIA-------.run
运行文件：sudo ./ NVIDIA------.run
安装完成后，重启电脑，可能需要start图形界面
sudo nvidia-smi
如果输出了显卡信息则成功
注意点：
	这篇很有帮助
	https://blog.csdn.net/ghw15221836342/article/details/79571559
在安装前需要卸载以前的驱动，：
sudo apt-get purge nvidia-*  //删除现有驱动（如果是apt安装的话）其他的安装方式可以自行百度。
禁用自带的nouveau驱动
sudo gedit /etc/modprobe.d/blacklist.conf
输入密码后在最后一行加上:  blacklist nouveau
使禁用 nouveau 真正生效终端输入 ： sudo update-initramfs –u 
电脑重启之后执行  
lsmod | grep nouveau  #没有输出，即说明成功
如果出现重启不能进入界面的情况，可以进入tty1卸载掉显卡驱动，重新安装，
卸载方法：运行安装文件，在最后加-uninstall
sudo ./ NVIDIA------.run -uninstall
重新安装时注意：出现这种情况应该是opengl lib的问题，就不要安装opengl files
方法：sudo ./NVIDIA-Linux-x86_64-375.20.run –no-opengl-files 
如果tty都不能进的话 就只有进入recovery mode里面修改文件了，可以参考：
1.	ubuntu在命令行下配置wifi
      https://blog.csdn.net/u013826101/article/details/50493136
   .	卸载显卡驱动
      $ sudo apt-get autoremove --purge nvidia-*
      $ sudo reboot
   .	ubuntu的recovery mode
      长按esc或者shift进入
      https://blog.csdn.net/luckywang1103/article/details/43157189
   .	ubuntu recovery mode root readonly filesystem 解决
      进入ubuntu recovery mode
      选择root opt
      进去后
      mount -o remount, rw /（符号一字不差）
      1.2降低gcc版本（并不需要降低gcc版本 5.5都可以）
      1.2.15.5 gcc 安装方法：
      1.2.1.1sudo apt-get install gcc-5 g++-5
      1.2.1.2更改软连接
      Cd /usr/bin
      Sudo rm gcc g++
      Sudo ln -s g++-5 g++
      Sudo ln -s gcc-4.8 gcc

1.2.2将gcc从5.4将到5.3
参考：https://blog.csdn.net/cheneykl/article/details/79114825
跟着一步步来没问题，
注意点
下载速度太慢可以先离线到百度云，用u盘拷贝上去
2然后要做的是安装CUDA
2.1 下载CUDA8和官方文档*
下载链接https://developer.nvidia.com/cuda-toolkit-archive
2.2安装CUDA
给文件可执行权限 sudo chmod a+x cuda_8.0.27_linux.run
注意在选择的时候一定要小心不要再安装驱动程序！！！！！！！！！！！！！！
其余都选yes
2.3配置环境
sudo gedit /etc/profile
文件末尾加入这两句
export PATH=/usr/local/cuda-8.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64$LD_LIBRARY_PATH
2.4重启电脑 reboot
2.5测试cuda的Samples
进入到samples目录下面 
sudo make
安装完成后，执行文件试试
cd bin/x86_64/linux/release 
./deviceQuery

如果出现则成功：


2.6注意点：期间可以参考官方文档进行操作
3安装配置Theano
3.1安装conda
可以安装miniconda 或者annaconda。
首先下载 安装包https://conda.io/docs/user-guide/install/linux.html
然后再 使用命令
bash Miniconda3-latest-Linux-x86_64.sh
它会自动配置好PATH
3.2安装Theano依赖的库
conda install numpy scipy mkl <nose> <sphinx> <pydot-ng> #<>里面的内容是可选项
pip install parameterized
3.3安装conda
conda install theano=0.7.0  pygpu
3.4安装完成之后配置文件
新建文件：sudo gedit ~/.theanorc 在文件里面写入以下内容
 [global] 
floatX=float32 
device=gpu  #注意必须是gpu不能是cuda或者cuda暂时还不知道为什么
[cuda] 
root=/usr/local/cuda-8.0
3.5测试安装结果
运行官方的程序：
Testing Theano with GPU
http://deeplearning.net/software/theano/tutorial/using_gpu.html
3.6注意点：
参考官方教程：
官方安装教程
http://deeplearning.net/software/theano/install_ubuntu.html#installation
官方UsingGPU教程
http://deeplearning.net/software/theano/tutorial/using_gpu.html

Cudnn的安装：
从官网上下载cudnn的安装包， deepin要下载那个linux对应的包， 按照官方文档给的方法吧文件复制过去就可以了。





linux下.run文件的安装与卸载

https://blog.csdn.net/caiwenfeng_for_23/article/details/43226647

Ubuntu16.04安装NVIDIA显卡驱动和CUDA时的一些坑与解决方案

https://blog.csdn.net/chaihuimin/article/details/71006654?locationNum=2&fps=1

 

Ubuntu环境变量——添加与删除

https://blog.csdn.net/u012803067/article/details/78581415

vim之快速查找功能

https://blog.csdn.net/ballack_linux/article/details/53187283

 

Ubuntu下查看显卡型号及NVIDIA驱动版本

https://blog.csdn.net/jyl1999xxxx/article/details/78871622

ubuntu+cuda安装问题总结

https://blog.csdn.net/cv_family_z/article/details/52101992

 

ubuntu16.04 + cuda8.0安装配置*

https://blog.csdn.net/iotlpf/article/details/54175064

 

Ubuntu下查看glibc版本

https://blog.csdn.net/xibeichengf/article/details/48290297

 

ubuntu 下 clang最新的安装方法已经绑定命令<https://blog.csdn.net/straydragon/article/details/79323502>

 

修改 gcc 和 g++ 的默认版本

https://blog.csdn.net/smilejiasmile/article/details/78248692

 

[专业亲测]Ubuntu16.04安装Nvidia显卡驱动（cuda）--解决你的所有困惑https://blog.csdn.net/ghw15221836342/article/details/79571559

 

给Ubuntu 16.04更换更新源

https://blog.csdn.net/fengyuzhiren/article/details/54844870

 

 

 

Ubuntu 16.04 GCC 5.4降级为5.3

https://blog.csdn.net/cheneykl/article/details/79114825

 

 

Ubuntu16.04+cuda8.0安装教程

https://blog.csdn.net/u010837794/article/details/63251725

 

 

PYCHARM

Deepin/Linux 安装破解pycharm专业版

https://blog.csdn.net/qq_34183451/article/details/79940763

 

Linux下将pycharm图标添加至桌面

https://blog.csdn.net/qq_36472696/article/details/75637163?locationNum=5&fps=1

 

 

inux入门：常用命令：bg、fg、jobs程序后台运行及唤醒https://blog.csdn.net/foryouslgme/article/details/52699608

 

Linux中怎么终止正在运行的后台程序

https://zhidao.baidu.com/question/1819125360697847748.html

 

 

theano 和 cuda 的配置：

首先需要 配置好PATH 和LD_LIBRARY_PATH

 

export PATH=/usr/local/cuda-8.0/bin:$PATH

export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH

https://blog.csdn.net/niuwei22007/article/details/50439478

然后新建文件 ~/.theanorc 在文件里面写入：

[global] 

floatX=float32 

device=gpu  #注意必须是gpu不能是cuda或者cuda0 现在暂时还不知道为什么

[cuda] 

root=/usr/local/cuda-8.0

然后 大功告成 ： 运行一下测试的样例