# golang语言基础



## 数据类型



### 内置类型

#### 1、int整型



```go
func main() {
	//定义十进制，转2/8/16进制
  //%d=十进制，%b=二进制，%o=八进制，%x=十六进制
	var a int = 10
	fmt.Printf("%d \n",a)
	fmt.Printf("%b \n",a)
	fmt.Printf("%o \n",a)
	fmt.Printf("%x \n",a)
	//定义2进制,0b开头
	b := 0b10000000
	fmt.Printf("%d \n",b)
	fmt.Printf("%b \n",b)
	fmt.Printf("%o \n",b)
	fmt.Printf("%x \n",b)
	//定义8进制,0开头
	c := 010
	fmt.Printf("%d \n",c)
	fmt.Printf("%b \n",c)
	fmt.Printf("%o \n",c)
	fmt.Printf("%x \n",c)
	//定义16进制,0x开头
	d := 0x10
	fmt.Printf("%d \n",d)
	fmt.Printf("%b \n",d)
	fmt.Printf("%o \n",d)
	fmt.Printf("%x \n",d)
}
```



#### 2、浮点数



float32/float64

```go
func main() {
	//math.MaxFloat32
	//定义float64位的浮点数
	a := 1.23432
	fmt.Printf("%T \n",a)//查看数据类型type
	//定义float32的浮点数
	b := float32(1.23432)
	fmt.Printf("%T \n",b)
}

```



#### 3、布尔值

​	bool

#### 4、字符串



go语言中的字符串是用双引号包裹的，跟java一样。

go语言中单引号包裹的是字符。

```go
//字符串
s := "hello world"
//字符
s := 'a'
s := '1'
s := '字'
//字节
```

```go
func main() {
	path := "D:\\a\\b\\c"
	path1 := "'D:\\a\\b\\c'"
	path2 := "\"D:\\a\\b\\c\""
	macPath := "/Users/x/go/src/study/day01"
	fmt.Printf("%s \n",path)
	fmt.Printf("%s \n",path1)
	fmt.Printf("%s \n",path2)
	fmt.Println(macPath)
	//多行的字符串
	s1 := `测	
测试2
2让`
	fmt.Println(s1)
	//打印长度，一个字符串中汉字长度为3，数字为1，回车为1，空格为1，tab为1
	fmt.Println(len(s1))

	//使用Sprintf拼接字符串
	a1 := "hello"
	a2 := " world"
	a3 := fmt.Sprintf("%s%s",a1,a2)
	fmt.Println(a3)

	//分割字符串,例子按/分割字符串
	p := strings.Split(macPath,"/")
	fmt.Println(p)
	//包含=>strings.Contains，返回bool
	fmt.Println(strings.Contains(macPath,"go"))
	fmt.Println(strings.Contains(macPath,"go1"))
	//前缀
	fmt.Println(strings.HasPrefix(a3,"hello"))
	//后缀
	fmt.Println(strings.HasSuffix(a3,"world"))
	//index,字符第一次出现的位置索引
	fmt.Println(strings.Index(a3,"l"))
	//LastIndex,字符最后一次出现的索引
	fmt.Println(strings.LastIndex(a3,"l"))
	//拼接,用-把数组拼接起来
	fmt.Println(strings.Join(p,"-"))
  //查询出现次数
  fmt.Println(strings.Count(a1,"l"))
}

```



#### 5、fmt占位符



```go
//fmt占位符
func main() {
	var n = 100
	var s = "hello"
	var m = "100"
	fmt.Printf("%T \n", n)  //查看类型
	fmt.Printf("%v \n", n)  //查看值
	fmt.Printf("%#v \n", m) //查看值,能看出是字符串还是int
	fmt.Printf("%s \n", s)  //查看字符串
}
//输出结果
int 
100 
"100" 
hello 
```

\n:换行

\t:横向/水平制表符，相当于按了tab键

\v:纵向/垂直制表符，不常用,它的作用是让‘\v’后面的字符从下一行开始输出,且开始的列数为“\v”前一个字符所在列后面一列.

\r:回车符，暂时不知道作用在哪

\f:换页符

%p:查看地址值

%v:查看值

%T:查看类型

### 引用类型

### 结构类型(结构体)

Go没有类，

个人理解：go的结构体相当于类，可以为结构体定义方法，在函数中func-方法名之间增加接收者，函数就变成了方法。就相当于把函数给到了某个结构体，然后结构体.方法()就能直接调用方法了。



## 流程控制



### 1、if else



```go
func main() {
	age := 18
	if age >= 18 {
		fmt.Println("允许上网")
	}else {
		fmt.Println("未成年人禁止上网")
	}
}
```



### 2、for



```go
func main(){
	for i := 0; i<10; i++ {
		fmt.Println("i:" ,i)
	}

  //下面这种声明变量的方式，变量的作用域不一样，可以在for循环外部打印出来,上面的不行。
	m := 0
	for ; m<10; m++ {
		fmt.Println("m:" ,m)
	}
	fmt.Println(m)//m=10

	//for range
	s := "hello world"
	for a,b := range s {
    //%c=>将字符正常显示，否则会显示ASCII码
    //a为索引，b为值
		fmt.Printf("%d %c\n",a,b)
	}
}
```

```go
//练习，打印九九乘法表
func main() {
	for i := 1; i<=9; i++{
		for j := 1; j<=i; j++{
			//fmt.Print(i, "*", j, " = ", i*j, "  ")
			fmt.Printf("%v * %v = %v\t",i,j,i*j)
		}
		fmt.Printf("\n")
	}
}

```



### 3、switch&goto



##### break

​	直接跳出循环

##### continue

​	跳出此次循环，继续下个循环

示例：

```go
func main() {
	for i := 0; i<10; i++ {
		if i == 5 {
			break
		}
		fmt.Println(i)
	}
	//结果：
	//0
	//1
	//2
	//3
	//4

	for i := 0; i<10; i++ {
		if i == 5 {
			continue
		}
		fmt.Println(i)
	}
	//结果：
	//0
	//1
	//2
	//3
	//4
	//6
	//7
	//8
	//9

}
```

##### switch

```go
func main() {
	var n = 0
	switch n{
	case 1,3,5,7,9:
		fmt.Println("奇数")
	case 2,4,6,8,10:
		fmt.Println("偶数")
	default:
		fmt.Println("test")
	}
}
```

了解就行：

Fall through:向下兼容

goto：跳到指定的label标签

Continue/break也能跳到指定的标签



## 运算符



#### 位运算符

​	&:按位与

​	|:按位或

​	^:按位异或

​	<<:二进制左移

​	>>:二进制右移

#### 赋值运算符

1. 
2. 

## 数组、切片、映射



### 1、数组Array

​	存放元素的容器，必须指定存放的元素的类型和容量，查询快，存储慢

#### 声明/初始化数组

​	int初始化值为0，字符串初始化值为""，bool初始化为false

```go
func main() {
	//声明一个数组
	//var 数组名 [长度]存储的元素的数据类型
	var a [3]int
	a1 := [5]int{1,2,3,4,6}
  //用...根据实际长度来定义长度
	a2 := [...]int{1,2,3,4,5,6,7,3,2}
  //根据索引进行初始化
	a3 := [6]int{0: 1,3: 4}
	fmt.Println(a)
	fmt.Println(a1)
	fmt.Println(a2)
	fmt.Println(a3)
	/*[0 0 0]
	[1 2 3 4 6]
	[1 2 3 4 5 6 7 3 2]
	[1 0 0 4 0 0]*/
}
```

#### 遍历数组

1. 根据索引遍历普通for循环

   ```go
   func main(){
   	citys := [...]string{"深圳","惠州","东莞"}
   	for i := 0; i < len(citys); i++{
   		fmt.Println(citys[i])
   	}
   }
   ```

2. for range

   ```go
   func main(){
   	citys := [...]string{"深圳","惠州","东莞"}
   	for _,v := range citys{
   		fmt.Println(v)
   	}
   }
   ```

#### 多维数组

#### 练习



```go
func main() {
	nums := [...]int{1,3,5,7,8}
	//sum := 0
	//for _,v := range nums {
	//	sum = sum +v
	//}
	//for i := 0; i<len(nums); i++ {
	//	sum = sum + nums[i]
	//}
	//fmt.Println(sum)

	//计算数组中和为8的两个值的索引
	for n := 0; n < len(nums) -1; n++ {
		for m := n+1; m < len(nums); m++ {
			fmt.Println(m)
			sum := nums[n] + nums[m]
			if sum == 8 {
				fmt.Printf("(%v,%v) \n",n,m)
			}
		}
	}
}
```



### 2、切片

#### 创建和初始化切片

切片在初始化的时候就会创建一个数组和一个关联切片

##### 常规方法

数组有缺点，不能增加长度，此时就需要用到切片了。

切片是数组元素提供动态大小的、灵活的视角。在实践中，切片比数组更常用。

类型 `[]T` 表示一个元素类型为 `T` 的切片。

切片有3个字段的数据结构：

1. 指向底层数组的指针
2. 切片访问的元素的个数（长度）
3. 切片允许增长到的元素个数（容量）。容量必须大于或等于长度

用len(切片)查看长度，用cap(切片)查看容量

切片截取的值

1. s3 := s1[1,4] 此时就是取的就是数组中索引为1，2，3的值，不包含索引4
2. s3 := s1[1:] 此时就是取的数组中索引1到最后一个元素的值。
3. 底层数组的值发生改变时，切片的值也会发生改变



```go
func main() {
	//声明切片
	var s1 []int
	var s2 []string
	fmt.Println(s1,s2)
	s1 = []int{1,2,3,4,5,6,7,8,9,10}
	s2 = []string{"深圳","东莞","惠州"}
	fmt.Println(s1,s2)
  //切片的容量是指底层数组的容量，也就是从切片的第一个元素开始算，到最后的元素的数量
  //s3的底层数组是s1，s4的底层数组是s3
	s3 := s1[3:]
	s4 := s3[3:]
  s5 := s1[1:5] //容量为9
	fmt.Println(s3)//[4 5 6 7 8 9 10]
	fmt.Println(len(s3),cap(s3))//7 7
	fmt.Println(s4)//[7 8 9 10]
	fmt.Println(len(s4),cap(s4))//4 4
  fmt.Println(s5)
	fmt.Println(len(s5),cap(s5))//1 9
  //当底层数组中的值发生变化时，切片的值也会发生改变
	s1[9] = 6
	fmt.Println(s3)//[4 5 6 7 8 9 6]
	fmt.Println(len(s3),cap(s3))
	fmt.Println(s4)//[7 8 9 6]
	fmt.Println(len(s4),cap(s4))
}
```

##### 用make创建和初始化



```go
func main() {
	//只传一个参数，长度/容量都为5
	s1 := make([]int,5)
	fmt.Println(s1,len(s1),cap(s1))//[0 0 0 0 0] 5 5
	//传2个参数，长度为5，容量为10
	s2 := make([]string,5,10)
	fmt.Println(s2,len(s2),cap(s2))//[    ] 5 10
}
```

#### 使用切片（append/copy）

##### 1、append

```go
func main() {
	s1 := []string{"北京","上海","深圳","上海","深圳"}//长度5，容量5
	s1 = append(s1, "测试1")
	s1 = append(s1, "测试2")
	s1 = append(s1, "测试3")
	s1 = append(s1, "测试4")
	s1 = append(s1, "测试5")//此时容量10
  //当使用append时，原底层数组长度不够，则会创建一个新的数组，长度为原底层数组两倍
	s1 = append(s1, "测试6")//此时容量20
  s2 := []string{"东莞","惠州","南昌","东莞","惠州","南昌","东莞","惠州","南昌","东莞","惠州","南昌"}
  //将s2添加进s1
  s1 = append(s1, s2...)//此时长度23，容量40
  s1 = append(s1, s2...)//再加一次，长度35，容量40
	fmt.Println(s1,len(s1),cap(s1))
}

```

注意：经测试，如果新增后的长度超了翻倍的容量，容量只翻倍一次。比如原本底层数组长度为10，现在往切片增加11元素，此时长度变成21，21>10*2，此时切片容量为21，容量不会翻倍2次。（不知道是bug还是特性就这样）

##### 2、copy

#### 切片的本质

切片就是一个框，框住了一块连续的内存,属于饮用类型，真正的数据都是保存在底层数组里面的。

##### 3、删除切片中的元素

删除第index个，就s1 = append(s1[:index],s1[index+1:]),在内存中的地址是不变的,删一个，长度减1，容量不变，后面的值往前面移动，最后一个值

底层数组的值也会被删除，长度不变，最后一个值会变成跟前面一位索引一样的值

```go
func main() {
	s := [...]string{"北京","上海","深圳","上海","东莞"}
	s1 := s[:]
	fmt.Printf("%p \n",&s1[1])//0xc00005c060
	s1 = append(s1[:1], s1[2:]...)
	fmt.Printf("%p 值：%v \n",&s1[1],s1)//0xc00005c060
  fmt.Printf("%p %v %v \n",&s[1],s[1],s) //[北京 深圳 上海 东莞 东莞] 

}

```



### 3、映射（map）

map是一种无序的基于`key-value`的数据结构，go语言的map是引用类型，必须初始化才能使用。



### 4、指针

&：根据值查看地址值

*：根据地址值查看值

```go
func main() {
	p1 := "测试"
	fmt.Printf("%p \n",&p1)
	fmt.Printf("%v \n",&p1)
	p2 := &p1
	fmt.Printf("%v",p2)
}
```

new函数申请一个内存地址

## 函数

常用格式如下：

```go
func 函数名(参数) (返回值){
	函数体
}
```

1. 函数说一段代码的封装
2. 把一段逻辑抽象出来封装到一个函数中，给它个名字，每次用到它的时候，直接用函数名调用即可
3. 使用函数能够让代码结构更清晰，更简洁
4. 如果返回值命名了，则return后面可以省略

几种声明函数的方式

### 匿名函数

一般在函数内部定义函数时才需要用到匿名函数。

### 闭包（closure）

闭包是一个函数值，正常情况，函数能使用全局变量（外部），跟局部变量（内部），但是外部无法使用函数内定义的变量，

```go
//外部
var i int

func test() {
  //内部
  //a无法在外部使用
  var a int
}
```



```go
//b相对于a，a是外部，b是内部。b相对于c。b是外部，c的内部
//a
//全局变量
var i int

func test() func() int{
  //b
  //a无法在外部使用
  a := 111
  //将函数当参数返回时，外部就能访问到c了
  return func test1() int{
    //c
    c := 12//b里面无法使用c
    return c
  }
}

```



#### 斐波纳契闭包

```go
package main

import "fmt"

// 返回一个“返回int的函数”
func fibonacci() func() int {
	s1,s2 := -1,1
	
	return func() int{
		sum := s1+s2
		s1,s2 = s2,sum
		return sum
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
    //通过闭包得到sum的值
		fmt.Println(f())
	}
}
//0 1 1 2 3 5 8 13 21 34
```



## 方法

func和函数名之间的参数被称为**接收者**，如果一个函数有接收者，则这个函数被称为**方法**。

接收者的类型定义和方法声明必须在同一个包内。



## 面向对象编程

结构体名称及其字段/属性大小写区分，大写开头则表示其他包可以使用，小写只能本包使用

```go
//入门案例

//定义一个Cat的结构体
type Cat struct{
  //定义字段 结构体字段 = 属性 = filed，叫法不同而已
	Name string
	Age int
	Color string
}

func main() {
	var cat1 Cat
	fmt.Println(cat1)
	cat1.Name = "果果"
	cat1.Age = 1
	cat1.Color = "银渐层"
	fmt.Println(cat1)
}
```

结构体变量（实例）在内存的布局

以上面那个cat1为例子

结构体变量是值类型。

结构体中字段为切片、map时，不能直接赋值，必须使用make关键字开辟内存空间，才能赋值。

```go
type Person struct{
	name string
	age int
	source [10]string
  point *int //需要用new创建内存空间
	slice []string
	grade map[string]int
}
func main() {
	var person Person
	person.source[0] = "12"

	person.slice = make([]string,10)
	person.slice[0] = "ce"

	person.grade = make(map[string]int)
	person.grade["语文"] = 100
	fmt.Println(person)
}
```



struct类型的内存分配机制



结构体使用的细节

```go
type Point struct{
	x,y int
}
type Rectangle struct{
	left,right Point
}

func main() {
	var r1 = Rectangle{Point{0,3},Point{3,3}}
	//r1中的4个int变量在内存中地址是连续的，int64每个都占8个字节
	fmt.Println(&r1.left.x)
	fmt.Println(&r1.left.y)
	fmt.Println(&r1.right.x)
	fmt.Println(&r1.right.y)
}
```

2、部分用户自定义数据类型转换可以转，但必须强转。



### 三大特性（封装、继承、多态）

#### 封装：

​	就是把抽象的字段和对字段的操作封装在一起，数据被保护在内部，程序的其他包只有痛过被授权的操作（方法），才能对字段进行操作。

​	1、将结构体、字段的首字母小写（不能到处访问了，其他包也不能使用，类似private）

​	2、给结构体所在的包提供一个工厂模式的函数，首字母大写，类似一个构造函数

​	3、提供一个首字母大写的Set方法，对属性进行判断并赋值

​	4、提供一个首字母大写的Get方法，用于获取属性的值

#### 继承：

​	

## 接口

### 什么是interface

​	interface是一组method签名的集合，我们通过interface来定义对象的一组行为。

如果某个对象中实现了某个interface中所有的方法，则表示该对象实现了此接口

### interface类型

### 空interface

空interface(interface{})不包含任何的method，正因为如此，所有的类型都实现了空interface。空interface对于描述起不到任何的作用(因为它不包含任何的method），但是空interface在我们需要存储任意类型的数值的时候相当有用，因为它可以存储任意类型的数值。它有点类似于C语言的void*类型。

```go
// 定义a为空接口
var a interface{}
var i int = 5
s := "Hello world"
// a可以存储任意类型的数值
a = i
a = s
```

一个函数把**interface{}**作为参数，那么他可以接受任意类型的值作为参数，如果一个函数返回**interface{}**,那么也就可以返回任意类型的值。

### interface值

​	interface也是一种数据类型，它可以用来接收实现了该接口的对象/变量

### interface函数参数

​	interface的变量可以持有任意实现该interface类型的对象

### interface变量存储的类型

### 嵌入interface

### 反射

## 并发

## 包结构

## 反射

## 测试





