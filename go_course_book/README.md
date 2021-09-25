

## go学习


## 01 Go语言基本语法

### 1.1 Go语言变量的声明

Go语言是静态类型语言，因此变量（variable）是有明确类型的，编译器也会检查变量类型的正确性。

声明变量的一般形式是使用var关键字:

```go
var name type
```

var 是声明变量的关键字，name是变量名，type是变量的类型。

Go语言的基本类型有

- bool
- string
- int、int8、int16、int32、int64
- uint、uint8、uint16、uint32、uint64、uintptr
- byte // uint8 的别名
- rune // int32 的别名 代表一个 Unicode 码
- float32、float64
- complex64、complex128

当一个变量被声明之后，系统自动赋予它该类型的零值：int 为 0，float 为 0.0，bool 为 false，string 为空字符串，指针为 nil 等。所有的内存在 Go 中都是经过初始化的。

变量的命名规则遵循骆驼命名法，即首个单词小写，每个新单词的首字母大写，例如：numShips 和 startDate 。

#### 标准格式

Go语言的变量声明的标准格式为:

```go
var 变量名 变量类型
```

#### 批量格式

```go
var (
    a int
    b string
    c [] float32
    d func() bool
    e struct {
        x int
    }
)
```

使用关键字 var 和 括号， 可以将一组变量定义放在一起

#### 简短格式

除var关键字外，还可以使用更加简短的变量定义和初始化语法。

```
名字 := 表达式
```

需要注意的是，简短模式（short variable declaration）有以下限制：

- 定义变量，同时显式初始化。
- 不能提供数据类型。
- 只能用在函数内部。

和 var 形式声明语句一样，简短变量声明语句也可以用来声明和初始化一组变量：

```go
i, j := 0, 1
```

```go
func main() {
   x:=100
   a,s:=1, "abc"
}
```



### 1.2 Go语言变量的初始化

每个变量会初始化其类型的默认值，例如:

- 整型和浮点型变量的默认值为 0 和 0.0。
- 字符串变量的默认值为空字符串。
- 布尔型变量默认为 bool。
- 切片、函数、指针变量的默认为 nil。

#### 变量初始化的标准格式

```go
var 变量名 类型 = 表达式
```

#### 编译器推导类型的格式

在标准格式的基础上，将int省略后，编译器会尝试根据等号右边的表达式推导hp变量的类型。

```go
var hp = 100
```

等号右边的部分在编译原理里被称做右值

```go
var attack = 40var defence = 20var damageRate float32
```

#### 短变量声明并初始化

```go
// 声明 hp 变量
var hp int
// 再次声明并赋值
hp := 10
```
编译报错如下
```
no new variables on left side of :=
```
在“:=”的左边没有新变量出现，意思就是“:=”的左边变量已经被声明了。


### 1.3 Go语言多个变量同时赋值



```go
func demo_301() {
	// golang如何一次性声明多个变量
	var n1, n2, n3 int
	fmt.Println("n1=", n1, "n2=", n2, "n3=", n3)

	// 一次性声明多个变量的方式2:
	var b1, b2, b3 = 100, "tom", 888
	fmt.Println("b1=", b1, "b2=", b2, "b3=", b3)

	// 一次性声明多个变量的方式3: 同样可以使用类型推导
	c1, c2, c3 := 100, "tome", 888
	fmt.Println("c1=", c1, "c2=", c2, "c3=", c3)

	// 打印全局变量
	fmt.Println("a1=", a1, "a2=", a2, "a3=", a3)
	fmt.Println("a4=", a4, "a5=", a5, "a6=", a6)
}
```

```go
func demo_302() {
	var a int = 100
	var b int = 200
	var t int
	t = a
	a = b
	b = t
	fmt.Println(a, b)
}
```

```go
func demo_303() {
	var a int = 100
	var b int = 200

	b, a = a, b
	fmt.Println(a, b)
}

```


### 1.4 Go语言匿名变量

匿名变量的特点是一个下划线 "_"，"_" 本身就是一个特殊的标识符，被称为空白标识符。

```go
func GetData() (int, int)  {	return 100, 200}func main() {	a, _ := GetData()	_, b := GetData()	fmt.Println(a, b)}
```

匿名变量不占用内存空间，不会分配内存。匿名变量与匿名变量之间也不会因为多次声明而无法使用。

### 1.5 Go语言变量的作用域

根据变量定义位置的不同，可以分为以下三种类型:

- 函数内定义的变量称为局部变量
- 函数外定义的变量称为全局变量
- 函数定义中的变量称为形式参数



#### 局部变量
```go
func demo501() {
	//声明局部变量 a 和 b 并赋值
	var a int = 3
	var b int = 4
	//声明局部变量 c 并计算 a 和 b 的和
	c := a + b
	fmt.Printf("a = %d, b = %d, c = %d\n", a, b, c)
}
```




#### 全局变量
```go
var a float32 = 3.14

func demo502() {
	//声明局部变量
	var a int = 3
	fmt.Printf("a = %d\n", a)
}
```


#### 形式参数

```go
func sum(a, b int) int {
	fmt.Printf("sum() 函数中 a = %d\n", a)
	fmt.Printf("sum() 函数中 b = %d\n", b)
	num := a + b
	return num
}

func demo503() {
	//局部变量 a 和 b
	var a int = 3
	var b int = 4
	fmt.Printf("demo503() 函数中 a = %d\n", a)
	fmt.Printf("demo503() 函数中 b = %d\n", b)
	c := sum(a, b)
	fmt.Printf("demo503()函数中 c = %d\n", c)
}
```



### 1.6 Go语言整型（整数类型）

Go语言同时提供了有符号和无符号的整数类型，其中包括 int8、int16、int32 和 int64 四种大小截然不同的有符号整数类型，分别对应 8、16、32、64 bit（二进制位）大小的有符号整数，与此对应的是 uint8、uint16、uint32 和 uint64 四种无符号整数类型。

此外还有两种整数类型 int 和 uint，它们分别对应特定 CPU 平台的字长（机器字大小），其中 int 表示有符号整数，应用最为广泛，uint 表示无符号整数。实际开发中由于编译器和计算机硬件的不同，int 和 uint 所能表示的整数大小会在 32bit 或 64bit 之间变化。

```
uint8  : 0 to 255 
uint16 : 0 to 65535 
uint32 : 0 to 4294967295 
uint64 : 0 to 18446744073709551615 
int8   : -128 to 127 
int16  : -32768 to 32767 
int32  : -2147483648 to 2147483647 
int64  : -9223372036854775808 to 9223372036854775807
```

**Unicode字符rune类型是和int32等价的类型，通常用于表示一个Unicode码点。这两个名称可以互换使用。同样byte也是uint8类型的等价类型，byte类型一般用于强调数值是一个原始的数据而不是一个小的整数。**

```go
// golang中整数类型使用
func demo601() {
	// int8的范围 -128-127
	var n1 int8 = 127
	fmt.Println("n1=", n1)

	// uint8的范围 0-255
	var n2 uint8 = 255
	fmt.Println("n2=", n2)

	// unsafe.Sizeof() 返回变量占用字节数
	fmt.Printf("n2 的 类型 %T  n2 占用的字节数是 %d ", n1, unsafe.Sizeof(n1))
}
```



### 1.7 Go语言浮点类型（小数类型）

这些浮点数类型的取值范围可以从很微小到很巨大。浮点数取值范围的极限值可以在 math 包中找到：

- 常量 math.MaxFloat32 表示 float32 能取到的最大数值，大约是 3.4e38；
- 常量 math.MaxFloat64 表示 float64 能取到的最大数值，大约是 1.8e308；
- float32 和 float64 能表示的最小值分别为 1.4e-45 和 4.9e-324。


```go
// golang中浮点类型使用
func demo701() {
	var price float32 = 2222
	fmt.Println("price=", price)
	var num1 float32 = 0.0000012
	var num2 float64 = 64444.333311
	fmt.Println("num1=", num1, "num2=", num2)

	// 尾数部分可能丢失、造成精度损失。 -123.0000901
	var num3 float32 = -123.0000901
	var num4 float64 = -123.0000901
	fmt.Println("num3=", num3, "num4=", num4)

	// Golang的浮点型默认声明为float64 类型
	var num5 = 1.1
	fmt.Println("num5的数据类型是 %T", num5)

	// 十进制数形式: 5.12  .512 必须有小数点
	num6 := 5.12
	fmt.Println("num6=", num6)

	// 科学计数法
	num7 := 5.1234e2 // 5.1234 * 10的2次方
	num8 := 5.123e-2 // 5.1234 * 10的-2次方
	fmt.Println("num7=", num7, "num8=", num8)
}
```

### 1.8 Go语言复数

复数的两个浮点数表示，其中一个表示实部(real)，一个表示虚部(imag)。

Go语言中复数的类型有两种，分别是complex128(64位实数和虚数) 和 complex64 (32位实数和虚数)。

复数的值由三部分组成RE + IMi, 其中RE是实数部分，IM虚数部分，RE和IM均为float类型，而最后的是i是虚数单位

声明复数的语法格式如下所示:

```
var name complex128 = complex(x, y)
```

其中 name  为复数的变量名，complex128 为复数的类型，`=`后面的complex为Go语言的内置函数用于复数赋值，x, y 分别表示构成该复数的两个 float64 类型的数值，x为实部，y为虚部。

```
name := complex(x, y)
```

对于一个复数`z := complex(x, y)`,可以通过Go语言的内置函数`real(z)`来获得该复数的实部，也就是x，`imag(z)`获得该复数的虚部，也就是y。

```go

// 复数类型
func demo801() {
	var x1 complex128 = complex(1, 2)
	var y1 complex128 = complex(1, 2)
	fmt.Println(x1)
	fmt.Println(y1)
	fmt.Println(x1 * y1)
	fmt.Println(real(y1), imag(x1))
}
```



### 1.9 Go语言bool类型（布尔类型）

一个布尔类型的值只有两种：true 或 false, if 和 for 语句的条件部分都是布尔类型的值，并且`==`和`<`等比较操作也会产生布尔型的值。

Go语言对于值之间的比较有非常严格的限制，只有两个相同类型的值才可以进行比较，如果值得类型是接口(interface)，那么它们也必须都实现了相同的接口，如果其中一个值是常量，那么另外一个值可以不是常量，但是类型必须和该常量类型相同。

布尔值可以和 && （AND) 和 || (OR) 操作符结合。

数字类型和布尔类型的切换

```go
func demo_901() {
	var b = false
	// bool类型占用存储空间是1个字节
	// bool类型只能取true或者false
	fmt.Println("b=", b)
}

func demo_902(b bool) int {
	if b {
		return 1
	}
	return 0
}

func demo_903(i int) bool {
	return i != 1
}

```



### 1.10 Go语言字符串类型

#### 转义字符

	\a             匹配响铃符    （相当于 \x07）               注意：正则表达式中不能使用 \b 匹配退格符，因为 \b 被用来匹配单词边界，               可以使用 \x08 表示退格符。\f             匹配换页符    （相当于 \x0C）\t             匹配横向制表符（相当于 \x09）\n             匹配换行符    （相当于 \x0A）\r             匹配回车符    （相当于 \x0D）\v             匹配纵向制表符（相当于 \x0B）\123           匹配 8  進制编码所代表的字符（必须是 3 位数字）\x7F           匹配 16 進制编码所代表的字符（必须是 3 位数字）\x{10FFFF}     匹配 16 進制编码所代表的字符（最大值 10FFFF  ）\Q...\E        匹配 \Q 和 \E 之间的文本，忽略文本中的正则语法\\             匹配字符 \\^             匹配字符 ^\$             匹配字符 $\.             匹配字符 .\*             匹配字符 *\+             匹配字符 +\?             匹配字符 ?\{             匹配字符 {\}             匹配字符 }\(             匹配字符 (\)             匹配字符 )\[             匹配字符 [\]             匹配字符 ]\|             匹配字符 |

- 定义字符串

- 定义多行字符串
- 字符串拼接

```go
// golang中string类型使用
func demo1001() {
	// string的基本类型使用
	var address string = "北京长城 110 hello world"
	fmt.Println(address)

	// 字符串一旦赋值了，字符串就不能修改了: 在Go中字符串是不可变的
	var str = "hello"
	// str[0] = 'a' 字符串不可变
	fmt.Println(str)

	// 使用反引号定义多行字符串
	var str2 = `
			func main() {
				var b = false
				// bool类型占用存储空间是1个字节
				// bool类型只能取true或者false
				fmt.Println("b=", b)
			}`
	fmt.Println(str2)

	var str3 = "hello" + ",world"
	fmt.Println(str3)
}
```



### 1.11 Go语言字符类型（byte和rune）

Go语言的字符有以下两种：

- 一种是 uint8 类型，或者叫 byte 型，代表了 ASCII 码的一个字符。
- 另一种是 rune 类型，代表一个 UTF-8 字符，当需要处理中文、日文或者其他复合字符时，则需要用到 rune 类型。rune 类型等价于 int32 类型。

在 ASCII 码表中，A 的值是 65，使用 16 进制表示则为 41，所以下面的写法是等效的：

```go
var ch byte = 65 或 var ch byte = '\x41'      //（\x 总是紧跟着长度为 2 的 16 进制数）
```

在书写 Unicode 字符时，需要在 16 进制数之前加上前缀`\u`或者`\U`。因为 Unicode 至少占用 2 个字节，所以我们使用 int16 或者 int 类型来表示。如果需要使用到 4 字节，则使用`\u`前缀，如果需要使用到 8 个字节，则使用`\U`前缀。

```go
func demo_1101() {
	var ch int = '\u0041'
	var ch2 int = '\u03B2'
	var ch3 int = '\U00101234'
	fmt.Printf("%d - %d - %d\n", ch, ch2, ch3) // integer
	fmt.Printf("%c - %c - %c\n", ch, ch2, ch3) // character
	fmt.Printf("%X - %X - %X\n", ch, ch2, ch3) // UTF-8 bytes
	fmt.Printf("%U - %U - %U", ch, ch2, ch3)   // UTF-8 code point
	/* Output
	65 - 946 - 1053236
	A - β - 􁈴
	41 - 3B2 - 101234
	U+0041 - U+03B2 - U+101234
	*/
}
```

Unicode 与 ASCII 类似，都是一种字符集。

字符集为每个字符分配一个唯一的 ID，我们使用到的所有字符在 Unicode 字符集中都有一个唯一的 ID，例如上面例子中的 a 在 Unicode 与 ASCII 中的编码都是 97。汉字“你”在 Unicode 中的编码为 20320，在不同国家的字符集中，字符所对应的 ID 也会不同。而无论任何情况下，Unicode 中的字符的 ID 都是不会变化的。

UTF-8 是编码规则，将 Unicode 中字符的 ID 以某种方式进行编码，UTF-8 的是一种变长编码规则，从 1 到 4 个字节不等。编码规则如下：

- 0xxxxxx 表示文字符号 0～127，兼容 ASCII 字符集。
- 从 128 到 0x10ffff 表示其他字符。

### 1.12 Go语言数据类型转换

Go語言不存在隐式类型转换，因此所有的类型转换都必须显示的声明:

```go
valueOfTypeB = typeB(valueOfTypeA)类型B的值 = 类型B(类型A的值)
```

```go
func demo1201() {
	// 输出各数值范围
	fmt.Println("int8 range:", math.MinInt8, math.MaxInt8)
	fmt.Println("int16 range:", math.MinInt16, math.MaxInt16)
	fmt.Println("int32 range:", math.MinInt32, math.MaxInt32)
	fmt.Println("int64 range:", math.MinInt64, math.MaxInt64)
	// 初始化一个32位整型值
	var a int32 = 1047483647
	// 输出变量的十六进制形式和十进制值
	fmt.Printf("int32: 0x%x %d\n", a, a)
	// 将a变量数值转换为十六进制, 发生数值截断
	b := int16(a)
	// 输出变量的十六进制形式和十进制值
	fmt.Printf("int16: 0x%x %d\n", b, b)
	// 将常量保存为float32类型
	var c float32 = math.Pi
	// 转换为int类型, 浮点发生精度丢失
	fmt.Println(int(c))
}
```

代码输出结果：

```
int8 range: -128 127int16 range: -32768 32767int32 range: -2147483648 2147483647int64 range: -9223372036854775808 9223372036854775807int32: 0x3e6f54ff 1047483647int16: 0x54ff 217593
```

根据输出结果，16 位有符号整型的范围是 -32768～32767，而变量 a 的值 1047483647 不在这个范围内。1047483647 对应的十六进制为 0x3e6f54ff，转为 int16 类型后，长度缩短一半，也就是在十六进制上砍掉一半，变成 0x54ff，对应的十进制值为 21759。

浮点数在转换为整型时，会将小数部分去掉，只保留整数部分。

### 1.13 Go语言指针

指针(pointer) 在Go语言中可以被拆分为两个核心概念:

- 类型指针，允许对这个指针类型的数据进行修改，传递数据可以直接使用指针，而无拷贝数据，类型指针不能进行偏移和运算。
- 切片，有指向起始元素的原始数量和容量组成 

#### 认识指针地址和指针类型

一个指针变量可以指向一个值得内存地址，它所指向的内存地址在32 和 64 位机器上分别占用4或8个字节，占用字节的大小与所指向的值得大小无关。当一个指针被定义后没有分配到任何变量时，它的默认值为nil。指针变量通常缩写为ptr。

每个变量在运行时都拥有一个地址，这个地址代表变量在内存中的位置。Go语言中使用在变量名前面添加`&`操作符(前缀)来获取变量的内存地址(取地址操作)

```
ptr := &v // v的类型为T
```

其中v代表被取地址的变量，变量v的地址使用变量ptr进行接收，ptr的类型为 `*T`, 称做T的指针类型，`*`代表指针。

变量、指针和地址三者的关系是，每个变量都拥有地址，指针的值就是地址。

#### 从指针获取指针指向的值

当使用`&`操作符对普通变量进行取地址操作并得到变量的指针后，可以对指针使用`*`操作符，也就是指针取值

```go
func demo_1302()  {
	fmt.Println("============demo_1302============")
	// 准备一个字符串类型
	var house = "Malibu Point 10880, 90265"

	// 对字符串取地址，ptr类型为*string
	ptr := &house

	// 打印ptr的指针地址
	fmt.Printf("ptr type : %T\n", ptr)

	// 打印ptr的指针地址
	fmt.Printf("address: %p\n", ptr)

	// 对指针进行取值操作
	value := *ptr

	// 取值后的类型
	fmt.Printf("value type: %T\n", value)

	// 指针取值后就是指向变量的值
	fmt.Printf("value: %s\n", value)
}
```

取地址操作符`&`和取值操作符`*`是一对互补操作符，`&`取出地址，`*`根据地址取出地址指向的值。

变量、指针地址、指针变量、取地址、取值的相互关系和特性如下:

- 对变量进行取地址操作使用`&`操作符，可以获得这个变量的指针变量
- 指针变量的值是指针地址
- 对指针变量进行取值操作使用`*`操作符，可以获得指针变量指向的原变量的值。

#### 使用指针修改值

```go
func demo_1303() {
	fmt.Println("============demo_1302============")
	x, y := 1, 2

	// 交换变量值
	swap(&x, &y)

	// 输出变量值
	fmt.Println(x, y)
}

func swap(a, b *int)  {
	// 取a指针的值，赋给临时变量t
	t := *a

	// 取b指针的值，赋给a指针指向的值
	*a = *b

	// 将a指针的值赋给b指针指向的变量
	*b = t
}
```

#### 使用指针变量获取命令行的输入信息

```go
var mode = flag.String("mode", "", "process mode")
func demo_1304()  {
	fmt.Println("============demo_1304============")
	// 解析命令行参数
	flag.Parse()

	// 输出命令行参数
	fmt.Println(*mode)

}

```




#### 创建指针的另一种方法--new()函数

new() 函数可以创建一个对应类型的指针，创建过程会分配内存，被创建的指针指向默认值。

```go
func demo_1305()  {
	fmt.Println("============demo_1305============")

	str := new(string)
	*str = "Go语言教程"

	fmt.Println(*str)

}
```

new() 函数可以创建一个对应类型的指针，创建过程会分配内存，被创建的指针指向默认值

### 1.14 Go语言变量的生命周期

变量的生命周期与变量的作用域有着不可分割的联系:

- 全局变量: 它的生命周期和整个程序的运行周期是一致的；
- 局部变量: 它的生命周期则是动态的，从创建这个变量的声明语句开始，到这个变量不再被引用为止；
- 形式参数和函数返回值：它们都属于局部变量，在函数被调用的时候创建，函数调用结束后被销毁。

```go
```



栈和堆的区别:

- 堆(heap): 堆是用于存放进行执行中被动态分配的内存段。它的大小并不固定，可动态扩张或缩减。

### Go语言逃逸分析

### 1.15 Go语言常量

Go语言中的常量使用关键字 const 定义，用于存储不会改变的数据，常量是在编译时被创建的，即时定义在函数内部也是如此，并且只能是布尔性、数字型(整数型、浮点型和复数) 和字符串型。

```
const name [type] = value
```

在Go语言中，你可以省略类型说明符 [type]，因为编译器可以根据变量的值来推断其类型。

- 显式类型定义： const b string = "abc"
- 隐式类型定义： const b = "abc"

```go
func demo_1401()  {	const (		e  = 2.7182818		pi = 3.1415926	)		fmt.Println(e, pi)}
```



#### iota常量生成器

常量声明可以使用 iota 常量生成器初始化，它用于生成一组以相似规则初始化的常量，但是不用每行都写一遍初始化表达式。在一个 const 声明语句中，在第一个声明的常量所在的行，iota 将会被置为 0，然后在每一个有常量声明的行加一。

```go
func demo_1402()  {	type Weekday int	const (		Sunday Weekday = iota		Monday		Tuesday		Wednesday		Thursday		Friday		Saturday	)	fmt.Println(Monday)}
```



#### 无类型常量

Go语言的常量有个不同寻常之处，虽然一个常量可以有任意个确定的基础类型，例如 int 或 float64， 或者是类似 time.Duration 这样的基础类型，但是许多常量并没有明确的基础类型。

```go
func demo_1403()  {	var x1 float32 = math.Pi	var y1 float64 = math.Pi	var z1 complex128 = math.Pi	fmt.Println(x1, y1, z1)	const Pi64 float64 = math.Pi	var x2 float32 = float32(Pi64)	var y2 float64 = Pi64	var z2 complex128 = complex128(Pi64)	fmt.Println(x2, y2, z2)}
```



编译器为这些没有明确的基础类型的数字常量提供比基础类型更高精度的算术运算，可以认为至少有 256bit 的运算精度。这里有六种未明确类型的常量类型，分别是无类型的布尔型、无类型的整数、无类型的字符、无类型的浮点数、无类型的复数、无类型的字符串。

### 1.16 Go语言类型别名

### 1.17 Go语言注释的定义及使用

```go
// 单行注释/*	块注释*/
```

### 1.18 Go语言关键字与标识符

#### 关键字

关键字即是被Go语言赋予了特殊含义的单词，也可以称为保留字。

Go语言中的关键字一共有25个:

| break    | default     | func   | interface | select |
| -------- | ----------- | ------ | --------- | ------ |
| case     | defer       | go     | map       | struct |
| chan     | else        | goto   | package   | switch |
| const    | fallthrough | if     | range     | type   |
| continue | for         | import | return    | var    |

#### 标识符

标识符是指Go语言对各种变量、方法、函数等命名时使用的字符序列，标识符由若干字母、下划线`_`、和数字组成，且第一个字符必须是字母。

标识符的命名需要遵守以下规则：

- 由 26 个英文字母、0~9、`_`组成；
- 不能以数字开头，例如 var 1num int 是错误的；
- Go语言中严格区分大小写；
- 标识符不能包含空格；
- 不能以系统保留关键字作为标识符，比如 break，if 等等。

命名标识符时还需要注意以下几点：

- 标识符的命名要尽量采取简短且有意义；
- 不能和标准库中的包名重复；
- 为变量、函数、常量命名时采用驼峰命名法，例如 stuName、getVal；

在Go语言中还存在着一些特殊的标识符，叫做预定义标识符，如下表所示：

| append | bool    | byte    | cap     | close  | complex | complex64 | complex128 | uint16  |
| ------ | ------- | ------- | ------- | ------ | ------- | --------- | ---------- | ------- |
| copy   | false   | float32 | float64 | imag   | int     | int8      | int16      | uint32  |
| int32  | int64   | iota    | len     | make   | new     | nil       | panic      | uint64  |
| print  | println | real    | recover | string | true    | uint      | uint8      | uintptr |