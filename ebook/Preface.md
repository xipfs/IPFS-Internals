# 前言

### IPFS : A peer-to-peer hypermedia protocolto make the web faster, safer, and more open.

星际文件系统（InterPlanetary File System，缩写 IPFS[^1]）是一个旨在创建持久且分布式存储和共享文件的网络传输协议。它是一种内容可寻址的对等超媒体分发协议。在 IPFS 网络中的节点将构成一个分布式文件系统。从2014年开始在 Protocol Labs 开源社区的帮助下发展。其最初由 Juan Benet 设计。IPFS 可以让我们的互联网速度更快、更安全、并且更加的开放。IPFS 协议的目标是替代 HTTP 协议。

目前互联网大量依靠 HTTP 协议进行通讯，HTTP 协议由蒂姆·伯纳斯-李于1989年在欧洲核子研究组织（CERN）所发起，至今已经快30年，它的不足逐渐显露了出来：

+ HTTP 的中心化是低效的, 并且成本很高。
+ 网络上的文件经常被删除。
+ 中心化限制了 Web 的成长。
+ 网络上的应用高度依赖主干网。


为了解决以上的问题，IPFS 应运而生，它将为我们构建一个更快、更健壮和更安全的存储网络。


IPFS 还能与区块链进行无缝的衔接，随着区块链技术的飞速发展，链上需要存储的数据越来越多，出于性能和成本的限值，区块链无法将所有数据都存于主链之上，最好的办法就是将数据存于主链之外，然后通过对数据进行加密， 哈希等手段来防止数据被篡改， 在区块链上保存所存数据的哈希值, 从而减少主链对数据的存储需求。

随着 IPFS 的发展，当 IPFS 的节点遍布世界的各个角落， IPFS 将会重构我们传递、获取、存储数据的方式。它的另一个项目 Filecoin[^2] 则为这一系统建立了激励体系来确保系统的运转，IPFS 或许会在不久的将来成为互联网应用的一个底层基础设施深刻的影响着我们的生活。


## 本书主要内容

第1章 介绍 IPFS 产生的背景、项目架构和相关的基础知识。

第2章 介绍 IPFS 环境的搭建和配置，主要包括如何通过源代码编译 IPFS 和 搭建 IPFS 开发调试环境。

第3章 介绍 IPFS 涉及到的一些底层技术包括： S/Kademlia DHT、 BitTorrent、 Git、 SFS、 Merkle tree等。

第4章 介绍  Multiformats 协议的设计与实现。

第5章 对统一的数据模型 IPLD 进行详细的剖析。

第6章 详解 IPFS 存储层的设计与实现，并对存储层中的关键代码进行分析。

第7章 将会对 IPFS Bitswap 数据交换层的内部实现机制进行深入的分析，并且对其中的关键代码进行详细的讲解。

第8章 对 IPFS 的网络层的设计与实现进行深入的分析，并且对其中的关键代码进行详细的讲解。

第9章 深入剖析 IPFS 集群的设计与实现。

第10章-11章 通过实战项目让读者熟练掌握 IPFS，进入 IPFS 的大门。


## 本书面向读者

+ 对 IPFS 感兴趣的爱好者。
+ 有一定开发基础，想深入了解 IPFS 设计与实现的开发人员。

## 如何阅读本书

本书每一章都建立在前一章 的基础上，但每一章又都可以阅读。本书内容主要围绕对 IPFS 设计与实现展开讨论。读者可以从第1章开始，按顺序阅读本书并运行每一章的源代码，也可以直接跳到感兴趣的章节阅读，必要时再阅读其他章节。

## 参考资料

由于目前 IPFS 资料匮乏，IPFS 参考资料主要还是以官方文档为主。然后还通过搜索引擎查阅分布于网络上的各种资料。笔者在本书创作过程中从下面所列资料中获得了极大的帮助，大家也可以从以下信息中找到更多关于 IPFS 的资料。

+ Filecoin Documentation [^2]​
+ IPFS Documentation [^3]​
+ IPFS 中国社区[^4]​
+ IPFSER[^5]​
+ 巴比特[^6]​
+ StackOverflow 
+ Wikipedia

## 下载本书源代码

[IPFS-Internals](https://github.com/xipfs/IPFS-Internals)

## 勘误和支持

尽管我们仔细对待本书的写作，由于水平和能力有限，错误还是不可避免。如果你在书中发现不妥或错误之处，请加入上面微信群获得支持和帮助。

## 致谢



## 参考文献

+ [1] https://en.wikipedia.org/wiki/InterPlanetary_File_System​
+ [2] https://filecoin.io/​
+ [3] https://docs.ipfs.io/​
+ [4] http://www.ipfs.cn/​
+ [5]  http://ipfser.org​
+ [6] https://www.8btc.com/p/ipfs

-----
​

[^1]: https://en.wikipedia.org/wiki/InterPlanetary_File_System
[^2]: https://filecoin.io/​
[^3]: https://docs.ipfs.io/​
[^4]: http://www.ipfs.cn/​
[^5]:  http://ipfser.org​
[^6]: https://www.8btc.com/p/ipfs​​