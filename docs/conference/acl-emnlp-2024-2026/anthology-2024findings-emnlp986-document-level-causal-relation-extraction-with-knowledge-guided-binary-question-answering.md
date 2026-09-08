---
title: Document-level Causal Relation Extraction with Knowledge-guided Binary Question Answering
title_zh: 知识引导的文档级事件因果关系抽取
authors: "Zimu Wang, Lei Xia, Wei Wang, Xinya Du"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.986.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 文档级事件因果抽取，使用知识引导的二元问答
tldr: 文档级事件因果抽取面临缺乏篇章建模和因果幻觉两大挑战。KnowQA先构造事件结构，再以知识引导的二元问答判断事件间的因果关系，利用结构化事件信息约束大模型。在MECI和MAVEN-ERE数据集的零样本与微调实验中，该方法明显改善了文档级因果抽取的效果，为跨句事件关系抽取提供了可参考的模型范式。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp986/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp986/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp986/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp986/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp986/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 539, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp986/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 721, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp986/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1537, \"height\": 937, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp986/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 766, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp986/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 812, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp986/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 687, \"label\": \"Table\"}]"
motivation: 现有事件因果抽取缺乏文档级建模且大模型易产生无据因果联系。
method: 先构造事件结构，再以知识引导的二元问答形式让LLM对事件对进行因果判定，抑制无证据关联。
result: 在MECI与MAVEN-ERE上的零样本及微调实验均优于基线，缓解文档级因果关系建模中的幻觉问题。
conclusion: 验证了事件结构与知识引导对大模型跨句事件关系抽取的可控增强作用。
---

## Abstract
As an essential task in information extraction (IE), Event-Event Causal Relation Extraction (ECRE) aims to identify and classify the causal relationships between event mentions in natural language texts. However, existing research on ECRE has highlighted two critical challenges, including the lack of document-level modeling and causal hallucinations. In this paper, we propose a Knowledge-guided binary Question Answering (KnowQA) method with event structures for ECRE, consisting of two stages: Event Structure Construction and Binary Question Answering. We conduct extensive experiments under both zero-shot and fine-tuning settings with large language models (LLMs) on the MECI and MAVEN-ERE datasets. Experimental results demonstrate the usefulness of event structures on document-level ECRE and the effectiveness of KnowQA by achieving state-of-the-art on the MECI dataset. We observe not only the effectiveness but also the high generalizability and low inconsistency of our method, particularly when with complete event structures after fine-tuning the models.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义
- 论文针对 **事件间因果关系抽取（Event-Event Causal Relation Extraction, ECRE）** 任务，该任务旨在识别并分类文本中事件触发词之间的因果关系（如“Cause / Effect / Precondition”）。
- 现有研究存在两大挑战：
  - **缺乏文档级建模**：传统方法依赖句子级 AMR 图等语义结构，难以捕捉跨句、隐式的文档级因果信息；
  - **因果幻觉**：大型语言模型（如 GPT-3.5）在 ECRE 上易过度推测因果关系，表现为低精度、高召回。
- 论文提出将 ECRE 分解为 **事件因果识别（ECI）** 与 **因果关系统计分类（CRC）**，并利用跨任务 IE 知识构建文档级事件结构来约束和指导 LLM 推理，从而缓解上述问题。

## 2. 方法论
论文提出 **KnowQA（Knowledge-guided binary Question Answering）**，包含两个阶段：

1. **事件结构构建（Event Structure Construction）**
   - 扩展 ACE 定义，将事件结构构成为：**事件触发词、事件论元、论元的单跳关系**（例如论元与实体间的关系三元组）。
   - 不使用 LLM 完成该步骤，而是采用 PLM 工具：
     - 事件检测：CLEVE 在 WikiEvents 上训练，采用 KAIROS 本体；
     - 事件论元抽取：BART-Gen 生成式模型；
     - 实体与关系联合抽取：JEREX（预训练于 DocRED）。
   - 将抽取结果匹配后形成文档级事件结构。

2. **二元问答应答（Binary Question Answering）**
   - 把 ECRE 建模为“输入+事件结构+问题+答案”的二元 QA 形式：
     - **单轮问答**：只问“Is there a causal relationship between ...?”，用于因果识别；
     - **多轮问答**：将具体关系的措辞（如“caused by / preconditioned by”）嵌入问题，在两个方向上迭代询问，既识别又分类因果关系。
   - 这样的 QA 设计可显式注入关系类型与事件结构，帮助模型对齐 schema。

## 3. 实验设计
- **数据集**：
  - **MECI**（英文子集）：标注 Cause / Effect 关系，文档 438 篇；
  - **MAVEN-ERE**：抽样后使用，标注 Cause / Precondition 关系，文档 4480 篇（实际上表1显示4480，文中采样子集）。
- **场景设置**：
  - **Zero-shot**：GPT-3.5 和 Flan-T5 XL 直接推理；
  - **Fine-tuning**：Flan-T5 Large 在训练集上微调后评估。
- **评测任务**：事件因果识别（ECI）与因果关系统计分类（CRC），均报告 Precision / Recall / F1。
- **基线模型**：PLM、Know、RichGCN、ERGO、DiffusECI、HOTECI、GIMC 等 PLM 或图网络方案（采用 XLM-RoBERTa 的复现/原实现）。
- **消融/分析实验**：
  - 事件结构完整性：无结构 vs. 有论元 vs. 有论元+关系；
  - 单轮 vs. 多轮 QA；
  - 句子内（Intra）与句子间（Inter）性能；
  - Case study；
  - 不同因果表达形式的影响；
  - 不一致性（inconsistency）评估。

## 4. 资源与算力
- 论文仅在实验设置中明确说明：“The main experiments were conducted on a single GeForce RTX 3090 graphic card”。
- 没有报告训练时长、GPU 数量、参数量细节或总计算量。GPT-3.5 使用 API，温度设为 0，但未说明调用开销。

## 5. 实验数量与充分性
- 实验覆盖两个数据集、两种设置（zero-shot 和 fine-tuning），并包含多组消融和分析实验，数量较丰富：
  - 零样本：GPT-3.5、Flan-T5 XL × MECI + MAVEN-ERE，每个模型有 Single-turn / Multi-turn 及事件结构三类变体；
  - 微调：Flan-T5 Large 在 MECI 上对比多种基线；
  - 附加实验：跨句分析、case study、因果表达鲁棒性、不一致性检验。
- 充分性评价：
  - **优点**：比较了较新的多种基线；同时做零样本与微调；不只报总体 F1，还报告 Precision/Recall 来分析幻觉问题；分析“不一致性”保证了多轮 QA 的可靠性。
  - **不足**：微调实验只在 MECI 上验证，未在 MAVEN-ERE 上微调；只测试了两种模型（GPT-3.5 和 Flan-T5），未覆盖 Llama/Mistral 等；事件结构来自自动模型而非金标，可能引入误差（论文将在 Limitations 中承认）。总体而言实验设计和分析较全面，但在跨数据集泛化和模型覆盖面方面存在一定局限。

## 6. 论文的主要结论与发现
- **KnowQA 有效性**：微调后的 Flan-T5 Large 在 MECI 上超过所有基线，达到 SOTA；零样本下事件结构也能明显提升效果。
- **事件结构的作用**：
  - 尤其是**文档级、跨句因果关系**上受益显著：融入事件结构后，inter-sentence F1 大幅提升，缩小了与 intra-sentence 的差距。
  - 能够帮助识别隐式因果关系（无显式因果连接词时）并纠正误判。
- **单轮 vs 多轮策略**：
  - 零样本下多轮 QA 更有效，可缓解因果幻觉（降低召回、提高精度）；
  - 微调后单轮 QA 更适合 ECI（因果识别），多轮 QA 更适合 CRC（因果分类）；
  - 模型微调后 Precision 与 Recall 差距显著减小，说明幻觉问题可被缓解。
- **泛化性与一致性**：
  - 换用不同因果表达（如 “cause”、“a cause of”）时性能仍稳定，说明方法具有高泛化性；
  - 多轮问答的不一致性在加入事件结构和微调后大幅降低（如 Flan-T5 Large + 完整事件结构的不一致率仅 1.0），体现了因果方向分类的可靠性。

## 7. 优点
- 将文档级事件结构（触发词 + 论元 + 论元之间的关系）引入 ECRE 的模型提示，有效补充了单一事件对无法体现的上下文知识。
- 利用“二元问答”将 ECRE 的不同子任务（识别和分类）统一到同一个范式，并通过“多轮问答”显式加入关系类型作为监督，思路简洁而新颖。
- 实验设计注重解决真实痛点，对 LLM 的“因果幻觉”进行 Precision/Recall 分析，不只以 F1 论优劣。
- 提出“不一致性”指标来考察多次提问顺序是否会扰动 LLM 决策，并系统对比不同事件结构配置，分析细致。
- 代码开源，促进复现和后续研究。

## 8. 不足与局限
- **事件结构非金标**：事件检测、论元抽取和关系抽取均由上游 IE 模型自动生成，其错误会传播到 ECRE，影响最终效果。
- **模型覆盖范围有限**：仅尝试 GPT-3.5 和 Flan-T5 两个模型，未评估 Llama、Mistral 等其他主流 LLM，也未在更多语言上测试。
- **语言与数据集覆盖有限**：只在英语数据上做细粒度实验；MAVEN-ERE 缺少事件论元关系抽取的模型输出，实验中直接使用黄金论元注释，可能带来指标偏高或不公平比较。
- **微调实验不够全面**：微调只在 MECI 上进行，未在 MAVEN-ERE 上验证；不同数据集上的结论可能不一致。
- **潜在偏差**：论文提到语言报道偏差会导致“因果幻觉”，但未对事件类型分布、语言变体进行深入分析；自动抽取的事件结构可能与 LLM 原有的内部知识产生冲突（尽管实验表明帮助更大）。
- **计算细节不透明**：未报告完整的超参数搜索过程、训练收敛时间以及资源消耗，可复现细节有待完善。

（完）
