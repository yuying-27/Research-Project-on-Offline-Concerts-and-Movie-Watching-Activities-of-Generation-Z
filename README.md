# 多源数据分析下 Z 世代线下演唱会支付意愿预测与体验优化研究

> 融合 **550 份问卷** + **2006 条社交媒体评论**，构建「**消费者画像 → 支付意愿预测 → 舆情诊断 → 方案择优**」的完整数据分析链路。

本项目面向 Z 世代线下演唱会消费场景，综合运用 K-means 聚类、因子分析、随机森林回归、LDA 主题模型、SnowNLP 情感分析与 TOPSIS 评价，覆盖从数据清洗、特征工程、无监督/有监督建模到多准则决策的全流程。**完整的方法论逻辑、结果解读与效度论证见 [深度分析报告](分析报告.md)**。

---

## 核心结果速览

| 模块 | 关键结论 | 核心指标 |
|:---|:---|:---|
| 消费者画像 | 三类人群：狂热核心型 53.8% / 边缘观望型 24.5% / 价格敏感型 21.6% | Bootstrap Jaccard **0.8746** |
| 支付意愿预测 | "座位影响价值 + 购票选位满意度"构成双因素主导 | 测试集 R² **0.6617**，Top2 贡献 **69.19%** |
| 舆情诊断 | 座位/实名制为最高风险痛点 | 主题占比 **41.8%**，风险指数 **0.2377** |
| 方案评价 | 综合运营优化方案最优 | TOPSIS 贴近度 **0.7277** |

---

## 分析方法一览

| 环节 | 方法 | 输出 |
|:---|:---|:---|
| 数据清洗 | 双源清洗流水线 + jieba 领域分词 | 550 份 / 2006 条高质量数据 |
| 分群建模 | K-means（肘部法则 + 轮廓系数 + Bootstrap 稳定性检验） | 3 类消费者 + 画像 |
| 降维与预测 | PCA 因子分析 + 随机森林回归 + PDP 非线性分析 | 特征重要性 + 边际效应 |
| 文本挖掘 | LDA 主题模型 + SnowNLP 情感 + TF-IDF + 共现网络 | 主题分布 + 风险指数 |
| 决策优化 | TOPSIS 多准则评价 | 方案排序 |

**技术栈**：Python · pandas · scikit-learn · jieba · gensim · SnowNLP · networkx · matplotlib

---

## 项目结构

```
.
├── README.md              # 项目门面（本文件）
├── 分析报告.md             # 深度分析报告（方法论 / 结果解读 / 效度论证）
├── code/                  # 分析代码
│   ├── 02_consumer_profiling/     # 消费者画像（聚类）
│   ├── 03_willingness_prediction/ # 支付意愿预测
│   ├── 04_sentiment_analysis/     # 舆情与文本分析
│   └── 05_strategy_optimization/  # 方案评价
├── data/
│   ├── data/              # 原始与清洗数据
│   └── 变量说明.md         # 数据变量说明
├── output/images/         # 结果图表（fig01–fig19）
└── requirements.txt
```

---

## 快速开始

```bash
pip install -r requirements.txt

# 消费者画像
python code/02_consumer_profiling/elbow_silhouette.py
python code/02_consumer_profiling/kmeans_scatter.py
python code/02_consumer_profiling/heatmap_radar_validation.py

# 支付意愿预测
python code/03_willingness_prediction/pca_random_forest.py

# 舆情与文本分析
python code/04_sentiment_analysis/text_features.py
python code/04_sentiment_analysis/lda_snownlp.py

# 方案评价
python code/05_strategy_optimization/topsis_evaluation.py
```

---

## 文档导航

| 文档 | 内容 |
|:---|:---|
| 📊 [分析报告.md](分析报告.md) | 研究设计逻辑、结果深度解读、效度与稳健性论证、决策启示 |
| 📖 [data/变量说明.md](data/变量说明.md) | 问卷与文本数据的变量定义、取值编码、清洗规则 |
| 💻 [code/](code/) | 全流程分析源代码 |

---

## 数据与局限

- 问卷数据已脱敏，不含受访者个人身份信息。
- **文本数据年龄不可控**：社交媒体评论无法按年龄筛选，可能混入非 Z 世代用户。文本结论的适用主体为「**市场整体舆论**」，不作「Z 世代态度」的直接证据，与问卷做**三角验证**（完整论证见 [分析报告 §七](分析报告.md)）。
