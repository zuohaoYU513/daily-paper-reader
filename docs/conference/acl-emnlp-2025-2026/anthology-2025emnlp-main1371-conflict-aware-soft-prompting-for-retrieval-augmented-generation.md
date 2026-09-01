---
title: Conflict-Aware Soft Prompting for Retrieval-Augmented Generation
title_zh: 面向检索增强生成的冲突感知软提示方法
authors: "Eunseong Choi, June Park, Hyeri Lee, Jongwuk Lee"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1371.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 解决RAG中上下文与参数记忆的冲突，提升可靠性与事实性
tldr: 针对RAG中检索上下文与大模型参数知识冲突导致生成错误的问题，提出冲突感知RAG（CARE）。该方法包含上下文评估器和基础LLM，上下文评估器将外部上下文编码为记忆嵌入，通过基于事实/对抗的软提示训练来识别不可靠上下文，并生成引导信号使推理朝正确方向进行。实验表明CARE能有效缓解上下文-记忆冲突，提升生成可靠性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1371/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1371/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1371/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1668, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1371/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1371/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 401, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1575, \"height\": 1175, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1645, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1533, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1648, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1461, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1371/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1648, \"height\": 1452, \"label\": \"Table\"}]"
motivation: RAG中检索上下文可能与模型参数知识矛盾，导致生成不可靠。
method: 设计上下文评估器与软提示训练，识别不可靠上下文并引导正确推理。
result: 实验验证CARE能缓解上下文-记忆冲突，提升RAG输出准确性。
conclusion: 为RAG提供了一种轻量级的冲突感知增强方案。
---

## Abstract
Retrieval-augmented generation (RAG) enhances the capabilities of large language models (LLMs) by incorporating external knowledge into their input prompts. However, when the retrieved context contradicts the LLM’s parametric knowledge, it often fails to resolve the conflict between incorrect external context and correct parametric knowledge, known as context-memory conflict. To tackle this problem, we introduce Conflict-Aware REtrieval-Augmented Generation (CARE), consisting of a context assessor and a base LLM. The context assessor encodes external context into compact memory embeddings. Through grounded/adversarial soft prompting, the context assessor is trained to discern unreliable context and capture a guidance signal that directs reasoning toward the more reliable knowledge source. Extensive experiments show that CARE effectively mitigates context-memory conflicts, leading to an average performance gain of 5.0% on QA and fact-checking benchmarks, establishing a promising direction for trustworthy and adaptive RAG systems.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **背景**：检索增强生成（RAG）通过将外部知识注入提示词来增强大语言模型（LLM）的能力，但当检索到的上下文与 LLM 自身的参数化知识相矛盾时，模型往往无法正确解决这种冲突，即"上下文-记忆冲突"（context-memory conflict）。
- **问题严重性**：论文实验表明，当给原本能正确回答问题的 LLM 附加负面上下文（hard negative context）后，各模型的性能下降了 **25.1%-49.1%**，说明错误的外部信息会覆盖正确的内部知识，造成显著的生成质量退化。
- **现有方案的不足**：
  - **自适应检索**（Adaptive Retrieval）：依赖硬性决策（是否检索），难以准确判断模型的知识边界；
  - **解码策略**（Decoding Strategy）：在已包含冲突信息的分布上做调整，缺乏内生的冲突感知能力；
  - **鲁棒训练**（Robust Training）：虽然能提升域内表现，但会导致**灾难性遗忘**，损害 LLM 的通用能力。

---

## 2. 方法论：CARE（Conflict-Aware REtrieval-Augmented Generation）

### 2.1 核心思想

- 提出一种**不修改基础 LLM** 的冲突感知框架，由两个组件构成：**上下文评估器（Context Assessor）**和**基础 LLM**。
- 上下文评估器从基础 LLM 本身实例化而来，将外部上下文编码为紧凑的、可训练的**记忆嵌入**（memory embeddings），并隐式编码对上下文**可靠性的判断**，从而引导 LLM 在选择外部知识或内部知识时做出正确权衡。

### 2.2 阶段一：重建预训练（Reconstruction Pre-training）

- 在输入上下文中拼接 K 个可学习的记忆令牌 M，形成序列输入；
- 通过单次前向传播获得记忆令牌对应的隐藏状态作为记忆嵌入 `E_mem`；
- 用重建损失（negative log-likelihood）训练，使记忆嵌入能够压缩并重建原始上下文信息；
- 使用 LoRA 适配器冻结 LLM 参数，仅训练 LoRA 参数与记忆令牌。

### 2.3 阶段二：冲突感知微调（Conflict-aware Fine-tuning）

- 输入格式：问题 + 上下文 + 记忆令牌；
- 根据闭卷（closed-book）设置下 LLM 是否正确回答来构造训练信号：

#### (1) 基于事实的软提示（Grounded Soft Prompting）
- 当 LLM 闭卷回答**错误**时，配对一个包含正确答案的正面上下文（C_pos）；
- 训练评估器将这种"可靠上下文"信号编码进记忆嵌入，引导 LLM 正确利用外部知识。

#### (2) 对抗性软提示（Adversarial Soft Prompting）
- 当 LLM 闭卷回答**正确**时，配对一个主题相关但不含正确答案的硬负面上下文（C_neg），模拟知识冲突；
- 训练评估器将"不可靠"信号编码进记忆嵌入，使误导信息对生成的影响减弱，LLM 回归参数知识。

#### (3) 训练目标
- **语言建模损失（L_LM）**：保证记忆嵌入支持准确的答案生成；
- **知识蒸馏损失（L_KD）**：根据场景选择不同的教师分布，通过 KL 散度进行蒸馏——正面场景以"上下文+问题"为教师，负面场景以"仅问题"（闭卷）为教师；
- 总损失：`L_FT = L_LM + λL_KD`。

### 2.4 核心优势

- 不需要微调基础 LLM，避免了灾难性遗忘；
- 通过连续软嵌入做"软决策"，比硬性检索决策更灵活；
- 在解码开始前就注入了冲突感知信号。

---

## 3. 实验设计

### 3.1 数据集与 Benchmark

| 任务类型 | 数据集 | 规模/指标 |
|---|---|---|
| 开放域问答（Open-domain QA） | Natural Questions（NQ） | 79,133/8,792/3,610（训练/验证/测试），Span EM |
| | TriviaQA | 11,313，Span EM |
| | WebQA（WebQuestions） | 2,023，Span EM |
| 长文本问答（Long-form QA） | TruthfulQA | 817，F1 / ROUGE-L |
| 事实核查（Fact checking） | FactKG | 9,041，准确率（Acc） |
| 检索器 | ColBERTv2 | 检索 top-1 上下文（Wikipedia） |

### 3.2 对比方法

- **鲁棒训练类**：RetRobust（基于官方代码复现）、Direct FT（将本文训练策略直接应用到基础 LLM）；
- **解码策略类**：CAD、ADA-CAD；
- **自适应检索类**：Adaptive-RAG、SKR-kNN、Priori Judgment；
- **基础基线**：Closed-book（无检索）、Vanilla RAG。

### 3.3 基础模型

- 主实验：Mistral-7B-Instruct-v0.2、LLaMA-3-8B-Instruct；
- 泛化实验：Qwen3-8B。

---

## 4. 资源与算力

- **GPU**：2 × NVIDIA A100 80GB；
- **训练时长**（以 LLaMA-3-8B 为例）：重建预训练约 **25 小时**，冲突感知微调约 **3 小时**；
- **超参**：记忆令牌数 K=16；LoRA rank 5（Mistral）/64（LLaMA）/8（Qwen）；批大小 64，最大输入长度 1,024（微调）；
- **推理效率**：CARE 预处理的额外延迟仅约 **0.06 秒/查询**，总计 1.19 秒，显著优于 Priori Judgment（2.10 秒）和 ADA-CAD（1.54 秒）；
- 论文提供了较完整的算力和效率数据。

---

## 5. 实验数量与充分性

### 5.1 实验覆盖

- **主实验**：2 个基础 LLM × 5 个数据集，共 10 组对比实验；
- **附加实验**：Qwen3-8B 上的泛化实验；
- **多上下文实验**：top-3 检索场景的初步评估（见附录 C）；
- **精细评估**：将 NQ 数据分为"韧性"（Resilience，原本回答正确加入上下文后仍正确）和"提升"（Boost，原本错误加入上下文后变正确）两个子集进行分析；
- **消融实验**：覆盖正面/负面上下文、随机负样本、预训练去除、LM 损失去除、KD 损失去除等多个维度；
- **可视化分析**：t-SNE 对比 SFR 与 CARE 对正负上下文的判别能力；
- **案例分析**：展示 TruthfulQA 和 FactKG 上的具体输出样例。

### 5.2 充分性与公平性评价

- 实验设计**比较全面**，涵盖多任务、多模型、多类基线，验证了方法的有效性和泛化性；
- 消融实验设计细致，能清楚分离各组件（预训练、LM 损失、KD 损失、正负样本、难负样本）的贡献；
- 基线复现方面，文中说明了对 RetRobust、CAD/ADACAD、Adaptive-RAG、SKR-KNN、Priori Judgment 均采用官方实现或作者提供的数据，提升了公平性；
- 有一个注意点：部分基线（如 Adaptive-RAG）的标签方案经过了自定义修改，与原始论文不完全一致，但文中给出了说明和理由。

---

## 6. 主要结论与发现

- CARE 在所有评估数据集和三个基础模型上均取得最佳平均性能：相对于 Vanilla RAG，在 Mistral 上平均提升 **5.01%**，在 LLaMA 上提升 **6.13%**，在 Qwen 上提升 **4.9%**；
- CARE 能有效**保持 Resilience**（在冲突上下文存在时仍保留正确的内部知识），同时取得较高的 **Boost**（在参数知识不足时利用外部知识），优于只侧重一面的基线方法；
- 直接微调 LLM（RetRobust、Direct FT）虽然能提升域内 QA 性能，但会导致在长文本问答和事实核查任务上的严重退化（灾难性遗忘），而 CARE 避免了这一问题；
- CARE 的软决策机制优于自适应检索的硬决策方法（如 SKR-kNN、Priori Judgment），能够更充分地利用参数化知识；
- t-SNE 可视化显示 CARE 的记忆嵌入能有效区分可靠与不可靠上下文；
- 额外的 top-3 多上下文实验表明，CARE 可以进一步缓解上下文间的相互矛盾。

---

## 7. 优点

- **方法设计新颖**：将软提示（soft prompting）从"上下文压缩"的用途延伸到"冲突感知"的新场景，通过记忆嵌入同时编码上下文内容及其可靠性，思路巧妙；
- **不修改基础 LLM**：通过 LoRA 仅训练轻量评估器，保留 LLM 的通用能力，规避了灾难性遗忘；
- **训练信号构造合理**：利用闭卷设置的正确性信号自动构造正/负训练对，无需人工标注，具备可扩展性；
- **双重训练目标（LM + KD）**：语言建模保证信息的充分保留，知识蒸馏明确引导"何时依赖外部/内部知识"，互补性强；
- **推断效率高**：预处理的额外开销极小（0.06 秒/查询），推理总延迟接近标准 RAG；
- **分析深入**：包含精细评估、消融、可视化、案例和效率分析，实验证据链完整；
- **跨模型泛化性好**：在 Mistral、LLaMA、Qwen 三种不同架构上均取得一致提升。

---

## 8. 不足与局限

- **仅关注单一冲突类型**：主实验限定在 top-1 检索和单步解码，未充分探索多段落之间的相互矛盾（inter-context conflict）以及推理不稳定导致的内在冲突（intra-memory conflict）。作者在附录中提供了 top-3 的初步实验，但仅作为探索性结果，缺乏深入分析；
- **固定记忆令牌预算**：使用固定 K=16 个记忆令牌编码上下文，对 Wikipedia 这类信息集中的短文本文档有效，但对于需要更多信息量的长上下文或复杂文档，固定容量可能成为瓶颈；如何实现动态分配记忆令牌，仍未解决；
- **闭卷正确性作为知识代理的局限**：以"闭卷回答是否正确"作为判断参数知识是否充足的信号，可能因为生成的不一致性而误判模型真实的知识边界；论文也承认更精确的方法（如多步探测）可以作为改进方向；
- **训练数据规模局限**：微调仅在 NQ 训练集上进行（约 79K 条样本），未使用更大规模或更多样化的训练数据来验证方法的扩展性；
- **单一种子实验**：文中说明所有实验以单一随机种子进行，缺少多次运行的结果和方差报告，统计显著性有待验证；
- **检索文档来源单一**：仅使用了 Wikipedia（ColBERTv2 检索），未覆盖新闻、科学文献、领域知识库等更广泛的 RAG 应用场景；
- **主观性指标局限**：Span EM 和 F1/ROUGE-L 主要衡量词面匹配，对生成质量（如忠实性、逻辑性）的评估不够全面；
- **多轮/复杂推理场景未覆盖**：方法尚未在更复杂的、需要多步推理和推理链条的 RAG 任务中验证。

---

（完）
