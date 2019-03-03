##### C++的拷贝构造

拷贝构造在调用的情形：

1. Object B = A; Object B(A)；
2. 函数传值的时
3. 动态创建　Object* p = new Object(A);

##### virtual与静态函数

在C++中静态成员函数不能被声明为virtural函数。因为：

1. static 成员不属于任何类对象或者类实例，所以即使加上virtural 也没有意义。

2. 静态成员函数没有this指针，就访问不到这个函数。

   **虚函数的的调用关系是：this->vptr->vtable->virtual function**

