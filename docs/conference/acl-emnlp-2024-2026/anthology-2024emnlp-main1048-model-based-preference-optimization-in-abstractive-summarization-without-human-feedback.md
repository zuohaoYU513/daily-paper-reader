---
title: Model-based Preference Optimization in Abstractive Summarization without Human Feedback
title_zh: 无人工反馈的抽象摘要中基于模型的偏好优化
authors: "Jaepill Choi, Kyubyung Chae, Jiwoo Song, Yohan Jo, Taesup Kim"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.1048.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 无人工反馈的偏好优化方法，缓解抽象摘要中的幻觉
tldr: 该文指出监督微调难以稳定提升摘要忠实度，而依赖人工反馈的偏好优化成本高昂。为此提出无人工反馈的基于模型偏好优化方法，利用模型自身构造偏好信号，减少生成源文档中不存在的内容。实验表明该方法能有效降低摘要幻觉并提升事实一致性，为偏好优化在忠实摘要中的低成本应用提供了方案。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1048/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 593, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1048/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1048/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1048/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1048/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 820, \"height\": 524, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 729, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 922, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 732, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 805, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 803, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 804, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 491, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1569, \"height\": 898, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1048/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1580, \"height\": 791, \"label\": \"Table\"}]"
motivation: 抽象摘要中LLM易生成源文不存在的幻觉内容，监督微调效果有限且人工偏好反馈成本过高。
method: 提出基于模型的偏好优化方法，不依赖人类反馈即可生成偏好信号并优化摘要模型。
result: 在摘要任务中有效减少幻觉内容，提升生成摘要的事实一致性。
conclusion: 该方法为低成本的偏好优化提升摘要忠实度提供了可行路径。
---

## Abstract
In abstractive summarization, the challenge of producing concise and accurate summaries arises from the vast amount of information contained in the source document. Consequently, although Large Language Models (LLMs) can generate fluent text, they often introduce inaccuracies by hallucinating content not found in the original source. While supervised fine-tuning methods that maximize likelihood contribute to this issue, they do not consistently enhance the faithfulness of the summaries. Preference-based optimization methods, such as Direct Preference Optimization (DPO), can further refine the model to align with human preferences. However, these methods still heavily depend on costly human feedback. In this work, we introduce a novel and straightforward approach called Model-based Preference Optimization (MPO) to fine-tune LLMs for improved summarization abilities without any human feedback. By leveraging the model’s inherent summarization capabilities, we create a preference dataset that is fully generated by the model using different decoding strategies. Our experiments on standard summarization datasets and various metrics demonstrate that our proposed MPO significantly enhances the quality of generated summaries without relying on human feedback. The code is publicly available at https://github.com/cjaep/MPO .

---

## 论文详细总结（自动生成）

## 论文结构化中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：在抽象式摘要任务中，大型语言模型（LLMs）虽然能生成流畅文本，但经常产生**幻觉内容（hallucination）**，即生成源文档中不存在或不一致的信息。
- **现有方案的不足**：
  - **监督微调（SFT）**以最大似然为目标，无法持续提升摘要的忠实度（faithfulness）；
  - **RLHF/DPO 等基于人类偏好的优化方法**效果好，但**严重依赖昂贵的人工反馈**；
  - 人工偏好并不可靠——Hosking et al. (2024) 发现人类偏好常常忽视事实一致性与忠实度；
  - 无人工反馈的既有方法多依赖外部指标（如 ROUGE、FactScore）或复杂过滤流程，这存在**过拟合于不完美指标**的风险（Goodhart’s Law）。
- **整体含义**：作者提出一种**完全不需要人工反馈和外部评估指标**的模型偏好优化方法，用于减少摘要幻觉、提升事实一致性，为低成本偏好优化提供了新路径。

---

### 2. 方法论：Model-based Preference Optimization (MPO)

#### 2.1 核心思想
利用**确定性解码（deterministic decoding）与随机解码（stochastic decoding）生成质量的固有差异**，由模型自身构造偏好数据集，无需外部知识、指标或人工标注。

#### 2.2 两阶段流程

**阶段一：监督微调（SFT）**
- 在训练集上对预训练语言模型进行监督微调，采用 QLoRA 高效微调；
- 直接使用已有 SFT 模型或对现有预训练模型进行适配。

**阶段二：基于模型的偏好优化（MPO）**
- 在验证集上，为每个源文档生成两个摘要：
  - **Chosen 样本**（偏好样本）：通过**确定性解码**（beam search）得到——生成的摘要更忠实于源文档；
  - **Rejected 样本**（拒绝样本）：通过**随机解码**（带温度系数的采样）得到——更易产生与源文档无关或幻觉性的内容；
- 偏好对形式为 \((x_i, y_w^{beam}, y_l^{temp})\)；
- 使用 **DPO（Direct Preference Optimization）** 损失优化模型。

#### 2.3 DPO 优化目标（文字说明）
- 使用 Bradley-Terry 模型对偏好对进行建模；
- DPO 损失函数通过对比 chosen 与 rejected 样本在策略模型与参考模型上的对数概率差来优化策略，无需显式训练奖励模型；
- 超参数 β 控制奖励与参考策略间的权衡，训练时冻结参考模型 SFT。

---

### 3. 实验设计

#### 3.1 数据集
| 数据集 | 内容 | 规模 |
|---|---|---|
| **TL;DR** | Reddit 帖文与其 TL;DR 摘要 | 训练 117k / 验证 6.45k / 测试 6.55k |
| **XSUM** | BBC 文章与其单句摘要 | 训练 204k / 验证 11.3k / 测试 11.3k |

#### 3.2 模型与架构
- **Decoder-only 模型**：GPT-J (6B)、Mistral-7B、LLaMA2-7B；
- **Encoder-decoder 模型**：BART；
- 训练采用：GPT-J 使用预训练好的 SFT checkpoint（HuggingFace CarperAI/openai_summarize_tldr_sft）；LLaMA2/Mistral 使用 QLoRA 在目标数据集上微调。

#### 3.3 评估指标（三类四指标）
- **忠实度（Faithfulness）**：AlignScore、FactCC；
- **相关性（Relevance）**：BARTScore、BS-FACT；
- **相似性（Similarity）**：ROUGE-L。

#### 3.4 对比方法
- **基于真值数据的基线**：SFT（训练集微调）、SFT++（额外在验证集上继续微调）；
- **基于人类偏好的基线**：PPO、DPO（使用 Stiennon et al. (2020) 人类偏好数据集）；
- **无人工反馈对照**：Preferred-FT（只用 MPO 的 chosen 样本做似然最大化的微调）；
- **其他解码策略基线**：Nucleus、ITI、DoLa、Faithfulness-aware Lookahead；
- 评估时均使用 beam search 与 greedy 两种生成方式。

#### 3.5 实现细节
- SFT：QLoRA，batch size=2，lr=1e-4，1 epoch；
- 偏好优化：β=0.5，lr=1e-4，batch size=4，1 epoch，beam size=6，温度 5.0（GPT-J）/ 1.0（LLaMA2、Mistral）。

---

### 4. 资源与算力

论文在附录 A.7 中有明确说明：

- **GPU**：NVIDIA RTX 6000（48GB）和 RTX 3090（24GB），每个实验分配单块 GPU；
- **模型偏好优化**：平均约 1.5 小时/次；
- **摘要生成（解码）耗时**：
  - GPT-J (6B)：beam search 约 20 小时；greedy 约 5.5 小时；
  - Mistral-7B & LLaMA2-7B：beam search 约 5 小时；greedy 约 1.5 小时；
- 所有实验**单次运行**，固定随机种子为 42。

---

### 5. 实验数量与充分性评估

#### 实验数量（较丰富）
论文包含以下主要实验：

1. **主实验**：GPT-J 在 TL;DR 上的完整对比（SFT、SFT++、Preferred-FT、PPO、DPO、MPO），beam & greedy 两种解码；
2. **跨模型跨数据集泛化实验**：GPT-J、Mistral、LLaMA2 在 TL;DR 与 XSUM 上的对齐结果；
3. **GPT-3.5 胜率评估**（TL;DR 上与 SFT、DPO 对比）；**人工评估**（100 个 TL;DR 样本，分组 A/B）——多角度交叉验证，可信度较高；
4. **解码策略兼容性测试**：LLaMA2 上对 Greedy、Nucleus、ITI、DoLa、Beam 多种解码的对比；
5. **偏好对消融实验**：不同 chosen/rejected 组合的影响及相似度分析；
6. **迭代训练分析**：3 轮迭代，动态调节温度，结合 MINT 和 extractive fragment coverage 分析忠实度-抽象性权衡；
7. **Encoder-decoder 架构验证**：BART 在 XSUM 上测试，包括 Lookahead 解码作为 chosen 样本的 MPO* 变体；
8. **质量验证**：对 chosen/rejected 样本本身的质量评估及多项 ROUGE 对比。

#### 结论
- **总体充分性较好**：覆盖多种模型、数据集、解码方式、架构类型和公平对比，并同时使用自动化指标、GPT-3.5 评估和人类评估多重验证。
- **存在的不足**：
  - 主结果均基于单次运行，未提供显著性检验的详细误差条讨论；
  - 人类评估仅涉及 100 个样本、一个数据集，规模有限；
  - GPT-3.5 胜率评估中 MPO 表现不稳定，作者也承认 MPO 在流畅性等方面可能不如 DPO；某些对比（如 DPO）使用的偏好数据更多，存在对比不对称性；
  - 自动评估结果中不同指标间的相对提升幅度并不一致。

---

### 6. 主要结论与发现

1. **MPO 显著优于监督微调**：在 TL;DR 上比 SFT 在 AlignScore、FactCC、BARTScore、BS-FACT 上均有明显提升，能有效降低幻觉；
2. **MPO 优于基于人类偏好的优化方法**：在忠实度与源相关性上胜过 PPO 与 DPO（即本实验中 AlignScore/FactCC 更高）；对比人类偏好数据中的不准确之处，MPO 不依赖人类偏好也能获得更高事实一致性；
3. **MPO 具备较好的泛化性能**：在 GPT-J、Mistral、LLaMA2 和 BART 等多种模型及 TL;DR、XSUM 两个数据集上普遍生效；
4. **MPO 对多种解码策略兼容**：模型经过偏好对齐后，忠实度均得到提升，并可结合 ITI、DoLa 等忠实度感知解码策略获得进一步增强；
5. **偏好对选择的正确组合至关重要**：beam search 作为 chosen、温度采样作为 rejected 的搭配效果最佳；若 chosen/rejected 太相似（如 greedy vs. beam）会导致性能退化；
6. **迭代训练会带来忠实度-抽象性权衡问题**：多次迭代后模型输出日趋抽取式，直接复制源文本，导致模型的创造性/抽象性下降；
7. **偏好信号可进一步替换为更优解码策略**：用 Lookahead 替代 beam search 生成 chosen 样本后，忠实度（AlignScore）进一步提升。

---

### 7. 优点

- **方法简洁且高效**：无需任何人工反馈、外部指标或额外过滤，利用模型自身在不同解码策略下的输出差异构造偏好对；
- **训练成本低**：QLoRA + DPO 方式显著降低资源需求、与 RL 相比的采样训练开销更小；
- **实践性强**：不依赖昂贵的人类标注，数据生成可扩展，对受限学术环境友好；
- **对“偏好污染”免疫**：能规避人工偏好中忽略事实一致性的问题（相对体现于忠实度指标上过 PPO/DPO 的结果）；
- **实验设计系统**：在多个维度和多种设置上进行验证（不同语言模型、不同架构、多数据集、不同解码策略、偏好组合消融、迭代训练、自动与人工评估）；
- **评估体系设计合理**：采用忠实度、相关性、相似性三分类评估框架，并验证了 AlignScore 与人类判断的一致性；
- **开源代码**，保证可复现性，并在附录中提供详细资源许可证信息。

---

### 8. 不足与局限

以下内容论文自身 “Limitation” 中提到了部分，也包含分析中观察到的不足：

1. **QLoRA 的使用限制了效果上限**：只使用 QLoRA 而非全参数微调，缺少对比实验验证其对性能的真实影响；模型规模限制在 7B 以内，未在更大模型上验证可扩展性；
2. **迭代训练导致摘要日趋抽取式**：模型倾向直接复写源句，与“抽象式”摘要目标冲突，可能最终退化为抽取式摘要；
3. **解码策略差异带来的偏好并非绝对正确**：该研究依赖“确定性解码结果优于随机解码”的假设，该假设在实验中有条件适用条件，并非普遍成立；
4. **GPT-3.5 胜率与人工评估中表现并非压倒性**：MPO 与 DPO 整体胜率约 51%，信服力较弱；两个模型的胜率对比结果高度受解码方式选择影响，稳定性存在疑问；
5. **伦理风险**：TL;DR 来自 Reddit 帖子，可能含有偏见或冒犯性内容，模型自我生成的反馈可能放大既有社会偏见；且随着模型日益倾向抽取式输出，对源文本中偏见的“过滤/改写”能力可能被削弱；
6. **实验细节不足**：大部分实验结果基于单次运行（固定 seed 42），缺少多次运行结果的误差线或显著性分析（对 DPO 做了 T-test，但全面分析不足）；实验比较在偏好对数量与质量和处理细节上存在不公平性（人类偏好数据量大于 MPO 的一对一构造），实际差异可能是量的差异而非质的差异；人类评估规模有限（仅 100 个样本、10 位标注者、单一数据集）。

---

（完）
