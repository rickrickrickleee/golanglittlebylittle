# Day1 My first code

## code for today
go run test.go

、、、go

package main // 包声明

import "fmt" // 引入包

/*
 Author by riri
 20231103
 */
func main() { // 函数
   fmt.Println("Hello, World!")
   fmt.Print("hello, world\n") 
}

、、、

、、、go
Hello, World!
、、、

## 组成
包声明 一个可独立执行的程序
引入包 需要使用 fmt 包，fmt 包实现了格式化 IO（输入/输出）的函数
函数 main 必须包含的，启动后第一个执行的函数，init() 函数则会先执行该函数
变量 
标识符（包括常量、变量、类型、函数名、结构字段等等）以一个大写字母开头，如：Group1，
那么使用这种形式的标识符的对象就可以被外部包的代码所使用（客户端程序需要先导入这个包），这被称为导出（像面向对象语言中的 public）；
标识符如果以小写字母开头，则对包外是不可见的，但是他们在整个包的内部是可见并且可用的（像面向对象语言中的 protected ）
语句 & 表达式
注释

{  // 错误，{ 不能在单独的行上

### 程序/函数
Go 程序可以由多个标记组成，可以是关键字，标识符，常量，字符串，符号。如以下 GO 语句由 6 个标记组成：
fmt.Println("Hello, World!")

1. fmt
2. .
3. Println
4. (
5. "Hello, World!"
6. )

多个语句写在同一行必须使用 ; 人为区分，但在实际开发中我们并不鼓励这种做法。
fmt.Println("Hello, World!")
fmt.Println("菜鸟教程：runoob.com")

### 标识符

命名变量、类型等程序实体，第一个字符必须是字母或下划线而不能是数字。
无效的标识符：

- 1ab（以数字开头）
- case（Go 语言的关键字）
- a+b（运算符是不允许的）

### 字符串连接

"Google" + "Runoob"


# Day2 基础语法和数据类型

## 关键字25
### 还需要搞懂的
#### defer 

defer函数会在return之后被调用,关闭/清理代码中所使用的变量
> https://www.cnblogs.com/vikings-blog/p/7099023.html#:~:text=%E8%80%8C%E4%BD%BF%E7%94%A8defer%E5%88%99%E5%8F%AF%E4%BB%A5%E9%81%BF%E5%85%8D%E8%BF%99%E7%A7%8D%E6%83%85%E5%86%B5%E7%9A%84%E5%8F%91%E7%94%9F%EF%BC%8C%E4%B8%8B%E9%9D%A2%E6%98%AF%E4%BD%BF%E7%94%A8defer%E7%9A%84%E4%BB%A3%E7%A0%81%3A%20func%20CopyFile%28dstName%2C%20srcName%20string%29%20%28written%20int64%2C%20err,defer%20dst.Close%20%28%29%20return%20io.Copy%20%28dst%2C%20src%29%20%7D

、、、go

// 规则一：当defer被声明时，其参数就会被实时解析
func a() {
i := 0
defer fmt.Println(i)
i++
return
}
 // 等同
 
func a() {
i := 0
defer fmt.Println(0) //因为i=0，所以此时就明确告诉golang在程序退出时，执行输出0的操作
i++
return
}

// defer输出的值，就是定义时的值而不是defer真正执行时的变量值(很重要，搞不清楚的话就会产生于预期不一致的结果)

func a() {
i := 0
defer fmt.Println(i) //输出0，因为i此时就是0
i++
defer fmt.Println(i) //输出1，因为i此时就是1
return
}
、、、


、、、go

// 规则二：defer执行顺序为先进后出
func b() {
for i := 0; i < 4; i++ {
defer fmt.Print(i)
}
}

// 安装先进后出的原则，我们可以看到依次输出了3210
、、、

、、、go

// 规则三 defer可以读取有名返回值

func c() (i int) {
defer func() { i++ }()
return 1
}
// 输出结果是12
// 当执行return 1 之后，i的值就是1. 此时此刻，defer代码块开始执行，对i进行自增操作。 因此输出2.
、、、


#### chan
#### goto
#### fallthrough

break	default	func	interface	select

case	defer	go	map	struct

chan	else	goto	package	switch
const	fallthrough	if	range	type
continue	for	import	return	var

## 预定义标识符36

append	bool	byte	cap	close	complex	complex64	complex128	uint16
copy	false	float32	float64	imag	int	int8	int16	uint32
int32	int64	iota	len	make	new	nil	panic	uint64
print	println	real	recover	string	true	uint	uint8	uintptr

程序一般由关键字、常量、变量、运算符、类型和函数组成。
程序中可能会使用到这些分隔符：括号 ()，中括号 [] 和大括号 {}。
程序中可能会使用到这些标点符号：.、,、;、: 和 …。


## Go 语言的空格
空格通常用于分隔标识符、关键字、运算符和表达式，以提高代码的可读性。
Go 语言中变量的声明必须使用空格隔开

、、、go
var x int
const Pi float64 = 3.14159265358979323846

// 关键字和表达式之间要使用空格。

if x > 0 {
    // do something
}

// 在函数调用时，函数名和左边等号之间要使用空格，参数之间也要使用空格。

result := add(2, 3)
、、、

## 格式化字符串

Sprintf 根据格式化参数生成格式化的字符串并返回该字符串。
Printf 根据格式化参数生成格式化的字符串并写入标准输出。

、、、go
package main

import (
    "fmt"
)

func main() {
   // %d 表示整型数字，%s 表示字符串
    var stockcode=123
    var enddate="2020-12-31"
    var url="Code=%d&endDate=%s"
    var target_url=fmt.Sprintf(url,stockcode,enddate)
    fmt.Println(target_url)
}
、、、
