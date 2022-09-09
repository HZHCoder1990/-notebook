[C++提高(黑马培训课程)](https://www.bilibili.com/video/BV1jt411274J?spm_id_from=333.999.0.0&vd_source=a74179950ed9c89d387679b4746b163b)

**①函数模版基本语法**

```c++
// 声明函数模版，类似"泛型"
template<class T> //class 等同于  typename
void sum(T& a, T& b) {
    T temp = b;
    b = a;
    a = temp;
}
```

> 一个template只能修饰一个函数

*函数模版和普通函数在一起调用规则*

> 1.函数模版可以像普通函数那样被重载
>
> 2.C++编译器优先考虑普通函数
>
> 3.如果函数模版可以产生一个更好的匹配，那么选择模版
>
> 4.可以通过空模板实参列表的语法限定编译器只能通过模版匹配

```C++
// 函数模版
template<class T>
int myAdd(T a, T b) {
    return a + b;
}
// 普通函数
int myAdd(int a, int b) {
    return a + b;
}

int main() {

    int a = 10;
    int b = 20;
    myAdd(a, b); // 断点调试，调用的是普通函数
    myAdd<int>(a, b); // 指定只能调用函数模版
    return 0;
}
```



*函数模版和普通函数的区别*

> 1.函数模版不允许自动类型转化
>
> 2.普通函数允许自动类型转化

```c++
// 函数模版
template<class T>
int myAdd(T a, T b) {
    return a + b;
}
// 普通函数
int myAdd(int a, char b) {
    return a + b;
}

int main() {

    int a = 10;
    int b = 20;
    char c1 = 'a';

    myAdd(a, c1); // 调用普通函数
    myAdd(a, b); // 函数模版函数
    myAdd(c1, b); // 调用普通函数，函数模版函数不允许自动类型转换

    return 0;
}
```

