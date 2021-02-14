# studygo [链接](https://www.liwenzhou.com/posts/Go/go_menu/)
## go语言学习笔记
### 1、make和new的区别
#####  (1) make和new都是用来申请内存的。
#####  (2) new很少使用，一般用来给基本的数据结构申请内存，例如:`int`,`string`,`bool`等，返回的是对应类型的指针(\*int、\*string、\*bool)。
#####  (3) make是用来给`slice`、`map`、`chan`申请内存的，make函数返回的是对应的这三个类型本身。

### 2、defer总结
#### (1) defer执行时机
##### 在Go语言的函数中return语句在底层并不是原子操作，它分为给返回值赋值和RET指令两步。而defer语句执行的时机就在返回值赋值操作后，RET指令执行前。具体如下图所示：
![](https://github.com/lsds888/image/blob/main/image_golang/%E6%88%AA%E5%B1%8F2021-02-14%20%E4%B8%8B%E5%8D%887.24.36.png)
#### (2) defer经典案例
```go,golang
func f1() int {
	x := 5
	defer func() {
		x++
	}()
	return x
}

func f2() (x int) {
	defer func() {
		x++
	}()
	return 5
}

func f3() (y int) {
	x := 5
	defer func() {
		x++
	}()
	return x
}
func f4() (x int) {
	defer func(x int) {
		x++
	}(x)
	return 5
}
func main() {
	fmt.Println(f1())
	fmt.Println(f2())
	fmt.Println(f3())
	fmt.Println(f4())
}
```
