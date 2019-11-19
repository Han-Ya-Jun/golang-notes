# 数据类型

## 基本数据类型

- 整数类型：
  - 系统架构有关的：int与uint（在32位系统下为32，64位系统下为64）；
  
  - 固定长度的： int8/16/32/64、uint8/16/32/64；
  
  - 整数类型详细表
    ![](http://cdn.hanyajun.com/20190630_163623_int.png)
    
  - 整数类型例子
    ```go
    //1、类型表示
    //int和int32为不同类型，不会自动类型转换需要强制类型转换
    //强制类型转换需注意精度损失（浮点数→整数），值溢出（大范围→小范围）
    var v2 int32
    v1:=64
    v2=int32(v1)
    //2、数值运算,支持“+,-,*,/和%”
    5%3 //求余
    //3、比较运算,“<,>,==,>=,<=,!=”
    //不同类型不能进行比较例如int和int8，但可以与字面常量（literal）进行比较
    var i int32
    var j int64
    i,j=1,2
    if i==j  //编译错误，不同类型不能进行比较
    if i==1 || j==2  //编译通过，可以与字面常量（literal）进行比较
    //4、位运算
    //Go(^x)取反与C语言(~x)不同，其他类似，具体见下表
    ```
  
  - 整数类型的位运算
  ![](http://cdn.hanyajun.com/20190630_164116_bit-operation.png)
  
- 浮点类型：float32、float64

  ```go
  //1、浮点型分为float32(类似C中的float)，float64(类似C中的double)
  var f1 float32
  f1=12     //不加小数点，被推导为整型
  f2:=12.0  //加小数点，被推导为float64
  f1=float32(f2)  //需要执行强制转换
  //2、浮点数的比较
  //浮点数不是精确的表达方式，不能直接使用“==”来判断是否相等，可以借用math的包math.Fdim
  ```

  

- 布尔类型：bool

  ```go
  //布尔类型的关键字为bool,值为true或false，默认为false
  var v1 bool
  v1=true
  //接受表达式判断赋值，不支持自动或强制类型转换
  v2:=(1==2)
  ```

- 复数类型： complex64、complex128

  ```go
  //1、复数的表示
  var v1 complex64
  v1=3.2+12i
  //v1 v2 v3 表示为同一个数
  v2:=3.2+12i
  v3:=complex(3.2,12)
  //2、实部与虚部
  //z=complex(x,y),通过内置函数实部x=real(z),虚部y=imag(z)
  ```

  

- 字符类型： byte（uint8的别名）、rune（int32的别名，标识Unicode）

- 字符串类型： string

  - 一个字符串是一个不可改变的字节序列，可以包含任意的数据，包括byte值0；
  
- for range 语法对UTF8字符串提供了特殊支持；
  
  - 对字符串和 []rune 类型的相互转换提供了支持：如utf8.RuneCountInString(str)；
  
- 字符串其实是一个结构体，因此字符串的赋值操作也就是reflect.StringHeader 结构体的复制过程，并不会涉及底层字节数组的复制。
  
  ```go
  //声明与赋值
  var str string
  str="hello world"
  ```
  
  

## 高级数据类型

- 数组：[N]T，[...]T

- 切片：[]T

- 字典：map[K]T

- 通道类型：chan T

  - 向无缓存通道写入时，会阻塞等待读取；

  - 关闭nil或已关闭通道会引发panic；

  - 向已关闭的通道发生数据会引发panic；

  - 从已关闭的通道读取，总是返回0值和false（对于缓存通道，先读取缓存的数据）；

 ## 自定义数据类型

- 自定义数据类型（可使用type定义）：

- 别名：type BuffSize int；BuffSize为新的类型，底层类型与int相同，但是为不同的类型，互操作时要进行类型转换(BuffSize(var))；

- 自定义类型： type Name struct { ... }

## 变量定义需要注意的几点

 ``` go
package main

import (
	"fmt"
	"math"
	"math/cmplx"
)

var (
	//1.外部的变量定义必须使用var
	aa = 3
	ss = "kkk"
	bb = true
)

    // 2.基本数据类型的初始值
func variableZeroValue() {
	var a int
	var s string
    var c bool
	fmt.Printf("%d %q\n %v", a, s,c)//  0 ""  false
}
   // 3. 可以直接使用  var 变量名 类型 = 值   来初始化变量，同类型的可以使用,来分割
func variableInitialValue() {
	var a, b int = 3, 4
	var s string = "abc"
	fmt.Println(a, b, s)  // 3 4 abc
}
  // 4. 相比上面可以省略变量类型，系统会根据后面初始化的值来自动确定类型
func variableTypeDeduction() {
	var a, b, c, s = 3, 4, true, "def"
	fmt.Println(a, b, c, s)  //3 4 true def
}
// 5. 使用 : 可以代替var 的作用
func variableShorter() {
	a, b, c, s := 3, 4, true, "def"
	b = 5
	fmt.Println(a, b, c, s)  // 3 5 true def
}
// 6. 复数的使用
func euler() {
	fmt.Printf("%.3f\n",
		cmplx.Exp(1i*math.Pi)+1)
}

func triangle() {
	var a, b int = 3, 4
	fmt.Println(calcTriangle(a, b))
}
// 7. 数据类型的转换
func calcTriangle(a, b int) int {
	var c int
	c = int(math.Sqrt(float64(a*a + b*b)))
	return c
}
// 8. 不指定 a,b的类型
func consts() {
	const (
		filename = "abc.txt"
		a, b     = 3, 4
	)
	var c int
	c = int(math.Sqrt(a*a + b*b)) // 系统判定a，b为float
	fmt.Println(filename, c)
}

func enums() {
	const (
		cpp = iota  // 自增常量
		_
		python
		golang
		javascript
	)
    // 常量定义使用const定义
	const (
		b = 1 << (10 * iota)
		kb
		mb
		gb
		tb
		pb
	)

	fmt.Println(cpp, javascript, python, golang)
	fmt.Println(b, kb, mb, gb, tb, pb)
}

func main() {
	fmt.Println("Hello world")
	variableZeroValue()
	variableInitialValue()
	variableTypeDeduction()
	variableShorter()
	fmt.Println(aa, ss, bb)
	euler()
	triangle()
	consts()
	enums()
}
 ```



 