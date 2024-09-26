### 抽象类
包含至少一个纯虚函数的类被称为抽象类。抽象类只能作为其他类的基类。且抽象类无法被实例化。
Q:为什么抽象类无法被实例化呢？
A:这时c++从设计层面考虑而做出的规定。 因为抽象类一般是某些事物的抽象体现。它无法代表一个真实存在的东西，因此无法被实例化。
### 纯虚函数
纯虚函数在类中的体现为函数声明的末尾添加了"=0"。<font color=red>纯虚函数在抽象类中可以被定义。但一般在抽象类的子类中对它进行定义，因为在抽象类中定义没有现实意义</font>。
Q：如果纯虚函数在抽象类中被定义，但子类中未被定义，那么子类是否能实例化，如果能，调用该函数的结果是什么？
A:

### 虚函数
虚函数在类外定义时不能再添加“virtual”关键字
### protected

### 智能指针
https://juejin.cn/post/7300779577060196362?from=search-suggest
#### 智能指针的使用
1. shared_ptr:
3. weak_ptr:
2. unique_ptr:
#### 智能指针的原理

### 左值，右值，左值引用，右值引用
1. 左值和右值的概念
左值：可以放在赋值号左边可以被赋值的值。**左值必须要在内存中有实体**
右值：当在赋值号邮编取出值赋给其他变量的值。**右值既可以在内存也可以在cpu寄存器**
一个对象呗作右值时，使用的是它的内容，当被用作左值时，使用的是它的地址
2. 引用
引用相当于变量别名，且引用必须初始化
    1. 声明医用时必须初始化，且一旦绑定，不可把引用绑定到其他对象。即引用必须初始化，不能对引用重定义
    2. 对引用的一切操作，就相当于对原对象的操作
3. 左值引用和右值引用
    * 左值引用： type &引用名 = 左值表达式
    * 右值引用： type &&引用名 = 右值表达式

#### std::move函数原型
```C++
template <typename T>
typename remove_reference<T>::type&& move(T &&t)
{
    return static_cast<typename remove_reference<T>::type&&>(t);
}
```

**引用折叠**
所有引用折叠最终都代表一个引用，要么是左值引用，要么是右值引用
规则：如果任一引用为左值引用，则结果为左值引用。否则结果为右值引用。
例：
* 「X& &」「x&& &」「x& &&」 都折叠为x&,当做左值处理
* 「x&& &&」「x&&」 都折叠为x&&,当做右值处理

### static_cast const_cast dynamic_cast reinterpret_cast
```c++
static_cast<new_type> (expression)
const_cast<new_type> (expression)
dynamic_cast<new_type> (expression)
reinterpret_cast<new_type> (expression)
```
#### static_cast
static_cast相当于c语言中的强转
