---
title: "Cram Less to Fit More: Training Data Pruning Improves Memorization of Facts"
title_zh: 少填勤进：训练数据剪枝提升事实记忆
authors: "Jiayuan Ye, Vitaly Feldman, Kunal Talwar"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c3584de609a79c748934f89df95398212975870d.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 通过训练数据剪枝缓解容量超载，从而增强事实记忆并降低幻觉
tldr: 大模型在参数中记忆事实常受容量限制，过多或长尾分布的事实训练数据会使事实精度远低于容量上限并诱发幻觉。本文从信息论角度刻画事实记忆，并提出仅基于训练损失的剪枝方案，在控制事实总量同时拉平事实频率分布。实验表明该数据选择策略能提高模型事实准确率并减少幻觉，为如何整理大规模事实数据提供了可操作原则。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 训练数据中事实信息超过模型容量或分布不均衡是记忆失败与幻觉的重要原因，需要更优的数据选择。
method: 从信息论推导事实精度容量下界，设计基于训练损失的剪枝与频率平缓化算法以限制并均衡事实学习。
result: 在知识密集型任务的评测中，所提剪枝方案提升了事实准确性并显著降低幻觉。
conclusion: 数据层面的容量管理比简单堆叠更多语料更利于事实记忆，可作为预训练数据筛选的参考。
---

## Abstract
Large language models (LLMs) can struggle to memorize factual knowledge in their parameters, often leading to hallucinations and poor performance on knowledge-intensive tasks. In this paper, we formalize fact memorization from an information-theoretic perspective and study how training data distributions affect fact accuracy. We show that fact accuracy is suboptimal (below the capacity limit) whenever the amount of information contained in the training data facts exceeds model capacity. This is further exacerbated when the fact frequency distribution is skewed (e.g. a power law). 
    We propose data selection schemes based on the training loss alone that aim to limit the number of facts in the training data and flatten their frequency distribution. On semi-synthetic datasets containing high-entropy facts, our selection method effectively boosts fact accuracy to the capacity limit. When pretraining language models from scratch on an annotated Wikipedia corpus, our selection method enables a GPT2-Small model (110m parameters) to memorize 1.3X more entity facts compared to standard training, matching the performance of a 10X larger model (1.3B parameters) pretrained on the full dataset.

---

## 论文详细总结（自动生成）

好的，以下是基于提供的论文元数据与摘要内容生成的详细中文总结。

---

## 论文信息
- **标题**: Cram Less to Fit More: Training Data Pruning Improves Memorization of Facts（少填勤进：训练数据剪枝提升事实记忆）
- **作者**: Jiayuan Ye, Vitaly Feldman, Kunal Talwar
- **来源**: ICML-2026-Accepted（会议检索收录）
- **元数据标签**: query:faithfulness；Score: 8.0

## 1. 核心问题与研究动机
- **背景**: 大型语言模型（LLM）经常难以将事实性知识记忆在参数中，这会导致幻觉（hallucination）以及在知识密集型任务上表现不佳。
- **核心问题**: 训练数据中事实信息的**总量**与**分布形态**如何影响模型参数的记忆容量上限与实际事实精度。
- **研究动机**: 如果事实数据中包含的总信息量超过模型容量，或者事实出现频率呈现偏斜分布（如幂律分布），模型的实际事实精度会远低于理论容量上限，并诱发幻觉。作者因此提出：与其无限制地堆叠数据，不如对训练数据进行剪枝，以提升记忆效率。

## 2. 方法论：核心思想与算法框架
- **核心思想**:
  1. **信息论视角的形式化**: 将事实记忆建模为一个信息论问题，并推导出当训练数据所需存储的信息量（以 bits 计）超出模型参数容量时，事实精度无法达到容量上限的理论下界。
  2. **频率分布的重要性**: 事实在数据中出现的频率分布越不均衡（如长尾幂律分布），越会加剧容量超载导致的精度损失。
  3. **数据选择策略**: 提出以“限制事实总量”和“平缓化事实频率分布”为目标的数据剪枝方案。
- **关键技术细节**:
  - **基于训练损失的剪枝**: 不需要额外的语义标注或知识图谱，仅依据样本在训练过程中的损失值来判断是否保留。被模型“轻易学会”（低损失）的事实可以视为冗余，从而被剪掉，以节省容量。
  - **频率平缓化**: 通过数据选择减少高频事实的重复出现，使得不同事实的学习机会更加平均，避免长尾分布带来的记忆瓶颈。
- **算法流程（文字说明）**: 在训练过程中（或一个预扫描阶段）记录每个事实相关样本的训练损失 -> 基于损失阈值对事实样本进行排序和过滤 -> 构建一个事实总量受限、频率分布更均匀的高质量子集 -> 使用该子集对模型进行重新训练或继续训练。

## 3. 实验设计
- **数据集与场景**:
  1. **半合成数据集（Semi-synthetic datasets）**: 包含高熵事实，用于在可控条件下验证理论预测（事实精度能否被提升至容量极限）。
  2. **真实语料库（Annotated Wikipedia corpus）**: 从零开始预训练语言模型，评估在真实知识密集型语料上的事实记忆效果。
- **Benchmark**: 以模型记住的**实体事实（entity facts）数量**为主要衡量尺度。
- **对比方法**:
  - **标准训练（Standard training）**: 在完整数据集上进行常规预训练。
  - **不同模型规模对比**: 使用剪枝方案训练的 GPT2-Small（110M 参数）对比在完整数据集上训练的 10 倍大的模型（1.3B 参数）。

## 4. 资源与算力
- **明确提到的规模指标**: 模型参数量分别为 110M（GPT2-Small）和 1.3B。
- **GPU 型号/数量/训练时长**: **文中未明确说明**。摘要和元数据中仅透露了训练方式为“在标注的 Wikipedia 语料上从零开始预训练”，但未提供 GPU 硬件配置、总训练步数或能耗数据，因此无法评估其训练的绝对算力成本。

## 5. 实验数量与充分性
- **实验组数**:
  - 主要包含两组核心实验：半合成数据验证实验和真实 Wikipedia 预训练实验。
  - 在半合成实验中，通过理论下界与实测精度的对比来验证机制。
  - 在真实实验中，通过跨规模（110M vs 1.3B）对照体现方法的有效性。
- **充分性评估**:
  - **客观与公平性**: 采用了模型容量（1.3B 全量训练）作为强 baseline，这种对比是强有力的证明（即“以小博大”）。
  - **不足之处**: 以“多知”作为目标，可能导致评估偏向记忆型知识，缺乏问答（QA）或推理下游任务评测；此外，由于没有提供消融实验（如单独验证剪枝 vs. 频率平缓化的贡献），无法判断两种机制各自的作用比重。该方法在更多元的大规模数据（如 C4、The Pile）上的泛化能力尚不明确。

## 6. 主要结论与发现
- 当训练数据中的事实信息量超过模型容量时，减少事实数量（Cram Less）确实能够提升模型的记忆效果（Fit More）。
- 通过基于训练损失的剪枝方案，可以将事实精度提升至容量极限。
- **关键量化结果**：在使用剪枝方案训练时，GPT2-Small（110M 参数）相比标准训练能够记忆 **1.3 倍**更多的实体事实；且其记忆能力**匹配甚至超过**了在完整数据集上预训练的 10 倍规模模型（1.3B 参数）。

## 7. 优点与亮点
- **数据效率视角新颖**: 突破“数据越多越好”的传统观念，从信息论层面将数据容量与模型容量的高效匹配作为核心目标。
- **理论指导性强**: 给出了事实记忆的下界表达式（尽管隐藏在全文，但从摘要中可看出其提供了可验证的公式），使实验结论具有理论支撑。
- **训练损失作为唯一信号**: 仅利用训练损失进行剪枝，无需额外昂贵的人工标注或外部知识库，工程可落地性强。
- **结果极具冲击力**: 以 110M 参数实现 1.3B 模型的记忆水平，在深度学习“规模法则”盛行的背景下提出了一个新的实质性突破方向。

## 8. 不足与局限
- **算力信息缺失**: 未披露 GPU 类型和训练时长，不利于复现者评估实际成本。
- **评价维度单一**: 仅聚焦“实体事实记忆数量”，未验证该方法是否影响语言建模困惑度、推理能力或生成质量。
- **幻觉评估局限**: 虽然声称降低幻觉，但在实验设计中缺乏针对“幻觉生成”的直接 benchmark 评测（如 TruthfulQA），仅能通过记忆精度间接推断。
- **数据集适用性**: 主要实验基于 Wikipedia 实体信息，对于包含常识、程序代码或合成数据的预训练场景，该剪枝策略的有效性仍待考证。
- **信息论假设的理想化**: 将事实定义精确到“信息量”并进行压缩和剪枝，在真实世界中知识体量更大、语义更复杂，且容量测算可能难以精确计算。

---

（完）
