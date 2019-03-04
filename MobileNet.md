### MobileNet概述

#### 1、深度可分离卷积(depthwise separable convolution)

1. 传统的卷积操作：

   - 卷积核大小为（C_in * K * K)，  一共有 C_out个，所以**总的参数个数**为C_in * K * K * C_out个。


   - 总的计算量：输出的feature map的某一个值的计算量是（C_in * K * K) ， 输出是一个shape为（C_out * H * W)的tensor，所以**总的乘法计算量**为C_in * K * K * C_out * H * W

2. 深度可分离卷积

   DepthConv：

   - 对每一个channel，对应一个K * K * 1的卷积核，生成一层（1 × H_mid × W_mid）的feature map；一共有C_in层，所以**总参数**共有K * K * C_in个。
   - 总的计算量：输出的某一个值的计算量是K * K * 1，输出的feature map是一个shape为（C_mid * H * W）的tensor，所以输出的**总计算量**是K * K * 1 * C_mid * H_mid * W_mid。(其中的C_mid = C_in)

   Pointwise Conv：

   - 直接对上面生成的tensor 进行1 × 1普通卷积，总的参数：C_mid * 1 * 1 * C_out，总的计算量为：C_mid * 1 * 1 * C_out * H * W 

   从上面参数量的比值和计算量的比值可以看出，深度可分卷积相对于传统的标准卷积可以极大的减少参数量和计算量。例如，对于输出通道 ![N=64 ](https://www.zhihu.com/equation?tex=N%3D64+) ，卷积核大小为 ![K=3](https://www.zhihu.com/equation?tex=K%3D3) 的标准卷积，参数数量变成了原来的 ![\frac{1}{64} + \frac{1}{9}](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7B64%7D+%2B+%5Cfrac%7B1%7D%7B9%7D) .  