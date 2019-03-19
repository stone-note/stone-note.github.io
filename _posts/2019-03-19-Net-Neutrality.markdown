---
layout: post
title:  "独辟蹊径！“网络中立”作为区块链扩容解决方案"
date:   2019-03-19 11:10:53 +0800
categories: learning
---
> 译注：扩容、可扩展性、可伸缩性、性能等词语在区块链背景下是对同一问题的不同表述。
  
> 本文作者：Aleksandar Kuzmanovic是美国西北大学计算机科学教授。他最近的研究包括内容交付网络、网络中立性和区块链。他是初创公司bloXroute Labs的联合创始人，并在该公司担任首席架构师。

由于区块链的去中心化特性（即没有一个实体控制其运行），越来越多的人们期待，或者至少是希望，区块链在更多领域发挥其颠覆性的潜力。然而，去中心化是有代价的：区块链无法规模化，无法及时处理大量甚至适量的交易。例如，比特币每秒处理三笔交易。

问题的根源，也是区块链的限制因素，在于区块链基于免信任（trustless）的对等网络模型。在这个模型中，信息必须在网络中的每一跳上传播和验证。毫无疑问，云分发网络可以解决其他领域的类似性能挑战(例如Akamai或YouTube 解决web和视频的传输性能)，也可以用于解决区块链的可扩展性问题。问题在于，像云这样如此庞大的中心化基础设施扰乱了区块链的去中心化特性，从而消除了区块链的颠覆性潜力。由此，可以提出这样一个问题：云分发网络能否在不破坏区块链去中心化特性的前提下提高其可扩展性？ 答案是肯定的，解决方案的关键基于现有概念（网络中立）提出一个修改的高级版本：可验证中立云分发网络。

由比特币在2008年发起区块链和加密货币革命正在蓬勃发展。主流加密货币的市值虽然剧烈波动，但仍有数千亿美金的规模。区块链的一个独特特性是没有中心化治理。区块链依赖于第三方仲裁(即，一个由验证和认证所有交易的参与节点组成的全球对等网络)。基于区块链的纯粹分布式和去中心化设计，许多人认为，这种系统在加密货币之外的其他领域具有颠覆性的潜力，包括医疗、政府、制造、零售、保险、物联网、共享经济等。许许多多大大小小的高科技公司都在密切关注区块链领域，分析这项新技术将如何影响他们现有或未来的运营。

区块链的一个主要问题是可扩展性。区块链系统吞吐量是用系统能够支持的TPS(每秒交易数)来度量的。比特币目前的平均吞吐量为3个TPS，而Visa中心化系统的平均吞吐量为2000个TPS，每日峰值为4000个TPS，最大吞吐量为5.6万个TPS。没有可扩展性，加密货币系统将很难成为主流，区块链也不太可能在任何其他领域实现其颠覆性潜力。

## 1	什么是区块链？
区块链是一个公共分布式账本，它存储所有过去的交易，本质上是一种类型的数据库，由对等网络中相互连接的多个(数万个)节点创建和共享。为了就数据库的正确副本达成共识，必须对写入数据库的某些规则加以规定。虽然规则可能有所不同，但一般包括以下内容：

* 交易(通常将一定数量的加密货币从一个用户发送给另一个用户)必须包含来自参与节点的数字签名，以便进行身份验证。
* 必须按顺序添加交易。交易不会单个加入账本，相反，它们是成批添加的，称为区块。例如，比特币区块链要求每个新区块都包含一个哈希“难题”的答案，这个答案是由链上最后一个交易区块和正在添加的当前区块所唯一确定的。
* 向区块链添加区块既昂贵又需要竞争。想要向区块链添加区块的各个参与节点要么投资加密货币，要么投资算力，例如，比特币需要的哈希“难题”。这样的参与节点称为矿工，向区块链添加新区块的过程称为挖矿。
* 最长的区块链是最新版本。当这条规则与前面的规则相结合时，这使得成功伪造区块链的代价非常高。即使复制现有的区块链并试图修改最后几个区块，其代价也非常昂贵。一旦区块在网络上得到足够的确认，删除或修改区块在数学上就变得不可能。因此，交易只能添加到区块链，它们永远不会被删除。
* 独立验证。当节点检查区块链数据库的副本时，它应该能够独立地验证前面的所有规则是否已被遵守。如果每个用户都能独立验证区块链，那么所有用户就可以就正确的区块链达成共识。
* 在区块链中添加区块可以收获报酬。因为向区块链写入区块比较困难，所以并不是所有节点都会参与这个过程。许多用户会创建交易，然后要求将交易写入网络，用户通常会支付一定的费用作为矿工报酬。此外，只要矿工在一轮挖矿过程中获胜，并有机会在区块链中添加一个区块，他们就可以将新产出的加密货币分发给自己。
* 区块链发生分叉，通过最长链规则解决。在区块链上达成共识不是立即的，有时区块链可能会出现分叉(数据库的不同副本)。分叉是区块链的公共账本在一段共同的历史之后发生分歧，账本的不同版本共存。节点通过选择网络上最长的区块链，可以解决分叉问题。


## 2	区块链可扩展性问题
在解释区块链可扩展性问题之前，让我们先看看它在现实中是如何表现的。图1和图2显示了比特币和以太坊这两种主流加密货币的交易积压情况。你可以看到，成千上万的交易定期等待区块链处理。为了增加被矿工选中“上链"的可能性，用户(自愿)增加了交易费。因此，交易费绝不是微不足道的，在交易拥堵期间，交易费可能会大幅增长。



+ http://melconway.com/Home/Committees_Paper.html
+ http://www.melconway.com/Home/Conways_Law.html
+ https://blog.gardeviance.org/2015/03/on-pioneers-settlers-town-planners-and.html
+ https://queue.acm.org/detail.cfm?id=3185224
+ https://blog.gardeviance.org/2015/03/on-pioneers-settlers-town-planners-and.html
+ http://dev2ops.org/2010/02/what-is-devops/


+ https://en.wikipedia.org/wiki/Nonviolent_Communication
+ https://devops-research.com/
+ https://www.mendix.com/what-does-bimodal-it-mean/


+ http://www.hbrchina.org/2018-09-29/6480.html

## 数学

+ http://www.acadiau.ca/~pranjan/links/journal_ranking.pdf
+ http://www.zjujournals.com/CN/qkw/home.shtml
+ http://www.math.zju.edu.cn/
+ http://www.actamath.com/Jwk_sxxb_cn/CN/volumn/home.shtml
+ http://www.scichina.com/
+ http://www.amjcu.zju.edu.cn/amjcua/
+ http://www.applmath.com.cn/CN/volumn/home.shtml
+ http://sltj.chinajournal.net.cn/WKB2/WebPublication/index.aspx?mid=SLTJ
+ http://www.tjyjc.com/
+ http://www.erj.cn/cn/default.aspx
+ 国内暂时没有看到专门的统计的权威期刊，学科评审只列了经济研究
外文期刊中的四大天王 jrssb aos jasa biometrika
以及和四大天王并驾齐驱的 joe
这上面的五大期刊应该是统计学最为权威的期刊
https://www.zhihu.com/question/35469777
http://blog.sciencenet.cn/blog-84348-686300.html


1. Tao Feng:

Finite flag-transitive affine planes with a solvable automorphism group. J. Comb. Theory, Ser. A 152: 225-254 (2017)

2. Tao Feng, Koji Momihara, Qing Xiang:
A family of m-ovoids of parabolic quadrics. J. Comb. Theory, Ser. A 140: 97-111(2016)

3. Tao Feng:
A Characterization of Two-Weight Projective Cyclic Codes. IEEE Trans. Information Theory 61(1): 66-71 (2015)

4. Tao Feng, Koji Momihara, Qing Xiang:
Cameron-Liebler line classes with parameter x=(q2-1)/2. J. Comb. Theory, Ser. A133: 307-338 (2015)

5. Tao Feng, Koji Momihara:
Evaluation of the Weight Distribution of a Class of Cyclic Codes Based on Index 2 Gauss Sums. IEEE Trans. Information Theory 59(9): 5980-5984 (2013)

6. Tao Feng, Koji Momihara:
Three-class association schemes from cyclotomy. J. Comb. Theory, Ser. A 120(6): 1202-1215 (2013)