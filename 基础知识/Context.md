### Context
***
  在我们使用开发应有服务的时候，比如一个web服务每个请求一般会开启一个*goroutine*处理一个请求，查询数据库、操作redis也会开启新的*goroutine*来进行处理同一个web请求。这样一个web请求会构成一个*goroutine*树，我们可以通过Context来同步传递信号，上层同步一个信号层的goroutine能够很好的收到上层传递的信息，进而处理相关业务处理。
  在一个goroutine构成的树形结构能够方便同步下游信号减少对资源的消耗利用，这就是*Context*最大的用途。
  
  
