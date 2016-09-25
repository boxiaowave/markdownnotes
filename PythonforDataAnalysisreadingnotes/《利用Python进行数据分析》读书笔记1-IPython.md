#《利用Python进行数据分析》读书笔记1-IPython


##IPython

Ipython有许多magic command，以%开头，例如`%run filename`运行python脚本，以下几个比较有意思的magic command：

* `！cmd` 	运行shell命令
* `%alias` 	为shell命令取别名，系统退出时失效
* `%bookmark` IPython的目录书签功能
* `%time` 程序执行一次的时间
* `%timeit 程序执行多次的平均时间

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

###%prun和%run -p
python有一个名为cProfile的性能分析工具，主要在命令行中使用，例如：

```bash
boxiao@boxiao-Ubuntu:~/Documents/PythonForStatistic$ python -m cProfile -s cumulative BubbleSort.py 
[1, 2, 3, 4, 5, 6, 7, 8, 10, 11]
         23 function calls in 0.000 seconds

   Ordered by: cumulative time

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    0.000    0.000 BubbleSort.py:6(<module>)
        1    0.000    0.000    0.000    0.000 BubbleSort.py:8(bubblesort)
       10    0.000    0.000    0.000    0.000 {range}
       10    0.000    0.000    0.000    0.000 {len}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}


```

它会列出各函数的运行次数和执行时间，`-s cumulative`会让输出按照制定规则排序。

在Ipython中可以使用%prun和%run -p完成以上功能，例如：
```bash
In [83]: %run -p -l 3 -s cumulative BubbleSort.py
[1, 2, 3, 4, 5, 6, 7, 8, 10, 11]
          96 function calls in 0.001 seconds

   Ordered by: cumulative time
   List reduced from 50 to 3 due to restriction <3>

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    0.001    0.001 <string>:1(<module>)
        1    0.000    0.000    0.001    0.001 interactiveshell.py:2443(safe_execfile)
        1    0.000    0.000    0.000    0.000 py3compat.py:281(execfile)

```
`%prun`只能运行python语句，不能运行文件，用法不是特别清楚，但`%run -p`的功能已经足够分析脚本。

##IPython Notebook
一个类似与mathematica的交互计算文档格式


