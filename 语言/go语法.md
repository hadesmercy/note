#Go 语言

##  IDE运行相关问题

###1. 运行的不同方法

* 下面给出官网的goland文档

  > - Run kind: a building scope for your application. File and Package scopes work similarly in tests and compilation/running configurations (in terms of the scope they cover).
  >
  >   - Directory: build an application in the specified directory as a package, without processing any subdirectories.
  >
  >     For test configurations, GoLand runs all the tests in the specified directory and all its subdirectories.
  >
  >   - File: build an application from files specified in the Files field. To pass multiple file paths, use the vertical bar () as a delimiter. This configuration is automatically selected when you run your program from scratch files.`|`
  >
  >   - Package: build a single package with all its dependencies. Specify a full import path to the package that you want to build in the Package path field (for example, ). This configuration is automatically selected when you run the function or a separate test by using the Run icon  in the gutter.`github.com/gorilla/mux``main`
  >
  >   - 官方文档地址：https://www.jetbrains.com/help/go/running-applications.html#create-go-build-configuration   

* Directory 目录，编译指定目录下的go语言，并且忽略子目录（演示）
* File，编译指定文件，可以使用|来添加多个目录
* Package，编译指定路径下的包，包括该包所有的依赖项
* 需要特别注意的是，在构建测试的时候，Directory也会测试子目录下的所有测试

### 2.测试功能

* 使用 go test -v 命令进行测试

demo.go：

```go
package demo

// 根据长宽获取面积
func GetArea(weight int, height int) int {
    return weight * height
}
```

 demo_test.go：

```go
package demo
import "testing"
func TestGetArea(t *testing.T) {
    area := GetArea(40, 50)
    if area != 2000 {
        t.Error("测试失败")
    }
}
```

* 使用 go test -bench = "."进行压力测试

## 基本语法

### 1. 变量

   * 定义变量

     ```go
     var a int = 10
     或使用简短声明格式
     a := 10
     编译器会自动推导类型
     ```
   
   * 多变量定义
   
     ```go
     var a int = 10
     var b int = 20
     a,b = b,a
     ```
   
   * 匿名变量
   
     ```go
     func tset()(int,int){
         return a,b
     }
     c,_ = test()
     ```

### 2. 流程控制

   * if语句

     ```go
     var ten int = 11
     if ten > 10 {
         fmt.Println(">10")
     } else {
         fmt.Println("<=10")
     }//多分支表达式
     
     if err := Connect(); err != nil {
         fmt.Println(err)
         return
     }//可以在if后添加一个执行语句
     
     ```

   * 循环
   
     * 只有for循环，且在语法上与一般的c语言不同，for i := 0; i < 10; i++ 
     
     * 同样的 声明的变量 i也只在for的作用域中可见
     
     * 并且可以使用for加条件当while使用
     
     ```go
     for j := 0; j < 5; j++ {
         for i := 0; i < 10; i++ {
             if i > 5 {
                 break JLoop
             }
             fmt.Println(i)
         }
     }
     
     ```
   
     * for range 可以遍历数组、切片、字符串、map 及channel，for range 语法上类似于其它语言中的 foreach 语句
     
       ```go
       for key, value := range []int{1, 2, 3, 4} {
           fmt.Printf("key:%d  value:%d\n", key, value)
       }
       ```
     
     * 也可以使用方式遍历得到字符串
     
       ```go
       var str = "hello 你好"
       for key, value := range str {
           fmt.Printf("key:%d value:0x%x\n", key, value)
       }//value，实际类型是 rune 类型，以十六进制打印出来就是字符的编码。
       ```
     
   * Switch
     * 与c语言类似，但默认在每个case后添加break
     
     ```go
     var a = "hello"
     switch a {
     case "hello":
         fmt.Println(1)
     case "world":
         fmt.Println(2)
     default:
         fmt.Println(0)
     }
     ```
     
     * 可以使用逻辑表达式作为索引
     
     ```go
       var r int = 11
       switch {
       case r > 10 && r < 20:
           fmt.Println(r)
       }
     ```
     
     * 利用switch实现类型判断
     
     ```go
     switch inst:=a.(type){
      	case TypeA:
         	inst.MethodA()
         default:
             fmt.Println("unknow")
           }    
     ```
     
   * defer语句
   
     * 利用该语句，实现延迟执行，执行结果为c，b，a
     
     ```
     defer a
     defar b
     c
     ```

## 数据结构

### 1.布尔、浮点、整型、复数、结构体

   * 逻辑值

     ```go
     var aVar = 10
     aVar == 5  // false
     aVar == 10 // true
     aVar != 5  // true
     aVar != 10 // false
     ```
     
   * 浮点

     ```go
     var a float32
     ```

   * 整型

     * 有符号整型:int8、int16、int32、int64、int 
     * 无符号整型:unit8、uint16、unit32、uint64、unit

     ```go
     var a int8 //声明有符号8位整数 
     var b uint8 //声明无符号8位整数
     ```

   * 复数

     ```go
     var x complex128 = complex(1, 2) // 1+2i
     var y complex128 = complex(3, 4) // 3+4i
     fmt.Println(x*y)                 // "(-5+10i)"
     fmt.Println(real(x*y))           // "-5"
     fmt.Println(imag(x*y))           // "10"
     ```

   * 结构体

     * 可以使用.直接访问结构体指针内的元素

     ```go
     type Point struct {
         X int
         Y int
     }
     
     var p Point
     p.X = 10
     p.Y = 20
     
     type Player struct{
         Name string
         HealthPoint int
         MagicPoint int
     }
     
     tank := new(Player)
     tank.Name = "Canon"
     tank.HealthPoint = 300
     ```

     

### 2.字符与字符串

   * 字符
     * 一种是 uint8 类型，或者叫 byte 型，代表了 ASCII 码的一个字符。
     
     * 另一种是 rune 类型，代表一个 UTF-8 字符，当需要处理中文、日文或者其他复合字符时，则需要用到 rune 类型。rune 类型等价于 int32 类型。

     ```go
     var ch int = '\u0041'
     var ch2 int = '\u03B2'
     var ch3 int = '\U00101234'
     fmt.Printf("%d - %d - %d\n", ch, ch2, ch3) // integer
     fmt.Printf("%c - %c - %c\n", ch, ch2, ch3) // character
     fmt.Printf("%X - %X - %X\n", ch, ch2, ch3) // UTF-8 bytes
     fmt.Printf("%U - %U - %U", ch, ch2, ch3)   // UTF-8 code point
     ```


   * 数组
     * 数组是一个由固定长度的特定类型元素组成的序列，一个数组可以由零个或多个元素组成。但是数组的长度是固定的	
       
      ```go
      var a [3]int             // 定义三个整数的数组
      fmt.Println(a[0])        // 打印第一个元素
      fmt.Println(a[len(a)-1]) // 打印最后一个元素
      
      
      for i, v := range a {
          fmt.Printf("%d %d\n", i, v)
      }
      
      
      for _, v := range a {
          fmt.Printf("%d\n", v)
      }
      ```
     
      
   ### 3.切片
​    切片是对数组的一个连续片段的引用，所以切片是一个引用类型

 ```go
 var a  = [3]int{1, 2, 3}
 fmt.Println(a, a[1:2])
 ```

 * 取出的元素数量为：结束位置 - 开始位置；

 * 取出元素不包含结束位置对应的索引，切片最后一个元素使用 slice[len(slice)] 获取；

 * 当缺省开始位置时，表示从连续区域开头到结束位置；

 * 当缺省结束位置时，表示从开始位置到整个连续区域末尾；

 * 两者同时缺省时，与切片本身等效；

 * 两者同时为 0 时，等效于空切片，一般用于切片复位。

 * 以下为所举的实例

   ```go
   var highRiseBuilding [30]int
   
   for i := 0; i < 30; i++ {
           highRiseBuilding[i] = i + 1
   }
   // 区间
   fmt.Println(highRiseBuilding[10:15])
   // 中间到尾部的所有元素
   fmt.Println(highRiseBuilding[20:])
   // 开头到中间指定位置的所有元素
   fmt.Println(highRiseBuilding[:2])
         [11 12 13 14 15]
          [21 22 23 24 25 26 27 28 29 30]
          [1 2]
          
          // 声明字符串切片
          var strList []string
          
          // 声明整型切片
          var numList []int
          
        // 声明一个空切片
       var numListEmpty = []int{}
          
       // 输出3个切片
       fmt.Println(strList, numList, numListEmpty)
      // 输出3个切片大小
      fmt.Println(len(strList), len(numList), len(numListEmpty))
   
      // 切片判定空的结果
      fmt.Println(strList == nil)
      fmt.Println(numList == nil)
      fmt.Println(numListEmpty == nil)
   
      [] [] []
      0 0 0
      true
      true
      false 




 * make函数

   ```go
   a := make([]int, 2)
   b := make([]int, 2, 10)
   
   fmt.Println(a, b)
   fmt.Println(len(a), len(b))

### 4.map类型

* 一种元素对（pair）的无序集合，pair 对应一个 key（索引）和一个 value（值）

  ```go
  
  func main() {
      var mapLit map[string]int
      var mapAssigned map[string]int
      mapLit = map[string]int{"one": 1, "two": 2}
      mapCreated := make(map[string]float32)
      mapAssigned = mapLit
      mapCreated["key1"] = 4.5
      mapCreated["key2"] = 3.14159
      mapAssigned["two"] = 3
      fmt.Printf("Map literal at \"one\" is: %d\n", mapLit["one"])
      fmt.Printf("Map created at \"key2\" is: %f\n", mapCreated["key2"])
      fmt.Printf("Map assigned at \"two\" is: %d\n", mapLit["two"])
      fmt.Printf("Map literal at \"ten\" is: %d\n", mapLit["ten"])
  }
  ```

### 5.常量

####  iota常量生成器

* 在编译期计算

  ```go
  const (
  	Zero   = iota      // 0
  	First              // 1
  	Second             // 2
  	Hi     = 0         // 0, 被打断后，后续值不变，直到用iota显示恢复
  	Four               // 0
  	Five               // 0
  	Six    = iota      // 6，显示恢复，iota接着累加，中间打断不中断累加
  	Seven              // 7
  	Eight  = iota * 10 // 80，iota不变，变更常量表达式，后续保持表达式
  	Nine               // 90
  )
  
  const (
  	TenZero   = iota * 10 // 0，表达式可以为各种go支持的计算表达式
  	TenFirst              // 10
  	TenSecond             // 20
  )
  ```

  

  





## 函数

### 1.普通函数

* 标准定义如下

  ```go
  func hypot(x, y float64) float64 {
      return math.Sqrt(x*x + y*y)
  }
  fmt.Println(hypot(3,4)) // "5"
  ```

* 函数可以有多个返回值，可以使用_选择使用该返回值

  ```go
  func hypot(x, y float64) float64 {
      return x + y,x - y
  }
  a,_ = hypot(3,4)
  _,b = hypot(3,4)
  ```

### 2.匿名函数

* 可以理解为没有名字的普通函数

* 可以在定义时调用该函数

  ```go
  func(data int){
      fmt.Println("hello",data)
  }(100)
  ```

* 可以将该函数赋值给变量

  ```go
  f := func(data int){
      fmt.Println("hello",data)
  }
  f(100)
  ```



  

### 3.方法



### 4.闭包



### 5.递归





## 包管理

### 1.导入



## 正则表达式

* 一种用来匹配字符串的表达式
### 1.包含字符
  字母、数字、下划线

### 2.转义字符

| 转义字符 | 描述   |
| -------- | ------ |
| \\\      | 反斜杠 |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |
|          |        |

### 3.原义字符串

使用反引号``引起来的字符不再转义

### 4.字符集

* 依次列出
* 以范围给出
* ^表示非该集合中的字符
* 将]和-放在字符集的第一个。若两个同时出现必须是“]”在前,”-”在后，且-后 边只能是字母。
* \^不要放在第一个，
* 若字符集中仅有\^则不能使用字符集而直接使用^。 [放在哪里都可以。

### 5.汉字匹配



## 常用包

### 1.strings包

### 2.striconv包



### 3.time包

![image-20220318173021756](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173021756.png)

![image-20220318173035011](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173035011.png)

![image-20220318173050610](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173050610.png)

![image-20220318173059435](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173059435.png)



### 4.math包

![image-20220318173137340](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173137340.png)

![image-20220318173145280](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173145280.png)

### 5.rand包

![image-20220318173656231](/Users/hadesmercy/Desktop/go/note/go语法.assets/image-20220318173656231.png)



## 并发

### 1. 进程/线程

* 进程为操作系统进行资源分配和调度的独立单位
* 线程为进程的一个执行实体，是CPU调度的一个独立单位
* 一个进程可以创建和撤销多个线程,同一个进程中的多个线程之间可以并发执行

### 2.Goroutine

* 一种轻量级并发的实现，是go语言实现并发的核心

* 可以理解为线程，但是在底层实现上十几个Goroutine可能只有几个线程，并且go语言实现了Goroutine的内存共享

  ```go
  package main
  
  import (
  	"fmt"
  	"time"
  )
  
  func running() {
  
  	var times int
  	// 构建一个无限循环
  	for {
  		times++
  		fmt.Println("tick", times)
  
  		// 延时1秒
  		time.Sleep(time.Second)
  	}
  
  }
  func running2() {
  
  	var times int
  	// 构建一个无限循环
  	for {
  		times++
  		fmt.Println("ticks", times)
  
  		// 延时1秒
  		time.Sleep(time.Second)
  	}
  
  }
  func main() {
  
  	// 并发执行程序
  	go running()
  	go running2()
  	// 接受命令行输入, 不做任何事情
  	var input string
  	fmt.Scanln(&input)
  }
  
  ```

  可以看到输出的顺序完全是随机的

  

### 3.并发通信

在引入channel之前，观察以下操作

* 在 10 个 goroutine 中共享了变量 counter。每个 goroutine 执行完成后，会将 counter 的值加 1。因为 10 个 goroutine 是并发执行的，所以我们还引入了锁，也就是代码中的 lock 变量。每次对 n 的操作，都要先将锁锁住，操作完成后，再将锁打开。

代码臃肿，复杂，由于锁的存在，导致进程之间通信十分麻烦，故go语言内提供了channel用来通信

```go
package main
import (
    "fmt"
    "runtime"
    "sync"
)
var counter int = 0
func Count(lock *sync.Mutex) {
    lock.Lock()
    counter++
    fmt.Println(counter)
    lock.Unlock()
}
func main() {
    lock := &sync.Mutex{}
    for i := 0; i < 10; i++ {
        go Count(lock)
    }
    for {
        lock.Lock()
        c := counter
        lock.Unlock()
        runtime.Gosched()
        if c >= 10 {
            break
        }
    }
}
```



### 4.sync包与锁

```go
package main
import (
    "fmt"
    "time"
)
func main() {
    var a = 0
    for i := 0; i < 1000; i++ {
        go func(idx int) {
            a += 1
            fmt.Println(a)
        }(i)
    }
    time.Sleep(time.Second)
}
```

  在该例子中，按照上面的顺序，有一个协程取得 a 的值为 3，然后执行加法运算，此时又有一个协程对 a 进行取值，得到的值同样是 3，最终两个协程的返回结果是相同的。

  而锁的概念就是，当一个协程正在处理 a 时将 a 锁定，其它协程需要等待该协程处理完成并将 a 解锁后才能再进行操作，也就是说同时处理 a 的协程只能有一个，从而避免上面示例中的情况出现。 

* 互斥锁

  问题怎么解决呢？加一个互斥锁 Mutex 就可以了。那什么是互斥锁呢 ？互斥锁中其有两个方法可以调用，如下所示：

```go
func (m *Mutex) Lock()
func (m *Mutex) Unlock()
```



```go
package main
import (
    "fmt"
    "sync"
    "time"
)
func main() {
    var a = 0
    var lock sync.Mutex
    for i := 0; i < 1000; i++ {
        go func(idx int) {
            lock.Lock()
            defer lock.Unlock()
            a += 1
            fmt.Printf("goroutine %d, a=%d\n", idx, a)
        }(i)
    }
    // 等待 1s 结束主程序
    // 确保所有协程执行完
    time.Sleep(time.Second)
}
```



### 5.并发通信通道chan

* 声明与创建

```go
var 通道变量 chan 通道类型
通道实例 := make(chan 数据类型)
ch1 := make(chan int)                 // 创建一个整型类型的通道
ch2 := make(chan interface{})         // 创建一个空接口类型的通道, 可以存放任意格式
type Equip struct{ /* 一些字段 */ }
ch2 := make(chan *Equip)// 创建Equip指针类型的通道, 可以存放*Equip
```



* 实际的例子

```go
ch := make(chan interface{})// 创建一个空接口通道
ch <- 0// 将0放入通道中
ch <- "hello"// 将hello字符串放入通道中
```



* 接受通道发送的信息

```go
data := <-ch // 阻塞，如果没有使用该变量，则会发生阻塞
data, ok := <-ch //非阻塞，ok表示是否接收到数据
<-ch //接受数据，并且忽略所接收到的数据，多用于在阻塞
```





## 面向对象

###  面向对象简介

* 属性与行为

* 结构体(struct)、方法(method) 、接口(interface）

### 结构体

```go
type Teacher struct{
    name string
    age int 
}
```

* 初始化方法如下

```go
type Player struct{
    Name string
    HealthPoint int
    MagicPoint int
}
tank := new(Player)
tank.Name = "Canon"
tank.HealthPoint = 300

var tank1
tank1.Name = "helo"
  
```

* 拷贝

  值类型的赋值是深拷贝，深拷贝为新对象分配了内存。

  引用类型的赋值是浅拷贝，浅拷贝仅是复制了对象的指针。

```go
type Player struct{
    Name string
    HealthPoint int
}

d1 := Player{
    "hello",
    110
}
d2 := d1//深拷贝
d3 := &d1 //浅拷贝
```

* 作为参数/返回值的两种形式

  * 值传递

  * 引用传递

* 匿名结构体

  * 即无需在定义结构体名字的情况下创建并使用的结构体



```go
a := struct{
    number1,number2 int
}{
    23,23
}
```
  * 匿名字段

    * 在结构体内部字段没有名字，则默认使用类型作为字段名
    
```go
a := struct{
     int
}{
    23
}
```

####   函数体嵌套

* 模拟聚合关系:一个类作为另一个类的属性

* 模拟继承关系:一个类作为另一个类的子类，实现子类和父类的关系

  ```go
  package main
  
  import "fmt"
  
  // 可飞行的
  type Flying struct{}
  
  func (f *Flying) Fly() {
      fmt.Println("can fly")
  }
  
  // 可行走的
  type Walkable struct{}
  
  func (f *Walkable) Walk() {
      fmt.Println("can calk")
  }
  
  // 人类
  type Human struct {
      Walkable // 人类能行走
  }
  
  // 鸟类
  type Bird struct {
      Walkable // 鸟类能行走
      Flying   // 鸟类能飞行
  }
  
  func main() {
  
      // 实例化鸟类
      b := new(Bird)
      fmt.Println("Bird: ")
      b.Fly()
      b.Walk()
  
      // 实例化人类
      h := new(Human)
      fmt.Println("Human: ")
      h.Walk()
  
  }
  ```
  
  

### 方法

* 函数(function)是一段具有独立功能的代码，可以被反复多次调用，从而实现代码 复用。而方法(method)是一个类的行为功能，只有该类的对象才能调用。

```go
func (e int) test(){
    //do something
}

```

  一段程序可以使用函数编写，但同时又 创建了方法，主要有以下两个原因: (1)Go不是一种纯粹的面向对象编程语言， 不支持类。因此创建方法旨在模拟类的行为。 (2)方法可以在不同类型上定义相同名称， 而函数却不允许有相同名称。



* 继承

  方法可以继承，如果**匿名字段**实现了一个方法，那么包含这个匿名字段的struct也能 调用匿名字段中的方法。

```go
type a struct{
    name,phone string
    age int
}

func (b *a) test(){
    fmt.Printf("%s,%d,%s",b.name,b.age,b phone)
}

type learn struct{
    a//匿名字段
    class string
}

func main(){
    s1 := {a{"xi","130939893893","17"},语文}
    s1.test()
}


```

* 方法重写

  按照就近原则

### 接口

* 一种类型
* 在面向对象语言中，接口用于定义对象的行为。接口只指定对象应该做什么，实现这 种行为的方式(实现细节)由对象决定。
* 利用接口实现多态
* **方法名：当方法名首字母是大写且这个接口类型名首字母也是大写时，这个方法可以被接口所在的包（package）之外的代码访问。**

```go
type Cat struct{}
func (c Cat) Say() {
	fmt.Println("喵喵喵~")
}

type Dog struct{}
func (d Dog) Say() {
	fmt.Println("汪汪汪~")
}

type Sayer interface {
	Say()
}

func loud(s Sayer) {
	s.Say()
}
func main() {
	a := Dog{}
	c := Cat{}
	loud(a)
	loud(c)
}
```

* 空接口
* 接口对象转型





## 文件

* 文件结构体

```go
type fileStat struct {
    name string
    size int64
    mode FileMode 
    modTime time.Time 
    sys syscall.Stat_t
}
```

* 文件接口，对应方法

```go
type FileInfo inteface {
    Name() string //文件基础名
    Size() int64 //常规文件的字节数，与系统有关 
    Mode() FileMode //文件的模式比特
    	ModTime() time.Time //修改时间
    IsDir() bool //是Mode().IsDir()的缩写
    Sys() interface{} //潜在的数据源，可以返回nil
}
```

* 文件路径


```go
filepath.IsAbs() //判断是否为绝对路径
filepath.Rel() //获取相对路径
filepath.Abs() //获取绝对路径
path.join() //拼接路径
```

* 创建目录

```go
os.Mkdir() //一层
os.MkdirAll() //多层目录
```

* 创建、打开、关闭文件

```go
os.OpenFile(filename, mode, perm)  //打开文件函数
//O_RDONLY 只读 O_WRONLY只写 O_RDWR读写 O_APPENDO_CREATE 不存在则创建
os.Create() //通过调用os.OpenFile() 来创建文件
os.Open() //通过调用os.OpenFile() 来打开文件
```



## 网络编程 

> https://www.cnblogs.com/aaronthon/p/10951929.html

### tcp socket编程

net/http包

服务端

* 服务端的处理流程

　　1）监听接口：8888

　　2）接收客户端的tcp链接，建立客户端和服务端的链接

　　3）创建goroutine，处理该链接的请求

```go
package main

import (
    "fmt"
    "net"
)

func process(conn net.Conn) {
    // 这里循环接收客户端发送的数据
    defer conn.Close()
    for {
        // 创建一个新切片
        buf := make([]byte, 1024)
        fmt.Printf("服务器在等待客户端%s 发送信息\n", conn.RemoteAddr().String())
        n, err := conn.Read(buf) // 从conn中读取
        if err != nil {
            fmt.Printf("客户端退出 err=%v\n", err)
            return
        }
        fmt.Print(string(buf[:n]))
    }
}

func main() {
    fmt.Println("服务器开始监听...")
    listen, err := net.Listen("tcp", "0.0.0.0:8888")
    if err != nil {
        fmt.Println("listen err=", err)
        return
    }
    defer listen.Close() // 延时关闭
    // 循环等待客户端来链接
    for {
        fmt.Println("等待客户端来链接...")
        conn, err := listen.Accept()
        if err != nil {
            fmt.Println("Accept() err=", err)
        } else {
            fmt.Printf("Accept() suc con=%v 客户端 ip=%v\n", conn, conn.RemoteAddr().String())
        }
        // 这里准备起一个协程，为客户端服务
        go process(conn)
    }
}
```

客户端

* 客户端的处理流程

  1）建立与服务端的链接

  2）发送请求数据，接收服务端返回的结果数据

  3）关闭链接

```go
package main

import (
    "bufio"
    "fmt"
    "net"
    "os"
    "strings"
)

func main() {
    conn, err := net.Dial("tcp", "192.168.2.229:8888")
    if err != nil {
        fmt.Println("client dial err=", err)
        return
    }
    // 功能一：客户端可以发送单行数据，然后退出
    reader := bufio.NewReader(os.Stdin) // os.Stdin代表标准输入
    for {
        // 从终端读取一行用户输入，并准备发送给服务器
        line, err := reader.ReadString('\n')
        if err != nil {
            fmt.Println("readString err=", err)
        }
        line = strings.Trim(line, " \r\n")
        if line == "exit" {
            fmt.Println("客户端退出")
            return
        }
        // 再将line发送给服务器
        _, err = conn.Write([]byte(line + "\n"))
        if err != nil {
            fmt.Println("conn.Write err=", err)
        }
    }
    //fmt.Printf("客户端发送了 %d 字节的数据，并退出", n)
}
```

### 简单的服务器搭建

* 网页

```go
func httpHandler(responseA http.ResponseWriter, requestA *http.Request) {
    responseA.WriteHeader(http.StatusOK)
    responseA.Write([]byte("Hello!"))
}
func main() {    http.HandleFunc("/", httpHandler)
   errT := http.ListenAndServe(":8838", nil)
    if errT != nil {
        fmt.Printf("打开HTTP监听端口时发生错误：%v\n", errT.Error())
    }}

```

* 文件服务器

 ```go 
 http.Handle("/", http.FileServer(http.Dir(`c:\test`)))
    errT := http.ListenAndServe(":8838", nil)
     if errT != nil {
         fmt.Printf("打开HTTP监听端口时发生错误：%v\n", errT.Error())
     }
 ```

* 静态文件型的Web网站服务器,前后端 go+html+css+js

```go
http.HandleFunc("/w/", serveStaticDir)
err := http.ListenAndServe(":8080", nil)
if err != nil {
    t.Printfln("打开HTTP监听端口时发生错误：%v", err.Error())
}
func serveStaticDir(w http.ResponseWriter, r *http.Request) {
    staticFileHandler := http.StripPrefix("/w/", http.FileServer(http.Dir(`c:\test\w`)))
   urlPathT := r.URL.Path
    filePathT := filepath.Join(`c:\test`, path.Clean(urlPathT))
   info, err := os.Lstat(filePathT)
    if err == nil {
        if !info.IsDir() {
            staticFileHandler.ServeHTTP(w, r)
        } else {
            if t.FileExists(filepath.Join(filePathT, "index.html")) {
                staticFileHandler.ServeHTTP(w, r)
            } else {
                http.NotFound(w, r)
            }
        }
    } else {
        http.NotFound(w, r)
    }}

```





## 数据库

SQLite数据库的第三方包

* 引用标准SQL包和SQLite数据库包

* 该数据库为基于文件的轻量级关系数据库

* 仅在程序开发（编译）时需要该包，发布可执行程序时，用户电脑上无需安装任何驱动

* 以及创建数据库语句

  ```go
  package main
  import (
      "os"
       "tools"
      "database/sql"
      _ "github.com/mattn/go-sqlite3"
  )
  
  // 如果存在该库（SQLite库是放在单一的文件中的）则删除该文件
  if t.FileExists(`c:\test\test.db`) {
      os.Remove(`c:\test\test.db`)
  }
  // 创建新库
  dbT, errT := sql.Open("sqlite3", `c:\test\test.db`)
  if errT != nil {
      t.Printfln("创建数据库时发生错误：%v", errT.Error())
      return
  }
  defer dbT.Close()
  
  ```



* 插入

  ```go
  txT, errT := dbT.Begin()
  if errT != nil {
      t.Printfln("新建事务时发生错误：%v", errT.Error())
      return
  }
  // 准备一个SQL语句，用于向表中插入记录
  stmtT, errT := txT.Prepare("insert into TEST(ID, CODE) values(?, ?)")
  if errT != nil {
      t.Printfln("准备SQL语句插入记录时发生错误：%v", errT.Error())
      return
  }
  defer stmtT.Close()
  // 向表中插入10条记录，每条记录的ID字段用循环变量的值赋值
  for i := 0; i < 10; i++ {
      _, errT = stmtT.Exec(i, t.GenerateRandomString(5, 8, true, true, true, false, false, false))
      if errT != nil {
          t.Printfln("执行SQL插入记录语句时发生错误：%v", errT.Error())
          return
      }
  }
  txT.Commit() // 执行事务，此时新纪录才会被真正插入到表中
  
  ```

* 查询

  ```go
  rowsT, errT := dbT.Query("select ID, CODE from TEST")
  if errT != nil {
      t.Printfln("执行SQL查询语句时发生错误：%v", errT.Error())
      return
  }
  defer rowsT.Close()
  
  for rowsT.Next() { // 遍历查询结果
      var idT int
      var codeT string
      errT = rowsT.Scan(&idT, &codeT)
      if errT != nil {
          t.Printfln("遍历查询结果时发生错误：%v", errT.Error())
          return
      }
      t.Printfln("ID: %v, CODE: %v", idT, codeT)
  }
  // 检查查询结果的错误
  errT = rowsT.Err()
  if errT != nil {
      t.Printfln("查询结果有错误：%v", errT.Error())
  }
  
  ```

* 删除

  ```go
  _, errT = dbT.Exec(`drop table TEST`)
  if errT != nil {
      t.Printfln("删除库表时发生错误：%v", errT.Error())
      return
  }
  
  ```

  