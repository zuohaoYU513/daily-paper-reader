---
title: Hallucination Detection in Structured Query Generation via LLM Self-Debating
title_zh: 基于大语言模型自我辩论的结构化查询生成幻觉检测
authors: "Miaoran Li, Jiangning Chen, Minghua Xu, Xiao-Long Wang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.873.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过自我辩论框架检测结构化查询生成中的幻觉
tldr: 针对低资源结构化语言（如Splunk搜索语言）生成中的幻觉检测难题，本文提出自我辩论（Self-Debating）检测框架。该框架让大语言模型从对立视角生成对比解释，再做出最终一致性判断。通过在真实SPL生成和合成数据上的实验，验证了该框架能有效识别幻觉。此方法为领域特定语言中的幻觉检测提供了通用方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp873/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 761, \"height\": 823, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp873/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 772, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp873/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 487, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp873/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 614, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp873/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1576, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp873/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1649, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp873/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 298, \"label\": \"Table\"}]"
motivation: 结构化查询语言（如SPL）在公共训练数据中代表性不足，导致大语言模型生成时易出现幻觉，需要有效的检测方法。
method: 提出Self-Debating框架，提示大语言模型从对立视角生成对比解释，然后进行最终一致性判断以检测幻觉。
result: 在真实SPL生成场景和合成数据上验证了该框架的检测效果，并给出了幻觉分类体系。
conclusion: 自我辩论方法能有效检测低资源结构化查询生成中的幻觉，为该类场景提供可借鉴的检测范式。
---

## Abstract
Hallucination remains a key challenge in applying large language models (LLMs) to structured query generation, especially for semi-private or domain-specific languages underrepresented in public training data. In this work, we focus on hallucination detection in these low-resource structured language scenarios, using Splunk Search Processing Language (SPL) as a representative case study. We start from analyzing real-world SPL generation to define hallucination in this context and introduce a comprehensive taxonomy. To enhance detection performance, we propose the Self-Debating framework, which prompts an LLM to generate contrastive explanations from opposing perspectives before rendering a final consistency judgment. We also construct a synthetic benchmark, SynSPL, to support systematic evaluation of hallucination detection in SPL generation. Experimental results show that Self-Debating consistently outperforms LLM-as-a-Judge baselines with zero-shot and chain-of-thought (CoT) prompts in SPL hallucination detection across different LLMs, yielding 5–10% relative gains in hallucination F1 scores on both real and synthetic datasets, and up to 260% improvement for LLaMA-3.1–8B. Besides hallucination detection on SPL, Self-Debating also achieves excellent performance on the FaithBench benchmark for summarization hallucination, demonstrating the strong generalization ability of Self-Debating, with OpenAI o1-mini achieving state-of-the-art performance. All these results consistently demonstrate the strong robustness and wide generalizability of Self-Debating.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **领域背景**：大语言模型（LLM）在高资源结构化查询语言（如 SQL、Python）的自然语言转代码/查询任务上取得了显著成功。然而，许多真实世界应用依赖的是**半私有或领域特定语言**，如 Splunk Search Processing Language（SPL）、New Relic Query Language（NRQL）、Kusto Query Language（KQL），这些语言在公共训练数据中代表性严重不足，导致 LLM 生成的查询更容易出现幻觉（hallucination）。
- **核心问题**：在低资源结构化语言（以 SPL 为代表）的生成场景中，幻觉检测是一个未得到系统性研究的空白领域。LLM 可能生成语法正确但语义上无依据或错误的 SPL 查询，削弱其在工业场景中的可靠性。
- **研究目标**：本文旨在填补这一空白——(1) 正式定义 SPL 生成中的幻觉并建立分类体系；(2) 提出一种轻量、模型无关的幻觉检测框架 Self-Debating；(3) 构建可复用的合成基准 SynSPL，为后续研究提供测试平台。
- **整体含义**：该研究揭示了低资源结构化语言中幻觉问题的严峻性（真实数据中 69% 的生成查询存在幻觉），并提出了一种不需要额外训练、不依赖外部知识库、可通过纯提示工程显著提升检测能力的通用范式。

## 2. 方法论

### 2.1 SPL 幻觉的正式定义

一个生成的 SPL 查询被视为**一致（consistent）** 当且仅当同时满足两个条件：
1. 所有结构组件（index、sourcetype、source、fields 等）均能被生成提示中提供的信息明确支持；
2. 查询不包含语法错误，符合 SPL 正确语法。

若任一条件被违反，则该 SPL 查询被视为**幻觉（hallucinated）**。

### 2.2 幻觉分类体系（五类）

| 类别 | 定义 |
|------|------|
| **Fabrication（捏造）** | 引入了提示中完全不存在、无任何证据支持的 index、sourcetype、source、field 或 lookup table。 |
| **Mixed Information（混合信息）** | 各组件（如 index、sourcetype、fields）单独看均有提示支持，但组合方式本身不受支持。 |
| **Misaligned Information（错误对齐信息）** | 字段名和字段值各自受支持，但二者的配对关系错误或无法验证（针对 field-value 关联错误）。 |
| **Syntax Error（语法错误）** | 出现无效或拼写错误的命令、引号缺失/错配、字段引用错误、命令结构或顺序不当等使查询无法执行的问题。 |
| **Misinterpretation（误解）** | 引入了用户请求中未支持或无法推断的额外条件、过滤器或要求。 |

### 2.3 Self-Debating 框架

核心思想：**让单个 LLM 通过内部对比推理来提升幻觉检测的准确性和可解释性**。分为两个阶段：

- **阶段一：对比解释生成（Explanation Generation）**
  - 给定（生成提示，生成结果）输入对，模型被要求分别生成两个对立视角的解释：
    - 假设输出是**幻觉的**：识别提示中不支持或不可验证的元素；
    - 假设输出是**一致的**：基于与输入上下文的对齐程度提供辩护。
  - 对比式解释强制模型同时阐述两种可能立场，为后续判断做准备。

- **阶段二：最终判断（Final Judgment）**
  - 模型被提供生成提示、生成结果以及前一阶段的两个解释，要求阅读并权衡两者后做出最终判断。
  - **位置偏差缓解**：整个过程执行两次，交替改变两个解释的呈现顺序。若两次结论一致，则接受该标签；若结论分歧，则以更高温度（实验中设为 0.5）额外运行三次，取所有运行结果的多数标签作为最终决定。

该框架具有通用性，可适用于任何"LLM 基于输入提示产生响应输出"的任务（结构化查询、摘要、问答等）。

## 3. 实验设计

### 3.1 数据集 / 场景

- **真实 SPL 数据（人工标注）**
  - 收集过程：25 个真实场景用户查询 × 8 个 LLM = 200 个（提示，SPL）对；
  - 标注过程：两名 SPL 专家独立标注（先二分类，再细分类别），分歧经讨论解决，必要时由第三人裁决；
  - 结果：138/200（69%）被判定为幻觉。

- **SynSPL（合成基准）**
  - 以 BIRD 数据集开发集为种子，选取最多 30 个样本/数据库（优先复杂查询），共 330 个 SQL 样本；
  - 三步构建一致对：(1) GPT-4o 将 SQL 翻译为 SPL；(2) GPT-4o 验证翻译语义等价性；(3) 人工审查修正，特别是涉及 JOIN 和表别名的字段引用错误。最终保留 252 个经过验证的无幻觉样本；
  - 为每个 SPL 生成结构化合成提示（含通用指令、检索到的元数据、相关示例查询、用户历史、当前用户查询）；
  - 幻觉注入：由 6 个 LLM（o1-mini、GPT-4o、LLaMA-3.1-8B、LLaMA-3.1-70B、DeepSeek-R1-8B、DeepSeek-R1-70B）分别注入 4 类幻觉（Fabrication、Syntax Error、Mixed Information、Misaligned Information；Misinterpretation 因真实数据中罕见被排除）；
  - 最终规模：6,300 个样本（252 一致 + 252 × 4 类 × 6 模型幻觉）。

- **FaithBench（泛化性验证）**
  - 摘要幻觉检测基准，人类标注高质量，用于评估 Self-Debating 的跨领域泛化能力。

### 3.2 对比方法

- **Zero-shot prompt**（Luo et al., 2023）：直接询问模型输出是否一致；
- **FACTS CoT**（Jacovi et al., 2025）：结合 CoT 推理提示；
- **Self-Debating**（本文方法）。

### 3.3 评估指标

- SynSPL：幻觉类别的 F1、精确率、召回率；各数据类型准确率；
- FaithBench：平衡准确率（Balanced Accuracy）、宏平均 F1（F1-Macro）、幻觉类和一致类的类别 F1。

### 3.4 骨干模型

o1-mini、GPT-4o、LLaMA-3.1-8B、LLaMA-3.1-70B、DeepSeek-R1-Distill-LLaMA-8B、DeepSeek-R1-Distill-LLaMA-70B（共 6 个）。

## 4. 资源与算力

- **文中未明确说明**使用的具体 GPU 型号、数量或训练/推理时长。
- 从论文描述推断：该方法为**纯推理式提示工程**，不涉及模型训练或微调；实验依赖多个 LLM 的 API 或本地推理（包括 8B 到 70B 规模的开源模型），因此算力开销主要来自推理调用次数（解释生成 + 多次判断投票），而非训练成本。
- 作者在 Limitations 中承认 Self-Debating 相比简单提示方法需要**额外的计算成本**（多次生成和推理轮次），可能限制其在低冗余场景中的实用性。

## 5. 实验数量与充分性评估

### 5.1 实验规模概览

- **真实数据收集与分析**：200 对（prompt, SPL），涉及 8 个 LLM，包含幻觉率统计、幻觉类别分布、各模型行为差异分析；
- **SynSPL 主实验**（表 2）：6 个 LLM × 3 种方法，报告 F1/精确率/召回率；
- **SynSPL 分类别准确率**（表 3）：6 个 LLM × 5 个数据类别（一致 + 4 类幻觉）× 3 种方法；
- **FaithBench 泛化实验**（表 4）：6 个 LLM × 3 种方法，报告 4 项指标；
- **附录**：提供五类幻觉的详细示例和 Self-Debating 与 zero-shot 的对比案例。

### 5.2 充分性评价

**充分的方面**：
- 骨干模型覆盖了从 8B 到 70B、从开源到闭源的多种规模和类型，验证了方法的**模型无关性**；
- 同时覆盖结构化查询生成（SPL）和开放域摘要（FaithBench）两个差异性大的任务，验证了**跨领域泛化能力**；
- 报告了分类别准确率（表 3），证明方法并非只会标记一切为幻觉，而是对不同幻觉类型均有针对性的检测提升；
- 真实数据分析与合成基准相结合，兼顾了生态效度与规模化评估。

**不够充分的方面**：
- **无消融实验**：未单独移除对比解释生成阶段、位置偏差缓解机制或多次投票策略来验证各组件的独立贡献；
- **基线的局限**：仅对比了两种提示式基线（zero-shot 和 FACTS CoT），未与更复杂的幻觉检测方法（如基于外部检索验证的方法、训练专用分类器、多智能体辩论等）进行比较；
- **SynSPL 的真实性限制**：合成数据基于 SQL 翻译而来，可能无法完全捕捉真实 SPL 场景中全部复杂性和多样性；
- **FaithBench 上弱模型提升有限**：如 DeepSeek-R1-8B 的 F1-Macro 虽从 30.72% 提升至 36.34%，但绝对性能仍偏低，泛化优势主要体现在中等及较强模型上。

## 6. 主要结论与发现

1. **SPL 生成中幻觉问题极其普遍**：200 个真实生成样本中 69% 被判定为幻觉，证实该问题的严重性和检测需求的迫切性。
2. **Fabrication 是最主要的幻觉类型**：占所有幻觉实例的 62.4%，说明 LLM 倾向于编造提示中不存在的组件；Mixed Information 占 24.2%；Misinterpretation 极为罕见（0.7%）。
3. **幻觉率存在显著的模型差异**：LLaMA-3.1-70B 最低（52%），GPT-4o 次之（56%），Mistral 8×22B 和 DeepSeek-R1-8B 最高（84%）；不同模型在幻觉类型倾向上也有独特模式（如 Mistral 多语法错误、DeepSeek 系列多错误对齐信息和分析）。
4. **Self-Debating 在 SynSPL 上一致优于基线**：
   - LLaMA-3.1-8B：F1 从 23.39%（zero-shot）/ 2.55%（CoT）提升至 **85.05%**；
   - DeepSeek-R1-8B：从 39.39% / 19.13% 提升至 **74.87%**；
   - DeepSeek-R1-70B：从 62.50% / 58.54% 提升至 **89.39%**；
   - o1-mini：从 86.03% / 84.59% 提升至 **91.94%**；
   - 弱模型提升幅度最大（最高相对提升 260%），体现方法对模型能力差距的补偿作用。
   - GPT-4o 出现轻微下降（96.23% → 95.40%），作者归因于强模型内部推理能力已足够成熟，额外的对比推理可能引入轻微混淆。
5. **Self-Debating 泛化到摘要幻觉检测**：在 FaithBench 上，6 个模型中 4 个获得 30% 以上的相对 F1-Macro 提升；应用于 o1-mini 时不仅超越其原始基线，还达到所有评估模型中的 SOTA 水平（F1-Macro 58.77，F1-Halu 65.88）。
6. **Self-Debating 的作用机制**：不仅简单地使模型变得"更保守"，而是根据基础模型的错误倾向进行自适应调整——对过度谨慎的模型（GPT-4o）提高选择性，对敏感性不足的模型（LLaMA-3.1-8B）扩大检测覆盖率。

## 7. 优点

- **方法轻量且通用**：Self-Debating 无需训练、无需外部工具或知识库、无需多智能体协作，仅通过改进单模型提示策略即可大幅提升检测性能，可作为任何 LLM 的即插即用模块。
- **位置偏差处理细致**：通过"两次判断 + 顺序交替 + 分歧时高温多次投票取多数"的机制，有效降低了解释呈现顺序带来的判断偏差，增强了结果的可靠性。
- **幻觉分类体系完整且实用**：五类分类基于真实数据分析构建，覆盖了从组件捏造到字段-值错配再到语义误解的层次化错误类型，为后续研究和错误诊断提供了清晰框架。
- **数据构建流程严谨**：SynSPL 采用多阶段验证（GPT-4o 翻译验证 + 人工审查 + 双模型一致性检查 + 人工修正），并利用 SQL 与 SPL 的结构相似性进行数据迁移，创造性地解决了 SPL 无现成基准的困境。
- **多维度验证**：涵盖真实数据 + 合成数据 + 跨领域基准、6 个不同规模/来源的 LLM、多种指标（F1/P/R、类别准确率、平衡准确率等），实验设计相对全面，结论可信度高。
- **可解释性**：对比解释的生成过程本身即提供了检测决策的推理依据，比黑盒式 judge 方法更具可解释性和可审计性。

## 8. 不足与局限

- **计算开销偏高**：需要生成两个对比解释，加上最多 5 次判断运行，推理成本显著高于 single-pass 的 zero-shot 或 CoT 提示，在低延迟或高吞吐需求场景中可能不实用。

## 8. 不足与局限（续）

- **真实数据规模有限**：仅收集 200 对（prompt, SPL）样本、覆盖 25 个用户场景，虽然足以支撑初步统计分析，但无法充分代表 SPL 在实际工业环境中的全部使用模式与交互多样性；幻觉类别的分布估计（如 Misinterpretation 仅占 0.7%）也可能因样本量小而存在偏差。
- **SynSPL 覆盖不完整**：由于 Misinterpretation 在真实数据中过于罕见，SynSPL 在构建时将其排除，导致该类型在定量评估中完全缺席——这使框架对"额外条件/过滤器误解"类幻觉的检测能力未被验证，形成评估盲区。
- **合成与真实的分布差异**：SynSPL 以 SQL-to-SPL 翻译为种子，虽然经过语义等价性验证，但翻译过程可能引入结构性偏差（如 JOIN 表达方式、字段引用习惯等）；合成提示由模板化拼装而成，与真实用户自然语言查询的表述风格存在差距，可能高估方法在真实场景中的表现。
- **自我辩论的固有局限**：框架完全依赖模型自身内部知识进行正反论证。当模型对 SPL 的整体知识存在系统性盲区时，"与提示对齐"和"幻觉"两种解释可能同时建立在错误理解之上，辩论无法纠正固有的知识缺陷；此外，若模型生成了误导性的对比解释，反而可能污染最终判断。
- **框架并非对所有模型无损**：GPT-4o 上出现轻微性能回退（96.23% → 95.40%），说明对于内部判断已高度成熟的强模型，额外引入的对比推理可能带来噪声。框架缺乏对"何时应该启用、何时应保持原判"的自适应机制。
- **主导逻辑的领域局限**：SPL 幻觉定义以"可被提示信息明确支持"为核心判定标准，强调结构组件的可验证性。这种定义在结构化查询语言领域有效，但未必能直接迁移到其他语言形式（如自然语言生成、代码生成等）中的幻觉概念，后者更依赖语义层面的事实一致性。

## 9. 未来工作与开放问题

1. **扩展到更多半私有结构化语言**：作者明确指出 SPL、NRQL、KQL 等语言具有相似的低资源特征，将 Self-Debating 与 SynSPL 构建流程迁移到这些语言，是验证方法通用性的直接下一步。
2. **将检测延伸到错误修正**：当前框架止步于"判断是否存在幻觉及类别"，未来工作可基于五类分类体系设计自动修正机制，直接产出无幻觉的 SPL 查询，形成"检测-修正"闭环，更具工程实用价值。
3. **引入语义级验证**：现有幻觉定义偏重结构组件支持性（字段是否存在、语法是否合法），尚未覆盖"查询语义是否真正回答了用户意图"这一更深层维度；未来可结合执行结果或数据统计信息进行语义一致性校验。
4. **降低计算成本**：探索自适应推理策略——如先用低成本单次判断筛选高置信样本，仅对低置信样本启用完整辩论与多轮投票，从而在性能与开销之间取得动态平衡。
5. **更丰富的对抗性评估**：当前幻觉注入来自 6 个 LLM，可进一步引入人工构造的对抗样本或真实生产环境日志，检验框架在更复杂、更隐蔽幻觉模式下的稳健性。

## 10. 最终评价

总体而言，本文是**低资源结构化语言生成幻觉检测领域的开拓性工作**。其贡献可归纳为三个层面：概念层面，首次为 SPL 生成定义幻觉并建立可操作的五类分类体系；方法层面，提出了一种优雅且通用的 Self-Debating 提示范式，以纯推理方式显著提升多种 LLM 的幻觉检测能力，并附带完整的位置偏差缓解机制；资源层面，构建并开源了 SynSPL 合成基准，为后续研究提供了可复用的测试平台。实验设计兼顾了真实生态效度与规模化验证，多模型、多任务、多指标的交叉验证使得结论具有较强的说服力。诚然，该方法在计算开销、基线对比广度和合成数据真实性方面仍有提升空间，且对强模型的收益边际递减，但这些局限并不削弱其作为"零训练、即插即用"检测方案的核心价值。对于任何部署在低资源结构化语言场景中的 LLM 应用，Self-Debating 都是一项值得优先采纳的可靠性增强手段。

（完）
