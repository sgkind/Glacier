一个函数要成为可重入的，必须具备如下几个特点：
* 不使用任何（局部）静态或全局的非const变量
* 不返回任何（局部）静态或全局的非const变量的指针
* 仅依赖于调用方提供的参数
* 不依赖任何单个资源的锁（mutex等）
* 不调用任何不可重入的函数

编译器在进行优化的时候，可能为了效率而交换毫不相干的两条相邻指令的执行顺序。可以使用volatile关键字试图阻止过度优化，volatile基本可以做到两件事情：
1) 阻止编译器为了提高速度将一个变量缓存到寄存器内而不写回
2) 阻止编译器调整操作volatile变量的指令顺序
