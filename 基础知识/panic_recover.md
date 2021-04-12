### panic 和 recover

***

1. panic

   panic 是*go*中的内置函数，当碰到 panic函数时候会立即停止执行当前函数剩余的内容，并在当前的Goroutine 递归调用 defer函数。

2. recover

   recover 用于阻止 panic崩溃， 并且只能再defer语句中起作用。

3. 原则

   1. 如果阻塞程序崩溃，一般使用 *panic* 和*recover* 配套使用。

   2. *panic* 只会作用于当前*Goroutine* 不会往其他*Goroutine*进行传递。

   3. *recover* 只能在defer 关键字中生效。

      

