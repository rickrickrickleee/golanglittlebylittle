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

# Day5 使用 := 赋值操作符

变量的初始化时省略变量的类型而由系统自动推断，
声明语句写上 var 关键字其实是显得有些多余了，
因此我们可以将它们简写为 a := 50 或 b := false。

a 和 b 的类型（int 和 bool）将由编译器自动推断。

这是使用变量的首选形式，
但是它只能被用在函数体内，
不可以用于全局变量的声明与赋值
使用操作符 := 可以高效地创建一个新的变量，称之为初始化声明。

注意事项

不可以再次对于相同名称的变量使用初始化声明，
例如：a := 20 就是不被允许的
，编译器会提示错误 no new variables on left side of :=，
但是 a = 20 是可以的，因为这是给相同的变量赋予一个新的值。

你声明了一个局部变量却没有在相同的代码块中使用它，
同样会得到编译错误，例如下面这个例子当中的变量 a：

package main

import "fmt"

func main() {
   var a string = "abc"
   fmt.Println("hello, world")
}

尝试编译这段代码将得到错误 a declared but not used。
单纯地给 a 赋值也是不够的，
**这个值必须被使用，所以使用**

fmt.Println("hello, world", a)

会移除错误。

**但是全局变量是允许声明但不使用的。 **

同一类型的**多个变量**可以声明在同一行，如：
var a, b, c int

 并行 或 同时 赋值
多变量可以在同一行进行赋值，如：
var a, b int
var c string
** a, b, c = 5, 7, "abc" **

想要交换两个变量的值，则可以简单地使用 a, b = b, a，两个变量的类型必须是相同。
空白标识符 _ 也被用于抛弃值，如值 5 在：_, b = 5, 7 中被抛弃。

_ 实际上是一个只写变量，你不能得到它的值。这样做是因为 Go 语言中**你必须使用所有被声明的变量，**

但有时你并不需要使用从一个函数得到的所有返回值。

并行赋值也被用于当一个函数返回多个返回值时，

比如这里的 val 和错误 err 是通过调用** Func1 **函数同时得到：val, err = Func1(var1)。



空白标识符在函数返回值时的使用：

package main

import "fmt"

func main() {
  _,numb,strs := numbers() //只获取函数返回值的后两个
  fmt.Println(numb,strs)
}

//一个可以返回多个值的函数
func numbers()(int,int,string){
  a , b , c := 1 , 2 , "str"
  return a,b,c
}

输出结果：

2 str

局部变量：在函数体内声明的变量称之为局部变量，它们的作用域只在函数体内，参数和返回值变量也是局部变量。

全局变量：在函数体外声明的变量称之为全局变量，全局变量可以在整个包甚至外部包（被导出后）使用。

备注：

1.局部变量不会一直存在，在函数被调用时存在，函数调用结束后变量就会被销毁，即生命周期。

2.Go 语言程序中全局变量与局部变量名称可以相同，但是函数内的局部变量会被优先考虑。

# Day5 Go 语言常量

只可以是布尔型、数字型（整数型、浮点型和复数）和字符串型
常量的定义格式：const identifier [type] = value

省略类型说明符 [type]，
显式类型定义： const b string = "abc"
隐式类型定义： const b = "abc"

多个相同类型的声明可以简写为：

const c_name1, c_name2 = value1, value2

package main

import "fmt"

func main() {
   const LENGTH int = 10
   const WIDTH int = 5  
   var area int
   const a, b, c = 1, false, "str" //多重赋值

   area = LENGTH * WIDTH
   fmt.Printf("面积为 : %d", area)
   println()
   println(a, b, c)  
}

面积为 : 50
1 false str

枚举
const (
    Unknown = 0
    Female = 1
    Male = 2
)

数字 0、1 和 2 分别代表未知性别、女性和男性。

len(), cap(), unsafe.Sizeof()函数计算表达式的值。常量表达式中，函数必须是内置函数，否则编译不过
package main

import "unsafe"
const (
    a = "abc"
    b = len(a)
    c = unsafe.Sizeof(a)
)

func main(){
    println(a, b, c)
}

abc 3 16

## iota 特殊常量
特殊常量，可以认为是一个可以被编译器修改的常量。
const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次(iota 可理解为 const 语句块中的行索引)。

iota 可以被用作枚举值：

const (
    a = iota
    b = iota
    c = iota
)

第一个 iota 等于 0，每当 iota 在新的一行被使用时，
它的值都会自动加 1；

所以 a=0, b=1, c=2 可以简写为如下形式：
const (
    a = iota
    b
    c
)

iota 用法

package main

import "fmt"

func main() {
    const (
            a = iota   //0
            b          //1
            c          //2
            d = "ha"   //独立值，iota += 1,3
            e          //"ha"   iota += 1,4
            f = 100    //iota +=1,5
            g          //100  iota +=1,6
            h = iota   //7,恢复计数
            i          //8
    )
    fmt.Println(a,b,c,d,e,f,g,h,i)
}

0 1 2 ha ha 100 100 7 8

 **为什么这里的e是ha：** d = "ha" 将 d 的值设置为字符串 "ha"，并且此时 iota 的值为 3。接下来，e 的声明没有显式地赋值，因此它会继承上一个常量的值，即 "ha"。

# Day6 Go iota 自增和二进制

package main

import "fmt"
const (
    i=1<<iota
    j=3<<iota
    k
    l
)

func main() {
    fmt.Println("i=",i)
    fmt.Println("j=",j)
    fmt.Println("k=",k)
    fmt.Println("l=",l)
}
以上实例运行结果为：

i= 1
j= 6
k= 12
l= 24

iota 表示从 0 开始自动加 1，所以 i=1<<0, j=3<<1（<< 表示左移的意思），

即：i=1, j=6，这没问题，关键在 k 和 l，从输出结果看 k=3<<2，l=3<<3。

简单表述:

i=1：左移 0 位，不变仍为 1。
j=3：左移 1 位，变为二进制 110，即 6。
k=3：左移 2 位，变为二进制 1100，即 12。
l=3：左移 3 位，变为二进制 11000，即 24。
注：<<n==*(2^n)。

解释
四个常量声明：i、j、k、l。它们都使用了 iota。

首先，iota 的初始值为 0。因此，i 的值为 1 左移 0 位，结果为 1。

接下来，iota 自增为 1。j 的值为 3 左移 1 位，结果为 6。这里是因为 iota 的二进制表示为 01，左移 1 位后变为 10，即十进制表示的 2，再乘以 3 得到 6。

然后，iota 自增为 2。k 的值为 3 左移 2 位，结果为 12。iota 的二进制表示为 10，左移 2 位后变为 1000，即十进制表示的 8，再乘以 3 得到 24。

最后，iota 自增为 3。l 的值为 3 左移 3 位，结果为 24。iota 的二进制表示为 11，左移 3 位后变为 11000，即十进制表示的 24。

因此，根据代码的输出结果，i 的值为 1，j 的值为 6，k 的值为 12，l 的值为 24。



# Day6 Go 语言运算符

- 算术运算符
- 关系运算符
- 逻辑运算符
- 位运算符
- 赋值运算符
- 其他运算符
 ## 算术运算符
%	求余

c = a % b
fmt.Printf("第五行 - c 的值为 %d\n", c )

不换行是 \n %d是占位符 右斜杠

## 关系运算符

>=
><=

## 逻辑运算符

&& || !

## 位运算符

位运算符对整数在内存中的**二进制位**进行操作。

&, |, 和 ^ 的计算：


p	q	  p & q	   p | q	   p ^ q
0	0	0	0	0
0	1	0	1	1
1	1	1	1	0
1	0	0	1	1  

假定 A = 60; B = 13; 其二进制数转换为：

A = 0011 1100

B = 0000 1101

-----------------

A&B = 0000 1100

A|B = 0011 1101

A^B = 0011 0001
# 解释二进制

位运算符是一组用于操作二进制位的运算符。它们直接对整数在内存中的二进制表示进行操作，而不考虑其十进制值。以下是几个常用的位运算符：

位与运算符（&）：对两个操作数的每个对应位执行按位与操作。只有当两个位都为 1 时，结果才为 1，否则结果为 0。

示例：8 & 3 的结果是 0，因为 8 的二进制表示是 1000，3 的二进制表示是 0011，按位与操作后的结果为 0000。

位或运算符（|）：对两个操作数的每个对应位执行按位或操作。只要两个位中至少有一个位为 1，结果就为 1。

示例：8 | 3 的结果是 11，因为 8 的二进制表示是 1000，3 的二进制表示是 0011，按位或操作后的结果为 1011。

异或运算符（^）：对两个操作数的每个对应位执行按位异或操作。如果两个位不同，结果为 1，如果两个位相同，结果为 0。

示例：8 ^ 3 的结果是 11，因为 8 的二进制表示是 1000，3 的二进制表示是 0011，按位异或操作后的结果为 1011。

## Go 语言支持的位运算符

如下表所示。假定 A 为60，B 为13：

运算符	描述	实例
&	按位与运算符"&"是双目运算符。 其功能是参与运算的两数各对应的二进位相与。	(A & B) 结果为 12, 二进制为 0000 1100
|	按位或运算符"|"是双目运算符。 其功能是参与运算的两数各对应的二进位相或	(A | B) 结果为 61, 二进制为 0011 1101
^	按位异或运算符"^"是双目运算符。 其功能是参与运算的两数各对应的二进位相异或，当两对应的二进位相异时，结果为1。	(A ^ B) 结果为 49, 二进制为 0011 0001
<<	左移运算符"<<"是双目运算符。左移n位就是乘以2的n次方。 其功能把"<<"左边的运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。	A << 2 结果为 240 ，二进制为 1111 0000
>>	右移运算符">>"是双目运算符。右移n位就是除以2的n次方。 其功能是把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数。	A >> 2 结果为 15 ，二进制为 0000 1111
>>

package main

import "fmt"

func main() {

   var a uint = 60      /* 60 = 0011 1100 */  
   var b uint = 13      /* 13 = 0000 1101 */
   var c uint = 0          

   c = a & b       /* 12 = 0000 1100 */
   fmt.Printf("第一行 - c 的值为 %d\n", c )

   c = a | b       /* 61 = 0011 1101 */
   fmt.Printf("第二行 - c 的值为 %d\n", c )

   c = a ^ b       /* 49 = 0011 0001 */
   fmt.Printf("第三行 - c 的值为 %d\n", c )

   c = a << 2     /* 240 = 1111 0000 */
   fmt.Printf("第四行 - c 的值为 %d\n", c )

   c = a >> 2     /* 15 = 0000 1111 */
   fmt.Printf("第五行 - c 的值为 %d\n", c )
}

# 学习二进制

计算机内部是使用二进制（binary）表示法来存储和处理数据的。

二进制是一种基于2的数制系统，只由两个数字组成：0和1。每位上的数字表示该位上的权重，最右边的位权重为2^0，依次向左增加。例如，二进制数 1010 表示：

1 * 2^3 + 0 * 2^2 + 1 * 2^1 + 0 * 2^0 = 8 + 0 + 2 + 0 = 10

所以，二进制数 1010 在十进制中等于 10。

在计算机中，内存中的所有数据都以二进制形式存储。计算机使用二进制来表示数字、字符、图像、音频等各种数据。二进制是计算机语言的基础，它可以通过位运算和逻辑运算来进行处理和操作。

## 赋值运算符
运算符	描述	实例
=	简单的赋值运算符，将一个表达式的值赋给一个左值	C = A + B 将 A + B 表达式结果赋值给 C
+=	相加后再赋值	C += A 等于 C = C + A
-=	相减后再赋值	C -= A 等于 C = C - A
*=	相乘后再赋值	C *= A 等于 C = C * A
/=	相除后再赋值	C /= A 等于 C = C / A
%=	求余后再赋值	C %= A 等于 C = C % A
<<=	左移后赋值	C <<= 2 等于 C = C << 2
>>=	右移后赋值	C >>= 2 等于 C = C >> 2
&=	按位与后赋值	C &= 2 等于 C = C & 2
^=	按位异或后赋值	C ^= 2 等于 C = C ^ 2
|=	按位或后赋值	C |= 2 等于 C = C | 2
>>

## &	返回变量存储地址	&a; 将给出变量的实际地址。
## *	指针变量。	*a; 是一个指针变量

package main

import "fmt"

func main() {
   var a int = 4
   var b int32
   var c float32
   var ptr *int

   /* 运算符实例 */
   fmt.Printf("第 1 行 - a 变量类型为 = %T\n", a );
   fmt.Printf("第 2 行 - b 变量类型为 = %T\n", b );
   fmt.Printf("第 3 行 - c 变量类型为 = %T\n", c );

   /*  & 和 * 运算符实例 */
   ptr = &a     /* 'ptr' 包含了 'a' 变量的地址 */
   fmt.Printf("a 的值为  %d\n", a);
   fmt.Printf("*ptr 为 %d\n", *ptr);
}
第 1 行 - a 变量类型为 = int
第 2 行 - b 变量类型为 = int32
第 3 行 - c 变量类型为 = float32
a 的值为  4
*ptr 为 4

var a int = 4：声明了一个变量 a，并赋值为 4。类型为 int。
var b int32：声明了一个变量 b，类型为 int32。没有显式赋值，因此默认为零值。
var c float32：声明了一个变量 c，类型为 float32。没有显式赋值，因此默认为零值。

var ptr *int：声明了一个指针变量 ptr，类型为 *int。没有显式赋值，因此默认为 nil。
ptr = &a：将变量 a 的地址赋值给指针变量 ptr。

fmt.Printf("第 1 行 - a 变量类型为 = %T\n", a)：使用格式化输出函数 Printf 打印出 a 变量的类型。
fmt.Printf("第 2 行 - b 变量类型为 = %T\n", b)：使用格式化输出函数 Printf 打印出 b 变量的类型。
fmt.Printf("第 3 行 - c 变量类型为 = %T\n", c)：使用格式化输出函数 Printf 打印出 c 变量的类型。

fmt.Printf("a 的值为  %d\n", a)：使用格式化输出函数 Printf 打印出变量 a 的值。
fmt.Printf("*ptr 为 %d\n", *ptr)：使用格式化输出函数 Printf 打印出指针变量 ptr 所指向的值。

## 运算符优先级

优先级	运算符
5	* / % << >> & &^
4	+ - | ^
3	== != < <= > >=
2	&&
1	||


# Day 6 条件语句 

语句	描述
if 语句	if 语句 由一个布尔表达式后紧跟一个或多个语句组成。 https://www.runoob.com/go/go-if-else-statement.html
if...else 语句	if 语句 后可以使用可选的 else 语句, else 语句中的表达式在布尔表达式为 false 时执行。
if 嵌套语句	你可以在 if 或 else if 语句中嵌入一个或多个 if 或 else if 语句。https://www.runoob.com/go/go-nested-if-statements.html
switch 语句	switch 语句用于基于不同条件执行不同动作。https://www.runoob.com/go/go-switch-statement.html 
select 语句	select 语句类似于 switch 语句，但是select会随机执行一个可运行的case。如果没有case可运行，它将阻塞，直到有case可运行。https://www.runoob.com/go/go-select-statement.html
Go 没有三目运算符，所以不支持 ?: 形式的条件判断。

# Day 7 条件语句 ALL IN

## if

package main

import "fmt"

func main () {

 var a int =100;

 if a <20 {
  fmt.Printf ("a is a baaby\n");
 }
 else {
  fmt.Printf("a is a adult\n ")
 }
 fmt.Printf("a is %d\n", a);
}

## if 语句嵌套
package main

import "fmt"

func main () {

var a int = 10;
if (a<1100){
  if (a<100){
  fmt.Printf("a is a number baby\n");
  }
}
fmt.Printf("%d\n",a);
}

### 笔记很好玩的 判断用户密码输入：

package main 

import"fmt"

func main(){
    var a int 
    var b int
    fmt.Printf("请输入密码：   \n")
    fmt.Scan(&a)
    if a == 5211314 {
    fmt.Printf("请再次输入密码：")
    fmt.Scan(&b)
        if b == 5211314 {
            fmt.Printf("密码正确，门锁已打开")
        }else{
            fmt.Printf("非法入侵，已自动报警")
        }
    }else{
        fmt.Printf("非法入侵，已自动报警")
    }
}

## switch 语句

每一个 case 分支都是唯一的，

switch 语句执行的过程从上至下，直到找到匹配项，匹配项后面也不需要再加 break。

switch 默认情况下 case 最后自带 break 语句，匹配成功后就不会执行其他 case，

如果我们需要执行后面的 case，可以使用 fallthrough 。

变量 var1 可以是任何类型，类型不被局限于常量或整数，但必须是相同的类型；或者最终结果为相同类型的表达式。
您可以同时测试多个可能符合条件的值，使用逗号分割它们，例如：case val1, val2, val3。
switch var1 {
    case val1:
        ...
    case val2:
        ...
    default:
        ...
}

package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var grade string = "B"
   var marks int = 90

   switch marks {
      case 90: grade = "A"
      case 80: grade = "B"
      case 50,60,70 : grade = "C"
      default: grade = "D"  
   }

   switch {
      case grade == "A" :
         fmt.Printf("优秀!\n" )    
      case grade == "B", grade == "C" :
         fmt.Printf("良好\n" )      
      case grade == "D" :
         fmt.Printf("及格\n" )      
      case grade == "F":
         fmt.Printf("不及格\n" )
      default:
         fmt.Printf("差\n" );
   }
   fmt.Printf("你的等级是 %s\n", grade );      
}
优秀!
你的等级是 A



### Type Switch
switch 语句还可以被用于 type-switch 来判断某个 interface 变量中实际存储的变量类型。

Type Switch 语法格式如下：

switch x.(type){
    case type:
       statement(s);      
    case type:
       statement(s); 
    /* 你可以定义任意个数的case */
    default: /* 可选 */
       statement(s);
}


package main

import "fmt"

func main() {
   var x interface{}
     
   switch i := x.(type) {
      case nil:  
         fmt.Printf(" x 的类型 :%T",i)                
      case int:  
         fmt.Printf("x 是 int 型")                      
      case float64:
         fmt.Printf("x 是 float64 型")          
      case func(int) float64:
         fmt.Printf("x 是 func(int) 型")                      
      case bool, string:
         fmt.Printf("x 是 bool 或 string 型" )      
      default:
         fmt.Printf("未知型")    
   }  
}
x 的类型 :<nil>

### fallthrough
 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。
 
 
package main

import "fmt"

func main() {

    switch {
    case false:
            fmt.Println("1、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("2、case 条件语句为 true")
            fallthrough
    case false:
            fmt.Println("3、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("4、case 条件语句为 true")
    case false:
            fmt.Println("5、case 条件语句为 false")
            fallthrough
    default:
            fmt.Println("6、默认 case")
    }
}

2、case 条件语句为 true
3、case 条件语句为 false
4、case 条件语句为 true

这里只对第一个串串管用，之间断掉就没用了

如果想要执行多个 case，需要使用 fallthrough 关键字，也可用 break 终止。
switch{
    case 1:
    ...
    if(...){
        break
    }

    fallthrough // 此时switch(1)会执行case1和case2，但是如果满足if条件，则只执行case1

    case 2:
    ...
    case 3:
}

switch 的 default 不论放在哪都是最后执行

### Go 语言 select 语句

https://www.runoob.com/go/go-select-statement.html

select 是 Go 中的一个控制结构，类似于 switch 语句。
select 语句会监听所有指定的通道上的操作，一旦其中一个通道准备好就会执行相应的代码块。
select 语句只能用于通道操作，每个 case 必须是一个通道操作，要么是发送要么是接收。

如果多个通道都准备好，那么 select 语句会随机选择一个通道执行。
如果所有通道都没有准备好，那么执行 default 块中的代码。


select {
  case <- channel1:
    // 执行的代码
  case value := <- channel2:
    // 执行的代码
  case channel3 <- value:
    // 执行的代码

    // 你可以定义任意数量的 case

  default:
    // 所有通道都没有准备好，执行的代码
}

以下描述了 select 语句的语法：

每个 case 都必须是一个通道
所有 channel 表达式都会被求值
所有被发送的表达式都会被求值
如果任意某个通道可以进行，它就执行，其他被忽略。
如果有多个 case 都可以运行，select 会随机公平地选出一个执行，其他不会执行。
否则：
如果有 default 子句，则执行该语句。
如果没有 default 子句，select 将阻塞，直到某个通道可以运行；Go 不会重新对 channel 或值进行求值。

package main

import (
    "fmt"
    "time"
)

func main() {

    c1 := make(chan string)
    c2 := make(chan string)

    go func() {
        time.Sleep(1 * time.Second)
        c1 <- "one"
    }()
    go func() {
        time.Sleep(2 * time.Second)
        c2 <- "two"
    }()

    for i := 0; i < 2; i++ {
        select {
        case msg1 := <-c1:
            fmt.Println("received", msg1)
        case msg2 := <-c2:
            fmt.Println("received", msg2)
        }
    }
}

received one
received two

select 语句等待两个通道的数据。如果接收到 c1 的数据，就会打印 "received one"；如果接收到 c2 的数据，就会打印 "received two"。

以下实例中，我们定义了两个通道，并启动了两个协程（Goroutine）从这两个通道中获取数据。

在 main 函数中，我们使用 select 语句在这两个通道中进行非阻塞的选择，
如果两个通道都没有可用的数据，就执行 default 子句中的语句。


以下实例执行后会不断地从两个通道中获取到的数据，当两个通道都没有可用的数据时，会输出 "no message received"。
package main

import "fmt"

func main() {
  // 定义两个通道
  ch1 := make(chan string)
  ch2 := make(chan string)

  // 启动两个 goroutine，分别从两个通道中获取数据
  go func() {
    for {
      ch1 <- "from 1"
    }
  }()
  go func() {
    for {
      ch2 <- "from 2"
    }
  }()

  // 使用 select 语句非阻塞地从两个通道中获取数据
  for {
    select {
    case msg1 := <-ch1:
      fmt.Println(msg1)
    case msg2 := <-ch2:
      fmt.Println(msg2)
    default:
      // 如果两个通道都没有可用的数据，则执行这里的语句
      fmt.Println("no message received")
    }
  }
}

select 会循环检测条件，如果有满足则执行并退出，否则一直循环检测。
https://www.runoob.com/go/go-select-statement.html 可以看下评论区 //todo
示例代码：https://play.golang.org/p/abKvSe-Nn30

# Day 8 循环语句
