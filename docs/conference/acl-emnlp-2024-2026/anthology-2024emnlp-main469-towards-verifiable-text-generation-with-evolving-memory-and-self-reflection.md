---
title: Towards Verifiable Text Generation with Evolving Memory and Self-Reflection
title_zh: 迈向可验证文本生成：演化记忆与自我反思
authors: "Hao Sun, Hengyi Cai, Bo Wang, Yingyan Hou, Xiaochi Wei, Shuaiqiang Wang, Yan Zhang, Dawei Yin"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.469.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 使用演化记忆与自我反思框架生成带引用文本，使生成声明可追溯到证据并减少幻觉
tldr: 生成带引用的可验证文本仍因焦点漂移和声明-引用对齐困难而存在挑战。论文提出VTG框架，引入演化型长短时记忆和自反思机制，使模型在生成过程中动态记忆、审视并维护声明与检索文档的关联，促使声明正确匹配引用。实验结果表明VTG改善了生成内容的事实正确性和可验证性，为缓解幻觉提供了一条可验证生成的实现路径。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main469/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main469/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1398, \"height\": 1383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main469/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main469/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main469/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1611, \"height\": 359, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 791, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1650, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1647, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1648, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main469/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1639, \"height\": 411, \"label\": \"Table\"}]"
motivation: 可验证生成面临焦点漂移、声明与引用对齐困难以及检索广度精度取舍等挑战。
method: 提出VTG框架，引入演化长短时记忆与自我反思机制来维护和校准声明对应的引用。
result: 实验表明VTG能生成附带准确引用的内容，显著改善文本可验证性和事实正确性。
conclusion: 演化记忆加自反思使模型生成过程持续核实证据，是提升可验证生成的高效方案。
---

## Abstract
Despite the remarkable ability of large language models (LLMs) in language comprehension and generation, they often suffer from producing factually incorrect information, also known as hallucination. A promising solution to this issue is verifiable text generation, which prompts LLMs to generate content with citations for accuracy verification. However, verifiable text generation is non-trivial due to the focus-shifting phenomenon, the intricate reasoning needed to align the claim with correct citations, and the dilemma between the precision and breadth of retrieved documents. In this paper, we present VTG, an innovative framework for Verifiable Text Generation with evolving memory and self-reflection. VTG introduces evolving long short-term memory to retain both valuable documents and recent documents. A two-tier verifier equipped with an evidence finder is proposed to rethink and reflect on the relationship between the claim and citations. Furthermore, active retrieval and diverse query generation are utilized to enhance both the precision and breadth of the retrieved documents. We conduct extensive experiments on five datasets across three knowledge-intensive tasks and the results reveal that VTG significantly outperforms baselines.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：大型语言模型在语言理解和生成方面能力突出，但常产生与事实不符的内容（即幻觉），这严重影响其在问答、搜索引擎、对话系统等场景中的可靠性。为缓解这一问题，学界提出**可验证文本生成（Verifiable Text Generation）**——要求 LLM 在生成每个声明（claim）时同时提供支撑该声明的引用文档（citation），使生成内容可追溯、可核验，如 Bing Chat 和 Perplexity.ai 等商用系统已采用该范式。
- **核心问题**：论文指出现有可验证文本生成方法仍面临三大挑战：
  1. **焦点漂移现象（focus-shifting）**：长文本生成过程中内容关注点会不断变化，导致静态检索文档难以支撑不断变化的主题；
  2. **声明-引用对齐难度高**：声明与潜在证据之间往往并非简单的字面匹配，而需要深层语义分析和逻辑推断；
  3. **检索精度与广度的两难**：既要避免噪声文档以精确保留高相关文档，又需要足够宽泛的文档覆盖以增强内容的可信度。

## 2. 论文提出的方法论

### 2.1 总体框架

- 提出 **VTG（Verifiable Text Generation with Evolving Memory and Self-Reflection）**，一个通过**迭代式生成—验证—再生成**来完成可验证文本生成的框架。
- 系统接收问题 q 和语料库 D，输出由 n 个声明组成的答案 S，每个声明 sᵢ 附带引用文献集合 Cᵢ。
- 框架核心是**演化型长短时记忆系统**：
  - **长期记忆 D_L**：存持续有价值的文档；
  - **短期记忆 D_S**：存与当前生成焦点相关的近期文档，随内容焦点变化动态更新。

### 2.2 三个阶段（如图 2 所示）

1. **记忆生成阶段（Generation with Memory）**：将声明生成与引用生成**分开处理**，分别使用专门的 Prompt，避免单一模块中上下文干扰；
2. **引用验证阶段（Citation Verification）**：利用**双层验证器**对声明与引用关系进行自我反思式检查；
3. **引用简化阶段（Citation Simplification）**：修剪不必要的引用，保留最小充分支撑集，使最终引用简洁有力。

### 2.3 关键组件

- **Claim Generator（声明生成器）**：基于长期记忆 D_L 和短期记忆 D_S 完成未完内容；初始 D_L 由原始问题检索 top-k 文档填充，D_S 初始为空。
- **Citation Generator（引用生成器）**：仅为当前声明从记忆中检索支撑文档并标注引用。
- **双层验证器**（均基于 NLI 模型，将证据视为前提、声明视为假设）：
  - **Generation Verifier（生成验证器）**：检查已引用的文档是否在逻辑上支撑声明。若通过则进入简化阶段；若不通过则转交记忆验证器；
  - **Memory Verifier（记忆验证器）**：判断整个记忆集合（D_S ∪ D_L）是否能支撑声明。
    - 若记忆整体可以支撑：说明问题出在“引用生成环节”——简化完整记忆集，用其结果作为引用；
    - 若记忆整体无法支撑：说明声明本身可能基于模型参数化知识产生了事实性错误，激活**Evidence Finder（证据查找器）**。
- **Citation Simplifier（引用简化器）**：遍历引用集中的每个文献，临时移除某个文献并测试声明是否仍被充分支撑；若移除后不影响支撑性则永久删除该文献。
- **Evidence Finder（证据查找器）**：只有当记忆验证器未能通过时才激活（保证“必要才检索”，提升精度）；通过 Prompt 让 LLM 生成多个**多样化查询**和**上下文感知查询**（融合原始问题、当前声明和未完成内容，消除代词歧义），再用检索器获取文档刷新短期记忆 D_S。

### 2.4 算法流程（Algorithm 1）

- 初始：D_L ← 检索(q, D, k)，D_S ← ∅；
- 循环：生成声明 s 和引用 C；若 s 为 EOS 则结束；
- 若 GenerationVerifier(s, C) 为真 → 引用简化 → 输出并入 D_L；
- 否则若 MemoryVerifier(s, D_S∪D_L) 为真 → 对记忆全集做简化作引用 → 输出并入 D_L；
- 否则若超过最大尝试 T → 接受当前 (s, C) 并继续；
- 否则 → 激活 EvidenceFinder 刷新 D_S，t 增加；
- 循环直到生成终止。

## 3. 实验设计

### 3.1 数据集与任务（共 5 个数据集，3 类任务）

| 任务类型 | 数据集 | 说明 |
|---|---|---|
| 多跳问答 | 2WikiMultihopQA | 2 跳复杂问题，涉及组合、比较或推理，Wikipedia 来源 |
| 长文本问答 | ASQA | 模糊问题，需覆盖多个解释的全面答案 |
| 长文本问答 | ELI5 | 复杂问题，需多文档支撑的深入长答案 |
| 开放域问答 | NQ（Natural Questions） | 单答案开放域问答 |
| 开放域问答 | WebQ（WebQuestions） | 基于 Freebase 的问答 |

### 3.2 对比方法（Baselines）

- **VANILLA**：基于 top-k 检索文档直接生成带引用文本；
- **SUMM**：先对 top-K 文档做摘要再生成带引用文本；
- **SNIPPET**：先提取相关片段再生成带引用文本；
- **RERANK**：高温采样生成 4 个回答，选引用召回率最高的输出；
- 附录还比较了多种后处理方法：POST CITE、REFINE CITE、VERI CITE、VERI REFINE。

### 3.3 模型与配置

- 两个生成模型：**Vicuna-13B-v1.5-16k** 和 **Text-Davinci-003**；
- 检索器：DPR（Dense Passage Retriever）；检索语料：Wikipedia dump（2018-12-20）；
- NLI 验证器：**TRUE 模型（T5-11B，在 NLI 混合数据上微调）**，另有附录以 t5_11b_trueteacher_and_anli 验证鲁棒性；
- 引用质量自动评估：ALCE 的 Citation Recall/Precision/F1，以及用 **Qwen-Max** 评估的 LLM.Citation Recall/Precision/F1；
- 数据集规模：Vicuna 下每组 500 条，Text-Davinci-003 下每组 200 条。

## 4. 资源与算力

- **论文未明确说明使用的 GPU 型号、数量及训练时长**。
- 本文属于**基于现有 LLM 的推理/生成框架**，不涉及训练新模型，主要计算开销来自多次 LLM API 调用（Vicuna-13B 本地推理与 Text-Davinci-003 API）以及 NLI 验证模型的推理。
- 论文提及 VTG 的计算成本较高，原因是多次 API 调用和频繁验证；其 token 成本可通过最大尝试数 T 调节以权衡性能与开销。

## 5. 实验数量与充分性评估

- **主实验**：5 个数据集 × 2 个 LLM（13B 与 Davinci），指标覆盖答案正确性和引用质量两方面，对比 4 个主流基线和 4 个后处理基线（附录），规模较充分。
- **消融实验**（2WikiMultihopQA，Vicuna-13B）：逐项移除“双层验证器”“演化记忆”“引用简化器”“多样查询生成”，结果显示每个组件均有贡献，其中验证器贡献最大。
- **超参数分析**：
  - 最大尝试 T 实验（T = 1~5）：增大 T 提升效果但增大 token 消耗；
  - 查询数量 M 与每查询检索数 N 的敏感性测试（ASQA）：存在最优区间；
  - token 消耗对比（NQ, Text-Davinci-003）：VTG 低于 RERANK 且引用质量更高。
- **NLI 鲁棒性实验**（附录 D）：在 ASQA 和 NQ 上换用不同 NLI 模型，VTG 仍优于强基线。
- **焦点漂移现象验证**（附录 C）：用 BGE 嵌入构建句间相似度矩阵，展示了随生成推进内容相关性下降的现象。

**评价**：整体实验设计覆盖多个任务类型、多样化和主流的数据集，消融和分析较完整，评测指标兼顾事实正确性和引用质量，还引入了独立 LLM 评估以减少单一 NLI 偏差，实验较充分、客观。但未提供统计显著性检验信息。

## 6. 论文的主要结论与发现

- 在不同参数规模的 LLM 上，**VTG 在所有数据集和指标上显著优于各基线**。
- 引用质量方面，相比于最强基线 RERANK，VTG 在 Text-Davinci-003 上相对提升约 **22%**，在 Vicuna-13B 上约 **9%**（Citation F1）。
- 可验证生成能力的增强同时带来了答案正确性的提升（综合约 5% 的相对提高），说明“生成带引用文本”与“生成准确内容”并非互相排斥，而是可协同促进的。
- 双层验证器能够有效区分“引用错误”与“声明错误”两种失败模式；对前者通过简化重新选择引用，对后者通过证据查找重新生成——这种自我反思机制是效果提升的关键。

## 7. 优点

1. **任务分解设计合理**：将可验证生成拆解为“声明生成”和“引用生成”两个独立模块，降低生成复杂性，避免引用编号干扰。
2. **演化型长短时记忆巧妙地应对焦点漂移**：长期记忆为全局提供稳定支撑，短期记忆按生成焦点动态刷新，设计直观有效。
3. **双层验证器机制精细**：通过生成验证器和记忆验证器的两级判断，能区分失败源自“引用错误”还是“声明错误”，并分别给出修正路径，具备较强的纠错能力。
4. **引用简化器**保证了引用最小充分性，提升了引用精确率。
5. **主动检索原则**：只在记忆无法支撑声明时才启动检索，减少无关噪声；多样化的上下文感知查询生成兼顾了查询广度与消歧能力。
6. **实验全面**：覆盖多跳 QA、长文本 QA、开放域 QA 三个任务，多个数据集、多模型、多基线、多组消融和参数分析，且同时引入 ALCE 指标和 LLM 评估指标，可信度较高。
7. **关注实际成本**：绘制了 token 消耗对比，让读者了解性价比。

## 8. 不足与局限

1. **计算开销较大**：需要多次 LLM 调用和频繁验证，在资源受限系统中部署和推广受限（论文已在 Limitations 中明确承认）。
2. **依赖 NLI 验证器的准确性**：若 NLI 模型判断失真，会将错误信息引入流程，影响最终可验证性（论文在 Limitations 中说明为未来方向）。
3. **未报告训练/推理的具体硬件与成本明细**：难以客观精确衡量其算力消耗，读者难以独立复现计算成本。
4. **生成模型规模有限**：仅使用了 13B 的开源模型和较早期的 API 模型，未在更大的主流先进模型（如 GPT-4、Llama-70B 等）上验证其通用性和可迁移性。
5. **对比基线相对有限**：主体对比来自 ALCE 系列方法，虽然附录加入了后处理基线，但未与同期更新的可验证生成/Self-RAG 等框架进行对比。
6. **未报告统计显著性检验**：不同方法和设置之间的差异是否具备统计显著性尚不清楚。
7. **最大尝试次数 T 的机制**：当验证多次失败后仍会无条件接受未验证声明，这虽然是保证生成终止的实际取舍，但也意味着**完全不保证**每条输出均可验证。
8. **评估对 NLI 模型的依赖**：虽然引入 LLM 评估缓解了部分问题，但 NLI 模型本身可能对某些“需要背景推理才能建立关联”的支持关系不敏感，评估指标和内部验证器共享同源模型时可能存在偏差。

（完）
