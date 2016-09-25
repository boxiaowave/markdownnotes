#《利用Python进行数据分析》读书笔记


##IPython使用的技巧

Ipython有许多magic command，以%开头，例如`%run filename`运行python脚本，以下几个比较有意思的magic command：

* `！cmd` 	运行shell命令
* `%alias` 	为shell命令取别名，系统退出时失效
* `%bookmark` IPython的目录书签功能

其中的目录书签功能，可以为平常常用的工作目录取别名，例如
```bash
In [58]: %bookmark db /home/boxiao/Documents/20160923/ #将dir以db记录在bookmark中

In [59]: %bookmark -l #列出bookmark中所有的目录
Current bookmarks:
db  -> /home/boxiao/Documents/20160923/
pyd -> /home/boxiao/Documents/PythonForStatistic/

In [60]: %cd db #进入书签目录
(bookmark:db) -> /home/boxiao/Documents/20160923/
/home/boxiao/Documents/20160923
```
利用该系统可以很好的切换工作目录。

###ipd调试工具
Ipython集成并加强了python的pd调试器，运行文件出错后可以输入`%debug`打开ipd调试器并自动跳转到出错的位置。也可以在运行python脚本时加入-d选项，例如
```bash
In [64]: %run -d BubbleSort.py #这里可以在-d后面加入另一个选项-b number自动在number行设置断点。

ipdb> *** Blank or comment
*** Blank or comment
*** Blank or comment
NOTE: Enter 'c' at the ipdb>  prompt to continue execution.
> /home/boxiao/Documents/PythonForStatistic/BubbleSort.py(6)<module>()
      4 
      5 @author: BoXiao
----> 6 """
      7 
      8 def bubblesort(li):
      
      s
> /home/boxiao/Documents/PythonForStatistic/BubbleSort.py(8)<module>()
      6 """
      7 
----> 8 def bubblesort(li):
      9     flag = 0
     10     for j in range(0,len(li)-1):
```

输入s进入调试模式，ipd下使用`b linenumber`在对应行加入断点，再输入c让程序运行到断点，输入n进行单步运行，输入`！变量名`可查看当前变量的值,输入q退出。

同时，可以在python代码中加入`set_trace()`函数，运行脚本时程序会自动在这个位置停止进行调制，输入c可以让程序继续运行。

还有个`%debug`可以用以调试函数，像`%debug(function，*arg）`.


