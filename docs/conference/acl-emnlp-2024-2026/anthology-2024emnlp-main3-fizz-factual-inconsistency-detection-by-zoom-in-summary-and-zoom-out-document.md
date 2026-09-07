---
title: "FIZZ: Factual Inconsistency Detection by Zoom-in Summary and Zoom-out Document"
title_zh: FIZZ：通过摘要聚焦与文档全局核对的事实不一致检测
authors: "Joonho Yang, Seunghyun Yoon, Byeongjeong Kim, Hwanhee Lee"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.3.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 基于细粒度原子事实分解并与原文对齐，检测抽象摘要中的事实不一致，可解释性强
tldr: 现有摘要事实一致性评测方法在精炼性和可解释性上有所不足。本文提出FIZZ，将摘要分解为细粒度原子事实，并在整个源文档范围内对这些原子事实进行对齐验证，从而定位不一致内容。该方法在检测性能和可解释性上均有改进，可为摘要系统的幻觉抑制提供更细腻的评测信号。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 631, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 414, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 606, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 799, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 800, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main3/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1610, \"height\": 488, \"label\": \"Table\"}]"
motivation: 抽象摘要评测方法多样但普遍缺乏精炼性与可解释性，难以定位细粒度事实错误。
method: 把摘要切成原子事实，再与源文档进行对齐，若源文档无法支持该原子事实则判定不一致。
result: 有效并具有可解释性地检测出摘要中的事实不一致，改进了既往方法。
conclusion: 原子事实分解加原文对齐是构建可解释摘要事实一致性检测的可行方向。
---

## Abstract
Through the advent of pre-trained language models, there have been notable advancements in abstractive summarization systems. Simultaneously, a considerable number of novel methods for evaluating factual consistency in abstractive summarization systems has been developed. But these evaluation approaches incorporate substantial limitations, especially on refinement and interpretability. In this work, we propose highly effective and interpretable factual inconsistency detection method FIZZ (Factual Inconsistency Detection by Zoom-in Summary and Zoom-out Document) for abstractive summarization systems that is based on fine-grained atomic facts decomposition. Moreover, we align atomic facts decomposed from the summary with the source document through adaptive granularity expansion. These atomic facts represent a more fine-grained unit of information, facilitating detailed understanding and interpretability of the summary’s factual inconsistency. Experimental results demonstrate that our proposed factual consistency checking system significantly outperforms existing systems. We release the code at https://github.com/plm3332/FIZZ.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义

- 研究背景：预训练语言模型使生成式摘要取得显著进步，但摘要系统常产生与源文档事实不一致的“幻觉”内容。
- 现有问题：
  - 已有事实一致性评测方法（如 NLI 句级比较、QA-based、parsing-based、LLM prompting）在准确性和可解释性上不足。
  - 句级评估粒度太粗，无法定位摘要中的细粒度错误；对代词和多句推理场景敏感，容易误判。
- 核心目标：提出一种更精细、可解释的事实不一致检测方法，帮助理解“摘要中哪一部分与原文矛盾”。
- 整体含义：论文提出的 FIZZ 方法通过**“先聚焦摘要（Zoom-in）分解原子事实，再扩展文档（Zoom-out）进行对齐验证”**，在 AGGRE FACT 基准上取得 SOTA 性能，并为摘要幻觉提供细粒度、可解释的检测信号。

## 2. 方法论

### 2.1 整体思想
- 将摘要分解为比句子更细粒度的“原子事实”（atomic facts）；
- 将每个原子事实与源文档句子进行 NLI 蕴含判断；
- 对需要多句推理的原子事实，自适应地扩大文档上下文粒度；
- 最终以最不支持的原子事实得分作为摘要整体分数。

### 2.2 关键流程（对应图 2）
1. **共指消解（Coreference Resolution）**
   - 同时对文档和摘要进行共指消解，将代词替换为实体名，避免 NLI 模型因代词与实体不一致而误判。
   - 形式化：`D′ = f_coref(D), S′ = f_coref(S)`。
   - 对于修饰语，采用“实体名 + 逗号 + 修饰语”的规则处理，保留关键信息。

2. **原子事实分解（Atomic Facts Decomposition）**
   - 对共指消解后的摘要逐句进行分解，使用 LLM（最终选用 Orca-2）配合 8-shot prompt 生成原子事实。
   - 原子事实定义为短小、精炼、平均包含 2~3 个实体，人称实体已消解的信息单元。
   - 过滤：用 NLI 模型检查生成的原子事实是否真正由摘要支持。以摘要句为前提、原子事实为假设，如果 `entailment` 概率不是最大值则删除该原子事实，避免 LLM 引入外部先验知识造成的噪声。

3. **原子事实评分（Atomic Facts Scoring）**
   - 将文档拆分为句子，将每个过滤后的原子事实作为假设、文档句子作为前提，计算 NLI 蕴含分数。
   - 对每个原子事实取与所有文档句子的最大蕴含分数作为该事实的得分：  
     `t_k = max_i e_{i,k}`
   - **自适应粒度扩展（Granularity Expansion）**：若该原子事实在给定句子维度下不是“最好被蕴含”（即最大分类不是 entailment），则从贡献最高分的文档句开始，逐步增加相邻上下文句子，最多使用 3~4 句作为前提重新计算蕴含分数，并取新分数与原分数中的最大值。  
     最终摘要分数为所有原子事实得分的最小值：  
     `FIZZ score = min(T*)`
   - 这样做可以应对抽象式摘要中“多句压缩为一句”的跨句推理需求。

## 3. 实验设计

### 3.1 数据集 / Benchmark
- 主实验使用 **AGGRE FACT** 基准，它聚合了 9 个主流摘要事实一致性检测数据集。
- 分为多个子集：`CNN / XSum`，各包含 `FTSOTA / EXFORMER / OLD` 等 split。
- 评估方式：二分类，根据验证集选择最佳阈值，报告 **balanced accuracy**，并在 FTSOTA split 上采用单阈值设置。

### 3.2 对比方法
- 基线覆盖：
  - NLI 类：SummaC-ZS、SummaC-Conv、AlignScore；
  - QA 类：QAFactEval、QuestEval；
  - 结构类：DAE；
  - 大模型 Prompt 类：ChatGPT-ZS、ChatGPT-CoT、ChatGPT-DA、ChatGPT-Star；
  - 原子事实类：FactScore、FacTool（将摘要分解后进行 QA 验证）；
  - 随机/人为基线等。

### 3.3 模型配置
- 共指消解：MT5 11B 模型 + 规则化代词替换。
- 原子事实生成：Orca-2（与多种 LLM 做对比）；
- 过滤与评分 NLI 模型：采用与 SummaC 相同的 ALBERT-xlarge-vitaminc-mnli，保证对比公平。
- 附加实验：尝试 DeBERTa、RoBERTa 作为 NLI 模型。

## 4. 资源与算力
- 论文**未给出 GPU 型号、卡数、训练时长等具体算力信息**。
- 仅从方法描述可以看出：
  - 共指消解使用了 11B 参数量的大模型 MT5，计算开销较大；
  - 原子事实分解用 7B/约 70 亿参数的 Orca-2 等 LLM；
  - NLI 预测需要逐句、逐原子事实进行多次推理，因此推理阶段较耗时。
- 作者在局限性中明确指出“方法相当耗时，实时性有待验证”，但未量化说明资源需求。

## 5. 实验数量与充分性
- 实验较为充分：
  - 主实验：在 AGGRE FACT-CNN 和 XSum 的多个 splits 上与大量基线对比；
  - FTSOTA split 的单阈值结果（表 1）与总体 AGGRE FACT 结果（表 2）；
  - 消融实验：去掉粒度扩展（w/o GE）、去掉过滤（w/o Filtering）、去掉原子事实层级（w/o AF）；
  - 额外分析实验：
    - 不同 LLM 生成原子事实的效果比较；
    - 在 RoSE 数据集上比较 LLM 原子事实与人工原子事实的质量（ROUGE-1、原子事实数量、token 长度）；
    - 不同粒度上限大小的影响；
    - 共指消解在文档/摘要两侧的效果分析；
    - 不同 NLI 模型的选择；
    - 不同句子分割器（NLTK vs Spacy）的影响；
    - 失败案例分析。
- 总体评估：实验较全面，有主客观对比，通过固定 NLI 模型与 SummaC 保持一致以提升公平性；但数据域仅限英文新闻/文章摘要，缺乏跨领域、多语言验证。

## 6. 主要结论与发现
- 提出的 FIZZ 在 AGGRE FACT 基准上平均性能达到 SOTA，特别是在 CNN 摘要上优势明显。
- 原子事实级分解比句级评估能更好地捕获细节事实错误，同时提供更高可解释性。
- 颗粒度扩展（Zoom-out）对需要跨句推理的 XSum 抽象摘要尤为重要，带来显著提升。
- 共指消解对于 NLI 模型准确判断蕴含关系非常关键，仅将代词换成实体名即可大幅提升分数。
- 在 LLM 原子事实生成方面，Orca-2 整体优于 GPT-3.5 系列和 Zephyr/Mistral；更短的原子事实 token 长度与更好性能相关，而 ROUGE-1 相似度不足以衡量分解质量，原子事实的数量和 token 长度也应考虑。
- 原子事实方法也有局限：某些语义上正确但分解后无法被文档直接支持的原子事实可能导致误判（如“tweet was about a rocket landing”）。

## 7. 优点
- 粒度更细：使用原子事实代替完整句子，可精确定位摘要中哪一小句、哪个信息片段与原文不一致，解释性强。
- 方法直观：通过核心消解 + 原子事实分解 + NLI 对齐 + 自适应粒度扩展，形成清晰的流水线。
- 自适应性：对只需单句验证的事实保持效率，对需要多句跨句推理的事实自动扩展文档粒度。
- 重视公平性：与 SummaC 使用同一 NLI 模型，能较好地隔离“原子事实层级”的贡献，而不是把模型差异当作方法提升。
- 分析到位：从多个角度剖析了影响性能的因素（共指、粒度、LLM 选择、原子事实长度等），提供了开源代码。

## 8. 不足与局限
- 计算开销大：共指消解和逐原子事实的 NLI 计算量明显高于部分现有指标，降低了大规模应用和实时评测的可行性。
- 评测域较窄：只在英语新闻/文章摘要上进行，未覆盖对话摘要、医学摘要等垂直领域。
- 语言单一：未验证其他语言的适用性，对多语种摘要评测的支持尚不明确。
- 过滤规则可能不完美：原子事实过滤依赖 NLI 对摘要本身的支持程度，可能滤掉一些间接蕴含但合理的表述，也可能保留异常事实；而“最小分”策略较敏感。
- 失败案例显示：原子事实分解可能将整句可验证的信息拆成过于孤立的碎片，导致正确摘要被错误判为不一致；虽然过滤减轻了部分影响，但并未完全消除。
- 阈值选择需依赖验证集，新场景下可能还需要重新调阈值。

（完）
