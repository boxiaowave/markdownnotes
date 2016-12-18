#《利用Python进行数据分析》读书笔记1-IPython


## IPython

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

### ipd调试工具
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

### %prun和%run -p
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

## IPython Notebook
一个类似与mathematica的交互计算文档格式，类似的可以导出基于JSON的ipynb格式文档以演示,需要使用浏览器打开.

它有一些快捷键,这里可以记一下:
####Command Mode (press Esc to enable)

`F`: find and replace
`Ctrl-Shift-P`: open the command palette
`Enter`: enter edit mode
`Shift-Enter`: run cell, select below
`Ctrl-Enter`: run selected cells
`Alt-Enter`: run cell, insert below
`Y`: to code
`M`: to markdown
`R`: to raw
`1`: to heading 1
`2`: to heading 2
`3`: to heading 3
`4`: to heading 4
`5`: to heading 5
`6`: to heading 6
`K`: select cell above
`Up`: select cell above
`Down`: select cell below
`J`: select cell below
`Shift-K`: extend selected cells above
`Shift-Up`: extend selected cells above
`Shift-Down`: extend selected cells below
`Shift-J`: extend selected cells below
`A`: insert cell above
`B`: insert cell below
`X`: cut selected cells
`C`: copy selected cells
`Shift-V`: paste cells above
`V`: paste cells below
`Z`: undo cell deletion
`D,D`: delete selected cells
`Shift-M`: merge selected cells, or current cell with cell below if only one cell selected
`Ctrl-S`: Save and Checkpoint
`S`: Save and Checkpoint
`L`: toggle line numbers
`O`: toggle output of selected cells
`Shift-O`: toggle output scrolling of selected cells
`H`: show keyboard shortcuts
`I,I`: interrupt kernel
`0,0`: restart the kernel (with dialog)
`Esc`: close the pager
`Q`: close the pager
`Shift-Space`: scroll notebook up
`Space`: scroll notebook down
#### Edit Mode (press Enter to enable)

Tab
: code completion or indent
`Shift-Tab`: tooltip
`Ctrl-]`: indent
`Ctrl-[`: dedent
`Ctrl-A`: select all
`Ctrl-Z`: undo
`Ctrl-Shift-Z`: redo
`Ctrl-Y`: redo
`Ctrl-Home`: go to cell start
`Ctrl-Up`: go to cell start
`Ctrl-End`: go to cell end
`Ctrl-Down`: go to cell end
`Ctrl-Left`: go one word left
`Ctrl-Right`: go one word right
`Ctrl-Backspace`: delete word before
`Ctrl-Delete`: delete word after
`Ctrl-M`: command mode
`Ctrl-Shift-P`: open the command palette
`Esc`: command mode
`Shift-Enter`: run cell, select below
`Ctrl-Enter`: run selected cells
`Alt-Enter`: run cell, insert below
`Ctrl-Shift-Minus`: split cell
`Ctrl-S`: Save and Checkpoint
`Down`: move cursor down
`Up`: move cursor up
## 书里的一些tips
### 模块更新后的重载
python导入模块后会创建一个同名命名空间将其中的函数和变量之类保存,下次导入模块都是对该命名空间的引用,所以及时你对模块文件进行了修改,重新导入模块无法使修改生效,这个问题可以在文件中加入reload()函数.例如:
```python
import module
reload(module)
```
当依赖变多了,便需要在很多地方加入reload,最好的办法还是重启解释器.


### IPython个人定制
IPython可以由用户自己定制,其配置文件为~/.config/ipython/ipython_config.py,可以用以下命令创建一个新个性配置:
```bash
ipython profile create secret_project
```
创建了profile_secret_project目录中配置文件,使用
```bash
ipython --profile=secret_project
```
即可使用相应配置打开IPython.


