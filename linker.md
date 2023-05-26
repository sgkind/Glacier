编译过程可以分为预处理(Prepressing)、编译(Compilation)、汇编(Assembly)和链接(Linking)

## 预编译
预编译过程主要处理源代码文件中的以"#"开始的预编译指令。比如"#include"、"#define"等，主要处理规则如下：
* 将所有的"#define"删除，并且展开所有的宏定义
* 处理所有条件预编译指令，比如"#if"、"#ifdef"、"#elif"、"#else"和"#endif"
* 处理"#include"预编译指令，将被包含的文件插入到该预编译指令的位置。这个过程是递归进行的，也就是说被包含的文件可能还包含其它文件
* 删除所有的注释
* 添加行号和文件名标识，以便于编译时编译器产生调试用的行号信息及用于编译时产生编译错误或警告时能够显示行号
* 保留所有的#pragma编译器指令，因为编译器要使用它们

```
gcc -E hello.c -o hello.i
```

## 编译
编译过程就是把预处理完的文件进行一系列词法分析、语法分析、语义分析及优化后产生相应的汇编代码文件

```
gcc -S hello.i -o hello.s
```

编译过程一般可以分为6步：扫描、语法分析、语义分析、源代码优化、代码生成和目标代码优化。
```
源代码 --scanner--> Tokens --Parser--> Syntax Tree --SemanticAnalyzer--> CommentedSyntaxTree --SourceCodeOptimizer--> IntermediateRepresentation --CodeGenerator--> Target Code --CodeOptimizer--> Final Target Code
```

中间代码使得编译器可以被分成前端和后端。编译器前端负责产生机器无关的中间代码，编译器后端将中间代码转换成目标机器代码。这样对于一些可以跨平台的编译器而言，它们可以针对不同的平台使用同一个前端和针对不同机器平台的数个后端。

## 汇编
汇编器是将汇编代码转变成机器可以执行的指令，每一个汇编语句几乎都对应一条机器指令。所以汇编器的汇编过程相对于编译器来讲比较简单，它没有复杂的语法，也没有语义，也不需要做指令优化，只是根据汇编指令和机器指令的对照表一一翻译就可以了。

```
as hello.s -o hello.o
```
or
```
gcc -c hello.s -o hello.o
```

## 链接
链接过程主要包括了地址和空间(Address and Storage Allocation)、符号决议(Symbol Resoulution)和重定位(Relocation)

