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
// Code=123&endDate=2020-12-31
、、、

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
    fmt.Printf(url,stockcode,enddate)
}


// Code=123&endDate=2020-12-31
、、、


# Day3 Go 语言数据类型

数据类型用于声明函数和变量。数据类型的出现是为了把数据分成所需内存大小不同的数据，编程的时候需要用大数据的时候才需要申请大内存，就可以充分利用内存。

## 布尔型
布尔型的值只可以是常量 true 或者 false。一个简单的例子：var b bool = true。

//示例代码
var isActive bool  // 全局变量声明
var enabled, disabled = true, false  // 忽略类型的声明
func test() {
    var available bool  // 一般声明
    valid := false      // 简短声明
    available = true    // 赋值操作
}

## 数字类型
整型 int 和浮点型 float32、float64，Go 语言支持整型和浮点型数字，并且支持复数，其中位的运算采用补码。
int、uint 和 uintptr。
### 整型 int 
uint8
无符号 8 位整型 (0 到 255)

uint16
无符号 16 位整型 (0 到 65535)

uint32
无符号 32 位整型 (0 到 4294967295)

uint64
无符号 64 位整型 (0 到 18446744073709551615)

int8
有符号 8 位整型 (-128 到 127)

int16
有符号 16 位整型 (-32768 到 32767)

int32
有符号 32 位整型 (-2147483648 到 2147483647)

int64
有符号 64 位整型 (-9223372036854775808 到 9223372036854775807)

 ### 浮点型 float32、float64
 float32
IEEE-754 32位浮点型数
float64
IEEE-754 64位浮点型数
complex64
32 位实数和虚数
complex128
64 位实数和虚数

### 其他数字类型

1	byte
类似 uint8
2	rune
类似 int32
3	uint
32 或 64 位
4	int
与 uint 一样大小
** 5	uintptr **
** 无符号整型，用于存放一个指针 **

## 字符串类型:
字符串就是一串固定长度的字符连接起来的字符序列。Go 的字符串是由单个字节连接起来的。Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本。

## 派生类型
包括：
(a) 指针类型（Pointer）
(b) 数组类型
(c) 结构化类型(struct)
(d) Channel 类型
(e) 函数类型
(f) 切片类型
(g) 接口类型（interface）
(h) Map 类型

go 1.9版本对于数字类型，无需定义int及float32、float64，系统会自动识别

package main
import "fmt"

func main() {
   var a = 1.5
   var b =2
   fmt.Println(a,b)
}
运行结果

# go run int.go
1.5 2

# Day3 Go 语言变量
储存计算结果或能表示值抽象概念。

Go 语言变量名由字母、数字、下划线组成，其中首个字符不能为数字。

声明变量的一般形式是使用 var 关键字：

var identifier type
var identifier1, identifier2 type

package main
import "fmt"
func main() {
    var a string = "Runoob"
    fmt.Println(a)

    var b, c int = 1, 2
    fmt.Println(b, c)
}

Runoob
1 2

# Day4 Go 语言变量 2
## 变量声明

第一种，指定变量类型，如果没有初始化，则变量默认为零值。系统默认设置的值。

数值类型（包括complex64/128）为 0
布尔类型为 false
字符串为 ""（空字符串）
以下几种类型为 nil：
var a *int
var a []int
var a map[string] int
var a chan int
var a func(string) int
var a error // error 是接口



package main
import "fmt"
func main() {

    // 声明一个变量并初始化
    var a = "RUNOOB"
    fmt.Println(a)

    // 没有初始化就为零值
    var b int
    fmt.Println(b)

    // bool 零值为 false
    var c bool
    fmt.Println(c)
}

RUNOOB
0
false



package main

import "fmt"

func main() {
    var i int
    var f float64
    var b bool
    var s string
    fmt.Printf("%v %v %v %q\n", i, f, b, s)
}

0 0 false ""

第二种，根据值**自行判定**变量类型。
package main
import "fmt"
func main() {
    var d = true
    fmt.Println(d)
}

true

第三种，如果变量已经使用 var 声明过了，再使用 := 声明变量，就产生编译错误，格式：v_name := value

var intVal int 
intVal :=1 // 编译错误，因为 intVal 已经声明，不需要重新声明

直接使用下面的语句即可：intVal := 1 // 不会产生编译错误，因为有声明新的变量，因为 := 是一个声明语句

intVal := 1 相等于：

var intVal int 
intVal =1 

可以将 var f string = "Runoob" 简写为 f := "Runoob"
package main
import "fmt"
func main() {
    f := "Runoob" // var f string = "Runoob"

    fmt.Println(f)
}

Runoob

## **多变量声明**

//类型相同多个变量, 非全局变量
var vname1, vname2, vname3 type
vname1, vname2, vname3 = v1, v2, v3

var vname1, vname2, vname3 = v1, v2, v3 // 和 python 很像,不需要显示声明类型，自动推断

vname1, vname2, vname3 := v1, v2, v3 // 出现在 := 左侧的变量-- 不应该是已经被声明过的 --


// **这种因式分解关键字的写法一般用于声明全局变量**
var (
    vname1 v_type1
    vname2 v_type2
)

package main
import "fmt"

var x, y int
var (  // 这种因式分解关键字的写法一般用于声明全局变量
    a int
    b bool
)

var c, d int = 1, 2
var e, f = 123, "hello"



// **这种不带声明格式的只能在函数体中出现**
//g, h := 123, "hello"

func main(){
    g, h := 123, "hello"
    fmt.Println(x, y, a, b, c, d, e, f, g, h)
}

0 0 0 false 1 2 123 hello 123 hello

## 值类型和引用类型
# 希望找到讲解GO 指针的视频
 int、float、bool 和 string 这些基本类型都属于值类型,变量直接指向存在内存中的值
 当使用等号 = 将一个变量的值赋值给另一个变量时，如：j = i，实际上是在内存中将 i 的值进行了**拷贝**

&i 来获取变量 i 的内存地址，例如：0xf840000040（每次的地址都可能不一样）。
值类型变量的值存储在堆中。

一个引用类型的变量 r1 存储的是 r1 的值所在的内存地址（数字），或内存地址中第一个字所在的位置。
内存地址称之为指针reference,这个指针实际上也被存在另外的某一个值.

同一个引用类型的指针指向的多个字可以是在连续的内存地址中（内存布局是连续的），这也是计算效率最高的一种存储形式；
也可以将这些字分散存放在内存中，每个字都指示了下一个字所在的内存地址。

当使用赋值语句 r2 = r1 时，只有引用（地址）被复制。

如果 r1 的值被改变了，那么这个值的所有引用都会指向被修改后的内容，在这个例子中，r2 也会受到影响。

