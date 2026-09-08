---
title: Summary Factual Inconsistency Detection Based on LLMs Enhanced by Universal Information Extraction
title_zh: 基于通用信息抽取增强的摘要事实不一致检测
authors: "Anguo Li, Lei Yu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1305.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 通过统一信息抽取增强LLM来检测摘要事实不一致，契合生成文本事实一致性评测
tldr: 自动摘要可能存在事实不一致问题，基于LLM的检测器推理成本高且可解释性不足。本文提出UIEFID框架，把信息抽取和推理能力解耦，通过自适应结构化schema指导微调后的LLM统一抽取文档与摘要中的结构化信息并据此判断不一致。方法兼顾效率与可解释性，为生成文本的事实一致性评测提供了通用范式。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 380}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 556}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1161, \"height\": 670}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 483}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 950}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 544}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1305/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 1495}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1305/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 694, \"height\": 229}]"
motivation: 大模型摘要事实检测依赖推理能力，存在效率和可解释性挑战。
method: 设计自适应结构化schema，指导微调LLM抽取文档与摘要的统一结构化信息，再判断是否不一致。
result: 在摘要事实不一致检测任务上实现了有效且可解释的检测结果。
conclusion: 解耦信息抽取和推理是可扩展的摘要事实一致性检测路线。
---

## Abstract
Automatic text summarization has a potential flaw that affects the factuality of summaries. Recently, Large Language Models (LLMs) have been introduced as detectors for factual inconsistencies in summaries. However, LLM-based methods rely on reasoning capabilities and face challenges in terms of efficiency and explainability. We focus on decoupling LLMs’ information extraction and reasoning capabilities to address prominent challenges, and propose a novel framework, UIEFID (Universal Information Extraction-enhanced Factual Inconsistency Detection). Our idea is to define a self-adaptive structured schema to guide fine-tuned LLMs in extracting unified structured information from documents and summaries, ultimately detecting the origins of inconsistencies in extraction information. The evaluation on 5 open-source models shows that UIEFID not only enhances the detection accuracy on the AGGREFACT benchmark but also significantly reduces redundant reasoning.

---

## 论文详细总结（自动生成）

## 论文总结：基于通用信息抽取增强的大语言模型摘要事实不一致检测

### 1. 论文的核心问题与整体含义

- 自动文本摘要模型（尤其是抽象式摘要）可能生成与原文不一致的内容，即“事实不一致”或“幻觉”。
- 现有基于大语言模型（LLM）的事实不一致检测方法主要依赖 LLM 的推理能力，存在两个核心痛点：
  - **效率低**：检测过程冗长、输出冗余，尤其在长文档场景下；
  - **可解释性差**：推理链可能出错或产生不稳定的“幻觉式”判断。
- 论文提出，将 LLM 的**信息抽取能力**与**推理能力解耦**，先用结构化抽取压缩语义信息，再针对结构化差异做判断，从而提升检测的效率和可解释性。
- 基于这一思想，作者提出 **UIEFID（Universal Information Extraction-enhanced Factual Inconsistency Detection）** 框架，将通用信息抽取（UIE）引入 LLM 事实一致性评测。

### 2. 论文提出的方法论

- **核心思想**：从文档 `D` 和摘要 `S` 中抽取统一结构化信息 `(I_d, I_s)`，把结构化为以“主语”为中心的三元组形式：`Sub_i : (k_j, v_j)`；通过比较文档与摘要的结构化信息差异来判定摘要是否与文档事实一致。
- **框架流程**：UIEFID 采用“检测 + 修正”的顺序策略，分为三个阶段：
  1. **Subject Alignment（主语对齐）**
     - 用命名实体识别比较文档与摘要中的“主语”；
     - 识别三类错误：不存在、拼写错误、错位；
     - 结合相似度计算与共指消解，用文档中的匹配主语替换摘要中的不一致主语，记录分析结果用于后续打分。
  2. **Key-value Analysis（键值对分析）**
     - 首先对 LLM 进行信息抽取任务微调；
     - 从摘要中抽取“主语-键值对”结构；
     - 将值掩码为 `[?]` 形成抽取模式（schema），引导模型从文档中检索并填充对应值；
     - 比较摘要与文档中结构化键值对的差异，得到不一致的来源与检测结果。
  3. **Factuality Evaluation（事实性评价）**
     - 综合前两阶段的不一致信息；
     - 用公式计算摘要的事实性分数（Factuality Score，FS）：
       \( FS = \frac{|ent_{fc}|}{|ent|} \times \frac{\sum_i |p^{fc}_i| / |p_i|}{|Sub|} \)
     - 分数同时考虑“实体层一致率”与“键值对层一致率”，使输出更加可解释、可量化。
- **实现细节**：
  - 主语检测使用 spaCy 的低资源工具；
  - 微调数据采用 IEPile 指令语料（约 0.32B tokens，涵盖 NER、关系抽取、事件抽取）；
  - 微调模型包括 Llama3-8B、Llama3.1-8B、Qwen2.5-7B、Qwen2.5-14B；
  - 另外通过 API 实验了 DeepSeek-R1。
- **关键设计差异**：传统方法以文档为参照验证摘要；UIEFID 反其道而行，以摘要为锚点构造“抽取模式”，再回文档中寻找对应证据，从而减少长文档带来的检索负担。

### 3. 实验设计

- **Benchmark**：AGGREFACT（正文写作 AGGRE FACT），包含两个子集：
  - AGGREFACT-CNN；
  - AGGREFACT-XSum。
- 所有摘要来自 CNN/DailyMail 和 XSum 新闻文章；检测结果进一步按摘要模型发展时期划分为 FTSOTA、EXFORMER、OLD 三个分组。
- **评价指标**：平衡准确率（balanced accuracy），用于缓解数据集中一致/不一致样本不平衡的问题。
- **基线方法**：共 12 类既有检测方法，覆盖三类范式：
  - **NLI 类**：DAE、SummaC-ZS、SummaC-Conv、MENLI、AlignScore；
  - **QA 类**：QuestEval、QAFactEval；
  - **LLM 类**：TrueTeacher、ChatGPT-ZS/CoT/DA/Star 等。
- **实验形式**：
  - 每个开源模型对比三种策略：零样本、信息抽取微调（+fine-tuning）、微调后按 UIEFID 执行（+UIEFID）。
  - 同时给出 5 个 LLM 在 UIEFID 框架下的整体表现。

### 4. 资源与算力

- 论文**没有明确说明** GPU 型号、数量、训练时长等具体硬件算力资源。
- 仅提到：受硬件资源限制，无法本地部署和微调 DeepSeek-R1，只能通过 API 调用；
- 其他四个开源模型（Llama3-8B、Llama3.1-8B、Qwen2.5-7B、Qwen2.5-14B）完成了本地微调和推理，但具体训练配置缺失。

### 5. 实验数量与充分性

- 主实验覆盖 2 个数据集子集、3 类摘要模型分组、5 个 LLM、3 种策略，并对比了 12 个已有基线，规模较完整。
- 另有 3 组辅助实验：
  - **消融研究**：使用微调 Qwen2.5-7B，配置 ZS、KVA、SA+KVA，每组重复 10 次，报告均值和波动区间；
  - **鲁棒性分析**：按压缩比把数据分为 5 档，测试 4 个微调 LLM 在不同压缩比下的准确性；
  - **效率分析**：用自定义效用指标 \(U\) 比较模型输出 token 与输入 token 的比值，评估冗余推理程度。
- **公平性与客观性**：
  - 主实验采用标准化的 AGGREFACT 评测集，并报告了多种基线的官方/复现结果；
  - 消融实验采用重复实验并报告波动范围，增强了可靠性；
  - 但未对 DeepSeek-R1 做消融，因其只能通过 API 使用；部分基线仓库缺少维护可能导致对比实验无法完整复现，存在一定的外部限制。

### 6. 论文的主要结论与发现

- UIEFID 能显著提升摘要事实不一致检测的**准确性、效率和可解释性**。
- 在 AGGREFACT 上，DeepSeek-R1 + UIEFID 达到最高平均平衡准确率 83.7，显著超过其零样本设置的 80.3。
- 四个本地微调模型中 Qwen2.5-14B + UIEFID 效果最好，平均为 79.8；Llama3.1-8B + UIEFID 平均为 77.3。
- 单纯信息抽取微调带来的性能提升有限，只有将微调后的模型放入 UIEFID 三阶段流程时，提升才明显（最高提升 14.5%）。
- 消融实验显示：键值对分析比零样本提升 10.9 个点的平均平衡准确率；加入主语对齐后进一步提升 3.7 个点；性能提升同时未显著增加输出波动。
- 效率指标显示，UIEFID 能明显减少冗余推理；但 DeepSeek-R1 因模型自带思维链输出大量思考 token，效用指标最低。
- 压缩比鲁棒性实验表明，模型准确率与“文档/摘要长度比”不是严格线性关系，中间压缩区间波动较大，但模型在极简单或极高压缩场景下相对稳定。

### 7. 优点

- **思想创新**：首次将 UIE 与 LLM 事实不一致检测结合，用“抽取 + 结构化比较”替代“纯推理”，是较新的技术路径。
- **可解释性与效率兼顾**：通过结构化的“主语-键值对”输出，检测结果可定位到具体实体和属性，并支持后续改写修正，缓解了 LLM 不透明和长文档推理负担大的问题。
- **以摘要为基准的验证设计**：从摘要出发构造抽取模式再检索文档，比“全文档直接比较”更契合摘要短、文档长的实际场景。
- **定量消融与鲁棒性分析较完整**：不只报主实验结果，还提供消融、重复实验区间、压缩比分析、效用指标，整体可信度较高。
- **在多种开源模型上均有增益**：验证了框架通用性，而不仅仅依赖单个超强 LLM。

### 8. 不足与局限

- **算力与实现细节缺失**：未报告 GPU 数量、微调时长、显存占用等，难以复现训练成本。
- **结构化表示不一定最优**：作者自己也承认“以主语为中心的三元组”未必是最佳结构化形式，其他语义表示可能有更好的效果。
- **基准数据范围有限**：AGGREFACT 主要来自 CNN/DM 和 XSum 的传统或早期摘要模型，缺少面向最新 LLM 生成的摘要数据集，可能低估当前 LLM 摘要的实际错误分布。
- **基线复现受限**：部分检测基线官方代码仓库不再维护或存在运行问题，影响了实验对比的完整度。
- **模型覆盖仍有缺口**：DeepSeek-R1 无法本地微调，不能参与同等的消融与压缩比实验；且最大本地模型为 14B，对外部更大模型缺乏进一步验证。
- **评估指标与理论假设依赖较强**：主语对齐依赖 NER 和共指消解工具，若摘要包含隐式指代或复杂描述，框架的抽取和匹配可能引入新的误差。

（完）
