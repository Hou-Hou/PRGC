# PRGC: Potential Relation and Global Correspondence Based Joint Relational Triple Extraction
This repository contains the source code and dataset for the paper: **PRGC: Potential Relation and Global Correspondence Based Joint Relational Triple Extraction.** Hengyi Zheng, Rui Wen, Xi Chen et al. ACL 2021.

## Overview

Paper：[PRGC: Potential Relation and Global Correspondence Based Joint Relational Triple Extraction (aclanthology.org)](https://aclanthology.org/2021.acl-long.486.pdf)

原始开源代码：[https://github.com/hy-struggle/PRGC](https://link.zhihu.com/?target=https%3A//hub.fastgit.xyz/hy-struggle/PRGC)

原理参考：[论文笔记—PRGC: Potential Relation and Global Correspondence Based Joint Relational Triple Extraction - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/440495418)

![image-20210622212609011](https://raw.githubusercontent.com/hy-struggle/img/master/markdown/20210622212609.png)

## 2023.2

添加baidu数据集，调试模型bug

|       | 数量  |                           数据示例                           |
| :---- | :---- | :----------------------------------------------------------: |
| train | 55959 | {"text": "《今晚会在哪里醒来》是黄家强的一首粤语歌曲，由何启弘作词，黄家强作曲编曲并演唱，收录于2007年08月01日发行的专辑《她他》中","spo_list": [   {"predicate": "作曲", "object_type": "人物", "subject_type": "歌曲", "object": "黄家强", "subject": "今晚会在哪里醒来"},   {"predicate": "所属专辑", "object_type": "音乐专辑", "subject_type": "歌曲", "object": "她他", "subject": "今晚会在哪里醒来"},   {"predicate": "歌手", "object_type": "人物", "subject_type": "歌曲", "object": "黄家强", "subject": "今晚会在哪里醒来"},   {"predicate": "作词", "object_type": "人物", "subject_type": "歌曲", "object": "何启弘", "subject": "今晚会在哪里醒来"}]} |
| test  | 13417 |                                                              |
| dev   | 11191 |                                                              |

关系类型：18种 

## Requirements

The main requirements are:

  - python==3.7.9
  - pytorch==1.6.0
  - transformers==3.2.0
  - tqdm

## Datasets

- [NYT*](https://github.com/weizhepei/CasRel/tree/master/data/NYT) and [WebNLG*](https://github.com/weizhepei/CasRel/tree/master/data/WebNLG)(following [CasRel](https://github.com/weizhepei/CasRel))
- [NYT](https://drive.google.com/file/d/1kAVwR051gjfKn3p6oKc7CzNT9g2Cjy6N/view)(following [CopyRE](https://github.com/xiangrongzeng/copy_re))
- [WebNLG](https://github.com/yubowen-ph/JointER/tree/master/dataset/WebNLG/data)(following [ETL-span](https://github.com/yubowen-ph/JointER))

Or you can just download our preprocessed [datasets](https://drive.google.com/file/d/1hpUedGxzpg6lyNemClfMCeTXeaBBQ1u7/view?usp=sharing).

## Usage

**1. Get pre-trained BERT model for PyTorch**

Download [BERT-Base-Cased](https://huggingface.co/bert-base-cased/tree/main) which contains `pytroch_model.bin`, `vocab.txt` and `config.json`. Put these under `./pretrain_models`.

**2. Build Data**

Put our preprocessed datasets under `./data`.

**3. Train**

Just run the script in `./script` by `sh train.sh`.

For example, to train the model for NYT* dataset, update the `train.sh` as:

```
python ../train.py \
--ex_index=1 \
--epoch_num=100 \
--device_id=0 \
--corpus_type=NYT-star \
--ensure_corres \
--ensure_rel
```

**4. Evaluate**

Just run the script in `./script` by `sh evaluate.sh`.

For example, to train the model for NYT* dataset, update the `evaluate.sh` as:

```
python ../evaluate.py \
--ex_index=1 \
--device_id=0 \
--mode=test \
--corpus_type=NYT-star \
--ensure_corres \
--ensure_rel \
--corres_threshold=0.5 \
--rel_threshold=0.1
```

