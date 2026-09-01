---
title: Attention-guided Self-reflection for Zero-shot Hallucination Detection in Large Language Models
title_zh: 注意力引导的自反思：大语言模型零样本幻觉检测
authors: "Qiang Liu, Xinlong Chen, Yue Ding, Bowen Song, Weiqiang Wang (王维强), Shu Wu, Liang Wang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1063.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用注意力贡献与自反思进行零样本幻觉检测
tldr: 大语言模型幻觉阻碍其有效应用，为此本文提出注意力引导的自反思（AGSER）零样本幻觉检测方法。该方法利用注意力贡献将输入查询分为注意力相关与不相关两类，分别通过模型生成回答并计算一致性分数，以二者差异作为幻觉估计。AGSER不仅有效检测幻觉，还显著降低计算复杂度，仅需三次模型调用。该工作为零样本场景下的幻觉检测提供了轻量高效方案。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1063/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 912, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1063/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1610, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1063/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1610, \"height\": 491, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1201, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1464, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1232, \"height\": 804, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 815, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 817, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 816, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 815, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 816, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 814, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 816, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 816, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 815, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 817, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 815, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 816, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 816, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 816, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 818, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 814, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 816, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 815, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 814, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 817, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 815, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 811, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 603, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 601, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 601, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 599, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 1589, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 1615, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 1512, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 1685, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 1554, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 1606, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 1684, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1063/table-040.webp\", \"caption\": \"\", \"page\": 0, \"index\": 40, \"width\": 1635, \"height\": 478, \"label\": \"Table\"}]"
motivation: 幻觉是大语言模型应用的主要障碍，现有零样本检测方法准确性有限且计算成本较高。
method: 提出AGSER方法，基于注意力贡献划分查询类别，分别生成回答并计算一致性分数，差异作为幻觉估计。
result: AGSER在有效检测幻觉的同时，显著降低计算复杂度，只需三次模型调用。
conclusion: 注意力引导的自反思为零样本幻觉检测提供了高效且经济的新方法。
---

## Abstract
Hallucination has emerged as a significant barrier to the effective application of Large Language Models (LLMs). In this work, we introduce a novel Attention-Guided SElf-Reflection (AGSER) approach for zero-shot hallucination detection in LLMs. The AGSER method utilizes attention contributions to categorize the input query into attentive and non-attentive queries. Each query is then processed separately through the LLMs, allowing us to compute consistency scores between the generated responses and the original answer. The difference between the two consistency scores serves as a hallucination estimator. In addition to its efficacy in detecting hallucinations, AGSER notably reduces computational complexity, requiring only three passes through the LLM and utilizing two sets of tokens. We have conducted extensive experiments with four widely-used LLMs across three different hallucination benchmarks, demonstrating that our approach significantly outperforms existing methods in zero-shot hallucination detection.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大语言模型（LLMs）在总结、机器翻译、智能体、信息检索等众多任务中表现出色，但容易生成过度自信且与事实不符的内容，即“幻觉”（Hallucination）现象，严重威胁模型的可信度，尤其限制了其在医疗、金融、法律等领域的应用。
- **核心问题**：如何准确且高效地进行**零样本幻觉检测**——即在不依赖目标模型特定标注样本的情况下，判断LLM生成的回答是否属于幻觉。
- **现有方法不足**：
  - 基于**答案一致性**的方法（如SelfCheckGPT、SAC³等）需要多次采样，计算开销大；当模型对错误答案极度自信时，多次采样结果可能依旧一致，导致漏检。
  - 基于**内部状态/注意力**的方法往往需要标注数据集训练分类器，泛化性不足。
  - 基于**外部工具/模型**的方法依赖额外资源。
- **整体含义**：本文提出一种轻量、零样本、仅基于模型自身注意力机制与自反思的幻觉检测方法，为提升LLM的可信度提供了一条高效路径。

## 2. 方法论（AGSER）

**核心思想**：受人类阅读理解时“重读关键内容进行反思”的启发，利用LLM在生成回答时的注意力贡献，将输入查询拆分为**注意力查询（attentive query）**与**非注意力查询（non-attentive query）**，分别输入LLM重新生成回答，根据新回答与原始答案的一致性差异来判断幻觉程度。

**关键技术细节**：

1. **注意力贡献计算**：对于输入查询 `X = {x1,...,xM}`，提取LLM自注意力层中所有头对最后一个 query token 的注意力权重之和，作为每个token的贡献分数 `s_i = a_{M,i}`（注意力来自最后查询token对第i个token）。
2. **注意力层选择**：文中比较了5种token贡献分数：
   - 第一层值 `s_first`
   - 中间层值 `s_mid`（第L/2层）
   - 最后一层值 `s_last`
   - 所有层最大值 `s_max`
   - 所有层均值 `s_mean`（实验最优，作为默认设置）。
3. **查询拆分**：
   - 注意力查询 `X_att` = 注意力贡献最高的前k个token（默认 k=2/3）；
   - 非注意力查询 `X_non_att` = 剩余token。
4. **自反思回答生成**：将 `X_att`、`X_non_att` 分别输入LLM，生成新的回答 `Y_att = f(X_att)`、`Y_non_att = f(X_non_att)`。
5. **一致性分数计算**：使用 Rouge-L 分别计算两个新回答与原始答案 `Y` 的一致性：`r_att = Rouge(Y_att, Y)`、`r_non_att = Rouge(Y_non_att, Y)`。
6. **最终幻觉估计**：`r = λ·r_att - r_non_att`（默认 λ=1.0）。**分数越低，表示幻觉越严重**。

**算法流程**：原始查询 → 获取原始答案并计算注意力贡献 → 按top-k拆分查询 → 分别生成两个新答案 → 计算两个Rouge-L一致性分数 → 按公式融合为最终幻觉指标。

## 3. 实验设计

- **数据集/基准（Benchmark）**：
  - **Books**（3000个样本）
  - **Movies**（3000个样本）
  - **Global Country Information（GCI）**（181个样本）
  - 三个数据集覆盖不同知识域，均为事实性知识回忆任务，答案正确性标注遵循InterrogateLLM论文的判定方式。
- **评估指标**：AUC（Area Under Curve）。
- **评估LLM**：4个主流开源模型——Llama2-7b、Llama2-13b、Llama3-8b、Qwen2.5-14b。
- **对比方法**：
  - SBERT（基于句子嵌入相似度的基线）
  - SelfCheckGPT（多次采样一致性）
  - INSIDE（嵌入空间一致性）
  - InterrogateLLM（反向问题验证，采用GPT-3+Llama2-7b+Llama2-13b集成的强力版本）
  - 内状态类方法因需要训练数据未纳入对比。

## 4. 资源与算力

- 论文在附录D中说明：**所有实验均使用NVIDIA A100 GPU（80GB内存）进行**，固定随机种子42，使用Spacy 2.3.9、transformers 4.30.2、rouge 1.0.1。
- **但是，关于GPU的具体数量、训练或推理的总时长等量化信息，论文未给出明确说明**，因此无法精确评估总体算力消耗，只能推断推理级别的工作量（无需训练、仅有多次前向传播）。

## 5. 实验数量与充分性

论文实验较丰富，主要包括：

- **主实验**：4个LLM × 3个数据集 = 12个评测组合，与4个基线方法对比。
- **消融实验1**：分别只用注意力查询、只用非注意力查询（在4个LLM × 3个数据集上都做了）。
- **消融实验2**：5种token贡献分数（s_first、s_mid、s_last、s_max、s_mean）的比较（同样覆盖4个LLM × 3个数据集）。
- **超参数研究**：k取2/5、1/2、2/3、3/4；λ取0.2～20的一系列取值，分别绘制AUC变化曲线。
- **附录扩展**：多个LLM在多个数据集上的一致性分数分布表（Tabs. 7-28）、更多层的消融实验（Tabs. 29-32）、运行示例（8个）和失败案例分析。

**充分性与客观性评价**：
- 实验覆盖面广，模型规模和数据集多样性较好；
- 消融实验设计明确，验证了各组件贡献；
- 但仍存在一些不足：未报告多次运行的方差/显著性检验，无法判断提升的统计显著性；超参数固定（k=2/3，λ=1.0）并未逐数据集调优，虽然作者说明了原因（避免过拟合），但最优性能可能被低估。

## 6. 主要结论与发现

1. **注意力贡献可以有效引导自反思**：对非幻觉样本，注意力查询重新生成的答案与原始答案高度一致；对幻觉样本，注意力查询可能导致答案改变。相反，非注意力查询在非幻觉样本上产生随机答案，但对部分幻觉样本可能保持原答案不变。
2. **AGSER在零样本幻觉检测上显著优于现有方法**：
   - 相比SelfCheckGPT平均提升10.4%~17.4%；
   - 相比INSIDE平均提升7.5%~15.2%；
   - 相比InterrogateLLM平均提升0.9%~6.7%。
3. **计算开销更低**：仅需3次LLM推理（原始查询、注意力查询、非注意力查询），token使用总量与原查询相同（注意力查询+非注意力查询=原查询），而对比方法普遍需要5次采样。
4. **注意力层选择很重要**：使用所有层的均值（`s_mean`）综合效果最佳，平均检测AUC为0.886；仅用第一层效果最差（0.794）。
5. **注意力查询起主要作用**：仅用注意力查询的AUC仍达0.84~0.97，但非注意力查询的补充可以轻微但稳定地进一步提升总体检测性能。

## 7. 优点

- **方法设计新颖**：将“人类重读关键信息进行反思”的认知过程引入幻觉检测，利用注意力贡献构造注意力/非注意力查询，思路独特且直观。
- **零样本通用性强**：不需要任何标注幻觉数据训练分类器，适用于不同LLM和不同数据集的即插即用场景。
- **计算效率高**：对比通用一致性方法（5次以上采样），AGSER只需3次推理且token不额外增加，效率明显占优。
- **实验系统全面**：覆盖4个LLM、3个领域数据集、多个基线、多样消融与超参数分析，验证较充分。
- **分析性验证扎实**：通过大量分布统计（Tables 1/2及附录B的Tabs 7-28）验证了注意力/非注意力一致性分数的判别性规律，支撑了方法的合理性。

## 8. 不足与局限

- **仅适用于可访问内部注意力的开源模型**：无法直接用于GPT-4、Claude等闭源API模型（作者已在Limitations中明确说明）。
- **仍需要3次推理调用**：虽然较已有方法效率提升明显，但实时或资源受限场景下仍有挑战。
- **查询拆分错误会带来误判**：附录I的坏例显示，注意力查询拆分可能丢失关键信息（如省略“作者是谁”或书名），导致非幻觉样本被误判；LLM对冷门信息（如出版年份）的固有记忆错误也可能导致幻觉样本反而高度一致。
- **评估域有限**：仅在知识回忆类任务（书籍/电影/国家信息）上验证，未覆盖开放性生成、多跳推理、对话等场景。
- **Rouge-L评定一致性存在偏差**：对同义改写或语义相同但字面不同的答案可能评分偏低。
- **缺乏统计显著性检验与多次运行方差报告**，结果稳健性说明不够充分。
- **超参数未逐场景调优**，实际应用中可能需要根据具体LLM/数据集做适配。

（完）
