---
title: Improving the Calibration of Confidence Scores in Text Generation Using the Output Distribution’s Characteristics
title_zh: 利用输出分布特性改进文本生成置信度分数的校准
authors: "Lorenzo Jaime Yu Flores, Ori Ernst, Jackie CK Cheung"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-short.15.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 利用输出分布特性改进文本生成置信度校准
tldr: 文本生成中存在多个有效答案，使单一序列的概率难以直接解释为模型自信程度。作者提出仅依赖模型概率分布的任务无关置信度指标，专门面向生成任务，以区分模型是任务不确定还是因为多种有效答案而分散概率。实验验证该方法能提升文本生成模型置信度分数的校准质量，减少低置信度且高风险预测被直接输出的风险。
source: ACL-2025-Short
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short15/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short15/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 750, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short15/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short15/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1589, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short15/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1537, \"height\": 321, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 670, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 748, \"height\": 1042, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 719, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1608, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short15/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1607, \"height\": 1474, \"label\": \"Table\"}]"
motivation: 文本生成存在多个有效答案，现有置信度指标常把多种有效高概率误判为模型不确定。
method: 提出仅基于模型概率分布的任务无关生成置信度度量，适配多有效答案的生成任务。
result: 实验证明新指标能改善生成模型的置信度校准，有助于低置信度输出触发人工复核。
conclusion: 为文本生成场景提供了更准确的置信度信号，提升模型安全性。
---

## Abstract
Well-calibrated model confidence scores can improve the usefulness of text generation models. For example, users can be prompted to review predictions with low confidence scores, to prevent models from returning bad or potentially dangerous predictions. However, confidence metrics are not always well calibrated in text generation. One reason is that in generation, there can be many valid answers, which previous methods do not always account for. Hence, a confident model could assign probability to many sequences because they are all valid, and not because it is unsure about how to perform the task. We propose task-agnostic confidence metrics suited to generation, which rely solely on model probabilities without the need for further fine-tuning or heuristics. Using these, we are able to improve the calibration of BART and Flan-T5 on summarization, translation, and question answering datasets.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义

文本生成模型（如摘要、翻译、问答系统）在实际部署中需要可靠的**置信度分数**，用于标识低质量输出、触发人工复核或让模型在不确定时弃权。然而，现有置信度估计方法大多受分类任务思维影响，**只关注模型输出的 top-1 序列的概率**，这在生成任务中会产生系统性偏差。

核心问题在于：**生成任务通常存在多个同样有效的输出**。一个自信的模型可能将概率分散分配给多个有效序列——这不是因为它"不确定"，而是因为它识别出了多个正确答案。若只看最高概率序列的数值，会错误地将这类输出判定为低置信度，导致置信度分数与输出质量之间校准不良。

论文所提出的方法**用分布的形状（而非单一峰值）来判断模型自信度**，从而做到任务无关、无需额外训练和启发式规则的置信度估计，适用于摘要、翻译、问答等多个开放式文本生成场景。

## 2. 论文提出的方法论

### 核心思想

论文提出，一个**自信的模型**在输出概率分布上应表现出两个特征：
- **对优劣序列有区分度**：分配给"好"序列的概率明显高于"一般"序列；
- **尾部薄（thin tail）**：大量"坏"序列获得的概率极低。

这两个特征无论合法答案数量是一个还是多个都成立，因此更适合生成任务。

### 两种新方法

**方法一：Ratio（概率比值法）**

衡量最高概率序列与第 k 个序列的概率比值：

\[
\text{Ratio}(x) = \frac{p_{\hat{y}^{(1)}}(x)}{p_{\hat{y}^{(k)}}(x)}
\]

- 直觉：自信的模型给 best beam 的概率远高于 average beam；不自信的模型两者接近。
- k 是一个超参数，在验证集上调优，反映任务中"好序列 vs 一般序列"的边界位置。

**方法二：Tail Thinness（尾部薄度）**

借鉴 Huang (2024) 提出的尾厚指标，对 beam search 生成的 N 个序列的概率先做 softmax 归一化，再计算平方和：

\[
\text{Tail Thinness}(x) = \sum_{i=1}^{N} p_{\hat{y}^{(i)}}(x)^2
\]

- 均匀分布 → 值小（粗尾）；退化分布 → 值大（细尾）；
- 与序列级熵表现接近，但对尾部分布的几何形状有更直观的解释，且能对"多个有效序列 + 大量低概率坏序列"（如长尾中存在多峰）的情况给出正确的高置信度打分。

### 推理设置

使用 beam search 生成 N=100 个序列，各序列概率为 token 概率连乘，在推理时直接计算置信度，无需额外训练、NLI 模型或 dropout。

## 3. 实验设计

### 数据集与场景（9 个数据集 × 2 个模型）

| 任务 | 数据集 |
|---|---|
| 翻译 | WMT 2017 DE-EN、RU-EN、FLORES（Filipino） |
| 问答 | SQuAD、HotpotQA |
| 摘要 | DebateSumm、Reddit-TiFu、CNN-DailyMail、XSUM |

### 模型

- BART Base
- Flan-T5 Base
- 均在各自数据集上进行监督微调（SFT），规模较小且无法口头表达置信度，避免与 verbalized confidence 方法混淆。

### 评估方式

- 计算置信度分数与质量分数的 **Spearman 相关系数**（质量分数：翻译用 BLEU、QA 用 F1、摘要用 ROUGE-L）；
- 显著性检验与稳定性评估采用 **bootstrap test**。

### 对比的基线方法

覆盖了四大类已有方法：
1. **基于概率**：ATP（平均 token 概率）、ATE（平均 token 熵）、DAE（dropout 平均熵）、WTP（top-K 加权 token 对数概率）；
2. **基于相似度/分歧度**：DSM（dropout 相似度，METEOR）、DVB（dropout 方差，BLEU）、DVK（dropout KL 散度）；
3. 额外补充对照：Beam Entropy、Sum Top-K Probs；
4. 未直接实现的类别：NLI 语义分组、OOD 检测、verbalized confidence（因模型不具备此能力或方法不适用）。

## 4. 资源与算力

论文在实现细节中说明：
- 微调和推理使用 **1 块 NVIDIA A100 GPU**；
- 总耗时约 **80 小时**；
- 学习率 5e-5，batch size 为 10，训练最多 3 个 epoch，多数数据集上采用 early stopping（验证集 loss 连续 2 步不改善则停止）；
- HotpotQA、WMT RU-EN 和 DebateSumm 未使用 early stopping（其中 WMT RU-EN 和 HotpotQA 训练步数达 6000/26835，远高于其他数据集）。

计算开销的说明：相比大多数概率类基线，Ratio 和 Tail 方法需要额外进行多序列 beam search 及概率统计，计算量相对较大。但相比 DAE/DVB/DSM 等需要多次 dropout 采样额外输出（图中是 10 次）的方法，两者计算量相近，甚至更少。

## 5. 实验数量与充分性

### 实验数量

- **16 组模型-数据集组合**（2 个模型 × 9 个数据集，注意 FLORES 只报告了英文作为源语言的子集及部分数据集子集）；
- 主体实验在 9 个数据集上与 7 种基线对比；
- 报告了 k 值对实验结果的曲线分析（每个模型绘制了 9 组 k 的曲线）；
- 含失败样本的定性分析、鲁棒性示例、以及尾部方法的额外补充实验（表5）；
- 在附录中对 2 个额外基线（Beam Entropy、Sum Top-K）做了补充对比。

### 充分性与客观性分析

- **优点**：覆盖了 3 种文本生成任务 × 9 个数据集，与 7 种已有方法对比，并用 bootstrap 检验确认显著性；表格标注了每个单元格与次优方法的差异程度；两个模型独立验证；结果表格完整透明。
- **不足**：没有尝试较大规模的模型（如 LLaMA、GPT 等）、没有开放式的长文本生成场景；只评估了 2 个同级别的中等规模模型；训练子集较小（部分数据集只有 900~2000 条训练样本，训练步数少，可能影响模型本身的置信度行为）；参考质量分数的自动评估指标（BLEU/ROUGE/F1）在生成任务中本身有噪声，这一点在附录表 7 中有详细例证但并未在主实验中进行处理。
- **公平性担忧**：在部分任务上，baseline 的超参数属于固定默认值（如采样数固定 10 次），未说明针对模型是否进行了额外调优；而新方法的 k 在验证集上调节——这本身对基线存在轻微不利的因素，但也可被解释为新方法说明了验证集调参的使用方式。

## 6. 主要结论与发现

- **两种新方法整体优于已有基线**：在所有 16 组模型-数据集组合中，Tail 方法取得 10 组最佳、Ratio 方法 8 组最佳、DSM 4 组最佳；中位排名方面 Tail 为 2、Ratio 为 3，优于此前最佳 ATP（中位 4）。
- **翻译和 QA 上提升最显著**：BART 上 DE-EN 的 Tail 方法比次优基线相关系数提升 13.6 个百分点（0.648 vs 0.512），FLORES 提升 20.2 个百分点（0.649 vs 0.441）；但摘要任务提升较小，甚至在 CNN/XSUM 上比不过 ATP 基线。
- **Tail Thinness 比 Ratio 更稳定**：两者原理相近，但 Tail 方法在整体上略优于 Ratio 且更适合跨任务泛化。
- **k 的选取具有任务规律**：开放式任务（摘要、翻译）需要较大的 k（通常超过 95，甚至超过 100 而上限截断），cloze 式任务（QA、Reddit）最佳的 k 更小（1~4）；这说明 k 起到划分“好 vs 平均”序列群的作用。
- **定性分析验证了核心动机**：确实存在“多个答案均正确但 top-beam 概率被分散”的样本，本文方法对其给出高置信度，而 top-probability 类基线却给低分，直接证明了已有方法的缺陷。
- **失败案例分析**：模型在错误翻译时也可能过度自信（稀有词、误译关键词），以及自动评估指标的误判（重复文本高 ROUGE、不匹配的“gold”标签等）对置信度评估存在根本性干扰。

## 7. 优点

- **问题诊断准确且被实验证明**：现有方法过度依赖 top-sequence 概率，在生成任务中的确存在问题——这在 SQuAD 的定性示例中得到了直观展示。
- **方法简洁且任务无关**：无需训练额外模型、无需 NLI 分组、无需 verbalized confidence，只依赖解码时的概率输出；任意自回归模型即可使用。
- **填补了理论空白**：把统计学的“尾部薄度”概念引入了 NLP 置信度评估，对生成任务中“多有效序列”的独特形态有直接的理论匹配：
  - 分类任务 → 单点高置信度；
  - 生成任务 → 多峰但尾部薄、整体区分度高的形态。
- **实验覆盖多任务多语言**：翻译涉及 3 个方向（英德/英俄/英菲），摘要覆盖辩论、新闻、对话等子类型，覆盖面较多；
- **详细公开了实现细节**：训练步数、超参数 k、温度、数据切分、失败样本，并计划开源代码和模型权重，有利于复现和后继研究。

## 8. 不足与局限

- **计算成本增加**：需要生成 100 条 beam 来算 tail/ratio；对于开放式任务最佳 k 可能超过 100（论文明确提到"capped k at 100 due to computational limitations，可能低估了最优值"），这在长文本大模型生成中是大开销，无法用于低成本在线推理场景。
- **参数 k 需要调优**：方法对每个数据集要单独在验证集上调 k，且调出的最佳值差异很大，跨任务泛化使用需要新的调整，并不完全任务无关。
- **模型覆盖有限**：只在 BART Base 和 Flan-T5 Base 两个中等规模模型上实验，未验证大规模 API 模型或 decoder-only 架构的通用性。且它们都经过了 SFT，模型的分布行为可能与 instruct-tuned 或 RLHF 模型有很大差异。
- **模型自带的过度自信未能消除**：作者承认，模型本身在对错误翻译给出高概率时，他们的方法依然会“自信地犯错”；方法只改进"概率→质量"的映射关系，不会修补模型本身的内在缺陷。
- **没有给出真正意义上的校准指标**：主实验只有 Spearman 相关（排除了尺度信息），而 classification 中常用的 ECE 在连续评价指标上没有直接对应物，作者呼吁未来工作对此设立更好的评估方式。
- **数据集规模与代表性有限**：部分数据集只用了很小的训练子集（如 2000 条以内），FLORES 只用了一种语言对，SQuAD/HotpotQA 的结果在不同模型上的一致性不理想（如 BART 在 HotpotQA 上相关系数偏低，只有 ~0.255），这些都会限制结论的推广范围。
- **自动评估指标的噪声污染**：ROUGE/BLEU/F1 并非完美质量代理指标——附录中列出的重复文本高分、gold 摘要风格不匹配等案例，会导致部分置信度评估的"校准失败"其实根本是质量参考本身不可靠，论文给出了实例证明但并未提出解决方案。

（完）
