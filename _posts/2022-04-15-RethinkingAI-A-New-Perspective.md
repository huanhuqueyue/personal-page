---
title: Rethinking AI, A new perspective
layout: category
permalink: /categories/RethinkingAI-A-New-Perspective/
taxonomy: Rethinking AI, A new perspective
---

# AI走向意识深处

在回到北京的这段时间里，和很多人有了新的探讨，记录一下自己最近的想法。

## 背景

在这两年的时间里，AI技术得到了越来越多的关注，也取得了原来不可能想象的一些成就，同样在学术圈也发生了和以往所有学科热潮当中完全不一样的趋势，简单举个例子：AI的论文数目和投稿数都是爆炸性的增长。这后面的原因我猜测大概有二：1. AI已经在很多个方向上有了比较较为成功的应用，这引起了来自不同领域的研究人员参与进来 2. AI模型作为一种黑盒模型，入门门槛很低，在torch等自动反向传播求导框架提出后，新的算法的提出就是某种意义上的搭积木。举一个我身边比较夸张的例子，一个非计算机专业的同学可以在4个月的时间里，从不会写代码开始，到投一篇顶会结束。

有一个观点我和沐神比较相似，每年新增长的超过99%的AI方向的文章都属于科研训练式的文章。在这样的热潮下又出现了哪些缺失的地方呢？这也是我在思考的问题。

## AI应用 in 建模角度

在AI一波接着一波的热潮当中，应用已经渗透到各个领域中了。OpenAI每隔几个月的时间就会搞出来一个大新闻，如AI会写代码了，AI可以核反应堆结合了，alphafold，GPT3都取得了空前的成功。以及在NLP，CV等传统的AI涉足的领域，现在其实已经走向生活的每个地方，这也为社会创造了巨大的财富。比如推荐系统，系统1%的准确率提升就能带来超过上千万的收入。

在这种思想的指导下，提高性能、刷榜成为了一个必然的趋势，从netflix的数据挖掘大赛，到一年一度的kdd cup，以及大大小小数不胜数的kaggle比赛。工业界和学术界的共同关注，让AI科技为我们带来更好的生活，这是所有人都希望看到的场景，我们也期待这个领域未来能取得更好的发展。

但是在AI的进展中，人们最愿意提及的是我的模型performance是不是work，理论上的贡献似乎被淡化了。这里我从传统的数学建模角度来重新审视一下这个问题。

一个新方法的应该有以下几个步骤： 

1. 假设： 对数据本身性质的一些或抽象或具体的先验，或者说是我们做模型的目的
2. 建模： 根据假设试图找到问题对应的好的模型
3. 求解： 我们会通过求闭解或者数值优化的方式（注意前向传播也可以认为是一种求解，构建计算图）
4. 验证： 验证模型的performance

让我们带入一般AI文章的求解思路，看看有哪些部分可以讨论：

深度学习经常谈论：学习某种要素，单单把神经网络的反向传播当作学习，让BP来解决追求泛化的优化问题，以期待能学到对应的要素，以此来达到泛化的终极目标。然后我们会把求解的模型在一些流行的数据集上进行验证。

但在这里我想提几个问题：

- 在几个数据集上泛化的好就在实际场景中能做的好吗？
- 为什么这套方案能泛化的好，而别的方案不行？
- 这套方案真的能学到想要的要素吗，还是模型其他方面起到了更本质的作用？

针对第一个问题，根据no free lunch理论，我的答案在绝大多数情况下是否定的。

第二个问题，我在实际生产中也经常遇到，也就是说我本身设计的是一个理解上很合理的方法，但是实际做实验的时候没有用处。为什么？我的理解是，BP和优化器在帮我们做模型的选择，甚至随机种子的选择，隐层的维度，隐层的深浅都可能决定这个问题。这种感觉就像三体中智子锁死了人类的科技水平一样，一些神经网络的基础设计锁死了深度学习的研究空间

第三个问题，我的理解是不知道，深度学习大多通过一种后事实的角度来验证模型的有效性，我们在研究一个问题的时候甚至经常跳过第一个assumption的步骤，或者说assumption大多是一种很模糊的想当然的东西，拍拍脑子。transformer效果比rnn要好，那肯定是因为transformer学到了全局信息，然而什么是全局信息？为什么需要全局信息？transformer能怎样反应全局信息这个assumption？在很多场景下都是没有理解的问题



## AI应用  &  理论直觉

从历史的眼光来看待学科发展，也有很多学科是以应用出发，学科得以发展。比如和AI最相关的凸优化，其实是发了二战的”战争财“。在求解了各种各样的实际问题，最后收敛发展成为一个真正的科学，有理论基础，有哲学思想。我个人也很殷切的期待AI在这么多人参与，如此多财力投入的情况下，也能走向这样的过程。

举一个例子来判断应用和理论之间的关系，应用可以理解为整个数据空间，而理论是在这个数据空间当中underlying的本质的流型。那么理论能怎样影响实际呢？我觉得有以下两个角度：

- 以严谨的数学角度在assumption的基础下，严谨的得出更可靠的结论
- 以严谨的数学为基础，辅以数学直觉，设计更新型的网络结构，比如self attention，细看其发展，也是bengio推动了好几年的结果
- 对AI技术进行抽象，找到其中的流形 （本质），抽象将网络结构看作一个整体，再设计真实的物理模型来验证，求解这个问题

在理论和应用的共同作用下，AI会迈向哲学，从感知计算迈向更高阶的智能。从correlation到causal，从look到do到imagine（what if）。

最后一句话总结我这个博客：让ai回归科学，回归本质的，数学的，哲学的思考，延续ai领域的生命力，让AI走向意识深处。