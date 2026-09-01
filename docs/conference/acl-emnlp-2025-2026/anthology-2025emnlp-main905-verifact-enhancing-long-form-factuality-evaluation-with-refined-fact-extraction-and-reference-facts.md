---
title: "VeriFact: Enhancing Long-Form Factuality Evaluation with Refined Fact Extraction and Reference Facts"
title_zh: VeriFact：通过精细事实抽取与参考事实增强长文本事实性评估
authors: "Xin Liu, Lechen Zhang, Sheza Munir, Yiyang Gu, Lu Wang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.905.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 长文本LLM回复的事实性评估框架，检测不完整和缺失事实
tldr: 评估LLM长文本回复的事实性具有挑战性，现有方法常遗漏关键关系事实。本文提出VeriFact框架，通过识别并补全不完整或缺失事实来改进事实抽取，从而支持更准确的验证；并构建FactRBench基准，同时评估精确率和召回率，弥补以往只关注精确率的不足。该工作为长文本幻觉评估提供了更全面的评测工具。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main905/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main905/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main905/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 169, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main905/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1620, \"height\": 593, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1563, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 766, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1502, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 763, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1461, \"height\": 559, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main905/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 742, \"height\": 157, \"label\": \"Table\"}]"
motivation: 长文本生成中事实抽取常丢失上下文和关系事实，评估不全面。
method: VeriFact识别并解决不完整和缺失事实，FactRBench评估精确率与召回率。
result: 更准确的事实提取和基准提升了长文本事实性评估质量。
conclusion: 为长文本LLM响应的事实性评估提供了精细化框架与双向度量基准。
---

## Abstract
Large language models (LLMs) excel at generating long-form responses, but evaluating their factuality remains challenging due to complex inter-sentence dependencies within the generated facts. Prior solutions predominantly follow a decompose-decontextualize-verify pipeline but often fail to capture essential context and miss key relational facts. In this paper, we introduce VeriFact, a factuality evaluation framework designed to enhance fact extraction by identifying and resolving incomplete and missing facts to support more accurate verification results. Moreover, we introduce FactRBench , a benchmark that evaluates both precision and recall in long-form model responses, whereas prior work primarily focuses on precision. FactRBench provides reference fact sets from advanced LLMs and human-written answers, enabling recall assessment. Empirical evaluations show that VeriFact significantly enhances fact completeness and preserves complex facts with critical relational information, resulting in more accurate factuality evaluation. Benchmarking various open- and close-weight LLMs on FactRBench indicate that larger models within same model family improve precision and recall, but high precision does not always correlate with high recall, underscoring the importance of comprehensive factuality assessment.

---

## 论文详细总结（自动生成）

# 中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

大型语言模型（LLM）在长文本生成方面表现出色，但其事实性评估极为挑战。长文本中的事实往往依赖于跨句上下文和复杂关系，现有评估方法普遍采用“分解—去上下文化—验证”（decompose-decontextualize-verify）流水线，但存在两个核心缺陷：

- **不完整事实（Incomplete Facts）**：分解时丢失关键上下文（如条件、比较对象），导致事实含义被曲解。例如，将“如果黄金作为首饰的需求消失，其价格可能下跌20%-50%，使其更具竞争力”分解为“黄金价格可能下跌20%-50%”就丢失了前置条件。
- **缺失事实（Missing Facts）**：未能抽取表达关键关系（如因果、时序）的事实，忽略重要的关系型信息。
- **仅关注精确率（Precision）**：已有工作几乎只评估生成内容中事实的正确比例，忽略了召回率（Recall），即回答是否充分覆盖了与问题相关的关键事实。

为此，本文提出 **VeriFact**（Verification of Refined Facts）——一个改进事实抽取与验证的评估框架，以及 **FactRBench**——首个同时支持精确率和召回率评估的长文本事实性基准，为LLM长文本事实性评估提供了更全面、更可靠的工具。

## 2. 提出的方法论

### 2.1 VeriFact 框架（四步流程）

VeriFact 基于 SAFE 的分解-去上下文化-验证范式，并加入反思式精炼环节，核心流程如下：

1. **Step 1：事实分解**
   - 采用与 SAFE 相同的分解方法，将模型回复拆分为原子事实。

2. **Step 2：检测不完整和缺失事实**
   - 使用三个 LLM（GPT-4o、Llama 3.3-70B、Qwen 2.5-32B）作为自动标注器，模拟人工标注流程。
   - **不完整事实**分类：通过提示词让LLM判断事实是否依赖上下文，并细分为模糊概念/代词、缺失比较对象、省略条件/来源、其他。
   - **缺失事实**检测：先用词映射算法（最长公共子串）找出原文中存在但未被事实覆盖的片段，再让LLM基于PDTB（Penn Discourse TreeBank）的时序关系和因果关系定义，判断这些缺失片段是否表达关键关系。
   - 采用多个LLM标注结果的并集（ensemble），以提高召回率（不完整事实检测召回0.89，缺失事实召回0.85），并增加一步验证避免假阳性。

3. **Step 3：精炼事实（self-reflection）**
   - 对不完整事实：提示LLM补入最小必要的上下文，使事实独立自洽。
   - 对缺失事实：提示LLM根据缺失的关系类型显式生成一个新事实，描述被遗漏的时序或因果关系。

4. **Step 4：事实验证**
   - 采用 FactCheck-GPT 的查询生成与证据检索流程，结合 VERIFY 的证据分类策略。
   - 使用 Serper API（Google Search）检索网页，提取相关片段，最后由 Llama 3.3-70B 将事实分为 **Supported / Contradicted / Undecided** 三类。

### 2.2 FactRBench 基准构建

- **提示来源**：
  - 从 FactBench（真实用户提示）中筛选出649个非发散性、可回答的问题（用GPT-4o过滤+人工检查）。
  - 从Reddit的r/askscience、r/AskHistorians、r/AskEngineers、r/AskEconomics收集447个问题（2024年1月后发布，避免数据泄漏；要求至少两个高赞回答，每个≥70词）。
  - 总计 **1096 个提示**。

- **参考事实集（用于召回评估）**：
  - 对FactBench问题：用GPT-4o、Claude 3.5-Sonnet、Gemini 1.5、Llama 3.1-405B四个LLM生成回答，经VeriFact抽取并验证，只保留Supported事实。
  - 对Reddit问题：从多个人类高赞回答中提取事实作为参考集。
  - 统计：FactBench平均每条回答71.18个参考事实，Reddit平均每条回答64.17个参考事实。

- **外部证据集**：
  - 为每个提示提供完整的网页快照（通过Google Search检索并存储），作为稳定、可复现的验证知识源，避免在线内容变化带来的评估偏差。

## 3. 实验设计

### 3.1 数据与基准

- **初步标注研究**：从FactBench随机选14个提示，采样GPT-4o-mini和Llama3.1-8B的回答，得到451个SAFE抽取的事实，由4名标注者手工分析。
- **事实抽取评估集**：人工标注了1168个事实（来自GPT-4o-mini和Llama3.1-8B的回答），用于对比各方法抽取的事实质量。
- **FactRBench基准**：包含1096个真实世界提示，用于评估12个LLM。

### 3.2 对比方法

- **基线方法**：FactScore、SAFE、FactCheck-GPT、VERIFY。
- **消融配置**：仅开源模型（Llama 3.3-70B + Qwen 2.5-32B）、仅Llama 3.3-70B、仅Qwen 2.5-32B。
- **被测模型**：12个LLM，包括3个闭源（GPT-4o、Claude 3.5-Sonnet、Gemini 1.5-Flash）和9个开源（Mistral-7B/24B/123B、Llama3.1-8B/70B/405B、Qwen2.5-8B/32B/72B）。

### 3.3 评估指标

- **事实抽取**：不完整事实比例（越低越好）、缺失事实数量（越低越好）、人类事实覆盖率（越高越好）。
- **FactRBench**：精确率（Precision）、召回率（Recall）、F1，并分别在FactBench和Reddit两个子集上报告。

## 4. 资源与算力

论文**未明确说明**使用的GPU型号、数量、训练时长等具体计算资源信息。由于VeriFact是评估框架而非训练模型，其运行主要依赖于：
- 多个API模型调用（GPT-4o、Claude 3.5-Sonnet、Gemini 1.5等）；
- 开源模型的本地推理（Llama 3.3-70B、Qwen 2.5-32B等，作者提到以float16运行开放权重模型以减少内存）；
- Google Search API（Serper）。

作者在局限性中提到，完整流水线涉及多次LLM调用（检测、精炼、验证），计算开销较大，可能不适合实时应用。

## 5. 实验数量与充分性

实验数量较为丰富，设计较全面：

- **多组实验**：
  1. 事实抽取方法对比（4个基线 + 3个消融配置，使用人工标注数据）；
  2. 12个模型在FactRBench上的系统评测（精确率/召回率/F1）；
  3. 错误标签变化分析（24.9%精炼事实的验证标签发生变化）；
  4. 离线网页证据与在线搜索的覆盖对比（200条回答、约2.2万条事实）；
  5. 案例研究（展示高精确率低召回率的例子）；
  6. 初步人工标注研究及人机一致性分析（Cohen's Kappa等）。
- **充分性**：
  - 覆盖了不同模型家族和规模，消融实验验证了各组件贡献，证据源对比增强了结论可靠性。
  - 但存在一些不足：人工标注规模相对有限（1168个事实）；参考事实集不可能完全覆盖所有相关事实，可能低估召回率；LLM自动标注与人工标注的一致性仍有提升空间（平均Kappa 0.33，但集成后召回较高）。
  - 总体而言，实验设计客观、对比公平，但资源细节缺失。

## 6. 主要结论与发现

- **VeriFact显著提升事实抽取质量**：
  - 不完整事实比例从SAFE的56.7%降至22.5%（最佳配置）；
  - 人均缺失事实数量从1.22降至0.76（减少37%）；
  - 人类事实覆盖率从77.5%提升至87.1%。
- **不完整事实会扭曲最终事实性评估**：24.9%的事实经精炼后正确性标签发生变化，其中Supported比例下降、Contradicted比例上升，说明现有方法可能高估模型事实性。
- **模型规模与表现**：同一模型家族内，更大的模型通常在精确率和召回率上都更好。
- **精确率与召回率并不必然相关**：例如Qwen2.5-32B在精确率上最高（82.80%），但召回率和F1并不领先；GPT-4o召回率最高（52.42%）但精确率并非最高。仅看精确率会得出误导性结论。
- **开源 vs 闭源**：闭源模型整体召回率更高，但大型开源模型（Mistral-123B、Llama3.1-405B、Qwen2.5-72B）在精确率上极具竞争力，甚至媲美闭源模型。
- **Reddit提示更难**：所有模型在Reddit来源的提示上表现均差于FactBench，因为人类参考事实更分散多样，对覆盖评测提出更高要求。

## 7. 优点

- **问题诊断深入**：通过人工标注揭示了SAFE等方法的缺陷，并提出了比“实体歧义”更全面的不完整事实分类（含缺失比较对象、省略条件等）。
- **方法论创新**：采用多LLM集成检测+反思性精炼，有效解决不完整和缺失事实问题，且消融实验表明即便只用单一开源模型也能优于所有基线，鲁棒性强。
- **基准设计先进**：FactRBench是首个同时提供参考事实集和完整网页证据的长文本事实性基准，支持可复现的召回评估；Reddit提示选择2024年后的数据，降低预训练泄漏风险。
- **评估全面性**：从精确率、召回率、F1等多个维度系统评估12个模型，并额外验证了离线证据的可靠性，考虑了实际应用中的可复现性问题。
- **案例与可视化直观**：用具体示例（如黄金价格问题、美国官方语言问题）清晰展示方法差异与评估维度重要性。

## 8. 不足与局限

- **参考事实集完整性受限**：召回率依赖于参考事实集的覆盖程度，虽然使用多个LLM和人类回答构建，仍可能遗漏相关事实，导致召回率被低估。
- **LLM标注偏差**：事实检测和精炼依赖LLM，与人工标注的一致性尚不完美（单模型Kappa约0.33），集成策略虽提高召回但可能引入额外噪声。
- **计算成本高**：流水线需要多次LLM调用，成本高、延迟大，难以用于实时或超大规模评估。
- **离线证据覆盖不足**：提供的网页快照虽稳定，但知识覆盖不如在线搜索，导致Undecided比例更高；对需要最新信息

对需要最新信息或快速变化的动态事实，离线快照可能存在滞后性，导致评估结果偏向“Undecided”，进而影响事实性判断的准确性。

## 9. 总结与展望

VeriFact 与 FactRBench 的提出，为长文本生成的事实性评估提供了一套更精细、更全面的方法论与评测资源。其核心贡献在于：

- **从“事实是否正确”转向“事实是否完整且正确”**，首次系统性地将召回率引入长文本事实性评估，弥补了既有研究只重精确率的片面性。
- **通过自动化的不完整/缺失事实检测与反思式精炼**，显著提升了事实抽取的质量，使下游验证建立在更忠实、更完整的原子事实上。
- **构建了首个同时支持精确率与召回率评估的公开基准**，并提供了稳定的离线网页证据集，为后续研究提供了可复现的基础设施。

未来工作可从以下方向展开：

- **提升参考事实集的覆盖度**：引入更强大的模型、更丰富的检索来源或众包标注，以构建更接近“完备”的参考事实集，减少对召回率的低估。
- **降低评估成本**：探索更高效的单次调用、模型蒸馏或缓存机制，使完整流水线适用于大规模、实时评估场景。
- **扩展事实类型与语言覆盖**：当前框架主要聚焦于时序与因果关系，未来可纳入模态、情感、主观观点等更复杂的事实类型；同时可拓展到多语言、多领域场景。
- **增强证据源的动态性与可复现性平衡**：研究如何在不牺牲评估可复现性的前提下，整合定期更新的知识快照或混合检索策略。

总体而言，VeriFact 与 FactRBench 为该领域树立了新的评估标准，为后续研究者提供了重要的基线资源与思考方向。尽管仍有局限，但其对“不完整事实”和“缺失事实”的系统性刻画，以及对精确率—召回率双维度的倡导，已使长文本事实性评估向前迈出实质性一步。

（完）
