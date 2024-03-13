---
title: 一个有趣的Hamming问题
date: 2024-03-13 10:37:18
tags:
---

于三月十二日晚间，和和王JM谈到数值计算方法这节课。然后然后他说“我们有数值分析“。我问“数值分析是什么”，“数值计算方法plus”。之后为展示该门课为什么是Plus，他给我看了一个颇为有趣的题目：

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

令人寒心的是，搜遍全网关于该问题的解法，所有人无一例外，全部埋头苦算，硬算完了就没下文了，连解释都懒得解释，也没有好奇地去找找Hamming到底有没有写过这个玩意，甚至没有形成一片报告文档。这怎么行？

好吧，今天彻底成不眠之夜了。我非得挖出这道题来。你都不知道这道题来源于什么工程环境，你怎么就上去硬干了呢？这不工程师啊。

# /……施工中……/
