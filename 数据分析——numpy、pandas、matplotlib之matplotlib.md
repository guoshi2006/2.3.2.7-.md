## 【python教程】数据分析——numpy、pandas、matplotlib之matplotlib

[来源](https://www.bilibili.com/video/BV1hx411d7jb?p=4)
1. 什么是matplotlib
2. matplotlib基本要点
3. matplotlib的散点图、直方图、柱状图
4. 更多的画图工具

### 1.什么是matplotlib

matplotlib: 最流行的Python底层绘图库，主要做数据可视化图表,名字取材于MATLAB，模仿MATLAB构建


### 2.matplotlib基本要点

### 绘制折线图
- 技术要点：```plt.plot(x,y)```


```python
from matplotlib import pyplot as plt #导入pyplot模块
x = range(2, 26, 2) #数据在x轴的位置，是一个可迭代对象
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15] #数据在y轴的位置，是一个可迭代对象
```

- x轴和y轴的数据一起组成了所有要绘制的坐标
- 分别是（2，15），（4，15），（6，14.5），（8，17）......

#### #绘图并展示图形


```python
plt.plot(x, y) #传入x和y，通过plot绘制出折线图
plt.show() #在执行程序的时候展示图形
```


![png](output_9_0.png)


### 但是目前存在以下几个问题:
- 设置图片大小(想要一个高清无码大图)
- 保存到本地
- 描述信息,比如x轴和y轴表示什么,这个图表示什么
- 调整x或者y的刻度的间距
- 线条的样式(比如颜色,透明度等)
- 标记出特殊的点(比如告诉别人最高点和最低点在哪里)
- 给图片添加一个水印(防伪,防止盗用)


```python
from matplotlib import pyplot as plt #导入pyplot模块
```


```python
x = range(2, 26, 2) #数据在x轴的位置，是一个可迭代对象
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15] #数据在y轴的位置，是一个可迭代对象
```

#### #设置图片大小


```python
plt.figure(figsize = (20, 8), dpi = 80) #设置figsize = (宽,高)，而dpi为每英寸像素点的个数
plt.plot(x, y) #传入x和y，通过plot绘制出折线图
```




    [<matplotlib.lines.Line2D at 0x81eb910>]




![png](output_14_1.png)


- figure图形图标的意思，在这里指的是就是画的图
- 通过实例化一个figure并且传递参数，能够在后台自动使用该figure实例
- 在图像模糊的时候可以传入dpi参数，让图片更加清晰


```python
plt.savefig("./sig_size.png") #保存图片，保存在当前位置./、名为sig_size、格式为png
```


    <Figure size 432x288 with 0 Axes>


- 可以保存为svg这种矢量图格式，放大不会有锯齿


```python
plt.show() #在执行程序的时候展示图形
```

### 这个x轴的刻度不是之前定义的x的刻度，可以调整x或者y轴上的刻度

- xticks()中有3个参数： ```xticks(locs, [labels], **kwargs)```
- locs参数是一个数组，用于设置X轴刻度间隔
- [labels]参数也是一个数组，用于设置每个间隔的显示标签
- **kwargs可用于设置标签字体倾斜度和颜色等


```python
from matplotlib import pyplot as plt
plt.figure(figsize = (20, 8), dpi = 80)
x = range(2, 26, 2) 
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15] 
plt.plot(x, y)
plt.xticks(x) #设置x的刻度
plt.show()
```


![png](output_21_0.png)


- 当刻度太密集时使用**列表的步长（间隔取值）**来解决，matplotlib会自动应对
- 即```plt.xticks(x[::2])```
- x的刻度想要设置什么，plt.xticks()里面就写什么

### 如果列表a表示10点到12点的每一分钟的气温,如何绘制折线图观察每分钟气温的变化情况?


```python
from matplotlib import pyplot as plt
import random
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)
plt.show()
```


![png](output_24_0.png)


- 先绘制简单的图形，再找出哪里有误，逐步进行细化调整

### 上述虽然画出图形，但x轴刻度并没有如题显示时间刻度出来，继续调整：


```python
from matplotlib import pyplot as plt
import random
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)
_x = list(x)[::10] #设置步长为10
_xtick_labels = ["hello,{}".format(i) for i in _x] #设置x轴显示的标签
plt.xticks(_x, _xtick_labels)
plt.show()
```


![png](output_27_0.png)


### 进一步设置


```python
from matplotlib import pyplot as plt
import random
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)
_x = list(x)
_xtick_labels = ["10点,{}分".format(i) for i in range(60)] 
_xtick_labels += ["11点,{}分".format(i- 60) for i in range(60, 120)]
plt.xticks(_x[::3], _xtick_labels[::3], rotation = 90) #将数值型数字对应到字符串上，并旋转标签
plt.show()
```

    G:\anaconda3\lib\site-packages\matplotlib\backends\backend_agg.py:214: RuntimeWarning: Glyph 28857 missing from current font.
      font.set_text(s, 0.0, flags=flags)
    G:\anaconda3\lib\site-packages\matplotlib\backends\backend_agg.py:214: RuntimeWarning: Glyph 20998 missing from current font.
      font.set_text(s, 0.0, flags=flags)
    G:\anaconda3\lib\site-packages\matplotlib\backends\backend_agg.py:183: RuntimeWarning: Glyph 28857 missing from current font.
      font.set_text(s, 0, flags=flags)
    G:\anaconda3\lib\site-packages\matplotlib\backends\backend_agg.py:183: RuntimeWarning: Glyph 20998 missing from current font.
      font.set_text(s, 0, flags=flags)
    


![png](output_29_1.png)


- **让列表_x中的数据和_xtick_labels上的数据都传入，最终会在x轴上一一对应的显示出来**
- plt.xticks()里的两个参数的数字和字符串一样步长，一样的长度，否则不能完全覆盖整个轴
- 使用列表的切片，**每隔3个**选一个数据进行展示
- 为了让字符串不会被覆盖，**使用rotation选项，让字符串旋转90度数**
- 唯有列表才能在后面加```[]```取步长

### 但上图x轴标签不显示中文
- matplotlib默认不支持中文字符，因为默认的英文字体无法显示汉字
##### 查看linux/mac下面支持的字体:
- ```fc-list```       ->查看支持的字体
- ```fc-list :lang=zh``` ->查看支持的中文(冒号前面有空格)
##### 如何修改matplotlib的默认字体?
- 通过matplotlib.rc可以修改,具体方法参见源码(windows/linux)
- 通过matplotlib 下的font_manager可以解决(windows/linux/mac)

#### 一种设置为：这个字体设置为全局设置，只用在该处修改即可


```python
from matplotlib import pyplot as plt
import random
import matplotlib
font = {"family" : "Microsoft Yahei",
        "size" : "10"} #设置字体为微软雅黑，字体大小为10
matplotlib.rc("font", **font) 
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)
_x = list(x)
_xtick_labels = ["10点,{}分".format(i) for i in range(60)] 
_xtick_labels += ["11点,{}分".format(i- 60) for i in range(60, 120)]
plt.xticks(_x[::3], _xtick_labels[::3], rotation = 45) 
plt.show()
```


![png](output_33_0.png)


- 而```matplotlib.rc("font", **font)```等价于```matplotlib.rc("font", "family" = "Microsoft Yahei","size" = "10")```

#### 一种设置为：指定具体字体文件路径，然后在需要显示中文的地方添加```fontproperties```参数


```python
from matplotlib import pyplot as plt
import random
import matplotlib
from matplotlib import font_manager #引入matplotlib模块的font_manager()方法
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") #实例化my_font，设置字体存放的路径
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)
_x = list(x)
_xtick_labels = ["10点,{}分".format(i) for i in range(60)] 
_xtick_labels += ["11点,{}分".format(i- 60) for i in range(60, 120)]
plt.xticks(_x[::3], _xtick_labels[::3], rotation = 45, fontproperties = my_font) #设置字体，在fontproperties传入参数my_font
plt.show()
```


![png](output_36_0.png)


### 进一步明确x轴、y轴与当前图形到底表示什么，即给图像添加描述信息


```python
from matplotlib import pyplot as plt
import random
import matplotlib
from matplotlib import font_manager #引入matplotlib模块的font_manager()方法
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") #实例化my_font，设置字体存放的路径
x = range(0, 120)
y = [random.randint(20, 25) for i in range(120)]
plt.figure(figsize = (20, 8), dpi = 80)
plt.plot(x, y)

#添加轴的描述信息
_x = list(x)
_xtick_labels = ["10点,{}分".format(i) for i in range(60)] 
_xtick_labels += ["11点,{}分".format(i- 60) for i in range(60, 120)]
plt.xticks(_x[::3], _xtick_labels[::3], rotation = 45, fontproperties = my_font) #设置字体，在fontproperties传入参数my_font
plt.xlabel("时间", fontproperties = my_font) #设置x轴的label
plt.ylabel("温度 单位（摄氏度）", fontproperties = my_font) #设置y轴的label
plt.title("10点到12点每分钟的时间变化情况", fontproperties = my_font) #设置标题

plt.show()
```


![png](output_38_0.png)


### 动手：

假设在30岁的时候,根据自己的实际情况,统计出来了从11岁到30岁每年交的朋友的数量如列表a,请绘制出该数据的折线图,以便分析自己每年交朋友的数量走势
- 要求:a = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
- y轴表示个数
- x轴表示岁数,比如11岁,12岁等


```python
from matplotlib import pyplot as plt
from matplotlib import font_manager 
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 
y = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
x = range(11, 31)
plt.figure(figsize = (20, 8), dpi = 80) #设置图片大小
plt.plot(x, y) #绘制折线图
_xtick_labels = ["{}岁".format(i) for i in x] #设置刻度
plt.xticks(x, _xtick_labels, fontproperties = my_font) #设置字体，在fontproperties传入参数my_font
plt.xlabel("年龄", fontproperties = my_font) #设置x轴的label
plt.ylabel("朋友个数", fontproperties = my_font) #设置y轴的label
plt.title("11岁到30岁每年交的朋友的数量情况", fontproperties = my_font) #设置标题

#绘制网格
plt.grid(alpha = 0.4) 

plt.show()
```


![png](output_40_0.png)


- 网格的绘制```plt.grid()```是按照x轴和y轴来进行，因此要想改变网格疏密度就需要修改x轴和y轴的刻度大小
- 网格绘制的参数```alpha```是表示透明度，介于0-1之间，1为完全不透明，0为透明

### 动手：

假设大家在30岁的时候,根据自己的实际情况,统计出来了**你和你同桌**各自从11岁到30岁每年交的朋友的数量如列表a和b,请在一个图中绘制出该数据的折线图,以便比较自己和同桌20年间的**差异**,同时分析每年交朋友的**数量走势**
- 要求：a = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
- b = [1,0,3,1,2,2,3,3,2,1 ,2,1,1,1,1,1,1,1,1,1]
- y轴表示个数
- x轴表示岁数,比如11岁,12岁等



```python
from matplotlib import pyplot as plt
from matplotlib import font_manager 
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 
y_1 = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
y_2 = [1,0,3,1,2,2,3,3,2,1,2,1,1,1,1,1,1,1,1,1]
x = range(11, 31)
plt.figure(figsize = (20, 8), dpi = 80) #设置图片大小

#绘制两条折线图
plt.plot(x, y_1) 
plt.plot(x, y_2)

_xtick_labels = ["{}岁".format(i) for i in x] #设置刻度
plt.xticks(x, _xtick_labels, fontproperties = my_font) #设置字体，在fontproperties传入参数my_font
plt.xlabel("年龄", fontproperties = my_font) #设置x轴的label
plt.ylabel("朋友个数", fontproperties = my_font) #设置y轴的label
plt.title("11岁到30岁每年交的朋友的数量情况", fontproperties = my_font) #设置标题
plt.grid(alpha = 0.4) #绘制网格
plt.show()
```


![png](output_43_0.png)


#### 上图虽然画出两条折线图，但并未明确不同折线代表的是哪一方，于是进一步操作：


```python
from matplotlib import pyplot as plt
from matplotlib import font_manager 
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 
y_1 = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
y_2 = [1,0,3,1,2,2,3,3,2,1,2,1,1,1,1,1,1,1,1,1]
x = range(11, 31)
plt.figure(figsize = (20, 8), dpi = 80) #设置图片大小

plt.plot(x, y_1, label = "自己") 
plt.plot(x, y_2, label = "同桌")

_xtick_labels = ["{}岁".format(i) for i in x] #设置刻度
plt.xticks(x, _xtick_labels, fontproperties = my_font) #设置字体，在fontproperties传入参数my_font
plt.xlabel("年龄", fontproperties = my_font) #设置x轴的label
plt.ylabel("朋友个数", fontproperties = my_font) #设置y轴的label
plt.title("11岁到30岁每年交的朋友的数量情况", fontproperties = my_font) #设置标题
plt.grid(alpha = 0.4) #绘制网格

#添加图例
plt.legend(prop = my_font, loc = "best") #loc = "best"等价于loc = 0，表示自行选择最佳位置

plt.show()
```


![png](output_45_0.png)


- ```plt.legend()```函数主要的作用就是给图加上图例，```plt.legend([x,y,z])```里面的参数使用的是list的的形式将图表的的名称传给这个函数
- ```plt.legend()```通过```prop```指定图例的字体，通过```loc```指定图例的位置，默认在右上角

#### 再自定义绘制图形的风格，如下：


```python
from matplotlib import pyplot as plt
from matplotlib import font_manager 
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 
y_1 = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
y_2 = [1,0,3,1,2,2,3,3,2,1,2,1,1,1,1,1,1,1,1,1]
x = range(11, 31)
plt.figure(figsize = (20, 8), dpi = 80) 

#自定义图形风格
plt.plot(x, y_1, label = "自己", color = "orange", linestyle = ":") 
plt.plot(x, y_2, label = "同桌", color = "cyan", linestyle = "-.")

_xtick_labels = ["{}岁".format(i) for i in x] 
plt.xticks(x, _xtick_labels, fontproperties = my_font) 
plt.xlabel("年龄", fontproperties = my_font) 
plt.ylabel("朋友个数", fontproperties = my_font) 
plt.title("11岁到30岁每年交的朋友的数量情况", fontproperties = my_font) 

#自定义网格
plt.grid(alpha = 0.4, linestyle = "--") 

plt.legend(prop = my_font, loc = "best") 
plt.show()
```


![png](output_48_0.png)


```plt.plot()```中，可以加入相应的参数，其中：
- ```color = "r"```     表示线条颜色
- ```linestyle = "--"```  表示线条风格
- ```linewidth = 5```    表示线条粗细
- ```alpha= 0.5```      表示透明度
![image.png](attachment:image.png)

### 动手：

- 假设你希望在图中**标记**出自己和同桌交朋友最多的那一年所对应的数据,应该怎么做?(**添加文本注释**)
- 假设你打算把自己的统计结果发布到网上供人瞻仰,但是很担心自己的图片**被人盗用**,你应该怎么做?(**添加文字(水印)到图中**)

### 总结：

- 绘制了折线图(```plt.plot()```)
- 设置了图片的大小和分辨率(```plt.figure```)
- 实现了图片的保存(```plt.savefig```)
- 设置了xy轴上的刻度和字符串(```xticks```)
- 解决了刻度稀疏和密集的问题(```xticks```)
- 设置了标题,xy轴的lable(```title```,```xlable```,```ylable```)
- 设置了字体(```font_manager.FontProperties```,```matplotlib.rc```)
- 在一个图上绘制多个图形(plt多次plot即可)
- 为不同的图形添加图例


### [matplotlib官网例子](https://matplotlib.org/gallery/lines_bars_and_markers/bar_stacked.html#sphx-glr-gallery-lines-bars-and-markers-bar-stacked-py)


```python
import matplotlib.pyplot as plt

labels = ['G1', 'G2', 'G3', 'G4', 'G5']
men_means = [20, 35, 30, 35, 27]
women_means = [25, 32, 34, 20, 25]
men_std = [2, 3, 4, 1, 2]
women_std = [3, 5, 2, 3, 3]
width = 0.35       # the width of the bars: can also be len(x) sequence

fig, ax = plt.subplots()

ax.bar(labels, men_means, width, yerr=men_std, label='Men')
ax.bar(labels, women_means, width, yerr=women_std, bottom=men_means,
       label='Women')

ax.set_ylabel('Scores')
ax.set_title('Scores by group and gender')
ax.legend()

plt.show()
```


![png](output_53_0.png)


### matplotlib只能绘制折线图么?
- matplotlib能够绘制**折线图**，**散点图**，**柱状图**，**直方图**，**箱线图**，**饼图**等
- 但是,我们需要知道不同的**统计图**到底能够表示出什么，以此来决定选择哪种统计图来更直观的呈现我们的数据

### 对比常用统计图

- **折线图**——以折线的上升或下降来表示统计数量的增减变化的统计图

*特点*：能够显示数据的变化趋势，反映事物的变化情况。(变化)

- **直方图**——由一系列高度不等的纵向条纹或线段表示数据分布的情况。 

一般用横轴表示数据范围，纵轴表示分布情况。

*特点*：绘制**连续性**的数据,展示一组或者多组数据的分布状况(统计)

- **条形图**——排列在工作表的列或行中的数据可以绘制到条形图中。

*特点*：绘制**离散**的数据,能够一眼看出各个数据的大小,比较数据之间的差别。(统计)

- **散点图**——用两组数据构成多个坐标点，考察坐标点的分布,判断两变量之间是否存在某种关联或总结坐标点的分布模式。

*特点*：判断变量之间是否存在数量关联趋势,展示离群点(分布规律)![image.png](attachment:image.png)

### 折线图的更多应用场景
- 呈现公司产品(不同区域)每天活跃用户数
- 呈现app每天下载数量
- 呈现产品新功能上线后,用户点击次数随时间的变化
- 呈现员工每天上下班时间

![总结图片](./数据分析day01总结.png)

#### 插入本地图片方法：Markdown模式下——>菜单栏——>Edit——>InsertImage

### 绘制散点图
- 技术要点：```plt.scatter(x,y)```

### 动手
假设通过爬虫你获取到了北京2016年3,10月份每天白天的最高气温(分别位于列表a,b),那么此时如何寻找出气温和随时间(天)变化的某种规律?
- a = [11,17,16,11,12,11,12,6,6,7,8,9,12,15,14,17,18,21,16,17,20,14,15,15,15,19,21,22,22,22,23]
- b = [26,26,28,19,21,17,16,19,18,20,20,19,22,23,17,20,21,20,22,15,11,15,5,13,17,10,11,13,12,13,6]
- [数据来源](http://lishi.tianqi.com/beijing/index.html)


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager 

#设置字体来源
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 

#导入数据
y_3 = [11,17,16,11,12,11,12,6,6,7,8,9,12,15,14,17,18,21,16,17,20,14,15,15,15,19,21,22,22,22,23]
y_10 = [26,26,28,19,21,17,16,19,18,20,20,19,22,23,17,20,21,20,22,15,11,15,5,13,17,10,11,13,12,13,6]
x_3 = range(1, 32)
x_10 = range(51, 82)

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80) 

#使用scatter(x,y)绘制散点图，这是与上面绘制折线图plot(x,y)的唯一区别
plt.scatter(x_3, y_3, label = "3月份", color = "orange") 
plt.scatter(x_10, y_10, label = "10月份", color = "cyan")

#调整x轴的刻度
_x = list(x_3) + list(x_10)
_xtick_labels = ["3月{}日".format(i) for i in x_3] 
_xtick_labels += ["10月{}日".format(i-50) for i in x_10] 
plt.xticks(_x[::3], _xtick_labels[::3], fontproperties = my_font, rotation = 45) #均取步长为3使得刻度显示不会过于密集

#添加描述信息
plt.xlabel("时间", fontproperties = my_font) 
plt.ylabel("温度", fontproperties = my_font) 
plt.title("北京2016年3、10月份每天白天的最高气温", fontproperties = my_font) 

#自定义网格
plt.grid(alpha = 0.4, linestyle = "--") 

#添加图例
plt.legend(prop = my_font, loc = "upper left")

#展示图形
plt.show()
```


![png](output_62_0.png)


### 散点图的更多应用场景
- 不同条件(维度)之间的内在关联关系
- 观察数据的离散聚合程度

### 绘制条形图
- 技术要点：```plt.bar(x,y)```

### 动手
假设你获取到了2017年内地电影票房前20的电影(列表a)和电影票房数据(列表b),那么如何更加直观的展示该数据?
- a = ["战狼2","速度与激情8","功夫瑜伽","西游伏妖篇","变形金刚5：最后的骑士","摔跤吧！爸爸","加勒比海盗5：死无对证","金刚：骷髅岛","极限特工：终极回归","生化危机6：终章","乘风破浪","神偷奶爸3","智取威虎山","大闹天竺","金刚狼3：殊死一战","蜘蛛侠：英雄归来","悟空传","银河护卫队2","情圣","新木乃伊",]
- b=[56.01,26.94,17.53,16.49,15.45,12.96,11.8,11.61,11.28,11.12,10.49,10.3,8.75,7.55,7.32,6.99,6.88,6.86,6.58,6.23] 单位:亿
- 数据来源: http://58921.com/alltime/2017


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager 

#设置字体来源
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 

#导入数据（x列表标签过长，可以用\n来分成两行显示）
x = ["战狼2","速度与激情8","功夫瑜伽","西游伏妖篇","变形金刚5：\n最后的骑士","摔跤吧！爸爸","加勒比海盗5：\n死无对证","金刚：\n骷髅岛","极限特工：\n终极回归","生化危机6：\n终章","乘风破浪","神偷奶爸3","智取威虎山","大闹天竺","金刚狼3：\n殊死一战","蜘蛛侠：\n英雄归来","悟空传","银河护卫队2","情圣","新木乃伊",]
y = [56.01,26.94,17.53,16.49,15.45,12.96,11.8,11.61,11.28,11.12,10.49,10.3,8.75,7.55,7.32,6.99,6.88,6.86,6.58,6.23]

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80) 

#使用bar(x,y)绘制条形图
plt.bar(x, y, label = "票房", color = "orange", width = 0.3) #可改为【plt.bar(range(len(a)), y, label = "票房", color = "orange")】

#设置字符串到x轴
_xtick_labels = [i for i in x] 
plt.xticks(x, _xtick_labels, fontproperties = my_font, rotation = 90) #可改为【plt.xticks(range(len(a)), x ,fontproperties = my_font, rotation = 45)】

#添加描述信息
plt.xlabel("电影名", fontproperties = my_font) 
plt.ylabel("票房（单位：亿元）", fontproperties = my_font) 
plt.title("2017年内地电影票房前20的电影", fontproperties = my_font) 

#自定义网格
plt.grid(alpha = 0.4, linestyle = "--") 

#添加图例
plt.legend(prop = my_font, loc = "upper right")

#展示图形
plt.show()
```


![png](output_66_0.png)


#### 关键点：

1、```_x = range(len(a)
_y = b
plt.bar(_x, b, width = 0.2, color = "orange")```
- bar绘制条形图，只能接受含数字的可迭代对象
- width表示长度的宽度，默认0.8

2、```plt.yticks(_x, a,fontproperties = my_font, rotation = 90)```
- 通过设置xticks实现数字与字符串的对应

#### 条形图也可以设置成横向表示：


```python
#绘制横向条形图
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager 

#设置字体来源
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 

#导入数据
x = ["战狼2","速度与激情8","功夫瑜伽","西游伏妖篇","变形金刚5：最后的骑士","摔跤吧！爸爸","加勒比海盗5：死无对证","金刚：骷髅岛","极限特工：终极回归","生化危机6：终章","乘风破浪","神偷奶爸3","智取威虎山","大闹天竺","金刚狼3：殊死一战","蜘蛛侠：英雄归来","悟空传","银河护卫队2","情圣","新木乃伊",]
y = [56.01,26.94,17.53,16.49,15.45,12.96,11.8,11.61,11.28,11.12,10.49,10.3,8.75,7.55,7.32,6.99,6.88,6.86,6.58,6.23]

#设置图形大小
plt.figure(figsize = (25, 8), dpi = 80) 

#使用barh(x,y)绘制横向条形图
plt.barh(range(len(x)), y, label = "票房", color = "orange", height = 0.3) #横向表示时，条形框的粗细变为高低显示的height

#设置字符串到y轴 
plt.yticks(range(len(x)), x,fontproperties = my_font) #横向xticks也要变成yticks

#添加描述信息
plt.xlabel("票房（单位：亿元）", fontproperties = my_font) 
plt.ylabel("电影名", fontproperties = my_font) 
plt.title("2017年内地电影票房前20的电影", fontproperties = my_font) 

#自定义网格
plt.grid(alpha = 0.4, linestyle = "--") 

#添加图例
plt.legend(prop = my_font, loc = "upper right")

#展示图形
plt.show()
```


![png](output_70_0.png)


### 动手
假设你知道了列表a中电影分别在2017-09-14(b_14), 2017-09-15(b_15), 2017-09-16(b_16)三天的票房,为了展示列表中**电影本身**房以及同其他电影的数据**情况**该如何更加直观的呈现该数据?
- a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
- b_16 = [15746,312,4497,319]
- b_15 = [12357,156,2045,168]
- b_14 = [2358,399,2358,362]
- 数据来源: http://www.cbooo.cn/movieday


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager 

#设置字体来源
my_font = font_manager.FontProperties(fname = "/Windows/Fonts/msyh.ttf") 

#导入数据（x列表标签过长，可以用\n来分成两行显示）
a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
b_16 = [15746,312,4497,319]
b_15 = [12357,156,2045,168]
b_14 = [2358,399,2358,362]

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80) 

bar_width = 0.2 #设置一个常用的固定值，可随时方便变更（条形图粗细不能设置得太大，假如为0.4时，柱体会挤在一起）

#使用bar(x,y)绘制条形图
x_14 = list(range(len(a)))
x_15 = [i + bar_width for i in x_14]           
x_16 = [i + bar_width * 2 for i in x_14]   
            
plt.bar(x_16, b_16, label = "9月16日票房", width = bar_width) 
plt.bar(x_15, b_15, label = "9月15日票房", width = bar_width)
plt.bar(range(len(a)), b_14, label = "9月14日票房", width = bar_width)

#设置x轴的刻度，将字符串传到x轴
plt.xticks(x_15, a ,fontproperties = my_font) #使用参数x_15可以使得字符串在条形图中间显示

#添加描述信息
plt.xlabel("电影名", fontproperties = my_font) 
plt.ylabel("票房（单位：亿元）", fontproperties = my_font) 
plt.title("各部电影三天的票房对比", fontproperties = my_font) 

#自定义网格
plt.grid(alpha = 0.4, linestyle = "--") 

#添加图例
plt.legend(prop = my_font, loc = "upper right")

#展示图形
plt.show()
```


![png](output_72_0.png)


#### 注意点
1、```plt.xticks(x_15, a ,fontproperties = my_font)```可修改为：

```_x_ticks = [i + bar_width for i in x_14]
plt.xticks(_x_ticks, a ,fontproperties = my_font)```则x轴标签的各个电影名仍会居于三天票房柱体中间

2、实际上```_x_ticks = [i + bar_width for i in x_14]```即是```x_15```

#### 分析：
- 由上表看出，三天票房最高的电影是猿球崛起3，其他几部电影票房底下，
- 原因估计是其它电影处于上映档期的后段，而猿星崛起3则在刚上映的阶段

### 条形图的更多应用场景
- 数量统计
- 频率统计(市场饱和度)

### 绘制直方图
- 技术要点：```plt.hist(a, num_bins)```
- 参数a为数据列表
- 参数num_bins为数据所分成的组数

### 动手
假设你获取了250部电影的时长(列表a中),希望统计出这些电影时长的分布状态(比如时长为100分钟到120分钟电影的数量,出现的频率)等信息,你应该如何呈现这些数据?
- a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]

#### 频数分布直方图


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]

#计算组数
dist = 3 #设置组距
num_bins = (max(a) - min(a)) // dist #取整使用地板除//

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制直方图
plt.hist(a, num_bins)

#设置x轴的刻度
plt.xticks(range(min(a), max(a) + dist, dist)) #x轴的刻度从最小值到最大值，取步长为dist，但由于range()函数不包括最后的值，所以为防止max(a)也可以含括在内，于是再加上一个组距dist

#绘制网格
plt.grid()

#展示
plt.show()
```


![png](output_79_0.png)


#### 把数据分为多少组进行统计???
- 组数要适当,太少会有较大的统计误差,大多规律不明显
- 组数：将数据分组，当数据在100个以内时，按数据多少常分为**5-12**组
- 组距：指每个小组的两个端点的距离
- 公式为：**$组数 = \frac{极差}{组距} = \frac{max(a) - min(a)}{bin_width}$**

#### 分析：
- 上图可以看出，时长105-141分钟之间范围内的电影出现的频率最多，都是2个小时左右的电影，而其他范围的则比较少
- 小于78分钟、87-90分钟、156分钟以上的电影几乎都没有，所以一般没有超过3个小时的电影
- 此图为**频数分布直方图**
- 将```plt.hist(a, num_bins)```修改为```plt.hist(a, num_bins, density = True)```后则变为**频率分布直方图**

#### 频率分布直方图


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]

#计算组数
bin_width = 3 #设置组距
num_bins = int((max(a) - min(a)) / bin_width) 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制直方图
plt.hist(a, num_bins, density = True)

#设置x轴的刻度
plt.xticks(list(range(min(a), max(a)))[::bin_width], rotation = 45) 

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_83_0.png)


- ```plt.hist(a, num_bins)```——传入需要统计的数据，以及数组即可
- ```plt.hist(a, [min(a) + i * bin_width for i in range(num_bins)])```——可以传入一个列表，长度为组数，值为分组依据，当组距不均匀的时候使用
- ```plt.hist(a, num_bins, density = True)```——参数```density:bool```是否绘制频率分布直方图，默认为频数直方图

### 动手问题：
在美国2004年人口普查发现有124 million的人在离家相对较远的地方工作。根据他们从家到上班地点所需要的时间,通过抽样统计(最后一列)出了下表的数据,**这些数据能够绘制成直方图么?**
- interval = [0,5,10,15,20,25,30,35,40,45,60,90] 【时间段】
- width = [5,5,5,5,5,5,5,5,5,15,30,60] 【组距】
- quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 【数据】
- 数据来源:https://en.wikipedia.org/wiki/Histogram
- 普查报告地址:https://www.census.gov/prod/2004pubs/c2kbr-33.pdf
- 如右图所示：![image.png](attachment:image.png)

### 回答：
- 问题问的是什么呢?问的是：**哪些数据能够绘制直方图**
- 前面的问题中给出的数据都是**统计之后的数据**，所以为了达到直方图的效果，**需要先绘制条形图**
- 所以：一般来说能够使用```plt.hist(a, num_bins)```方法的是那些**没有统计过的数据**，即是参数```a```是未经处理的原始数据

#### 初步编写代码：


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
interval = [0,5,10,15,20,25,30,35,40,45,60,90] 
width = [5,5,5,5,5,5,5,5,5,15,30,60] 
quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制条形图
plt.bar(range(len(quantity)), quantity ,width = width) #以参数quantity的长度与其自身绘制条形图，而width = width表示条形图每个柱体的宽度等于直方图的各个区间

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_88_0.png)


- 上图出现问题为：x轴标签有负数
- 由于三组数据的长度len(interval) = len(width) = len(quantity) = 12，不存在数据长度不一致的问题，说明数据本身没问题
- 同时条形图的宽度并非我们想象的直方图组距一样
#### 于是，先修改为一致的宽度，均为默认宽度，即删除width = width，如下所示：


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
interval = [0,5,10,15,20,25,30,35,40,45,60,90] 
width = [5,5,5,5,5,5,5,5,5,15,30,60] 
quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制条形图
plt.bar(range(len(quantity)), quantity) #删除了width = width

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_90_0.png)


- 上图来看，是一个条形图，要变成直方图的话，与直方图的区别在于：直方图是连续的变量，所以柱体是一个连在一起的
#### 继续修改为连续的柱体样子，即将柱体的宽度设置大一点，由于柱体默认宽度为0.8，于是可修改为width = 1，如下所示：


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
interval = [0,5,10,15,20,25,30,35,40,45,60,90] 
width = [5,5,5,5,5,5,5,5,5,15,30,60] 
quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制条形图
plt.bar(range(len(quantity)), quantity, width = 1) #修改width = 1

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_92_0.png)


- 连在一起后，新的问题点是：x轴的刻度是从-0.5开始的，而且各个刻度与区间不一致
#### 因此需要将x轴的0刻度位置往左移动0.5，如下所示：


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
interval = [0,5,10,15,20,25,30,35,40,45,60,90] 
width = [5,5,5,5,5,5,5,5,5,15,30,60] 
quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制条形图
plt.bar(range(len(quantity)), quantity ,width = 1)

#设置x轴的刻度
_x = [i - 0.5 for i in range(len(quantity))] #将x轴的0刻度位置往左移动0.5
_xtick_labels = interval 
plt.xticks(_x, _xtick_labels) 

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_94_0.png)


- 移动刻度对齐后，发现新问题：90刻度之后没有上限值，根据最后的区间为60，可知最后刻度为90+60=150
#### 进一步修改为：


```python
#导入模块
from matplotlib import pyplot as plt
from matplotlib import font_manager

#导入数据
interval = [0,5,10,15,20,25,30,35,40,45,60,90] 
width = [5,5,5,5,5,5,5,5,5,15,30,60] 
quantity = [836,2737,3723,3926,3596,1438,3273,642,824,613,215,47] 

#设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

#绘制条形图
plt.bar(range(len(quantity)), quantity ,width = 1)

#设置x轴的刻度
_x = [i - 0.5 for i in range(len(quantity) + 1)] #相应地_x的range(len(quantity))内部要加1，才能与下面_xtick_labels的+[150]的数相一致
_xtick_labels = interval + [150] #最后刻度在90以上后不显示，但为显示上限，_xtick_labels在原来的基础上加刻度150
plt.xticks(_x, _xtick_labels) 

#绘制网格
plt.grid(True, linestyle = "-.", alpha = 0.5)

#展示
plt.show()
```


![png](output_96_0.png)


### 直方图更多应用场景
- 用户的年龄分布状态（年龄为连续的数据）
- 一段时间内用户点击次数的分布状态（时间为连续的数据）
- 用户活跃时间的分布状态（时间为连续的数据）

### matplotlib常见问题总结
- 应该选择那种图形来呈现数据
- matplotlib.plot(x,y)
- matplotlib.bar(x,y)
- matplotlib.scatter(x,y)
- matplotlib.hist(data,bins,normed)
- xticks和yticks的设置
- label和titile,grid的设置
- 绘图的大小和保存图片

### matplotlib使用的流程总结
- 明确问题
- 选择图形的呈现方式
- 准备数据
- 绘图和图形完善

### matplotlib更多的图形样式
- 1、matplotlib支持的图形是非常多的，如果有其他的需求，可以查看一下[官网](http://matplotlib.org/gallery/index.html)url地址：
```http://matplotlib.org/gallery/index.html```
- 2、[百度Echarts](https://echarts.apache.org/examples/zh/index.html)：
```https://echarts.apache.org/examples/zh/index.html```

### 更多的绘图工具
- 1、**plotly**：可视化工具中的github，相比于matplotlib更加简单，图形更加漂亮，同时兼容matplotlib和pandas
- 使用用法：简单，照着文档写即可，**动态效果**
- [网址](https://plot.ly/python/)：```https://plot.ly/python/```
- 2、**seaborn**，只有**静态效果**：
- [网址](http://seaborn.pydata.org/)：```http://seaborn.pydata.org/```
