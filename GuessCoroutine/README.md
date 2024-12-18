#  C++20协程（Coroutine）介绍


## 简单介绍协程
协程可以简单的理解为，它是一个可以随时“中断”，并再次恢复执行的函数。


## 协程和函数的区别
协程是一个可以随时“中断”，并再次恢复执行的函数。

### 普通函数的执行过程

一个普通函数在执行的时候，主要包含两个操作，分别是**调用（call）**和**返回（return）**。

当一个普通函数执行call的时候，将会创建一个新的栈帧（Frame），然后停止调用者的执行并转移到新的方法上进行执行。

当发生return的时候，该方法将会返回一个值给调用者，并且销毁当前使用的栈帧（Activation Frame），调用者将会按照原先的逻辑继续执行。


### ChatGPT的简要说明

C++协程和函数调用在本质上有几个关键区别：
控制流程：函数调用是线性的，即按照顺序依次执行函数中的语句，直到函数返回。而协程可以在执行过程中暂停和恢复，允许在不同的执行点之间切换控制流。这种非线性的控制流使得协程可以更好地处理异步操作和状态管理。
保存状态：函数调用会将函数的参数、局部变量和返回地址保存在调用栈中，当函数返回后，这些状态会被清除。而协程在暂停时会保存其当前的状态，包括局部变量和执行位置。当协程恢复时，这些状态会被还原，继续执行。
暂停和恢复：函数调用的执行是一次性的，无法中途暂停和恢复。而协程可以在执行过程中通过特定的语法（如co_yield和co_await）暂停执行，并在之后的某个时刻恢复执行。这种能力使得协程可以实现异步操作和事件驱动的编程模型。
总的来说，函数调用是一种线性、一次性的执行模式，而协程提供了非线性、可暂停和恢复的执行模式。协程的设计目的是为了更方便地处理异步和事件驱动的编程任务，提高代码的可读性和可维护性。


## 协程的技术实现
C++协程是通过生成器（generator）和异步状态机（async state machine）的方式来实现的。以下是C++协程的背后实现原理的简要说明：
生成器（Generator）：
C++协程使用生成器来定义协程函数。生成器是一种特殊的函数，可以在执行过程中暂停和恢复执行，并返回一个值序列。
在生成器中，使用co_yield语句可以暂停协程的执行并返回一个值，而co_return语句用于结束协程的执行并返回最终的值。
异步状态机（Async State Machine）：
C++协程背后的实现依赖于异步状态机。异步状态机是一个有限状态机，用于管理协程的状态和控制流。
当协程被暂停时，异步状态机会保存协程的当前状态和局部变量，并将控制流转移到其他任务上。
当协程被恢复时，异步状态机会还原协程的状态和局部变量，并继续协程的执行。
编译器支持：
实现C++协程需要编译器的支持。C++20引入了协程的语法和关键字，并为编译器提供了协程相关的库和特性。
编译器在编译协程代码时会对生成器和异步状态机进行转换和优化，以生成对应的状态转换和控制逻辑。
通过生成器和异步状态机的组合，C++协程提供了一种更简洁和可读性更好的编程模型，可以方便地处理异步操作和状态管理。协程可以帮助开发者编写更简洁、可维护和高效的异步代码。需要注意的是，协程的实现可能因编译器和标准库的不同而有所差异，具体细节可以参考相应的编译器文档和C++标准。






## Ref
https://lewissbaker.github.io/2017/09/25/coroutine-theory
https://lewissbaker.github.io/2017/11/17/understanding-operator-co-await


