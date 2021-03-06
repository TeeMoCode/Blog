title: 神经网络历史以及浅析神经网络与感知机
date: 2019-04-22 08:54:03
updated: 2019-04-22
categories:
- AI
tags:
- 感知机
- 神经网络

---

{% note info %} 本文为吴岸城《神经网络与深度学习》学习过程中0-3章部分的学习笔记的整理。{% endnote %}

<!-- more -->

## I. 神经网络历史

### 1943年

![](/img/neuro-history-perceptron-1.jpg)

麦卡洛(神经生理学)可和皮茨(逻辑强的天才，很小的时候就解读了罗素《数学原理》，后来学习了卡尔纳普《语言的逻辑句法》)发表了模拟神经网络的原创文章《神经活动中思想内在性的逻辑演算》

### 1947年

![](/img/neuro-history-perceptron-2.jpg)

图灵发表《计算机和智能》，提出"机器会思考吗?"，并给出肯定的回答，甚至给出了十分具有可操作性的方法以及预言2000年可以出现骗过30%裁判的机器人

### 人工智能流派

1. 自顶向下的逻辑和符号系统(通过狭义统计学预设和反馈来达成)
2. 自底向上的仿造大脑来达成(模拟大脑中的神经网络)


### 1951年

马文·明斯基设计并构建第一部能自我学习的人工神经网络机器SNARC

### 1952年

![](/img/neuro-history-perceptron-3.jpg)

马文·明斯基发明会自动关闭电源的Useless Machine

### 1956年

达特茅斯夏季会议确定人工智能的概念

### 1957年

罗森布拉特基于生物工程的人脑机制提出感知机模型(单层神经网络)，后明斯基和派珀特出了一本《感知机》的数证明感知机无法处理XOR亦或问题

### 1958年

明斯基与麦卡锡来到MIT成立第一个人工智能实验室

### 1959年

维德罗和霍夫提出自适应线性元件(Adaline)，这是感知机(只允许0或1)的变化形式，不同的是，Adaline有一个线性激活函数，允许输出任意值

### 1982年

![](/img/neuro-history-perceptron-4.jpg)

霍普菲尔德神经网络提出，提出动力方程和学习方程，引入了能量函数的概念，使圣经网络的平衡状态有了明确的判断方法；递归(复发型)神经网络，结合存储系统和二元系统的神经网络；离散的Hopfield网络用于联想记忆；连续的Hopfield网络用于求最优化问题

### 1986年

杰弗里·辛顿(Geoffrey Hinton): 反向传播算法和对比散度发明，改进算法可以对七层或更多深度神经网络进行训练

### 1984年

霍普菲尔德用模拟集成电路实现自己提出的模型，使得大量学者被激发研究神经网络的热情

### 2004年

美国电气电子工程师协会(IEEE)特别设立罗森布拉特奖，奖励圣经网络领域杰出研究

### 2012年6月

吴恩达和谷歌科学家合作用1.6万台计算机模拟了一个人脑神经网络，在无外界干涉下，从1000万段从Youtube随机选取的视频中自己认识到"猫"是怎样的动物，识别率达到81.7%

### 2015年5月28日

![](/img/neuro-history-perceptron-5.jpg)

LeCun、Bengio、Hinton在Nature上发布一篇名为Deep Learning的综述并开设Deep Learning专栏，涉及概率机器学习、强化机器学习、机器人等多方面，卷积神经网络(CNN)改进再应用: 勒丘恩(Lecun): 第一个把BP算法用在CNN上，完善CNN使其可以真正应用上工作，1998年后近20年CNN第一推动者

### 2016年3月10日

![](/img/neuro-history-perceptron-6.jpg)

李世石败于哈萨比斯的AlphaGo

## II. 从买橙子说起

- 什么橙子最甜? 个头大的比较甜
- 另一种品种，中小的、浅色的最甜: 迁移学习
- 表妹不在乎甜不甜，多汁就好，捏起来越有弹性汁越多: 优化目标变化

### 编程思路

- 下发配置
- `if...then`

### 机器学习思路


- Traning Data: 记录橙子属性和类型的关系
- Feature: 颜色、大小、形状、场地
- Output Variables: 甜度、成熟度、多汁度

根据训练集以及预期的输出进行自我学习迭代，最终使得输入Feature得到预期Output Variables。

## III. 大脑学习过程

![](/img/neuro-history-perceptron-7.jpg)

比如我们学习数字1，会先记住1这个图像，然后再通过一个苹果、一只小熊、一个人类似的在大脑中建立了1这个形状与苹果、熊、人的联系，这个联系的建立是神经元轴突终端连接到其他神经元上。而其中涉及的各种形状存储在不同的神经元或海马体中。

### 生物意义上的神经元

> 神经元事实上是神经细胞的别称。

#### 神经元是如何工作的?

![](/img/neuro-history-perceptron-8.jpg)

- 树突: 接收其他神经元的信息并传至胞体
- 轴突: 把冲动传至远处，传给另一个神经元的树突或肌肉与腺体
- 细胞体: 进行复杂的化学变化，确定是否需要对轴突产生输出

主要拥有兴奋性和传导性两大特性:

- 当刺激强度未达到某一阀值时，神经冲动不会发生
- 当刺激强度达到该阀值时，神经冲动发生并能瞬时达到最大强度，此后刺激强度即使再继续加强或减弱，已诱发的冲动强度也不再发生变化

以上的两个特性在后续讲述人工神经元时的传输函数中得到体现。

神经元的功能多样性:

- 感觉神经元，作为传入神经元将兴奋传至脊髓和大脑
- 运动神经元，作为传出神经元将通过兴奋引起肌肉与腺体活动
- 联络神经元，将传入神经元与传出神经元联络起来组成复杂的网络，多存在于脑和脊髓里

比如了解火的认知，需要感觉神经元先接受传入视觉、温度等信号然后传递给作为联络神经元的脑神经元，再多次传入后，以后接触到火就会通过运动神经元将伸出接触火焰的手收回来。

后续的人工神经网络也会存在各类神经元的联络来达到更复杂的学习目的。

#### 神经网络的自组织

![](/img/neuro-history-perceptron-9.jpg)

脑神经系统如上图所示，最复杂的部分在**大脑皮层**，其具有高度分析和综合能力。
而大脑皮层是由许多**不同的功能区构成**的，每个功能区负责不同的模块，有负责运动控制的、有负责视觉的等。
每个功能区又包含**许多负责某一具体功能的神经元群**，如视觉功能区有负责水平光响应的、有负责垂直光响应的等。
区域是遗传决定的，但是功能大部分是后天学习而来。
我们称这种学习为**自组织特性**，这里没有"领导"去安排工作，每个神经元都决定自己和另外哪些神经元链接或者不链接。
这种自组织构成了神经元的自主学习的特性。

后续的人工神经网络中模型的训练就类似这里能够自己决定特性的自组织。

## III. 构造神经网络

![](/img/neuro-history-perceptron-10.jpg)

如上图我们构造的神经元就类似生物意义上的神经元。

这里特别注意的:

- 拥有多个树突p，每个树突传入有不同的权重w
- 信息处理将所有树突的值累加起来在加上内部默认强度b: $s=p1w1+p2w2+...+pnwn +b$
- 传到轴突时，通过传递函数进行"化学反应" $f(s)$，然后输出结果

常见的传递函数如下图:

![](/img/neuro-history-perceptron-11.jpg)

我们接来下基本上要用到的都是第一个Step函数。

### 感知机

感知机是最简单的神经网络，其可以是一个神经元，一个神经元无法理解"网络"的概念，但是其已经可以解决香蕉、苹果的分类问题。

| 品种 | $p_1$颜色 | $p_2$形状 | 期望结果
| --- | --- | --- | ---
| 苹果 | 1(红色) | 1(圆形) | 1(苹果)
| 香蕉 | -1(黄色) | -1(弯曲) | 0(香蕉)

我们预设:

$$w_1=w_2=1$$
$$b=0$$

传递函数我们使用$Step$

传入红色、圆形:

$$s=1\*1+1\*1+0=2$$
$$f(2) = 1$$

得到$苹果(1)$

传入黄色、弯曲:

$$s = -1\*1 + -1\*1 + 0 = -2$$
$$f(-2) = 0$$

得到$香蕉(0)$

这里就已经完成了识别。**对于前面预设的权重w1,w2以及内部默认强度可以是其他值吗？这个预设值是怎么得到的？这个问题就是接下来感知机的学习需要提到的**

### 感知机的学习

如果我们预设:

$$w_1=1, w_2=-1, b=0$$

套用公式会发现:

同样传入红色、圆形:

$$s = 1\*1 + 1\*(-1) + 0 = 0$$
$$f(0) = 0$$

得到的居然是$香蕉(0)$

这里我们就涉及到感知机的学习，我们对预设的权重与默认强度进行修正:

$$w(new)=w(old)+e$$
$$b(new)=b(old)+b$$

上面的e表示误差，$e=t-a$，$t$为目标值，$a$为实际输出值

这里红色、原型的目标结果是$苹果(1)$，而实际输出是$0$

误差计算:
$$e=1-0=1$$

权重重新计算:

$$w1=1+1=2$$
$$w2=-1+1=0$$

默认强度重新计算:
$$b=0+1=1$$

我们重新带入$红色(1)$与$圆形(1)$:

$$s=1\*2+1\*0+1=3$$
$$f(3)=1$$

我们发现结果正确了，得到了$苹果(1)$

我们再传入$黄色(-1)$与$弯形(-1)$试试:

$$s=-1\*2+(-1)\*0+1=-1$$
$$f(-1)=0$$

也得到了正确的结果，得到了$香蕉(0)$

自此已经完成该感知机的学习训练。

---

- [《神经网络与深度学习》](https://book.douban.com/subject/26820803/)
