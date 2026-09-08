---
title: Enhanced Language Model Truthfulness with Learnable Intervention and Uncertainty Expression
title_zh: 通过可学习干预与不确定性表达增强语言模型真实性
authors: "Farima Fatahi Bayat, Xin Liu, H. Jagadish, Lu Wang"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.737.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: LITO选择最准确回答或拒答，直接对应选择性预测与弃权机制
tldr: 针对LLM幻觉问题，现有推理期干预方法以固定强度将表示推向真实方向，难以跨查询泛化。LITO提出可学习的适真性干预方法，自动确定每个上下文的最优干预强度，并探索一系列增强强度的生成序列，从中挑选最准确的回答或直接拒答。实验表明该方法能在不同上下文下有效提升生成真实性并避免低质量输出，是选择性预测与拒答机制的直接实现。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl737/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl737/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1504, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl737/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1642, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl737/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl737/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1646, \"height\": 356, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl737/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1484, \"height\": 867, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl737/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1489, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl737/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 717, \"height\": 309, \"label\": \"Table\"}]"
motivation: 统一强度的真实方向干预无法适配不同上下文，导致LLM真实性提升效果受限。
method: 提出LITO，学习每个上下文的最优干预强度，并通过递增强度探索生成序列，选择最准确回答或拒答。
result: 在多种上下文下，LITO提升回答真实性与准确性，并通过拒答避免不可靠输出。
conclusion: 上下文自适应的可学习干预与不确定性表达是提升LLM真实性、实现可控拒答的有效路径。
---

## Abstract
Large language models (LLMs) can generate long-form and coherent text, yet they often hallucinate facts, which undermines their reliability. To mitigate this issue, inference-time methods steer LLM representations toward the “truthful directions” previously learned for truth elicitation. However, applying these truthful directions with the same intensity fails to generalize across different query contexts. We propose LITO, a Learnable Intervention method for Truthfulness Optimization that automatically identifies the optimal intervention intensity tailored to each specific context. LITO explores a sequence of model generations based on increasing levels of intervention intensities. It selects the most accurate response or refuses to answer when the predictions are highly uncertain. Experiments on multiple LLMs and question-answering datasets demonstrate that LITO improves truthfulness while preserving task accuracy. The adaptive nature of LITO counters the limitations of one-size-fits-all intervention methods, maximizing truthfulness by reflecting the model’s internal knowledge only when it is confident. Our code is available at https://github.com/launchnlp/LITO.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- 大型语言模型（LLM）虽然能生成连贯的长文本，但常产生缺乏真实世界依据的“幻觉”内容，严重限制其在关键应用中的可靠性。
- 现有推理期干预方法（如 ITI）通过在模型内部表征中识别“真实方向”（truthful directions），并在生成时以**固定强度**将激活推向该方向，从而提升真实性。
- 然而，**固定干预强度无法适配不同查询上下文**。论文图 1 表明：不同问题往往在不同干预强度下才能得到正确回答，有些问题无论强度如何变化都无法被纠正（例如“What flag is red and has a gold star?”）。
- 因此，论文提出一个关键问题：**如何针对每个具体上下文自动确定最优干预强度，并在无法可靠作答时恰当地表达不确定性？**

## 2. 方法论：LITO（Learnable Intervention for Truthfulness Optimization）

### 核心思想

- 不再对所有查询使用同一干预强度，而是**学习一个自适应的强度选择策略**：以多个递增强度干预模型，收集一系列生成结果，从中筛选出最可能真实的回答；若全部不可靠，则拒答（输出“I have no comment"）。
- LITO 是与底层干预方法无关的框架，论文将其实例化在两种干预技术上：ITI（Inference-time Intervention）与 RepE（Representation Engineering）。

### 技术细节

1. **多强度生成采样**：基于 ITI 学到的真实方向集合 \(D=\{d_h^l\}\)，在 k 组递增强度 \(\alpha \in \{5, 10, 15, 20, 25\}\) 下分别干预模型，获得 k 个响应 \(A=\{a_1,...,a_k\}\)。
2. **每个响应的三部分特征**：
   - 文本输出 \(y_i\)；
   - 最后一层隐藏状态 \(h_i\)（对生成 token 的隐藏状态取平均）；
   - 置信度分数 \(p(y_i|x)\)：基于 token 概率的几何平均：
     \[
     p(y_i|x)=\sqrt[N]{\prod_{t=1}^{N} p(y_{i,t}|x, y_{i,<t})}
     \]
3. **LSTM 序列分类器**：将 k 个响应的聚合隐藏状态 \(h_1,...,h_k\) 按干预强度递增顺序输入一层 LSTM，使模型学习随强度变化的响应模式（如正确性转折点、置信度骤降等）；LSTM 输出经全连接层与 sigmoid 得到每个响应的事实性概率 \(p_w(h_{r,i})=\delta(\langle w, h_{r,i}\rangle)\)。
4. **推理时决策**：
   - 将被判定为真实（概率 > 0.5）的所有候选中置信度最高者作为最终回答；
   - 若所有响应都被判为不真实，则输出 “I have no comment” 以表达不确定性：
     \[
     i^* = \arg\max_i p(y_i|x) \quad \text{s.t.} \quad \delta(\langle w, h_{r,i}\rangle)>0.5
     \]
5. **标签构造**：短语级 QA 用 DeBERTa-large（MultiNLI fine-tuned）通过文本蕴含判断正确性；TruthfulQA 用 GPT-4 判断语义等价性。

## 3. 实验设计

### 数据集与基准

| 类型 | 数据集 | 响应层次 |
|---|---|---|
| 短语级开放域 QA | Natural Questions (NQ)、SciQ、TriviaQA | 短语/实体 |
| 句子级 QA | TruthfulQA | 完整句子 |

每个数据集按 1K 样本训练 ITI 探针，LITO 用 3K 训练样本；TruthfulQA 因其无官方训练集，用 408 个样本训练并评估其余数据。

### 评估指标

- **Truthfulness**：准确回答与不确定性回答之和所占比例。
- **Accuracy**：任务准确率。
- **TA score**：真实性与准确率的几何平均：
  \[
  TA=\sqrt{\text{Truthfulness}\times\text{Accuracy}}
  \]
  用于衡量真实性提升与任务准确性保持之间的平衡。

### 模型

- **Llama 系**：Llama2-Chat-7B、Llama2-Chat-13B、Vicuna-7B。
- **GPT-2 系**：GPT2-large、GPT2-XL。

### 对比方法

- 原始 LM（无干预）；
- ITI（best of 5）——取 5 个固定强度中表现最优者（oracle 选取）；
- Majority Voting（多数投票）；
- Maximum Confidence（最大置信度）；
- Maximum Confidence > T（阈值过滤 + 拒答机制，T=0.6）；
- LITO（本文方法）。

另有 RepE 实例化实验、跨领域迁移实验、LSTM vs MLP 消融、k 值调节实验等。

## 4. 资源与算力

- 训练 LITO 及收集模型输出共进行 **100 次实验**，每次约需 **1–2 小时**，使用 **单张 NVIDIA A40 GPU**。
- LITO 自身的训练（20 次，按模型与数据集组合各一次）使用 **64 个 CPU 核心**，单次在 **3–5 分钟内**完成。
- 需要指出：LITO 在推理时对 LLM 进行 k 次前向查询，因此比单次 ITI/RepE 慢约 k 倍（本文 k=5），但其自身的可学习模块开销极低。

## 5. 实验数量与充分性

- **主实验**：4 个数据集 × 5 个 LM，共 20 组 TA 分数对比，覆盖不同响应长度、不同模型规模与训练方式，规模充足。
- **扩展实验**：
  - RepE 作为底层干预方法的泛化实验（4 数据集 × 2 类 LM）；
  - 跨域迁移实验（5 个 LM 的两两数据集组合）；
  - 设计选择消融（LSTM vs MLP、k 值调优）。
- **公平性评估**：基线包含 oracle 强度选取（对基线有利）、最大置信度、投票等聚合策略；使用统一的 prompt 格式与阈值设定。实验整体较为客观，但只评估了短语级和句子级 QA，未涉及长文本生成。

## 6. 主要结论与发现

- LITO 在几乎所有实验设定中优于原始 LM 与现有基线，显著提升平衡指标 TA score。
- 示例：在 NQ 上，LITO 将 Llama2-Chat-7B 的 TA 分数提升 9.6 分；对 GPT2-large 与 GPT2-XL 的平均 TA 提升达 +14.4 与 +12.0。
- LITO 在真实性上始终处于前两名，同时将准确率保持在 ITI 的 5% 以内（20 组实验中的 16 组）。
- 用 RepE 实例化 LITO 同样有效——4 个数据集上分别比 RepE best-of-5 提升 +9、+2.5、+4.9 与 +1.5 TA 点，验证了框架的可泛化性。
- 跨域迁移实验表明 LITO 学到的是任务无关的“真实性”概念，在大多数跨任务设定下表现良好，且在 NQ + GPT2-Large 上甚至超过域内表现。

## 7. 优点与亮点

- **自适应干预强度**：针对不同上下文动态确定最优干预强度，克服了固定强度方法的根本局限。
- **显式不确定性表达**：引入 “I have no comment” 拒答机制——当模型对所有干预强度的输出都不自信时放弃作答，有效降低幻觉。
- **框架通用性**：与底层干预方法解耦，可适配 ITI、RepE 及未来同类技术。
- **新颖评估指标 TA score**：同时考虑真实性与任务准确率，避免模型通过过度拒答“刷真实性”的作弊行为。
- **特征设计合理**：利用 LSTM 建模跨强度响应的序列信息，让模型从响应整体模式中识别可靠“干预区间”。
- **计算开销分布合理**：主要开销在 LLM 多强度前向调用，可学习模块训练极轻量（3–5 分钟）。

## 8. 不足与局限

- **响应长度覆盖有限**：仅测试了短语级与句子级回答，未验证长文本生成场景下的有效性。
- **对底层干预方向质量敏感**：LITO 的准确度依赖于所学习“真实方向”的质量，输入的干预信号若本身存在偏差，则 LITO 的提升也会受限。
- **推理开销增加**：相比单次干预方法，需要 k 次 LLM 推理调用（约为原来的 k 倍），影响实时性。
- **部分场景需要权衡**：LITO 在部分数据集上会牺牲少量准确率以换取更高的真实性；在 Vicuna-7B 上不如 Maximum Confidence > T 基线高。
- **TruthfulQA 训练的跨域迁移能力较弱**，且该任务的 LSTM F1 分数相对于 MLP 有所下降，可能受限于训练数据规模。
- **可解释性不足**：LITO 选择判定的内部机制尚未深入可视化，未来可探索模型对“不确定性”随干预强度变化的学得表示。

（完）
