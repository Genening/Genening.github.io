---
title: expression_estimate_parameters
author: Genening
# thumbnail: /gallery/thumbnail/
date: 2021-07-23 08:22:28
updated: 2021-07-23 08:22:28
categories: Bioinformatics
tags: TPM-RPKM-FPKM
---
## 前言
在转录组学中，表达定量分析是一个非常重要的步骤，可以说是整个转录组的支撑，一个好的定量手段和结果可以让后续的差异分析工作得以展开。在转录组当中，用于定量的统计量有三个，分别是TPM/RPKM/TPKM，这三个统计量的统计结果有所区别，但结果基本上一致，不同的是三种参数的可解释性不太一样，接下来我们就仔细聊聊这三个定量参数。

<!--more-->

## 1. 概述]

在RNA-Seq的分析中，为了获得差异表达基因，只需要对不同基因的测序Read数进行比较即可。然而比对到不同基因上的Read数目并不能直接用于比较这两个基因的表达量差异，因为在RNA-seq中有一个很浅显的道理，基因越长，比对到此基因上的Read就会越多；测序深度越大，那么本次RNA-seq的所有Read数都会增加。也就是说Read数除了和基因表达量相关外，也和**基因的长度**、**测序深度** 有关，因此为了比较多个RNA-seq重复（测序深度有一定差异）的不同基因（基因长度有一定差异）之间的表达量差异，那么就不能使用Read数直接进行比较，而是需要对Read数进行标准化。而标准化对应的就正是两个步骤——测序深度标准化和基因长度标准化。

对应这些标准化操作，生信分析常用分析参数如下：

* RPKM: Reads Per Kilobase of exon model per Million mapped reads (每千个碱基的转录每百万映射读取的reads)

* FPKM: Fragments Per Kilobase of exon model per Million mapped fragments(每千个碱基的转录每百万映射读取的fragments)

* RPM/CPM: Reads/Counts of exon model per Million mapped reads (每百万映射读取的reads)

* TPM：Transcripts Per Kilobase of exon model per Million mapped reads (每千个碱基的转录每百万映射读取的Transcripts)


## 2. RPKM-Reads Per Kilobase of exon model per Million mapped reads
根据RPKM的全称我们可以得知其含义：代表每百万reads中来自于某基因每千碱基长度的reads数。根据这个含义我们有如下公式：


$RPKM = \frac{TotalReads}{MappedReads(Millions)*ExonLength(KB)}$


RPKM是将map到基因的read数除以map到基因组上的所有read数(以million为单位)与RNA的长度(以KB为单位)。RNA-seq是二代测序技术中用来表示基因表达量或丰度的方法。在衡量基因表达量时，若是单纯以map到的read数来计算基因的表达量，在统计上是不合理的。因为在随机抽样的情况下，序列较长的基因被抽到的机率本来就会比序列短的基因较高，如此一来，序列长的基因永远会被认为表达量较高，而错估基因真正的表现量，所以Ali Mortazavi等人在2008年提出以RPKM在估计基因的表现量。

## 3. FPKM-Fragments Per Kilobase of exon model per Million mapped fragments
同样顾名思义，FPKM即每千个碱基的转录每百万映射读取的fragments数。假如有1百万个reads映射到了人的基因组上，那么具体到每个外显子呢，有多少映射上了呢，而外显子的长度不一，那么每1K个碱基上又有多少reads映射上了呢，这大概就是这个FPKM的直观解释。有如下公式

$FPKM = \frac{TotalExonFragments}{MappedReads(Millions)*ExonLength(KB)}$

这个表达式与RPKM的计算方式如出一辙，这也意味着两者的定量思路非常一致，但是不同的是，RPKM聚焦于reads数本身，而FPKM聚焦于fragments数。在二代测序中分为单端测序和双端测序。单端测序得到一条条的read，这个方式对应reads；双端测序对应得到可以匹配的2条序列，也就是从左端和右端分别测得的相同的序列片段，两者配对称为一个fragment，当然也存在配对不上的read，这种read单独算一个fragment。因为现在的测序几乎都是双端测序了，所以自然而然地RPKM就用得少了。两者的科学解释性几乎是相同的。


## 4. TPM-Transcipts Per Kilobase of exon model per Million mapped reads

### TPM的计算方法
1. 标准化基因长度：将所有基因的Read数除以基因长度（基因长度单位为kb）；

2. 计算总Read数：计算每一个样本的总Read数，然后将其换算为以百万位单位（M）；

3. 标准化总Read数：将所有基因的Read数除以总Read数；




## 结语

目前都已经推荐进行TPM标准化，不再使用了RPKM、FPKM了，为何会这样？

将每个转录本的相应RPKM和TPM值进行加总后，可以发现不同转录本的总RPKM并不相同，而进行TPM变换后的加总TPM值是相同的。事实上所有进行TPM变换后的转录本的加总TPM值都是相同的（正常情况下，是百万）。

由于RNA-seq就是为了通过比较不同样本间的标准化后的Read数差异来得出基因表达量差异的结果的，那么不同样本的加总RPKM不同，就会导致无法通过直接比较RPKM值确定两者的差异。

举例来说，在不考虑统计差异的情况下，以基因A为例，Rep1的RPKM值为1.43，Rep3的RPKM值是1.42，那么能说基因A在Rep1中的表达量大于Rep3中的表达量吗？

答案是不能，因为Rep1的总RPKM值是4.29，而Rep3的总RPKM值是4.25，虽然Rep1中基因A的RPKM大，但是Rep1的总RPKM值也是较大的（说白了，RPKM的测序深度标准化并不完善）。

而对于TPM数据就不同了，由于总TPM都是相同的，Rep1中基因A的TPM值3.33大于Rep3中基因A的TPM值3.326，所以在不考虑统计学差异的情况下，可以直接得出Rep1中基因A的表达量是要大于Rep3的。