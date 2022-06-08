**Cocoapods相关**

```ruby
// 安装制定版本
sudo gem install -n /usr/local/bin cocoapods -v 1.9.2 
// 卸载制定版本
sudo gem uninstall -n /usr/local/bin cocoapods -v 1.9.3
// 安装或升级pods
sudo gem install cocoapods -n /usr/local/bin
// 查看pod版本
pod --version

// 查看安装的所有的cocoapods版本
gem list cocoapods
```

**Flutter相关**

```ruby
// 清除缓存
flutter clean
// 运行flutter
flutter run
// flutter 升级
flutter upgrade
// 查看flutter版本
flutter --version
```

今天在公司电脑上跑flutter工程时发现一个问题，因为公司电脑安装了多个版本的cocoapods(1.11.3、1.10.0等)，而我在ios工程中指定了cocoapods的版本(1.10.0)，并执行`bundle exec pod install`时能成功安装需要的库。但是运行`flutter run`命令时，默认回去执行`pod install`命令(会去默认使用1.11.3版本)，这就不能使用指定的cocoapods运行工程了。解决办法就是删除cocoapods的1.11.3版本，让其执行`pod install`命令时使用的是和工程指定的1.10.0版本即可。

