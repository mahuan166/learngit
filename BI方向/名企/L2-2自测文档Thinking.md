# Thinking1

`Q：MVC框架指的是什么`

`R：能简要说出MVC框架的内容（20points）`

`A：`

​         MVC全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范，用一种业务逻辑、数据、界面显示分离的方法组织代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。MVC被独特的发展起来用于映射传统的输入、处理和输出功能在一个逻辑的图形化用户界面的结构中。

​        MVC开始是存在于桌面程序中的，M是指业务模型，V是指用户界面，C则是控制器，使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。比如一批统计数据可以分别用柱状图、饼图来表示。C存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新。MVC 是一种使用 MVC（Model View Controller 模型-视图-控制器）设计创建 Web 应用程序的模式，同时提供了对 HTML、CSS 和 JavaScript 的完全控制。

**Model（模型）**是应用程序中用于处理应用程序数据逻辑的部分。
　　通常模型对象负责在数据库中存取数据。

**View（视图）**是应用程序中处理数据显示的部分。
　　通常视图是依据模型数据创建的。

**Controller（控制器）**是应用程序中处理用户交互的部分。
　　通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

​       MVC 分层有助于管理复杂的应用程序，因为您可以在一个时间内专门关注一个方面。例如，您可以在不依赖业务逻辑的情况下专注于视图设计。同时也让应用程序的测试更加容易。同时也简化了分组开发。不同的开发人员可同时开发视图、控制器逻辑和业务逻辑。

# Thinking2

`Q:基于Python的可视化技术都有哪些，你使用过哪些`

`R:分享自己使用过的工具（20points）`

`A:`

***基于Python的可视化技术***

- Matplotlib：基于Python的绘图库，提供完全的 2D 支持和部分 3D 图像支持。在跨平台和互动式环境中生成高质量数据时，matplotlib 会很有帮助。也可以用作制作动画。

- Seaborn：该 Python 库能够创建富含信息量和美观的统计图形。Seaborn 基于 matplotlib，具有多种特性，比如内置主题、调色板、可以可视化单变量数据、双变量数据，线性回归数据和数据矩阵以及统计型时序数据等，能让我们创建复杂的可视化图形。

- ggplot：ggplot是基于ggplot2, ggplot2是一个R语言作图系统。汲取*The Grammar of Graphics*书中的思想*.* ggplot 和matplotlib的作图方式不同，它是把元素一层一层地画在画布上（坐标轴，点，线等等）。而不是像matplot画x轴其实是把x轴属性设置一下而已。

- Bokeh：像ggplot一样，Bokeh也是汲取*The Grammar of Graphics*书中的思想，但是与ggplot不同的是，它是用Python写的，不是接R语言的。Bokeh优势在于和HTML，JSON应用结合的很好。而且对于流处理和实时数据支持的很好。Bokeh 支持高，中，低三种接口。最高级的接口可以直接用来话柱状图，盒图，线图，等等，只要你给JSON数据就行了。下一级接口有点像matplotlib，你要自己把图中的组件画出来。最底层的接口是专门给开发者的，这就给了你很多自定义的能力。

- geoplotlib：geoplotlib是用来画地图的。可以用来画等值区域图，热图，密度图等等。在使用前你必须先安装Pyglet（一个基于对象的编程接口）。

- pyecharts：pyecharts 是一个用于生成 Echarts 图表的类库。Echarts是百度开源的一个数据可视化 JS 库。实际上就是 Echarts 与 Python 的对接。

  

***使用过的基于Python的可视化技术***

​        使用过Matplotlib、Seaborn、ggplot、pyecharts。

举例（部分代码）：

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt  # 导入图像库
import statsmodels.tsa.stattools as ts
import seaborn as sns
import datetime

#导入数据  xq1,xq2,xq3

def box_test(xq1,xq2,xq3):

​    texts = xq1.columns.values.tolist()
​    da = xq1[0:7].sort_values(by=['日期'], ascending = [True]).reset_index(drop = True)
​    dat = da['星期']
​    kk1 = xq1[0:7].sort_values(by=['星期'], ascending = [True]).reset_index(drop = True)
​    kk2 = xq2[0:7].sort_values(by=['星期'], ascending = [True]).reset_index(drop = True)
​    kk3 = xq3[0:7].sort_values(by=['星期'], ascending = [True]).reset_index(drop = True)
​    data = (datetime.datetime.now()-datetime.timedelta(days=1)).strftime('%Y-%m-%d')
​    for i in range(3,len(texts)):
​       plt.rc("font",family="SimHei",size="15")  #解决中文乱码问题
​       fig,axes = plt.subplots(1,3,figsize=(25, 6),sharex=False,sharey=False)
​       sns.set(style="whitegrid")
​       dd1 =  pd.pivot_table(xq1,values=[texts[i]],index=['weeks'],columns=['星期'],aggfunc=[np.sum])
​       df1  = dd1['sum'][texts[i]]
​       dd2 = pd.pivot_table(xq2,values=[texts[i]],index=['weeks'],columns=['星期'],aggfunc=[np.sum])
​       df2 =  dd2['sum'][texts[i]]
​       dd3 = pd.pivot_table(xq3,values=[texts[i]],index=['weeks'],columns=['星期'],aggfunc=[np.sum])
​       df3 = dd3['sum'][texts[i]]
​       df1s = pd.concat([df1[dat[0]],df1[dat[1]],df1[dat[2]],df1[dat[3]],df1[dat[4]],df1[dat[5]],df1[dat[6]]],axis=1)
​       df2s = pd.concat([df2[dat[0]],df2[dat[1]],df2[dat[2]],df2[dat[3]],df2[dat[4]],df2[dat[5]],df2[dat[6]]],axis=1)
​       df3s = pd.concat([df3[dat[0]],df3[dat[1]],df3[dat[2]],df3[dat[3]],df3[dat[4]],df3[dat[5]],df3[dat[6]]],axis=1)
​       sns.boxplot(data=df1s,orient="v",color='cyan',ax=axes[0]) 
​       sns.boxplot(data=df2s,orient="v",color='lightcoral',ax=axes[1]) 
​       sns.boxplot(data=df3s,orient="v",color='gold',ax=axes[2]) 
​       df11 = np.zeros(df1.shape)
​       df12 = np.zeros(df2.shape)
​       df13 = np.zeros(df3.shape) 
​       df11 = pd.DataFrame(df11)
​       df12 = pd.DataFrame(df12)
​       df13 = pd.DataFrame(df13)
​       for j in range(0,df1.shape[1]):
​           df11[j] = df1.mean()[j+1]
​           df12[j] = df2.mean()[j+1]
​           df13[j] = df3.mean()[j+1]
​       df111 = np.zeros(df1.shape)
​       df112 = np.zeros(df2.shape)
​       df113 = np.zeros(df3.shape) 
​       df111= pd.DataFrame(df111)
​       df112 = pd.DataFrame(df112)
​       df113= pd.DataFrame(df113)
​       df11s = pd.concat([df11[dat[0]-1],df11[dat[1]-1],df11[dat[2]-1],df11[dat[3]-1],df11[dat[4]-1],df11[dat[5]-1],df11[dat[6]-1]],axis=1)
​       df12s = pd.concat([df12[dat[0]-1],df12[dat[1]-1],df12[dat[2]-1],df12[dat[3]-1],df12[dat[4]-1],df12[dat[5]-1],df12[dat[6]-1]],axis=1)
​       df13s = pd.concat([df13[dat[0]-1],df13[dat[1]-1],df13[dat[2]-1],df13[dat[3]-1],df13[dat[4]-1],df13[dat[5]-1],df13[dat[6]-1]],axis=1)
​       sns.swarmplot(data=df11s, color='black',ax=axes[0]) 
​       sns.swarmplot(data=df12s, color='black',ax=axes[1]) 
​       sns.swarmplot(data=df13s, color='black',ax=axes[2]) 
​       for m in range(0,df1.shape[1]):
​           df111[m] = kk1[texts[i]][m]
​           df112[m]  = kk2[texts[i]][m]
​           df113[m] = kk3[texts[i]][m] 
​       df111s = pd.concat([df111[dat[0]-1],df111[dat[1]-1],df111[dat[2]-1],df111[dat[3]-1],df111[dat[4]-1],df111[dat[5]-1],df111[dat[6]-1]],axis=1)
​       df112s= pd.concat([df112[dat[0]-1],df112[dat[1]-1],df112[dat[2]-1],df112[dat[3]-1],df112[dat[4]-1],df112[dat[5]-1],df112[dat[6]-1]],axis=1)
​       df113s = pd.concat([df113[dat[0]-1],df113[dat[1]-1],df113[dat[2]-1],df113[dat[3]-1],df113[dat[4]-1],df113[dat[5]-1],df113[dat[6]-1]],axis=1)
​       sns.pointplot(data=df111s, color='r',ax=axes[0]) 
​       sns.pointplot(data=df112s, color='r',ax=axes[1]) 
​       sns.pointplot(data=df113s, color='r',ax=axes[2])
​       plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
​       plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
​       datas = data + '       ' + texts[i]       
​       fig.suptitle(datas, fontsize = 17, fontweight='bold')
​       plt.xlabel('青绿色-XX  粉红色-XXX  黄绿色-XXXX')
​       plt.ylabel('红色--XX  黑色--XX')
​    return '完成'

box_test(xq1,xq2,xq3)