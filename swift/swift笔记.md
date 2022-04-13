#### 零散的Swift笔记

- 尾随闭包

  函数的最后一个参数为闭包则这个闭包叫尾随闭包

  ```swift
  private func clourse(_ first:Int,predicate:(_ a:Int) -> Void) -> Bool{
    predicate(first + 20)
    return first > 10
  }
  
  // 传统写法
   _ = clourse(21) { (a) in
        print(a)
     }
  //如果是尾随闭包 可以按照下面的写法
   _ = clourse(21, predicate: { print($0)})
   _ = clourse(3, predicate: { (a) in
        print(a)
    })
  ```

- **.self**

     `.self`可以用在类型后面取得类型本身，也可以用在实例后面取得这个实例本身

举例:

```swift
 let p = Person()
 print(p.self)  // 实例本身 工程名.Person
 print(Person.self) // 类型本身 Person
```

> public typealias AnyClass = AnyObject.Type
>
> *AnyClass 在 Swift 中被一个typealias 所定义，通过 AnyObject.Type 这种方式得到的是一个`元类型（Meta）`*

<font color=#F00>A.Typ 代表的是A这个类型的类型【也就是类 类型】，也就是说声明一个元类型来存储A这个类型本身 let typeA: A.Type = A.self //用在类型后面取得的是 类型本身(元类),用来获得一个表示该类型的值 let obj = A().self //用在实例后面取得的是 这个实例本身，用来拿到实例本身</font>.

   ```swift
   class Person {
   
       // 静态方法
       class func method(){
           print("method")
       }
       
       // 实例方法
       func objMethod() {
           print("objMethod")
       }
   }
   
    // 调用静态方法
    // 方式1
    Person.method()
    // 或者
    let anyClass:AnyClass = Person.self
    (anyClass as! Person.Type).method()
   
    // 调用实例方法
    let obj = Person()
    obj.objMethod()
   ```

.self使用场景

```swift
class MusicViewController: UIViewController {
  
}

class AbumViewController: UIViewController {
  
}

//调用
//元类使用的意义
let usingVCTypes: [AnyClass] = [MusicViewController.self ,AbumViewController.self]
      
func setupViewController(_ vcTypes: [AnyClass]) {
    for vctype in vcTypes {
        if vctype is UIViewController.Type {
              let vc = (vctype as! UIViewController.Type).init()
                  print(vc)
             }
        }
   }
      
setupViewController(usingVCTypes)
```

- **Self**

  > Self 不仅指代的是 实现该协议的类型本身，也包括了这个类型的子类

     ```swift
     protocol Copyable {
         //不能在协议中定义 范型 进行限制
         // 谁实现了协议 Self就代表那个类型
         func copy() -> Self
     }
     
     class MMyClass: Copyable {
         var num = 1
         func copy() -> Self {
             let result = type(of: self).init()
             result.num  = num
             return result
         }
         required init() {}
     }
     
     // tips
      func test() -> Cat {
         let cat = Cat()
         return cat
      }
     ```



- **Swinject框架的作用**

  先看下面的例子

  ```swift
  // 定义三个类 Cat、Dog、Person
  class Cat {
      let name:String
      init(name:String) {
          self.name = name
      }
      func sound() -> String{
          return "喵喵喵"
      }
  }
  
  class Dog {
      let name:String
      init(name:String) {
          self.name = name
      }
      func sound() -> String{
          return "汪汪汪"
      }
  }
  
  class Person {
      let innerObj:Cat
      init(animal innerObj:Cat) {
          self.innerObj = innerObj
      }
      func play() -> String {
          return "我和\(innerObj.name) 一起玩,它:\(innerObj.sound())"
      }
  }
  
    let p = Person(animal: Cat(name: "🐱"))
    print(p.play())
  
  // Person类可能对Cat和Dog有依赖
  // 如果想把Cat换成Dog 有没有办法?
  // 传统的方法是把Cat和Dog抽一个公共类(基类) 然后在Person里面引用这个基类即可。
  // 还有没有其他的方法呢？
  // 答案就是使用协议!
  
  protocol AnimalAble {
      // readonly 遵守该协议的类一定要有name属性
      var name:String { get }
      func sound() -> String
  }
  
  class Cat : AnimalAble{
      let name:String
      init(name:String) {
          self.name = name
      }
      func sound() -> String {
          return "喵喵喵"
      }   
  }
  
  class Dog : AnimalAble{
      let name:String
      init(name:String) {
          self.name = name
      }
      func sound() -> String{
          return "汪汪汪"
      }
  }
  
  // Person类改造为
  class Person {
      // 协议作为类型
      let innerObj:AnimalAble
      init(animal innerObj:AnimalAble) {
          self.innerObj = innerObj
      }
      func play() -> String {
          return "我和\(innerObj.name) 一起玩,它:\(innerObj.sound())"
      }
  }
  
  // 外界使用
   // OC的写法是:(id<协议名称>)形参
          
   // 如果想把Cat换成Dog 除了继承还有没有办法?
   let p1 = Person(animal: Cat(name: "🐱"))
   print(p1.play())
  
   let p2 = Person(animal: Dog(name: "🐶"))
   print(p2.play())
  
  // 这样Person类就摆脱了对Dog或Cat类的依赖!!
  ```