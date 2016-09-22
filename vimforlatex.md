#使用vim遇到的一些问题

#Latex篇

###安装texlive2016
系统环境是Ubuntu，安装时texlive2016，下载iso文件挂载后进入挂载目录，运行install—tl文件就会一路安装了。

最后要注意的时需要添加一些texlive的工作目录到环境变量中，否则终端无法使用一些latex编译命令，这一步修改根目录的.bashrc文件即可实现（修改后使用source .bashrc使之生效），修改正确后在终端中输入`tex --version`可查看latex的相关信息。

###安装vim-latex（latex-suite）
由于有了插件管理工具Vundle和github的clone功能，现在vim的插件安装非常方便，不用在相关网站下载好插件后放入ftplugin文件中，只需要在.vimrc配置文件中加入：Plugin +github上插件项目名，管理员权限打开vim执行`：PluginInstall`,Vundle工具会自动安装该插件。

vim-latex又叫latex-suite，如果需要帮助文件，在vim中需要`:h latex-suite.txt`,而不是`:h vim-latex`。


###编译快捷键
vim-latex的功能时比较强大的，有许多的快捷键，这里我们只是为了安装vim-latex测试工作状态，对于快捷键不做深入了解，这里只需要知道编译快捷键为在Normal模式下`<leader>ll`,这里的`<leader>`要注意下，很多网上的参考文章将快捷键表达为`\ll`，但其实这里\指的时vim定义的`<leader>`键，可以在.vimrc中修改定义，我的vim默认`<leader>`为，键，所以快捷键为`,ll`，相对应的查看输出的文档的快捷键为`<leader>lv`。

除此之外还需要在.vimrc增加一些配置使默认的编译工具修改为xelatex，输出文档格式为pdf，这个可以参考帮助文件。

###ubuntu下字体安装
之前在osx和windows下写的tex文件中都对部分字体进行了重命名，但是osx、ubuntu、windows下字体集不一样，之前是对tex文件针对osx和windows写了两个重命名代码段，比较麻烦，需要找到匹配的黑体，宋体和楷体的内部名字。这次直接把macbook上的字体找出来，字体文件夹为`/Library/Fonts`，开始尝试用在ubuntu字体文件夹`/usr/share/fonts`下建立新文件夹放入osx的字体文件修改文件权限后执行

```bash
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv
```

但是一直无法在字体中找到安装的新字体，并且编译tex文件也显示字体未找到。后面在网上找到font-manager这个软件，非常简单，只需要导入文件字体软件就完成了安装字体的操作。

前面的尝试可能时缺少了某些步骤导致失败，以后可以继续尝试下。


###picins.sty宏包的安装
picins宏包很早就从texlive的镜像中移除了，所以必需手动安装，直接google下载地址下载解压得到picins文件夹，将文件夹放入`texmf-dist/latex/tex`下，到这一步在texhash即可。

但我在这遇到问题时在本地用户下运行texhash没有对`texmf-dist`文件夹的读权限，执行`sudo texhash`会有找不到texhash命令的报错信息，或许时环境变量对root没有生效？最后是把只能暴力解决，把`texmf-dist`文件夹权限改成777，后面出现`texmf.dist/ls-R`文件夹无读权限，依葫芦画瓢，问题解决。

这里对于latex编译时找不到picins.sty时，latex会让你键入picins.sty的地址，可以键入你下载的picins.sty的绝对路径让编译继续下去，当然这样每次编译都需要键入绝对路径，非常麻烦。

###结果
经过以上操作，最后成功编译。不过有些问题还需要解决，例如latex代码的自动补全实现以及bibtex的实现。

