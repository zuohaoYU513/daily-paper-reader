---
title: "ClaimVer: Explainable Claim-Level Verification and Evidence Attribution of Text Through Knowledge Graphs"
title_zh: ClaimVer：通过知识图谱实现可解释的声明级验证与证据归因
authors: "Preetam Prabhu Srikar Dammu, Himanshu Naidu, Mouly Dewan, Youngmin Kim, Tanya Roosta, Aman Chadha, Chirag Shah"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.795.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 通过知识图谱进行细粒度声明级证据归因
tldr: 面对社交虚假信息与AI生成文本泛滥，作者提出ClaimVer，在声明粒度上对文本进行验证并通过知识图谱完成证据归因，从而为每条预测提供可解释依据。系统并非黑箱判断，而是尽可能向用户展示做出判断的理由，研究表明这将显著影响用户对自动化系统的信任。ClaimVer为可解释、细粒度的事实核查和证据溯源提供了可行的技术路径。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 735, \"height\": 861, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1575, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 695, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 698, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 702, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 707, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 697, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 702, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 704, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 701, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp795/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1397, \"height\": 2086, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 607, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 1149, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 646, \"height\": 348, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 646, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 789, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 790, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 650, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 792, \"height\": 551, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 662, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp795/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 800, \"height\": 663, \"label\": \"Table\"}]"
motivation: 事实核查需要易于使用且可解释的细粒度证据归因，才能让用户信任自动化结果。
method: 基于知识图谱定位文本中的声明并关联证据，实现声明级验证和证据归因，输出解释信息。
result: 在细粒度验证上提供可解释证据链接，增强用户对系统判断的信任。
conclusion: 以证据归因支撑的声明级验证是提升事实核查可用性和透明度的关键。
---

## Abstract
In the midst of widespread misinformation and disinformation through social media and the proliferation of AI-generated texts, it has become increasingly difficult for people to validate and trust information they encounter. Many fact-checking approaches and tools have been developed, but they often lack appropriate explainability or granularity to be useful in various contexts. A text validation method that is easy to use, accessible, and can perform fine-grained evidence attribution has become crucial. More importantly, building user trust in such a method requires presenting the rationale behind each prediction, as research shows this significantly influences people’s belief in automated systems. Localizing and bringing users’ attention to the specific problematic content is also paramount, instead of providing simple blanket labels. In this paper, we present ClaimVer, a human-centric framework tailored to meet users’ informational and verification needs by generating rich annotations and thereby reducing cognitive load. Designed to deliver comprehensive evaluations of texts, it highlights each claim, verifies it against a trusted knowledge graph (KG), presents the evidence, and provides succinct, clear explanations for each claim prediction. Finally, our framework introduces an attribution score, enhancing applicability across a wide range of downstream tasks.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

虚假信息（misinformation）与恶意的错误信息（disinformation）问题由来已久，而 AI 生成文本工具的普及加剧了这一风险。现有的事实核查方法普遍存在两个缺陷：
- **缺乏可解释性**：大多给出“真/假”式的整体标签（blanket label），用户不清楚判断依据，难以建立对系统的信任。
- **缺乏细粒度（granularity）**：通常在句子或段落层面进行整体验证，无法精确定位文本中具体哪一部分有误，且假设“输入文本与单个参考文本”一一对应，不支持信息分散在多个数据源的情形。

研究表明，向用户呈现每个预测背后的理由（rationale）能显著影响其对自动化系统的信任。因此，论文提出 **ClaimVer**——一个以人为中心（human-centric）的框架，目标是：
- 将输入文本自动拆分为多个声明（claims）；
- 从**知识图谱（KG）**中检索证据三元组，实现**声明级（claim-level）**验证；
- 为每条预测输出**可读的解释**（rationale）与**可验证的证据**，降低用户的认知负担。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

#### 2.1 整体流程

ClaimVer 的流水线分为四大步骤：
1. **预处理（Preprocessing）**：
   - **NER**：识别文本中的命名实体（采用适配 Wiki 实体的工具，并链接到 Wikidata）；
   - **共指消解**：使拆出的声明语义自包含；
   - **KG 实体链接**：标注文本中出现在 KG 中的实体；
   - **分块（Compartmentalization）**：当输入超过上下文长度时进行拆分。

2. **相关三元组检索**：
   - 使用 **Woolnet**（多起点 BFS 算法），在 KG 中检索与当前声明相关的多跳路径三元组；
   - 最大允许 **3 跳**、最多返回 **4 条潜在路径**，以保证三元组相关性。

3. **LLM 微调与声明推理**：
   - 目标函数（objective function）定义为：

     f(input_text, retrieved_triplets) = {(claim_span_i, claim_pred_i, rel_triplets_i, rationale_i)}_{i=1}^{n}

   - 即：模型需同时完成两个子任务：
     - 子任务 1：将输入文本分解为多个文本跨度（claim spans）；
     - 子任务 2：对每条声明给出预测标签、相关三元组和解释理由。

4. **三级标签体系**：
   - **Attributable**：三元组完全支持该声明；
   - **Extrapolatory**：三元组信息不足，无法判断该声明（含“无相关三元组”与“有相关三元组但不够充分”两个情况，分别计分）；
   - **Contradictory**：三元组直接反驳该声明。

5. **评分机制**（用于下游任务）：
   - **Claim Scores（cs）**：为每条声明赋分（Attributable=2；Extrapolatory 且有三元组=1；Extrapolatory 且无三元组=0；无归因=0；Contradictory=-1）。
   - **Triplets Match Score（TMS）**：反映声明与相关三元组的匹配度，采用“语义相似度（SS）”与“实体覆盖率（EPR）”的加权和：

     TMS = α · SS + β · EPR

     （实验取 α=β=0.5）

   - **KG Attribution Score（KAS）**：将 TMS·cs 求和后经**修正 Sigmoid** 压缩至 0~1 区间：

     KAS = σ_mod( Σ_i [TMS_i · cs(y_i)] , γ )

     其中 γ=3（对错误文本惩罚更重，对正确文本奖励较轻）。

#### 2.2 数据集构建

- 选择 Wikidata 作为 KG，从 WikiQA 数据集中保留答案文本（去除问题）；
- 筛选包含至少两个 Wiki 实体的条目（排除依赖问题的单字答案）；
- 使用 **GPT-4 + 人工检查**生成高质量的微调数据与测试标签；
- 最终发布数据集：训练集中 3,400 个样本/5,342 条声明；测试集中 1,000 个样本/1,677 条声明（标签分布见表 1）。

### 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集**：基于 WikiQA 构造的训练/测试集（各 3,400 / 1,000 样本）。
- **评估方法**：模型输出要求“声明文本跨度 + 相关三元组 + 预测标签”三者与 ground truth **完全一致**才算匹配。
- **对比方法**：无传统基线对比；作者对 **8 个不同规模(2B~10B)的开源 LLM** 分别进行 LoRA 微调并进行横向对比：
  - Gemma-2B-IT-Chat、Phi-3-mini-4k-Chat、Zephyr-7B-Beta-Chat、Vicuna-7B-v1.5-Chat、Mistral-7B-v0.3-Chat、Gemma-7B-IT-Chat、Llama3-8B-Chat、Solar-10.7B-Chat。

### 4. 资源与算力

论文**未明确说明所使用的GPU型号、数量及训练时长**。仅可确认：
- 使用 **LoRA + 4-bit 量化**（rank=8，alpha=16）微调模型；
- 上下文长度 4,096 tokens；
- 所有模型训练 **2 epochs** 后收敛。

训练算力的具体细节（如 GPU 数量、总耗时等）在文中并未披露。

### 5. 实验数量与充分性

#### 实验覆盖
- **模型横向对比实验**：8 个不同规模 LLM 在 1,677 条声明上的 ROUGE-L / ROUGE-1 以及 Acc / P / R / F1 对比（见表 3、表 4）；
- **无消融实验**：未对三元组检索算法（如跳数选择）、评分参数（α、β、γ）进行敏感性分析；
- **无基线与 SOTA 对比**：论文属于新任务设定（声明级拆解 + KG 证据归因），因此无传统的端到端 baseline 对照。作者仅在训练数据构造环节提到 GPT-4 的直接输出质量不足（作为间接参照）；
- **人工评测与案例分析**：论文通过 Table 2 的 6 个多主题案例展示系统实际输出（含 KAS 从 0.818 到 0.057 的梯度变化）。

#### 充分性评价
- **优点**：覆盖不同参数规模的模型、报告了多个指标，并提供了人工审阅案例，实验结果有较高说服力；
- **不足**：缺乏消融实验、缺乏与现有事实核查/归因方法（如 FactScore、AIS）在同一任务上的系统对比，评估框架的“一键式”严格匹配也可能低估模型在大语言模型推理上的泛化表现。

### 6. 论文的主要结论与发现

1. **小规模开源模型经微调即可胜任声明级证据归因任务**：性能最好的 Solar-10.7B-Chat 在 1,677 条测试声明中实现 1,031 条完全匹配，精确率/召回率/F1 均达 89% 以上；
2. **模型可以可靠地区分 Attributable / Extrapolatory / Contradictory 三类标签**（各模型的 F1 均高于 74%，最强模型为 89.30%）；
3. **KAS 分数能够有效反映文本整体可信程度**——案例排序显示高 KAS 文本（多 Attributable 声明）与低 KAS 文本（Contradictory）区隔明显；
4. **KG 方法消除了“一个输入对应一个参考文本”的限制**，允许从多个来源汇总事实，做多跳推理验证（如 Airbus 示例综合 3 个三元组支持第 1 条声明）；
5. **模型能够找出 KG 中的具体反例来反驳笼统的否定断言**（如“Boeing 737 从未被西南航空运营”被两条具体 operator 三元组反驳），展示出较强的细粒度核查能力。

### 7. 优点

- **以人为中心的设计**：输出彩色标注的文本跨度、逐条解释、相关实体描述框，极大降低用户的认知负荷；
- **首次将“声明拆解 + KG 证据归因 + 解释生成”整合为统一框架**——对比 AIS（Rashkin et al.）仅限句子级 QA 场景、FactScore（Min et al.）仅计算比例不做解释，ClaimVer 向前推进了一大步；
- **评分机制 KAS 具有向下游扩展性**：可支持排序、过滤、检索增强、模型微调等（连续、区间 0~1、偏向惩罚错误更适合事实核查场景）；
- **公开微调权重与数据集**，便于后续研究，推动领域发展；
- **效率观**：采用 LoRA/4-bit 量化微调中小模型（2B~10B），比直接依赖 GPT-4 更经济实用。

### 8. 不足与局限

- **知识图谱本身局限**：知识覆盖不全、更新滞后导致信息过时；假设 KG“最新且充分”不一定成立；暂不提供传统文章引文（citation）；
- **声明拆解主观性强**：同一文本可能有多样但同样合理的拆解方式（作者在文中也承认此问题，并指出其使自动化评估变得困难）；
- **LLM 推理缺陷**：虽然使用微调后的 LLM 进行声明级推理，仍存在错误推理或幻觉的风险，可通过字符串匹配和人工检查缓解但不能根除；
- **数据集限制**：依赖 WikiQA，主体为 Wikidata 中能用百科三元组回答的声明，对常识推理、多模态文本、时序敏感信息或需更专业领域知识（如医学、法律）的声明适用性可能不足；
- **未提供面向真实场景（如社交媒体帖文、LLM 长文本）的评估**，存在与现实部署之间的 Gap；
- **训练数据生成依赖 GPT-4**，声称经过人工检查保证质量，但仍可能存在 ICL 样本偏差或系统性错误未被完全清除；
- **实验资源信息不透明**，且缺乏完整消融研究和与既有框架的系统性定量比较。

（完）
