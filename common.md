1.向Github提交代码时出现如下错误的解决办法:

```shell
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
```

[CSDN链接](https://blog.csdn.net/weixin_41010198/article/details/119698015)



2.删除已经提交的`.DS_Store`文件

首先在git管理的文件夹下创建`.gitignore`文件，并输入以下内容:

```ruby
.gitignore
**/.DS_Store
```

然后删除已经提交到本地git中的`DS_Store`文件：

```ruby
# 删除本地git中的.DS_Store文件
git rm -r --cached .DS_Store
# 提交
git commit -m"删除.DS_Store文件"
# 推送到远程
git push origin master
```

这样远程仓库中的`.DS_Store`文件也被删除了

<font color=#FF0000 size=4>由此引伸出怎么样删除已经提交的文件?</font>

首先在github上创建一个测试工程: JustTest

然后在本地创建一个文件夹包含两个文件:a.text,b.text

首先把文件夹提交到JustTest仓库

```ruby
# 初始化本地git
git init
# 把2个文件加入暂存区
git add .
# 添加commit日志
git commit -m"第一次提交"
# 本地和远程仓库进行关联
git remote add origin https://github.com/HZHCoder1990/JustTest.git
# 第一次提交
git push -u origin master
# 以后提交
git push origin master
```

这样两个文件就被提交到远程仓库JustTest了。

如何删除远程仓库中的a.text文件? 除了删除本地再提交一次之外 还可以按照下列方式操作(<font color=#FF0000>这样本地的a.text文件也会被删除!!!!</font>)

```ruby
# 删除本地git暂存区的文件
git rm -r --cached a.text
# 提交日志
git commit -m"删除a.text"
# 推送到远程仓库
git push origin master
```



<font color=#FF0000 size=4>提交iOS工程时，怎么忽略Pod的文件?</font>



- 使用RN 模板创建TypeScript工程报错的解决办法

  > 1.删除旧版本 react-native-cli
  >
  > npm uninstall -g react-native-cli
  >
  > 2.重新安装来自"react-native-community"的cli库 :
  >
  > npm i -g @react-native-community/cli
  >
  > 3.重新初始化项目即可:
  >
  > npx react-native init MyApp --template react-native-template-typescript

