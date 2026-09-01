---
title: "FactBench: A Dynamic Benchmark for In-the-Wild Language Model Factuality Evaluation"
title_zh: FactBench：野外语言模型事实性评估的动态基准
authors: "Farima Fatahi Bayat, Lechen Zhang, Sheza Munir, Lu Wang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1587.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向真实世界交互的LM事实性评估基准，识别幻觉提示
tldr: 针对语言模型在真实交互中事实性评估困难的问题，提出VERIFY证据评估管道和FactBench基准。VERIFY基于网络检索证据将生成内容单元分为支持、不支持或无法判定，其判定的相关性优于现有方法。通过识别高频引发事实错误的幻觉提示，构建了覆盖150个主题的1000条提示数据集，为事实性评测提供了动态资源。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1575, \"height\": 711, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 565, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1563, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 768, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1482, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 718, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1587/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1563, \"height\": 1929, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1015, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1507, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1318, \"height\": 646, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 740, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1369, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 630, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1658, \"height\": 1428, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1587/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1570, \"height\": 908, \"label\": \"Table\"}]"
motivation: 现有事实性评估方法难以应对真实世界用户交互中的多样内容。
method: 提出VERIFY管道，基于Web检索证据对内容单元进行支持性分类，并构建FactBench提示集。
result: VERIFY的事实性判断与人类评估相关性更强，FactBench包含1000条跨150个主题的提示。
conclusion: 为野外场景下的LLM事实性评估提供了新基准和方法。
---

## Abstract
The rapid adoption of language models (LMs) across diverse applications has raised concerns about their factuality, i.e., their consistency with real-world facts. We introduce VERIFY, an evidence-based evaluation pipeline that measures LMs’ factuality in real-world user interactions. VERIFY considers the verifiability of LM-generated content and categorizes content units as Supported, Unsupported, or Undecidable based on Web-retrieved evidence. Importantly, factuality judgment by VERIFY more strongly correlates with human evaluations than existing methods. Using VERIFY, we identify “hallucination prompts,” i.e., those that frequently elicit factual errors in LM responses. These prompts form FactBench, a dataset of 1K prompts spanning 150 topics and tiered into Easy, Moderate, and Hard prompts. We benchmark widely-used openweight and proprietary LMs from six families, yielding three key findings: (i) LMs’ factual precision declines from Easy to Hard prompts, (ii) factuality does not necessarily improve with scale; Llama3.1-405B-Instruct performs comparably to or worse than its 70B variant, and (iii) Gemini1.5-Pro shows a notably higher refusal rate, with over-refusal in 25% of cases.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 语言模型（LM）在真实世界应用中广泛部署，但其**事实性（factuality）**问题突出，即模型可能生成与真实世界事实不一致或无法验证的内容（幻觉）。
- 现有长文本事实性评估基准存在明显不足：
  - **静态设计**：容易被数据污染（data contamination）影响。
  - **覆盖范围窄**：如 FactScore 局限于传记问答、ExpertQA 依赖专家领域问题、LongFact 由 LM 生成提示而非用户驱动。
  - **缺乏真实世界适用性**：多数基准使用人工筛选或 LM 生成的查询，不能反映真实用户的交互模式。
- 为此，论文提出两个核心贡献：
  - **VERIFY**：基于证据检索的事实性评估管道，将 LM 生成内容分解为内容单元，并依据 Web 检索证据标注为 Supported、Unsupported 或 Undecidable。
  - **FactBench**：一个动态、真实世界来源的基准数据集，包含 1000 条提示、覆盖 150 个主题，按难度分为 Easy、Moderate 和 Hard 三档，用于持续评测 LM 的事实性表现。

## 2. 论文提出的方法论

### 2.1 整体框架

论文采用两步流程：

1. **Step 1（Collect）**：从 LMSYS-Chat-1M 真实用户对话数据中挖掘**可验证且有用**的提示。
2. **Step 2（VERIFY）**：对 LM 的响应进行细粒度事实性评估，计算幻觉分数，用于筛选“幻觉提示”并构建 FactBench。

### 2.2 提示收集（Prompt Harvesting）

- **数据清洗**：从 LMSYS-Chat-1M 中抽取首轮用户提示，通过 Llama3-70B-Instruct 检测英语提示，去除匿名化（30.9%）、去重（12.1%）以及 Jaccard 相似度 > 0.9 的提示，最终得到 294,333 条不同提示。
- **聚类**：使用 BERTopic（结合 OpenAI text-embedding-3-small 嵌入、UMAP 降维、HDBSCAN 聚类），识别出 142,702 条离群提示并剔除，最终得到 382 个主题簇；每个簇用 c-TF-IDF 选 top 100 代表提示，并用 GPT-4 Turbo 汇总为简短主题。
- **可验证性分类**：使用 Llama3-70B-Instruct 将提示分为 Factual / Faithful / Neither，其中 45.8% 的提示被判定为可验证（Factual 或 Faithful）。
- **有用性评估**：采用 GPT-4-Turbo 和 Llama3-70B-Instruct 两个模型，对提示在四个标准（清晰性、泛化性、相关性、可行性）上独立打分（0-5），取平均得到有用性分数 S(P)：

  \( S(P) = \frac{1}{|C|} \sum_{c \in C} \sum_{m \in M} S_m(c) \)

  其中 C 为四个标准集合，M 为两个评估模型集合。

### 2.3 VERIFY 事实性评估管道

VERIFY 包括五个关键组件：

1. **单元提取与标注（Unit Extraction & Labeling）**：
   - 使用 Llama3-70B-Instruct 将响应分解为内容单元，类型包括 Fact、Claim、Instruction、Data Format、Meta Statement、Question 等。
   - 只有 Fact 和 Claim 进入后续验证流程。
2. **单元去语境化（Unit Decontextualization）**：
   - 基于“分子单元”（molecular units）思想，对每个可验证单元进行最小化修改，使其自包含、可独立验证，解决指代不清、上下文缺失等问题。
3. **查询生成与证据检索（Query Generation & Evidence Retrieval）**：
   - 使用 SerperAPI 进行 Google Search 检索。
   - 采用**交互式查询优化**：迭代生成查询 → 检索 → 评估检索片段与目标单元的相关性 → 改进查询，共执行 5 轮迭代。
4. **最终判定（Final Answer Generation）**：
   - 使用 Llama3-70B-Instruct 作为裁判模型，通过 Chain-of-Thought 推理，对每个单元判定为：
     - **Supported**：证据支持。
     - **Unsupported**：证据矛盾。
     - **Undecidable**：证据不足、语境缺失或无法验证。
5. **幻觉分数（Hallucination Score）**：

   \( H(R) = \frac{|U_S| + \alpha |U_D|}{\sqrt{|V|}} \)

   - \( U_S \)：Unsupported 单元集合；\( U_D \)：Undecidable 单元集合；\( V \)：所有可验证单元集合。
   - \( \alpha \in (0,1) \) 控制 Undecidable 的权重，论文通过人工分析 100 条响应、570 个 Undecidable 单元，发现 57% 为事实性内容，因此取 α = 0.5。
   - 分母使用 \( \sqrt{|V|} \) 使分数对长文本响应中的错误保持敏感性。

### 2.4 FactBench 构建与更新

- 基于响应 LM 的能力（按 Chatbot Arena 排名）将提示分为 Hard、Moderate、Easy 三档，并设置不同有用性阈值（Hard: 4.0, Moderate: 4.5, Easy: 5.0）。
- 从 70K 候选提示中筛选出 4.2K 提示，最终选取 top 1K 提示，保持原始档位比例：532 Hard、332 Moderate、136 Easy。
- FactBench 可通过定期纳入 LMSYS-Chat-1M 新数据及 WildChat 数据实现更新。

## 3. 实验设计

### 3.1 使用的数据集与基准

- **来源数据**：LMSYS-Chat-1M（大规模真实用户-LM 对话数据）。
- **FactBench 基准**：1000 条提示，覆盖 150 个主题，按易到难分为 Easy（136 条）、Moderate（332 条）、Hard（532 条）。
- 主题分布示例：旅行行程（8.9%）、医疗问题（6.5%）、食谱请求（4.9%）、LM 应用（2.9%）、GPU 推荐（2.1%）、游戏比较（2.1%）等。

### 3.2 评测模型

- **专有模型**：GPT-4o、Gemini1.5-Pro、Claude-3.5-Sonnet、Command R+。
- **开放权重模型**：Llama3.1-70B-Instruct、Llama3.1-405B-Instruct、Mistral-Large-2。

### 3.3 对比方法（Baselines）

- **FactScore**：将文本分解为原子事实，用 Wikipedia 检索验证。
- **SAFE**（Search-Augmented Factuality Evaluator）：原子事实分解 + Google Search 证据检索。
- **FactCheck-GPT**：多步标注管道，使用 GPT-3.5 作为骨干，进行 claim 分解、去语境化、证据检索和事实判定。
- 所有 baseline 使用 gpt-3.5-turbo-0613 作为骨干 LM。

### 3.4 人类评估

- 从 FactBench 中随机抽取 40 条提示，覆盖不同主题。
- 4 个模型（GPT-4o、Gemini1.5-Pro、Llama3.1-70B、Llama3.1-405B）对 40 条提示生成响应，共 160 条响应。
- VERIFY 将响应分解为 4,467 个内容单元，由两位标注者独立评估：
  - 单元独立性（Independent vs Dependent），Cohen's Kappa = 0.53，独立一致率 82.6%。
  - 事实性（Factual vs Other），Cohen's Kappa = 0.57，一致率 85.9%。
- 另取 48 条响应（每模型 12 条）进行人工单元穷举提取，用于计算 VERIFY 的召回率。

## 4. 资源与算力

- 论文**未明确说明**所使用的 GPU 型号、数量或训练时长。
- 提及以下模型用于管道各环节：Llama3-70B-Instruct（单元提取、去语境化、查询生成、裁判）、GPT-4 Turbo（有用性评分、拒绝分类）、GPT-3.5-turbo（baseline 骨干）、text-embedding-3-small（嵌入）。
- 检索依赖 SerperAPI（Google Search API）。由于未报告具体硬件配置和推理成本，无法评估其算力投入。

## 5. 实验数量与充分性

### 5.1 实验组数

- **主实验**：7 个模型在 FactBench 三档（Easy/Moderate/Hard）上评测，报告 Factual Precision 和 Hallucination Score。
- **方法对比**：VERIFY 与 FactScore、SAFE、FactCheck-GPT 在四模型（GPT-4o、Gemini1.5-Pro、Llama3.1-70B、Llama3.1-405B）上的对比。
- **人类相关性分析**：40 条提示、160 条响应、4,467 个单元，人工标注后计算准确率、平衡准确率、Pearson/Spearman 相关。
- **α 敏感性分析**：在 α ∈ {0.1, 0.2, ..., 1.0} 下重复提示选择，计算与前一 α 的重叠率。
- **召回率小规模分析**：48 条响应，计算 VERIFY 单元提取的 macro-average recall。
- **拒绝率分析**：不同模型在三个档位上的拒绝率及拒绝原因分类。
- **定性案例分析**：对 Llama3.1-405B 与 70B 的 30 个差异最大案例进行人工审查，并使用主观性分类模型验证。

### 5.2 充分性与公平性

- **优点**：实验覆盖多种模型家族（开放权重 + 专有）、多档难度、多种评估方法，且与人类标注进行了多重相关性验证；默认考虑模型拒绝（refusal）的影响；对 α 进行敏感性分析。
- **不足**：
  - 人类评估仅覆盖 40 条提示，样本量偏小。
  - baseline 的单元粒度与 VERIFY 不同，虽采用统一单元作为输入，但不同方法的内部机制仍可能影响结果公平性。
  - 召回率实验仅基于 48 条响应，规模有限。
  - 未提供置信区间或显著性检验，实验结果的统计稳健性难以判断。

## 6. 论文的主要结论与发现

1. **VERIFY 与人类判断相关性最强**：
   - 在事实单元上 Pearson 相关达 0.97，非事实（Other）单元上 0.73，均高于 FactScore、SAFE 和 FactCheck-GPT。
   - 在平衡准确率上比现有方法平均高 15.7%。
2. **从 Easy 到 Hard，事实性显著下降**：所有模型在 Hard 档上的 Factual Precision 均明显低于 Easy 档。
3. **事实性并非随规模增加而必然提升**：
   - Llama3.1-405B-Instruct 的表现与 70B 版本相当或更差；405B 产生更多 Undecidable 单元，原因在于其回答中更多使用主观修饰词（如“solid”、“exclusive”），从而导致更严格的 VERIFY 无法判定。
4. **Gemini1.5-Pro 拒绝率显著偏高**：
   - 在 Hard 档拒绝近 10% 的提示，但其中 25% 为过度拒绝（例如将“COVID 疫苗间隔研究”误判为医疗建议）。
   - 49% 的无效拒绝源于“misinformation risk”担忧，29% 源于高估伦理/法律风险。
5. **FactCheck-GPT 的总体准确率虽高，但依赖内部参数知识**，对未见过或更新信息不可靠；VERIFY 采用证据驱动的严格判定，更稳健。

## 7. 优点

- **真实世界来源**：提示数据来自 LMSYS-Chat-1M，比人工或 LM 生成的查询更贴近实际应用。
- **动态更新机制**：FactBench 设计为可定期更新，缓解静态基准的数据污染问题。
- **细粒度的可验证性处理**：区分 Fact/Claim、去语境化、引入 Undecidable 标签，比二元判断更符合人类核查逻辑。
- **相关性验证充分**：同时使用准确率、平衡准确率、Pearson/Spearman 相关评估方法的人类一致性，多角度证明 VERIFY 的有效性。
- **考虑了拒绝行为**：将模型的拒答率及其合理性纳入分析，揭示了评估中易被忽视的因素。
- **开放资源**：发布 human annotations（4,467 个单元），便于后续研究。

## 8. 不足与局限

- **单模型依赖**：VERIFY 使用单一 LM（Llama3-70B-Instruct）完成分解和标注，可能引入模型偏差；虽然提到可扩展多模型，但未实际验证。
- **无召回率保障**：对开放式查询，无法穷举所有相关事实，无法测量评估的召回率；论文中的召回率分析仅基于 48 条响应，规模不足。
- **人类评估规模小**：40 条提示的样本难以代表 FactBench 全部 1000 条的多样性。
- **单元粒度差异**：不同评估方法提取单元的粒度不同，统一输入单元后仍可能存在方法内部不一致；直接跨方法比较可能具有误导性。
- **未报告算力与成本**：缺少模型调用的计算资源、时间与经济成本细节，难以复现总成本。
- **静态评估的局限性**：VERIFY 依赖 Google Search 的实时证据，检索质量与搜索引擎本身相关，可能随环境变化产生波动。
- **未考虑单元间的逻辑一致性**：仅验证单个事实的支持程度，未检查响应整体的连贯性。
- **主观性处理偏向保守**：VERIFY 对带主观修饰的单元倾向标记为 Undecidable，可能导致对风格化回答的误判，如 Llama3.1-405B 的表现低于实际事实性。

（完）
