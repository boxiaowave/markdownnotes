# git和github配置

之前维勇帮我在OSX下配置了一下，初始化git和github之后，主要用的命令就是`git add`，`git commit`，`git pull`和`git push`之类的简单命令，这次在ubuntu上面自己配置完全懵逼了，赶紧查了下资料自己配置了下，这里把过程记录下。

这里时打算把用markdown写的文档同步到github上，云端好跨平台同步，同时有版本控制比较好回滚，最主要现在evernote不支持markdown文件导入（就我目前所知是这样的），像wiznote之类的不太愿意用。

好，我们开始吧。

## git的本地设置
linux和osx都是自带git软件的，而windows下需要下载，可以下载github上提供的客户端，里面最主要有个git bash的玩意，使用起来和ubuntu的终端很像，感觉特别好，可以用来用gcc和g++编译C/C\+\+，比cmd不知道高到哪里去了。

我们这里希望把markdownnotes文件夹同步到github上，首先要在本地用git初始化，加入本地git配置，进入文件夹，依次使用以下命令初始化当前目录的git配置

```bash
git config --global user.email xbustc@gmail.com
git config --global user.name boxiaowave
git init
```

之后就可以用命令`git add`和`git commit -m <comment>`在本地添加文件到分支并提交.其中用户名和邮箱的配置文件`.gitconfig`在`～/`下，可以修改它达到改变user.name和user.email的目的。

## 将本地仓库和github的远端仓库连接并同步

首先需要在本地生成SSH秘钥
``` bash
ssh-keygen -t rsa -C 'xbustc@gmail.com'
```

它会在`～/.ssh/`生成id_ras和id_rsa.pub两个文件。

打开id_rsa.pub文件，他的内容就是我们要的SSH的key，复制内容粘贴到github上创建的新SSH中即可。这里要注意的时用vim打开的内容直接复制在粘贴github会报错提示key is invaild,可能时某些空白字符复制时出现的问题，最后是cp一份到根目录下用gedit打开后鼠标复制粘贴成功。

用以下命令可以检查是否成功，
```bash
ssh -T git@github.com
```
出现```Hi username! You've successfully authenticated, but GitHub does not provide shell access.```即表明成功。

之后在github下创建一个新的仓库准备和本地的仓库连接，这里我取的仓库名时markdownnotes，和本地一致，使用以下命令即可完成连接的配置
```bash
git remote add origin https://github.com/boxiaowave/markdownnotes.git
git push -u origin master


```
这样基本就完成了本地仓库和云端仓库的连接设置。这样就可以愉快的使用`git pull`和`git push`让本地文件和远端文件同步更新。

这里的配置在linux，OSX和windows下应该都是通用的，windows的cmd应该也可以完成类似的工作，个人还是推荐git bash。



