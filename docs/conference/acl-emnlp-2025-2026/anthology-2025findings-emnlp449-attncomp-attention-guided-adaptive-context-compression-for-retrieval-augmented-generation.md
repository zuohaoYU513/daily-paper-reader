---
title: "AttnComp: Attention-Guided Adaptive Context Compression for Retrieval-Augmented Generation"
title_zh: AttnComp：注意力引导的自适应上下文压缩用于检索增强生成
authors: "Lvzhou Luo, Yixuan Cao, Ping Luo"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.449.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 注意力引导的上下文压缩通过过滤不相关内容提升RAG的事实准确性
tldr: 检索增强生成虽能提升事实准确性，但检索内容中的无关信息会损害效果。本文提出AttnComp框架，利用LLM注意力机制识别相关信息，通过Top-P压缩算法自适应调整压缩率，保持低延迟并整合多文档信息。实验表明该方法能在过滤无关上下文的同时提高RAG的生成质量与准确性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1604, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 782, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1624, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1606, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1608, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp449/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1610, \"height\": 605, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp449/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1650, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp449/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 701, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp449/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 716, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp449/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp449/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1592, \"height\": 2404, \"label\": \"Table\"}]"
motivation: RAG检索到的无关内容会阻碍生成效果，现有压缩方法难以自适应和低延迟。
method: 基于LLM注意力识别相关信息，用Top-P算法进行自适应上下文压缩。
result: 实验显示AttnComp在提高压缩效率的同时增强了RAG的事实准确性。
conclusion: 为RAG提供了一种高效且上下文感知的压缩方案。
---

## Abstract
Retrieval-augmented generation improves the factual accuracy of Large Language Models (LLMs) by incorporating external context, but often suffers from irrelevant retrieved content that hinders effectiveness. Context compression addresses this issue by filtering out irrelevant information from context before LLM generation. However, existing methods struggle to adaptively adjust compression rates for different context, maintain low latency and integrate information across multiple documents. To overcome these limitations, We introduce AttnComp, an adaptive, efficient and context-aware compression framework. By leveraging the attention mechanism of LLMs to identify relevant information, AttnComp employs a Top-P compression algorithm to retain the minimal set of documents whose cumulative attention weights exceeds a predefined threshold. In addition to compression, AttnComp estimates response confidence by assessing the overall relevance of the retrieved content, enabling users to gauge response reliability. Experiments demonstrate that AttnComp outperforms existing compression methods and uncompressed baselines, achieving higher accuracy with substantial compression rates and lower latency.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：检索增强生成（RAG）通过引入外部知识来提升大语言模型（LLM）的事实准确性，但在实际应用中，检索到的文档往往包含大量与查询无关的噪声信息。
- **核心问题**：现有上下文压缩方法存在三大局限：
  - **缺乏自适应性**：多依赖固定压缩率或目标长度（如 RECOMP-ext、LongLLMLingua），忽略了不同上下文中相关信息比例的差异，易导致欠压缩或过压缩。
  - **效率不足**：抽象式压缩方法（如 CompAct）依赖 token-by-token 的自回归解码，训练和推理延迟高，难以满足实时应用需求。
  - **缺乏上下文整合能力**：多数抽取式方法仅评估单个句子或文档与查询的相关性，无法整合跨文档的语义依赖信息，难以应对多跳 QA 等复杂任务。
- **文章主张**：一个理想的压缩方法应同时具备三点特性——**自适应**（Adaptive）、**高效**（Efficient）和**上下文感知**（Context-Aware），而已有方法均无法同时满足。

### 2. 论文提出的方法论：核心思想、关键技术细节与算法流程

AttnComp 是一种基于注意力引导的自适应抽取式上下文压缩框架，整体流程包含两个阶段：

**阶段一：注意力计算（Attention Computation）**

- 复用 LLM 前 L 层（默认 L=13）的 transformer 层来编码上下文和查询，并增加一个交叉注意力层。
- 交叉注意力层计算查询 token 对上下文各 token 的注意力权重，公式如下：

  \[
  Q_i = X_q \cdot W^Q_i, \quad K_i = X_c \cdot W^K_i
  \]
  \[
  A = \frac{1}{H} \sum_{i=1}^{H} \text{softmax}\left(\frac{Q_i K_i^T}{\sqrt{d_a}}\right)
  \]

- 基于此得到指令（instruction）和每个文档的注意力得分，公式为：

  \[
  s = \frac{1}{|I_q|} \sum_{i \in I_q} \sum_{j \in I_d} a_{ij}
  \]

**阶段二：Top-P 压缩算法（Top-P Compression）**

- 将指令得分 `s_ins` 作为初始累积值，文档按得分降序排列，依次累加文档得分，直到累积值达到阈值 p（默认 0.95）或当前文档得分低于最小阈值 ε（默认 10⁻²）为止。
- 该策略天然具备**自适应性**：相关信息分散时需保留更多文档；相关信息集中时保留少量文档；全部文档无关时则全部滤除。
- 伪代码见论文 Algorithm 1。

**注意力微调（Attention Fine-Tuning）**

- 交叉注意力层初始化为第 L+1 层的 top-16 注意力头，冻结前 L 层，仅微调交叉注意力层（约 0.5% 参数）。
- 构造训练数据的自动化标注管线（Algorithm 2）：通过多轮不同排列的 Top-P 压缩取交集标注相关文档，再通过 LLM 生成答案进行验证，同时构造全文档无关的负例。
- 训练目标包含**文档级监督**（二元交叉熵）和**指令级监督**：

  \[
  \mathcal{L}_{doc} = -\sum_{i=1}^{k} [r_i \log s_{d_i} + (1-r_i)\log(1-s_{d_i})]
  \]
  \[
  \mathcal{L}_{ins} = -\left[ r_{ins} \log s_{ins} + (1-r_{ins})\log(1-s_{ins}) \right]
  \]
  \[
  \mathcal{L} = \mathcal{L}_{doc} + \lambda \mathcal{L}_{ins}, \quad \lambda = 0.8
  \]

**置信度估计（Confidence Estimation）**

- 模型微调后，指令注意力得分 `s_ins` 与检索内容整体相关性呈负相关。定义置信度：

  \[
  \text{confidence} = 1 - s_{ins}
  \]

- 置信度分数可作为 RAG 回答可靠性的指标，并可能用于未来的迭代式 RAG 研究。

### 3. 实验设计：数据集、基准与对比方法

- **单跳 QA 数据集**：Natural Questions（NQ）、PopQA。
- **多跳 QA 数据集**：HotpotQA、2WikiMultiHopQA、MuSiQue。
- **检索语料**：2018 年 12 月的 Wikipedia dump，截断为每 100 词的文档；每个查询检索 top-100 文档，检索器为 E5-base-v2。
- **对比方法**：
  - 无检索基线（No Retrieval）；
  - 未压缩的 RAG 基线（All Documents、Top 5、Top 10）；
  - 压缩方法：RECOMP-ext、LongLLMLingua、CompAct、Provence、以及 AttnComp 的无微调版本。
- **读者模型**：Llama-3.1-8B-Instruct（主实验），另以 Qwen2.5-7B-Instruct-1M 进行补充验证。
- **评估指标**：压缩率（Comp.）、F1 分数、准确率（Acc）。

### 4. 资源与算力

- **训练**：使用 4 张 NVIDIA RTX 4090 GPU（24GB 每张），训练时长约 4 小时，微调约 0.5% 的参数（仅交叉注意力层）。
- **推理**：压缩阶段使用 1 张 RTX 4090，生成阶段使用 2 张 RTX 4090（论文在效率分析部分明确了硬件配置）。
- **骨干模型**：Llama-3.1-8B-Instruct。

### 5. 实验数量与充分性

论文开展了多组系统实验，整体较为充分：

- **主实验**：5 个 QA 数据集上的全面对比，包含 F1、准确率和压缩率三项指标。
- **效率分析**：端到端延迟对比（压缩时长 + 生成时长）。
- **自适应性分析**：保留文档数的分布统计（HotpotQA vs PopQA）。
- **鲁棒性分析**：
  - 不同检索文档数量（k = 5/10/20/50/75/100）；
  - 不同 Top-P 阈值（p = 0.6~0.98）；
  - 不同上下文粒度（文档级 vs 句子级）。
- **消融研究**：不同层数（L = 7/13/15/23/31）与微调与否的对比。
- **置信度验证**：将置信度分数分箱后统计 F1 分数，并计算 Pearson 相关系数。
- **补充实验**：以 Qwen2.5-7B-Instruct-1M 作为读者模型验证模型无关性。

实验设计总体客观公平，所有基线统一使用 Llama-3.1-8B-Instruct 作为读者模型，并沿用其官方实现；但训练数据仅来自 HotpotQA，其余数据集为零样本评估，跨数据集泛化性的验证有待加强。

### 6. 论文的主要结论与发现

- **三组关键观察**：
  1. LLM 中间层部分注意力头能有效识别相关信息；
  2. 注意力分配模式会随相关信息密度自适应变化（短依赖任务注意力集中，长依赖任务注意力分散）；
  3. 当上下文与查询相关性下降时，模型对初始 token 的注意力显著上升（注意力 sink 现象）。
- **压缩效果**：AttnComp 在微调后的平均准确率比未压缩基线提升 1.9 个百分点，而所有其他压缩方法至少下降 3 个点；平均压缩率达 17×。
- **多跳优势**：在多跳 QA 数据集上，AttnComp 平均准确率比未压缩基线提升 3.3 点，在 2WikiMultiHopQA 上比 Provence 高 8.8 点，验证了其上下文感知的信息整合能力。
- **延迟表现**：端到端延迟降至未压缩基线的 49%（平均压缩延迟 0.91 秒，生成延迟 0.16 秒）。
- **置信度估计**：置信度分数与 F1 分数呈正相关（HotpotQA 上 Pearson 系数为 0.35），低置信度区间（<0.1）平均 F1 为 0.13，高置信度区间（>0.9）平均 F1 为 0.91。

### 7. 优点

- **新颖的注意力利用方式**：直接利用 LLM 内在的注意力机制进行压缩，无需额外训练大型模型，仅微调 0.5% 参数即可取得显著效果。
- **真正自适应**：Top-P 压缩算法根据注意力分布动态决定保留文档数（实验中从 0 到 23 个不等），摆脱了固定压缩率的限制。
- **上下文感知的多文档整合**：在文档级联合计算注意力，能捕捉跨文档语义关联（案例分析清楚展示了这一点），在多跳 QA 上优势明显。
- **额外提供置信度估计能力**：这不仅帮助用户判断回答可靠性，还为未来迭代式 RAG 研究提供了价值。
- **低延迟高压缩率**：兼顾了精度与效率，端到端延迟显著低于抽象式压缩方法。
- **消融与鲁棒性分析完备**：对层数、训练策略、阈值、检索数量、粒度等均做了充分验证。

### 8. 不足与局限

- **模型规模有限**：受计算资源约束，仅在 8B 参数模型上验证，未评估更大规模模型（如 70B+）上的表现。
- **架构覆盖窄**：仅验证了稠密 transformer 架构，未探索 MoE（Mixture-of-Experts）等模型架构的适用性。
- **自动标注可能存在噪声**：数据标注依赖 Llama-3.1-8B-Instruct 进行答案验证，LLM 幻觉可能导致部分标注错误。
- **置信度估计维度单一**：仅考虑检索质量，未涵盖 LLM 参数知识、信息整合方式等其他影响回答可靠性的因素，存在评估偏差风险。
- **压缩可能引入偏差**：压缩模型可能表现出主题相关的偏好，在敏感或高风险领域带来公平性和可靠性问题。
- **跨数据集泛化验证不足**：训练数据仅源于 HotpotQA，其他数据集全部为零样本评估，对训练集分布之外场景的适应性需要进一步验证。

（完）
