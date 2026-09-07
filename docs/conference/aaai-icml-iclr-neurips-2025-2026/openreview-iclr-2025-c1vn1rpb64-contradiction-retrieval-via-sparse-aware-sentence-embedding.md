---
title: Contradiction Retrieval Via Sparse-Aware Sentence Embedding
title_zh: 基于稀疏感知句嵌入的矛盾检索
authors: "Haike Xu, Zongyu Lin, Kai-Wei Chang, Yizhou Sun, Piotr Indyk"
date: 2024-09-27
pdf: "https://openreview.net/pdf?id=c1Vn1RpB64"
tags: ["query:faithfulness"]
score: 6.0
evidence: 基于稀疏感知的矛盾检索可获取与论断相反的证据，服务于事实核查，可辅助检测无依据事实内容
tldr: 现有方法难以在大规模语料中检索与论断相矛盾的文档，相似检索偏向语义相近内容，交叉编码器计算代价高。论文提出SparseCL，用稀疏感知句嵌入训练保留细微矛盾线索的向量表示，使矛盾检索高效且可扩展。实验表明其在矛盾检索、事实验证与数据清洗等下游任务上优于一般相似检索与稠密模型。该方法为验证生成结论是否缺乏支持提供了可用的矛盾证据检索工具。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 大规模语料中的矛盾检索对事实核查和数据清洗重要，但相似检索无法表达矛盾、交叉编码器计算成本高。
method: 提出SparseCL，通过稀疏感知训练句嵌入，使编码器保留并检索与查询语义相悖的细致矛盾内容。
result: 在大型语料上显著提升矛盾检索性能，并改善事实验证与数据清洗效果。
conclusion: 专用矛盾检索嵌入可有效支撑以证据为基础的事实一致性判断。
---

## Abstract
Contradiction retrieval refers to identifying and extracting documents that explicitly disagree with or refute the content of a query, which is important to many downstream applications like fact checking and data cleaning. To retrieve contradiction argument to the query from large document corpora, existing methods such as similarity search and crossencoder models exhibit significant limitations. The former struggles to capture the essence of contradiction due to its inherent nature of favoring similarity, while the latter suffers from computational inefficiency, especially when the size of corpora is large. To address these challenges, we introduce a novel approach: SparseCL that leverages specially trained sentence embeddings designed to preserve subtle, contradictory nuances between sentences. Our method utilizes a combined metric of cosine similarity and a sparsity function to efficiently identify and retrieve documents that contradict a given query. This approach dramatically enhances the speed of contradiction detection by reducing the need for exhaustive document comparisons to simple vector calculations. We validate our model using the Arguana dataset, a benchmark dataset specifically geared towards contradiction retrieval, as well as synthetic contradictions generated from the MSMARCO and HotpotQA datasets using GPT-4. Our experiments demonstrate the efficacy of our approach not only in contradiction retrieval with more than 30% accuracy improvements on MSMARCO and HotpotQA across different model architectures but also in applications such as cleaning corrupted corpora to restore high-quality QA retrieval. This paper outlines a promising direction for improving the accuracy and efficiency of contradiction retrieval in large-scale text corpora.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

**动机**

- 在大规模文档语料库中，检索与给定查询（Query）在语义上**相矛盾（Contradiction）**的文档，是事实核查、数据清洗等下游应用的关键能力。
- 现有方法存在明显缺陷：
  - **相似性检索（Similarity Search）**（如基于向量的稠密检索）从根本上偏向语义相近的内容，难以捕捉“语义相反但主题相关”的矛盾关系（如“主张 A 为真” vs. “主张 A 为假”）。
  - **交叉编码器（Cross-Encoder）** 能精细判断矛盾关系，但需要对每条候选文档与查询进行成对全量计算，在大规模语料库上计算开销不可承受。

**整体含义**

- 论文提出 **SparseCL（Sparse-Aware Contradiction Learning）**，训练专门的句嵌入模型，使“矛盾”这一细微的语义线索能被保留在向量表示中，从而将矛盾检索从昂贵的成对比较**降维到高效的向量运算**，在保持准确率的同时显著提高可扩展性。

---

### 2. 方法论：核心思想、关键技术细节与流程

**核心思想**

- 矛盾关系不仅体现在整体语义的相反，更体现在局部、稀疏的“关键差异线索”上（例如否定词、反义短语、数值改变、事实性对立的动词等）。
- 传统的稠密向量训练（如对比学习）倾向于拉近语义相近样本、推开不相似样本，但这种“全局语义”的约束往往会**磨平**那些局部但关键的矛盾线索。
- SparseCL 的思路是：在训练句嵌入时，显式地强化对这类**稀疏矛盾信号**的敏感性，使得编码器在推理时能通过简单的向量距离运算捕捉到“语义相近但立场相反”的对立内容。

**关键技术细节**

- 模型基于句子 Transformer 编码器（如 Sentence-BERT 架构），输出句向量。
- 训练阶段采用“矛盾对 + 相似对”联合构造的对比学习目标：
  - 相似对用于保持语义一致性；
  - 矛盾对用于学习在整体主题相似的前提下区分具体反对关系。
- 论文引入一种**稀疏函数（Sparsity Function）+ 余弦相似度的联合度量**：
  - 令查询向量为 \( q \)，候选文档向量为 \( d \)；
  - 检索得分 = \( \cos(q, d) + \lambda \cdot \text{Sparsity}(q, d) \)；
  - 该函数使与查询共享关键词/主题但存在关键反义线索的文档获得更高得分——即同时考虑向量之间的总体语义接近程度和“稀疏差异”模式。
- 整个检索流程为：先对语料离线编码成向量并存入索引，在线查询时仅需一次向量计算即可完成检索，无需逐对交叉验证。

**算法流程（文字描述）**

1. 输入：用大语言模型或已有数据集构造大量（查询，矛盾文档）和（查询，相似文档）训练样本；
2. 用这些样本训练一个句嵌入模型，损失函数同时包含相似项和矛盾项的对比约束；
3. 训练完成后，将目标语料库中所有文档编码为句向量；
4. 给定查询时，将其编码为句向量，计算其与语料中每个向量的组合得分（余弦相似度 + 稀疏惩罚项）；
5. 按得分为 Top-K 返回与查询相矛盾的文档。

---

### 3. 实验设计：数据集、Benchmark 与对比方法

**数据集**

- **Arguana**：论文使用的标准矛盾检索 Benchmark 数据集，源于学术互联网论坛上的反驳性讨论，专门用于评价矛盾检索模型。
- **MSMARCO**：从该数据集生成合成矛盾样本，作为训练和评测数据之一。
- **HotpotQA**：同样使用 GPT-4 生成合成矛盾样本进行评测和训练。

*注：MSMARCO 和 HotpotQA 的原始构造是 QA/检索类数据集，论文用 GPT-4 将原有相关文档改写成“对原始答案/事实进行反驳”的内容，以构造（查询，矛盾文档）对。*

**场景描述**

- 矛盾检索准确度评测（在 Arguana、MSMARCO 和 HotpotQA 上）。
- 数据清洗下游任务：从语料中剔除被污染（注入矛盾内容）的文档，恢复高质量的 QA 检索环境。

**对比基线方法**

- 一般的相似性检索模型（相似性检索，如稠密段落检索语言模型、Sentence-BERT 等多类架构作为底层编码器）。
- 交叉编码器模型（作为高精度基线）。

**评测方式**

- 将多个不同底层编码器替换为本文训练后的模型，测试其在矛盾检索上的命中精度，并与原始模块、交叉编码器做对比。
- 同时验证了方法在不同编码器架构上的泛化能力。

---

### 4. 资源与算力：文中未明确披露

- 论文正文中**没有明确报告 GPU 型号、数量、训练时长、batch size 等具体训练资源细节**。
- 无法据此评估训练成本，这是全文在可复现性/工程效能报告上的一个缺口。

---

### 5. 实验数量与充分性：整体充分但略有欠缺

**实验数量与维度**

- 在 **3 个数据集环境**（Arguana、MSMARCO 合成矛盾集、HotpotQA 合成矛盾集）上做了矛盾检索评测；
- 在**不同模型架构**下验证了方法（论文称“across different model architectures”），即同一个训练策略嵌套到多种基础编码器上的效果；
- 做了**下游应用实践**：从被污染的语料中清洗矛盾数据，以恢复 QA 检索质量；
- 但**未见到详尽的消融实验**（如逐项去除稀疏项、改变 \(\lambda\) 等对效果的贡献分析）、对失败案例的分析、以及对阈值/度量中稀疏函数具体形式的敏感度检验，未获取全部数据以作逐一核实。

**公平性与客观性判断**

- 数据集的交叉验证较为合理：在合成数据集上训练，在独立数据集（Arguana）上评测，能说明一定泛化能力。
- 但合成矛盾对由 GPT-4 生成，存在自身风格偏差；对矛盾的定义可能过于依赖 GPT-4，缺乏人类标注的真实矛盾语料的进一步验证。

---

### 6. 论文主要结论与发现

- **SparseCL 显著提升了矛盾检索的效率与准确性**：
  - 在 MSMARCO 和 HotpotQA 构造的矛盾检索任务上，相比常规相似性检索，在多种模型架构下带来**超过 30% 的准确率提升**；
  - 同时其推理过程只是向量计算，避免了交叉编码器的大量成对计算开销。
- 训练的嵌入具有较好的可迁移性：在别的数据集上进行测试，仍能保持比传统检索模型更优的矛盾检索能力。
- 将 SparseCL 嵌入用于清理被污染的语料，可以**恢复高质量 QA 的检索效果**，证明了方法能作为上游数据治理的有效工具。

---

### 7. 优点（亮点）

1. **问题聚焦且落地性强**：矛盾检索对事实核查和会话语料治理非常重要，方法直接着手解决该场景的低效问题。
2. **方向新颖**：从“稀疏感知”角度去思考矛盾的特殊结构——不是泛泛追求语义相反，而是识别“彼此围绕同一话题但存在犀利反证/反驳”的内容，相比一般对比学习思路更契合矛盾信号的本质。
3. **兼具架构通用性**：在多个预训练编码器上对接训练策略，结果表明模型平台无关，便于实际应用。
4. **系统化的效率思维**：在准确率和检索效率之间取得了好看的折中设计，利用向量化避免逐对精算，适合部署到大规模语料处理中。
5. **下游验证扎实**：不仅是在静态检索数据集上做评测，也通过真实下游数据清洗和 QA 检索的恢复情况来证明价值。

---

### 8. 不足与局限

1. **只依赖合成矛盾训练数据**：MSMARCO/HotpotQA 矛盾对经由 GPT-4 生成，与真实人类矛盾表达存在系统性差异，可能引入生成式偏差；且仅在 Arguana 一个真实基准上做了评判，“真实语义矛盾检索”的最终效果仍待更多人工标注数据的确认。
2. **算力与工程细节不透明**：没有给出训练开销（GPU 型号、训练耗时、显存需求、索引规模的具体膨胀比例等），对工业级部署的参考意义打了折扣。
3. **对故障模式讨论不足**：方法对明显的反例（例如应识别为矛盾却被判断为相似，或语义错误但被当作矛盾诱导的对抗性样本）没有展开细致的错误分析，模型鲁棒性证据有限。
4. **缺少对比公平性的细节报告**：对最强基线（交叉编码器）的精度上限对比、时间取舍、以及不同稀疏函数形式上的权衡，没有给出足够详细的数据表；需要核对摘要中 30% 这一数字的绝对口径/相对口径。
5. **局限在英语+单一句子级粒度**：两两矛盾关系有时是跨文档、跨句的逻辑推导（如长链演绎产生的矛盾），当前方法主要针对句子级或段落级编码；尚未讨论跨段落复杂推理场景。

---

### （完）
