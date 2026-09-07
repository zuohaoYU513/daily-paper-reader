---
title: Structured Discourse Representation for Factual Consistency Verification
title_zh: 面向事实一致性验证的结构化话语表示
authors: "Kun Zhang, Oana Balalau, Ioana Manolescu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.46.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 结合结构化话语表示与分类器的生成文本事实一致性验证方法
tldr: 检测生成文本是否忠实需要能系统比较文本间事件表示的语义结构。本文提出结合结构化话语信息抽取与分类器的事实一致性验证方法 FDSpotter，通过识别原子事实及其话语关系实现更深层语义比较。实验发现对抗性话语关系对语言模型构成挑战，但在 DiscInfer 标注数据上微调后可获得竞争力的性能。该方法有助于细粒度识别与源文档不一致的生成内容。
source: ACL-2025-Findings
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1642, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1644, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 809, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 800, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1658, \"height\": 791, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 784, \"height\": 502, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 824, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 663, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1650, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl46/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1651, \"height\": 679, \"label\": \"Table\"}]"
motivation: 要比较生成文本与源文本事件差异以判断幻觉，需要细粒度结构化语义表示及话语关系理解。
method: 提出 FDSpotter，将结构化话语信息抽取与一致性分类器结合，用标注数据 DiscInfer 微调增强判别。
result: 在提出的具有挑战性话语关系数据上，通过 DiscInfer 微调后达到有竞争力的事实一致性验证效果。
conclusion: 结构化话语表示能提升事实一致性验证的细致程度，是检测生成幻觉的有效工具。
---

## Abstract
Analysing the differences in how events are represented across texts, or verifying whether the language model generations hallucinate, requires the ability to systematically compare their content. To support such comparison, structured representation that captures fine-grained information plays a vital role.In particular, identifying distinct atomic facts and the discourse relations connecting them enables deeper semantic comparison. Our proposed approach combines structured discourse information extraction with a classifier, FDSpotter , for factual consistency verification. We show that adversarial discourse relations pose challenges for language models, but fine-tuning on our annotated data, DiscInfer , achieves competitive performance. Our proposed approach advances factual consistency verification by grounding in linguistic structure and decomposing it into interpretable components. We demonstrate the effectiveness of our method on the evaluation of two tasks: data-to-text generation and text summarisation. Our code and dataset will be publicly available on GitHub.

---

## 论文详细总结（自动生成）

# 面向事实一致性验证的结构化话语表示：论文总结

## 一、核心问题与整体含义（研究动机与背景）

- **核心问题**：如何系统性地比较两段文本在事件层面的表达差异，进而验证文本生成（如摘要、数据到文本生成）是否忠实于源文本，是否存在幻觉（hallucination）。
- **研究动机**：
  - 现有基于 RDF 三元组（subject-predicate-object）的表示方法存在语义不完整问题，例如难以编码状语（adverbials）中的时间、地点、方式等信息，也无法表达因果、对比等话语层面语义。
  - 大规模语言模型和小型分类器常无法检测由对抗性话语连接词（adversarial discourse connectives，如将 "but" 替换为 "so"）引入的矛盾。
- **整体思路**：通过引入更丰富、更细粒度的结构化表示——将状语和补语纳入原子事实（atomic facts），并显式建模原子事实之间的话语关系（discourse relations）——来提升跨文本事实一致性验证的效果，使验证过程更具可解释性和语言学依据。

## 二、方法论

### 2.1 结构化信息表示
- **原子事实（Atomic Fact）表示**：每个原子事实（对应一个英语小句）被结构化为六元组：`⟨subject, predicate, direct object, indirect object, short adverbial, short complement⟩`。相比 RDF 三元组，额外包含短状语和短补语，以承载更完整的信息。
  - 若某个元素内部嵌套另一个事实（如非限定动词、关系从句、同位语），则将其拆分为独立的原子事实。
- **话语关系（Discourse Relation）表示**：每个话语关系形式化为 `⟨fact1, connective, fact2⟩`，涵盖 PDTB 中三类话语关系及其子类：时间（temporal：precedence/succession/synchronous）、比较（comparison：concession/contrast/similarity）、因果（contingency：reason/result/condition/negative condition）。文本中未包含的重要信息，如启发性关系，不纳入建模范围。

  - **不包含 expansion 类连接词**（如 and、for example、in summary 等），理由是其存在不改变文本的关键信息，在比较时可忽略。
- **抽取实现**：由于传统话语连接词检测仍有挑战，本文使用 **few-shot prompting** 的 LLM（GPT-4-Turbo、GPT4o、Llama3.1 8B / 70B）联合抽取原子事实和话语关系。

### 2.2 事实包含（Factual Inclusion）与事实重叠（Factual Overlap）评分
- **内在置信度（Intrinsic Confidence）**：训练一个分类器 FD，估计某个原子事实 Aᵢ 或话语关系 Dⱼ 是否被文本 T 表达，即 C(Aᵢ|T)、C(Dⱼ|T)。该置信度用于过滤抽取中可能的幻觉，也用于候选选择。
- **外在置信度（Extrinsic Confidence）**：验证文本 T₁ 中的原子事实/话语关系是否在另一文本 T₂ 中被表达，即 C(Aⁱ₁|T₂)、C(Dʲ₁|T₂) 等。
- **计算公式**：
  - 过滤函数 δ_θ(x)（阈值 θ=0.5），只保留内在置信度足够高的内容单元参与评分；
  - **FI_A(T₁⊂T₂)** 和 **FI_D(T₁⊂T₂)** 分别为 T₁ 的原子事实和话语关系被 T₂ 覆盖的加权和；
  - **FI（Factual Inclusion）**：归一化后的单向包含得分；
  - **FO（Factual Overlap）**：对称的双向得分，综合 FI(T₁⊂T₂) 与 FI(T₂⊂T₁)。

### 2.3 FDSpotter 分类器
- **架构**：基于 304M 参数的 DeBERTa V3 Large，预训练于 tasksource 数据集。
- **训练数据**：
  1. 从 FactSpotter 方法衍生的合成原子事实蕴涵数据（以 WebNLG 为基础）；
  2. 从文本蕴涵数据（NLI：SNLI、MNLI、FEVER、ANLI、LingNLI、WANLI、CNC）中，使用 spaCy 抽取结构化的原子事实作为假设；
  3. **DiscInfer 数据集**：从 NLI 数据中筛选含话语连接词的样本，将其中的一个连接词替换为可能使假设与前提矛盾的对抗性连接词（如 "if" 替换为 "unless"），再经人工验证标签，共 920 条标注样本，用于训练和测试对抗性话语关系推理。

## 三、实验设计

### 3.1 数据集与基准
- **话语/原子事实抽取质量评估**：50 条 Causal News Corpus 样本，由两位人工标注者提供黄金标注，使用 Hungarian 算法进行匹配，并采用 4 种指标（Strict match、LCS ratio、SBERT element、SBERT full）评估。
- **DiscInfer 测试**：评估 DeBERTa（有无 DiscInfer 微调）与 GPT-4 zero-shot 在话语关系蕴涵测试集上的准确率。
- **数据到文本生成**：WebNLG 2020 基准，16 个系统参与，人类评判数据覆盖率、正确性、相关性等维度。
- **文本摘要评测**：
  - **SummEval**：23 个摘要系统，评判一致性维度。
  - **AggreFact**（FTSOTA / EXFORMER / OLD 子集）：二分类事实性标签，报告平衡准确率。
  - **DiverSumm**：涵盖 ChemSumm、QMSUM、ArXiv、GovReport、MultiNews 五个领域的更长文档摘要忠实度分类，以 ROC-AUC 评估。

### 3.2 对比方法
- **传统指标**：BLEU、METEOR、BERTScore、BARTScore、BLEURT。
- **先进事实一致性方法**：FactSpotter、DAE、QuestEval、SummaC（ZS/Conv）、QAFactEval、TrueTeacher、MENLI、AlignScore、FENICE、ChatGPT-ZS / COT / DA / Star、G-EVAL-4、INFUSE、FullDoc、SentLI 等。

## 四、资源与算力

- 论文仅提及使用 **NVIDIA Tesla V100** 对 DeBERTa 进行微调，学习率 1e-5、batch size 16、AdamW 优化器、训练 3 个 epoch。
- 未明确说明 GPU 的具体数量、总训练时长或额外算力消耗（其中包括 LLM 推理的开销）。
- 代码和数据集声称将开源，但文中未给出具体链接。

## 五、实验数量与充分性分析

### 实验数量
- **抽取质量实验**：覆盖原子事实和话语关系，在 4 种匹配度量下的多模型（GPT-4-Turbo、GPT4o、Llama3.1 8B/70B）和多温度参数评估，结果较为全面。
- **DiscInfer 训练集测试集消融**：有/无 DiscInfer 微调的对比，并评估 GPT-4 zero-shot。
- **三个主要任务**：WebNLG（文本级与系统级相关性）、SummEval（系统级与样本级相关性）、AggreFact（三个分割）和 DiverSumm（五个领域）——总体实验场景丰富。
- **消融与敏感性等**：包括不同抽取格式（SPO 三元组 vs 原子事实 vs 原子事实+话语关系）、DiscInfer 的影响、温度参数对抽取的影响等，消融较充分。

### 充分性与客观性评估
- **优点部分**：覆盖多种评估任务类型，与大量 SOTA 方法对比，既报告相关性也报告分类准确率。广泛采用 95% 置信区间及多种相关系数，统计严谨。
- **局限性部分**：
  - 在 DiverSumm 的 MultiNews 领域上，FactInclusion（44.88）明显差于 INFUSE（53.16）等基线，虽然平均值最高，但对部分领域泛化有风险；
  - 温度/模型稳定性不足（Llama3.1 8B 在某些温度下召回率显著波动），对参数较敏感；
  - 部分基准对比从原文看已选定与测试有关的基线（如 DAE 在 AggreFact 中排除训练覆盖的分割），但整体方法是透明的；
  - 人类标注者数量及标注者间一致性并未得到系统的深入报告。

## 六、主要结论与发现

- **抽取质量**：GPT-4 系列抽取质量最高，Llama3.1 8B 在话语关系抽取上精度高但召回率低（原子事实抽取表现较弱），Llama3.1 70B 在两者间折中。
- **话语关系识别的困难**：在没有 DiscInfer 微调时，DeBERTa 对对抗性话语关系准确率很低（如 contrast 仅 23.1）；加入 DiscInfer 微调后大幅提升（如 contrast 达 84.3，comp. 达 59.6），甚至超过 GPT-4 zero-shot。
- **对事实一致性验证的改善**：在 WebNLG、SummEval、AggreFact（FTSOTA/CNN-DM、XSUM 平均）上，FactInclusion/FactOverlap 与人工评判的相关性均达到或接近第一名；在 DiverSumm 长文档摘要上，平均 ROC-AUC（65.20）明显优于所有基线。
- **结构性消融**：相比仅用 SPO 三元组（65.4 / 69.6），只加“原子事实”可提升（66.4 / 72.4），再加话语关系进一步提升（69.6 / 73.8，AggreFact CNN-DM / XSUM），验证了原子事实与话语关系各自的重要性。
- **DiscInfer 数据集的贡献**：含有对抗性话语连接词的人工标注数据，能显著提升模型对错误连接词引起的逻辑矛盾的判别能力。

## 七、优点

- **语言学动机清晰**：将话语关系引入事实一致性验证，在摘要和数据到文本任务中是较新的方向，契合自然语言的丰富性和深层语义。
- **结构化、可解释性好**：通过原子事实+话语关系的分解，使事实验证结果可以追查“哪些事实未得到支持，或哪些关系被改变”。
- **实验覆盖面广**：涵盖两代评测基准、判别数据集和长文档摘要基准，与大量 SOTA 方法进行了系统比较。
- **构造了新的挑战数据集 DiscInfer**：聚焦对抗性话语连接词这一实际问题，并通过人工验证确保标注质量。
- **实践应用灵活**：定义 FI 和 FO 两个指标，分别适用于单向（摘要）和对称（数据到文本）事实一致性验证场景。

## 八、不足与局限

- **多语言缺失**：目前仅限英语，结构化表示基于英语句法，尚未验证在其他语言中的推广能力。
- **“蕴涵”与“严格事实包含”之间存在概念差距**：NLI 数据中假设可以基于常识或隐含推理成立，但严格“事实包含”需要显式地出现在前提中，会造成一定程度的误判风险。
- **依赖 LLM 抽取结构**：抽取中或引入噪声，尽管通过内在置信度阈值部分地缓解了此问题，但结构抽取的不确定性依然影响下游分类。
- **泛化与鲁棒性有限**：部分结果位于多数据集中明显低于基线，整体上缺乏错误分析的细节和对 Sensitive 参数的讨论（如对阈值和温度等参数的敏感性实验）。
- **资源信息不透明**：未报告模型总体计算成本、GPU 数量、总训练时间；对比模型间推理成本差异容易影响实际可复制性。
- **过于依赖新型人工测试数据**：DiscInfer 的规模较小（920 条），且对抗性替换方式是在特定连接词对上进行，覆盖全部语义组合的潜力有限。

（完）
