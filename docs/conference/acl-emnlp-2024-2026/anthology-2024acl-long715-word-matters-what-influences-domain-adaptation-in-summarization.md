---
title: "Word Matters: What Influences Domain Adaptation in Summarization?"
title_zh: 词很重要：什么在影响摘要任务的领域自适应？
authors: "Yinghao Li, Siyu Miao, He-Yan Huang (黄河燕), Yang Gao (扬 高)"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.715.pdf"
tags: ["query:faithfulness"]
score: 4.0
evidence: 分析词级数据集学习难度对摘要领域自适应的作用
tldr: 领域自适应通常被模型参数量和训练数据规模等全局因素诱导，但这些因素不能反映领域差异的细粒度原因。作者面向摘要任务提出以基于词的压缩率和抽象程度量化数据集学习难度，以此解释领域自适应表现的差异。实验表明，考虑数据集学习难度后，训练数据中的词级特性更能影响模型在新领域上的摘要效果。该工作为摘要领域的微调和数据选择提供了可解释的量化依据，但其未涉及事实一致性与幻觉问题。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long715/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1578, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long715/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 714, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long715/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 672, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long715/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 709, \"height\": 594, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long715/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1462, \"height\": 653, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1645, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1654, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long715/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 526, \"label\": \"Table\"}]"
motivation: 为摘要任务中的领域自适应寻找除模型规模和数据量之外的细粒度影响因素。
method: 提出用基于词的压缩率与抽象程度刻画数据集学习难度，并考察其与领域适应性能的关系。
result: 数据集学习难度比通用规模因素更能解释不同领域上的摘要生成表现。
conclusion: 词级别的数据难度可指导领域微调与训练数据选择，但未直接处理幻觉。
---

## Abstract
Domain adaptation aims to enable Large Language Models (LLMs) to generalize domain datasets unseen effectively during the training phase. However, factors such as the size of the model parameters and the scale of training data are general influencers and do not reflect the nuances of domain adaptation performance. This paper investigates the fine-grained factors affecting domain adaptation performance, analyzing the specific impact of ‘words’ in training data on summarization tasks. We propose quantifying dataset learning difficulty as the learning difficulty of generative summarization, which is determined by two indicators: word-based compression rate and abstraction level. Our experiments conclude that, when considering dataset learning difficulty, the cross-domain overlap and the performance gain in summarization tasks exhibit an approximate linear relationship, which is not directly related to the number of words. Based on this finding, predicting a model’s performance on unknown domain datasets is possible without undergoing training. Source code and scripts are available at https://github.com/li-aolong/Word-Matters.

---

## 论文详细总结（自动生成）

# 中文论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **领域自适应的核心痛点**：大语言模型（LLMs）在一个领域上训练后，难以有效泛化到其他领域，造成资源浪费。传统的领域自适应研究通常将模型参数量、训练数据规模等视为影响性能的一般性因素，但这些因素无法反映领域自适应的细粒度差异。
- **作者的核心观点**：提出应从更细粒度的语言单元——“词”的视角出发，探究训练数据中“词”的特性对摘要任务领域自适应性能的影响，而非仅关注模型规模或数据总量。
- **研究切入角度**：摘要任务与其他任务（如机器翻译、分类）不同，其核心是从长文档中提取关键信息生成简短文本。作者认为，输入文档与目标摘要之间的信息提取程度和交互方式，会影响模型在领域自适应中的表现。
- **整体含义**：通过量化数据集的学习难度和跨域词重叠，预测模型在未知领域上的性能，从而无需实际训练即可进行快速、低成本的性能评估。

## 2. 论文提出的方法论

### 2.1 核心思想

将“词”作为分析的原子单位，从两个层面展开：
- **数据集自身特征**：通过压缩率与抽象程度量化数据集的学习难度。
- **跨领域间的词关系**：通过跨域重叠与词数量考察对领域自适应效果的影响。

### 2.2 关键指标定义

- **压缩率（Compression Ratio, α）**：反映数据集在形式上的学习难度，即源文档相对于生成摘要的长度压缩程度。
  - 公式：α = (1/n) Σ (|Di| / |Si|)，其中 |Di|、|Si| 分别表示第 i 篇文档与摘要的词数。
  - 压缩率越高，说明模型需要从长文本中提取更核心的信息，任务越难。

- **抽象程度（Abstraction Level, β）**：反映数据集在内容上的学习难度，定义为文档-摘要对之间 ROUGE 分数均值的倒数。
  - β = n / Σ ROUGE(di, si)。
  - 文档与摘要间 ROUGE 越低，说明摘要不直接从原文复制，而是经历了更高程度的改写和抽象，学习难度更大。

- **学习难度系数（Learning Difficulty Coefficient, λ）** = α × β：将形式难度与内容难度综合为一个统一指标。

- **性能增益（ROUGE Gain）**：衡量领域自适应带来的绝对性能变化。
  - Gain = ROUGE_fine-tuned − ROUGE_base（微调后模型与基础模型在同一测试集上的 ROUGE 之差）。

- **跨域重叠（Cross-domain Overlap, γ）**：表征源领域与目标领域之间词级重叠程度的指标，计算源域各数据集与目标域各数据集的词频重叠的平均比例。

- **LD-Gain** = λ × Gain：将学习难度纳入考量后的性能增益，用于与跨域重叠或词数进行相关分析。

### 2.3 研究假说

- **假说 1**：跨域重叠 γ 与 LD-Gain 之间存在线性关系。
- **假说 2**：词数 WC 与 LD-Gain 之间存在线性关系。

## 3. 实验设计

- **数据集**：使用来自 4 个不同领域的摘要数据集：
  - **CNNDM**（新闻领域）
  - **PubMed**（科学领域）
  - **SAMSum**（对话领域）
  - **WikiHow**（通用/科普领域）
- **数据处理**：从 CNNDM、PubMed、WikiHow 中分别采样 35,000 条训练样本；SAMSum 数据集规模较小，保留全量（14,732 条）。所有测试集均采样 500 条。
- **模型**：
  - Bloom-1.1B、Bloom-3B：全参数微调。
  - Llama2-7B：使用 LoRA 参数高效微调。
- **实验场景**：
  1. **单域自适应**：仅用单一源领域训练，分别测试其余目标领域的性能增益；涉及 3 种训练-测试域组合，每个模型 12 组配置。
  2. **多域自适应**：将除测试域外的 3 个领域数据混合作为训练集；涉及 2 个模型 × 4 个测试域。
  3. **词数影响实验**（增量训练实验）：将 CNNDM 训练集分为 10 份（chunk），逐份加入训练，观测性能随词数增长的变化；同时在 4 个测试域上测试。
  4. **可预测性验证实验**：基于已有数据的线性拟合结果，重新采样 500 个新测试样本，预测模型在新领域上的性能并与实际结果对比。

## 4. 资源与算力

- **文中明确信息**：
  - 单域自适应实验中，Bloom-1.1B、Bloom-3B 和 Llama2-7B 在 4 张 RTX 3090 GPU 上训练。
  - Bloom 模型使用全参数微调，1 个 epoch，学习率 2e-5，batch size 4。
  - Llama2-7B 使用 LoRA 微调，3 个 epoch。
- **未明确信息**：文中未说明各实验的具体训练时长、总 GPU 耗时、多域自适应的完整超参数细节（仅说与单域自适应相同）以及词数增量实验的硬件配置等。

## 5. 实验数量与充分性

- **实验数量**：较丰富。包含 4 个跨领域数据集、3 种不同规模的模型、单域/多域/增量/预测四种实验场景，附录中还包含使用 BERTScore 替代 ROUGE 的补充实验（验证结论对评估指标选择的稳健性）。
- **充分性与客观性评估**：
  - **积极方面**：实验结果在多个不同规模模型（1.1B、3B、7B）中均呈现一致的线性趋势，结论具有一定泛化性。使用 BERTScore 的交叉验证增强了指标选择的稳健性。
  - **潜在不足**：
    - 数据集仅涉及 4 个英语摘要数据集，尚未覆盖更多领域（如法律、金融、医学）和低资源语言。
    - 作者在 Limitations 中坦诚指出：结论限于 adaptation tuning 方法，未覆盖 continual pre-training 和分布对齐等路径；LoRA 与全参数微调间的差异未做对照分析。
    - ROUGE（词重叠指标）被用于计算摘要性能、抽象程度和跨域重叠等多个指标，存在指标间循环依赖的风险。

## 6. 论文的主要结论与发现

1. **跨域重叠与性能增益呈近似线性关系**：当引入数据集学习难度系数（λ）后，跨域重叠 γ 越大，LD-Gain 越高。该线性关系在单域和多域自适应场景中（Bloom-1.1B、Bloom-3B、Llama2-7B）均稳健存在。
2. **词数量与性能增益无显著相关性**：在增量训练实验中，随着词数从约 256 万增加到约 261 万，LD-Gain 在多个目标领域上均无明显上升或下降趋势，仅在特定区间内波动，说明简单的数据规模扩大不能有效促进领域自适应。
3. **数据集学习难度是解释领域自适应差异的关键调节变量**：在用 λ 对性能增益调整前，Rouge 提升与实际性能差距之间往往难以直接对齐；调整后则呈现出清晰的线性规律。
4. **无需训练的领域自适应性能预测成为可能**：通过已有数据拟合 γ—LD-Gain 的线性趋势线，可对新目标领域的性能进行预估，预测与实际结果趋势一致、偏差较小。

## 7. 优点

- **选题视角新颖**：将领域自适应性能分析下沉到“词”这一细粒度层面，不再停留在模型规模和数据量的宏观视角。
- **指标设计有洞察力**：提出压缩率、抽象程度与学习难度系数等概念，合理结合了文本长度比与词重叠度，为量化生成任务数据集的“难度”提供了新工具。
- **多模型验证提高了结论泛化性**：用不同家族、不同规模和使用不同微调方式的模型验证了规律的一致性。
- **预测性输出实用性强**：该发现可指导实际应用中的数据选择和领域适配策略，显著节省训练前的算力投入。
- **评估稳健性检查**：作者用 BERTScore 替换 ROUGE 做补充验证，增强了核心结论的可靠性。
- **开源代码和脚本**：提供源码供后续研究复现与改进。

## 8. 不足与局限

- **理论分析较浅**：论文以实证发现为主，对“为什么跨域重叠与 LD-Gain 呈线性关系”、“为什么词数无关”缺少深入的理论推导或因果分析，多为相关性层面的探索。
- **实验覆盖有限**：数据集限于 4 个，难以覆盖更多样的文本类型（如情感分析、法律文书、对话机器人等）；模型虽有大有小但均为中等规模（≤7B），未在更大规模 LLM（如 13B、70B 或 100B+）上验证结论。
- **评估指标依赖词重叠**：ROUGE 本文基于词重叠，与跨域重叠本身均依赖表层词汇重合度。虽然作者用 BERTScore 做了补充验证，但在高抽象、高改写场景下的可靠性仍然有限。
- **指标循环风险**：学习难度系数由文档-摘要 ROUGE 计算而来，而性能增益也使用 ROUGE 计算，存在一定程度的内生性。
- **未涉及事实一致性/幻觉问题**：论文摘要元数据中明确指出，该工作未处理摘要生成中的事实一致性和幻觉问题，这是摘要任务中一个重要但缺失的维度。
- **作者自认局限**：论文自身 Limitations 指出 - 结论仅适用于 adaptation tuning 方法，对 continual pre-training 等路径不讨论；未系统探究微调方法差异（如全参数微调 vs LoRA）的影响。

---

（完）
