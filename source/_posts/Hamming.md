---
title: 一个有趣的Hamming问题
date: 2024-03-13 10:37:18
tags:
---

植树节晚间，和和王JM谈到数值计算方法这节课。然后然后他说“我们有数值分析“。我问“数值分析是什么”，“数值计算方法plus”。之后为展示该门课为什么是Plus，他给我看了一个颇为有趣的题目：

Produce a table of the values of the series  

{% blockquote %}

{% katex [displayMode] %}

\sum\limits_{k=1}^{+\infty}\frac{1}{k(k+x)}

{% endkatex %}

{% endblockquote %}

 for the 3001 values of x, x= 0.000, 0.001, 0.002, ..., 3.000. All entries of the table must have an absolute error less than 0.5e-10 (12 digits of precision). This problem is based on a problem from Hamming (1962), when mainframes were very slow by today's microcomputer standards.

跟着王JM的思路，我以“Numerical Summation of A Series”为标题试着搜了一下这道题。果不其然，出现了一遛的CSDN……

其中一种非常典型的方法（采用裂项法）如下：

{% blockquote @HGGshiwo https://blog.csdn.net/HGGshiwo/article/details/108869233 %}

需要用公式将x不是整数的情况收敛到整数...

{% endblockquote %}

(不要问我为什么不用CSDN。我不知道我这个偏见是从哪里来的，但是我就是不用。)

至于为什么要这么做，该文档没有说。因为已经是深夜，直接问了王JM，他也说不出理论上的所以然，只是说如果硬用小数裂项计算，收敛速度不仅很慢，而且不准；只有在化为整数后，该算法才有比较好的准头。我严重怀疑在裂项过程中，由于严重的拖尾效应，大数干掉了小数，因此造成了这种奇葩的现象，但我也没得验证。

但重点是，这个题目中提到了一个很有意思的人：

{% blockquote %}

...This problem is based on a problem from **Hamming(1962)**, when mainframes were...

{% endblockquote %}

这人是谁？

{% blockquote  @wikipedia https://en.wikipedia.org/wiki/Richard_Hamming %}

Richard Wesley Hamming (February 11, 1915 – January 7, 1998) was an American mathematician whose work had many implications for computer engineering and telecommunications. His contributions include the Hamming code (which makes use of a Hamming matrix), the Hamming window, Hamming numbers, sphere-packing (or Hamming bound), Hamming graph concepts, and the Hamming distance.

{% endblockquote %}

哥们，这么重量级的人物啊！！！汉明码创始人啊！！！作为计算机学院的人你怎么能忽略这个信息呢！！！！

令人寒心的是，搜遍全网关于该问题的解法，所有人无一例外，全部埋头苦算，硬算完了就没下文了，连解释都懒得解释，也没有好奇地去找找Hamming到底有没有写过这个玩意，甚至没有形成一片报告文档。这怎么行？你都不知道这道题来源于什么工程环境，你怎么就上去硬干了呢？这不工程师啊。

好吧，今天彻底成不眠之夜了。我非得挖出这道题来。

## 第一步，尝试搜索

本来如果Hamming在世，这个问题一封邮件就可以解决（且不论对方理不理我）。可惜生晚了。

我的第一想法是利用谷歌学术，穷举Hamming在1960年到1970年写过的所有文献。原因很简单，作者声称这个序列曾经被他在1962年开过光。但是我翻遍了Hamming在1960-1970写过的所有文献，没有。所有有关该序列的内容都一致指向2001年出现的ZOJ Problem Set，也就是该死的浙大自己的习题集中。

搜寻了两个小时后，我发现，最有可能的是，该例子作为某物的引证，出现在祖师爷的 <a href="https://safari.ethz.ch/digitaltechnik/spring2019/lib/exe/fetch.php?media=numerical.methods.for.scientists.and.engineers_2ed_hamming_0486652416.pdf">Numerical Methods for scientists and engineers(1962)</a> 中。这本书有足足七百多页，如果换白天，我可能会选择直接放弃。但是那是晚上，我非常不愿意把问题隔夜，不然会睡不着。

粗略二分搜寻了两遍，无果。实在撑不住，发了个朋友圈（我拒绝熬夜喝咖啡），发现张YH点了个赞。抱着*哦，原来有人和我一样熬夜啊*的这种心情，重整旗鼓，去目录上找。一个子条目引起了我的注意：

{% asset_img  contents.png %}

第十二章是无穷级数啊。看来这个地方大概会有。

功夫不负有心人，经过十分钟的仔细阅读，我发现了这个：

{% asset_img  firstpage.png %}
{% asset_img  secondpage.png %}

原来如此！这下我们就清楚这个无穷级数的庐山真面目了。这个东西其实就是伪装的非常好的Digamma函数(双伽玛函数。如果你不记得这玩意是什么的话，还记得Gamma函数指的是阶乘对实数域的拓展吗？双伽玛就是把他对数一下求个导)。其递归关系如下（不包括整数。整数的运算很简单，有另一套无穷级数，这里不讨论）：

{% blockquote %}

{% katex [displayMode] %}

\psi(1+z) = -\gamma + \sum\limits_{k = 1}^{\infty}(\frac{1}{k}-\frac{1}{z+k})

{% endkatex %}

{% endblockquote %}

其中，γ是所谓的Euler–Mascheroni constant，欧拉-马斯刻若尼常数。具体细节可以在<a href="https://en.wikipedia.org/wiki/Digamma_function">这里阅读</a>。我们要的那玩意和他区别无非是：

{% blockquote %}

{% katex [displayMode] %}

\sum\limits_{k=1}^{+\infty}\frac{1}{k(k+x)} = \frac{1}{x}(\psi(x+1)+\gamma)

{% endkatex %}

{% endblockquote %}

## 第二步，一种很简单，很简单的算法

大家如果熟悉Matlab，就应当会知道，这玩意是可以直接调用函数计算的。

{% asset_img  thirdpage.png %}

和实际的真值完全没有误差。

Matlab的psi函数是什么原理？我打天落地查不到。但是通过<a href=https://personal.math.ubc.ca/~cbm/aands/abramowitz_and_stegun.pdf>Handbook of Mathematical Functions with Formulas, Graphs and Mathematical Tables</a>中的描述，我们可以猜测这东西要么是暴力打表的（事先存储[0,1]的一张表，用递推公式算。如果精度不够，那就再放大以后，再按照递推公式算！！），要么是通过任一种展开方式干的。原题用的是C语言做的，当然不能直接调用Matlab的库（这就是为什么计院的这门课不允许你用Matlab……控院的*数值计算方法*看起来还是挺文明的）。不过，我们可以站在巨人的肩膀上，看看别人是怎么做的。

我们来看一个几乎比我爸爸都老的论文：<a href="https://www.uv.es/~bernardo/1976AppStatist.pdf">Bernardo, José M. (1976). "Algorithm AS 103 psi(digamma function) computation"</a>。

1976年。按照当时的微处理器速度，累加出一大堆项是一个很烦的过程，更不用说打算加到一个很大的值让他收敛了。但是，谁说我们一定要用挫爆了的欧拉递推公式来算？

如果你的记忆力超群（比如说一些数院的天才——我显然不在列，我是控院的），那么你就会知道，有一种叫做<a href="https://en.wikipedia.org/wiki/Stirling%27s_approximation">Stirling's approximation</a>的东西，曾经被用在估计x值比较大的伽玛函数中。这东西可不可以用于估计双伽玛函数？显然是可以的。

{% blockquote %}

{% katex [displayMode] %}

\psi(1+x) = ln(x) - \frac{1}{2x} - \sum\limits_{j=1}^{\infty}\frac{B_{2j}}{2jx^{2j}}

{% endkatex %}

{% endblockquote %}

这个级数对于任意x都收敛。其中，B代表的是<a href="https://en.wikipedia.org/wiki/Bernoulli_number">伯努利数</a>。

在实际应用中，我们只需要取这个级数前面的几项，比如，忽略掉7次以上的项，应该就足够了。但是这么干了之后，虽然说x值越大越精确，但对比较小的x而言（在这里是8.5左右以下），这个级数的符合程度就差到爆表了。 但是这怎么要紧？x小的时候的值可以用大的时候的值来推算啊。还记得这个吗：

{% blockquote %}

{% katex [displayMode] %}

\psi(x+1) = \psi(x) + \frac{1}{x}

{% endkatex %}

{% endblockquote %}

那么，这堆小的不能再小的[0.001:3.000:0.001]，就可以这么来计算：

{% blockquote %}

{% katex [displayMode] %}

\psi(x) = \psi(x+n) - \sum\limits_{ i = 1 }^{n-1}\frac{1}{x+i} 

{% endkatex %}

{% endblockquote %}

{% blockquote %}

{% katex [displayMode] %}

\psi(x+n) \approx \ln(x+n) - \frac{1}{2(x+n)} - \frac{1}{12(x+n)^2} + \frac{1}{120(x+n)^4} - \frac{1}{252(x+n)^6}

{% endkatex %}

{% endblockquote %}

根据这个简单的递推，我们就可以来写程序了。我用的是Matlab，但是没有用到超过C语言范畴的东西。

{% codeblock Digamma.m lang:Matlab %}

function v = Digamma(y,n)
    x = y + n;
    sol = log(x)-1/(2*x)-1/(12*x^2)+1/(120*x^4)-1/(252*x^6);

    while(1)
        sol = sol - 1/( x - 1 );
        x = x - 1;
        if ( x > 1 && x < 2 ), break,end
    end
    v = sol;
end

{% endcodeblock %}

结果展示如下。你可以自己去验证一下，符合地都很好。我没法都截取，这样太占据博客空间了。

{% asset_img  ans1.png %}

{% asset_img  ans2.png %}

诶，大就是好。那么n是越大越好吗？你此时已经嗅到了一丝不对的气息。我们试试看把n的值调大。

{% asset_img  ans3.png %}

我去，有效位数怎么退化了？虽然说还是符合题目要求的十位，但是明显感觉到后面的玩意不对劲了。这样下去，之后一通计算猛如虎，误差变成二百五。

造成这样现象的原因很简单：**我们采取这种方法的根本原因，就是要避开 带有和大整数一起玩的 很小的数的 项！但如果你把n的值设的太大，n和需要的x一对比，比如100000对比0.0001，这十三点东西又出现了！**因此，n千万不能选的太大。经过不断测试，一百也许也太大了。区间在30到50是比较合理的，适用范围也比较广。

ok，最后为了满足题目条件，随便做个计算：

{% asset_img  ans4.png %}

和题目答案一对比，丝毫不差。精度、速度还远远高于题目要求。何乐不为？

## 结语

双伽玛函数不止这种简单的计算方法，光维基百科上就能有近十种。我还有一大堆算法并没有拿出来讨论，因为他们的效果基本上和这种简单算法差不多，大同小异。不过也有很多算法很标新立异，比如<a href="https://cse.buffalo.edu/faculty/mbeal/papers/beal03.pdf">这篇牛津大学的文献</a>,用了一些令人瞠目结舌的方法进行计算。我觉得这彻底超纲了，就没有讨论，有兴趣，有能力的时候再自己做吧。

# 这个故事告诉我们，有问题别特么就想着硬算，先看看这个东西的本质是什么！

*ps 关于本篇采用的算法：这篇1976年的论文居然是用Fortran写的。我不会这种语言，他写的也实别是烦逼醪糟的。最后自己写的玩意可能和他搞的有出入，烦请见谅。*

### reference

1.Hamming, R. (1962). Numerical methods for scientists and engineers. Dover Publications. 
2.Abramowitz, M., & Stegun, I. A. (Eds.). (1968). Handbook of mathematical functions with formulas, graphs, and mathematical tables (Vol. 55). US Government printing office.
3.Bernardo, José M. (1976). Algorithm AS 103 psi(digamma function) computation.
4.Beal, Matthew J. (2003). Variational Algorithms for Approximate Bayesian Inference.
