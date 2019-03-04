# **学习过程中遇到的东西**

#### numpy random类

numpy.random.random() 生成随机浮点数，范围在0.0~1.0,默认为生成一个随机的浮点数，范围是在0.0~1.0之间，也可以通过参数size设置返回数据的size;

eg:

```python
import numpy
n = numpy.random.random()
print n
output:

0.429489486421

import numpy
n = numpy.random.random(size=(3, 2))  # 产生 在 0~1之间的随机数！！！！
print n

output:
[[ 0.32018625  0.22410508]
 [ 0.57830333  0.74477335]
 [ 0.08333105  0.48533304]]


numpy.random.randint() # 产生随机整数
numpy.random.randn()　# 标准正态分布随机数

import numpy as np
print np.random.randn(4, 2)
output:

[[-1.88753851 -2.54412195]
 [ 0.51856343 -1.07733711]
 [ 1.05820592 -0.23889217]
 [ 0.73309062  0.42152066]]

## 
```

#### 将NaN变成实数np.nan_to_num 

Replace nan with zero and inf with large finite numbers.

If *x* is inexact, NaN is replaced by zero, and infinity and -infinity replaced by the respectively largest and most negative finite floating point values representable by x.dtype.

#### 关于numpy.random.normal的参数的含义

axis = 1 表示的是横向

np.random.normal 参数的意义：

loc：float

​    此概率分布的均值（对应着整个分布的中心centre）

scale：float

​    此概率分布的标准差（对应于分布的宽度，scale越大越矮胖，scale越小，越瘦高）

size：int or tuple of ints

输出的shape，默认为None，只输出一个值



#### 保存矩阵（array）

<https://docs.scipy.org/doc/numpy/reference/generated/numpy.savetxt.html>

<http://www.php.cn/python-tutorials-391963.html>

```Python
 np.savetxt(string filename, array src, string fmt)
```

注意这种方法只能保存array



#### numpy中axis的理解

1. numpy 中axis 的作用：就是指的“以第几个坐标的方向，使用这个函数”

<https://blog.csdn.net/fangjian1204/article/details/53055219>

比如：

\>>> import numpy as np

\>>> data = np.array([

... [1,2,1],

... [0,3,1],

... [2,1,4],

... [1,3,1]])

\>>> np.sum(data, axis=1) // axis = 1 代表以 下标的第二位增大的方向作用函数

array([4, 4, 7, 5])         //也就是横着

2. numpy.bincount 函数，统计每个数出现的次数，再Knn的时候用到的

 

\# 我们可以看到x中最大的数为7，因此bin的数量为8，那么它的索引值为0->7

x = np.array([0, 1, 1, 3, 2, 1, 7])

\# 索引0出现了1次，索引1出现了3次......索引5出现了0次......

np.bincount(x)

\#因此，输出结果为：array([1, 3, 1, 1, 0, 0, 0, 1])



\# 我们可以看到x中最大的数为7，因此bin的数量为8，那么它的索引值为0->7

x = np.array([7, 6, 2, 1, 4])

\# 索引0出现了0次，索引1出现了1次......索引5出现了0次......

np.bincount(x)

\#输出结果为：array([0, 1, 1, 0, 1, 0, 1, 1])

3. numpy.argsort 函数。将下标按所对应的数值的大小顺序排列起来。

 https://blog.csdn.net/maoersong/article/details/21875705>

4. 向量之间计算欧式距离：

dist = numpy.sqrt(numpy.sum(numpy.square(vec1 – vec2), axis = 0))

5. numpy 中array的拼接：

numpy.concatenate([arr,arr],axis = 0)

numpy.vstack([arr,arr]) 

numpy.hstack([arr,arr])

<https://blog.csdn.net/xiaodongxiexie/article/details/71774466>



#### Numpy 数组交换两行的值：（注意下标的取值方式）

```python
import numpy as np
a = np.array([[1,2,3],[2,3,4],[1,6,5], [9,3,4]])
a[[1,2], :] = a[[2,1], :]
```



##### [numpy中的广播（broadcast）](https://blog.csdn.net/qq_36387683/article/details/80628577)

1. 会检查两个矩阵维数是否相同，如果不同，对维数少的补一，如一个二维矩阵（n,d）和一个一维数组（m,）相乘，补一操作就是把一维数组变成（1，m），**补一总是在shape数组的开始补一**。

2. 输出的数组是输入数组各维度的最大值，比如（2，3）和（3，）相乘，第一步会把（3，）变成（1，3），然后比较第一维2和1，选择2 ，比较第二维3和3 选择3，所以输出数组维度是（2， 3）。

3. 输入数组各维的值和输出数组各位的关系，要么相等，要么为一。

   例如第二步的例子中，输入数组（2，3）和输出数组（2，3）在各维的值都相等，而（1，3）和（2，3）虽然第一维不想等，但是却是1，所以可以计算。再举个反例，（2，4）和（3，）相乘，第一步转成（2，4）和（1，3），第二步比较各维，输出为（2，4），然后进行第三步，（2，4）和（2，4）的各维相等，（1，3）和（2，4）的第二维既不等于4 也不是1，计算就会出错。

4. 就高不就低

   a是一维列矩阵(6,1)，b是一维行矩阵(1,5)，注意这里b是补充了维度的。在行和列方向上分别取最大值，结果就应该是（6,5）的矩阵。a和b在参与计算之前都要先进行广播，即复制延伸。a延伸成了：[[0, 0, 0, 0, 0], [1, 1, 1, 1, 1], [2, 2, 2, 2, 2], [3, 3, 3, 3, 3], [4, 4, 4, 4, 4], [5, 5, 5, 5, 5]]b延伸成了：[[0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4]]现在经过广播之后a和b都是(6,5)的矩阵了，然后按照对应元素相加就得到最终结果了。