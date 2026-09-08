---
title: "TicTac: Time-aware Supervised Fine-tuning for Automatic Text Dating"
title_zh: TicTac：面向自动文本定年的时序感知监督微调
authors: "Han Ren, Minna Peng"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1129.pdf"
tags: ["query:evidence-qa"]
score: 4.0
evidence: 面向文档定年的时序语义建模，与文档内跨句时间抽取相关但目标不同
tldr: 自动文档定年要求模型理解文本间的时序关联，而预训练模型常采用与时序无关的表征。TicTac提出时序感知监督微调框架，通过对比学习建模文档之间的两类时序关系，并用度量学习刻画历史文本的相对时间距离，以捕捉长时间跨度语料中的时间语义。实验表明该框架提升了自动文本定年任务的准确性，显示显式利用文档时序关联对时间敏感的文本理解的价值。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1129/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1568, \"height\": 901, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1129/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1591, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1129/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1571, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1129/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1607, \"height\": 641, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1129/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1129/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1129/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1552, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1129/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1587, \"height\": 704, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1129/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1631, \"height\": 1450, \"label\": \"Table\"}]"
motivation: 现有预训练模型缺少时间感知能力，难以捕捉长时间跨度文档中的时间关联，影响自动定年。
method: TicTac用时序相关的对比学习与度量学习进行监督微调，建模文档间的相对时间关系。
result: TicTac在自动文本定年任务上利用文档间时序关联取得更好效果，验证了时间感知表示的有效性。
conclusion: 为需要时间语义的文档理解提供了将时序关系注入预训练模型的新视角。
---

## Abstract
Pre-trained langauge models have achieved success in many natural language processing tasks, whereas they are trapped by the time-agnostic setting, impacting the performance in automatic text dating. This paper introduces TicTac, a supervised fine-tuning model for automatic text dating. Unlike the existing models that always ignore the temporal relatedness of documents, TicTac has the ability to learn temporal semantic information, which is helpful for capturing the temporal implications over long-time span corpora. As a fine-tuning framework, TicTac employs a contrastive learning-based approach to model two types of temporal relations of diachronic documents. TicTac also adopts a metric learning approach, where the temporal distance between a historical text and its category label is estimated, which benefits to learn temporal semantic information on texts with temporal ordering. Experiments on two diachronic corpora show that our model effectively captures the temporal semantic information and outperforms state-of-the-art baselines.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文核心问题与整体含义（研究动机和背景）

- 自动文本定年（Automatic Text Dating, ATD）旨在根据文档内容推断其撰写时间或所属历史时期，是数字人文、时间敏感问答等下游任务的基础环节。
- 现有预训练语言模型（PLMs）虽然NLP表现优秀，但其表示是**时间无关（time-agnostic）**的，难以捕捉语言在长期内的动态变化，导致在历史文本定年等时间敏感任务上效果受限。
- 已有方法存在三类问题：
  - 从头训练大模型成本高、数据少、有灾难性遗忘风险；
  - 依靠词汇语义变化的模型忽视了**文档之间的时序关联性**；
  - 多数研究把时间类别视为独立离散标签，忽略了它们之间的**顺序关系**。
- 论文提出 TicTac，一种面向 ATD 的时序感知监督微调模型，旨在以低训练成本建模语言演化、捕捉文档间时态关联，并利用时间类别的有序性提高定年精度。

## 2. 方法论：TicTac 模型

### 2.1 总体框架

- 采用标准的监督微调范式，基础编码器为 BERT；文档输入 BERT 后取 `[CLS]` 向量作为文档表示。
- 损失函数由三部分共同组成：  
  \[
  L = L_{CE} + L_{CLR} + L_{CLA} + L_{TOC}
  \]
  - \(L_{CE}\)：常规交叉熵分类损失；
  - \(L_{CLR}\)：基于**相对时间关系**的对比学习损失；
  - \(L_{CLA}\)：基于**绝对时间关系**的对比学习损失；
  - \(L_{TOC}\)：面向时序类别的**序数分类损失**（基于 EMD）。

### 2.2 时序感知对比学习（Time-aware Contrastive Learning）

- 定义两类时间关系：
  - **相对时间关系**：文档与文档之间的局部关系；
  - **绝对时间关系**：文档与时间类别标签之间的全局关系。
- **相对时序对比学习（CLR）**：一个锚点文档与同时间类别的其他文档构成正样本对，不同类别的构成负样本对，采用监督对比学习，拉近同类文档、推开异类文档。
- **绝对时序对比学习（CLA）**：引入可学习的标签嵌入矩阵 \(W_{label}\)，每个时间类别 t 对应一个标签向量 \(z_l\)；以标签向量作为锚点，文档嵌入与其正确类别嵌入拉近，与错误类别嵌入推开，使文档围绕各自时间类别中心聚拢。

### 2.3 时序感知序数分类（Time-aware Ordinal Classification）

- 相比交叉熵只关注是否完全匹配，本文强调“分错得越远、惩罚应越大”，故将 ATD 视为 **序数分类（ordinal classification）** 问题。
- 使用 **Earth Mover’s Distance（EMD）** 损失衡量预测分布与真实分布之差：
  - 定义预测累积分布函数 CDF_pred，与真实 CDF（根据真实标签构造的阶梯函数），逐一类别计算二者累积概率差的平方和。
- 该损失近似于“预测时间与真实时间的相对距离”，可使模型学习时间类别的排序信息，即使预测错误也更倾向于邻近类别。

## 3. 实验设计

### 3.1 数据集与评估

- 使用两个历时语料：
  - **Twenty-Four Histories Corpus（中国二十四史语料）**：跨度约公元前2500年到公元1600年，包含约4000万汉字、2647卷，划分为12个历史时期类别；
  - **Royal Society Corpus（英国皇家学会语料）**：收录1660–1880年的9779篇英文论文，按每20年划分为11个时间类。
- 两种语料均将文本切成约420字符片段，按 8:1:1 划分训练、验证与测试集。
- 评估指标：精确率（P）、召回率（R）、F1、分类精度（C-acc）、相邻精度（A-acc）。

### 3.2 对比方法

- **非预训练模型**：LSTM、TALM；
- **预训练模型**：BERT、SBERT、RoBERTa（直接微调）；
- **序数分类方法**：WKL（加权Kappa损失）、OLL（序数对数损失），均以 BERT 为底座；
- **大语言模型**：Qwen2.5（7B）、Baichuan2（7B）、GPT-4o-mini（通过 prompt 直接进行分类）；
- 以及 **EMD、OLL、WKL、SOFT 等序数损失替换实验**和**消融实验**。

### 3.3 资源与算力

- 论文在实验设置中提到：训练使用 **单张 RTX 4090 GPU（24GB 显存）+ 10 vCPU**；
- 学习率 \(1\times10^{-5}\)，batch size 32，early stopping patience 为 5 epochs；
- 未提及具体训练总时长、GPU 使用数量等更详细的计时信息。

## 4. 实验数量与充分性

- 主要实验包括：
  1. **整体性能对比实验**：在两组数据集上与 10 个方法比较，报告 P、R、F1、C-acc、A-acc；
  2. **消融实验**：逐项移除 CLR、CLA、TOC 三个模块，在两个数据集上分别测试；
  3. **序数损失替换实验**：在 TicTac 框架下对比 EMD、OLL、WKL、SOFT 四种损失；
  4. **可视化分析**：对 TicTac 与 BERT 的文档嵌入做 t-SNE 聚类对比；
  5. **案例研究**：按历史时期逐类别比较 TicTac 与最强的 RoBERTa，检测不同时期的成功率；并绘制混淆矩阵分析易混类别。
- 实验覆盖中文和英文各一组语料，包含多个维度的分析和验证，较全面。但不足之处是未在更多语种或更多数据规模上重复验证，结论的可泛化性仍有限。
- 对比设置总体上是公平的：用相同文本切分和划分方式，PLM 系列配置沿用 Ren et al. (2023)，序数损失类方法使用同一骨架；但大语言模型评估提示词简单，仅允许输出类别名，可能低估了 LLM 在此任务上的真实能力。

## 5. 主要结论与发现

- **TicTac 在两个数据集的几乎所有指标上取得最优**：
  - 二十四史语料：F1 88.36%，C-acc 90.18%，A-acc 95.01%（相比 RoBERTa F1 87.94% 提升有限但一致）；
  - 皇家学会语料：F1 62.60%，C-acc 67.66%，A-acc 91.95%（明显优于最优 PLM RoBERTa 59.96%；也明显优于 WKL 44.40% 和 OLL 59.37%）。
- 非预训练方法总体效果低于预训练模型；直接在原语言语料上微调 BERT/RoBERTa 比从头训练更有效。
- **纯序数分类方法（WKL/OLL）单独使用并不理想**，需要结合时间感知学习目标和合适的序数损失。
- **LLM（含GPT-4o-mini）在ATD任务上表现很差**（F1 往往低于20%），不能简单通过 prompt 完成精细的历史定年，说明任务专用模型仍必要性明显。
- 消融实验表明三个模块均有贡献，删除任一模块都会导致 F1 下降；贡献程度在不同语料上略有差异（二十四史语料中 TOC 贡献最明显，皇家学会语料中 CLA/CLR 也很重要）。
- 序数损失对比中，EMD 损失明显优于 OLL、WKL、SOFT，证明 EMD 更适合利用时间类别的排序语义。
- 可视化显示 TicTac 学到的类别簇内更紧凑、簇间界限更清晰，验证了时间感知表征的有效性。
- 常见错误集中在相邻且时间跨度短的时期（如南朝梁与北朝齐），显示短时间片段区分仍然是难点。

## 6. 优点

- 提出“相对时序关系+绝对时序关系”双重对比学习框架，同时建模文档之间及文档与时间标签之间的时序语义，粒度新颖。
- 将 ATD 视为序数分类问题，以 EMD 损失描述时间距离，比简单交叉熵更贴合时间推断语义，结果也验证了这一设计的价值。
- 采用轻量级的 PLM 微调范式，避免昂贵的从零预训练，易于扩展到其他时间敏感任务。
- 实验设计完整：同时进行主对比、逐模块消融、损失替换、可视化和案例分析，多角度验证模型有效性。
- 同时使用中文历史语料和英文历史科学语料，兼顾跨语言与跨文体验证。

## 7. 不足与局限

- **数据集覆盖有限**：只验证了中文和英文，未覆盖其他语言或更大范围的多元历时语料，通用性尚未证实。
- **短时间跨度文本难点**：模型依赖语言演化线索，对于时间跨度短或缺乏明显时序特征的文本，性能下降；例如皇家学会语料中 1680–1700 和 1720–1740 期F1偏低。
- **资源信息不透明**：未报告训练总时间、能耗或推理成本，难以评估方法相对自己训练模型的经济性。
- **与 LLM 的对比条件不完全均衡**：论文给 LLM 使用简单分类 prompt，无少样本示范、无链式推理或结构化输出约束，这可能低估了大模型的实际能力，需谨慎解读“LLM 远差于 TicTac”这一结果。
- **细微指标提升有限**：在二十四史语料上相对 RoBERTa 提升较小（F1 差约 0.42%），显著性检验也未报告，需更严格的统计验证。
- **依赖性**：方法依赖预定义的时间类别粒度，不同粒度（如逐年、逐十年）的迁移效果未加以探讨。

（完）
