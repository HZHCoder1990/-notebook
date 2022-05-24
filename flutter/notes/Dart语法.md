**Visual Code下Dart环境配置**

安装插件： Dart、Flutter、Code Runner

**变量与常量**

使用关键字`var`来定义变量(具备自动推到类型的能力)，也可以在定义时指定变量的类型

```dart
var str1 = "你好啊";
String str2 = "哈哈哈";
int num = 123;
print(str1);
print(str2);
print(num);
```

使用`const`、`final`关键字来定义常量

二者区别:

```dart
final time1 = new DateTime.now(); // 正确
const time2 = new DateTime.now(); // 报错
```

> 用`final`修饰的常量，必须在定义时将其初始化，其值在初始化后不可改变；
> `const`用来定义常量。
>
> 它们的区别在于，`const`比`final`更加严格。`final`只是要求常量在初始化后值不变，但通过`final`，我们无法在编译时（运行之前）知道这个变量的值(编译时无法确定)；而`const`所修饰的是编译时常量(编译时就能确定)，我们在编译时就已经知道了它的值，显然，它的值也是不可改变的。

to do : 王红元笔记

**字符串拼接**

```dart
var str1 = "Hello";
String str2 = "Dart";

print("$str1,$str2"); // 使用美元符号取值
print(str1 + str2);
```

**数据类型**

> int, double, bool(true or false), => 都是Class类型，对象类型，不再是基本数据类型

```dart
var list = ["张三", 20, true]; // List存储Object类型
print(list[0]);
var list2 = <String>["1", "3"]; // 指定数据类型
list2.add("4");
// 创建静态List
var list3 = List.filled(2, "1");
print(list3);
```

