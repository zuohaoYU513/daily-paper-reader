---
title: Fact-and-Reflection (FaR) Improves Confidence Calibration of Large Language Models
title_zh: 事实与反思提示改善大语言模型的置信度校准
authors: "Xinran Zhao, Hongming Zhang, Xiaoman Pan, Wenlin Yao, Dong Yu (于东), Tongshuang Wu, Jianshu Chen"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.515.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 系统研究提示策略对置信度校准的影响，发现部分提示诱发过度自信，提出事实与反思提示方法改善校准
tldr: 为使大语言模型的置信度与真实表现更好对齐，论文在问答场景系统比较了六种提示策略，发现它们虽整体改善预期校准，却会在部分实例上诱发过度自信。受人类认知启发，作者提出事实与反思(FaR)提示方法，引导模型在反思事实的基础上给出置信度。实验表明FaR能显著提升置信度校准质量并缓解过度自信，为无需额外训练的可靠性增强提供了轻量提示方案。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 690, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 706, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 679, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1490, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 757, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1625, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 794, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 789, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl515/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 788, \"height\": 793, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 611, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 670, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 729, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 828, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 642, \"height\": 533, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 825, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 585, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1481, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl515/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1606, \"height\": 1030, \"label\": \"Table\"}]"
motivation: 提示策略会影响模型总体校准，但也会在部分实例上诱发过度自信。
method: 提出事实与反思提示，让模型先核验事实并进行反思再给出置信度。
result: 与多种提示基线相比，该方法显著改善置信度校准并抑制过度自信。
conclusion: 通过认知启发式提示可低成本提升大语言模型置信度的可信度。
---

## Abstract
For a LLM to be trustworthy, its confidence level should be well-calibrated with its actual performance. While it is now common sense that LLM performances are greatly impacted by prompts, the confidence calibration in prompting LLMs has yet to be thoroughly explored.In this paper, we explore how different prompting strategies influence LLM confidence calibration and how it could be improved. We conduct extensive experiments on six prompting methods in the question-answering context and we observe that, while these methods help improve the expected LLM calibration, they also trigger LLMs to be over-confident when responding to some instances.Inspired by human cognition, we propose Fact-and-Reflection (FaR) prompting, which improves the LLM calibration in two steps. First, FaR elicits the known “facts” that are relevant to the input prompt from the LLM. And then it asks the model to “reflect” over them to generate the final answer.Experiments show that FaR prompting achieves significantly better calibration; it lowers the Expected Calibration Error by 23.5% on our multi-purpose QA tasks. Notably, FaR prompting even elicits the capability of verbally expressing concerns in less confident scenarios, which helps trigger retrieval augmentation for solving these harder instances.

---

## 论文详细总结（自动生成）

# 论文总结：Fact-and-Reflection (FaR) Improves Confidence Calibration of Large Language Models

## 1. 核心问题与整体含义

- **研究动机**：大语言模型（LLM）的置信度需要与真实性能对齐才能具备可信度。尽管提示（prompting）已被普遍认可会显著影响模型表现，但**提示策略对置信度校准的影响**鲜有系统性研究。
- **核心问题**：不同提示策略如何影响 LLM 的置信度校准？如何设计提示来提升校准质量？
- **研究发现的初始问题**：通过系统评测六种常见提示策略（QA 场景），作者发现这些方法虽在总体上可改善预期校准（ECE 上表现更好），但会引发模型在部分实例上的**过度自信（over-confidence）**，导致实例级校准误差变大。
- **整体含义**：提示设计不仅关乎任务性能，也关乎可靠性与可信度；通过受认知科学启发的提示方法可以低成本改善模型置信度的可信度，无需求助额外训练。

## 2. 方法论：FaR（Fact-and-Reflection）提示

- **核心思想**：借鉴人类认知研究——将“事实获取（fact acquisition）”与“推理决策（reasoning）”分离，可缓解锚定效应导致的过度自信。模型应先在推理前回顾全部相关事实，再进行审视推理，而非边生成观点边得出结论。
- **FaR 具体流程（三步式）**：
  1. **Fact（事实提炼）**：要求模型列出与问题相关的已知事实（即内部知识），并附上对应的事实来源。
  2. **Reflection（反思推理）**：要求模型基于上述事实进行审视性推理，将多个事实联系起来。
  3. **Answer（最终答案）**：将事实与反思作为上下文，输入模型生成最终答案。
- **概率视角**：FaR 将采样过程从 p(A|Q, T, θ) 拓展为 p(A|Q, Tf, Tr, θ)，Tf 表示事实生成步骤，Tr 表示反思步骤，Tf 的结果先于 Tr 产生并稳定生成过程。
- **正交性设计**：FaR 与置信度提取方法正交，可兼容多种置信度提取手段（Token Prob.、P(True)、Verbalized Confidence）。
- **消融变体**：
  - **fact-only**：不进行反思步骤。
  - **no-source**：省略来源生成子步骤。
  - **+explain**：将最终提示从 “Answer:” 改为 “Explain and Answer:”。

## 3. 实验设计

### 3.1 数据集 / Benchmark
- 两类 QA 数据，衡量模型的宏观平均性能：
  - **StrategyQA**：需要隐式推理的问答数据集（229 个开发集样本）。
  - **Web Questions (WQ)**：基于知识库事实的问答数据集（100 个测试集样本）。
- 答案格式为 Yes/No 或短短语（如 "English and Creole"）。
- 有些补充实验使用 StrategyQA 人工标注事实（因只有该数据集提供支持事实标注）。

### 3.2 对比方法（8 种基线 + FaR）
- **标准提示（Standard）**
- **Step Decomposition 类**：
  - Knowledge prompting（生成相关知识后再作答）
  - Knowledge+Explain（最后提示要求解释并作答）
  - Chain-of-Thought（CoT，“Let's think step by step”）
  - Self-Ask（模型自我追问子问题并组合回答）
  - Self-Ask (aggregate)（一次性生成全部中间问答）
- **Multi-Candidate Selection 类**：
  - Self-Consistency（10 次采样多数投票）
  - Pseudo-ToT（模拟多专家对话讨论）

### 3.3 置信度提取方法
- **Token Prob**：对生成序列 top-1 token 概率取平均后取指数。
- **P(True)**：模型在 "Possible answer" 前附加 True/False 选项问答，取回答 "A" 的概率。
- **Verbalized Confidence**：模型用语言输出置信度数值。
- 由于 Verbalized Confidence 总体上效果最差，主实验主要报告 Token Prob. 与 P(True) 的平均表现；分析部分也涉及三类方法的分布对比。

### 3.4 评估指标
- **ECE（Expected Calibration Error）**：分桶聚合校准误差，易受桶内正负相消影响。
- **MacroCE（Macro-averaged Calibration Error）**：实例级校准误差的正负样本宏平均，能反映极端值影响。
- 模型性能度量：精确匹配（exact match）。

### 3.5 实验模型
- **主实验**：OpenAI GPT-3（text-davinci-003），报告了 max output length=120、temperature=1.2 等参数。
- **泛化实验**：Vicuna-13B、Baichuan2-13B-Chat、Llama-2-13B-Chat，使用 vLLM 推理。

## 4. 资源与算力

- **论文未明确说明**所使用的 GPU 型号、数量或训练时长。所提方法为纯推理期提示方法，不需要训练或微调，计算开销主要在多次 LLM 推理的自然语言生成上。
- 主实验用 GPT-3 API 完成；开源模型实验使用 vLLM 框架，但未报告具体硬件配置。

## 5. 实验数量与充分性

- **数量较充分**，主要包括：
  - 3 类基线共 8 种提示方法的系统性对比（表 2）；
  - 3 种置信度提取方法对比（表 1，表 6，附录表 8）；
  - FaR 的 4 个消融变体 + 完整 FaR（表 3）；
  - FaR 在 3 个开源模型上的泛化实验（表 5）；
  - FaR 引入人工标注事实的控制实验（表 7）；
  - 置信度分布可视化分析（图 5）、过度自信分析（图 4 / 附录图 8）；
  - 表达不确定性（Expressing Concern）的频率与行为分析（表 4、图 6）；
  - 困难样本检索增强模拟实验（68.0% 增益 vs. 随机采样 15.0%）；
  - 讨论了最终提示长度和示例数量对校准的混淆影响（附录图 9、图 10）。
- **充分性与公平性评价**：
  - 公平之处在于比较维度全面：覆盖多种提示类型、多种置信度提取方法、多种模型、多类指标；
  - 附录中对提示长度、演示样本数等混淆因素做了控制分析，增强了结论的稳健性；
  - 数据集规模较小（合计仅约 329 例），可能影响统计效力；
  - 主实验仅依赖 GPT-3（text-davinci-003）一个 OpenAI 模型，模型多样性略显不足；泛化验证只覆盖 13B 开源模型。

## 6. 主要结论与发现

- **现有提示方法普遍引发过度自信**：Step Decomposition 方法虽可改善 ECE，但在 MacroCE 上往往退步；Multi-Candidate Selection 方法两方面均表现不佳。
- **FaR 提示显著提升置信度校准**：
  - 在混合 QA 任务上使 ECE 下降约 **23.5%**，MacroCE 下降约 **13.9%**；
  - 在 GPT-3 上实现 ECE 22.8（优于最佳基线 Self-Ask aggregate 的 26.0）和 MacroCE 47.0（大幅优于 Standard 的 54.6）；
  - 在 Vicuna-13B、Baichuan2-13B、Llama-2-13B 上一致降低 ECE 与 MacroCE；
  - 引入人工标注真实事实后校准改善更为显著。
- **FaR 引发模型“表达不确定性”（Expressing Concern）**：如 “there is not yet sufficient evidence to answer” 等谨慎表述；FaR 下出现频率（8.8%）高于 CoT（3.9%），放开格式约束时更高达 59.2%。
- **表达不确定性伴随置信度和准确率的同步下降**：模型表达的 concern 是准确的“困难信号”——在 FaR 中，模型表达担忧的样本准确率仅 25%，而不表达担忧的样本为 67.0%。
- **实用价值**：以 concern 作为触发检索增强的证据，可带来 68.0% 的准确率增益（对比随机抽样仅 15.0%），说明 FaR 能有效标识需要外部知识增强的困难实例。
- **校准改进非来自提示长度混淆**：附录实验证明更长的提示并不必然降低误差，FaR 在不同长度下都优于 CoT。

## 7. 优点

- **认知科学启发下的方法创新**：将人类的“锚定偏差缓解”洞见映射为提示设计原则，因果链条清晰。
- **方法正交、通用**：FaR 可与不同置信度提取方法和外部知识增强无缝结合。
- **评测框架全面**：同时使用 ECE 与 MacroCE，兼顾整体校准和实例级误差；充分考虑桶相消效应的问题。
- **深入剖析机制**：不止于指标提升，还对过自信分布、表达不确定性行为及其与准确率/置信度的关系做了详细分析。
- **发现有应用价值的行为信号**：模型输出 concern 可作为困难样本的自然标识，为检索增强等下游应用提供线索。
- **尝试消解混淆因素**：对最终提示长度、示例数量做了控制实验，结论更稳健。
- **验证了模型的跨模型泛化性**：在三种开源模型上保持一致结论。

## 8. 不足与局限

- **任务覆盖较窄**：仅在 QA（推理 + 知识检索）场景验证；论文明确指出未涉及 Human Eval 等自由形式的人类指令任务，通用性存疑。
- **主实验依赖单一模型**：主要结论基于 GPT-3（text-davinci-003），因当时该模型是唯一支持 logits 访问且推理能力足够的方案。
- **“事实”未经外在验证**：FaR 中模型生成的事实及其来源的准确性缺乏客观保障，模型可能在错误事实上建立推理链（作者在 Limitations 中也承认这一点）。
- **准确性的小幅“校准税”**：在主比较中 FaR 的准确率优于 5/8 的基线但略低于 CoT 和 Knowledge prompting，提示准确率与校准之间存在轻微权衡。
- **Concern 的定义和质量评估尚不成熟**：论文承认何为“好的 concern”有待后续研究。
- **MacroCE 改进幅度有限且受模型影响**：在 Vicuna 上 MacroCE 的改善较小；且多数 FaR 变体在 MacroCE 上其实不及 Standard，说明实例级误差来源复杂。
- **所有数据与输出均为英文**，跨语言/多文化的通用性未测试。
- **未探索模型内部机制**：论文沿用黑箱视角，未用可解释性工具分析 FaR 是否真正内部缓解了锚定效应。

（完）
