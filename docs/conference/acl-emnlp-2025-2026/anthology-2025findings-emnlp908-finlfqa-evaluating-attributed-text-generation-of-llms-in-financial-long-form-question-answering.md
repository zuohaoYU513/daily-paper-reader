---
title: "FinLFQA: Evaluating Attributed Text Generation of LLMs in Financial Long-Form Question Answering"
title_zh: FinLFQA：大语言模型金融长文问答的归因文本生成评估
authors: "Yitao Long, Tiansheng Hu, Yilun Zhao, Arman Cohan, Chen Zhao"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.908.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 面向金融长文问答的归因文本生成与幻觉评估基准
tldr: 针对金融应用中LLM长文回答易幻觉且现有归因基准过于简单的问题，提出FinLFQA基准。该基准通过人工标注评估三个方面：支持证据抽取、归因相关性和归因充分性，强调归因不仅是参考检索。在复杂金融问题上的评估揭示了LLM在细粒度归因上的不足，为金融场景的幻觉缓解提供了评测基础。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp908/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 833, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp908/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 925, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp908/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1602, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp908/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1556, \"height\": 2445, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 635, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1565, \"height\": 1260, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1482, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1457, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1679, \"height\": 427, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1563, \"height\": 1269, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1309, \"height\": 1508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1309, \"height\": 1508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1605, \"height\": 1191, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp908/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1556, \"height\": 2445, \"label\": \"Table\"}]"
motivation: 金融领域LLM长文问答幻觉严重，且现有归因基准忽略细粒度归因。
method: 构建FinLFQA基准，通过人工标注评估支持证据、归因相关性和充分性。
result: 发现LLM在细粒度归因上表现不足，为金融幻觉研究提供评测方法。
conclusion: 强调金融场景归因应超越参考检索，为可信金融LLM开辟评估方向。
---

## Abstract
Large Language Models (LLMs) frequently hallucinate to long-form questions, producing plausible yet factually incorrect answers. A common mitigation strategy is to provide attribution to LLM outputs. However, existing benchmarks primarily focus on simple attribution that retrieves supporting textual evidence as references. We argue that in real-world scenarios such as financial applications, attribution goes beyond reference retrieval.We introduce FinLFQA, a benchmark designed to evaluate the ability of LLMs to generate long-form answers to complex financial questions with reliable and nuanced attributions. FinLFQA evaluates three critical aspects of attribution through human annotations: (1) supporting evidence extracted from financial reports, (2) intermediate numerical reasoning steps, and (3) domain-specific financial knowledge that informs the reasoning process.We further provide an automatic evaluation framework covering both answer quality and attribution quality. Through extensive experiments on eight LLMs across multiple attribution-generation paradigms, we find that fine-grained metrics are important to distinguish model capabilities, that end-to-end generation achieves comparable performance to post-hoc approaches, and that iterative refinement only helps when guided by external feedback.

---

## 论文详细总结（自动生成）

# FinLFQA：大语言模型金融长文问答的归因文本生成评估（论文总结）

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLMs）在长文问答（LFQA）任务中频繁产生幻觉，生成看似合理但事实错误的答案。传统缓解策略是提供归因，但现有归因基准（如 ALCE）主要关注单一维度的“证据检索/引用”，即从源文档中找出支撑段落，这在真实金融应用中远不够充分。
- **金融领域的特殊性**：金融文本富含数值数据，可靠结论不仅需要指出证据来源，还需要（a）精确执行数值推理并展示中间步骤（如通过可执行代码），（b）整合领域特定的金融专业知识（如损益表、递延税负债等概念），才能得到可验证、可信的答案。
- **论文主张**：归因在金融场景中应超越参考检索，涵盖 **支持证据、中间数值推理步骤、领域专业知识** 三个维度。
- **整体含义**：该工作填补了金融领域归因文本生成评估基准的空白，为构建可信、可验证的金融长文问答系统提供了评测基础和方向指引。

## 2. 方法论

### 2.1 FinLFQA 基准构建（任务定义）

- 给定两家公司的财务报告文档集 `D`（文本+表格段落）和查询 `q`，模型需生成由 n 个语句 `s1, s2, …, sn` 构成的回答 `R`。每个语句 `si = (ti, Ci, Pi, Ki)`，其中：
  - **ti**：一个独立陈述子句；
  - **Ci**：支持该陈述的证据段落索引列表；
  - **Pi**：包含数值推理的 Python 代码（如可用）；
  - **Ki**：使用的专业知识条目索引。
- 最优响应建模为 `R* = argmax_R P(R | q, D, K)`。

### 2.2 数据构建流程（三阶段）

1. **报告选择（Report Selection）**：基于 SIC 行业代码选取同行业公司对（如 CWT 与 AWK），获取同一财季的 10-Q 报告，保证行业可比性与时间一致性。
2. **问答标注（Question & Answer Annotation）**：标注者从报告中识别数值内容和重叠信息，撰写需跨公司、多源推理的计算型问题，优先涵盖跨公司比较、表格与文本融合、时间趋势推理（如同比变化）、衍生指标计算等；回答被拆分成语义完整的子句，并逐句标注证据和计算步骤。
3. **归因标注（Attribution Annotation）**：金融专家验证并拆分语句为带证据的子句；从 Wikipedia 知识库中随机采样 20 条金融概念，标注每子句是否使用相关专业知识；将已验证的计算转换为结构化 Python 函数，用于可复现性验证。

### 2.3 自动化评估系统

- **LLM-as-Judge 答案评估**：使用 GPT-4o 结合报告全文、问题、生成答案和参考答案，从三个维度打分（1–5 分/维度，总分 3–15）：
  - **准确性（Accuracy）**：是否正确回答问题并与参考答案一致；
  - **数值正确性（Numerical Correctness）**：所有数值计算是否准确；
  - **证据蕴含（Evidence Entailment）**：所有主张是否被报告内容充分支撑。
- **数值推理评估**：从参考答案和生成答案中提取数值集合，计算精确率（Precision）、召回率（Recall）和 F1；并采用**容差匹配**（相对误差 0.01 内算对）与**单位归一化**（如 3 million 与 3,000,000 等价）。
- **细粒度归因评估**：
  - **证据（Evidence）**：计算证据引用精确率、召回率和 F1；
  - **代码（Code）**：统计 Python 代码片段的**执行成功率**；
  - **专业知识（Professional Knowledge）**：使用基于召回率的评估衡量专业知识识别的完整度。

### 2.4 三种归因生成范式

- **Post-hoc Generation**：两阶段流程，第一阶段生成答案，第二阶段根据答案生成三种归因；提示词分别如图 3、图 4。
- **End-to-end Generation**：单次生成回答子句及其三种归因；提示词如图 5。
- **Iterative Refinement**：初始生成后，模型提取并执行代码块，基于四个标准（完整性、证据支撑、数值一致性、专业知识整合）自我评估并迭代改进；在迭代中加入外部反馈（如更强模型或领域微调模型 Fino1-8B 的指导）。

## 3. 实验设计

- **Benchmark**：FinLFQA 数据集，包含 **1,008 个专家标注实例**，按 7:3 划分为测试集（706 个）与开发集（302 个），答案不公开以在线评估平台形式供评测。
- **数据统计**：平均问题长度 16.3 词，回答长度 52.4 词，报告约 2221.6 词（约 40.5 个段落），单实例平均涉及 2.9 条证据、1.1 个代码、1.2 条专业知识。
- **评估模型**：8 个 LLM——GPT-4o（闭源）、Qwen2.5-72B、Llama-3.3-70B、Llama-3.2-3B、Llama-3.2-1B、Mistral-Small-24B、Mistral-8x22B、Phi-4（开源主力模型，覆盖小到大规模）。
- **对比方法**：三种归因生成范式（post-hoc、end-to-end、iterative refinement）。
- **评估指标**：传统表面指标（ROUGE-L、BERTScore）+ 细粒度指标（LLM-as-Judge 15 分制、数值精确率/召回率/F1、证据 F1、代码执行成功率、知识召回率）。
- **辅助实验**：迭代细化在不同反馈来源下的消融分析，包括 Llama-3.1-8B 结合 Fino1-8B 金融领域反馈，以及小模型接受大模型反馈的实验。
- **人类评估**：随机抽取 50 个样本，由两名金融背景标注者独立评分，验证自动化评估系统的可靠性。

## 4. 资源与算力

- **论文未明确说明**具体 GPU 型号、数量或训练时长。仅在致谢中提到使用了 NYU IT 高性能计算（HPC）资源；实验使用 vLLM 框架部署开源模型，所有推理为零样本（temperature=1.0，最大输出 2048 tokens）。

## 5. 实验数量与充分性

- **实验组数**：较充分——8 个模型 × 3 种范式在开发集和测试集上的系统性评估（主结果两张表）；另含 3 组迭代细化外部反馈消融实验、50 样本的人机评估相关性验证、50 个失败代码案例的人工分析、150 个输出（3 种设置 × 50 样本）的错误分析。
- **充分性评价**：
  - **优点**：覆盖模型层级广（1B 到 72B，开源到闭源），维度多（答案质量、数值、证据、代码、知识全链路评估），且开发集与测试集双验证。
  - **局限性**：代码执行成功率的显著提升仅体现在迭代细化场景，评估集本身全部来自美国上市公司 10-Q 报告和同行业两两配对结构（公司数量有限）；GPT-4o 作为评估者存在少数维度（如 evidence entailment 相关系数仅 0.630）与人类判断相关度偏低的偏差风险。

## 6. 主要结论与发现

- **GPT-4o 总体领先**：在 LLM-as-Judge（13.7/15）、数值准确性（F1 42.3）和代码执行成功率（29.8%）上均最优；但开源模型（Qwen2.5-72B、Llama-3.3-70B、Mistral-Small-24B）已具备相当竞争力。
- **细粒度指标比传统指标更重要**：所有模型 BERTScore 接近（≈88 分），ROUGE 普遍偏低，无法体现模型差异；只有结合数值匹配、证据 F1 等细粒度指标才能有效区分模型能力。
- **Post-hoc 与 End-to-end 无显著差异**：端到端生成在性能上与两阶段方法持平，且计算成本更低、代码生成一致性更好。
- **迭代细化（self-feedback）无显著增益**：与已有研究一致，模型自我反馈无法改进推理表现；仅在代码执行成功率上有提升（因执行结果提供了显式纠错信号）。
- **外部反馈需模型具备足够能力**：Llama-3.2-3B 能从 Llama-3.3-70B 反馈中受益，而 1B 模型受益有限；**领域专精反馈更有效**，如 Fino1-8B（金融 RL 微调）对 Llama-3.1-8B 的改进超过了同架构通用模型。
- **主要错误类型**：证据归因错误（25%）、代码执行错误（22%）、数值提取与计算错误（20%）、知识验证错误（15%）、流畅性/事实一致性/推理错误（12%）、其他（6%）；其中代码错误主要是缺参数调用（46%）、缺 return 语句（20%）和缩进错误（16%）。

## 7. 优点

- **全新的三维归因框架**：首次将“证据、数值推理（代码）、专业知识”整合进金融长文问答基准，归因粒度细到子句级别，较 ALCE 的粗粒度归因更贴近金融实际应用。
- **高质检的人工标注**：11 位具备金融行业经验或金融专业背景的标注者参与，包含双重验证（质量检查和专家复核），问题设计强调跨公司比较、时间推理和衍生指标计算，难度和多样性可控。
- **自动化评估体系全面**：将 LLM-as-Judge、模糊数值匹配（容差+单位归一化）、代码运行验证和证据/知识召回结合，形成了金融归因多维度评测闭环；还专门做了人机评分相关性验证。
- **实验设计周密**：对三种主流归因生成范式进行了系统对比，并额外验证了自反馈、跨模型反馈和领域反馈三种迭代细化策略，结论对部署路径有实用参考价值。
- **提供公开评测平台**：测试集答案不公开、提供在线排行榜，降低了数据污染风险。
- **错误分析细致**：量化了错误分布并找出代码失效的根因（缺参数、无返回值、缩进），对后续系统改进有直接指导意义。

## 8. 不足与局限

- **场景规模有限**：仅使用两家公司的报告配对，任务定义简化为双公司环境；对更复杂的多公司或全行业分析尚未覆盖（作者已承认并列为未来工作）。
- **知识库来源局限**：专业知识来自 Wikipedia 的 20 条随机采样子集，可能与报告分析所需金融概念匹配不完整；且以“是否存在”二值判断为标准，未考量知识应用的正确程度。
- **评估器偏差风险**：GPT-4o 判断的证据蕴含维度与人类一致性仅 0.630，低于其他维度；LLM-as-Judge 可能存在偏好模型风格、遗漏领域细节等系统性偏差。
- **数值匹配策略局限性**：虽然支持容差和单位归一化，但对复杂数值语义（如同比变化率与绝对值的区别、表格头部单位继承错误）无法完全覆盖。
- **代码评估范围较窄**：仅统计执行成功率，不验证代码计算逻辑是否与子句推理语义一致。
- **迭代细化实验受限于算力与模型范围**：未覆盖更大规模的闭源模型多重外部反馈组合，涉及的消融模型组合数量有限。
- **零样本设定**：未探索少样本（few-shot）或带检索增强（RAG）的归因生成表现，实验结果保守但未覆盖全部实际部署形态。

（完）
