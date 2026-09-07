---
title: Stress Testing Factual Consistency Metrics for Long-Document Summarization
title_zh: 面向长文档摘要的事实一致性指标压力测试
authors: "Zain Muhammad Mujahid, Dustin Wright, Isabelle Augenstein"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1472.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 在长文档摘要中压力测试多种无参考事实一致性指标，评估其检测无依据内容的可靠性
tldr: 长文档摘要的事实一致性评估仍是难题，既有指标多在短摘要设定下提出，受输入长度和长距离依赖限制。论文对六种常用无参考事实性指标施加七类保持事实性的扰动，包括改写、简化、同义替换、词汇压缩与源文本插入等，系统考察其长文档可靠性。结果显示各指标对扰动、检索上下文和主张信息密度表现出不同敏感度。该压力测试为选择和开发更稳健的长文档事实一致性指标提供了实证依据。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 731, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 926, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 1201, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1621, \"height\": 961, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1620, \"height\": 961, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1472/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1621, \"height\": 961, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1619, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1638, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1626, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1616, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1610, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1472/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1611, \"height\": 294, \"label\": \"Table\"}]"
motivation: 长文档场景下既有事实一致性指标可靠性未经验证，易受长度和远程依赖影响。
method: 设计七类保持事实性的扰动并应用于长文档摘要，对六种无参考事实性指标进行系统压力测试。
result: 揭示了不同指标在长文档、扰动、检索上下文和主张信息密度下的鲁棒性差异。
conclusion: 系统压力测试为长文档事实一致性评估提供了方法学参考，有助于改进既有评测指标。
---

## Abstract
Evaluating the factual consistency of abstractive text summarization remains a significant challenge, particularly for long documents, where conventional metrics struggle with input length limitations and long-range dependencies. In this work, we systematically evaluate the reliability of six widely used reference-free factuality metrics, originally proposed for short-form summarization, in the long-document setting. We probe metric robustness through seven factuality-preserving perturbations applied to summaries, namely paraphrasing, simplification, synonym replacement, logically equivalent negations, vocabulary reduction, compression, and source text insertion, and further analyze their sensitivity to retrieval context and claim information density. Across three long-form benchmark datasets spanning science fiction, legal, and scientific domains, our results reveal that existing short-form metrics produce inconsistent scores for semantically equivalent summaries and exhibit declining reliability for information-dense claims whose content is semantically similar to many parts of the source document. While expanding the retrieval context improves stability in some domains, no metric consistently maintains factual alignment under long-context conditions. Finally, our results highlight concrete directions for improving factuality evaluation, including multi-span reasoning, context-aware calibration, and training on meaning-preserving variations to enhance robustness in long-form summarization.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与研究动机
- **背景**：摘要生成模型（尤其是 LLM 驱动的抽象式摘要）虽生成流畅，但常引入幻觉内容，严重制约其在医疗、法律、科研等高敏感场景中的可信使用。
- **核心问题**：现有的事实一致性评测指标（ROUGE/BLEU 不适用；无参考指标多在短文档上设计）在**长文档摘要**场景下是否仍然可靠？
- **关键挑战**：
  - 长文档与多文档摘要中输入长度远超过指标上下文限制；
  - 信息分散，需跨段跨文档链接证据；
  - 长距离依赖和"lost in the middle"位置偏差；
  - 缺少参考摘要与人工标注，难以进行内在评估。
- **研究目标**：将已有的用于短文本的压力测试方法论系统化地迁移到长文档场景，揭示既有六种无参考事实性指标在长文档设置下的鲁棒性及失效模式。

### 2. 方法论框架

本工作延续 Ramprasad & Wallace (2024) 的压力测试思路，核心为"施加保持事实性的扰动 → 观测指标分数变化"，并结合检索式打分框架完成长文档事实一致性评估。

**2.1 七类保持事实性的扰动（P1–P7）**
- **改写（Paraphrased）**：以不同措辞和句法结构复述原摘要；
- **简化（Simplified）**：将复杂句拆写为清晰短句；
- **同义替换（Synonym Replaced）**：用近义词替换内容词，测试词汇不变性；
- **降低词汇多样性（Less Diverse）**：减少用词差异，探测是否隐含奖励文采；
- **逻辑等价否定（Negated）**：引入语义等价的双重否定/逻辑变换；
- **进一步压缩（Summarized）**：在保持事实基础上压缩摘要；
- **插入源文无关句（Added Source Text）**：从源文档插入与摘要主内容无关的真实句子。
- 所有扰动由 GPT-4o 生成（带专用提示词模板，严格禁止删信息/改语义）。

**2.2 检索式句子级评分框架（公式 1–2）**
- 设摘要句子集合 $S=\{s_1,\ldots,s_m\}$，源文档句子集合 $D=\{d_1,\ldots,d_n\}$；
- 对每个摘要句 $s_j$，用 SBERT 编码器计算与源句的余弦相似度，取出 top- $K$ 相似句子；
- 对每个检索句 $d_{j,k}$，扩展为以窗口 $w$ 包围的上下文片段 $d^{(w)}_{j,k}$；
- 得句子级分数为各上下文片段上指标得分的最大值：
$$\mathrm{score}(s_j)=\max_{k\in\{1,\dots,K\}} M(s_j,\,d^{(w)}_{j,k});$$
- 摘要级总分再取全句平均。

**2.3 主张信息密度的度量（公式 3–4）**
- 对每个摘要句（主张）计算其与全部源文档句子的平均余弦相似度：
$$\mathrm{Sim}(s_j,D)=\frac1n\sum_{i=1}^{n}\cos(e_j,e_{D_i});$$
- 按相似度分箱计算各箱子的平均事实性分数，用以刻画"信息越密集、证据越分散的主张是否更难评对"。

### 3. 实验设计
- **数据集与场景覆盖（三个长文档基准）**：
  - **SQuALITY**：科幻小说，专家撰写的叙事摘要（260 例）；
  - **LexAbSumm**：欧洲人权法院司法判决摘要（351 例，体裁高度结构化）；
  - **ScholarQABench**：计算机科学论文的多文档查询式摘要（100 例，证据跨文档重复）。其中 LexAbSumm 文档最长（~10,840 tokens）而 SQuALITY 摘要相对长。
- **对比的指标（六个无参考指标）**：BARTScore（生成式）、SummaC-Conv、SummaC-ZS（NLI/蕴含式）、AlignScore（统一对齐）、UniEval（多维度 QA）、MiniCheck（轻量级事实性分类器，具备 32k 上下文，可吃完整文档）。
- **实验矩阵与对照**：
  1. 七扰动 × 六指标 × 三数据集，对照原始摘要得分测量分数变化（图 2、表 4–6）；
  2. 检索窗口 $w=\{0,1,2\}$ 的影响（表 1）；
  3. 主张信息密度分箱 vs. 指标分数（图 3）；
  4. 附加每类扰动与原始摘要的 NLI 矛盾率校验（表 3），证明扰动总体保持事实性。

### 4. 资源与算力
- 文中仅在最终的 Model Size & Budget 处注明：**全部实验使用单张 NVIDIA H100 SXM5 80GB GPU 完成**。
- 未明确报告 GPU 数量、实验总时长、推理/评价耗时、Token 消耗量或能耗方面的细节。

### 5. 实验数量与充分性
- **覆盖面**：6 个指标 × 7 类扰动 × 3 个领域数据集，外加窗口尺度分析、信息密度关联分析和 NLI 校验，矩阵规模较大，兼顾了叙事、法律与科学多文档三类典型长文档场景，实验总体是系统的。
- **客观性**：
  - 指标均以公开发布版本原样使用，未做针对性调参，避免"自定义指标"的偏置；
  - 扰动统一由 GPT-4o 生成，并加 NLI 校验，确认大多数扰动保持了事实性。
- **不足与公平性隐患**：
  - 扰动自动生成，没有人工逐条确认（对 Negated 的全局事实保持无法保证）；
  - 未与人工事实性判断做相关性验证；
  - 只用检索式打分框架，未对比完整上下文（如 MiniCheck 32k）与分块对比等方法；
  - 未探索对指标做长文适配/微调是否能弥补缺陷。

### 6. 主要结论与发现
- 现有短文档事实指标在长文档摘要上**并不鲁棒**：
  - 许多指标对改写、简化、逻辑等价否定等无事实损害的改动给出不一致分数（图 2）；
  - AlignScore、SummaC-ZS 综合表现最不稳；BART 在 LexAbSumm 呈系统性负向偏移；UniEval 和 MiniCheck 相对稳定，但对 Negated 明显失败；
- **检索上下文窗口影响**：多数指标在增大窗口（w=0→2）时改善分数，特别在结构复杂的 LexAbSumm 上最明显；SummaC 系列对窗口变化不敏感，显示其仍依赖本土化蕴含信号；
- **信息密度相关**：对 LexAbSumm 与 SQuALITY，越"泛"且与文档多方重叠的主张得分越低，说明现有指标难以处理压缩性/分布式证据；相反，ScholarQABench 上高相似度主张反而得分更高，因为跨文档反复出现的表述提供了冗余证据；
- 没有任何指标能在长上下文条件下保持稳定的事实对齐。

### 7. 优点
- **问题真实且有针对性**：聚焦长文档评测缺失，填补了主流短文本压力测试的空缺；
- **方法设计严谨**：七类扰动覆盖面广且"保义"约束明确；借用检索式句子级打分框架，使得短文档指标能扩展至长文；
- **多域多指标交叉**：科学、法律、叙事＋六种不同范式指标，结论概括力强；
- **引入信息密度视角**：以主张-全文语义重叠度量"证据分散度"，有助于解释长文特有的失败模式；
- 公开了复现代码、扰动数据和 prompt 模板，具备较强可复现性。

### 8. 不足与局限
- **缺人工验证**：扰动由 GPT-4o 生成，缺乏人类标注确定是否完全保义；尤其 Negated 类矛盾率高，不能直接断定全局语义等价；
- **无人工评测对标**：未用长文档场景的人工事实性判断来校准指标得分；
- **领域与语言受限**：仅英语，仅科幻、法律、科学三域，未覆盖医疗、金融等高风险领域和低资源语言；
- **检索策略静态**：固定 top-K + 对称窗口，未对比更动态的证据选择或多阶段检索；
- **指标未训练/校准**：没有探索在长文数据上继续训练或做上下文感知校准后指标是否会改善；
- **无法对内文图 2、图 3 做精细手动复核**：由于本文以文本方式提供信息，未能对图内具体数据点进一步定量复核，分析依赖作者报告。

（完）
