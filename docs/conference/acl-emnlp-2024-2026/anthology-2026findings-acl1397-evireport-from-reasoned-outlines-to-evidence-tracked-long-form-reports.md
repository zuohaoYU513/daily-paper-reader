---
title: "EviReport: From Reasoned Outlines to Evidence Tracked Long-Form Reports"
title_zh: EviReport：从推理提纲到带证据追踪的长篇报告生成
authors: "Zihan Liu, Jianhui li, Zexin Wang, Fei Sun, Jingjing LI, Zheyuan Li, Ke Xiang, Hang Cui, Houhua Gong, Changhua Pei, Gaogang Xie"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1397.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 证据追踪的长篇报告生成以缓解事实缺失与数字漂移
tldr: 在长篇幅、强证据型报告写作中，大型语言模型一次生成常常会遗漏核心事实、数字漂移并缺少配图，导致结果不可信。作者提出EviReport工作流，把语料证据组织成紧凑可追溯的单元并检索查询相关的子图，再让推理型LLM先规划大纲、对话型LLM细化成层次化提纲，确保报告覆盖完整且证据可追溯。该方法能有效提升事实密集报告的可靠性与定量准确性。该框架虽然并非金融专用，但可直接迁移到依赖证据的摘要和数据到文本场景。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1626, \"height\": 1003, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 189, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1397/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1663, \"height\": 1642, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1617, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 993, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1615, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1714, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1397/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 989, \"label\": \"Table\"}]"
motivation: 解决长报告生成中核心事实遗漏、数字漂移和证据支撑不足导致的不可信问题。
method: 通过可追踪证据单元和查询相关子图检索，结合推理型LLM规划与对话型LLM细化提纲，完成报告写作。
result: 实验表明该流程能显著减少无依据内容、改善报告事实密集度与数字正确性。
conclusion: 将证据组织与大模型规划结合，可提升长报告生成的可信度与可追溯性。
---

## Abstract
Evidence-intensive analytical reports are expected to be fact-dense, quantitatively correct, and supported by figures. Yet one-shot long-form generation with large language models (LLMs) frequently produces fluent but under-supported drafts: core facts are missed, numbers drift, and key visuals are absent, making the report hard to trust. We propose EviReport, an evidence-tracked report-writing workflow that improves reliability by (i) organizing corpus evidence into compact, traceable units and retrieves query-relevant subgraphs into retrieval-ready packages (ii) leveraging a reasoning-focused LLM sketches a high-level plan for full coverage, then a chat-based LLM sharpens it into a detailed hierarchical outline with explicit scope and ordering (iii) rive generation with a facts-first iterative loop: extracting verifiable facts, composing strictly from those facts, then triggering gap-aware append queries to fill missing evidence To evaluate both correctness and completeness, we introduce EviReportBench, a benchmark instantiated on data-rich indicator reports that measures factual accuracy (claim verification), factual coverage (quiz-based evaluation), and visual evidence integration (image recall). Across 8 topics, experiments show that EviReport consistently outperforms strong baselines in factual coverage ( 2.16× ), factual accuracy (+8.9 points), and visual evidence integration (+34 points), approaching the quality of expert-written reports across multiple dimensions.

---

## 论文详细总结（自动生成）

以下是对论文《EviReport: From Reasoned Outlines to Evidence Tracked Long-Form Reports》（ACL 2026 Findings）的详细中文总结。

## 1. 论文的核心问题与整体含义

### 研究动机与背景
- 论文关注**证据密集型长报告生成**（evidence-intensive long-form report generation）任务，典型场景如联合国可持续发展目标（SDG）报告、政策评估报告等。
- 此类报告要求**事实密集、数值准确、量化正确、有图表支撑**，但直接用 LLM 一次性生成长篇报告存在三类典型缺陷：
  1. **事实覆盖率低**：遗漏关键事实，泛泛而谈；
  2. **定量不可靠**：数字错误或缺少时间、单位、口径等限定条件；
  3. **视觉证据缺失**：缺少关键图、表，或图文不对应。
- 上述问题使 AI 生成的报告难以被信任，而现有方法缺乏结构化证据组织、系统化规划和多模态评估，难以诊断和改善。

### 核心解决思路
- 提出 **EviReport** 工作流，将证据组织、两阶段提纲规划和迭代式证据追踪写作结合，提升长报告的正确性、完整性和可视化证据集成能力。
- 同时构建 **EviReportBench** 基准，从事实准确性、事实覆盖率和图像召回三个维度系统评估长报告生成质量。

## 2. 论文提出的方法论

### 总体框架：检索–规划–写作（Retrieve–Plan–Write）

#### (1) 图增强证据检索（KG-RAG）
- 从参考语料构建"证据导向知识图谱"（SDG-KG），实体类型包括：**Goal / Indicator / Case / Dataset / Method**，形成"指标–案例–数据集–方法"的证据链。
- 检索时：对查询进行关键词与语义混合检索 → 找到相关 Case 节点 → 提取实体中心子图（h 跳以内）→ 剪枝 → 用子图生成检索约束 → 检索文本块 → 摘要为紧凑、可追溯的证据包（subgraph + textual summary）。
- 证据包用于后续大纲规划和写作，确保生成内容有据可依、来源可追踪。

#### (2) 两阶段大纲规划（Two-stage Outline Planning）
- **阶段一**：用**推理型 LLM**（reasoning-oriented LLM）基于证据包生成粗略的章节规划，负责全球结构，如背景、数据、方法、结果、贡献、讨论等。
- **阶段二**：用**对话型 LLM**（chat-oriented LLM）将粗略规划细化为小节级层次化大纲，明确每个小节的写作范围、核心内容、顺序及对应证据包。
- 设计动机：全局覆盖与局部细化需要不同能力，单一模型难以同时满足，粗细分离可兼顾完整性和结构性。

#### (3) 证据引导的多模态内容生成（Evidence-guided Multimodal Writing）
- 对每个小节，根据规划上下文检索文本与图像；其中包含**标题引导的图像检索（CGIR）**：从文本证据中提取可能的图题文本，作为辅助查询检索图片。
- 采用三步迭代循环（facts → draft → gap-aware append query），每小节循环最多 T=3 次：
  - **Step 1（事实抽取）**：从检索上下文中抽取可验证的事实列表；
  - **Step 2（基于事实写作）**：仅依据事实列表撰写正文，禁止无依据陈述；
  - **Step 3（缺口感知补检索）**：模型判断现有证据是否不足，若有缺失则生成追加检索查询，并将新证据补充到上下文后再循环。
- 所有子节顺序生成，写作时参考已生成内容以保持全局一致性；最后进行轻量风格统一与润色。

### 评估基准（EviReportBench）
- 面向 SDG 风格指标类报告，从权威来源收集 30 份报告、8 个主题，围绕三个维度：
  - **事实准确性（claim verification）**：抽取独立事实声明，逐一比对证据验证正确率；
  - **事实覆盖率（quiz-based）**：每个主题构造 40 道测验题，用 LLM 基于生成报告作答，计算可答率与正确率；
  - **图像召回（image recall）**：以专家报告中的关键图片为 ground truth，计算生成报告中覆盖的比例。

## 3. 实验设计

### 使用的数据集/场景
- SDG 相关研究报告及技术文档：
  - 109,731 篇 SDGs 相关研究论文；
  - 14 份 CBAS（2019–2025）可持续发展报告；
  - 3 份"一带一路"可持续发展报告（2020–2022）；
  - 687 份联合国及国际组织/政府文件。

### Benchmark 主题（8 个）
- 覆盖多种 SDG 目标，如：全球农田变化、非洲粮食生产区、湖泊藻华、建筑电气化、夜间灯光、热浪变化、印度支那水稻种植等。
- 每个主题对应一份权威专家撰写报告及代表图。

### 对比方法/基线
- **Naive_RAG**：普通 RAG 直接生成；
- **ReAct_RAG**：ReAct 式工具调用 agent；
- **WriteHERE**：自适应长文本写作框架；
- **Coze**、**OpenAI Deep Research**、**Gemini Deep Research**：商用/搜索型深度研究平台；
- 此外，EviReport 还测试了不同 backbone LLM（GPT-5、Gemini-2.0-flash、Claude-sonnet-4、DeepSeek-v3.1）。

### 是否说明资源/算力
- 论文主体及附录主要在描述方法、系统和实验，**未明确报告 GPU 型号、数量、训练时长或推理总算力**。
- 只是说明使用 bge-large-en-v1.5 作为 embedding 模型，DeepSeek-V3、GPT-5 作为生成/规划 LLM，Qwen-Max 作为验证模型；但**未给出可复现的硬件配置与训练成本细节**。

## 4. 资源与算力
- **未具体披露实验所用 GPU/TPU 资源、节点数、训练时间、API 调用次数**。
- 仅在实现部分注明嵌入模型和生成模型的选择，但对算力与能源成本没有量化说明。
- 对于这类依赖多次外部 LLM 调用（生成、验证、评分）的工作，**算力消耗较高**；论文缺少该方面透明度，可能影响可复现性和公平性评估。

## 5. 实验数量与充分性分析

### 实验数量
- **主实验**：8 个主题上，对比 7 种方法 × 3 类指标（事实准确性、覆盖率、图像召回），结果见 Table 1。
- **消融实验**（Table 2）：
  - 去除知识图谱（w/o KG）；
  - 去除事实抽取（w/o Fact Extraction）；
  - 去除标题引导图像检索（w/o CGIR）。
- **额外分析**：
  - 迭代次数 T = 1–5 的影响（Table 4）；
  - 不同 backbone LLM 变体（Table 5）；
  - 逐主题雷达图（8 个主题 × 4 指标）；
  - 图像精确率与图文语义一致性评估（3 个 VLM 评审，1–5 分，Table 6）。

### 充分性与公平性评价
- **优点**：
  - 三个评测维度覆盖了"正确/完整/视觉整合"，比单一文本质量评测更有诊断价值；
  - 消融实验针对各模块逐步验证，能较清晰归因；
  - 对 OpenAI_DR/Gemini_DR/Coze 不计算图像召回的原因做了说明（数据语料不同），处理较为诚实；
  - 多 backbone 泛化测试显示稳定，胜出并非依赖单一模型。
- **不足**：
  - 论文未给出报告长度、生成词数、事实抽取数量等基础统计，影响可比性；
  - 宣传“2.16×覆盖率提升”实际是绝对值较小（0.396 vs 0.183），但性能提升的绝对幅度有限；
  - 事实验证依赖 Qwen-Max 联网搜索，本质上是 LLM 判断，可能有系统性偏差；
  - 测试主题数仍偏少（8 个），且集中于 SDG 领域，对跨领域一般性结论而言样本尚不充分。

## 6. 论文的主要结论与发现

- EviReport 在所有指标上显著优于强基线：
  - 事实准确的正确率从最强 ReAct-RAG 的 0.8311 提升至 **0.9687**（+8.9 分）；
  - 事实覆盖 Overall Score 为 **0.3963**（约为 ReAct-RAG 的 2.16 倍）；
  - 图像召回达到 **0.79**（对比 Naive_RAG/ReAct_RAG +34 个点）；
  - 提取的核验正确事实数量最多（**78.5**），显示不仅能减少幻觉，还能增加信息密度。
- 知识图谱结构对覆盖率贡献极大——移除后覆盖率几乎减半，说明显式"指标–案例–数据集–方法"链条对组织证据至关重要。
- 两阶段规划比单一模型规划更好：仅用对话型或推理型模型都会在覆盖率/准确率之间牺牲一个维度。
- 标题引导的图像检索不仅能提升图像召回，还能辅助文本事实准确性，呼应图文多模态证据的互补性。
- 迭代“事实→草稿→追加查询”过程在 T=3 时达到最佳性价比；继续增加迭代虽可稍提高事实数但准确率下降。
- 系统已接近专家撰写报告的质量（在多个维度）——是证据型长报告自动化的一步实用化探索。

## 7. 优点
- **新颖且场景真实**：从 SDG 报告这个高度证据密集、数据密集、图表密集的应用场景切入，对系统提出了远超“流畅文本”的要求，具有很强现实意义。
- **完整的工作流设计**：将知识图谱、两类 LLM 的分工（推理型/对话型）、迭代补检索、图文结合统一成一个端到端框架，设计合理且可解释。
- **多维评测**：不只是自动打分的“幻觉指标”，而是设计了面向读者回答的测验式覆盖率评价，更接近真实阅读使用场景。
- **可视化与可追溯**：证据包（图+摘要）支持来源追溯，满足证据密集型报告的实际需求。
- **消融完整、控制细致**：对图谱、事实抽取、CGIR、迭代次数、backbone 等都做了系统性的分析，可信度较高。
- 公开了评测构建与打分代码（GitHub），有助于后续复现与扩展。

## 8. 不足与局限
- **缺乏算力与成本披露**：未给出 GPU 类型/数量/训练时间，也未评估 API 调用总成本，实际落地门槛未知。
- **测试领域较窄**：基准集中于 SDG 指标报告，虽声明“domain-agnostic”，但缺少政策分析、科学调研、工业分析等跨领域验证，泛化结论尚有保留。
- **LLM 评测误差风险**：事实校验和 quiz 作答都依赖 LLM 自主判断，可能产生与事实无关的“礼貌妥协”；不同检查器间一致性未作充分讨论。
- **更新滞后**：系统无法实时获取最新外部数据，不能计算最新指标值；未来需集成多智能体数据平台。
- **仍可能产生幻觉或不精确表述**；知识图谱构建本身依赖 LLM 抽取，会引入错误传播。
- **图像召回的评价过于宽松**：仅判断 ground-truth 图片是否“出现”，未考虑图片重复、缩放、能否读懂等细节；不同来源图的差异也未仔细考虑。
- **系统复杂，依赖多个专用组件**：通用性尚待证明，替换到新领域需要重新构造知识图谱/检索库，成本不低。
- **用户风险提醒不足**：文章虽写明需人工核验，但对高利害场景的潜在误用讨论较少，伦理部分略显简短。

（完）
