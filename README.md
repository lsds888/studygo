# studygo
## go语言学习笔记
### 1、make和new的区别
#####  (1) make和new都是用来申请内存的。
#####  (2) new很少使用，一般用来给基本的数据结构申请内存，例如:`int`,`string`,`bool`等，返回的是对应类型的指针(\*int、\*string、\*bool)。
#####  (3) make是用来给`slice`、`map`、`chan`申请内存的，make函数返回的是对应的这三个类型本身。
