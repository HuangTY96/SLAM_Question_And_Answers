# SLAM_Question_And_Answers
Share all the questions related with SLAM

以问答形式对SLAM中常用的热点问题进行阐述，以帮助自己及有需要的读者，如有意合作，联系simiter@126.com

[TOC]

# 什么是齐次坐标？

[详细介绍点这里](https://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485921&idx=1&sn=dfccfc8772d4905c744cab53c3c4c7b3&chksm=97d7ec76a0a065608fda155f6de835c534fa2b012b6659d317c279181e040480e6b883867d14&scene=21#wechat_redirect)

简单的说：齐次坐标就是在原有坐标上加上一个维度：
简单的说：齐次坐标就是在原有坐标上加上一个维度：
$$
\begin{array} { r l } { ( x , y ) } & { \rightarrow ( x , y , 1 ) } \\ { ( x , y , z ) } & { \rightarrow ( x , y , z , 1 ) } \end{array}
$$

## 使用齐次坐标有什么优势？

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wCH8qOTKicZwJyEoDBvgpIERVVSIPyKVGibLWswEfuAN5y9nXqGwa3PvA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 使用齐次坐标有什么优势？

齐次坐标的使用能够大大简化在三维空间中的点线面表达方式和旋转平移等操作，具体分如下几点进行说明。

### 能否非常方便的表达点在直线或平面上

在2D平面上，一条直线 l 可以用方程 ax + by + c = 0 来表示，该直线用向量表示的话一般记做

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wtmZ7Fibiat4LeYMl3X7syf8M053HywtegoSo2MqALfb1UxPSXhY7KS2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我们知道点p = (x, y)在直线 l 上的充分必要条件是 ax + by + c = 0

如果使用齐次坐标的话，点p的齐次坐标就是 

p'=(x, y, 1)

那么 ax + by + c = 0 就可以用两个向量的内积（点乘）来表示：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wjiaksbibkLZpibrPDuiaicxoyk5dAjEp8AOtTrUSor6Nn5xXLItEPwbfhNA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

因此，点p在直线l上的充分必要条件就是 直线l 与p的齐次坐标p'的内积：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wsqjaWRw1zxOZzOmocK1TQgdKH1fT3jDFqdrEe28yuY3e0icUBfoL2Dw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

是不是很方便呢！



同理，我们知道 三维空间的一个平面A可以用方程 ax + by + cz + d = 0 来表示，三维空间的一个点P=(x, y, z) 的齐次坐标 P'=(x, y, z, 1)，类似的，点P在空间平面A上可以用两个向量的内积来表示，如下：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wjzrCHJlv3IynOibAkgr6hXdn6EDA37lRAe9NSvwS1wNlow8V2cpfzeA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

因此，点P在平面A上的充分必要条件就是平面A 向量与P的齐次坐标P'的内积（点乘）：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wTA8IK5r0bCBGRXBWZbGx177GxiaFn3LPyXiaogib9rESsDibWwBDFp8kEQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 方便表达直线与直线，平面与平面的交点

先给出结论，后面再具体解释：

**结论：在齐次坐标下，可以用两个点 p, q 的齐次坐标叉乘结果来表达一条直线 l，也就是**

**l = p x q**

**也可以使用两条直线 l, m 的叉乘表示他们的交点 x**

**x = l x m**

见下面示例图。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08w6SIfl1iavAJ3SibBiaOlXicbxu4rABtZjLHVIAD0BeSmDjcVzdSwwB4jRA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

之所以可以这么简洁的表示交点是因为采用了齐次坐标的表示方式。

那么这是为什么呢？



先介绍一下叉乘（也称叉积、外积）的概念：



两个向量 a和b 的叉乘仅在三维空间中有定义，写作  a x b

a x b 是与向量 a, b都垂直的向量，其方向通过右手定则（见下图）决定。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wTYlUZW9ib6wIYaQP6STmTk1iboCpwCgA2xeFR5iciaU82rDNPnUjOW4EBw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其模长等于以两个向量为边的平行四边形的面积（见下图）。

叉乘可以定义为：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wbQfw0rYlkibqxsZsWGChDHzZEHpO3rdpeCOAEWy5Zh6xuGPf6SMdSyw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其中 θ表示a, b的夹角（0°到180°之间），||a||, ||b||是向量a, b的模长

 n则是一个与向量a, b所构成的平面垂直的单位向量

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wvtHLt9mVJIMd8bKyiaOWcN17occSE3fqUNYmpichS1JQPVydSYTY5I2g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

根据叉乘定义：

向量自身叉乘结果为0，因为夹角为0。也就是说三维向量 a x a =0, b x b = 0而点乘（也称点积，内积）的定义是

a * b = ||a||* ||b|| *cos(θ)



根据定义：如果两个向量垂直，cos(θ) = 0，点积也为0。



好了，经过上面点乘和叉乘定义的铺垫。下面来推导一下上面的结论：



为什么两条直线 l, m 的叉乘 l x m 等于它们的交点 p，也就是 p = l x m？



原因如下：首先，根据前面叉乘的定义，l x m 的结果向量（记为 p = l x m） 与 l 和 m都垂直，根据点乘的定义，垂直的向量之间的点积为0，因此可以得到：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wy7LoAdEeyYO6exliahgxDoWKaX9K3H0WQSuWb6JAKpnOp9MF27L3KfQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

因此，根据前面点在直线上的结论，可以看到p既在直线l 上又在直线m上，所以  p = l x m 是两条直线的交点。此处 p 是齐次坐标。



同样的，可以证明，两点p, q 的叉乘 可以表示 过两点的直线l，即 l = p x q。

### 能够区分一个向量和一个点

(1)从普通坐标转换成齐次坐标时

   如果(x,y,z)是个点，则变为(x,y,z,1);

   如果(x,y,z)是个向量，则变为(x,y,z,0)

(2)从齐次坐标转换成普通坐标时   

   如果是(x,y,z,1)，则知道它是个点，变成(x,y,z);

   如果是(x,y,z,0)，则知道它是个向量，仍然变成(x,y,z)

[具体解释](http://www.cnblogs.com/csyisong/archive/2008/12/09/1351372.html)

### 能够表达无穷远

比如 两条平行的直线 ax+by+c=0, ax+by+d=0，

可以分别用向量 l = (a, b, c), m = (a, b,d)表示

根据前面直线交点的计算方法，其交点为 l x m

根据叉乘计算法则

向量

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wfNMiaUT5bQvun4KFciatldy9Uq62kuAvx5uwd13rH7FZCYdIDAN62aBw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

的叉乘结果可以用如下方法计算得到

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wE3shbR0x7o687Bh6VtWR5tZukArToHazeQ1vBMJicib2RmuZc3HQ3qvA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最终：l x m = (d-c)(b,-a,0)，忽略标量(d-c)，我们得到交点为(b,-a,0)，并且是齐次坐标，如果要转化为非齐次坐标，那么会得到 (b/0, a/0)，坐标是无穷大，可以认为该点为无穷远点，这与我们通常理解的：平行线相交于无穷远的概念相吻合。



因此，如果一个点的齐次坐标中，最后一个元素为0，则表示为无穷远点。

### 更简洁的表达欧氏空间变换

这是齐次坐标最重要的一个优势之一。在以后的学习中你会更加深刻的理解。



使用齐次坐标，可以方便的将加法转化为乘法，方便的表达平移。



比如我们要完成将2D坐标点x=[u,v]' 平移t=[tu, tv]，如果用非齐次方法的话，是用如下的加法

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wL6cVP659FbQcedL93P9H0vIDSFibDBBuEqYiaYVnZaU0bkK0AsUycsbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如果用齐次坐标表示时可以将加法转换为乘法

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wibr5TNIu3OX64fUqq8mJUrWHaa5uJMjrUDAvHMmX4zcMVAR58k5y5gQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在欧氏变换中一般有两种操作：旋转和平移。



如果我们想要将向量a进行一个标准的欧氏变换，一般是先用旋转矩阵R进行旋转，然后再用向量t进行平移，其结果a' = R*a + t，这样看起来没什么问题。



但是，我们知道SLAM中一般都是连续的欧氏变换，所以会有多次连续的旋转和平移，假设我们将向量a进行了两次欧氏变换，分别为R1, t1 和 R2，t2，分别得到：

b = R1*a + t1,  c = R2*b + t2

最终的结果 c = R2*(R1*a + t1) + t2



显然，这样的变换在经过多次后会变的越来越复杂。其根本原因是上述表达方式并不是一个线性的变换关系。



此时，齐次坐标就显示出它的魅力了，如果使用齐次坐标来表达 a' = R*a + t 的话可以写为：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wcAt8mT1qjyPkvraH4BwXLu4ricn9VyZ7f0Hp7GfofyggtGdq8Quhdyg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

旋转和平移可以用一个矩阵T来表示，该矩阵T称为变换矩阵（transform matrix），这样欧氏变换就变成了线性关系，进行多次欧氏变换只需要连乘变换矩阵就行了，比如前面的两次欧氏变换使用齐次坐标就可以表示为：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNle3AGYGXwhKEKPYFFict08wVaYhVnvIOAdfzeLpxibRkn0thOXS5eW0S6kgsVBsIIpQic492ZDnapGQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其中，波浪号代表齐次坐标。一般的，在SLAM中，b = Ta 的形式默认都是齐次坐标。

# 三维空间中刚体的旋转如何表示？

三维空间中刚体的旋转总共有4种表示方法，高翔的十四讲中的第3讲比较详细的讲解了。这里有一个[详细归纳介绍](https://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485988&idx=1&sn=eaec2aa09cb4baeae36d2f669cc89174&chksm=97d7efb3a0a066a50e8ad29f05fe595a304dd19cc55be0edbe83969c3288b97f2fecc77cd440&scene=21#wechat_redirect)

## 旋转矩阵

1. SLAM编程中使用比较频繁。需要重点掌握。

1. 旋转矩阵不是一般矩阵，它有比较强的约束条件。旋转矩阵R具有**正交性，R和R的转置的乘积是单位阵，且行列式值为1**。

1. 旋转矩阵R的逆矩阵表示了一个和R相反的旋转。

1. 旋转矩阵R通常和平移向量t一起组成齐次的变换矩阵T，描述了欧氏坐标变换。**引入齐次坐标是为了可以方便的描述连续的欧氏变换**，这个在《[为什么要用齐次坐标？](http://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485921&idx=1&sn=dfccfc8772d4905c744cab53c3c4c7b3&chksm=97d7ec76a0a065608fda155f6de835c534fa2b012b6659d317c279181e040480e6b883867d14&scene=21#wechat_redirect)》中有讲解。

1. 冗余。用9个元素表示3个自由度的旋转，比较冗余。

## 四元数

1 .SLAM编程中使用频繁程度接近旋转矩阵。稍微有点抽象，不太直观，但是一定得掌握。

2 .四元数由一个实部和三个虚部组成，是一种**非常紧凑、没有奇异**的表达方式。

3 .编程时候很多坑，必须注意。首先，一定要**注意**四元素定义中**实部虚部**和打印系数的**顺序**不同，很容易出错！

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnhZHwre77bNREbMXSIoshfbibibDVqaFcibeABoDlLJgVGQLrldr7Ac1h731yv2FFrE7LhYS8iavicNCQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其次，单位四元素才能描述旋转，所以四元素使用前必须**归一化**：q.normalize()。

## 旋转向量

1. 用一个旋转轴n和旋转角θ来描述一个旋转，所以也称轴角。不过很明显，因为旋转角度有一定的周期性（360°一圈），所以这种表达方式具有奇异性。

1. 从旋转向量到旋转矩阵的转换过程称为 罗德里格斯公式。这个推导比较麻烦，否则也不会有一个专属的名字了。OpenCV和MATLAB中都有专门的罗德里格斯函数。

1. 旋转向量本身没什么出彩的，不过**旋转向量和旋转矩阵的转换关系，其实对应于李代数和李群的映射**，这对于后面理解李代数很有帮助。

## 欧拉角

1. 把一次旋转分解成3次绕不同坐标轴的旋转，比如航空领域经常使用的“偏航-俯仰-滚转”（yaw，pitch，roll）就是一种欧拉角。该表达方式最大的优势就是直观。

1. 欧拉角在SLAM中用的很少，原因是它的一个致命缺点：**万向锁**。也就是在俯仰角为±90°时，第一次和第3次旋转使用的是同一个坐标轴，会丢失一个自由度，引起奇异性。事实上，想要表达三维旋转，至少需要4个变量。

# SLAM为啥需要李群与李代数？

[有趣又详细的解释在这里](https://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247486047&idx=1&sn=25d97bb47c26ac3babafd668ee0c013b&chksm=97d7efc8a0a066de0990dc79de32c666aff4698aa1f8dbfc131cc426e6beba96cd5260d0a667&scene=21#wechat_redirect)

## 为啥需要李代数？

小白：师兄，我最近在学习SLAM，看到李群、李代数这一块一直看不懂，不知所云啊，师兄能不能用通俗易懂的方式给我讲解一下？

师兄：好啊，正好这会有空，讲完正好去吃饭。

小白：我请师兄吃烧烤！

师兄：哈哈，那我必须给你讲明白啦！现在开始吧。

小白：好，先问下师兄，我在看高博的书，前面几章挺顺利的，第四章突然跳出来李群和李代数，一堆公式推导，看的我头都大了。

师兄：这部分公式是有点多，不过李群李代数是为了解决SLAM中非常实际的问题的。到后面会用到的。

小白：看来逃不过啊。。。

师兄：是的，这部分必须理解的啊。刚才说到了解决SLAM中实际问题，我展开说下。我们知道SLAM的过程就是不断的估计相机的位姿和建立地图。其中，相机位姿也就是我们所说的变换矩阵T。

小白：嗯嗯，是。上节课《[三维空间刚体的旋转](http://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485988&idx=1&sn=eaec2aa09cb4baeae36d2f669cc89174&chksm=97d7efb3a0a066a50e8ad29f05fe595a304dd19cc55be0edbe83969c3288b97f2fecc77cd440&scene=21#wechat_redirect)》中还讲了变换矩阵呢！

师兄：对~下面举个例子说明。比如你拿着相机一边移动一边拍，假设某个时刻相机的位姿是T，它观察到一个在世界坐标系中的一个空间点p，并在相机上产生了一个观测数据z，那么

z = Tp + noise

noise是观测噪声。那么观测误差就是

e = z - Tp

小白：嗯，我 知道，我们的目的就是使得误差最小咯~

师兄：对的，假设我们总共有N个这样的三维点p和观测值z，那么我们的目标就是寻找一个最佳的位姿T，使得整体误差最小化，也就是

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQJMWXHdXYNbBSF7y1PJdSCytNhkw01qZePrJ2eJuvVa3vTpSbFbSE4w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



求解此问题，就是求目标函数J对于变换矩阵T的导数。

小白：嗯，对矩阵求导？第一次 听说啊。。

师兄：听起来确实有点怪。我们先来看看变换矩阵T，我们知道T所在的SE(3)空间，对加法计算并不封闭，也就是说任意两个变换矩阵相加后并不是一个变换矩阵，这主要是因为旋转矩阵对加法是不封闭造成的，它是有约束的。

小白：旋转矩阵对加法不封闭啥意思？

师兄：嗯，这个我一会会细讲，这里你先记住好了。到后面你就知道了

小白：好的，那刚才的问题怎么解决呢？

师兄：这个问题问的好，李代数就是解决这个问题的。我们把大写SE(3)空间的T映射为一种叫做李代数的东西，映射后的李代数我们叫做小se(3)好了。它是由向量组成的，我们知道向量是对加法封闭的。这样我们就可以通过对李代数求导来间接的对变换矩阵求导了。

## 李群怎么理解？

师兄：不急，我一个个说。我先说说李群吧，额，不，先说说群吧。按照数学上定义：群（group）就是一种**集合**加上一种**运算**的代数结构。群有几个运算性质，好像高博说是“凤姐咬你”

小白：（瞪大了眼睛）嗯？

师兄：哦，谐音谐音。。。就是：封闭性，结合律，幺元，还有逆。对了，比如旋转矩阵和乘法就构成了旋转矩阵群，变换矩阵和乘法也构成了变换矩阵群。对了，你说，旋转矩阵和加法能构成群吗？

小白：额。。刚才好像说不行吧？

师兄：嗯，不行的 ，他们不满足封闭性。刚才没有细讲，下面仔细解释原因。我们知道旋转矩阵R本身有一定的约束：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQOcicCXId6IXLhQHnOIW1ntrpeJc3d0GN8I1rBg4JsAsJDaexB0oLvNA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



两个旋转矩阵R1+R2的结果就不能满足上述约束了，但是R1*R2满足。此外，旋转矩阵还满足结合律：R1*R2=R2*R1，还有幺元是单位矩阵I，也有逆矩阵满足R乘以R的逆等于幺元（单位阵）。还有，我们在SLAM里最常说的有两个，一个是特殊正交群SO(3)，也就是旋转矩阵群，还有特殊欧氏群SE(3)，也就是变换矩阵群，3代表是三维的。

小白：嗯嗯，书上看了，我差不多理解群是个什么东东了，那李群呢？

师兄：李群的定义是指连续光滑的群，比如我们前面说的旋转矩阵群SO(3)，你想象你拿个杯子就可以在空间中以某个支点连续的旋转它，所以SO(3)它就是李群。如果你一般旋转一边移动它，也是连续的或者说光滑的运动，所以变换矩阵群SE(3)也是李群。

## 李代数是李群的亲戚吗？

小白：嗯，师兄，那李代数呢，它和李群都姓李，他们什么关系？

师兄：（一脸黑线）我个人的理解是这样的，就是我们相机在三维空间中是连续的旋转或者变换的嘛，刚才说过，而我们SLAM目的就是优化求解相机的这个最佳的位姿T（变换矩阵），优化方法一般都采用迭代优化的方法，每次迭代都更新一个位姿的增量delta，使得目标函数最小。这个delta就是通过误差函数对T微分得到的。也就是说我们需要对变换矩阵T求微分（导数），我们先以SO(3)空间中的旋转矩阵 R为例来说说吧，你觉得如何对R求微分呢？

小白：矩阵怎么求。。求微分，这个能微分吗？以前没有学过啊

师兄：可以的，李群和李代数都姓李（笑），你还别说，他们之间的确存在某种微分关系。我们先把结论放这里：**李代数对应李群的正切空间，它描述了李群局部的导数**。

小白：也就是说，李代数对应了李群的导数？

师兄：可以这么理解，你可以去看一下十四讲中65-66页那部分的推导，我们只关注两个结论就行了

第一个结论：

看下面的公式，我们发现旋转矩阵的微分是一个反对称(也叫斜对称)矩阵左乘它本身，也印证了我前面说的，矩阵是可以微分的。**对于某个时刻的R(t)（李群空间），存在一个三维向量φ=（φ1，φ2，φ3）（李代数空间），用来描述R在t时刻的局部的导数**。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQ3dfzYVfqDscrlE2lDDy0vQo22AaIL1FJicjWNN0LYzdgdPY1GkJuLjQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 反对称矩阵是啥？

小白：等一下，师兄，反对称矩阵是啥？第一次听说啊

师兄：哦哦，忘记解释了。反对称矩阵英文是skew symmetric matrix，有的地方也翻译为斜对称矩阵，其实是一个东西。

小白：这个反对称矩阵是啥意思？

师兄：反对称矩阵其实是将三维向量和三维矩阵建立对应关系。它是这样定义的：如果一个3 X 3的矩阵A满足如下式子

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQTgnToXgXlxoKN5QTzp099npYa998CiaUKWTPYK6YAfaZQCnuYA6UibZw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



那么A就是反对称矩阵。你看左边有个转置，右边有个负号，叫反对称矩阵，还是挺形象的。

小白：额，好像有点明白，不过这个有啥用啊？

师兄：先别急，先问你一个问题，你觉得反对称矩阵它的元素有什么特点？

小白：啊。。特点啊，我想想（一分钟过去了。。）

师兄：根据它的性质，先想想对角线元素。你看，上式等式左边矩阵A转置后，对角线元素aii是不是还在对角线上？

小白：对哦，师兄好厉害

师兄：额。。别打岔，等式右边，所有元素取负号，那么对于对角线元素aii来说，是不是满足aii=-aii？

小白：是哦，所以aii=0，也就是说反对称矩阵对角线元素都为0？

师兄：bingo！确实是这样。那么非对角线元素还有6个，它们能不能精简呢？

小白：我想想，感觉好像是有重复的，好像可以用更少的元素来表示

师兄：没错！我举个例子，等式左边第2行第1列位置的元素，是矩阵A元素a12转置后到了位置a21，等式右边原来a21变成了 -a21，所以其实对于矩阵A，元素a12 = -a21，所以用一个元素及其负数就可以表示矩阵中这两个元素，同理，其他4个元素也是这样。所以，其实矩阵A中非对角线元素只用3个元素就可以表示。也就是说反对称矩阵A只有3个自由度。

小白：嗯呢，师兄好厉害！不过。。。知道这些有啥用啊？

师兄：这个反对称矩阵只有3个自由度很重要啊，这样我们就可以把一个三维向量和一个三维矩阵建立对应关系。

小白：师兄，感觉还是很抽象啊

师兄：哦哦，那我举个栗子给你看看。我们假设有一个反对称矩阵A的定义如下：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQE8pkX9hQichp7z1226Ribmp8DvtOsSZWxvEf75p6ZRGSYPvNaEUiahxQw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：等下，我看看是否满足性质：该矩阵的转置等于该矩阵元素取负数。。

师兄：你看是不是我们前面推算的一致啊，对角线元素为0，只有3个自由度？

小白：是哦，确实没错！师兄继续。。

师兄：我们定义对应的一个三维向量：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQevrfE1sbm4s5xE6W9wJeIIeMTYHBVPsrs0TuoJp98BIQR35VFib841g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



然后我们用一个上三角符号来表示这个向量α和三维矩阵A的对应关系

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQXXkUVen0qmibhA9OZlrWzGEtdoiagLxYmyJmRednt99s6ibmad9qBiaJDg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：这个符号感觉很神奇啊

师兄：是的，通过这个符号，我们把向量和矩阵建立了对应关系。这个在后面非常重要。你再看看前面的第一个结论

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQ3dfzYVfqDscrlE2lDDy0vQo22AaIL1FJicjWNN0LYzdgdPY1GkJuLjQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



就好理解很多了。

## 指数映射是啥?

师兄：好 ，下面说说第二个结论。通过高博一系列辛苦的 计算（笑），我们最终得到下面式子，它的前提是R在原点附近的一阶泰勒展开，我们看到这个向量φ=（φ1，φ2，φ3）反应了R的导数性质，故称它在SO(3)上的原点 φ0 附近的正切空间上。这个φ正是李群大SO(3)对应的李代数小so(3)。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQHLDzB8N6XTGqs8I8LdSTibVuUWknqGgXDORYvdp2TjfhdYdVsWCVnfA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：好晕啊。。

师兄：你这么理解吧，李代数小so(3)是三维向量φ的集合，每个向量φi的反对称矩阵都可以表达李群(大SO(3))上旋转矩阵R的导数，而R和φ是一个指数映射关系。也就是说，李群空间的任意一个旋转矩阵R都可以用李代数空间的一个向量的反对称矩阵指数来近似。

小白：好绕的绕口令啊。。

师兄：没事，你只要记得用旋转矩阵表示的话就是李群空间，也是我们熟悉的表示方法。而用向量的反对称矩阵表示的话就是李代数空间，这两个空间建立了联系。

小白：师兄，那这个古怪的式子

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQJ64Xs5exoUdzayAiaBET23Eb1Nn5iccZKnVZiczS5nBPWbxZWarAHrQ3Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



如何计算呢？

师兄：嗯，这个用大一学的微积分就行。

小白：微积分忘的差不多了。。。

师兄：没事，其实就只用到指数e的泰勒展开

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQu4F56nwhv4h92Z1gpp0jGCtrfQxCgPrc8yyXBxGm3pYVUrAH7srvlA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：师兄，书上的推导好麻烦啊

师兄：先不管具体推导过程，我们先来看看结论，你说的那个指数形式的古怪的式子通过运用泰勒展开，以及反对称矩阵的性质，我们可以得到如下结果：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQc2y4Uyt37PfProhBiclVyEWiceMIpKa2iaQfSmLx00l0Uxop76b0lC5bA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



其中：三维向量 φ = θa，a是一个长度为1的方向向量。看到这个式子有没有觉得很神奇？

小白：好像在哪里见过啊

师兄：嗯，这个式子和罗德里格斯公式长的一模一样

小白：忘了什么是罗德里格斯公式了。。。

师兄：你还记得旋转的表示方法吗？有旋转矩阵、旋转向量、欧拉角、四元数，而**罗德里格斯公式是表示从旋转向量到旋转矩阵的转换过程**的

小白：师兄这么一说，我想起来了，旋转向量也有一个旋转角θ，旋转轴也是单位方向向量

师兄：其实旋转向量就是这里的李代数

小白：啊？这怎么会扯上关系？

师兄：你可能有点反应不过来，不过的确**小so(3)的李代数空间就是由旋转向量组成的的空间，其物体意义就是旋转向量。而前面结论二中的指数映射关系就是罗德里格斯公式，他们在数学上本质是一样**的

小白：真的好神奇啊

师兄：嗯，这样我们可以说旋转矩阵的导数可以由其对应的旋转向量指定，指导如何在旋转矩阵中进行微积分运算。

小白：这样就好理解多了

## 李群李代数之间如何互相转换？

师兄：嗯，反过来，用对数映射也能把大SO(3)李群空间中元素映射到小so(3)李代数空间中去。前面我们都是讲的SO(3)上的映射关系，放到SE(3)上推导类似，也是泰勒展开，旋转矩阵R映射结果和SO(3)一样，平移部分指数映射后会有稍许的不同，它前面多了一个系数矩阵，这些都可以自己证明一下（留作作业）。

小白：嗯嗯，师兄，是不是只要记住高博大神书上的对应关系图就行啦？

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQtPxWqCZKBuoLicFUrIiazEJ34vgicNib8RThTV3pwNYcW9FPl6QTg8nftA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



师兄：这个图要理解透彻

小白：对了，师兄，好像还有一个左扰动，右扰动什么的，这个是干什么用的呀

师兄：这个是用李代数解决求导问题时使用的方法。对了，李代数是对加法封闭的吗？

小白：嗯，李代数是由向量组成的，向量对加法运算是封闭的。

师兄：嗯，学的真快！你说的没错。李代数求导分两种：一种是用李代数表示位姿，然后根据李代数加法来对李代数求导。这种方法书中也推导了，结果中有复杂的雅克比公式，不是很方便。一般都用第二种，就是对李群进行左乘或者右乘微小的扰动，然后对该扰动求导。书上高博也推导了，你看结果还是挺简洁的。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNkg5icRTC7h4qHibqNpgnstOQpBbTwqShyfW67z9oQ3rcXutP7Nx8OR5SheicFF1DPRI3rjD6Qoo2Kjg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：那我们就用扰动模型好啦

师兄：确实实际SLAM问题中，扰动模型比较实用方便。扰动模型的推导一定要自己推一遍哦

## 疑难公式推导

[SO(3)左扰动模型，SO(3)李代数求导，SE(3)左扰动模型 公式推导视频讲解](https://v.qq.com/x/page/p0758q8ohvo.html?start=1)

# 如何理解相机成像模型？

[详细介绍在这里](https://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247486116&idx=1&sn=38252b8f03ef16122e3ac494d7ec8740&chksm=97d7ef33a0a06625b34d491fc83c5e6e820baa11c6f9f0c113e32fdb7c7bf1e04e40fd8019ab&scene=21#wechat_redirect)

## 如何理解小孔成像？

师兄：相机成像模型我们主要介绍针孔相机。中学时我们都学过小孔成像，还记得吧。像下面这个图，就是小孔成像示例。你看三维空间的蜡烛在带有小孔的黑箱子里成像一个倒立是像，这个是实像

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqFqFsjO0uDTtaO0Fap70HBM1qPNCWrkIF93bVgs6fsyCwo5t97xLicNQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：嗯嗯，还有印象，那个正立的虚线画的就是虚像吧

师兄：是的。话说几千年前人们就发现了这个现象了~

![img](https://mmbiz.qpic.cn/mmbiz_jpg/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqFyPO4zMwLNI0zhOEdJuYdJAIJocswGzfRZZffHNlFRhGaEUaG71icJg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：那师兄为啥要画这个虚像呢？

师兄：因为这个虚像和实像是完全对称的，数学上可以等价，后面我们推导公式的时候比较方便。

小白：这样啊，还有个问题，为啥我看好多书上提到相机模型都是讲的针孔相机？

师兄：因为自然界中这个成像过程最普遍，我们普通的相机，视场角不太大的话都符合针孔相机成像模型

小白：可是，普通相机好像没有针孔那么小。。。

师兄：哈哈，这个针孔是个类比，比如手机摄像头镜头相对于被拍摄物体到手机的距离就非常小了，可以近似为一个针孔的

小白：糗大了。。。

师兄：没事，不懂就问不能不懂装懂嘛。我们继续，前面针孔相机用数学表达就是下面这样。我们把倒立的实像去掉，用正立的虚像代替就行啦。三维空间的点大P在成像平面上成的像就是小p了。大P，小p还有相机中心C在同一条直线上。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqWEQmB4YiaY0dUxhfozM8gU1Jtv0Pz77ojr3pOKfeADYsiawg4CicRiby2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 世界坐标系、相机坐标系、图像坐标系有什么区别和联系？

师兄：下面我们即将进入公式的世界，yeah~

小白：师兄，我数学是语文老师教的。。。尽量通俗易懂的讲哈

师兄：嗯，第一步，我们先要明白，这个三维空间有好多坐标系，一个，两个。。大概有三四个吧。

小白：（捂脸）

师兄：首先说两个，世界坐标系和相机坐标系。顾名思义：



**世界坐标系(world coordinate system)**：就是用户定义的三维世界的坐标系，以某个点为原点，为了描述目标物在真实世界里的位置而被引入。单位为m。

**相机坐标系(camera coordinate system)**：就是以相机为原点建立的坐标系，为了从相机的角度描述物体位置而定义，作为沟通世界坐标系和图像/像素坐标系的中间一环。单位为m。



小白：师兄，你说的好学术啊，这俩有啥不一样？

师兄：举个栗子吧。比如姚明要开始100米跨栏了，我们可以定义那个起点就是世界坐标系原点。。

小白：打住。。。姚明好像是打篮球的吧？

师兄：哦哦，对，说错了，是刘翔在世界坐标原点（在师妹面前糗大了）。那么，那么那个拍照的摄影师，对，那个摄影师假如是姚明，那么姚明所在的位置就是相机坐标系的原点，这时候刘翔在相机坐标系中就不是原点了。

小白：理解~

师兄：我们举个普通的例子，比如下面这个图，最右上方的那个点在三维空间中，如果以世界坐标系为原点，它的坐标就是Xw，如果以相机坐标系为原点，它的坐标就是Xc，我们可以通过旋转R和平移t来把世界坐标系转换到和相机坐标系重合

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9Fdkq81mmDiajedNictbLiaMLOAwCyWjfo6FDibu6yhll9lwKZOYjC6lKlic1JxA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：这个R，t就是之前我们讲过的变换矩阵吧

师兄：对啊，如果用数学公式表示的话，就是下面这个啦，我们在《[从零开始一起学习SLAM | 为什么要用齐次坐标？](http://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485921&idx=1&sn=dfccfc8772d4905c744cab53c3c4c7b3&chksm=97d7ec76a0a065608fda155f6de835c534fa2b012b6659d317c279181e040480e6b883867d14&scene=21#wechat_redirect)》还讲了为什么要使用齐次坐标，还记得吧？

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9Fdkqd9XS8IKsFBfE3fc5iaicMJIBUz4dwSPHqVWRpOwYebG5Jpa0rYBicBB4w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：记得呢，我有复习过的哦（顿时感觉自己也没有那么小白了），嘻嘻

师兄：不错。这个R,t 为就是相机的外部参数，一般用T表示，这个参数随着相机的移动而变化。下面我们假设已经把世界坐标系变换到相机坐标系下了。

我们再来说一下**图像坐标系(image coordinate system)**吧，它是为了描述成像过程中物体从相机坐标系到图像坐标系的投影透射关系而引入，是我们真正从相机内读取到的图像所在的坐标系。单位为像素。

## 针孔相机成像模型如何理解？

我们来看看下面这个图吧。相机坐标系下的点P(X, Y, Z)在相机成像平面上成的像为P'(X', Y', Z')

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqZkryricQ9xcwx1TS6Xy6gJ1lsLmSP3YicZ7H8YCK47G6FCSUDKqUibR5Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



那么根据三角形相似原理，如右图所示，能推导出如下式子

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqDgMJdErqibIoc2ibKNMqXRLeMs6tyMOwicBVo7iawMv9HwF1FUCax4VrMg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其中，f是相机的焦距。

小白：嗯，这个三角形相似还有印象，这个式子看懂了

师兄：但是成像过程一般是以图像中心点为坐标系原点的，如下图所示。而我们做图像处理的时候习惯于从左上角为图像坐标系原点，所以。。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqZB2aqw9k4QyiaKnbCAIsqVmVBVXhLpErbWiaVQQPYyNy8UZicHH0icBIiaA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：所以还需要一个平移？

师兄：恭喜，你都会抢答啦！下面式子中cx, cy就是分别在x,y方向的平移，一般是长和宽的一半。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqfA9ichXuqgRricYxJN69nAshow7IXIyqzLDXqhJk38SpU2jcqSpHMlPQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：师兄，好好的为什么要平移啊？

师兄：哦，这是因为虽然成像的时候是以图像中心为原点，但是我们图像存储的时候都是从左上角开始存储的，这样方便数据的读写

小白：原来是这样啊！除了平移外，还有个尺度因子α，β，这个尺度因子从哪里冒出来的？！

师兄：你想想，前面X', Y'单位是什么？cx, cy单位是什么？

小白：X', Y'单位应该和X,Y 类似，是（毫）米吧，cx, cy是图像坐标系的，我们一般说图像多少多少像素，那单位应该是像素吧？

师兄：没错！所以需要尺度因子统一一下单位，所以尺度因子α，β单位是像素/（毫）米，这样和X',Y'相乘后单位就是像素啦！

小白：是哦，这样就可以直接和cx, cy相加啦！等我默念一般哈：



X', Y'单位是 毫米

α，β单位是像素/（毫）米

cx, cy单位是像素



好啦，师兄继续吧~

师兄：有了前面两个式子，我们把第2个带入第1个，就得到了下面式子，u, v都是图像坐标系下坐标，单位是像素

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqndBy8a9Rjvzz1GXeE4icNnKYNEmMyEd5ZVVEoamN4nyNfkegAia159Qg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：这个公式看懂啦！不过我看书上都写成矩阵的样子了啊

师兄：没错，一般都写成齐次坐标，用矩阵表示，如下图

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9Fdkq6icxjDtsURMATbYI5kMZzBtRbNUNJ8DmgTBVE6mAsXVEibr7rXubX19w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



左侧图像坐标是齐次坐标，中间红色框内的矩阵K称为内参数，最右侧蓝色框内的就是相机坐标系下的三维点P啦！

小白：写成矩阵形式真的挺方便的！

师兄：对，你看还有一个1/Z 的系数，这个Z是相机坐标系下P点的Z坐标，如果把这个 1/Z 和 P(X,Y,Z) 进行相乘，就得到了相机坐标系下P的归一化坐标 P = (X/Z, Y/Z, 1)， 它位于相机前方z =1 的平面上。

小白：原来这就是归一化坐标说法的来源啊！

师兄：对，我们结合前面从世界坐标系到相机坐标系的变换，就有了如下式子：



![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqIgC6wf5DmecKzwcnGECIWwkjoZA1FT8DBwibn7oIzPDw5hNFic4ianCdA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其中 fx, fy 分别是x, y方向焦距，一般都是相等的, cx,cy是光心位置，一般是长和宽的一半，他们都叫**内参**，此外还有畸变系数也属于内参，他们都是相机固有参数。

到此，针孔相机成像模型就讲完啦！

小白：嗯，感觉很有收获！



师兄：**总结一下整个过程**：

1、首先，世界坐标系下有一个三维点Pw

2、若世界坐标系到相机坐标系下的变换为旋转矩阵 R 和平移向量t 组成的变换矩阵 T，那么Pw在相机坐标系下的坐标为 Pc = R*Pw + t = T*Pw

3、此时的Pc三个分量分别是X, Y, Z，我们需要把它投影到归一化平面Z=1上，这样我们得到了相机坐标系下Pc的归一化坐标 Pc' = (X/Z, Y/Z, 1)

4、用内参矩阵乘以归一化坐标就得到了像素坐标 Puv = K*Pc'

## 相机畸变是怎么回事？

小白：师兄，那个畸变参数还没讲呢！

师兄：哦对，这个畸变参数也很重要的，也是内参的重要组成。

小白：师兄，为啥相机会畸变啊？

师兄：这是因为我们的相机前面有个透镜，如果想要相机一次性拍摄很大的范围，像下面这个图这样，就需要把透镜做的中间很厚两边薄，这样光线经过透镜后会发生折射，相机就能看到更多物体啦。不过这样的话，我们前面的针孔模型中的那些三角形相似的假设就不能满足啦！

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqoVppBDnaLeKK6SKzb22Q8lwjK0Jz0ia0apWneJiaX8XAphQRmRuYc6ZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



也就是说：畸变产生的原因是：透镜不能完全满足针孔模型假设

小白：嗯，好像是这样，那种鱼眼相机看起来就是凸的很呢，拍出来图片边缘的房子都扭曲了。是不是所有相机都是一种类型的畸变啊？

师兄：不是的，相机透镜的畸变主要分为径向畸变和切向畸变，还有其他的畸变，但都没有径向和切向畸变影响显著，所以我们在这里只考虑**径向和切向畸变**。

小白：啥是径向啥是切向啊？

师兄：你看下面这个图，很形象。这是径向畸变的两种类型，一种是桶形，像个木桶，一种是枕形，像个枕头

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqhZWS7J0YUiauLZw5aqoAL5ZPbUiahLs7TzxoQ5Gliam2AHxaTgicumyPww/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：真的很像哎，哈哈

师兄：你看他们的畸变程度有什么特点？

小白：好像中间部分还好，越往周围扭曲越严重？

师兄：是，畸变程度都是从中心开始，用一个半径画圆的话，半径越大，圆周上的畸变程度也越大。这个就是由于相机透镜的形状导致的，且越向透镜边缘移动径向畸变越严重。

小白：嗯，挺直观的，那切向畸变是啥？

师兄：切向畸变是由于透镜和CMOS或者CCD的安装位置误差导致。看下面的图，因此，如果存在切向畸变，一个矩形被投影到成像平面上时，很可能会变成一个梯形。不过随着相机制造工艺的大大提升，这种情况很少出现了，我们一般也不考虑切向的畸变。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9FdkqHZfOJJ61ibvribqYZNac1ylCMCNUvr8ErlyQUJH6EkSAVt8ZkF4g2NdA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：那就是说只要考虑径向畸变就行了？（不用学切向畸变了，yeah！）

师兄：对。下面我们来说说怎么样对畸变进行去除

小白：感觉很难的样子。。。

师兄：是有点麻烦。首先需要对相机进行标定，标定完就能得到相机的所有内参，包括畸变系数。我们用标定的畸变系数就能对畸变的图像进行去畸变啦

小白：那这个相机标定怎么做的？

师兄：这个还是挺复杂的，标定的原理你可以看看一个叫“计算机视觉life”的公众号，里面讲相机标定原理还是挺清楚的~

小白：嗯，师兄，记住啦，我去关注一下。

师兄：假设我们已经标定好了，下面来看看如何用畸变系数来去畸变吧

小白：好啊，这个感觉很神奇啊

师兄：对，你看下面式子就是去畸变的公式，记住这个就行了。你看等式左边都是拍摄的原图的坐标，就是发生了畸变的。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9Fdkq3k6Sibj4u7d3Nhy4fYetGCDoNRtNmp0Qd5xiadyl6KDt8kIA88L9jqbg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：下标的distorted出卖了它，哈哈

师兄：嗯，等式右边的坐标x, y是去畸变后的图像坐标，它是归一化的坐标，以图像中心为原点，还有那个r 就是半径啦，你看这是一个圆的方程。你觉得这个怎么计算出 x, y？

小白：感觉这个计算好像很麻烦啊，左边是已知，右边是未知，再带进去那个半径，天呐，没法想象啊！

师兄：确实如你所说，如果是正常的思维方式，确实很难解。不过，我们可以反过来算，就简单多了

小白：怎么反过来？

师兄：就是我们假设已经有了去畸变的图像了，对应下面左图，它的坐标 x, y自然已经知道了，然后带入右边式子，最后得到一个x_distorted, y_distorted的坐标，这个坐标对应的就是扭曲的图里的坐标，就是下面右图，我们只要把这个像素值替换掉去畸变的图片里的 x, y 处像素值就好啦！

小白：这个好神奇哦

师兄：嗯，很巧妙的方法。不过计算得到的 x_distorted, y_distorted可能不是整数，是一个浮点数，这就需要进行插值计算了。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNnbXNzhpogwd6Olzna9Fdkq4HjQDNNHHPXT0BctFBnar22jTjIA72XKNHmvQeNz5CqfgxahMGvtmA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# 如何真正理解对极约束?

[以下内容详细介绍在这里](https://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247486151&idx=1&sn=2b322f466d916704b1070ece20e669db&chksm=97d7ef50a0a06646a984fcbf82870011ec10a9233899ee74fe8c09432517c5efaa285f1897c9&scene=21#wechat_redirect)

## 对极几何是什么？

师兄：好。那我就从几何意义的角度来推导一下对极几何中的对极约束吧。先看下面这个图，很熟悉吧，对极约束中很常见的图。它表示的是一个运动的相机在两个不同位置的成像，其中：



左右两个平行四边形分别是相机在不同位置的成像平面

C0, C1分别是两个位置中相机的光心，也就是针孔相机模型中的针孔

P是空间中的一个三维点，p0, p1分别是P点在不同成像平面上对应的像素点

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbT9eLuuwf4ysbMdDuJHPum1BCiaUkbmiaL5bLB4n6hibv7oflHro9x1yjPg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



小白：嗯，这个图见到很多次了，不过一直理解的不透彻

师兄：你看上面左侧的图，如果将点P沿着C0-p0所在的直线移动，你会发现P在左边相机的成像一直不变，都是p0，这时候P在右边相机的成像点p1是一直在变化的



小白：对，好像是沿着右边那条红色的线滑动

师兄：嗯，你看C0-C1-P-p0-p1他们都是在同一个平面上的，你可以想象C0-C1-P组成的平面是一个三角尺，它所在的平面称之为极平面（epipolar plane），它像一把锋利的刀，切割了左右两个成像平面



小白：哇塞，这样感觉直观多了

师兄：嗯，其中和成像平面相交的直线称之为极线（epipolar line），两个光心C0, C1和成像平面的交点叫做极点（epipole）。



小白：师兄，好多新的术语啊，都要记吗？

师兄：不用死记，知道是哪个就行了。我们重点来说说极平面，你看下面这个图，C0-C1-P-p0-p1他们是不是都是在极平面上？

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTQZdjhSELhS4pSIgHS36t6FibCNzrfCNttLDeqbL5fMp8ibyN8wOQ7OVA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：嗯，是的，它们都是共面的。

## 如何理解对极约束的物理原理？

师兄：还记得我们在《[从零开始一起学习SLAM | 为什么要用齐次坐标？](http://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485921&idx=1&sn=dfccfc8772d4905c744cab53c3c4c7b3&chksm=97d7ec76a0a065608fda155f6de835c534fa2b012b6659d317c279181e040480e6b883867d14&scene=21#wechat_redirect)》里讲的叉乘的定义吗？两个向量的叉乘结果是一个同时垂直于这两个向量的向量。

小白：记得呢，叉乘只在三维空间中有定义，比如两个向量 a和b 的叉乘写作  a x b，它是与向量 a, b都垂直的向量，其方向通过右手定则决定。



师兄：对，除了叉乘，还有点乘，a点乘b的定义是

a * b = ||a||* ||b|| *cos(θ)

因此如果两个互相垂直的向量点乘，cos(θ) = 0，点乘结果也为0。

小白：师兄，这些我都记得呢！可是怎么突然说这个呢，和对极几何有什么关系吗？



师兄：当然有关系！刚刚你说了点乘和叉乘的特点，现在我们把极平面中C0-C1-p0-p1单拎出来，看下面的图

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTvzEot8GZBqlmNy58CxxxdrkNvjWOMzsb9s6TSqUX7vonxjib2R5veqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我们能够得到下面的 结论1：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTVNSy7fnlnzNfKVZVM59DVG2LlveFMZjxhPD5RuyDDmHfkQ747X2buw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

你自己说说为什么这个等式成立？

小白：我看看哈，额，根据叉乘的定义

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbT5SnH17ZVr8kicynIfGaVyy7YSg77WAdaVFTOEmHP37bsa9YPYpibNT9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

的结果是一个同时垂直于它们的向量，也就是说垂直于C0-C1-p0-p1组成的极平面，因此这个叉乘的结果再点乘

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbThItKzMYWqbuk8o0spaHzWYnv2OsTJeyMh6HYA5NKyENRaFyJ6XwC5g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果就是0了。是吧，师兄？

师兄：完全正确，用到的都是我们前面刚刚讲过的基础知识~

小白：可是，师兄，叉乘不是仅在三维空间中有定义吗？我们这里的p0, p1都是图像上的二维点啊



师兄：这个问题问的好！确实如你所说，p0, p1都是图像上的二维点，不过，这里我们会把它变成三维的方向向量来考虑

小白：啥是方向向量啊？



师兄：就是我们只考虑它的方向，而不考虑它的起点或终点的向量。我们假设一个归一化的图像平面，该平面上焦距f =1 ，因此我们可以定义在以C0为原点的坐标系下

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbT1awMwEto2YzXR0rdraMGxQicykmOFkgBPJhZoHZ9aqNdqk9VD3na7Xg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

而在以C1为原点的坐标系下

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTM8Cmkrnxr1cgWXD62q1DHm9cX2OibkTadUSMyWo4GLn74U9SGeDDNGA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：这样定义可以吗？

师兄：可以的，事实上，你在C0-C1-p0-p1组成的极平面上，保证

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbThItKzMYWqbuk8o0spaHzWYnv2OsTJeyMh6HYA5NKyENRaFyJ6XwC5g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

的方向不变，在极平面上随便移动，结论1中等式都成立。同样的道理，在极平面上，保证

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTAdDh9OHibYjMJ3dQrfBFeTRousTYVGzHo9xSxHRTEkyL5wJJiabpOwXA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

方向不变，在极平面上随便移动，结论1中等式仍然都成立。

小白：确实是这样，师兄，下一步怎么办？好像p0, p1不在同一个参考坐标系里？



师兄：是的，前面说过，p0在以C0为原点的参考坐标系，p1在以C1为原点的参考坐标系，所以我们还是需要转换坐标系。这里我们把所有点的坐标都转换到以C0为原点的坐标系。前面说过这些向量都是方向向量和向量起始位置无关，所以这里坐标系变换只考虑旋转就可以。我们记 R 为从C1坐标系到C0坐标系的旋转矩阵

小白：那么 Rp1 就是p1 在以C0为原点的C0坐标系了

师兄：对的~现在再看看**结论1**：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTVNSy7fnlnzNfKVZVM59DVG2LlveFMZjxhPD5RuyDDmHfkQ747X2buw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



最左边向量C0-p0就可以用p0表示，向量C0-C1就是光心C1相对于C0的平移，我们记为t， 向量C1-p1根据前面的讨论，可以用 Rp1 来表示，那么结论1可以表示为以下的结论2：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTZxBicxurHRRVhONYa84sGxjdzt1YH99QKm3dicuEiaxZWyiadgSOXDjW8A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这个式子是根据对极几何得到的，我们称之为对极约束。

小白：哇塞，师兄，原来对极约束也可以这样得到啊！我现在能完全理解啦！

## 如何得到极线方程？

师兄：对，这就是对极约束最直观的解释，一般把中间的部分拿出来，像下面这样，记为本质矩阵或本征矩阵（Essential Matrix）。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTDh5CdJJQc236jDsuaY1LfqyTS0sTwJNcxhR0AxRhUJVibaJRmmLYcgQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后我们就得到了如下的结论3：

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTtYZibicpHNsypcRDpF7Q5QjBgIXerStdsworCKVZym511lw68tAmIlRg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：厉害了师兄，这下彻底明白啦，不过之前提到的极线什么的好像也没说怎么求啊？

师兄：其实根据上面结论3就可以求出极线方程啦！



小白：啊，怎么求极线方程？

师兄：还记得我们在《[从零开始一起学习SLAM | 为什么要用齐次坐标？](http://mp.weixin.qq.com/s?__biz=MzIxOTczOTM4NA==&mid=2247485921&idx=1&sn=dfccfc8772d4905c744cab53c3c4c7b3&chksm=97d7ec76a0a065608fda155f6de835c534fa2b012b6659d317c279181e040480e6b883867d14&scene=21#wechat_redirect)》里讲过的

点p在直线l上的充分必要条件就是 直线l 的系数与p的齐次坐标p'的内积为0

![img](https://mmbiz.qpic.cn/mmbiz_jpg/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTGOFSo6Kc4T0JaibsCrH3wIUPlqXVu9meibOxvhavR9nSbUEic0Uv5nfYQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：记得呢！那节课的习题我都认真做了，所以印象深刻！

师兄：不错！那结论3我们就可以把E*p1看做是直线的方程，p0看做是直线上的点，也就是说E*p1就是以C0为原点坐标系中的极线了。如下图中红色线条所示，就是极线啦，它的方程是E*p1。

![img](https://mmbiz.qpic.cn/mmbiz_png/rqpicxXx8cNlNmrbfVSTgDpbzDXKNCmbTDPBrYKu0icbSedUwKT3fD8iaNVRqNtIpq3qo51ULAoNiaT4S1mHAr5hAQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小白：原来如此，看来以前的基础很重要啊！哪里都能用上。谢谢师兄，今天没有推导公式，我竟然能够得到极线约束的式子，太神奇了，而且印象很深刻！

# 什么是**Bag-of-words**？

词袋算法 ，它是主要用来判断同一个地点是不是被重新访问过，在实现的原理上可以认为是对每一帧或者叫每一幅图用了很多单词来进行描述。

在实际应用中在这个词袋中使用的单词量会非常大，并且这些词在现实中并没有一个非常明确的物理含义；词袋方案现在主流所采取的方案之一，它做得最好的一方案叫 DBOW2，也是一个开源的方案。

DBoW2来源于论文Bags of Binary Words for Fast Place Recognition in Image Sequences，是ORB_SLAM2的作者同门师兄的一作。可见牛逼的人都是扎堆的~

DBoW2是一个对大量训练图像使用fast关键点+BRIEF描述子的方法提取特征，再将大量特征做K-mean++聚类形成一棵词典树的模型。词典离线建立好之后，在实际应用过程之中，将每一幅待处理图像提取特征与词典树中的描述子相比较得到一些索引，从而可以提高搜索相似图像和得到图像之间特征匹配的效率。



