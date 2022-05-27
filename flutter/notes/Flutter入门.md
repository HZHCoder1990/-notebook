**Flutter运行**

```shell
# 运行Flutter
flutter run
# 热更新
控制台输入: r
```

**Material风格**

```dart
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Flutter Demo')),
        body: const Center(child: Text('Flutter Content')),
      ),
    );
  }
}
```

MaterialApp -> Scaffold -> appBar & body