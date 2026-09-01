---
title: Hallucination Detection in LLMs with Topological Divergence on Attention Graphs
title_zh: 基于注意力图拓扑散度的大型语言模型幻觉检测
authors: "Alexandra Bazarova, Andrei Volodichev, Aleksandr Yugay, Andrey Shulga, Alina Ermilova, Konstantin Polev, Julia Belikova, Rauf Parchiev, Dmitry Simakov, Maxim Savchenko, Andrey Savchenko, Serguei Barannikov, Alexey Zaytsev"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.704.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 基于注意力图拓扑散度检测LLM幻觉，尤其适用于RAG
tldr: 幻觉是LLM在RAG设置中的关键挑战，输出可能缺少上下文支持。本文提出TOHA，利用注意力矩阵诱导图的拓扑散度量化提示子图与回复子图的结构差异，发现特定注意力头的较高散度与不忠实输出相关，且跨数据集一致。在问答和摘要任务上的实验验证了其有效性，为LLM幻觉检测提供了无需额外训练的拓扑判据。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 1043, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1709, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 814, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 792, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1615, \"height\": 1024, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long704/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1638, \"height\": 710, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 1469, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1504, \"height\": 721, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 813, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 697, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 700, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 727, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1484, \"height\": 598, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 838, \"height\": 1499, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 741, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 625, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1650, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1650, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 553, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1653, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long704/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 805, \"height\": 250, \"label\": \"Table\"}]"
motivation: RAG设置下LLM可能生成缺乏上下文支持的内容，需要有效的幻觉检测方法。
method: 提出基于注意力图拓扑散度的幻觉检测器TOHA，比较提示与回复子图的结构差异。
result: 实验显示特定注意力头的拓扑散度与幻觉输出稳定相关，检测效果优越。
conclusion: 提供了一种数据无关的拓扑信号用于LLM幻觉检测。
---

## Abstract
Hallucinations remain a critical challenge for large language models (LLMs), particularly in Retrieval-Augmented Generation (RAG) settings where models may generate outputs unsupported by the provided context. To address this, we introduce TOHA, a TOpology-based HAllucination detector, which leverages a topological divergence metric to quantify the structural properties of graphs induced by attention matrices. Examining the topological divergence between prompt and response subgraphs in RAG settings reveals consistent patterns: higher divergence values in specific attention heads correlate with unfaithful outputs, independent of the dataset. Extensive experiments — including evaluations on question answering and summarization tasks — show that our approach achieves state-of-the-art or competitive results on several benchmarks while requiring minimal annotated data and computational resources. Our findings indicate that the topological structure of attention matrices provides an efficient and robust metric for assessing the correctness of LLM’s responses.

---

## 论文详细总结（自动生成）

# 《基于注意力图拓扑散度的大型语言模型幻觉检测》论文详细总结

## 1. 核心问题与研究动机

- **背景**：大型语言模型（LLM）在检索增强生成（RAG）场景中，虽然借助外部知识库提升了事实性，但仍会产生**幻觉**，即生成内容与提供的上下文不一致或不忠实。
- **现有方法的痛点**：
  - 基于一致性的方法（如 SelfCheckGPT、语义熵）需要多次采样生成，**计算成本高**；
  - 基于监督分类器的方法依赖**大规模标注数据**，且跨任务泛化性差；
  - 基于输出概率（如困惑度）的方法无法充分捕捉模型内部的不确定性；
  - 已有注意力图方法要么把所有注意力头同等对待，要么只利用简单的图属性（如自环权重），**忽略了注意力图蕴含的几何结构**。
- **核心问题**：能否利用 LLM 注意力矩阵的**拓扑结构**，在不进行额外生成、仅需极少标注数据的条件下，高效且鲁棒地检测 RAG 场景中的幻觉？

## 2. 方法论：TOHA（Topology-based HAllucination Detector）

### 2.1 核心思想

- 将每一层的注意力矩阵视为一个**完全加权无向图**（节点为 token，边权重为 \(1 - w_{ij}\)），称为**注意力图**；
- 注意力图自然分为**提示（P）子图**和**响应（R）子图**；
- 假设：当响应不忠实于提示（即产生幻觉）时，提示与响应子图之间会表现出**更大的拓扑散度**；
- TOHA 用这种拓扑散度作为幻觉评分，并进一步筛选少数**“幻觉感知头”**（hallucination-aware heads）来聚合最终分数。

### 2.2 MTop-Div\(_G\)(R, P)：图上的拓扑散度

- 定义：将提示节点 P 内部的边权重全部置零后，计算修改后图的 **Vietoris-Rips 复形**的 **0 阶持续同调条码（B0 barcode）**；
- 散度值 = B0 中所有区间长度之和：
  \[
  \text{MTop-Div}_G(R,P) = \sum_{[b_i,d_i]\in B_0} |d_i - b_i|
  \]
- **几何解释**（Proposition 3.1）：该值恰好等于**将响应节点连接到提示节点的最小生成森林（MSF）的总边长**；
- **信息论解释**：MSF 长度可作为几何离散度的代理，因此该指标衡量的是**响应相对于提示的结构新颖性**——新颖性越高，越可能幻觉。

### 2.3 幻觉感知头的识别

- 对每个注意力头 \(h_{ij}\)，计算其在幻觉样本与正常样本上的**平均 MTop-Div 之差** \(\Delta_{ij}\)：
  \[
  \Delta_{ij} = \frac{1}{|S_{\text{hallu}}|}\sum_{s\in S_{\text{hallu}}} d_{ij}(s) - \frac{1}{|S_{\text{gr}}|}\sum_{s\in S_{\text{gr}}} d_{ij}(s)
  \]
- 实验发现：在多个数据集上，**相同的少数几个头**（如 Mistral-7B 的 4 个头、Llama-2-7B 的 3 个头）始终出现在高分离区域，说明这些头具有跨数据集的“幻觉感知”能力。

### 2.4 TOHA 算法流程

1. **头选择阶段**（需少量标注探针集，约 50–100 个样本）：
   - 计算所有头的 \(\Delta_{ij}\)，按降序排列；
   - 从 \(N=1\) 到 \(N_{\max}\)（论文取 10）逐步增加头数量，在探针集上计算 AUROC，选出最优头数 \(N_{\text{opt}}\)。
2. **预测阶段**：
   - 对测试样本，取这 \(N_{\text{opt}}\) 个头的平均 MTop-Div 作为最终幻觉分数。

### 2.5 零标注变体（TOHA Copy Heads）

- 由于幻觉感知头与模型中的**复制/归纳头（induction heads）**高度重合，可以用复制头排名（不需要任何标注）直接替代探针集选择，实现**完全无监督幻觉检测**。

## 3. 实验设计

### 3.1 数据集与任务场景

- RAGTruth 的两个子集：**MS MARCO**（长问答）、**CNN/DM**（摘要，含 Recent News）；
- **CoQA**（对话式问答）、**SQuAD**（阅读理解）、**XSum**（极端摘要）；
- 额外多跳数据集：**HotpotQA**（模拟真实复杂查询）。

### 3.2 评估模型

- LLaMA-2-7B/13B-chat、LLaMA-3.1-8B-Instruct、Mistral-7B-Instruct-v0.1、Qwen2.5-7B-Instruct。

### 3.3 对比方法（8 类基线）

- 基于不确定性：Perplexity、Max entropy；
- 基于内部状态：ReDeEP、HaloScope、LLM-Check；
- 基于一致性（多生成）：SelfCheckGPT、Semantic entropy、EigenScore；
- 公平性处理：一致性方法分别采用**单个额外生成**（效率对齐版）和 **20 个额外生成**（完整版）两种配置进行比较。

### 3.4 主要结果

- **主要表（Tables 1–2）**：TOHA 在多数数据集上取得第一或第二：
  - 例：MS MARCO（Mistral-7B）0.76 vs 最强基线 Max entropy 0.68（+11.7%）；
  - CoQA（Llama-2-7B）0.90，比最优基线高 21.6%。
- **HotpotQA 表（Table 3）**：Llama-2-13B 上 0.80，显著优于所有基线。
- **整体排名**：Wilcoxon-Holm 事后检验显示 TOHA 平均排名 1.67，且与所有基线差异**统计显著**（p ≤ 0.0016）。

## 4. 资源与算力

- 论文**未明确报告**使用的 GPU 型号、数量及具体训练时长；
- 仅在附录 E 中提到：所有实验在 **NVIDIA L40** 上完成；
- 但论文在**推理效率**方面有详细对比：在 16 个 MS MARCO 样本上，TOHA 检测时间约 **2.0 秒**，而 SelfCheckGPT 需 69 秒左右（单额外生成），Max entropy 约 10.5 秒；若 SelfCheckGPT 采用 10–20 次生成，TOHA 可快 **70 倍以上**；
- 因此，虽然算力细节不透明，但论文明确强调其方法**计算开销极低**，接近单次前向传播成本。

## 5. 实验数量与充分性

### 5.1 实验总量

- 覆盖 **5 个主要数据集 + 1 个多跳数据集**；
- **5 个不同规模的 LLM**；
- 每个结果平均 **5 次不同数据划分**；
- 包含多组消融：
  - 对比完整 MST 与 MTop-Div；
  - 对比其他注意力特征（熵、谱范数、Wasserstein 距离、稀疏度、首 token 注意力等）在监督分类器中的效果；
  - 探针集规模敏感性（50–400 样本）；
  - 头数量 \(N_{\max}\) 敏感性（1–10）；
  - 与 LookBack Lens 的注意力比率特征对比；
  - 与 100 样本训练的线性探针对比；
  - 零标注复制头变体；
  - 跨数据集迁移实验（如 MS MARCO 作为探针集在 CoQA 上测试等）；
  - 单词响应（超短输出）的退化分析。

### 5.2 充分性与公平性

- **优点**：对比基线覆盖全面，且考虑了多生成方法的两种配置（标准与效率对齐），确保比较公平；统计显著性检验完整（Wilcoxon-Holm、t 检验）；消融实验细致，足以支撑核心设计决策。
- **不足**：实验仅覆盖 7B–13B 量级的开源模型，未涉及更大规模或闭源模型（作者也在局限性中承认）；自动标注依赖 GPT-4o，虽经人工抽查验证，但仍可能存在标注噪声。

## 6. 主要结论与发现

1. **拓扑散度是有效的幻觉信号**：提示与响应的注意图拓扑散度在特定头上能稳定区分幻觉与正常输出，且跨数据集一致性高。
2. **存在通用的“幻觉感知头”**：少数注意力头（4 个/3 个）在不同数据集上表现一致，平均这些头的散度即可获得强检测性能。
3. **幻觉感知头与复制/归纳头高度重合**：这些头常出现在模型前 25 的复制排名中；幻觉生成常伴随对首 token 的过度注意力，符合“复制失败后默认指向第一个 token”的机制。
4. **检测效率大幅提升**：无需多次生成、无需大量标注（50–100 样本即可），推理速度比同级方法快一个数量级。
5. **零标注可实现**：直接使用复制头排名（TOHA Copy Heads）即可接近完整 TOHA 的性能，为无监督幻觉检测提供了新路径。
6. **跨域迁移鲁棒**：在跨数据集迁移实验中，性能下降不显著，表明方法对数据分布变化具有较好的鲁棒性。

## 7. 方法亮点

- **新颖的拓扑视角**：将 TDA 中的 MTop-Div 首次改造用于注意力图，提供既有几何意义又有信息论解释的度量；
- **极低数据需求**：仅需 50 个标注样本即可稳定工作，远低于监督方法；
- **极低计算成本**：单次前向传播 + 少量图计算，远快于一致性与采样类方法；
- **可解释性**：发现的“幻觉感知头”与可解释的复制/归纳头机制关联，增强了方法的可解释性和可信度；
- **完全无监督变体**：证明了无需任何标注也能达到具有竞争力的性能；
- **充分的统计验证**：包括多轮数据划分、标准误报告、事后多重比较检验，结论可靠。

## 8. 不足与局限

- **模型依赖**：幻觉感知头可能随模型架构变化，论文仅验证了开源 7B–13B 模型，对 GPT-4、Claude 等闭源/超大模型未验证；
- **多模态未覆盖**：当前方法仅适用于文本，扩展到视觉-语言模型需重新设计注意力图；
- **超短响应退化**：对单词回答（如 SQuAD 中的“是/否”类）性能下降明显，虽然仍高于随机，但实用性受限；
- **长响应的判别力较弱**：响应越长，幻觉信号占比越小，所有方法性能均下降，TOHA 虽优于基线但仍不够完美；
- **算力细节不透明**：未报告 GPU 数量、训练时间等资源消耗，不利于复现成本评估；
- **标注依赖 GPT-4o**：虽然验证了与人工标注一致性，但自动化标注可能带来系统性偏差；
- **风险因素**：作者在附录中提出，过度信任 TOHA 分数可能导致高风险场景（如医疗）误放行；同时注意力模式可能被对抗性提示操纵，造成规避检测的风险。

（完）
