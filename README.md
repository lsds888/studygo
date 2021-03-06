# studygo [链接](https://www.liwenzhou.com/posts/Go/go_menu/)
## go语言学习笔记
### 1、[make和new的区别](https://www.liwenzhou.com/posts/Go/07_pointer/)
#####  (1) make和new都是用来申请内存的。
#####  (2) new很少使用，一般用来给基本的数据结构申请内存，例如:`int`,`string`,`bool`等，返回的是对应类型的指针(\*int、\*string、\*bool)。
#####  (3) make是用来给`slice`、`map`、`chan`申请内存的，make函数返回的是对应的这三个类型本身,而不是指针，因为这三种类型就是引用类型，所以就没有必要返回他们的指针了。

### 2、[defer总结](https://www.liwenzhou.com/posts/Go/09_function/)
#### (1) defer执行时机
##### 在Go语言的函数中return语句在底层并不是原子操作，它分为给返回值赋值和RET指令两步。而defer语句执行的时机就在返回值赋值操作后，RET指令执行前。具体如下图所示：
![](https://github.com/lsds888/image/blob/main/image_golang/%E6%88%AA%E5%B1%8F2021-02-14%20%E4%B8%8B%E5%8D%887.24.36.png)
#### (2) defer经典案例
```go,golang
func f1() int {
	x := 5
	defer func() {
		x++ // 修改的是x不是返回值
	}()
	return x
}

func f2() (x int) {
	defer func() {
		x++
	}()
	return 5 // 返回值 = x
}

func f3() (y int) {
	x := 5
	defer func() {
		x++ // 修改的是 5
	}()
	return x  // 返回值 = y = x = 5
}
func f4() (x int) {
	defer func(x int) {
		x++  // 改变的是函数中的副本
	}(x)
	return 5  // 返回值 = x = 5
}
func main() {
	fmt.Println(f1())
	fmt.Println(f2())
	fmt.Println(f3())
	fmt.Println(f4())
}
```
##### 运行结果为：5 6 5 5
### 3、go语言中的函数传参都是拷贝传参
