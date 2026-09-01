---
title: "FG-PRM: Fine-grained Hallucination Detection and Mitigation in Language Model Mathematical Reasoning"
title_zh: FG-PRM：语言模型数学推理中的细粒度幻觉检测与缓解
authors: "Ruosen Li, Ziming Luo, Xinya Du"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.228.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 针对大模型数学推理中的幻觉进行细粒度检测与缓解
tldr: 现有大模型在数学等复杂多步推理任务中容易出现幻觉，而既有方法只判断是否存在幻觉，缺乏对幻觉类型和表现的细粒度理解。为此论文提出FG-PRM细粒度过程奖励模型，基于六类幻觉分类法在步骤级检测并缓解幻觉，同时提出自动生成训练数据的方法以降低人工标注成本。实验证明其能更准确地定位推理中的幻觉并提升生成质量，为可解释幻觉治理提供了新思路。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp228/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp228/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp228/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1551, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp228/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 781, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp228/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1428, \"height\": 939, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1549, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1641, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1641, \"height\": 1908, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1186, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1186, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1363, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 847, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1157, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1010, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1169, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp228/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 851, \"height\": 449, \"label\": \"Table\"}]"
motivation: 复杂多步推理中大模型幻觉频发，现有方法仅检测幻觉存在性，缺少细粒度类型识别。
method: 提出FG-PRM细粒度过程奖励模型，构建六类幻觉分类法，在步骤级检测并缓解幻觉，并自动生成训练数据。
result: 在数学推理任务上验证了FG-PRM能够准确检测不同类型幻觉，并有效缓解推理中的幻觉问题。
conclusion: 细粒度、步骤级的幻觉检测与缓解可显著提升大模型在数学推理等复杂任务上的可靠性。
---

## Abstract
Hallucinations in large language models (LLMs) pose significant challenges in tasks requiring complex multi-step reasoning, such as mathematical problem-solving. Existing approaches primarily detect the presence of hallucinations but lack a nuanced understanding of their types and manifestations. In this paper, we first introduce a comprehensive taxonomy that categorizes the common hallucinations in mathematical reasoning tasks into six types. We then propose FG-PRM (Fine-Grained Process Reward Model), an augmented model designed to detect and mitigate hallucinations in a fine-grained, step-level manner. To address the limitations of manually labeling training data, we propose an automated method for generating fine-grained hallucination data using LLMs. Our FG-PRM demonstrates superior performance across two key tasks: 1) Fine-grained hallucination detection: classifying hallucination types for each reasoning step; and 2) Verification: ranking multiple LLM-generated outputs to select the most accurate solution. Our experiments show that FG-PRM excels in fine-grained hallucination detection and substantially boosts the performance of LLMs on GSM8K and MATH benchmarks. These results highlight the benefits of fine-grained supervision in enhancing the reliability and interpretability of LLM reasoning processes. Codes and datasets are available at: https://github.com/du-nlp-lab/FG-PRM.

---

## 论文详细总结（自动生成）

# FG-PRM 论文详细中文总结

## 1. 论文的核心问题与整体含义

### 研究动机与背景

- **问题源头**：大语言模型（LLMs）在需要复杂多步推理的任务（如数学解题）中，即使采用思维链（CoT）等先进提示技术，仍会频繁产生内容不正确或不可验证的“幻觉”（Hallucination），严重影响推理的可靠性。
- **现有方法的不足**：此前针对推理链幻觉的缓解方法大多只做**粗粒度检测**，即判断某个步骤或整条推理链“是否正确”，缺乏对幻觉**类型**和具体**表现形式**的细粒度理解，无法精准定位错误、提供有针对性的反馈。
- **核心研究问题**：如何**细粒度地**识别推理过程中每一步出现的幻觉类型，并利用这种细粒度监督来提升LLM在数学推理任务上的准确性和可解释性？
- **整体含义**：论文主张“细粒度监督优于粗粒度监督”。通过构建幻觉分类体系、自动合成细粒度训练数据，并训练专门的过程奖励模型（FG-PRM），能够在步骤级别检测幻觉并据此筛选最优答案，从而显著增强LLM推理的**可靠性**和**可解释性**。

## 2. 论文提出的方法论

### 2.1 六类幻觉分类法（Fine-grained Hallucination Taxonomy）

论文基于既有研究（Ji et al., 2023），将数学推理中的常见幻觉分为**内在幻觉**与**外在幻觉**两大类，共六个细分类别：

- **内在幻觉（Intrinsic）**
  - **上下文不一致（Context Inconsistency, CI）**：推理步骤与用户提供的上下文信息矛盾。
  - **逻辑不一致（Logical Inconsistency, LI）**：当前步骤与之前推理步骤之间存在逻辑矛盾或信息引用错误。
  - **指令不一致（Instruction Inconsistency, II）**：推理未遵循用户给定的明确指令（如要求以分数表示却输出小数）。
- **外在幻觉（Extrinsic）**
  - **计算错误（Calculation Error, CE）**：数值计算或公式应用错误，可通过外部工具验证。
  - **事实不一致（Factual Inconsistency, FI）**：与现实世界可验证的事实相矛盾。
  - **捏造（Fabrication, FA）**：包含无法在现实或上下文中验证的虚构事实、实体或数据。

### 2.2 自动幻觉数据生成框架

为解决人工标注步骤级细粒度数据成本高昂的问题，论文提出一个两阶段的自动化数据合成方法：

1. **阶段一：目标推理步骤识别（Feasibility Verification）**
   - 对于带标准答案（golden CoT）的数学问题，使用外部LLM判断每个正确推理步骤是否具备注入某类幻觉的**条件**。
   - 例如，若步骤不涉及现实世界事实，则不适合注入“事实不一致”幻觉。论文设计了针对六类幻觉的判断规则提示（见附录H）。
2. **阶段二：幻觉注入（Hallucination Injection）**
   - 对确认可注入的步骤，利用LLM（Llama-3-70B）基于**定制指令**和**少样本演示**生成包含特定幻觉类型的下一推理步骤。
   - 每个幻觉类型分别生成，以控制数据分布并保证注入成功率和质量。

### 2.3 FG-PRM 模型架构与训练

- **模型结构**：FG-PRM 由 **6 个任务专用 PRM 组成**（每个PRM对应一个幻觉类型），输入格式为“问题 + 推理步骤序列”，在每个步骤间的 `[sep]` 标记上输出该步骤是否包含对应幻觉类型的概率。
- **训练目标**：每个子PRM采用逐步交叉熵损失，类似于标准PRM的公式：

  \[
  L_{PRM} = \sum_{i=1}^{L} \left[ y^*_i \log r_{y_i} + (1 - y^*_i) \log(1 - r_{y_i}) \right]
  \]

- **推理与聚合**：给定一个候选解答，FG-PRM 将六个子模型的逐步对数概率累加得到整体奖励：

  \[
  R_\Phi(x, y) = \sum_{t=1}^{6} \sum_{i=1}^{L} \log \left( R_{\phi_t}(x, y_i) \right)
  \]

  正确步骤的概率接近1，对总奖励贡献极小，因此**答案长度不会影响最终排序分数**。

## 3. 实验设计

### 3.1 任务设置

论文在两个核心任务上评估FG-PRM：

1. **细粒度幻觉检测（Hallucination Detection）**：对每个推理步骤，判断其所属的幻觉类型，使用精确率、召回率和F1分数评估。
2. **幻觉缓解（Hallucination Mitigation / Verification）**：对LLM生成的64个候选答案进行排序，选择最正确的解答（best-of-N selection）。

### 3.2 数据集

- **基准数据集**：GSM8K（小学数学题）和 MATH（竞赛级数学题，含LaTeX公式）。
- **粗粒度数据集（CG-H）**：从两数据集训练集各采样700个实例、测试集各采样100个实例，包含人工标注的步骤正确性标签。
- **细粒度数据集（FG-H）**：通过自动数据生成方法，将CG-H扩充到每类12,000个实例，覆盖六类幻觉且分布均衡。
- **对比数据集**：Math-Shepherd（基于蒙特卡洛树搜索自动构造的过程监督数据，12,000实例；另有公开的400K全量模型用于对比）。

### 3.3 对比方法

- **提示型检测器**：ChatGPT（GPT-3.5-turbo）和 Claude-3-haiku，使用精心设计的提示词进行幻觉类型检测。
- **模型型检测器**：传统粗粒度 PRM。
- **缓解任务Verifier**：Self-Consistency (SC)、ORM、PRM、CG-PRM（在FG-H上以粗粒度二分类标签训练的单一PRM）、FG-ORM（六类细粒度ORM）、FG-PRM。
- **基础模型**：Longformer-base-4096 和 Llama-3-8B。
- **答案生成器**：Llama-3-70B（主要生成器），并额外测试了 Qwen2.5-Math-7B。

## 4. 资源与算力

- **GPU硬件**：论文明确说明所有实验在 **4张 NVIDIA A100 80G GPU** 上完成。
- **数据合成成本**：使用Llama-3-70B生成幻觉数据以降低API成本；文中提到若使用GPT-4o或Claude-3.5-Sonnet生成12K实例估计需花费超过$400，因此选用了本地开源模型。
- **训练时长**：论文**未明确报告**具体训练时长（如小时数或总GPU时数）。

## 5. 实验数量与充分性

### 主要实验组

1. **细粒度幻觉检测**（合成数据 + 人工标注数据，各六类幻觉，含F1、精确率、召回率）—— 对比ChatGPT、Claude、PRM、FG-PRM，共2组设置。
2. **幻觉缓解（Verification）**—— GSM8K和MATH两个基准，两个基础模型（Longformer、Llama-3-8B），多个对比verifier，并取3组采样结果的平均值，带显著性检验（p<0.05）。
3. **扩展分析**：
   - **候选数量影响分析**：从1到64个候选答案的变化趋势。
   - **OOD（分布外）评估**：用GSM8K训练的模型在MATH上测试，检验泛化能力。
   - **消融研究**：依次移除六类幻觉子PRM，观察性能下降。
   - **数据规模对比**：FG-PRM（12K）与Math-Shepherd PRM（12K、400K）对比。
   - **不同生成器和基础模型**：Qwen2.5-Math-7B作为生成器/基础模型的性能。
   - **紧凑FG-PRM对比**：单一多分类verifier vs. 六个独立二分类PRM。
   - **人工标注一致性**：Cohen's Kappa = 0.79。
   - **幻觉注入成功率评估**：六类型各50例，平均成功率94%（88%~100%）。

### 充分性与客观性评价

- **实验覆盖广**：覆盖两个主流数学基准、两个基础模型、多种对比方法、合成+人工数据、消融、OOD、数据规模、生成器多样性，实验矩阵相当丰富。
- **统计显著性**：对提升做了显著性检验，增加了结论可信度。
- **人工标注验证**：使用人工标注的真实数据和中等一致性（Kappa=0.79）验证合成数据上的结论，降低了仅依赖合成数据的偏差风险。
- **局限性**：人工标注数据仅50题/类，规模较小；部分对比（如ChatGPT/Claude）无法控制其实验细节和随机性，且其模型参数远大于FG-PRM基础模型，比较存在一定不对等性。

## 6. 论文的主要结论与发现

- **细粒度检测更优**：在合成数据上，FG-PRM在CI、LI、II、CE四类幻觉检测上超过ChatGPT和Claude，且在所有六类幻觉上均超过粗粒度PRM（平均F1从0.441提升至0.499；人工数据上从0.428提升至0.484）。
- **大型闭源模型在外在幻觉上仍占优**：ChatGPT和Claude在FI（事实不一致）和FA（捏造）检测上优于FG-PRM，原因是其参数量更大、世界知识更丰富。
- **缓解效果显著**：在GSM8K和MATH上，FG-PRM显著优于所有基线verifier：
  - Longformer基础：GSM8K 94%、MATH 57%（对比PRM 89%/53%）；
  - Llama-3-8B基础：GSM8K 93%、MATH 58%。
- **细粒度监督是核心优势**：与CG-PRM、FG-ORM同数据规模对比，FG-PRM均更优；单纯扩大训练数据量（PRM vs. CG-PRM）并不能带来显著提升，说明**标注粒度**而非数据规模是关键。
- **12K数据可胜过400K数据**：FG-PRM（12K，Longformer）超过Math-Shepherd PRM（400K，Mistral-7B），证明高质量细粒度监督的数据效率。
- **各幻觉类型的贡献不均**：消融显示移除“计算错误”类PRM影响最大（GSM8K -4%、MATH -5%），其次是逻辑不一致（-3%/-4%）；即使低频类型（指令不一致、捏造）也有1-3%的贡献。
- **强大的OOD泛化能力**：GSM8K训练的FG-PRM在MATH上性能几乎不下降（+0.01，而PRM下降+0.03），说明模型学到了可迁移的幻觉模式。

## 7. 优点

### 方法与设计亮点

- **细粒度幻觉分类体系**：首次针对数学推理提出覆盖六种不同幻觉类型的结构化分类法，弥补了此前粗粒度二元判断的不足，为细粒度诊断和缓解提供了统一框架。
- **自动化数据合成框架**：两阶段“可行性验证 + 幻觉注入”方法有效解决了人工标注成本高、难以规模化的问题；利用开源模型（Llama-3-70B）替代昂贵API，兼顾了成本与质量（注入成功率94%+）。
- **模块化的FG-PRM架构**：六个独立二分类PRM的设计优于单一多分类模型（避免“无错误”类别偏置），且各子模型可独立分析、独立贡献。
- **长度无关的奖励聚合**：通过对数概率累加、正确步骤近零贡献，消除了推理链长度对打分的影响。
- **显著的数据效率**：12K细粒度数据优于400K粗粒度数据，展示了“少而精”的监督信号对模型学习的价值。

### 实验与展示亮点

- 实验覆盖面广且层层递进，从检测到缓解、从合成到人工数据、从内部分布到OOD、从主实验到消融，逻辑链完整。
- 附带详细的成功/失败案例分析（附录J），并报告了人工评估的注入成功率，增强了方法透明度。
- 代码和数据已公开，便于复现与后续研究。

## 8. 不足与局限

### 方法层面的局限

- **依赖ground-truth推理步骤**：自动数据合成以标准（golden）推理链为起点，对于没有高质量标准推理过程的领域或问题难以直接应用，限制了大规模扩展性。
- **成本仍不低**：虽然使用开源模型降低了成本，但生成12K实例仍需GPU推理资源；若需更大规模数据，成本依然可观。
- **数据质量依赖注入成功率**：尽管平均成功率94%，仍有约6%的生成步骤可能不匹配目标幻觉类型或注入不自然，对模型训练带来噪声。

### 实验层面的局限

- **人工验证数据规模有限**：每个幻觉类型仅50条人工标注样本，数据量偏小，统计效力有限。
- **与闭源模型对比不对等**：ChatGPT-3.5和Claude-3的参数量远超FG-PRM的基础模型（Longformer-base、Llama-3-8B），在事实类幻觉检测上的比较结果部分反映了规模差异而非方法优劣。
- **领域局限**：实验仅覆盖数学推理（GSM8K、MATH），未验证在科学问答、常识推理等其他多步推理任务上的适用性。
- **评估指标较单一**：缓解任务主要使用最终答案准确率，未评估推理过程的整体忠信度或中间步骤改进。
- **训练时长和超参数细节缺失**：未报告训练轮数、学习率等关键训练细节，复现时需自行探索。

### 应用层面的限制

- **数学领域特性**：六类幻觉分类法中“计算错误”在数学任务中占绝对主导，其他类型（如捏造、事实不一致）在数学中相对低频；迁移到其他领域可能需要调整分类体系。
- **奖励模型类方法的固有限制**：FG-PRM本质上是判别式奖励模型，其性能受限于训练数据分布，对分布外新题型或新幻觉模式的泛化仍有边界。

---

（完）
