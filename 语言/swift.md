# 技术栈要求

* UIKit
* SwiftUi
* SpriteKit
* SceneKit
* ARKit

# 移动应用开发基础知识

## swift基本现状

* apple在wwdc2014上所发布的语言

* xcode、模拟器、人机交互规范

* playground 轻量开发环境

  * 可以提交基于playground的一个小的idea

* Xcode

  可以使用 show quick help和build developer document 来查看帮助

## app 设计流程

* 调研 原型 视觉 开发 测试 迭代
* 调研
  * 大学生焦虑
  * 做一款能够记录自己往昔 设定自己未来目标的app
  * 归墟 --心灵宁静之地
* 原型
  * xmind设计主界面以及分界面的逻辑关系
  * axure 墨刀
  * 交互设计
* 视觉
  * 视觉设计
  * 色彩
  * 美工
* 开发
* 测试
* 迭代





政治正确 

传统文化 主推技术

有温度的产品

记录美好时刻

ar 结合展示自己记录的美好 走廊





记录目标 

目标设置以7 /14 / 30 / 365为时间



追踪目标

根据目标获得奖励

达成目标后 获得一颗属于自己星星 构成星座之后 可以利用手机 看到现实中存在的位置 

记录自己以前达成的成绩







将有自己美好回忆的地方发出来 汇集在地图上 让大伙都看





# swift语言基础

https://swiftgg.gitbook.io/swift

## 变量、常量、函数

* 第一个程序

  ```swift
  print("Hello, World!")
  ```

* 变量

  ```swift
  var a = 1024
  a += 10
  print(a)
  var b:Double = 10.21 //浮点变量的赋值
  print(b*0.9)
  ```

* 常量

  ```swift
  let constA = 42//用let声明常量
  let sex = "man"
  let name = "菜鸟教程"
  let site = "http://www.runoob.com"
  
  print("\(name)的官网地址为：\(site)")//在字符串中可以使用括号与反斜线来插入常量
  ```

* 类型转换和print

  ```swift
  String(a)
  ```

## 数组和字典

* 数组

  ```swift
  var letter = ["a","b","c"]
  letter = []// 清空
  print(letter)
  ```

* 字典

  ```swift
  var match = [
      "a" : "1",
      "b" : "2",
      "c" : "3",
  ]
  match = [:]//清空
  
  print(match)
  ```

## 控制流

* 循环

  ```swift
  for a in b{
      if{
          
      }else if{
          
      }else
  }
  
  while{
      
  }
  ```

* 空数据

  ```swift
  var a:Int? = nil//可选(Optionals)
  
  if let a = a{
      print(a)//如果a的值不为空 输出a
  }
  
  var b  = 0
  print(a??b)//a不空 输出a 不然输出b
  ```

* 字典数组

  ```swift
  let allScores = [
      "computerScience": [48, 34, 23, 50, 49],
      "software": [48, 36, 50, 28, 48],
      "industrialDesign": [30, 45, 32, 48, 18],
  ]
  
  var maxScore = 32
  var minScore = 32
  
  for (_, scores) in allScores {
      for score in scores {
          if maxScore <= score {
              maxScore = score
          }
          if minScore >= score {
              minScore = score
          }
      }
  }
  
  print("最高分: \(maxScore)", "最低分: \(minScore)")
  
  
  var avgOfSoftWare = 0
  var totalOfSoftWare = 0
  var softWareScore = [48, 36, 50, 28, 48]
  var index = 0
  
  while index < softWareScore.count {
      totalOfSoftWare += softWareScore[index]
      index += 1
  }
  
  avgOfSoftWare = totalOfSoftWare / softWareScore.count
  
  print(avgOfSoftWare)
  ```

## 枚举

```swift
enum DaysofaWeek {
    case Sunday
    case Monday
    case TUESDAY
    case WEDNESDAY
    case THURSDAY
    case FRIDAY
    case Saturday
}

var weekDay = DaysofaWeek.THURSDAY
weekDay = .THURSDAY
switch weekDay
{
case .Sunday:
    print("星期天")
case .Monday:
    print("星期一")
case .TUESDAY:
    print("星期二")
case .WEDNESDAY:
    print("星期三")
case .THURSDAY:
    print("星期四")
case .FRIDAY:
    print("星期五")
case .Saturday:
    print("星期六")
}
//当var一个变量之后，用var weekDay = DaysofaWeek.THURSDAY赋值后，自动推断确定了类型，之后就可以使用 .FRIDAY缩写直接赋值
```



##  函数

* 定义

  ```swift
  func ans(a:Int,b:Int ) -> Double {
      return Double(a+b)*0.6
  }
  print(ans(a: 2, b: 3))//形参
  
  func ans(first a:Int,second b:Int ) -> Double {
      return Double(a+b)*0.6
  }
  print(ans(first: 2, second: 3)) //实参和形参
  
  func ans(_ a:Int,_ b:Int ) -> Double {
      return Double(a+b)*0.6
  }
  print(ans(1, 2))//用_省略实参
  ```

* 嵌套函数

  ```swift
  func computer(a:Int,b:Int)->Int{
      func computer(c:Int,d:Int)->Int{
          return a+b
      }
      return a+b+computer(c: a, d: b)//调用的为嵌套的computer函数
  }
  
  print(computer(a: 1, b: 2))
  ```

* 闭包

  ```swift
  func backward(_ s1: String, _ s2: String) -> Bool {
      return s1 > s2
  }
  var reversedNames = names.sorted(by: backward)
  // reversedNames 为 ["Ewa", "Daniella", "Chris", "Barry", "Alex"] 正常排序
  
  reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
      return s1 > s2
  })//闭包写法
  
  
  { (parameters) -> return type in
      statements
  }
  
  ```

* 随机

  ```swift
  var a = ["4","5"]
  print(a.randomElement())
  print(a.randomElement()!) //randomElement返回的是一个可选类型，通过！来进行强制解包
  ```

  



