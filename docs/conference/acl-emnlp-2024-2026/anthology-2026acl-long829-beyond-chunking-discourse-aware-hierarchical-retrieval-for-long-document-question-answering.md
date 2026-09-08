---
title: "Beyond Chunking: Discourse-Aware Hierarchical Retrieval for Long Document Question Answering"
title_zh: 超越分块：面向长文档问答的篇章感知分层检索
authors: "Huiyao Chen, Yi Yang, Yinghui Li, Meishan Zhang, Baotian Hu, Min Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.829.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 利用修辞结构树进行篇章感知的分层检索，解决长文档跨段信息获取
tldr: 长文档问答常将文档视为扁平序列或任意切块，忽视修辞结构对理解的作用。本文提出基于修辞结构理论（RST）的篇章感知分层检索框架，把长文解析成句子级表示，并用大模型增强篇章节点语义。通过结构引导的分层检索在多个长文档问答数据集上取得提升，展示了利用文档层级结构进行跨段证据定位的价值。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 735, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 297, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1634, \"height\": 1307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 791, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 214, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 801, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 791, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 793, \"height\": 556, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 758, \"height\": 747, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1639, \"height\": 977, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1645, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 488, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 765, \"height\": 713, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 769, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long829/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 793, \"height\": 160, \"label\": \"Table\"}]"
motivation: 长文档问答中扁平处理或启发式分块会破坏跨段语义，需要建模篇章层级结构。
method: 将RST篇章树转为句子级表示，结合LLM增强节点并进行结构引导的分层检索。
result: 在多个长文档问答数据集上验证了该方法相比常规分块检索的优越性。
conclusion: 结构化篇章建模能高效支持长文档中的跨段落信息检索与问答。
---

## Abstract
Existing long-document question answering systems typically process texts as flat sequences or use heuristic chunking, which overlook the discourse structures that naturally guide human comprehension. We present a discourse-aware hierarchical framework that leverages rhetorical structure theory (RST) for long document question answering. Our approach converts discourse trees into sentence-level representations and employs LLM-enhanced node representations to bridge structural and semantic information. The framework involves three key innovations: language-universal discourse parsing for lengthy documents, LLM-based enhancement of discourse relation nodes, and structure-guided hierarchical retrieval. Extensive experiments on four datasets demonstrate consistent improvements over existing approaches through the incorporation of discourse structure, across multiple genres and languages. Moreover, the proposed framework exhibits strong robustness across diverse document types and linguistic settings.

---

## 论文详细总结（自动生成）

# 论文详细总结

**《Beyond Chunking: Discourse-Aware Hierarchical Retrieval for Long Document Question Answering》**

> Huiyao Chen, Yi Yang, Yinghui Li, Meishan Zhang, Baotian Hu, Min Zhang
> 哈尔滨工业大学（深圳）等机构 | ACL 2026 (Long Papers)

---

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有长文档问答系统大多将文档视为扁平序列，或采用启发式的固定窗口分块策略。这类方法**忽略了文档本身固有的话语/篇章结构**（discourse structure），而这种结构恰恰是人类理解和组织文本信息的自然方式。
- **背景与差距**：
  - LLM 在短文档 QA（如 SQuAD，平均 117 词）上表现优秀（F1 > 85%），但在长文档任务（如 QASPER）上 F1 往往低于 50%。
  - 以往改进多为**语义聚类**（如 RAPTOR）或**二分法局部切分**（如 Bisection），前者依赖表层语义相似度，后者维持局部连贯，但都缺少语言学原则的指导。
- **核心假设**：修辞结构理论（RST）所定义的层级话语关系（对比、并列、阐述等），能够比语义相似度或任意边界更精准地刻画文档组织，从而引导检索系统和生成模型找到**跨段落的、语义连贯的证据**。

---

## 2. 论文提出的方法论

### 2.1 总体框架：DISRetrieval

三个核心阶段（对应三个关键创新）：

**(1) 话语感知树构建（Discourse-Aware Tree Construction）**

- **粒度适应**：传统 RST 处理到"基本话语单元（EDU）"级别，计算开销大且语义碎片化。本文将 RST 解析**提升到句子级别**，训练句子级解析器：将 EDU 级语料内部 EDUs 合并为句子单位，句子间关系通过原树中最低公共祖先分析获得。
- **语言适应**：用 GPT-4o 将 RST-DT 训练语料**翻译为中文**，保留句子级结构，与原语料合并训练统一的"语言通用"解析器 `fdiscourse`。
- **两阶段建树**：
  - Phase 1 — **段落级树构建**：对每段句子序列 Si 用解析器生成局部话语树 Ti。
  - Phase 2 — **文档级树构建**：对段落级树的内部节点做自底向上的 LLM 增强——当子节点合并长度超过阈值 τ 时用 LLM 生成摘要，否则直接拼接；段落根节点表示再输入解析器，形成层级结构，捕捉段落间话语关系。

**(2) 基于话语的节点表示（Discourse-Aware Node Representation）**

- 对文档级树的内部节点统一进行自底向上 LLM 增强，为每一个结构占位节点赋予"有意义的文本表示"，使其能参与向量空间语义匹配。
- 通过**替换式集成**将文档级树的叶子节点替换为对应的段落级话语树，形成"多层粒度并存"的单一话语树 TD。
- 使用预训练编码器对树中每个节点生成稠密向量：`ev = fenc(v)`。

**(3) 结构引导的分层证据检索（Structure-Guided Evidence Retrieval）**

- 对查询 q 编码后，与所有节点向量做余弦相似度，得到排序。
- 使用**双选择策略**：
  - 叶子节点相关度高 → 直接选择；
  - 内部节点相关度高 → 抽取子树中最相关的 top-k 个未使用叶子；
  - 冗余消除：已使用节点不再重复选入。
- 核心权衡：在"单句精确证据"与"话语连贯片段"之间取得平衡。

> 具体解析器采用基于转移系统（transition-based）的算法：stack/queue 配合 shift、reduce、pop-root 动作；节点表示由句向量或子节点向量均值计算，动作评分依赖堆栈中最近三个子树与队列首句的拼接表征。

---

## 3. 实验设计

### 3.1 数据集与评估指标

| 数据集 | 文档类型 | 平均长度 | 指标 |
|---|---|---|---|
| QASPER | 科研论文 | ~4,170 词 | F1-Match；检索：token级 F1/Recall |
| QuALITY | 小说/杂志（阅读理解） | ~5,022 词 | Accuracy |
| NarrativeQA | 图书/电影剧本 | ~51,372 词 | BLEU-1 / ROUGE / METEOR |
| MultiFieldQA-zh | 中文多领域文档 | ~6,701 词 | F1 |

### 3.2 对比基线

- **flatten-chunk**：固定 100 词切块；
- **flatten-sentence**：句子级切块直接检索；
- **RAPTOR**：递归语义聚类树；
- **Bisection（本文消融）**：与 DISRetrieval 共享节点增强与检索机制，仅将话语树替换为均衡二叉树——**隔离话语结构的贡献**。

### 3.3 实现细节

将收到的上下文长度统一为 200/300/400 词用于公平比较。测试两个嵌入模型：Sentence-BERT 与 OpenAI text-embedding-3-large，并使用三类不同的生成模型：UnifiedQA-3B、GPT-4.1-mini、Deepseek-v3。

---

## 4. 资源与算力

原文在正文中明确提到的硬件资源如下：
- 训练句子级话语解析器使用 **1 块 NVIDIA A100-40G**；
- 其余实验（解析、LLM 总结、节点嵌入、检索与生成）使用 **4 块 NVIDIA A800-80G**。
- 结论：论文**未明确给出总训练时间或总 GPU 小时数**，也未给出解析器具体收敛轮数与迭代耗时，只提供了推理阶段每篇文档的预处理复杂度（如 50K 词：约 103 秒）。不过作者单列了计算效率对比与消融，说明其将计算资源消耗作为核心考量之一。

---

## 5. 实验数量与充分性

### 实验覆盖很广，可以概括为多个维度：
1. **主实验**：覆盖四类评测任务（QA 生成 + 检索质量），加上 3 个生成模型 ×2 个嵌入模型 ×3 种上下文长度。
2. **多语言**：中文数据集验证跨语言能力。
3. **极端长文档**：NarrativeQA（平均 5 万+词，最长 34.7 万词）。
4. **六个专门研究问题（RQ1–RQ6）的深入剖析**：例如"更长文档是否更有利？"、"精确检索有多关键？"、"层级检索策略是否必要？"、"LLM 规模是否影响树构建质量？"、"解析器质量影响多大？"、"哪些因素真正导致性能差异？"
5. **大量消融实验**：K 值（1–20）、阈值 τ（0–400）、不同内部节点数 / 深度统计、不同节点增强 LLM（Llama-3.1-8B、Qwen2.5-7B、Mistral-7B、GPT-4o-mini、Deepseek-v3）、检索到的中间节点比例与深度分布等。
6. **计算效率对比**：DISRetrieval vs RAPTOR（10K–90K 词）耗时与加速比。

### 客观性与公平性考量
- 保证所有方法在相同上下文长度下对比，控制变量；
- Bisection 消融的设计尤其严谨——与 DISRetrieval 在节点表示与检索算法上完全一致，仅改变树构造方式，从而清晰分离"层级结构贡献"与"话语结构的独特增益"。

**整体评价**：实验规模充分、参数覆盖全面、跨语言与跨领域验证较完整，消融设计与对比基准逻辑清晰，证据链相当扎实。

---

## 6. 论文的主要结论与发现

- **话语感知方法在性能上全面优于基线方法**：在各种上下文长度、嵌入模型和生成模型设置下均取得一致提升。
  - 例如在 QASPER 中，400 词上下文 + UnifiedQA-3B，DISRetrieval 相比 flatten-sentence 提升 +2.66% F1-Match；相比 RAPTOR 提升显著。
- **话语结构优于纯语义聚类**：在公平对比下，RST 提供的组织编码比 RAPTOR 使用的嵌入聚类组织更具普适性和有效性。
- **层级结构本身优于扁平结构，但话语结构是"锦上添花"而非可替代品**：Bisection > flatten 说明层级组织有帮助；DISRetrieval > Bisection 证明话语组织是超过简单层级组织之外的必要增益。
- **精确证据集＞长上下文**：黄金证据（平均 129 词）F1 分数明显高于全文档输入。将检索所得证据并入完整文档后仍有提升（+0.73%~+1.39%），说明高质量检索对问答系统价值显著。
- **方法在多语言中泛化良好**：由英语新闻数据训练的解析器经数据增强后可迁移到中文文档，并在中文 QA 上持续领先基线。
- **话语解析器的质量直接影响下游表现**：解析器训练数据从 0%→100% 增加时，检索召回率和答案 F1 同步上升，说明框架的瓶颈在解析环节。
- **核心增益来源于树结构本身而非关系标签**：Top-20 检索节点与全文档间各类关系标签的分布几乎一致，表明关系类型不具检索判别力；真正促进效果的是由 RST 构建的自然分层分组。
- **推理效率优于 RAPTOR**：在 50K 词规模下，DISRetrieval 比 RAPTOR 快约 3 倍左右，且在自身节点增强阶段对 LLM 规模不敏感（使用 7B/8B 模型即可）。

---

## 7. 优点

- **用语言学理论支撑工程方案**：RST 的引入是系统性的（语法解析→跨语言→增强→检索），而非把话语关系当作文本特征做表面拼接，实现了真正"从结构和语义出发"的信号融合。
- **澄清机制而非只刷分**：专门设计 RQ6 + 关系分布分析，从实证角度说明"树结构优于类型标签"；在输出性能的同时提供了可解释性。
- **出色的消融设计**：将 Bisection 与 DISRetrieval 保持同构，只是替换"树的形成规则"，做到单变量归因，是分离因素贡献时非常干净的对照。
- **对计算成本有明确意识**：显式设计了"预处理一次、无限查询分摊"的机制，实际推理成本可接受，适合工业部署的环境。
- **跨语言和极端长度压力测试**：覆盖多来源文档，所有场景做严格等长度比较，验证稳健性和泛化边界。
- **开放与可复现**：附完整算法细节、提示词和参数选择依据，承诺发布代码与数据。

---

## 8. 不足与局限

- **解析器是相对瓶颈**：整个系统的效果受限于句子级 RST 解析器质量；由于训练语料 RST-DT 偏新闻语体，虽然已展示跨语体稳健性，但域差异仍可能限制在纯学术文献、法律、立法等多领域的峰值表现。
- **跨语言范围有限**：目前仅英文→中文，若要拓展到更多语言，还需要通过同类数据增强获取注释数据。其他语种（如日文、德文）没有长文档 QA 公开基准，因此多语验证尚不够广。
- **阈值 τ 策略简单**：虽是自适应的，但只有两个取值（0 和 50），动态阈值（基于语义复杂性或层级位置）可能改善更多场景。
- **评测方式本身有局限**：现有 QA 指标（F1/BLEU等）未必完全反映篇章感知检索的收益，比如篇章连贯性、多跳证据的合理组织等。
- **对场景的适用性边界明显**：在短文档 QA 或跨文档检索场景中，话语层级带来额外构造开销但相对增益有限——论文作者本人对此做了坦率说明，未给出针对这类弱结构问题的替代方案。
- **LLM 数据增强的偏见风险**：基于 GPT-4o 翻译训练语料，虽关注点集中在语言结构而非语义内容，降低了部分偏差风险，但翻译模型自身的偏见仍可能传入跨语言解析器。
- **缺少对测试集（而非验证集）的直接报道**：QuALITY 中因标签公开性原因使用了 dev 集而非测试集，这限制了个别数据集上的可比性。

---

（完）
