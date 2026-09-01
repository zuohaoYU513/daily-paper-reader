---
title: "FactReasoner: A Probabilistic Approach to Long-Form Factuality Assessment for Large Language Models"
title_zh: FactReasoner：大型语言模型长文本事实性评估的概率方法
authors: "Radu Marinescu, Debarun Bhattacharjya, Junkyu Lee, Tigran T. Tchrakian, Javier Carnerero-Cano, Yufang Hou, Elizabeth M. Daly, Alessandra Pascale"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.785.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 结合外部知识检索的概率化长文本事实性评估
tldr: 大型语言模型在长文本生成中常出现事实性错误，而现有评估方法难以捕捉其逻辑关系。本文提出 FactReasoner，一种基于神经符号的概率事实性评估框架：先将长回复拆分为原子事实单元，再从外部知识源检索相关上下文，并对这些单元与上下文之间的蕴含、矛盾等逻辑关系进行概率建模。通过综合分析这些关系，FactReasoner 能给出长回复的可靠事实性判断，为长文本生成提供了更精细、可解释的事实评估手段，也有助于指导模型纠正错误。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 783, \"height\": 156, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 764, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 717, \"height\": 1158, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 713, \"height\": 1156, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 717, \"height\": 1158, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 713, \"height\": 1157, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp785/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 717, \"height\": 1159, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 727, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 806, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 723, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 728, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 731, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 730, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 729, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 732, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 723, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 725, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 728, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 730, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 728, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 729, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 802, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 804, \"height\": 132, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 801, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 796, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 810, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 811, \"height\": 610, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 806, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 799, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 797, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 795, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 803, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 796, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 794, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 798, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 797, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 794, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 789, \"height\": 58, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 794, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 796, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 795, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-040.webp\", \"caption\": \"\", \"page\": 0, \"index\": 40, \"width\": 798, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-041.webp\", \"caption\": \"\", \"page\": 0, \"index\": 41, \"width\": 798, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-042.webp\", \"caption\": \"\", \"page\": 0, \"index\": 42, \"width\": 795, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-043.webp\", \"caption\": \"\", \"page\": 0, \"index\": 43, \"width\": 787, \"height\": 58, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-044.webp\", \"caption\": \"\", \"page\": 0, \"index\": 44, \"width\": 798, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-045.webp\", \"caption\": \"\", \"page\": 0, \"index\": 45, \"width\": 797, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-046.webp\", \"caption\": \"\", \"page\": 0, \"index\": 46, \"width\": 795, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-047.webp\", \"caption\": \"\", \"page\": 0, \"index\": 47, \"width\": 796, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-048.webp\", \"caption\": \"\", \"page\": 0, \"index\": 48, \"width\": 797, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-049.webp\", \"caption\": \"\", \"page\": 0, \"index\": 49, \"width\": 795, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-050.webp\", \"caption\": \"\", \"page\": 0, \"index\": 50, \"width\": 804, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-051.webp\", \"caption\": \"\", \"page\": 0, \"index\": 51, \"width\": 804, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-052.webp\", \"caption\": \"\", \"page\": 0, \"index\": 52, \"width\": 805, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-053.webp\", \"caption\": \"\", \"page\": 0, \"index\": 53, \"width\": 805, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-054.webp\", \"caption\": \"\", \"page\": 0, \"index\": 54, \"width\": 804, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-055.webp\", \"caption\": \"\", \"page\": 0, \"index\": 55, \"width\": 803, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-056.webp\", \"caption\": \"\", \"page\": 0, \"index\": 56, \"width\": 803, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-057.webp\", \"caption\": \"\", \"page\": 0, \"index\": 57, \"width\": 804, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp785/table-058.webp\", \"caption\": \"\", \"page\": 0, \"index\": 58, \"width\": 985, \"height\": 2232, \"label\": \"Table\"}]"
motivation: 长文本生成常包含隐含的事实错误，现有评估缺乏对逻辑关系的显式建模。
method: 将回复分解为原子单元，检索外部上下文，并用概率编码建模蕴含与矛盾关系，评估事实性。
result: FactReasoner 在长文本事实性评估任务上结合外部知识取得了可靠结果。
conclusion: 为长文本LLM提供了一种概率化、可解释的事实性评估框架。
---

## Abstract
Large language models (LLMs) have achieved remarkable success in generative tasks, yet they often fall short in ensuring the factual accuracy of their outputs thus limiting their reliability in real-world applications where correctness is critical. In this paper, we present FactReasoner, a novel neuro-symbolic based factuality assessment framework that employs probabilistic reasoning to evaluate the truthfulness of long-form generated responses. FactReasoner decomposes a response into atomic units, retrieves relevant contextual information from external knowledge sources, and models the logical relationships (e.g., entailment, contradiction) between these units and their contexts using probabilistic encodings. It then estimates the posterior probability that each atomic unit is supported by the retrieved evidence. Our experiments on both labeled and unlabeled benchmark datasets demonstrate that FactReasoner often outperforms state-of-the-art prompt-based methods in terms of factual precision and recall.

---

## 论文详细总结（自动生成）

# FactReasoner：大型语言模型长文本事实性评估的概率方法 — 详细总结

## 1. 核心问题与研究动机

- **背景问题**：大型语言模型（LLMs）在生成任务中表现出色，但生成的文本常包含**幻觉（hallucination）**，即与真实世界知识相矛盾的事实性错误，严重限制了其在需要高正确性的真实场景中的可靠性。
- **现有方法的不足**：当前主流的长文本事实性评估方法（如FactScore、VeriScore、FactVerify）均为**基于提示（prompt-based）**的方法，主要分为三步：①将回复分解为原子事实单元；②从外部知识源检索证据；③提示LLM判断每个原子是否被证据支持。这类方法存在三个关键局限：
  - **上下文跨原子相关性被忽略**：为某个原子检索的上下文可能与其他原子相关（支持或矛盾），但提示方法难以在有限上下文窗口中整合所有信息。
  - **上下文之间的冲突难以处理**：多个检索上下文之间可能彼此矛盾，提示方法缺乏原则性的机制来解决这类冲突。
  - **未能充分利用LLM在NLI（自然语言推理）任务上的优势**，而是直接让LLM做复杂的事实性判断。
- **论文目标**：提出一种**神经符号（neuro-symbolic）**的评估框架FactReasoner，将事实性评估转化为概率推理问题，以更稳健、更可解释的方式评估长文本回复的事实准确性。

## 2. 方法论：FactReasoner 框架

### 2.1 核心思想

- FactReasoner 将回复中的**原子单元**和从外部知识源检索到的**上下文**分别建模为二值变量（true/false），并利用**因子图（factor graph）/ 概率图模型**刻画它们之间的逻辑关系（蕴含、矛盾、等价）。
- 通过对图模型进行概率推理（计算后验边缘概率），获得每个原子单元被证据支持的**概率估计**，从而判断该原子为真/假/未定。

### 2.2 技术细节

- **变量定义**：
  - 原子变量集合：Xa = {A1, ..., An}，每个对应回复中的一个原子事实。
  - 上下文变量集合：Xc = {C1, ..., Cm}，每个对应检索到的一段外部证据。
  - 每个变量均为二值：`true` 或 `false`。

- **因子（Factors）设计**：
  - **先验因子**：原子先验均为 `f(ai)=0.5, f(¬ai)=0.5`（不作先验假设）；上下文先验设为 `f(cj)=0.99`（假设外部知识源可靠，若来源可信度低可调低）。
  - **二元关系因子**：由预训练的关系模型（如BERT或LLM）对文本对（原子, 上下文）或（上下文, 上下文）进行NLI分类，输出 `{none, entail, contradict, equivalence}` 及其概率 `p*`，然后依据特定规则将逻辑关系编码为条件概率表（见论文表1）。例如：
    - 若是蕴含关系（上下文 C 蕴含原子 A），则 `P(A=true|C=true)=p*`；
    - 若是矛盾关系，则 `P(A=false|C=true)=p*`，以此类推。
  - 因子集合包含：原子-上下文因子 `f(Ai, Cj)`、上下文-上下文因子 `f(Cj, Ck)`、原子先验因子和上下文先验因子。

- **推理算法**：
  - 使用 **Weighted Mini-Buckets (WMB)** 近似变分推理算法，计算每个原子变量的后验边缘概率 `P(ai)`。
  - 推理效率极高：论文报告所有基准的推理时间均小于 **0.05 秒**。
  - 原子分类规则：`P(ai) > P(¬ai)` 时判定为支持（supported），否则为不支持。

- **三个变体**：
  - **FR1**：仅考虑每个原子与其 top-k 检索上下文之间的关系。
  - **FR2**：去重所有检索到的上下文，考虑每个原子与**所有**去重上下文之间的关系。
  - **FR3**：在FR2的基础上，额外考虑**上下文与上下文之间**的关系。

- **完整流水线**：包含四个阶段——**Atomizer**（将回复分解为原子单元）、**Reviser**（对原子进行去上下文化改写）、**Retriever**（从Wikipedia/Google Search检索证据）、**Evaluator**（构建图模型并做概率推理评估）。

- **新增评估指标**：提出基于熵的 **E-measure**，利用原子的后验概率衡量整体回复的事实性不确定性（E 越接近0，回复越可信）。

## 3. 实验设计

- **数据集**：
  - **有标注**：Biographies（157篇ChatGPT生成的人物传记，含人工标注的原子级ground truth）。
  - **无标注**：AskHistorians（AskH）、ELI5、FreshBooks（Books）、LongFact-Objects（LFObj）。
  - **自制数据集**：Conflicts——从ConflictBank中随机采样1000条真实声明，每条配备一条支持性上下文和一条矛盾性上下文（用于专门测试冲突处理能力）。
- **对比方法**：FactScore（FS）、FactVerify（FV）、VeriScore（VS），并额外引入DeepSeek-v3作为强力参考。所有方法共享相同的原子分解、改写和检索结果，确保评估公平。
- **后端LLM**：granite-3.0-8b-instruct、llama-3.1-70b-instruct、mixtral-8x22b-instruct 三个开源模型，前端生成回复统一使用 llama-3.3-70b-instruct。
- **知识源**：Wikipedia（每原子 top-3 上下文）和 Google Search（每原子 top-5 上下文）。
- **评估指标**：事实精确率（Pr）、F1@K、MAE（仅标注集）、标准F1（仅标注集）、E-measure（仅FR）。

## 4. 资源与算力

- 论文提到所有LLM均远程托管在配备 **A100 80GB GPU** 的计算节点上，通过 litellm API 访问，可支持每秒1500个prompt的吞吐。
- **未明确说明**具体使用的GPU数量、训练时长或整体计算成本。

## 5. 实验数量与充分性

- **实验覆盖较广**：涵盖5个公开基准数据集+1个自制冲突数据集；两种外部知识源；三种后端LLM；三类baseline方法 + DeepSeek-v3 + FactReasoner 三个变体；进行了关系模型对比（BERT vs LLM）、统计显著性检验、Brier score校准评估、ROC曲线分析等，实验数量较充足。
- **公平性较好**：所有方法共享完全相同的原子集和上下文集；超参数固定；在标注数据集上比较MAE和F1，统计显著性检验支持主要结论。
- **不足之处**：
  - 关系模型仅评估了两种（vitc BERT和llama-3.1），未对更多NLI模型做系统化比较。
  - 未设置不同大小的K值参数敏感性实验。
  - 在无标注数据集上无法精确验证是否存在误报问题。

## 6. 主要结论与发现

- **FR2/FR3显著优于 prompt-based 方法**：在 Biographies 标注数据集上，FR2/FR3（使用LLM/llama-3.1-70b 和 mixtral-8x22b 时）相比 FV/VS/FS 在精度、F1、F1@K 上更优，MAE更低，统计显著性检验 p 值近零。
- **冲突处理能力突出**：在 Conflicts 数据集上，FR2/FR3 准确率超80%（llama），而 prompt-based 方法在冲突情境下准确率显著更低（如FS仅0.35）；FR 能通过上下文间的矛盾关系削弱虚假证据的影响。
- **无标注数据集表现**：FR2/FR3 在多数情况下取得最高Pr和F1@K，优于FV/VS，与DeepSeek-v3相当或更优；FS虽识别的支持原子最多，但可能包含大量假阳性。
- **FR3 ≈ FR2**：上下文-上下文关系在多数情况下是等价关系，因此FR3相比FR2提升有限。
- **LLM关系模型优于BERT关系模型**：在Biographies数据集上，基于llama的关系模型F1接近BERT关系模型的2倍。
- **概率校准良好**：Biographies上FR2（llama-3.1-70b）的平均Brier分数为0.18，说明概率输出具有合理校准度。

## 7. 优点与创新亮点

- **范式创新**：从“直接提示LLM做事实判断”转向“将事实性评估转化为概率图模型上的推理问题”，更稳健、更可解释。
- **充分利用NLI能力**：将复杂事实判断分解为多个简单的蕴含/矛盾判断，发挥LLM在NLI任务上的强项。
- **显式建模上下文间的冲突与支持关系**：能够综合全部证据，解决现有方法难以处理的冲突情况。
- **输出概率化结果**：不止给出二元判断，而是输出每个原子的后验概率，支持更丰富的下游应用和不确定性量化评估。

## 8. 不足与局限

- **上游模块敏感**：Atomizer和Reviser的表现受提示质量、few-shot示例和所选模型影响较大，论文仅用llama-3.3-70b-instruct一种模型，可能引入偏差。
- **检索器限制**：使用现成的LangChain Wikipedia检索器，未采用更先进的检索策略或LLM生成查询，可能影响证据质量。
- **关系模型依赖**：关系提取的准确性直接影响图模型质量，论文采用简单prompt和少量模型，未做微调优化。
- **计算开销**：FR2需要O(n·m)次NLI调用，FR3需要O(n·m + m²)次，相比prompt-based方法的O(n)有显著增加（其中n为原子数，m为去重后上下文数）。
- **FR1性能较弱**：当仅依赖每个原子的 top-k 上下文时，FR1的表现与FV/VS相当，说明全局信息整合是性能提升的关键，但也是在计算开销上最重的部分。
- **无标注数据集验证受限**：对无标注集上FS的高支持数是否包含更多假阳性，只能推测而无法确证，缺乏更细粒度的证据。
- **未披露完整算力信息**：未说明整体实验中GPU数量和总计算时长，不利于复现和成本评估。

（完）
