#### 字符串的格式化

```python
>>> li = ['hoho',18]
>>> 'my name is {} ,age {}'.format('hoho',18)
'my name is hoho ,age 18'
>>> 'my name is {1} ,age {0}'.format(10,'hoho')
'my name is hoho ,age 10'
>>> 'my name is {1} ,age {0} {1}'.format(10,'hoho')
'my name is hoho ,age 10 hoho'
>>> 'my name is {} ,age {}'.format(*li)
'my name is hoho ,age 18'
```

#### Python中新式类和经典类的区别

经典类会有继承bug而新式类修复了

#### zip()函数

zip() function pairs up each elements from each iterable;

eg: zip('foo', 'bar') produce [('f', 'b'), ('o', 'a'), ('o', 'r')]

#### python中@的作用（装饰器）

https://www.cnblogs.com/cicaday/p/python-decorator.html

没有看太懂，等以后用到在看看。

#### Python中的断言

assert len(lists) >=5, '列表元素小于5个' 

如果断言不为真那么就会执行后面的语句。

#### python中re.sub 的用法

re.sub用于替换字符串中的匹配项。下面一个例子将字符串中的空格 ’ ’ 替换成 ‘-’ : 

```python
import re  
  
text = ”JGood is a handsome boy, he is cool, clever, and so on…”  
print re.sub(r‘\s+’, ‘-‘, text)  
```



#### python中闭包

字面定义：闭包是函数及其相关的引用环境组合而成的实体。在一个内部函数里，对在外部作用域的变量进行引用，那么内部函数就被认为是闭包

```python
def add(x)：
	def adder(y): return x+Y
    reutrn adder
c = add(x)
c(10)  # 结果是18
```

在这里adder(y) 就是内部函数，就是一个闭包。