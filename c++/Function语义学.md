### Virtual Member Functions
如果func为一个虚函数成员，那么 ptr->func()的调用将被转换为(* ptr->vptr[1])(ptr).
* vptr 由编译器产生 指向该类的虚函数表
* 1 表示func函数在虚函数表中的索引
* 第二个ptr表示this指针

