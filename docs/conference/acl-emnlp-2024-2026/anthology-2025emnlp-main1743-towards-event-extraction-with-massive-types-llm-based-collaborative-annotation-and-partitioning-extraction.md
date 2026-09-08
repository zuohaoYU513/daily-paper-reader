---
title: "Towards Event Extraction with Massive Types: LLM-based Collaborative Annotation and Partitioning Extraction"
title_zh: 面向海量类型的事件抽取：基于LLM的协同标注与分区抽取
authors: "Wenxuan Liu, Zixuan Li, Long Bai, Yuxin Zuo, Daozhu Xu, Xiaolong Jin, Jiafeng Guo (嘉丰 郭), Xueqi Cheng (程学旗)"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1743.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 海量类型事件抽取与触发词/论元标注框架，可迁移至长文档事件抽取
tldr: 通用事件抽取需要支持海量事件类型，但缺少高效的标注框架和数据集构建手段。本文提出多LLM协商投票的协同标注方法，精化远监督触发词并完成论元标注，再配合分区抽取以应对巨大类型空间。由此构建迄今最大事件抽取数据集EEMT，含20余万样本、3465种事件类型和6297种角色类型。人工标注测试集上的评测验证了该方案在大规模事件抽取中的可行性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 670, \"height\": 642, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1558, \"height\": 789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 681, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 600, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1389, \"height\": 1790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1743/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1461, \"height\": 1282, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1473, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 754, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1377, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1447, \"height\": 669, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 601, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 701, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 565, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 814, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 658, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 585, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1684, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1743/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 782, \"height\": 202, \"label\": \"Table\"}]"
motivation: 事件抽取要覆盖海量事件类型时缺乏高效标注框架与大规模数据集支持，是长期存在的关键瓶颈。
method: 提出多LLM协作并投票的标注流程，先精化远程监督得到的触发词，再完成论元标注，并采用分区抽取处理海量类型。
result: 构建了迄今最大事件抽取数据集EEMT，含超过20万样本、3465种事件类型和6297种角色类型，人工标注测试集证明其有效性。
conclusion: 展示了LLM协同标注与分区抽取能够支撑大规模多类型事件抽取体系，为通用事件抽取提供方法积累与数据基础。
---

## Abstract
Developing a general-purpose system that can extract events with massive types is a long-standing target in Event Extraction (EE). In doing so, the basic challenge comes from the absence of an efficient and effective annotation framework to construct the corresponding datasets. In this paper, we propose an LLM-based collaborative annotation framework. Through collaboration among multiple LLMs and a subsequent voting process, it refines annotations of triggers from distant supervision and then carries out argument annotation. Finally, we create EEMT, the largest EE dataset to date, featuring over **200,000** samples, **3,465** event types, and **6,297** role types. Evaluation on human-annotated test set demonstrates that the proposed framework achieves the F1 scores of **90.1%** and **85.3%** for event detection and argument extraction, strongly validating its effectiveness. Besides, to alleviate the excessively long prompts caused by massive types, we propose an LLM-based Partitioning method for EE called LLM-PEE. It first recalls candidate event types and then splits them into multiple partitions for LLMs to extract. After fine-tuning on the EEMT training set, the distilled LLM-PEE with 7B parameters outperforms state-of-the-art methods by **5.4%** and **6.1%** in event detection and argument extraction. Besides, it also surpasses mainstream LLMs by **12.9%** on the unseen datasets, which strongly demonstrates the event diversity of the EEMT dataset and the generalization capabilities of the LLM-PEE method.

---

## 论文详细总结（自动生成）

## 一、核心问题与研究动机

- **研究背景**：事件抽取（EE）是 NLP 中长期关注的任务，通常分为事件触发词/类型识别（Event Detection, ED）和事件论元/角色抽取（Event Argument Extraction, EAE）两个子任务。
- **核心挑战**：要实现覆盖海量事件类型的通用事件抽取系统，最大瓶颈是**缺乏高效且有效的标注框架**来构建对应数据集。
- **现有方法的不足**：
  - **人工标注**（如 ACE 2005、MAVEN-arg）：质量高但效率低、成本大，难以扩展事件类型和数据规模；
  - **远监督标注**（如 GLEN）：效率高但存在三类噪声——不合理触发词标注（如将副词 "voluntarily" 标为触发词）、粗粒度类型标注（层次化类型无法精确定位到细粒度义项）、以及论元标注缺失（知识库无法穷举所有可能论元）。
- **核心目标**：构建一个能够支撑海量类型（thousands of types）事件抽取的高质量数据集与高效抽取方法。

---

## 二、方法论：核心思想与关键技术细节

本文提出了两个互相衔接的核心方法：

### 1）基于 LLM 的协同标注框架（LLM-based Collaborative Annotation Framework）

在远监督生成的初步标注基础上，利用多个 LLM 协作＋投票机制，进行四阶段流水线优化：

1. **事件触发词预标注**：沿用 GLEN 的远监督方法，基于 Propbank + Wikidata（DWD Overlay）生成初始触发词及其候选事件类型。
2. **事件触发词过滤**：利用多个 LLM 判断远监督标注的触发词是否符合事件定义，过滤掉不合理的标注；采用**多数投票**收敛最终结果；若平票则重复投票直至多数。
3. **事件类型精化**：将多义词触发词对应的多个候选类型整理为多项选择题，令各 LLM 挑选最符合上下文语境的细粒度类型；同样采用投票策略，加入“以上皆非”选项处理无匹配情况。
4. **事件论元标注**：基于精化后的事件类型及其 schema，LLM 负责识别句中对应各角色（role）的文本片段。为提升一致性引入两个关键机制：
   - **规则引导**：在提示中注入人工总结的论元标注规则（逻辑一致性、简洁性、重叠消解等）；
   - **偏移对齐**：由于不同 LLM 输出的 span 起止存在系统性偏差，先令每个模型依据规则修正自己的标注结果，再经多模型投票确定最终论元；对分歧极大的案例，由 GPT-4o 重新标注。

### 2）基于 LLM 的分区抽取方法 LLM-PEE

用于解决将海量类型放进单个提示词会导致**提示过长**的问题：

- **流程**：输入句子 → 相似度召回 → 类型分区 → LLM 分区内抽取 → 汇总预测结果。
- **相似度类型召回**：用 ColBERT 将句子和候选事件类型编码，计算相似度并取 top-k 候选事件类型。
- **类型分区提示**：将候选事件类型划分为若干分区，每一分区分别组装提示词。文中提出三种分区策略：
  - **Random**：随机均匀划分；
  - **Average**：使每个分区内的置信度之和尽量均衡；
  - **Level**：按置信度排序后分成难易不同的组。
  实验表明 **Level** 策略最优，因为它将易混淆的相似事件类型放入同一分区，有助于模型学习细粒度判别。
- **基于 LLM 的事件抽取**：采用与 KnowCoder 一致的两阶段抽取流程，先做事件检测（ED），再基于已知触发词与类型做论元抽取（EAE）。

### 构建的数据集 EEMT

- 在 GLEN 基础上重新标注，包含 **20.8 万**样本、**3,465** 种事件类型、**6,297** 种角色类型；
- 训练/开发/测试沿用 GLEN 的 90/5/5 划分，并额外标注了 **1,500 条**人工测试集。

---

## 三、实验设计

### 数据集与 Benchmark

- **EEMT**（主数据集）：LLM 自动标注的训练/开发/测试集 + 1,500 条人类标注测试集；
- **ACE 2005**：用于零样本泛化评估和额外监督评估；
- 标注 LLM 选用三个主流模型：**DeepSeek-V3**、**Qwen-Plus**、**GPT-4o-mini**。

### 评估指标

- ED：Trigger Identification (TI) F1、Trigger Classification (TC) F1；
- EAE：Argument Identification (AI) F1、Argument Classification (AC) F1。

### 对比方法（Baselines）

- **分类方法**：DMBERT、Token-Level、Span-Level、CDEAR（面向海量类型 ED）；
- **EAE 分类/生成方法**：CRF-Tagging、Tag-Prime、Bart-Gen；
- **LLM 方法**：InstructUIE、IEPILE、KnowCoder（均在 EEMT 上微调，7B 级）；另评测 Qwen-Plus、GPT-4o-mini、DeepSeek-V3、GPT-4o、Gemini-2.0-flash、Qwen-Max、LLaMA-3.1-405B 等主流 LLM。

---

## 四、资源与算力

- 论文明确提到：三个标注 LLM 均通过 **Web API 服务**调用，总标注成本约 **500 美元**；温度设为 0.5。
- **未明确说明**微调 LLM-PEE 时所用 GPU 型号、数量及具体训练时长，仅在实现细节中给出：LoRA rank=8、最大序列长度 2048、batch size 256、训练 4 epochs、推理用 vLLM + greedy search，主干为 LLaMA2-7B-Base。
- 这是一个值得注意的透明度缺口——读者无法准确估算训练资源的实际需求。

---

## 五、实验数量与充分性

本文实验数量较多，覆盖面较广：

1. **主实验（表 3、4）**：LLM 标注测试集与人工标注测试集上，对 10+ 种方法的 ED/EAE 性能对比；
2. **标注质量评估（表 2）**：三个标注步骤（触发词过滤、类型精化、论元标注）分别对比单 LLM 与协同框架的 F1；
3. **消融实验（表 3 底部）**：去除类型召回 / 去除分区提示的 ED 性能；
4. **零样本评估（表 5）**：ACE 2005 上对比 7B 蒸馏模型与主流商用 LLM；
5. **与 GLEN 语料对比（表 6）**：同一 LLM-PEE 分别在 GLEN 和 EEMT 上训练的效果；
6. **分区策略对比（表 7）**：Random / Average / Level 三种策略；
7. **主干泛化实验（表 8）**：不同规模（0.5B ~ 7B）与不同系列（LLaMA、Qwen）的主干；
8. **主流 LLM 评测（表 9）**：GPT-4o、Gemini-2.0-flash、LLaMA-3.1-405B 等无微调直接在人工测试集上的效果；
9. **案例分析（表 10）**：展示 GLEN 与 EEMT 上细粒度类型预测差异；
10. **ACE 2005 监督实验（表 11）**：验证方法在小类型数据集上的普遍适用性。

整体上，实验覆盖了监督/零样本、ED/EAE、多主干、多数据源、消融与案例，设计是较系统和充分的。但在公平性上存在以下偏差点：

- 主流 LLM baseline（如表 9）以零样本/少样本方式评估，而 LLM-PEE 经过了 EEMT 全量微调，本质上两类方法处于不同数据条件，虽然作者在正文中试图说明这种对比的合理性，但仍需谨慎看待；
- 在 EAE 评估中未给各 LLM 加偏移对齐，而协同标注框架中用了偏移对齐，单 LLM 性能可能被低估；
- 表 3 部分 Token-Level/Span-Level 方法的 TC 数值（"62.0"）疑似排印错误（与 F1=39.5 不一致），但不影响整体结论。

---

## 六、主要结论与发现

1. **协同标注框架是有效的**：在人工标注测试集上，事件检测（ED）F1 达到 **90.1%**，论元抽取（EAE）F1 达到 **85.3%**，说明该框架生成的数据与人类标注高度一致。
2. **多人协同 + 投票优于任意单一 LLM**：各标注阶段中，协同框架的 F1 均显著高于使用任一单 LLM 标注的结果，证明了投票与偏移对齐机制的价值。
3. **LLM-PEE 在大规模监督场景下表现突出**：7B 参数模型在 ED 上比最优 SOTA（KnowCoder）TC 提升 5.4%，在 EAE 上 AC 提升 6.1%。
4. **分区抽取能缓解长提示问题**：去除类型召回使 TC 下降 18.3%，去除分区策略使 TC 下降 5.1%，验证了两者的必要性。
5. **EEMT 数据具有较强泛化性**：在不经任何微调的情况下，LLM-PEE 在 ACE 2005 上比 DeepSeek-V3 等大模型平均提升 **12.9%**，说明数据具有跨数据集的事件语义迁移能力。
6. **LLM 直接做 EE 的瓶颈**：在无微调情况下，主流 LLM（包括超大模型）在 EEMT 上的 ED/EAE 性能整体偏低，且“高召回低精确”的过度生成问题严重。

---

## 七、优点

- **方法论创新性强**：将远监督的低成本与 LLM 的语义理解能力结合，构建出“粗标注 → 过滤 → 精化 → 补齐论元”的递进式标注流水线，兼顾了效率与质量。
- **数据规模与类型覆盖度领先**：EEMT 无论是事件类型数、角色类型数还是数据量，都远超此前的数据集，有力弥补了领域空白。
- **消融设计完整**：对标注框架（单 LLM vs 协同）、抽取框架（去召回/去分区）均做了干净的对照实验，因果归因清晰。
- **关注偏差控制**：同时提供 LLM 标注测试集和人工标注测试集，既反映大规模数据上的相对性能，又能保证无偏评估；另在 Zero-shot 条件下进行泛化检验。
- **开源友好**：标注成本低（约 500 美元），模型采用 7B 开源主干，整体复现门槛相对较低。
- **实际价值高**：论文验证了 LLM 自动标注数据可以用来训练出在零样本场景下超越大模型的小型开源模型，这对资源受限的工业应用具有参考意义。

---

## 八、不足与局限

- **事件层级结构处理不足**（作者自述）：类型层次（大类 → 细类）未充分建模，限制了对细粒度/层次化事件的理解。
- **非端到端抽取**（作者自述）：LLM-PEE 仍拆为 ED 和 EAE 两个子任务，尚未实现真正端到端的事件抽取。
- **局限于句子级标注**（作者自述）：EEMT 只覆盖句子级事件；文档级应用中需将文档切分为句，会损失跨句事件关联。
- **潜在的 LLM 系统性偏差**：尽管测试结果验证了与人类高度一致性，但三个标注 LLM 的文化与语义偏好仍可能留下隐性偏差，而人工测试集仅 1,500 条，难以保证全面覆盖。
- **零样本对比的公平性问题**：用于对比的商用 LLM 未经微调，而 LLM-PEE 在 EEMT 上经过监督训练；虽然作者解释该设置意图是检验数据增强泛化能力，但直接称之为“超越”需谨慎解读。
- **资源信息不透明**：未说明具体 GPU 型号与数量、训练时间、API 调用次数等，复现难度增加。
- **对罕见类型效果未知**：3,465 种事件类型的长尾分布严重（如案例中某些类型仅有 4-5 条样本），模型对低频类型能否稳定抽取，论文未做专门的分析。

---

（完）
