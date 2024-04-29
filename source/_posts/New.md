---
title: NumericalMethodsComputer Assignments 数值计算作业
date: 2024-03-10 22:29:51
---

Assignments for the Numerical Methods of Zhejiang University by Dr.Red. Update regularly every Sunday.

浙大数值计算方法作业。俺写的。不要问我为什么用英文，好看。

**Computer Assignment #1**

普通的matlab使用练习。很挫，当时对latex的该模版还不是很熟悉，不建议观看。

{% pdf https://drive.google.com/file/d/1umTdsfcUBgg76hR6mkXWAqw3j-VoZCof/preview %}

**Computer Assignment #2**

虽然是小作业，还是用很长的时间改进了排版。应该花了一天左右，同时学习了Matlab如何画图。这里的精华在于第三种方法实际上是用牛顿法的特例（几千年前的海伦法）搞出来的，严格来说已经不是原先的那种方法了（二次收敛，而非线性收敛。这就是为什么迭代次数骤降了一倍），起码我拒绝承认这还是原来的那种纯粹的不动点迭代法。这个东西需要一定的观察才能看出来，不知道出出来是不是坑人的。

{% pdf https://drive.google.com/file/d/13QqzjI0OjYaZlUIt8Kz_t6cnaz9_2OYx/preview %}

**Computer Assignment #3**

非常普通的矩阵求解。注意这个矩阵因为行列式接近于0，是病态的。另外对代码排版的探索也是在这一版中逐渐明确的

{% pdf https://drive.google.com/file/d/1I4lo01R5yXWb11lHp9SkkNPS0NH_rXAV/preview %}

**Computer Assignment #4**

插值。可以感受到非常明显的Romberg效应，因此这个例子其实并不怎么适合lagrange插值，反而倒是真·线性插值适合一些。

{% pdf https://drive.google.com/file/d/1MQhJ5PNHE-23gAETaHXgf3uA0JmvDaKG/preview %}

**Assignment #1**

复习了一遍积分的递推公式。这里很有意思的点在于，递推需要考虑算法的收敛性。一开始正着递推误差会阶乘式爆炸性变大，而倒着推就会减小，所以采用倒推法。不过这需要超前的Newton-Cotes法等知识，不建议使用。

{% pdf https://drive.google.com/file/d/1Fg7_wFJveM5AskkhFMn95VCb0Xk1nZFr/preview %}

**Assignment #2**

求根的非常多的方法。很简单，没什么好说的。值得注意的是不动点法如果不经过转换，会直接飞出去。所以千万不要直接上。

{% pdf https://drive.google.com/file/d/1VSLn79VU7BMeVu2Rc47fIUhqY-upRWa4/preview %}

**Assignment #3**

这篇年代有些久远了，技术细节基本上忘光了。要注意的大概是这道题的中文翻译表述有很严重的问题。原题写的“待萃取物的组分Yin”实际上指的是萃余相中溶质A的浓度，“萃取剂的组分Xin”是萃取相中溶质A的浓度，这两个描述的是同一个物质在不同萃取相中的组分差别，不是萃取剂自己的差别。不然可能会觉得“萃取剂”在“被萃取的过程中”正在“越来越少”，这显然错误。和赵豫红老师沟通过，她大概会改一下这道题的表述。

{% pdf https://drive.google.com/file/d/1v_BHKR7_BL-CEqkGyT09f-g8i3_-1GIi/preview %}

**Assignment #4**

非常美的一篇小报告。Gauss-Newton法在非线性回归中无往不利，百战百胜，唯一的问题是不能用在最简单的线性回归中。至于分析，嗯……马后炮而已，不要管。

{% pdf https://drive.google.com/file/d/1TSeJri3Uqk0mOS25_WHPV80Ha0RYzR4v/preview %}

**Assignment #5**

Gauss-Legendre方法很惊艳，但是确定Gauss点的方法更加惊艳。可以在维基百科上搜索GaussQuadrature的确定方法（包括Legendre多项式），让人大开眼界。

P.S. 很有趣的地方在于，当时问的Chatgpt，Chatgpt给出了一个让人摸不着头脑的副对角数值计算方法。后来找到了很冷门的文献，发现这正好是正确结果的计算式子的倒数表达形式……令人叹服AI的信息知会能力。

{% pdf https://drive.google.com/file/d/1rnwzQB6mljR5ewjJCQg-4gGRRvxaVZ-y/preview %}

**End-term Assignment**

大作业做的计算化学，浅要地用休克尔规则解决了一下之前在做化学竞赛的时候困扰我的各种问题。反正有这个计算方法以后，对于大的有机碳骨架共轭体系应该不是什么大问题的，无非还要解决各种杂原子的微扰动。不过那就是别的问题了，作为搞控制的我也不用太拘泥于此。了却心愿而已。

{% pdf https://drive.google.com/file/d/1bc7mHrELnLydjvdWIvZ7UQ2uaLqqPSgL/preview %}
