# 2019年01月28日14:58:15:

#### Pytorch 中遇到的内存泄露的问题:

在训练的循环中:

​        running_loss = (float(running_loss * i) + float(loss)) / float(i + 1)

在这里，total_loss你的循环训练中积累了历史，因为它loss是一个具有autograd历史的可微变量。你可以通过编写total_loss += float(loss)来解决这个问题。

#### Pytorch 批量化初始化权重：

1. 定义一个初始化函数：

   ```python
   def weights_init(m):
       if isinstance(m, torch.nn.Conv2d): # 这里可以更换成你想要的网络类别
           torch.nn.init.kamin_normal_(m.weight, mode='fan_out')
           torch.nn.init.constant_(m.bias, 0) # bias直接设置成0就可以了
   ```

2. apply()到网络上去

   ```python
   net.apply(weights_init)
   ```

   参考连接：https://blog.csdn.net/dss_dssssd/article/details/83990511

   



