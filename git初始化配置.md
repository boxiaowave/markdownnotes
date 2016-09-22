#git和github配置

之前维勇帮我在windows下配置了一下，初始化git和github之后，主要用的命令就是`git add`，`git commit`，`git pull`和`git push`之类的简单命令，这次在ubuntu上面自己配置完全也懵逼了，赶紧查了下资料自己配置了下，这里把过程记录下。

这里时打算把用markdown写的文档同步到github上，云端好跨平台同步，同时有版本控制比较好回滚，最主要现在evernote不支持markdown文件导入（就我目前所知是这样的），像wiznote之类的不太愿意用。

好，我们开始吧。

##git的本地设置
linux和osx都是自带git软件的，而windows下需要下载，可以下载github上提供的客户端，里面最主要有个git bash的玩意，使用起来和ubuntu的终端很像，感觉特别好，可以用来用gcc和g++编译C/C\+\+，比cmd不知道高到哪里去了。

我们这里希望把markdownnotes文件夹同步到github上，首先要在本地用git初始化，加入本地git配置，进入文件夹，使用git late
