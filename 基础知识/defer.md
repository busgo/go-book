### defer

***

​	    大多数开发语言中都有*defer*关键字，go语言中使用 *defer* 对函数返回之前执行传入的函数。一般我们使用*defer* 进行关闭文件、流、连接、回滚事务等。

1. 原则

   1. defer调用顺序问题 先进后出的原则，

   2. defer 作用在函数退出作用域而不是代码块作用域

   3. defer预赋值问题。

      ```go
      
      now:=time.Now()
      
      defer fmt.Println(time.Since(now))
      
      time.Sleep(time.Second)
      
      // 输出 0s
      
      ```

       这种问题感觉不是我们要的结果我们想要的是1s 而输出的是 0s， 因为 在*go*语言中函数的参数都是值传递的， *defer* 关键字会立即拷贝函数对应的参数， 那么 **time.Since(now)** 则会立即执行了，我们可以使用匿名函数来解决当前问题。

      ```go
      now := time.Now()
      
      defer func() {
          
          fmt.Println(time.Since(now))
      }()
      time.Sleep(time.Second)
      // 输出 1s
      ```

      

  