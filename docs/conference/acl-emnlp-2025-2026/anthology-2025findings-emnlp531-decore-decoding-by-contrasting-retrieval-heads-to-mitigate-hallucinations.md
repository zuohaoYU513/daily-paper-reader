---
title: "DeCoRe: Decoding by Contrasting Retrieval Heads to Mitigate Hallucinations"
title_zh: DeCoRe：通过对比检索头解码缓解幻觉
authors: "Aryo Pradipta Gema, Chen Jin, Ahmed Abdulaal, Tom Diethe, Philip Alexander Teare, Beatrice Alex, Pasquale Minervini, Amrutha Saseendran"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.531.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 对比检索头解码，放大上下文与参数信息以减少幻觉
tldr: 大模型幻觉常源于未能正确利用上下文或内部知识。该工作关注Transformer中的检索头，假设遮蔽这些头可诱发幻觉，并由此提出DeCoRe解码策略：对比原始模型与遮蔽检索头模型的输出，放大上下文和参数中的有效信息。该方法无需训练即可减少不忠实和事实性错误输出，为解码端幻觉缓解提供了轻量方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 649, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1580, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1598, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1593, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1624, \"height\": 1167, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1411, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1419, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1567, \"height\": 1133, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1622, \"height\": 1137, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1616, \"height\": 1171, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1539, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1573, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp531/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1557, \"height\": 470, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1644, \"height\": 681, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1644, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1652, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1649, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1643, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1241, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1243, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1323, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 747, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 749, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1652, \"height\": 708, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1647, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1241, \"height\": 862, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1243, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1242, \"height\": 899, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1242, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1649, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1647, \"height\": 678, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1327, \"height\": 702, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1649, \"height\": 514, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1326, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1319, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 992, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1646, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1152, \"height\": 502, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 1661, \"height\": 1793, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 1382, \"height\": 1037, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 608, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 825, \"height\": 348, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp531/table-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 818, \"height\": 325, \"label\": \"Table\"}]"
motivation: 大模型由于错误利用上下文或记忆会产生幻觉，检索头在其中起关键作用。
method: 遮蔽检索头构造幻觉模型，对比其与基础模型的解码输出以放大正确信息。
result: DeCoRe无需训练即可有效降低幻觉，提升输出忠实性。
conclusion: 检索头对比解码是训练无关的幻觉缓解新途径。
---

## Abstract
Large Language Models (LLMs) often hallucinate, producing unfaithful or factually incorrect outputs by misrepresenting the provided context or incorrectly recalling internal knowledge. Recent studies have identified specific attention heads within the Transformer architecture, known as retrieval heads, responsible for extracting relevant contextual information. We hypothesise that masking these retrieval heads can induce hallucinations and that contrasting the outputs of the base LLM and the masked LLM can reduce hallucinations. To this end, we propose Decoding by Contrasting Retrieval Heads (DeCoRe), a novel training-free decoding strategy that amplifies information found in the context and model parameters. DeCoRe mitigates potentially hallucinated responses by dynamically contrasting the outputs of the base LLM and the masked LLM, using conditional entropy as a guide. Our extensive experiments confirm that DeCoRe improves performance on tasks requiring high contextual faithfulness, such as summarisation (XSum by 18.6%), instruction following (MemoTrap by 10.9%), and open-book question answering (NQ-Open by 2.4% and NQ-Swap by 5.5%).

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义

**研究动机与背景：**
- 大语言模型（LLMs）在多种自然语言生成任务中表现出色，但普遍存在**幻觉（Hallucination）** 问题，即生成内容在事实上不正确或缺乏上下文依据。这在医疗、法律等高风险领域尤其值得担忧。
- 已有研究（Wu et al., 2024）发现 Transformer 中存在特定注意力头——**检索头（Retrieval Heads）**——负责从上下文中提取相关信息。这些头的功能对模型的上下文忠实性至关重要，但此前鲜有研究探索如何利用这一机制来**缓解幻觉**。
- 本文的核心假设：**掩蔽检索头可以诱导模型产生幻觉**，进而可通过对比基础模型与掩蔽模型的输出分布，来放大来自上下文和模型参数中的真实信息，从而抑制幻觉输出。

---

### 2. 方法论

**DeCoRe（Decoding by Contrasting Retrieval Heads）** 是一种**无需训练（training-free）** 的解码策略，核心由三步构成：

1. **掩蔽检索头（Masking Retrieval Heads）**
   - 使用 Wu et al. (2024) 提出的方法，基于 Needle-in-a-Haystack (NitH) 数据集计算各注意力头的**检索分数（retrieval score）**，即头执行成功"复制-粘贴"操作的比例。
   - 选取检索分数最高的前 N 个头作为检索头集合 \(H_{\text{retrieval}}\)。
   - 在模型前向传播时，通过 Hadamard 积将检索头的输出置零（掩蔽处理），得到掩蔽模型 \(f_{\text{masked}}\)。该模型因无法有效检索上下文信息，更容易产生幻觉。

2. **对比解码（Contrastive Decoding）**
   - 基础模型 \(f_{\text{base}}\) 与掩蔽模型 \(f_{\text{masked}}\) 同时预测下一个 token 的分布。
   - 通过如下公式对比二者的输出分布：
   \[
   p(x_t \mid x_{<t}) \propto \exp \left[ (1+\alpha) \log p_{\text{base}}(x_t \mid x_{<t}) - \alpha \log p_{\text{masked}}(x_t \mid x_{<t}) \right]
   \]
   - 该公式**增强**基础模型青睐的 token 的概率，同时**惩罚**掩蔽模型（幻觉倾向）青睐的 token，使得最终输出更忠实于上下文。

3. **动态熵调控（Dynamic Entropy-based Control）**
   - 使用基础模型的**条件熵（conditional entropy）** 动态调整对比强度 α：
   \[
   H(x_t) = -\sum_{x_t \in V} p(x_t \mid x_{<t}) \log p(x_t \mid x_{<t})
   \]
   - 将 α 设为当前 token 的条件熵值。**熵越高（模型越不确定），α 越大，对比惩罚越强**，从而更积极地抑制可能的幻觉候选。

**变体**：
- **DeCoRe static**：α 固定不变。
- **DeCoRe entropy**：α 动态取条件熵，完整版。
- **DeCoRe entropy-lite**：使用同词表但更小的模型作为掩蔽模型（如用 Llama3-8B 辅助 Llama3-70B），以降低计算成本。

---

### 3. 实验设计

**评估任务与数据集**（按幻觉类型划分）：

| 任务类型 | 数据集 | 评估指标 |
|---------|--------|---------|
| 上下文忠实性（Faithfulness） | XSum（摘要）、MemoTrap（指令遵循）、IFEval（指令遵循）、Open-book NQ-Open（开放问答）、NQ-Swap（实体交换问答） | ROUGE-L、BERTScore、factKB、Macro/Micro Accuracy、Prompt/Instruct Strict Accuracy、EM |
| 事实准确性（Factuality） | TruthfulQA（MC1/MC2/MC3/Gen）、TriviaQA、PopQA、Closed-book NQ-Open | EM、MC指标、GPT-judge评估（TruthfulQA Gen） |
| 多跳推理（Chain-of-Thought） | MuSiQue（Closed-book / Open-book，有无 CoT） | EM |

额外场景：
- **Lost-in-the-Middle (LitM)** 干扰文档实验：1个关键文档 + 9个干扰文档，变体关键文档位置（第1/第4/第9）。

**对比基线方法**：
- Greedy Decoding（贪心解码）
- Contrastive Decoding（CD）
- Context-Aware Decoding（CAD）
- Decoding by Contrasting Layers（DoLa-low / DoLa-high）
- Activation Decoding（AD）
- Inference-Time Intervention（ITI，需要训练的基线）

**主实验模型**：Llama3-8B-Instruct、Llama3-70B-Instruct；附录还测试了 Mistral-7B-Instruct-v0.3、Qwen2-7B-Instruct。

---

### 4. 资源与算力

论文在实验设置中给出了明确的算力信息：
- **GPU 类型**：NVIDIA A100 80GB
- **数量**：7B/8B 参数模型使用 1 块 GPU；70B 参数模型使用 2 块 GPU
- **训练时长**：DeCoRe 无需训练，因此没有训练时间。ITI 基线需要训练，但论文未报告其具体训练时长。
- **TruthfulQA Generation 评估成本**：微调两个 davinci-002 模型约花费 **43 美元**，每次评估约 **0.8 美元**。

---

### 5. 实验数量与充分性

论文实验规模**非常充分**，主要包含以下实验模块：

- **主实验**：2 个模型 × 3 类任务（Faithfulness、Factuality、CoT）× 9-10 种解码策略。
- **消融研究**：
  - 掩蔽不同数量的检索头（0–100，步长10）对各任务的影响。
  - 对比掩蔽**随机头**的效果（有误差棒）。
  - DeCoRe static 中 α 的选择（-0.5 至 8.0）对各任务的影响。
  - 其他模型家族（Mistral、Qwen2）的验证。
- **统计显著性检验**：
  - EM/MC1 等离散指标用 **McNemar's Test**。
  - ROUGE、BERTScore 等连续指标用 **Bootstrap Resampling**。
  - 进行了 Bonferroni 多重比较校正。
- **熵分析**：
  - 验证了条件熵与正确性的相关性（T-test、Mann-Whitney U-test）。
  - 比较不同解码策略在长生成任务中的长度归一化熵。
- **计算性能对比**：报告了 TFLOPS（DeCoRe 约 4.32，CAD 为 8.44）。
- **定性样例**：展示了 XSum、TruthfulQA、MuSiQue 上的输出样例与熵曲线。

该实验设计**覆盖面广、对比充分、统计检验严谨**，公平性较好。

---

### 6. 主要结论与发现

1. **DeCoRe 显著提升上下文忠实性**：
   - XSum factKB：从 47.61 提升至 66.10（+18.6% 相对提升）。
   - MemoTrap Macro Acc：从 65.86% 提升至 74.14%。
   - Open-book NQ-Open EM：从 69.68 提升至 70.66。
   - NQ-Swap EM：从 60.62 提升至 66.08。

2. **在干扰文档场景（Lost-in-the-Middle）中表现稳健**，优于或持平所有基线，尤其是在关键文档位置靠后时仍有较好的 EM 表现。

3. **事实性任务（Factuality）** 也获得改善，虽然幅度相对较小，但在 PopQA、Closed-book NQ-Open 等任务上有所提升。TruthfulQA Gen 任务中 DeCoRe entropy 得分较高（信息量 / 真值交叉指标 53.00%，仅次于需训练的 ITI）。

4. **结合 CoT 可提升多跳推理能力**：
   - Llama3-8B：MuSiQue Open + CoT 从 69.84 提升至 74.47。
   - Llama3-70B：从 74.43 提升至 75.05。

5. **熵随生成过程降低**：在长生成任务中，DeCoRe entropy 生成的序列具有更低的长度归一化条件熵，表明其整体不确定性更低、输出更可靠。

6. **检索头掩蔽确实能够诱发幻觉**，且掩蔽检索头比掩蔽随机头对上下文忠实性任务的影响更显著——验证了核心假设。

---

### 7. 优点

- **无需训练**（training-free）：相比 ITI（需要微调），DeCoRe 设计为纯推理时方法，部署成本低且通用性强，可在任意现有模型上直接应用。
- **具备可解释性基础**：以可解释性研究（检索头）为理论依据，利用模型内部机制引导解码，而非启发式规则或额外训练信号。
- **动态熵调控机制设计巧妙**：根据模型自身预测的不确定性自适应调整对比强度，避免了固定 α 在不同任务中表现不一的问题（附录 J 展示了不同任务对 α 的敏感性差异）。
- **实验体系非常全面**：覆盖多种任务类型（faithfulness / factuality / reasoning）、多个模型规模（8B / 70B）与家族（Llama3 / Mistral / Qwen2）、多种消融设置和统计检验。
- **计算效率较高**：通过共享 KV Cache 实现，TFLOPS 与贪心解码相当（~4.32），远低于 CAD（8.44）。
- **附带详实的定性分析与样本展示**，有助于直观理解熵与生成过程的关系。

---

### 8. 不足与局限

- **性能提升具有任务依赖性，并非在所有任务上优于全部基线**：
  - ITI 在 TruthfulQA 上仍是最佳方法（需训练），CAD 在 NQ-Swap 上表现更好。
  - 在事实性任务（factuality）上的增益普遍较小，作者也承认检索头在这类任务中的作用有限（事实回忆主要由 MLP 层承担）。
- **α 的自动熵控制仍缺乏理论最优性保障**：虽然动态熵调节优于静态 α，但并未系统论证为何条件熵是最优选择——作者亦提到可使用语义熵（semantic entropy）等更高级的不确定性量化方法作为替代。
- **对 IFEval 的某些子指标（如 Prompt-level Strict Acc）未带来改善**，甚至在部分设置下略有下降，说明该方法对指令遵循类任务支持不均衡。
- **算力需求较高**：尽管无训练成本，但需同时前向运行两个 LLM（基础 + 掩蔽），推理成本高于单模型推理。虽然论文报告了 TFLOPS 说明共享 KV Cache 的优化效果，但总显存和耗时仍是现实部署的障碍。
- **TruthfulQA Gen 评估依赖 GPT-2 davinci 模型评判**，评估成本较高且带有模型偏置风险。
- **开放环境中未讨论对故意误导性上下文的鲁棒性**：作者在伦理声明中提到该方法可能被滥用（如提供错误上下文生成看似可信的答案），但未给出具体防护方案。
- **检索头在不同架构间可能有分布差异**：虽然附录验证了 Mistral 和 Qwen2 上也有效，但如何在更大规模（如数百B）的模型上保持效能，仍需进一步验证。

---

（完）
