---
title: "Follow the Path: Reasoning over Knowledge Graph Paths to Improve Large Language Model Factuality"
title_zh: 沿路径推理：基于知识图谱路径提升大语言模型事实性
authors: "Mike Zhang, Johannes Bjerva, Russa Biswas"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.561.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过将推理轨迹锚定到知识图谱路径来提升LLM事实性
tldr: 针对LLM在复杂开放域问答中推理轨迹事实性不足的问题，提出fs1方法。该方法从大型推理模型获取推理轨迹，并以知识图谱路径为条件进行事实性锚定，微调8个指令微调LLM。在6个基准、2.3万问题的评估中，fs1相比并行采样的指令微调模型提升6-14个绝对点，尤其在多跳复杂问题上提升显著。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 820, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 828, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 458, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 558, \"height\": 238, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1049, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1642, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1639, \"height\": 1228, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1671, \"height\": 965, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1642, \"height\": 1092, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 654, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 813, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl561/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1545, \"height\": 539, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl561/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl561/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 711, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl561/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 529, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl561/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1456, \"height\": 1436, \"label\": \"Table\"}]"
motivation: 大模型推理轨迹常缺乏事实依据，尤其在复杂多跳问题中事实性下降。
method: 用知识图谱路径条件化推理轨迹，微调指令微调LLM以生成事实锚定的推理过程。
result: 在复杂问答基准上显著提升准确率，多跳问题上受益最大。
conclusion: 证明KG路径为基础的事实性锚定能有效提升LLM推理的事实性。
---

## Abstract
We introduce fs1, a simple yet effective method that improves the factuality of reasoning traces by sourcing them from large reasoning models and grounding them by conditioning on knowledge graph (KG) paths. We fine-tune eight instruction-tuned Large Language Models (LLMs) on 3.9K factually grounded reasoning traces and rigorously evaluate them on six complex open-domain question-answering (QA) benchmarks encompassing 23.9K questions. Our results demonstrate that our fs1-tuned model consistently outperforms instruction-tuned counterparts with parallel sampling by 6-14 absolute points (pass@). Our detailed analysis shows that fs1 considerably improves model performance over more complex questions (requiring 3 or more hops on KG paths) and numerical answer types compared to the baselines. Furthermore, in single-pass inference, we notice that smaller LLMs show the most improvements. While prior works demonstrate the effectiveness of reasoning traces primarily in the STEM domains, our work shows strong evidence that anchoring reasoning to factual KG paths is a critical step in transforming LLMs for reliable knowledge-intensive tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

论文标题：**《Follow the Path: Reasoning over Knowledge Graph Paths to Improve Large Language Model Factuality》**（沿路径推理：基于知识图谱路径提升大语言模型事实性）

---

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：大语言模型（LLM）通过“思考”（thinking）或链式推理（CoT）在数学、谜题等复杂任务上表现显著提升，但这类推理技术能否改善**事实性**（factuality），尤其是在**复杂多跳开放域问答（multi-hop QA）**中，仍是一个悬而未决的问题。
- **研究动机**：
  - 多跳问答要求模型综合多条证据、跨多个资源进行推理，对事实性要求极高。
  - 大型推理模型（如 QwQ-32B、DeepSeek-R1）产出的推理轨迹（reasoning traces）虽能给出正确答案，但中间推理过程未必事实正确，存在幻觉风险。
  - 知识图谱（KG）以有向、带标签的图结构编码事实，可作为**可验证的事实基础**来约束和指导推理过程。
- **整体含义**：通过在推理轨迹中注入知识图谱路径，将模型推理“锚定”在事实结构上，有望将 LLM 改造为更可靠的知识密集型任务求解器。该工作提供了在 STEM 领域之外、面向知识密集型 QA 的事实性推理证据。

---

## 2. 方法论：fs1

### 2.1 核心思想
- 从大型推理模型（QwQ-32B 和 DeepSeek-R1）获取原始推理轨迹（rt），再通过**知识图谱（KG）路径**对这些轨迹进行条件化增强，得到 `fs1`（factual simple test-time scaling）训练数据。
- 微调指令微调 LLM，使其学会在推理时“遵循 KG 路径”，从而提升最终答案的事实性和准确性。

### 2.2 关键技术细节

- **原始推理轨迹（rt）构造**：
  - 基于 ComplexWebQuestions（CWQ）开发集（3,519 个问题）。
  - 用 QwQ-32B 和 DeepSeek-R1 查询问题，提取 `<think>...</think>` 内的推理过程，并要求最终答案以 `\boxed{}` 输出。
  - 仅保留最终答案正确的轨迹，共 **3,434 条**。

- **知识图谱增强轨迹（fs1）构造**：
  - 将 CWQ 中的 Freebase 实体对齐到 Wikidata 实体。
  - 提取问题实体与答案实体之间的**最小跳数路径**（1-hop → 2-hop → 3-hop，逐级搜索），作为隐式语义过滤。
  - 多实体问题时，分别查询每个问题实体与答案实体，也联合查询以捕捉多实体路径。
  - 路径以 **“主语—关系—宾语”** 三元组形式线性化，保留语义方向。
  - 将线性化图作为“灵感”注入提示词，引导推理模型重写更可信的推理轨迹，最终得到 **3,886 条** fs1 轨迹。

- **训练目标**：
  - 标准监督微调（SFT）损失，自回归交叉熵：
    \[
    L_{SFT}(\theta) = -\frac{1}{T} \sum_{t=1}^{T} \log p_\theta(y^*_t | x, y_{<t})
    \]
  - 训练超参数：5 epochs、序列长度 8,192、batch size 16、学习率 1×10⁻⁵（余弦调度、5% warmup）、权重衰减 1×10⁻⁴。

- **推理设置**：
  - 原始指令模型：温度 0.7，top_p 0.8；微调模型：温度 0.6，top_p 0.95。
  - 并行采样：每个问题生成 16 次，计算 pass@k（k=1,2,4,8,16）。

---

## 3. 实验设计

### 3.1 基准测试集（Benchmarks）
在 **6 个复杂开放域 QA 数据集**上评估，总计 **23.9K 问题**：

| 数据集 | 说明 | 测试规模 |
|---|---|---|
| CWQ | 基于 Freebase 的复杂多跳问答 | 3.5K |
| ExaQT | 时序知识图谱问答 | 3.2K |
| GrailQA | 带逻辑形式标注的 KG 问答 | 6.8K |
| SimpleQA | 短事实性问答，用于衡量事实准确性 | 4.3K |
| Mintaka | 多语言复杂问答（仅英文子集） | 4.0K |
| WebQSP | 基于 WebQuestions 的 SPARQL 问答 | 2.0K |

### 3.2 对比方法 / Baselines
- **基础模型**：Qwen2.5-72B-Instruct、QwQ-32B、DeepSeek-R1-70B、o3-mini。
- **微调模型**（八种）：
  - Qwen2.5 系列：0.5B、1.5B、3B、7B、14B、32B
  - SmolLM2 系列：360M、1.7B
- **四种设置**：
  1. 零样本直接回答（instruction-tuned）
  2. 零样本 CoT（追加“Think step-by-step”）
  3. 基于 rt 微调
  4. 基于 fs1 微调

### 3.3 评估指标
- 主要采用 **pass@k**（k=1,2,4,8,16），衡量并行采样下的正确生成上界。
- 答案正确性判定采用 **LLM-as-a-Judge**（Llama-3.3-70B-Instruct），判断预测答案与黄金答案是否指向同一真实世界实体；与 gpt-4o-mini 对比差异极小。

---

## 4. 资源与算力

- **API 调用费用**：约 **250 美元**（用于 DeepSeek-R1、o3-mini、gpt-4o-mini 等）。
- **本地训练/推理硬件**：
  - 使用芬兰 LUMI 超算集群，节点内为 **AMD MI250x GPU**（每个节点 8 个 GPU 模块）。
  - 32B 模型训练需 4 节点，推理需 1 节点。
- **总计算量**：约 **6,500 GPU 小时**。
- **环境足迹**：按芬兰绿色能源碳效率估算，约排放 **276 kg CO₂ 当量**。
- **说明**：论文未明确给出每个单一训练任务的具体 GPU 时长，仅提供总体数字。

---

## 5. 实验数量与充分性

- **实验规模**：
  - 在 6 个基准、共 23.9K 问题上进行评估。
  - 8 个不同规模模型 × 4 种设置（inst/cot/rt/fs1），单次推理结果见表 4。
  - 对 Qwen2.5-32B 并行采样至 pass@16，在 6 个数据集上均做了对比曲线（图 5）。
- **消融与分析实验**：
  - **教师模型消融**：分别用 QwQ-32B 和 DeepSeek-R1 的 fs1 子集训练，结果几乎无差异，证明增益来自 fs1 而非教师模型能力。
  - **数据泄漏检查**：计算训练集与测试集之间的余弦相似度、精确匹配，结果显示几乎无重叠，排除数据泄漏。
  - **按问题难度（跳数）分析**：1/2/3/3+ hops。
  - **按答案类型分析**：日期、数字、其他、人物、地点。
  - **按领域分析**：艺术、地理、历史、音乐、政治等 11 个领域。
- **充分性评价**：
  - 实验覆盖面广，控制变量清晰，消融较完整，公平性较好。
  - 但 pass@k 仅是上界，且未引入最终答案选择机制，实际部署效果可能低于所示数字。

---

## 6. 主要结论与发现

1. **并行采样下显著提升**：fs1 微调的 Qwen2.5-32B 在 6 个基准上，pass@16 相比原始指令微调模型提升 **6–14 个绝对百分点**。
2. **复杂问题受益最大**：fs1 在 3 跳及以上的复杂问题上相对改进最大；CoT 和 rt 在简单问题（1–2 跳）上表现更好。
3. **数值答案类型提升明显**：fs1 在数字、日期等答案类型上相对提升最高。
4. **小模型单次推理获益最大**：在 pass@1 设置下，0.5B 级模型相对提升最大（例如 WebQSP +74.6%）；大模型（32B）提升幅度较小，甚至在某些数据集（如 SimpleQA）出现性能下降。
5. **KG 路径而非教师模型是增益来源**：QwQ-32B 与 DeepSeek-R1 作为教师几乎无差异，说明 KG 路径注入本身才是关键。
6. **数据泄漏假设被排除**：训练集与测试集无实质重叠，证明性能提升来自方法而非记忆。

---

## 7. 优点

- **方法简单有效**：无需推理时检索 KG，而是离线生成高质量 KG 增强训练数据，不增加部署成本。
- **可验证性**：KG 路径来自结构化知识库，为推理过程提供可解释、可验证的事实基础。
- **系统性强**：覆盖 360M 到 32B 的多个规模模型，在 6 个基准、23.9K 问题上做大规模评测，并提供多维度分析（跳数、答案类型、领域）。
- **消融严谨**：通过教师模型对比、数据重叠检查等实验，排除了常见混淆因素。
- **资源开放**：公开代码、模型和 3.4K rt + 3.9K fs1 推理轨迹，便于后续研究。
- **角度新颖**：区别于推理时检索增强，将 KG grounding 用于训练数据生成，提升模型内在推理能力。

---

## 8. 不足与局限

- **假设依赖**：假设 KG 路径能改善推理轨迹，但并不能保证中间推理过程完全正确。
- **评估上界问题**：pass@k 是理论上的性能上界，实际应用需要一个选择机制（如投票、验证器），论文未提供该机制的端到端评估。
- **基准时效性**：部分测试数据集较旧，且以英文为主（Mintaka 虽多语言但只用英文），无法完全排除已混入 LLM 预训练数据的风险。
- **LLM-as-Judge 偏差**：用 LLM 判断答案等价性本身有固有局限，尽管作者做了交叉验证。
- **可扩展性受限**：需要 KG 对齐和 SPARQL 路径提取，对于缺乏结构化知识图谱的领域（如开放域长文本）难以直接应用。
- **大模型收益有限**：在 32B 级模型上单次推理提升不显著，甚至出现负优化（如 SimpleQA -10.3%），说明方法对强参数化知识模型的价值可能有限。
- **训练数据规模较小**：仅约 3.9K 条 KG 增强轨迹，可能限制了更复杂推理能力的泛化。

---

（完）
