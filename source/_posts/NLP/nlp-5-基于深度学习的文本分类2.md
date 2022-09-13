---
title: nlp-5-基于深度学习的文本分类2
author: Genening
# thumbnail: /gallery/thumbnail/
date: 2020-07-25 20:05:41
updated: 2020-07-25 20:05:41
categories: NLP
tags: nlp
---

## 前言
昨天我们采用了fasttext进行文本处理分类，今天我们使用word2vec模型进行训练。

## 什么是word2vec模型？
word2vec工具主要包含两个模型：跳字模型（skip-gram）和连续词袋模型（continuous bag of words，简称CBOW），以及两种高效训练的方法：负采样（negative sampling）和层序softmax（hierarchical softmax）。值得一提的是，word2vec词向量可以较好地表达不同词之间的相似和类比关系。

<!--more-->
自然语言是一套用来表达含义的复杂系统。在这套系统中，词是表义的基本单元。在机器学习中，如何使用向量表示词？顾名思义，词向量是用来表示词的向量，通常也被认为是词的特征向量。近年来，词向量已逐渐成为自然语言处理的基础知识。

NLP（自然语言处理）里面，最细粒度的是 词语，词语组成句子，句子再组成段落、篇章、文档。所以处理 NLP 的问题，首先就要拿词语开刀。词语，是人类的抽象总结，是符号形式的（比如中文、英文、拉丁文等等），所以需要把他们转换成数值形式，或者说——嵌入到一个数学空间里，这种嵌入方式，就叫词嵌入（word embedding)，而 Word2vec，就是词嵌入（ word embedding) 的一种。简单点来说就是把一个词语转换成对应向量的表达形式，来让机器读取数据。

最后强调一下，word2vec一个NLP工具，它可以将所有的词向量化，这样词与词之间就可以定量的去度量他们之间的关系，挖掘词之间的联系。word2vec主要包含两个模型Skip-gram和CBOW。以及两种高效的训练方法负采样，层序softmax。[引用博客来源](https://blog.csdn.net/yu5064/article/details/79601683)

## 搭建word2vec模型
```
## 1
import logging
import random

import numpy as np
import torch

logging.basicConfig(level=logging.INFO, format='%(asctime)-15s %(levelname)s: %(message)s')

# set seed
seed = 666
random.seed(seed)
np.random.seed(seed)
torch.cuda.manual_seed(seed)
torch.manual_seed(seed)


## 2
# split data to 10 fold
fold_num = 10
data_file = './train_set.csv'
import pandas as pd


def all_data2fold(fold_num, num=10000):
    fold_data = []
    f = pd.read_csv(data_file, sep='\t', encoding='UTF-8')
    texts = f['text'].tolist()[:num]
    labels = f['label'].tolist()[:num]

    total = len(labels)

    index = list(range(total))
    np.random.shuffle(index)

    all_texts = []
    all_labels = []
    for i in index:
        all_texts.append(texts[i])
        all_labels.append(labels[i])

    label2id = {}
    for i in range(total):
        label = str(all_labels[i])
        if label not in label2id:
            label2id[label] = [i]
        else:
            label2id[label].append(i)

    all_index = [[] for _ in range(fold_num)]
    for label, data in label2id.items():
        # print(label, len(data))
        batch_size = int(len(data) / fold_num)
        other = len(data) - batch_size * fold_num
        for i in range(fold_num):
            cur_batch_size = batch_size + 1 if i < other else batch_size
            # print(cur_batch_size)
            batch_data = [data[i * batch_size + b] for b in range(cur_batch_size)]
            all_index[i].extend(batch_data)

    batch_size = int(total / fold_num)
    other_texts = []
    other_labels = []
    other_num = 0
    start = 0
    for fold in range(fold_num):
        num = len(all_index[fold])
        texts = [all_texts[i] for i in all_index[fold]]
        labels = [all_labels[i] for i in all_index[fold]]

        if num > batch_size:
            fold_texts = texts[:batch_size]
            other_texts.extend(texts[batch_size:])
            fold_labels = labels[:batch_size]
            other_labels.extend(labels[batch_size:])
            other_num += num - batch_size
        elif num < batch_size:
            end = start + batch_size - num
            fold_texts = texts + other_texts[start: end]
            fold_labels = labels + other_labels[start: end]
            start = end
        else:
            fold_texts = texts
            fold_labels = labels

        assert batch_size == len(fold_labels)

        # shuffle
        index = list(range(batch_size))
        np.random.shuffle(index)

        shuffle_fold_texts = []
        shuffle_fold_labels = []
        for i in index:
            shuffle_fold_texts.append(fold_texts[i])
            shuffle_fold_labels.append(fold_labels[i])

        data = {'label': shuffle_fold_labels, 'text': shuffle_fold_texts}
        fold_data.append(data)

    logging.info("Fold lens %s", str([len(data['label']) for data in fold_data]))

    return fold_data


fold_data = all_data2fold(10)


## 3
# build train data for word2vec
fold_id = 9

train_texts = []
for i in range(0, fold_id):
    data = fold_data[i]
    train_texts.extend(data['text'])
    
logging.info('Total %d docs.' % len(train_texts))


## 4
logging.info('Start training...')
from gensim.models.word2vec import Word2Vec

num_features = 100     # Word vector dimensionality
num_workers = 8       # Number of threads to run in parallel

train_texts = list(map(lambda x: list(x.split()), train_texts))
model = Word2Vec(train_texts, workers=num_workers, size=num_features)
model.init_sims(replace=True)

# save model
model.save("./word2vec.bin")


## 5
# load model
model = Word2Vec.load("./word2vec.bin")

# convert format
model.wv.save_word2vec_format('./word2vec.txt', binary=False)

```

## 结语
现在虽然明白了word2vec的工作原理，但是亲手实践这个模型的能力还是略为欠缺，需要仔细研究一下源码，好好学习一下。另外，这个模型非常大，一般电脑没有办法训练这个网络，因为权重矩阵太大，动不动就是几百上千万的参数，所以需要很长的训练时间，不建议使用个人电脑来运行这个模型，可以考虑在服务器中运行此模型。