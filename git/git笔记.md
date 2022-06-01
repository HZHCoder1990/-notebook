**Stash**

意为贮存的意思。

例子: 创建一个文件夹，包含2个文件(a.txt，b.txt) 提交到远程代码仓库。

B电脑从代码仓库拉下文件夹。

步骤一: A电脑修改a.txt和b.txt文件，提交时，只提交a.txt。

步骤二: B电脑拉下A提交的代码，并同时修改了a.txt和b.txt文件，提交到远程。

不步骤三: 此时在A电脑上拉取远程仓库的代码，会出现下列出错:

![](./images/1.png)

原因是b.txt文件有未提交的记录，如果从远程拉取到b.txt文件会覆盖本地未提交的记录。

为了解决这个问题，此时*stash*就排上用场了。

在A电脑上执行命令: 

```shell
git stash
```

把b.txt未提交的内容贮存起来。(此时b.txt中的内容会回到上个提交之前)

然后在执行拉取命令就没问题了:

```shell
git pull origin master
```

此时如果我们想取出b.txt贮存区里面的内容，则会报冲突的:

```shell
git stash pop
```

![](./images/2.png)

我们使用Visual Code 打开文件夹，修复冲突:

![](./images/3.png)

修复冲突再提交即可。



**Clone仓库时切分支**

```shell
git clone -b 分支名 仓库地址
```

如果直接使用 git 命令，默认分支是master

```shell
git clone 仓库地址
```

**Merge时发生冲突**

当从分支A Merge 到分支B时，如果出现冲突。解决办法:

1.本地先切换到分支A，2.在pull 一下分支B的代码到本地 3. 解决冲突后再push 到A即可。
