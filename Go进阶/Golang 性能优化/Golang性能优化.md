提供几个性能调优技巧（可以说是在实习时，leader提醒你的）：  
1、在大切片的基础上新建小切片，记得释放内存，不然大切片的底层数组一直存在  
2、新建切片，map时，记得预分配内存，避免扩容（本质是较少内存拷贝）。不然相同的代码可能有5倍以上的性能差距  
3、在进行字符串拼接时，不要使用+,因为字符串在go中是不可变类型，每次使用+都要重新分配内存。如果使用库strings.Builder，底层是byte[]，不需要每次拼接都分配内存，性能有80倍以上的差距。
4、使用空结构体节省内存