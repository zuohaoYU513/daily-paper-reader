---
title: "LegalCore: A Dataset for Event Coreference Resolution in Legal Documents"
title_zh: LegalCore：法律文档中的事件共指消解数据集
authors: "Kangda Wei, Xi Shi, Jonathan Tong, Sai Ramana Reddy, Anandhavelu Natarajan, Rajiv Jain, Aparna Garimella, Ruihong Huang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1284.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 首个法律事件共指数据集，在约2.5万词的长合同中标注事件提及与超长距离共指链
tldr: 已有事件共指研究多集中于新闻语料，法律长文档中的事件共指缺少标注与评测。本文发布LegalCore，对平均约2.5万词的法律合同进行事件提及和共指关系统计与标注，揭示法律文档事件密度高、共指链可跨越很长的文本距离。进一步用主流大语言模型构建基线评测，显示现有模型难以胜任这类长距离事件共指任务。该数据集为长文档与法律场景的事件抽取和共指研究提供重要资源。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1284/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1284/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1284/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1284/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1284/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 739, \"height\": 505, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 556, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 822, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 779, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1661, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 809, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 735, \"height\": 769, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 813, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1659, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 818, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1518, \"height\": 1619, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1646, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1284/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1638, \"height\": 543, \"label\": \"Table\"}]"
motivation: 事件共指研究多局限于新闻文章，法律合同中密集且跨远距离的事件共指缺少数据与评测。
method: 人工标注首个法律事件共指数据集LegalCore，标注合同事件提及和共指链，并评测大语言模型的事件共指能力。
result: 数据平均每篇约2.5万词，事件提及密集且包含大量超长距离共指链，主流LLM在此设置下面临挑战。
conclusion: 提供法律长文档事件共指首个资源与基线，为跨段落和超长距离事件链接方法研究奠定基础。
---

## Abstract
Recognizing events and their coreferential mentions in a document is essential for understanding semantic meanings of text. The existing research on event coreference resolution is mostly limited to news articles. In this paper, we present the first dataset for the legal domain, LegalCore, which has been annotated with comprehensive event and event coreference information. The legal contract documents we annotated in this dataset are several times longer than news articles, with an average length of around 25k tokens per document. The annotations show that legal documents have dense event mentions and feature both short-distance and super long-distance coreference links between event mentions. We further benchmark mainstream Large Language Models (LLMs) on this dataset for both event detection and event coreference resolution tasks, and find that this dataset poses significant challenges for state-of-the-art open-source and proprietary LLMs, which perform significantly worse than a supervised baseline. We will publish the dataset as well as the code.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义（研究动机与背景）

- **研究动机**：事件识别及其共指消解是文本语义理解的关键环节，而现有事件共指数据集几乎全部集中于新闻领域（如 ACE 2005、ECB+、TAC KBP、MAVEN-ERE 等）。即便存在少数面向 Twitter、文学作品和生物医学文本的语料，也通常只标注事件提及而缺少共指关系。
- **背景缺口**：法律合同平均长度远超新闻文章（约 2.5 万 token/篇），且文档结构化为“引言 + 编号条款”，事件会跨条款反复引用，构成密集、长距离的共指网络。该领域缺少带有事件共指标注的数据资源。
- **整体含义**：本文旨在为法律领域提供首个人工标注的事件与事件共指数据集 **LegalCore**，以推动事件共指研究向长文档、真实法律场景延伸，并验证主流大语言模型在此类任务上的能力边界。

## 论文提出的方法论：核心思想、关键技术细节与流程

- **总体设计**：借鉴 RED 语料的标注准则，设计了 **“事件提及标注 → 局部共指标注 → 非局部（跨节）共指标注”** 的三阶段流水线，如图 2 所示。
- **第一阶段：事件提及标注**
  - **事件定义**：遵循 O'Gorman et al. (2016) 的定义，将*任何值得放在时间线上的发生、动作、过程或状态*视为事件，句法上可为动词、名词化形式、名词或形容词，不预设事件类型。
  - 两名标注者依据语义判断（是否属于时间线上的变化/状态）进行标注，共标注出 **23,183 个事件提及**，平均约每 10 个 token 就有一个事件词，密度远高于新闻语料。
  - 标注者间一致性为 Cohen's kappa = 80.2%。
- **第二阶段：局部共指标注**
  - 仅在同一合同章节（section）内建立共指链接；每个事件提及只与最近的前置共指提及链接。
  - 采用 O'Gorman et al. (2016) 的准则，Cohen's kappa = 70.0%。
- **第三阶段：非局部共指标注**
  - 识别跨章节（cross-section）的共指链，由作者自建标注准则。
  - 因为法律合同极长且有结构化章节，作者采用两遍层次化处理方法：先在每个章节内找局部链，再跨章节找非局部链，从而恢复完整的共指簇。
  - Cohen's kappa = 74.8%。
- **最终的共指簇统计**：共识别出 **853 个非单例事件簇**，其中 653 个为局部簇（平均 2.5 个提及），200 个为非局部簇（平均 4.4 个提及）；非局部簇约一半跨越 2 个章节，约 15% 跨越 6 个及以上章节。
- **监督基线方法**：
  - **事件识别（T-5 模型）**：参照 Hicke and Mimno (2024)，将原始句子作为输入，输出标记了事件提及的同一句子（可直接看作序列标注的 seq2seq 形式）。
  - **事件共指（RoBERTa-base）**：参照 Wang et al. (2022)，将整个文档编码后（超长时切块分别编码），抽取每个事件提及的上下文表示，用分类头做 pair-wise 判定是否存在共指链接。

## 实验设计：使用的数据集、基准与对比方法

- **数据集**：
  - 提出的新数据集 **LegalCore**：100 份法律合同文档，约 250k token，平均每篇约 2.5k token（注：摘要写“25k”，正文抽象写 2.5k，实际正文表格里大概是 2495 tokens 每篇，表 2 中写 2495，应为约 2500 token，属于文本中一处小矛盾。原文摘要处写的 25k tokens 与正文表格不一致，实际统计为每篇约 2495 token）。
  - 对比使用的外部数据集：ACE 2005、ECB+、TAC KBP、MAVEN-ERE、RED 等，主要比较 token 数、每篇文档 token 数、每篇 mention 数、共指链距离分布等。
- **LLM benchmark**：
  - 评估模型：GPT-4（GPT-4-Turbo）、Llama-3.1-8B-Instruct、Mistral-Nemo-Instruct-2407、Qwen2.5-14B-Instruct。
  - 零样本、一样本、两样本（few-shot）提示，事件识别以逐句方式进行提示，事件共指以整篇文档提示进行。
- **评测指标**：
  - 事件识别：micro-Precision / Recall / F1。
  - 事件共指：MUC、B³、CEAF_e、BLANC 四类标准指标。
  - 同时报告了使用金黄事件提及的共指性能和端到端（模型识别的事件提及上做共指）性能。
- **监督基线**：
  - T-5（small / base / large）用于事件识别；
  - RoBERTa-base + pair-wise 分类头用于共指；
  - 5 折交叉验证。

## 资源与算力

- **硬件**：文中提到所有训练在 A-100 GPU 上完成，但**未说明具体 GPU 卡数、训练时长、总耗能或租用费用**。
- **超参数**：
  - T-5 检测模型：学习率 1e-4，batch size 4，训练 100 epochs，5 折交叉验证。
  - RoBERTa 共指模型：Bert 部分学习率 1e-5，分类头学习率 1e-5，batch size 4，训练 200 epochs，5 折交叉验证。
- **LLM 推理**：论文没有给出 LLM 推理所用的算力规模，只提及 GPT-4 实验时间为 2025 年 1 月 15 日至 2 月 15 日期间。

## 实验数量与充分性：是否充分、客观、公平

- **总体实验量**：覆盖两个任务（事件识别、事件共指），各任务包含多组提示设置（零样本、一/两样本）和端到端评估，加上局部 vs 非局部簇的细分和错误类型分析，整体实验量较为充分。
- **监督基线充分**：事件识别尝试了 T-5 small/base/large 三种规模；事件共指采用 5 折交叉验证，可有效评估泛化性能。
- **LLM 对比**：涵盖 1 个专有模型和 3 个开源模型，公平性略显不足，因为 Llama-3.1 是 8B，Qwen 是 14B，Mistral 是 12B 级别，而 GPT-4 仍是 API 版本且参数规模远大于它们。这种规模不对等会导致对比结论（“LLM 表现差”）并不能完全归因于模型架构差异。
- **局限性**：没有做包括监督模型使用更长上下文（比如 Longformer/GAU 或 LongRoBERTa）在内的消融，未验证“长距离是监督模型瓶颈”的假设。也没有测试参数更大的 Llama-70B 等模型。
- 从数据集标注质量看，每个阶段只抽样 5 份文档计算 kappa，样本偏小，未给出全量数据集的标注者一致性。

## 论文的主要结论与发现

- **数据集挑战性**：
  - 法律文档事件提及密度极高（约为每 10 个 token 一个事件），“短距离共指链”占比 55.7%（小于 50 token），明显高于 ACE（36.4%）、TAC KBP（22.8%）和 MAVEN-ERE (31.9%)。
  - 同时存在大量超长距离共指链，几十个链跨越 1000–1600 个 token 以上；跨 6+ 个章节的非局部簇约 30 个（15%）。
- **事件识别结果**：
  - 监督 T-5 模型几乎达到完美的 F1 ≈ 98.8–98.9（表 5），远高于 LLM。
  - 零样本下 LLM 普遍“精度高、召回低”，说明 LLM 低估了事件提及密度。
  - 少样本提示可显著提高召回。GPT-4 在 T5-large 基线 98.8% 对比下最佳为两样本 F1=77.7，仍明显低于监督基线。
- **事件共指结果（表 7，两样本设置）**：
  - 监督基线在 MUC F1=57.5、B³ F1=95.6、CEAF_e F1=94.8、BLANC F1=72.3 上明显领先。
  - LLM 表现很差，MUC F1 均低于 8%，BLANC 也极低（GPT-4 最好也仅 4.8）。
  - 少样本提示对 LLM 共指改善有限，说明“给示例”并不能弥补模型对任务模式的深层理解不足。
- **局部 vs 非局部**：
  - LLM 反而在非局部簇上表现相对更好，推断是因为它们在整篇文档上工作而忽视局部密集上下文。
  - 监督基线更擅长局部簇（MUC F1=51.5）而非长距离非局部簇（MUC F1=45.2），瓶颈源于 RoBERTa 512 token 的上下文窗口。
- **错误分析**：
  - 监督模型 FP 占 63%，主要是短距离模式被过度泛化。
  - LLM 的错误以误链接跨章节不相关事件为主，其中 Llama-3.1 的问题尤其严重，会逐步将文档中所有事件链接成一个巨型簇，导致 B³ 和 CEAF_e 分数明显偏低。
- **端到端**：在金标准事件提及被替换为自动识别结果时，LLM 共指分数进一步骤降，凸显事件检测误差的级联影响；监督基线相对稳健。

## 优点：方法或实验设计中的亮点

- **首个法律域数据集**：填补了事件共指研究在长文档法律文本上的空白。
- **三阶段分层的标注方案**：针对法律合同“长、结构强、内容跨节引用”的特点，设计“事件→局部→非局部”两遍共指标注流程有较强的实践合理性，提高了标注质量和可操作性。
- 事件定义没有预设类型（all event mentions），因而能够覆盖合同中可能出现的各类状态、过程和动作，更贴近开放域的实际需求。
- 多维度分析丰富：既提供总体统计（表 2），也分析“共指链距离分布（表 3、图 4）”“局部/非局部簇对比”“跨章节跨度分布”“错误来源分解”和“端到端表现”，为后续研究提供了很好的诊断信息。
- 提示和标注指南将随数据公开，便于复现与后续工作扩展。

## 不足与局限：实验覆盖、偏差风险、应用限制等

- **偏差风险**：
  - 数据完全来自法律合同（CUAD 子集），不含判决书、法规、专利或法庭记录，不能代表整个法律领域。
  - 共指标注者抽样数少（每个阶段仅 5 份文档），全量可信度缺乏更细粒度的量化。
- **LLM 评估不均衡**：GPT-4 为闭源 API 模型，无法精确复现或扩展；开源模型均基于 12B 以下参数量，未测试更大规模的 70B 级 Llama 等，导致“主流 LLM 难以解决任务”结论的适用范围有限。
- **推理成本与输入长度**：事件共指采用全文档输入，LLM 会面临长上下文窗口压力；当文档超过上下文长度时如何处理并没有交代清楚。
- **指标困惑**：文本提到 LLM，例如 Llama-3.1 的 B³ 和 CEAF_e 等某些指标“很高”，但实际上指标会受单例簇的影响，容易造成“高指标、低真实能力”的误读。论文中的低 MUC、BLANC这样的高低对比说明这个现象，但很容易被摘要式阅读忽略。
- **共指定义细节**：仅标注“指向同一时空事件”的核心共指关系，对部分语义相关但有差异的事件（如“develop”与“development”的同根不同义场景）没有更细的说明；事件核心标注采用“单词级触发词”而没有给出完整提及 span，可能损失短语级或跨句式事件表达信息。
- **无消融实验**：未对“二阶段两遍式共指”与“一遍整篇”标注方案做系统性比较，也没有消融监督模型上下文切块策略的各个 chunk 组合方式。

（完）
