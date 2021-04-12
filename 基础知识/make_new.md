### make 和 new

***

一、概述

1. make 用于初始化内置结构体的并且只有三种 *slice*、*map*、*chan* 。
2. *new*用于传入指定类型进行创建指定内存大小的内存并返回对应的指针。

二、 底层

1.  make 使用底层的 *OMAKESLICE*、*OMAKEMAP*、*OMAKECHAN* 

2.  new 则使用  *ONEWOBJ

   * 如果申请内存大小为0 则返回一个表示为空的指针  *zerobase*
   * 其他情况则直接转入 newobject 进行处理。

   

