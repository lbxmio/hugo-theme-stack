+++
author = "coucou"
title = "C语言——内存篇"
date = "2023-08-01"
description = "C语言专题之内存篇"
categories = [
    "C语言"
]
tags = [
    "C语言","内存篇"
]

+++


![](1.jpg)

## C语言——内存

### 内存分配方式

>1. **栈内存分配（Stack Allocation）**：
>
>   - 栈内存是一种自动分配和释放的内存，用于存储局部变量和函数调用的上下文信息。
>   - 变量在函数内部声明时，存储在栈内存中。栈的特性是后进先出（LIFO），所以最后进入栈的变量会最先被释放。
>
>   ```c
>   void someFunction() {
>       int x; // 在栈上分配内存
>       // 函数执行完毕后，x 的内存会被自动释放
>   }
>   ```
>
>2. **堆内存分配（Heap Allocation）**：
>
>   - 堆内存是一种动态分配和释放的内存，用于存储程序运行时需要动态分配的数据。
>   - 使用`malloc()`、`calloc()`、`realloc()` 等函数在堆上分配内存，并使用 `free()` 函数释放堆内存。
>
>   ```c
>   int *ptr = (int *)malloc(sizeof(int)); // 在堆上分配内存
>   // 使用完毕后，需要手动释放内存
>   free(ptr);
>   ```
>
>3. **全局变量和静态变量分配（Static and Global Variables）**：
>
>   - 全局变量和静态变量存储在静态存储区，它们在程序的整个生命周期内存在。
>   - 全局变量在所有函数之外声明，而静态变量在函数内部使用 `static` 关键字声明。
>
>   ```c
>   int globalVar; // 全局变量，在静态存储区分配内存
>   void someFunction() {
>       static int staticVar; // 静态变量，在静态存储区分配内存
>   }
>   ```

### 堆和栈的区别

>1. **生存周期**:
>   - **栈**：栈上的变量的生命周期通常局限于函数的执行期间。当函数返回时，栈上的局部变量会被销毁，内存被释放。
>   - **堆**：堆上分配的内存的生命周期可以长于任何特定函数调用，通常由程序员来管理。内存只有在显式释放时才会被回收。
>2. **大小限制**:
>   - **栈**：栈的大小通常受限于编译器或操作系统的设置，较小。因此，栈适合存储相对较小的数据结构。
>   - **堆**：堆的大小通常受系统内存的限制，可以分配较大的内存块，适合存储大型数据结构。
>3. **访问速度**:
>   - **栈**：栈上的内存访问速度较快，因为它是线性分配，且栈上的数据通常存储紧凑。
>   - **堆**：堆上的内存访问速度较慢，因为它是动态分配的，数据可能分散存储在内存中。
>4. **分配方式**:
>   - **栈**：栈上的内存分配和释放是自动的，不需要程序员干预。
>   - **堆**：堆上的内存需要程序员手动分配和释放，使用 `malloc()`、`free()` 等函数。

### 栈在c语言中的作用

>1. 用来保存临时变量，临时变量包括函数参数，函数内部定义的临时变量
>2. 多线程编程的基础就是栈，每个线程多最少有自己的专属的栈，用来保存本线程运行时各个函数的临时变量

### c++的内存管理

>在c++中虚拟内存分为代码段、数据段、bss段、堆、共享区、栈
>
>1. 代码段:包括只读存储去和文本区，其中只读存储区字符串常量，文本区存储程序的机械代码
>2. 数据段：全局变量、静态变量（全局、局部）
>3. BSS段：未初始化的全局变量和静态变量（全局、局部），以及所有被初始化为0的全局变量和静态变量
>4. 堆:调用new/malloc申请的内存空间，地址由低地址向高地址扩张
>5. 栈：局部变量、函数的返回值，函数的参数，地址由高地址向低地址扩张

### 内存泄漏

> 简单来说就是申请了内存，不使用之后并没有释放内存，或者说，指向申请的内存的指针突然又去指向别的地方，导致找不到申请的内存，
>
> **影响**
>
> 随着程序运行时间越长，占用内存越多，最终用完内存，导致系统崩溃
>
> **减少内存泄漏**
>
> 1. 良好的编码习惯，使用内存分配的函数，一但使用完毕之后就要记得使用对应的函数是否掉
> 2. 将分配的内存的指针以链表的形式自行管理，使用之后从链表中删除，程序结束时可以检查改链表
> 3. 使用智能指针

### 字节对齐问题

>1. **对齐要求**：计算机体系结构规定了数据类型的对齐要求，通常以字节为单位。例如，一个32位体系结构可能需要数据类型的存储地址是其大小的整数倍，比如4字节对齐或8字节对齐。
>2. **未对齐访问**：如果数据没有按照对齐要求存储在内存中，访问该数据可能会导致性能损失或硬件要求，并可能导致错误。在这种情况下，需要将数据移动到字节对齐的地址进行访问。
>
>**常见就是求复合类型大小，比如结构体、联合体**  

### C语言函数参数压栈顺序

>C语言中，函数参数的压栈顺序通常是从右到左，也就是从最后一个参数开始压栈，依次向前。这是因为C语言的调用约定是"cdecl"（C Declaration），按照这个约定，函数的调用者（调用函数的地方）会将参数从右到左依次推入栈中，然后调用函数。
>
>举个例子，假设有一个如下所示的函数：
>
>```c
>int addNumbers(int a, int b, int c) {
>    return a + b + c;
>}
>```
>
>如果在另一个函数中调用`addNumbers`函数，假设要计算`addNumbers(1, 2, 3)`，参数的压栈顺序是这样的：
>
>1. 首先，数字3（参数c）被推入栈中。
>2. 然后，数字2（参数b）被推入栈中。
>3. 最后，数字1（参数a）被推入栈中。

### 可能内存溢出的函数

>1. **`strcat`**:
>
>   - `strcat` 用于将一个字符串附加到另一个字符串的末尾。
>   - 可能导致内存溢出，因为它不会检查目标字符串的容量，如果目标字符串不足以容纳被附加的内容，就会溢出。
>
>   改进方法：使用 `strncat` 函数，该函数接受一个额外参数，指定要附加的最大字符数，从而避免溢出。
>
>2. **`strncat`**:
>
>   - `strncat` 具有改进版的 `strcat`，可以控制附加的字符数。
>   - 仍然需要小心，确保指定的字符数不会超过目标字符串的容量。
>
>3. **`strcmp`**:
>
>   - `strcmp` 用于比较两个字符串是否相等。
>   - 不会导致内存溢出，但可能导致无限循环或错误，如果比较的字符串没有正确的终止符。
>
>   改进方法：使用 `strncmp` 函数，并始终确保比较的字符串以 null 结尾。
>
>4. **`strcpy`**:
>
>   - `strcpy` 用于将一个字符串复制到另一个字符串。
>   - 可能导致内存溢出，因为它不会检查目标字符串的容量，如果目标字符串不足以容纳被复制的内容，就会溢出。
>
> 改进方法：使用 `strncpy` 函数，该函数接受一个额外参数，指定要复制的最大字符数，从而避免溢出。

### 内存申请函数

>```c
>// 申请堆内存
>void *malloc(size_t size); //申请size_t个字节内存
>void free(void *ptr); //释放内存，但是指针还是可以用
>void *calloc(size_t nmemb, size_t size); //申请nmemb快内存，每块size_t个字节
>void *realloc(void *ptr, size_t size);//申请内存，重新申请size_t字节内存，
>void *reallocarray(void *ptr, size_t nmemb, size_t size); 
>```