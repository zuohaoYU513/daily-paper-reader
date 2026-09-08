---
title: Calibrating Long-form Generations From Large Language Models
title_zh: 大语言模型长文本生成的校准
authors: "Yukun Huang, Yixin Liu, Raghuveer Thirukovalluru, Arman Cohan, Bhuwan Dhingra"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.785.pdf"
tags: ["query:metacognitio"]
score: 10.0
evidence: 基于自评价与自一致性校准长文本生成的置信度
tldr: 传统校准依赖回答正确与否的二元判定，难以处理可部分正确的长文本生成。本文提出统一校准框架，将回答正确性与置信度视为分数分布，并设计三种校准评估指标及基于自一致性和自我评价的置信度诱发方法。实验表明该方法能更有效地评估并改进大模型长文本生成的置信度校准。相关工作为需要高可靠长文本生成的应用提供了统一度量与训练依据。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1660, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 152, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 757, \"height\": 864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 512, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 512, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 514, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 512, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 514, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 514, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp785/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 787, \"height\": 535, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1534, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1267, \"height\": 789, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 670, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 593, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 783, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1660, \"height\": 2350, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp785/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1660, \"height\": 2545, \"label\": \"Table\"}]"
motivation: 传统置信度校准依赖二元正误判断，难以适配可部分正确的长文本生成。
method: 提出统一校准框架，将正确性与置信度建模为分数分布，并引入自一致性与自我评价的置信度诱发方法。
result: 实验表明所提校准指标与置信度诱发方法能在大模型长文本生成中更好地对齐置信度与正确性。
conclusion: 为长文本生成提供了面向分布的校准与评估方案，可增强大模型可靠性。
---

## Abstract
To enhance Large Language Models’ (LLMs) reliability, calibration is essential—the model’s confidence scores should align with the likelihood of its responses being correct. However, traditional calibration methods typically rely on a binary true/false assessment of response correctness, unsuitable for long-form generations where an answer can be partially correct. Addressing this gap, we introduce a unified calibration framework, in which both the correctness of the LLMs’ responses and their associated confidence levels are treated as distributions across a range of scores. We develop three metrics for assessing LLM calibration and propose confidence elicitation methods based on self-consistency and self-evaluation. Our experiments demonstrate that larger models don’t necessarily guarantee better calibration, that various calibration metrics complement each other, and that self-consistency methods excel in factoid datasets. We also find that calibration can be enhanced through techniques such as fine-tuning, scaling the temperature. Finally, we illustrate one application of long-form calibration through selective answering in long-form responses, optimizing correctness within a constrained API budget.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 论文的核心问题与整体含义

传统的大语言模型（LLM）置信度校准方法通常依赖于一种二元（True/False）正确性判定，将回答正确性视为 0 或 1，并要求模型的置信度与“回答完全正确”的概率对齐。然而，长文本生成（Long-form Generation）的回答常常能*部分正确*，其正确性并非简单的非对即错。本文将正确性与模型置信度建模为分数空间（例如 [0,1]）上的概率分布，提出了一个**统一的校准框架**，适用于偏序、连续、主观等多种评估方式，以更好地评估、理解和改进大模型在长文本生成中的可靠性。核心目标是解决传统二元校准无法适配长文本生成的粒度化正确性问题，并为 LLM 在开放长文本任务中的置信度评估定义了新的规范。

### 2. 论文提出的方法论

**核心思想**：论文将 LLM 回答某长文本的正确性 `T` 与模型对该回答的置信度 `C` 均视为在正确性分数空间 `S` 上的概率分布（如“该回答有 x% 的概率是 s% 正确的”），目标是让这两个分布尽可能对齐。

**关键技术细节**：
- **正确性分布（Target Correctness Distribution）**：由外部评估器给出。短文任务可直接使用任务特定指标，长文任务可使用 GPT-4 或人工评估得到分数（0-5级），再归一化为分布。
- **置信度分布估计**：
  - **连续自我评估（CSE）**：使模型直接自我打分，通过多次采样获得一个分布。
  - **成对自一致性（PSC）**：使用相似度度量（如 Naive / Split / Claim / NER）在主回答与其余自采样得到的多个候选答案之间进行两两比较，生成一个相似度分布。
- **校准评估指标**：
  - **ECE-M（多类期望校准误差）**: 对各个正确性水平上的置信度-频率差异加权求和，衡量校准误差。
  - **Correlation（相关度）**: 计算模型预期置信度列表与实际正确性列表之间的相关性，用于反映排序能力。
  - **Selective F1**: 使用置信度和正确性的双阈值，衡量模型筛选高质量回答（超过特定正确性阈值）的精确率与召回率的调和平均数。

**算法流程**（以文字说明）：
1. 生成回答 → 2. 使用评估器估计正确性分布 → 3. 通过 CSE 或 PSC 得到置信度分布 → 4. 计算 ECE-M、Correlation、Selective F1 评估校准程度。

### 3. 实验设计

**数据集/场景**：
- 长文本 QA 数据集：ASQA（事实性多源问答）、ELI5（开放域长按需解释）、QAMPARI（包含多答案列表）。
- 总结任务数据集：CNNDM（新闻摘要）。
- 部分实验引入人类评估员协助验证 GPT-4 评估的正确性。

**评估者与基准对比**：
- 正确性“金标准”使用 GPT-4 评估或任务特定指标（如 F1-5 评分）。
- 与任务特定指标（如 EM-recall）进行对照，验证 GPT-4 评估的可靠性。
- 对比方法分为三类基线：
  - 基于 logits 的**句子似然（SL）**
  - 基于自我评估的**二元自我评估（BSE）**
  - 基于自一致性的**平均自一致性（ASC）**（将相似度平均后作为单个分数）和**成对自一致性 F1（PSC-F1）**。
- 本研究提出的方法：**连续自评估（CSE）** 和 **成对自一致性（PSC）**（采用更详细的相似度度量，如 Claim 或 NER）。

### 4. 资源与算力

论文的公开提取文本**未明确提及**所使用的 GPU 型号、集群规模、节点数量或对应的训练/实验总时长。文中的模型（如 GPT-3.5、GPT-4）以 API 形式调用，开放权重模型（如 Llama-2-13b/70b 等）具体训练卡数也未披露，因此算力资源无法量化总结。

### 5. 实验数量与充分性

- **数量**：论文对 5 个模型（Llama-2-13b/70b 等）在 4 个数据集上共做了 7 组主要对照实验（不同置信度诱发方法对比），加上 2 大类消融改进实验（Fine-tuning 与 Temperature 调整）以及额外分析（source documents 影响与混合置信度诱发），实验量较丰富。
- **充分性与客观性**：
  - 实验覆盖面广（涵盖不同模型尺寸、不同任务类型），且进行了人类评估以检验 GPT-4 评估指标的合理性。
  - 但部分实验缺少统计显著性检验，不同基线设计在某些场景下并不完全对等（表 1 中 PSC 的某些分数优势不是很稳定），整个评估框架受制于 GPT-4 或评估器的准确性，在主观性较强的任务上不能完全排除偏差。

### 6. 论文的主要结论与发现

- **更大的模型并不自动带来更好的校准**：如 Vicuna-13b 在相关度上有时高于 Llama-2-13b/70b，而 GPT-3.5 (大型 API 模型) 虽然排名高，但其校准不一定优于开源小模型。不过更强的模型由于可生成更多高质量回答，因此在 Selective F1 上表现优异。
- **自洽性方法在事实性数据集上更强**：PSC 方法在 ASQA 与 QAMPARI 上优于自我消融评价方法，但在开放域较强的任务（ELI5 与 CNNDM）上优势不明显。
- **基于分布的度量方法有效且必要**：相比单一分数基线，将一致性视为分布（PSC-F1）以及细化自评估（CSE）能更好地抓住长文本正确性，且校准指标从不同角度（分类、排序、选择）提供信息，互为补充。
- **校准指标互补**：不同类型的方法只在某一指标上可靠，因此多指标并用对全面评估校准至关重要。
- **校准可通过微调与解码设置改善**：通过微调（尤其在加入生成任务时）和减小或提升 temperature 可以有效提升置信度与实际正确性的一致性。
- **混合置信度诱发**（结合自我评估和自一致性）可进一步提升校准。
- **额外上下文**：Oracle 文档能提升校准水平（相关文档），随机文档则影响有限或带来负效果。

### 7. 优点

- **方法论创新**：首次系统提出将长文本置信度与正确性同时建模为分布，并设计了三位一体的衡量框架（解释性和理论基础较强）。
- **通用性与灵活性**：框架评估器无关（可替换 GPT-4 / 任务特定指标 / 人类评估）、置信度诱发机制不依赖单一模型（适用多种 LLM）。
- **自一致性度量设计细致**：提出了 Naive / Split / Claim / NER 四个由粗到细的相似性比较策略，兼顾不同粒度与效率。
- **应用价值高**：提出 cascade 选择推理策略，可在 API 预算受限的情况下通过小模型处理“自信”问题，大模型兜底，显著节省成本且保证回答质量。
- **实验扩展性强**：进行了人类评估、微调、温度、加引用上下文等多种辅助分析，较充分探索了边界条件。

### 8. 不足与局限

- **依赖 GPT-4 打分的局限**：在主观性更强的任务（如 ELI5）上，不同评价者/任务对正确答案的理解差异带来更大评分方差，GPT-4 与人类打分者都难以精确抓到理论分布。
- **领域通用性缺失**：实验集中在新闻总结、通用长文本 QA 和事实型问答，法律、医学、教育等高风险领域的校准未见说明。
- **计算开销大**：自一致性方法的多次采样与两两对比与评估造成显著计算成本，较难在生产环境实时实现。
- **未提供充分的显著性检验 / 校准置信区间**：横向对比并未提供多个随机种子的均值方差（除了 cascade 实验中），校准比较的确定性需要进一步验证。
- **缺乏针对更细粒度专业评估的适配**：GPT-4 作为裁判在内容逐句事实核查、结构化输出（如数字列表）上的不可靠性未被系统消融分析（如使用 FactScore 等专门事实性评估器）。

（完）
