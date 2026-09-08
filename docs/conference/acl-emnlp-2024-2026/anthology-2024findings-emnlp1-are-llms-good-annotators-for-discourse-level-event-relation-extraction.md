---
title: Are LLMs Good Annotators for Discourse-level Event Relation Extraction?
title_zh: 大语言模型能否胜任篇章级事件关系抽取的标注任务？
authors: "Kangda Wei, Aayush Gautam, Ruihong Huang"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.1.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 面向长文档的篇章级事件关系抽取，涵盖共指、时间、因果和子事件关系
tldr: 大语言模型在许多NLP任务上表现优秀，但在篇章级事件关系抽取任务上尚未充分验证。本文针对长文档上的共指、时间、因果和子事件等复杂关系，系统评测GPT-3.5和LLaMA-2，发现其效果显著弱于监督学习基线。监督微调虽能提升LLM性能，但其提升幅度不如更小的有监督模型，说明当前的LLM不适合直接作为长文档事件关系标注工具，仍需发展结构化的文档级建模方法。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1656, \"height\": 980, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1621, \"height\": 1152, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1614, \"height\": 1042, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1662, \"height\": 1402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp1/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1662, \"height\": 1404, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 764, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 691, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 1025, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 564, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 1403, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1669, \"height\": 1051, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1645, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp1/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1637, \"height\": 546, \"label\": \"Table\"}]"
motivation: 长篇文档中的事件关系涉及共指、时间、因果等复杂类型，LLM在该任务上的性能未明。
method: 使用GPT-3.5与LLaMA-2在篇章级事件关系抽取上评测，并与有监督基线和监督微调比较。
result: LLM明显弱于监督基线，监督微调有帮助但扩展性不及小规模监督模型。
conclusion: LLM尚不宜直接替代监督模型进行篇章级事件关系抽取。
---

## Abstract
Large Language Models (LLMs) have demonstrated proficiency in a wide array of natural language processing tasks. However, its effectiveness over discourse-level event relation extraction (ERE) tasks remains unexplored. In this paper, we assess the effectiveness of LLMs in addressing discourse-level ERE tasks characterized by lengthy documents and intricate relations encompassing coreference, temporal, causal, and subevent types. Evaluation is conducted using an commercial model, GPT-3.5, and an open-source model, LLaMA-2. Our study reveals a notable underperformance of LLMs compared to the baseline established through supervised learning. Although Supervised Fine-Tuning (SFT) can improve LLMs performance, it does not scale well compared to the smaller supervised baseline model. Our quantitative and qualitative analysis shows that LLMs have several weaknesses when applied for extracting event relations, including a tendency to fabricate event mentions, and failures to capture transitivity rules among relations, detect long distance relations, or comprehend contexts with dense event mentions.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义

- **研究动机**：事件关系抽取（ERE）旨在于文本中识别并分类事件之间的共指、时间、因果和子事件等关系，对事件预测、问答和阅读理解等应用十分重要。然而，篇章级 ERE 涉及长文档和密集、复杂的跨句关系，难度较高。近年来大语言模型（LLMs）在许多 NLP 任务上表现出色，但其在篇章级 ERE 上的效果尚未被充分探索。
- **核心问题**：LLMs 是否能胜任篇章级事件关系抽取（即作为标注者）？其性能相比传统监督学习基线如何？
- **整体含义**：论文通过系统评测发现，LLMs 在篇章级 ERE 上明显弱于监督基线，即使经过监督微调也难以超越小规模监督模型，说明 LLMs 尚不适合直接作为长文档事件关系标注工具，需要进一步发展结构化的文档级建模方法。

### 2. 论文提出的方法论

- **核心思路**：在仅靠提示（prompting）和可选监督微调（SFT）两种设定下，评估 LLMs 抽取四类事件关系的能力。
- **任务设定**：给定文档，先标注出所有事件提及和 TIMEX 提及（格式为 `[x_i Event_p]` 或 `[x_i TIMEX_q]`），要求模型预测共指、时间、因果和子事件关系，并使用特定格式输出（如 `Event_1 BEFORE Event_0; SHIFT;`）。
- **提示模式**：设计了四种不同的提示模式：
  - **Bulk Prediction**：一次查询列出某一关系类型的所有关系对，1-shot 示例。
  - **Iterative Prediction**：逐句迭代，将之前预测出的关系增补到上下文中，再让模型预测新句子中提及与历史提及的关系；演示示例有两类：整篇文档（whole doc）和 n-shot（每个示例仅取原文档前两句）。
  - **Event Ranking**：逐事件（或 TIMEX）查询所有满足特定关系的前驱或后继事件，1-shot。
  - **Pairwise**：对所有事件对逐一提问，判断具体关系（或 NONE），仅在 LLaMA-2 上测试。
- **监督微调（SFT）**：将 LLaMA-2 以 pairwise 格式进行微调，使其与基线模型的分类任务格式一致；使用 LoRA、4-bit 量化，训练 3 epochs。
- **引入传递性分析**：在误差分析中，将模型预测与可传递规则推导出的关系比较，评估模型是否遵守传递性。

### 3. 实验设计

- **数据集**：MAVEN-ERE，包含 4480 篇英文 Wikipedia 文档，标注了共指、时间、因果和子事件四类关系。测试集有 857 篇文档、18908 条共指链、234844 条时间关系、11978 条因果关系和 3822 条子事件关系。模型测试使用了全部测试集（部分初步实验仅用验证集前 10 篇）。
- **模型**：
  - 商业模型：gpt-3.5-turbo-16k（snapshot gpt-3.5-turbo-0613）；GPT-4 仅作为补充在验证子集测试。
  - 开源模型：Llama-2-7b-chat-hf。
- **基线**：Wang et al. (2022) 提出的监督基线——基于 RoBERTa-base，为每个关系类型训练单独分类头，采用 pairwise 分类。
- **对比设置**：
  - 不同提示模式（Bulk / Iterative / Event Ranking / Pairwise）在验证集前 10 篇文档上的效果。
  - Iterative Prediction 的 whole-doc 与 1/2/5/10-shot 变体在完整测试集上的效果。
  - SFT：改变训练数据量（1、2、5、10、20、50、100、200 篇文档），对比 LLaMA-2 与基线模型的 F-1 曲线。
- **评价指标**：共指采用 MUC、B³、CEAF_e、BLANC；其他关系采用 Precision、Recall、F-1；总体采用四类关系的宏平均。

### 4. 资源与算力

- 文中并未说明 GPU 型号与数量，只提到使用了 Texas A&M 高性能计算资源。
- 推理耗时估计（表 1）：
  - GPT-3.5：Iterative Prediction 约 48 小时，成本约 300 美元；Event Ranking 约 600 小时，成本约 3,500 美元；Pairwise 约 3,600 小时，成本约 30,000 美元。
  - LLaMA-2（7B）：Iterative 约 36 小时；Event Ranking 约 480 小时；Pairwise 约 3,000 小时。
- SFT 耗时：用 200 篇文档微调 LLaMA-2 3 个 epoch 约需 72 小时；RoBERTa-base 基线仅需约 1 小时，差距显著。
- 完整测试集上 GPT-3.5 共跑 5 次不同的 Iterative 变体，总成本约 1,650 美元。

### 5. 实验数量与充分性

- **实验数量**：
  - 在验证集前 10 篇文档上比较了多种提示模式；
  - 在完整测试集上对 GPT-3.5 和 LLaMA-2 分别进行了 5 种 Iterative 变体的评测；
  - SFT 实验覆盖 8 档训练数据量，对四类关系分别比较；
  - 还进行了 GPT-4 在验证子集上的补充实验。
- **充分性与公平性**：
  - 优点：评测了多种主流提示策略，并在全量测试集上报告结果；SFT 与基线在相同数据量下对比，相对公平。
  - 不足：由于成本原因，Event Ranking 和 Pairwise 未在完整测试集上运行，仅在小验证集上对比；GPT-3.5/GPT-4 版本会随时间更新，结果难以精确复现；基线使用全监督、而多数 LLM 评测是 few-shot，两者直接对比本身存在“不公平”因素（作者通过 SFT 同数据量比较来缓解这一偏差）。

### 6. 论文的主要结论与发现

- LLMs 在篇章级 ERE 上显著弱于监督基线：无论共指、时间、因果、子事件，GPT-3.5 和 LLaMA-2 的 F-1 都远低于 RoBERTa 基线（例如总体宏平均约 20 vs. 51.6）。
- 增加 few-shot 示例数量对 GPT-3.5 有一定帮助，但总体仍无法达到基线；LLaMA-2 效果更差，常无法输出一致格式。
- SFT 能提升 LLaMA-2 性能，但可扩展性差：通常需要约两倍于基线的训练数据才能达到同等总体性能；仅当训练数据极少时 LLaMA-2 才能因预训练先验而略优。
- LLMs 存在三种主要弱点：
  1. **幻觉与格式不一致**：会杜撰文本中不存在的事件提及或关系，且无法稳定遵循输出格式。
  2. **不遵守传递性规则**：例如预测了 A BEFORE B 和 B BEFORE C，却不预测 A BEFORE C，甚至预测反向关系；表 3 显示加入传递推导出的关系后时间关系 F-1 可提升约 6–7%。
  3. **对长距离和密集事件上下文不敏感**：跨句关系比句内关系更难；事件距离越远，性能越差；同一句子中事件越多，性能越低。

### 7. 优点

- 系统性地覆盖了四种常用事件关系，并使用统一的 MAVEN-ERE 数据集，便于比较。
- 设计了多种提示模式并评估了不同演示数量，提供了丰富的经验数据。
- 在 SFT 实验中细致比较了不同训练数据量下 LLM 与小规模监督模型的数据效率，揭示扩展性问题。
- 定量与定性分析相结合，对错误类型（FP/FN、传递性、距离、密度）进行了有意义的统计，能指导后续研究。
- 公开了成本估计，帮助社区评估这类任务的实验可行性。

### 8. 不足与局限

- 实验成本高，限制了大量提示模式在完整测试集上的评测，例如 Event Ranking 和 Pairwise 未跑全量。
- 仅测试了一个开源模型规模（LLaMA-2 7B）；13B/70B 或许表现更好，但未覆盖。
- GPT-3.5 和 GPT-4 版本会变化，结果难以长期复现；OpenAI 模型内部细节不透明，限制了深入分析不同版本差异的原因。
- 虽然对比了多种提示，但仍可能存在更好的提示设计；零样本能力也未完全探索。
- 闭源 API 的使用本身涉及费用和地区可访问性问题，对社区复现和广泛采用构成障碍。

（完）
