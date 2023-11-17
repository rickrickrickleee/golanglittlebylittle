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
select 是随机执行的不是循环检测，是为了避免饥饿问题，

package main

import (
   "fmt"   "time")

func Chann(ch chan int, stopCh chan bool) {
   for j := 0; j < 10; j++ {
      ch <- j
      time.Sleep(time.Second)
   }
   stopCh <- true}

func main() {

   ch := make(chan int)
   c := 0   stopCh := make(chan bool)

   go Chann(ch, stopCh)

   for {
      select {
      case c = <-ch:
         fmt.Println("Receive C", c)
      case s := <-ch:
         fmt.Println("Receive S", s)
      case _ = <-stopCh:
         goto end
      }
   }
end:
}


import 语句导入了需要使用的包，其中包括 fmt 和 time。

Chann 函数是一个并发的 goroutine 函数。它接受两个参数：一个是整型类型的通道 ch，另一个是布尔类型的通道 stopCh。在函数中，使用一个循环向 ch 通道发送数字，并使用 time.Sleep 函数暂停一秒钟。

main 函数是程序的入口函数。

在 main 函数中，首先创建了一个整型类型的通道 ch，用于接收数字。

c 是一个整型变量，用于存储从 ch 通道接收到的数字。

stopCh 是一个布尔类型的通道，用于通知程序停止运行的信号。

使用 go 关键字启动一个新的 goroutine，调用 Chann 函数并传递 ch 和 stopCh 通道。

使用 select 语句，不断地监听多个通道的数据
当 ch 通道接收到数据时，将数据赋值给变量 c 并打印出来。
当 ch 通道接收到另一个数据时，将数据赋值给变量 s 并打印出来
。当 stopCh 通道接收到数据时，会执行 goto 语句跳转到标签 end，从而结束程序的执行。

end 标签是一个程序结束的标记。

总体而言，这段代码创建了两个 goroutine，
一个用于向 ch 通道发送数字，另一个在 main 函数中使用 select 语句监听多个通道的数据，
并对接收到的数据进行处理和打印。程序在接收到 stopCh 通道的数据后结束执行。

请注意，使用 goto 语句是一种控制流的方式，但在实际的代码编写中，通常应避免过多使用 goto 语句，以保持代码的可读性和可维护性。


# Day 8 循环语句1

循环类型	描述
for 循环	重复执行语句块 https://www.runoob.com/go/go-for-loop.html
循环嵌套	在 for 循环中嵌套一个或多个 for 循环 https://www.runoob.com/go/go-nested-loops.html

## for 循环
执行指定次数的循环
### 有 3 种形式，

只有其中的一种使用分号。

- 和 C 语言的 for 一样：
for init; condition; post { }
- 和 C 的 while 一样：
for condition { }
- 和 C 的 for(;;) 一样：
for { }


init： 一般为赋值表达式，给控制变量赋初值；
condition： 关系表达式或逻辑表达式，循环控制条件；
post： 一般为赋值表达式，给控制变量增量或减量。


### for语句执行过程如下：

1、先对表达式 1 赋初值；

2、判别赋值表达式 init 是否满足给定条件，
若其值为真，满足循环条件，则执行循环体内语句，
然后执行 post，进入第二次循环，再判别 condition；
否则判断 condition 的值为假，不满足条件，就终止for循环，执行循环体外语句。

for 循环的 range 格式可以对 slice、map、数组、字符串等进行迭代循环。格式如下：

for key, value := range oldMap {
    newMap[key] = value
}

key 和 value 是可以省略。

如果只想读取 key，格式如下：
for key := range oldMap
for key, _ := range oldMap

如果只想读取 value，格式如下：
for _, value := range oldMap

### 四个
例子可以自己手打一下
https://www.runoob.com/go/go-for-loop.html

#### 计算 1 到 10 的数字之和：
package main

import "fmt"

func main() {
   sum := 0
      for i := 0; i <= 10; i++ {
         sum += i
      }
   fmt.Println(sum)
}

###  sum 小于 10 的时候计算 sum 自相加后的值：
init 和 post 参数是可选的，我们可以直接省略它，类似 While 语句
package main

import "fmt"

func main() {
   sum := 1
   for ; sum <= 10; {
      sum += sum
   }
   fmt.Println(sum)

   // 这样写也可以，更像 While 语句形式
   for sum <= 10{
      sum += sum
   }
   fmt.Println(sum)
}

还差最后俩 https://www.runoob.com/go/go-for-loop.html 
### For-each range 循环
对字符串、数组、切片等进行迭代输出元素。
package main
import "fmt"

func main() {
   strings := []string{"google", "runoob"}
   for i, s := range strings {
      fmt.Println(i, s)
   }


   numbers := [6]int{1, 2, 3, 5}
   for i,x:= range numbers {
      fmt.Printf("第 %d 位 x 的值 = %d\n", i,x)
   }  
}

0 google
1 runoob
第 0 位 x 的值 = 1
第 1 位 x 的值 = 2
第 2 位 x 的值 = 3
第 3 位 x 的值 = 5
第 4 位 x 的值 = 0
第 5 位 x 的值 = 0

for 循环的 range 格式可以省略 key 和 value，如下实例：

package main
import "fmt"

func main() {
    map1 := make(map[int]float32)
    map1[1] = 1.0
    map1[2] = 2.0
    map1[3] = 3.0
    map1[4] = 4.0
   
    // 读取 key 和 value
    
    for key, value := range map1 {
      fmt.Printf("key is: %d - value is: %f\n", key, value)
    }

    // 读取 key
    
    for key := range map1 {
      fmt.Printf("key is: %d\n", key)
    }

    // 读取 value
    
    for _, value := range map1 {
      fmt.Printf("value is: %f\n", value)
    }
}

key is: 4 - value is: 4.000000
key is: 1 - value is: 1.000000
key is: 2 - value is: 2.000000
key is: 3 - value is: 3.000000
key is: 1
key is: 2
key is: 3
key is: 4
value is: 1.000000
value is: 2.000000
value is: 3.000000
value is: 4.000000

### slice
在编程中，Slice（切片）是一种动态数组的抽象数据类型。Slice 提供了对底层数组的引用，并提供了一组操作函数来方便地操作数组。

Slice 由三个主要部分组成：

指向底层数组的指针。
Slice 的长度，即当前 Slice 中的元素数量。
Slice 的容量，即底层数组中可访问的元素数量。
Slice 可以动态地增长和缩小，因此非常灵活。当你向 Slice 中添加元素时，
如果超过了当前容量，Slice 会自动扩容，底层的数组也会重新分配更大的内存空间。
这使得 Slice 非常适用于处理动态大小的数据集合。

在 Go 语言中。它是基于数组的一种高级抽象，提供了方便的操作和灵活的大小调整能力
在使用 Slice 时，你可以使用索引访问和修改元素，
也可以使用内置的函数来执行各种操作，如追加、复制、切割等。

package main

import "fmt"

func main() {
   // 创建一个 Slice
   s := []int{1, 2, 3, 4, 5}

   // 使用索引访问和修改元素
   fmt.Println(s[0]) // 输出: 1
   s[2] = 10
   fmt.Println(s) // 输出: [1 2 10 4 5]

   // 使用内置函数操作 Slice
   s = append(s, 6) // 追加元素
   fmt.Println(s)  // 输出: [1 2 10 4 5 6]

   // 切割 Slice
   subSlice := s[1:4]
   fmt.Println(subSlice) // 输出: [2 10 4]
}

# Day 9 循环语句2

GO 语言支持以下几种循环控制语句：
控制语句	描述
break 语句	经常用于中断当前 for 循环或跳出 switch 语句 https://www.runoob.com/go/go-break-statement.html 
continue 语句	跳过当前循环的剩余语句，然后继续进行下一轮循环。 https://www.runoob.com/go/go-continue-statement.html
goto 语句	将控制转移到被标记的语句。https://www.runoob.com/go/go-goto-statement.html

## 无限循环
如果循环中条件语句永远不为 false 则会进行无限循环，我们可以通过 for 循环语句中只设置一个条件表达式来执行无限循环：
package main

import "fmt"

func main() {
    for true  {
        fmt.Printf("这是无限循环。\n");
    }
}
要停止无限循环，可以在命令窗口按下ctrl-c 。
package main

import "fmt"

func main() {
   sum := 0
   for {
      sum++ // 无限循环下去
   }
   fmt.Println(sum) // 无法输出
}
  

## Go 语言循环嵌套

for [condition |  ( init; condition; increment ) | Range]
{
   for [condition |  ( init; condition; increment ) | Range]
   {
      statement(s);
   }
   statement(s);
}

循环嵌套来输出 2 到 100 间的素数：

package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var i, j int

   for i=2; i < 100; i++ {
      for j=2; j <= (i/j); j++ {
         if(i%j==0) {
            break; // 如果发现因子，则不是素数
         }
      }
      if(j > (i/j)) {
         fmt.Printf("%d  是素数\n", i);
      }
   }  
}

2  是素数
3  是素数
5  是素数
7  是素数
11  是素数
13  是素数
17  是素数
19  是素数
23  是素数
29  是素数
31  是素数
37  是素数
41  是素数
43  是素数
47  是素数
53  是素数
59  是素数
61  是素数
67  是素数
71  是素数
73  是素数
79  是素数
83  是素数
89  是素数
97  是素数
    
九九乘法表：
package main 

import "fmt"

func main() {
    for m := 1; m < 10; m++ {
    /*    fmt.Printf("第%d次：\n",m) */
        for n := 1; n <= m; n++ {
            fmt.Printf("%dx%d=%d ",n,m,m*n)
        }
        fmt.Println("")
    }
}

## break 语句
终止当前循环或者 switch 语句的执行

用于循环语句中跳出循环，并开始执行循环之后的语句。
break 在 switch 语句中在执行一条 case 后跳出语句的作用。
break 可应用在 select 语句中。
在多重循环中，可以**用标号 label 标出**想 break 的循环。

package main

import "fmt"

func main() {
    for i := 0; i < 10; i++ {
        if i == 5 {
            break // 当 i 等于 5 时跳出循环
        }
        fmt.Println(i)
    }
}

0
1
2
3
4

在变量 a 大于 15 的时候跳出循环：

package main

import "fmt"

func main() {
   /* 局部变量 */
   var a int = 10
   
   for a < 20 {
      fmt.Printf("a 的值为 : %d\n", a);
      a++
      if a > 15 {
         /* a 大于 15 时使用 break 语句跳出循环 */
         break
      }
   }
   
}
a 的值为 : 10
a 的值为 : 11
a 的值为 : 12
a 的值为 : 13
a 的值为 : 14
a 的值为 : 15

多重循环，演示了使用标记和不使用标记的区别：

package main

import "fmt"

func main() {

   // 不使用标记
   fmt.Println("---- break ----")
   for i := 1; i <= 3; i++ {
      fmt.Printf("i: %d\n", i)
      for i2 := 11; i2 <= 13; i2++ {
         fmt.Printf("i2: %d\n", i2)
         break
      }
   }

   // 使用标记
   fmt.Println("---- break label ----")
   re:
      for i := 1; i <= 3; i++ {
         fmt.Printf("i: %d\n", i)
         for i2 := 11; i2 <= 13; i2++ {
         fmt.Printf("i2: %d\n", i2)
         break re
      }
   }
}

---- break ----
i: 1
i2: 11
i: 2
i2: 11
i: 3
i2: 11
---- break label ----
i: 1
i2: 11    

在 switch 语句中使用 break：
import "fmt"

func main() {
    day := "Tuesday"
    switch day {
    case "Monday":
        fmt.Println("It's Monday.")
    case "Tuesday":
        fmt.Println("It's Tuesday.")
        break // 跳出 switch 语句
    case "Wednesday":
        fmt.Println("It's Wednesday.")
    }
}

select：
package main

import (
    "fmt"
    "time"
)

func main() {
    ch1 := make(chan int)
    ch2 := make(chan int)

    go func() {
        time.Sleep(2 * time.Second)
        ch1 <- 1
    }()

    go func() {
        time.Sleep(1 * time.Second)
        ch2 <- 2
    }()

    select {
    case <-ch1:
        fmt.Println("Received from ch1.")
    case <-ch2:
        fmt.Println("Received from ch2.")
        break // 跳出 select 语句
    }
}

Received from ch2.

*没看懂*解释
段代码使用了goroutine和channel来实现并发通信。在main函数中，首先创建了两个整型的通道ch1和ch2。

接下来，通过go关键字创建了两个匿名函数作为goroutine。第一个匿名函数会在2秒后向ch1通道发送值1，而第二个匿名函数会在1秒后向ch2通道发送值2。

然后，在select语句中使用了两个case分支，分别监听ch1和ch2通道。select语句会等待这两个通道中的数据到达，并执行对应的分支。

由于ch2通道的数据会先到达（1秒后），因此第二个case分支会被执行，打印出"Received from ch2."的消息。

在这个例子中，break语句被用于跳出select语句，因此程序会在打印消息后结束执行。

总结起来，这段代码创建了两个goroutine，在不同的时间点向两个通道发送数据，并使用select语句监听通道并执行相应的操作。在本例中，先收到数据的通道会触发相应的case分支执行，而break语句用于跳出select语句。

*看懂了*

break 语句在 select 语句中的应用是相对特殊的。由于 select 语句的特性，break 语句并不能直接用于跳出 select 语句本身，因为 select 语句是非阻塞的，它会一直等待所有的通信操作都准备就绪。如果需要提前结束 select 语句的执行，可以使用 return 或者 goto 语句来达到相同的效果。

以下实例，展示了在 select 语句中使用 return 来提前结束执行的情况：
package main

import (
    "fmt"
    "time"
)

func process(ch chan int) {
    for {
        select {
        case val := <-ch:
            fmt.Println("Received value:", val)
            // 执行一些逻辑
            if val == 5 {
                return // 提前结束 select 语句的执行
            }
        default:
            fmt.Println("No value received yet.")
            time.Sleep(500 * time.Millisecond)
        }
    }
}

func main() {
    ch := make(chan int)

    go process(ch)

    time.Sleep(2 * time.Second)
    ch <- 1
    time.Sleep(1 * time.Second)
    ch <- 3
    time.Sleep(1 * time.Second)
    ch <- 5
    time.Sleep(1 * time.Second)
    ch <- 7

    time.Sleep(2 * time.Second)
}

以上实例中，process 函数在一个无限循环中使用 select 语句等待通道 ch 上的数据。当接收到数据时，会执行一些逻辑。当接收到的值等于 5 时，使用 return 提前结束 select 语句的执行。

输出结果：

No value received yet.
No value received yet.
Received value: 1
No value received yet.
Received value: 3
No value received yet.
Received value: 5

*没看懂*解释
在main函数中，首先创建了一个整型通道ch。然后，通过go关键字启动了一个goroutine，其中调用了process函数，并将通道ch作为参数传递进去。

process函数是一个无限循环，在每次循环中使用select语句监听通道ch。在select语句中，有两个case分支：

第一个case分支是对ch通道的接收操作。当通道中有值可接收时，会将接收到的值打印出来，并执行一些逻辑。在这个例子中，如果接收到的值等于5，那么会使用return语句提前结束select语句的执行。
第二个case分支是默认分支（default）。如果通道中没有值可接收，那么default分支会被执行，打印出"No value received yet."的消息，并通过time.Sleep函数暂停500毫秒。
回到main函数，接下来通过time.Sleep函数分别等待了2秒、1秒、1秒和1秒，然后向通道ch发送了四个值：1、3、5和7。

在process函数的循环中，由于ch通道中有值可接收，因此第一个case分支会被执行。这样，在接收到值为5时，process函数使用return语句提前结束了select语句的执行。

最后，main函数通过time.Sleep函数等待了2秒，以保证process函数有足够的时间执行完毕。

总结起来，这段代码展示了如何使用select语句和channel实现非阻塞的接收操作。通过在select语句中使用default分支，可以在通道没有值可接收时执行一些其他的逻辑，而不会阻塞整个程序的执行。

通过使用 return，我们可以在 select 语句中提前终止执行，并返回到调用者的代码中。

需要注意的是，使用 return 语句会立即终止当前的函数执行，所以请根据实际需求来决定在 select 语句中使用何种方式来提前结束执行。

## continue
 continue 不是跳出循环，而是跳过当前循环执行下一次循环语句
 for 循环中，执行 continue 语句会触发 for 增量语句的执行。
在多重循环中，可以用标号 label 标出想 continue 的循环。

在变量 a 等于 15 的时候**跳过本次循环**执行下一次循环：

package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 10

   /* for 循环 */
   for a < 20 {
      if a == 15 {
         /* 跳过此次循环 */
         a = a + 1;
         continue;
      }
      fmt.Printf("a 的值为 : %d\n", a);
      a++;    
   }  
}

a 的值为 : 10
a 的值为 : 11
a 的值为 : 12
a 的值为 : 13
a 的值为 : 14
a 的值为 : 16
a 的值为 : 17
a 的值为 : 18
a 的值为 : 19

多重循环，演示了使用标记和不使用标记的区别：
package main

import "fmt"

func main() {

    // 不使用标记
    fmt.Println("---- continue ---- ")
    for i := 1; i <= 3; i++ {
        fmt.Printf("i: %d\n", i)
            for i2 := 11; i2 <= 13; i2++ {
                fmt.Printf("i2: %d\n", i2)
                continue
            }
    }

    // 使用标记
    fmt.Println("---- continue label ----")
    re:
        for i := 1; i <= 3; i++ {
            fmt.Printf("i: %d\n", i)
                for i2 := 11; i2 <= 13; i2++ {
                    fmt.Printf("i2: %d\n", i2)
                    continue re
                }
        }
}

---- continue ---- 
i: 1
i2: 11
i2: 12
i2: 13
i: 2
i2: 11
i2: 12
i2: 13
i: 3
i2: 11
i2: 12
i2: 13
---- continue label ----
i: 1
i2: 11
i: 2
i2: 11
i: 3
i2: 11

解释
在第一个部分中，使用了continue语句而没有标记。代码执行进入第一个for循环，i的值从1到3依次递增。在每次循环中，有一个内部的for循环，i2的值从11到13递增。在内部循环中，continue语句被执行，导致内部循环直接跳到下一次迭代。因此，每次迭代只打印出了i的值，而i2的循环只执行了一次。

在第二个部分中，使用了带有标记的continue语句。在外部for循环之前，有一个标记re。在内部循环中，continue语句被执行时，它指定了标记re，表示继续外部循环的下一次迭代。这样，每次迭代中的内部循环都会被重新开始，从i2的初始值11开始，直到13。因此，每次迭代都会打印出i的值，并执行完整的内部循环。

总结起来，continue语句用于跳过当前循环中剩余的代码，并继续下一次循环的执行。当不使用标记时，continue只会跳过当前循环。而使用标记时，continue可以跳过带有标记的循环，并继续执行标记所在的循环的下一次迭代。

# Day 10 必须自己写一个上面的类似的
## goto 语句 代码块

goto 语句可以无条件地转移到过程中指定的行。
通常与条件语句配合使用。可用来实现条件转移， 构成循环，跳出循环体等功能。
在结构化程序设计中一般不主张使用 goto 语句

goto label;
..
.
label: statement;

在变量 a 等于 15 的时候跳过本次循环并回到循环的开始语句 LOOP 处：
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 10

   /* 循环 */
   LOOP: for a < 20 {
      if a == 15 {
         /* 跳过迭代 */
         a = a + 1
         goto LOOP
      }
      fmt.Printf("a的值为 : %d\n", a)
      a++    
   }  
}
a的值为 : 10
a的值为 : 11
a的值为 : 12
a的值为 : 13
a的值为 : 14
a的值为 : 16
a的值为 : 17
a的值为 : 18
a的值为 : 19

打印九九乘法表:希望自己也可以写出这样的逻辑

package main 

import "fmt"

func main() {
    //print9x()
    gotoTag()
}

//嵌套for循环打印九九乘法表
func print9x() {
    for m := 1; m < 10; m++ {
        for n := 1; n <= m; n++ {
          fmt.Printf("%dx%d=%d ",n,m,m*n)
        }
        fmt.Println("")
    }
}

//for循环配合goto打印九九乘法表
func gotoTag() {
    for m := 1; m < 10; m++ {
    n := 1
    LOOP: if n <= m {
        fmt.Printf("%dx%d=%d ",n,m,m*n)
        n++
        goto LOOP
    } else {
        fmt.Println("")
    }
    n++
    }
}

## 求 100 内素数，我也来贴一个最终版的：
（这些人是在刷题吧，应该可以吧脑子通过刷题变灵活）
// 打印100内的素数
// 素数定义：在大于1的自然数中，因数只有1和自身的数称为素数。
func t01_test2() {
    const RANGE = 100
    for num := 2; num <= RANGE; num++ {
        // 当前因数 factor 对应的另一个因数就是 num / factor。
        // 当前者大于后者时，可以认为所有因数已经分析完毕。
        for factor := 2; factor <= (num / factor); factor++ {
            //能除尽，则表示 factor 是 num 的一个因子。那么num就不是素数。
            if num%factor == 0 {
                goto NEXT_NUM
            }
        }
        fmt.Printf("%d\t是素数\n", num)
    NEXT_NUM:
    }
}

## 欢迎进入成绩查询系统

package main
import "fmt"
import "strconv"
import "os"

func main(){
    var score int = 0
    var fenshu string = "A"
    fmt.Printf("欢迎进入成绩查询系统\n")
    ZHU: for true{
        var xuanzhe int = 0
        fmt.Println("1.进入成绩查询 2.退出程序")
        fmt.Printf("请输入序号选择:")
        fmt.Scanln(&xuanzhe)
        fmt.Printf("\n")
        if xuanzhe == 1{
             goto CHA
        }
        if xuanzhe == 2{
            os.Exit(1)
        }

    }

    CHA: for true {
        fmt.Printf("请输入一个学生的成绩:")
        fmt.Scanln(&score)

        switch {
            case score >= 90:fenshu = "A"

            case score >= 80&&score < 90:fenshu = "B"

            case score >= 60&&score < 80:fenshu = "C"

            default: fenshu = "D"
        }

        //fmt.Println(fenshu)
         var c string  = strconv.Itoa(score)
        switch{
            case fenshu == "A":
                fmt.Printf("你考了%s分,评价为%s,成绩优秀\n",c,fenshu)
            case fenshu == "B" || fenshu == "C":
                fmt.Printf("你考了%s分,评价为%s,成绩良好\n",c,fenshu)
            case fenshu == "D":
                fmt.Printf("你考了%s分,评价为%s,成绩不合格\n",c,fenshu)
        }
        fmt.Printf("\n")
        goto ZHU
}
    //fmt.Println(score)
}

# Day 10 Go 语言函数 函数定义

函数是基本的代码块，用于执行一个任务。

Go 语言最少有个 main() 函数。

你可以通过函数来划分不同功能，逻辑上每个函数执行的是指定的任务。

函数声明告诉了编译器函数的名称，返回类型，和参数。

Go 语言标准库提供了多种可动用的内置的函数。例如，len() 函数可以接受不同类型参数并返回该类型的长度。如果我们传入的是字符串则返回字符串的长度，如果传入的是数组，则返回数组中包含的元素个数。

Go 语言函数定义格式如下：

func function_name( [parameter list] ) [return_types] {
   函数体
}

函数定义解析：

func：函数由 func 开始声明
function_name：函数名称，参数列表和返回值类型构成了函数签名。
parameter list：参数列表，参数就像一个占位符，当函数被调用时，你可以将值传递给参数，这个值被称为实际参数。参数列表指定的是参数类型、顺序、及参数个数。参数是可选的，也就是说函数也可以不包含参数。
return_types：返回类型，函数返回一列值。
return_types 是该列值的数据类型。
有些功能不需要返回值，这种情况下 return_types 不是必须的。

函数体：函数定义的代码集合。

max() 函数的代码，该函数传入两个整型参数 num1 和 num2，并返回这两个参数的最大值：
/* 函数返回两个数的最大值 */
func max(num1, num2 int) int {
   /* 声明局部变量 */
   var result int

   if (num1 > num2) {
      result = num1
   } else {
      result = num2
   }
   return result
}


## 函数调用

通过调用该函数来执行指定任务。在 main() 函数中调用 max（）函数

package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 100
   var b int = 200
   var ret int

   /* 调用函数并返回最大值 */
   ret = max(a, b)

   fmt.Printf( "最大值是 : %d\n", ret )
}

/* 函数返回两个数的最大值 */
func max(num1, num2 int) int {
   /* 定义局部变量 */
   var result int

   if (num1 > num2) {
      result = num1
   } else {
      result = num2
   }
   return result
}
最大值是 : 200


## 函数返回多个值

package main

import "fmt"

func swap(x, y string) (string, string) {
   return y, x
}

func main() {
   a, b := swap("Google", "Runoob")
   fmt.Println(a, b)
}

Runoob Google

## 函数参数

函数如果使用参数，该变量可称为函数的形参。
形参就像定义在函数体内的局部变量。
调用函数，可以通过两种方式来传递参数：

传递类型	描述
值传递	https://www.runoob.com/go/go-function-call-by-value.html
值传递是指在调用函数时将实际参数复制一份传递到函数中，
这样在函数中如果对参数进行修改，将不会影响到实际参数。

引用传递	https://www.runoob.com/go/go-function-call-by-reference.html
引用传递是指在调用函数时将实际参数的地址传递到函数中，
那么在函数中对参数所进行的修改，将影响到实际参数。
默认情况下，Go 语言使用的是值传递，即在调用过程中不会影响到实际参数

## 函数用法

函数用法	描述
函数作为另外一个函数的实参	函数定义后可作为另外一个函数的实参数传入 https://www.runoob.com/go/go-function-as-values.html
闭包	闭包是匿名函数，可在动态编程中使用 https://www.runoob.com/go/go-function-closures.html
方法	方法就是一个包含了接受者的函数https://www.runoob.com/go/go-method.html

