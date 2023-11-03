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

