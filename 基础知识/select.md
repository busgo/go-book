### select 

***

1. 概述

   ​	*select*是操作系统的调用函数，一般我们使用*select*、*poll*、*epoll* 函数来构建多路复用IO模型来提高应用的性能，在操作系统上*select* 可以监听多个文件描述符(fd_set)就绪状态，*go*语言里面的*select* 相类似，*select* 可以监听多个通道(*channel*) 可读、可写状态，一般我们在处理多个*channel* 的时候一般配合*select*使用 。

2. select 语法

   ```go
   select {
       case <-ch1:
       case <-ch2:
       default:
       fmt.Println("default")
   }
   ```

    select 语法与switch语法比较类型，但是 *select*对应的*case*语句必须是通道类型，遗憾的是*select*关键字 并不像*map*一样有对应的底层结构体，但是编译器处理select的时候每个*case* 会有对应一个结构体用于 

   OCASE 

   ```go
   type ocase struct {
       hchan 
       elem uint
   }
   ```

    	

3. select 特点

   1. 能够同时监听多个通道可读、可写状态，如果*select*语句包含有*default*语句则会执行*default*代码块。

   2. *select*执行case代码块是随机性的,这样做的目的防止后面的*case*语句饥饿。

   3. 如果*select*语句如果不包含任何一个语句的时候，*go*调度器会直接把当前协程进行阻塞挂起，并且永远也不可能被唤醒操作。

   4. 如果*select* 语句中如果只包含一个*case*语句并且对应的*channel*为nil 则*go*调度器也会直接把当前协程进行阻塞挂起，并且永远不可能进行唤醒操作。

   5. 如果当前没有就绪的*case*代码块(可读、可写状态)，如果有*default*代码块，则会直接执行*default*代码块 否则直接阻塞当前协程等待调度器进行调度唤醒。

      