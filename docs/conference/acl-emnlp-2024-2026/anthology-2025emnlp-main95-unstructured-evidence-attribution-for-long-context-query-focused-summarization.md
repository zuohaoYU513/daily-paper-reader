---
title: Unstructured Evidence Attribution for Long Context Query Focused Summarization
title_zh: 长上下文查询聚焦摘要中的非结构化证据归因
authors: "Dustin Wright, Zain Muhammad Mujahid, Lu Wang, Isabelle Augenstein, David Jurgens"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.95.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 在长文档摘要中抽取任意长度的证据片段并回链到原文
tldr: 长上下文查询聚焦摘要通常只支持固定粒度的证据引用，如句子或段落，限制了证据的准确匹配。作者提出抽取任意长度的非结构化证据，以提升相关性和一致性，并构建SUnsET数据集。实验显示现有系统难以正确复制并引用非结构化证据，且这些证据易在长上下文中被丢失（lost in the middle）。该工作为需要生成内容并附原文证据的可信摘要系统提供了新基准和改进方向。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 768, \"height\": 725, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1341, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1356, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1309, \"height\": 801, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1339, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1607, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 984, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1622, \"height\": 896, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1601, \"height\": 1356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1627, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main95/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1627, \"height\": 531, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 702, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 764, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1634, \"height\": 1325, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1584, \"height\": 1332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1544, \"height\": 1319, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1365, \"height\": 1319, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main95/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 777, \"height\": 255, \"label\": \"Table\"}]"
motivation: 固定粒度证据引用限制了证据的灵活性，且长上下文证据容易在中间丢失。
method: 提出非结构化证据抽取任务，创建SUnsET数据集，评估大模型复制和引用任意长度证据的能力。
result: 现有系统难以稳妥引用非结构化证据，并受长上下文中间丢失影响。
conclusion: 需更强的复制和归因能力，以支持证据级可信的长文档摘要。
---

## Abstract
Large language models (LLMs) are capable of generating coherent summaries from very long contexts given a user query, and extracting and citing evidence spans helps improve the trustworthiness of these summaries. Whereas previous work has focused on evidence citation with fixed levels of granularity (e.g. sentence, paragraph, document, etc.), we propose to extract unstructured (i.e., spans of any length) evidence in order to acquire more relevant and consistent evidence than in the fixed granularity case. We show how existing systems struggle to copy and properly cite unstructured evidence, which also tends to be “lost-in-the-middle”. To help models perform this task, we create the Summaries with Unstructured Evidence Text dataset (SUnsET), a synthetic dataset generated using a novel pipeline, which can be used as training supervision for unstructured evidence summarization. We demonstrate across 5 LLMs and 4 datasets spanning human written, synthetic, single, and multi-document settings that LLMs adapted with SUnsET generate more relevant and factually consistent evidence with their summaries, extract evidence from more diverse locations in their context, and can generate more relevant and consistent summaries than baselines with no fine-tuning and fixed granularity evidence. We release SUnsET and our generation code to the public (https://github.com/dwright37/unstructured-evidence-sunset).

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与研究动机

- **任务背景**：长上下文查询聚焦摘要（LCQFS）要求模型在长篇或多篇文档中根据用户查询生成摘要，并对引用内容给出证据归因。
- **现有缺陷**：已有工作大多采用**固定粒度证据**（如整句、段落或全文档），难以精确支撑摘要中某句话；过长/过短都可能引入噪声或证据不足。
- **核心问题**：
  1. LLM 难以直接从上下文中**逐字复制并正确引用任意长度证据**；
  2. 即使能引用，证据也普遍“**lost-in-the-middle**”（位置处于上下文中部时更难被选中）；
  3. 缺乏可用于监督训练的“文档-查询-摘要-非结构化证据”数据。
- **整体含义**：作者主张用**任意长度的非结构化 span 作为证据**来提升摘要的可信度、相关性与事实一致性。

## 2. 方法论

### 2.1 核心思想
- 摘要句不再引用固定片段，而是显式附上一个**非结构化证据列表**；模型必须先复制证据文本，再在正文中用 `[n]` 标注对应关系。
- 利用合成数据微调模型，使其学会“精确定位—逐字抄写—一致性引用”的完整链路。

### 2.2 关键技术：SUnsET 六阶段归纳式生成流水线

| 阶段 | 作用 |
|---|---|
| P1 标题生成 | 生成多样且不重复的虚构/非虚构书名 |
| P2 大纲生成 | 为每本书生成含 6 个章节的写作大纲 |
| P3 查询+摘要+证据生成 | 每本书生成 5 组{question, summary, evidence}，每条证据分配到指定章节 |
| P4 逐章节文档生成 | 按顺序逐章编写内容，强制将证据原文包含进该章节；若未逐字嵌入则自动检索找回 |
| P5 精炼 | 基于最终完整文档重写总结和证据 |
| P6 验证 | 用模型判断总结是否完整回答查询、是否事实忠实，过滤低质量元组 |

- 结果数据：**2,352 篇文档**、**11,309 条 <doc, query, summary> 元组**。
- 多样性设计：用标题引导降低主题重复；对照非流水线（Non-Pipelined）与 Title+Doc 变体，SUnsET 在 TTR、语义余弦距离、主题多样性上均显著更优，且接近 SQuALITY、LexAbSumm 等人类书面数据集水平。

### 2.3 训练策略
- **LoRA 适配器**：rank=16、alpha=16，应用在全部线性层，不冻结/不修改位置编码。
- 两个变体：
  - `+ SUnsET`（位置保持）：按文档原章节顺序拼接后训练；
  - `+ Shuffled`（位置无关）：训练时随机打乱章节顺序（文档模块化特性支持），缓解位置偏差。

### 2.4 推理策略（长上下文分治）
- 文档超过模型最大长度时，按 chunk 切分，先生成各段带证据的局部摘要，再用组合提示，将这些局部摘要与证据清单汇总成最终总结。

## 3. 实验设计

### 3.1 Benchmark / 数据集
- **4 个测试集**：
  - SQuALITY（单文档、人类书写的科幻小说，~5.2k tokens）
  - LexAbSumm（单文档、人类书写的法律判决书，~14.4k tokens）
  - SummHay（多文档、合成新闻 “干草堆”，~93k tokens）
  - ScholarQABench（多文档、CS 学术论文，~16.3k tokens）

### 3.2 对比方法 / 模型
- 5 个底座：Llama 3.2 1B / 3.2 3B / 3.1 8B、Mistral Nemo 2407、Mixtral 8x7B。
- 四档对照：
  1. `Fixed Gran.`（固定粒度证据基线上限；OpenScholar 式 prompt）
  2. `Unstruct. Base`（不微调 + 非结构化证据 prompt）
  3. `+ SUnsET`（标准 SUnsET 微调）
  4. `+ Shuffled`（打乱章节的 SUnsET 微调）
- 另以 **GPT-4o-mini 无微调**作为性能上界参照。

### 3.3 评测方式
- **自动评测器（LLM-as-a-Judge）**：DeepSeek-V3，采用此前经人类相关性验证的 1–5 分提示词，从 Relevance 与 Consistency 两个维度评估；
- 证据复制成功率用最长公共子串（LCS）计算 exact match / 50% overlap；
- 证据质量：precision、recall、F1；
- 摘要质量：整段摘要相对原文档与查询的相关性与一致性。

## 4. 资源与算力

- 论文明确说明：训练与推理均在 **1–2 张 Nvidia A100（48 GB）** 上完成；
- 未报告总 GPU 小时、FLOPs 或能耗等详细计量；
- 超参范围曾做扫描（学习率、batch size、warmup、epochs、LoRA rank），最终选取值在正文/附录中标注。

## 5. 实验数量与充分性

- 主要矩阵规模可观：**5 个模型 × 4 个数据集 × 4 种方法**（外加 GPT-4o-mini），另有三个 RQ 分别给出表、图与统计置信区间（95% 非重叠 CI）。
- 证据复制率（表 3）、证据质量（图 5/6 及附录中的 precision/recall/F1 细表）、证据位置分布（图 7）、摘要质量（图 8/表 7）覆盖完整。
- 消融实验：
  - 训练样本数量对性能的影响（约 1k–3k 样本即可达到平台期）；
  - 标准 vs 打乱训练方式；
  - 自动评测结果鲁棒性检验（DeepSeek-V3 与 GPT-4o-mini 相关性 r=73.29）。
- 客观性评估：
  - 对 SUnsET 本身做了 **100 条元组 × 3 个问题**的双人独立人工测评，分数 2.90–2.99/3，准确一致率 93.67%；
  - 自动评测 prompt 此前经过人工相关性验证；
  - 不足：全文没有给出每次实验运行的具体随机种子/运行次数，质量评估主要采用自动打分器而非大规模人工判定。整体而言实验设计较充分且结论可信。

## 6. 主要结论与发现

- **证据复制困难**：未微调的模型（包括 GPT-4o-mini）逐字复制非结构化证据的成功率极低（Exact Match 最高仅 ~11%），而 SUnsET 微调后可大幅提升（如 Mistral Nemo 从 5.48%→82.20%）。
- **Lost-in-the-middle 普遍存在**：所有无微调模型的证据分布都偏向上下文两端；SUnsET 微调（尤其打乱训练）能使证据源位置更均匀，更接近参考摘要中的真实证据分布。
- **非结构化证据优于固定粒度**：平均引用质量（相关性与一致性）和 F1 均系统性提升；且训练后模型仍倾向于生成更精确的小段证据，而非整句拖带上噪声。
- **摘要质量同步提升**：学习非结构化证据可改善整段摘要的相关性与一致性，且摘要质量与引用质量中度正相关（Pearson r≈0.35）。
- **模型规模规律**：中等/大模型（8B 以上）收益显著；Llama 3.2 1B 此类过小模型即使微调也难以胜任该复杂任务。
- **效率/性价比**：SUnsET 合成数据成本约 200 美元，远低于人工标注同等规模数据估算的

人工标注同等规模数据的成本（作者估算约 4.8 万美元），说明合成数据路线在可控预算内具备可观的可扩展性。

## 7. 局限性与未来工作

- **语言与领域覆盖面有限**：SUnsET 以英语合成图书/新闻类文本为主；虽然实验覆盖小说、法律、新闻、学术论文四种下游测试集，但未验证小语种、对话/口语体、医疗/金融等高专业领域中的迁移效果。
- **评估依赖自动评测器**：核心结论多建立在 DeepSeek-V3 与 GPT-4o-mini 的自动打分上。尽管评测 prompt 经过人工相关性验证且两个打分器之间具有较高一致性，自动评测仍可能对“事实细节错误”“边缘案例”不敏感，真正的用户级判断需要更大规模的人工评测。
- **长上下文分治策略的损失**：超长多文档场景下采用“分段摘要→合并摘要”的分治方案，在中间过程中可能丢失跨文档的全局依赖信息；论文对此流程仅给出初步验证，未与直接全上下文处理进行系统对照。
- **证据生成与定位依赖指代消解**：合成阶段假定文档逐字包含证据，对现实中证据被改写、转述、跨句散布的情况建模不足，模型在真实世界噪声文本上的鲁棒性仍需检验。
- **可能存在的过度拟合风险**：LoRA 微调基于一种特定“标题—大纲—逐章生成”的强结构语料，是否会让模型过度偏好“先复制、后标注”的表层形式，而牺牲对隐式证据的抽象推理能力，尚未得到充分的消融验证。
- **未来方向**：作者建议引入多语言与多文档混合的合成数据；将证据抽取与忠实度校验做成显式反馈循环；利用推理时搜索策略进一步提升证据选择；并将评测维度扩展至 citation recall 之外的可信粒度与可读性。

## 8. 总结

本工作系统性地回答了一个此前未被重视的问题：面对长上下文和查询聚焦的摘要场景，模型能否生成并引用**任意长度、非结构化**的证据片段。论文在高价值数据稀缺时，用一套六阶段的归纳式合成流程（SUnsET）低成本地构造大规模训练语料，在 1B 到 8x7B 的不同底座上验证了“证据复制—证据选择—摘要生成”的端到端协同作用，同时揭示了固定粒度证据方案的相对局限及 lost-in-the-middle 偏差的普遍性。对于工程实现而言，其设计了一套可复现的 LoRA 微调与存储分治推理方案；对于研究层面而言，该文也在证据定位与摘要可信度之间建立了可量化的关联，为后续模型在 RAG、长文档摘要与引用归因等领域的发展提供了一个可靠的数据与训练范式的参考。

（完）
