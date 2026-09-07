---
title: Towards Mitigating Factual Hallucination in LLMs through Self-Alignment with Memory
title_zh: 通过带记忆的自我对齐缓解大模型事实幻觉
authors: "Siyuan Zhang, Xiangsheng Li, Yinpeng Dong, Yichi Zhang, Jian Xie, Dong Yan, Hang Su"
date: 2024-09-22
pdf: "https://openreview.net/pdf?id=Hfv4LoCQPo"
tags: ["query:faithfulness"]
score: 6.0
evidence: 通过增强内部记忆利用的后训练自对齐，缓解事实幻觉生成
tldr: 大模型虽强大但仍难以保证回答符合客观事实，常见后训练方法在诚实与帮助之间存在权衡且泛化不足。本文提出基于记忆的自我对齐方法FactualBe，增强模型调用预训练知识这一基本能力。该方法旨在提升模型对事实的利用，同时避免过度牺牲帮助性。实验表明其能有效缓解事实幻觉并具备更强的泛化性，为不依赖外部检索的忠实生成提供后训练手段。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: 后训练缓解事实幻觉存在诚实性与帮助性权衡，且难以泛化到新场景。
method: 提出FactualBe，用自我对齐提升模型利用预训练内部记忆保持客观事实的能力。
result: 实验显示该方法能在保持帮助性的同时降低事实幻觉并提升泛化性。
conclusion: 增强内部记忆的利用比简单后训练更能全面提升回答的真实性。
---

## Abstract
Despite the impressive performance of Large Language Models (LLMs) across numerous tasks and widespread application in real-world scenarios, LLMs still struggle to guarantee their responses to be accurate and aligned with objective facts. This leads to factual hallucination of LLMs, which can be difficult to detect and mislead users lacking relevant knowledge. Post-training techniques have been employed to mitigate this issue, yet they are usually followed by a trade-off between honesty and helpfulness, along with a lack of generalized improvements. In this paper, we propose to address it by augmenting LLM's fundamental capacity of leveraging its internal memory, that is, the knowledge derived from pre-training data. We introduce FactualBench, a comprehensive and precise factual QA dataset consisting of nearly 200k Chinese generative QA data spanning 21 domains for both evaluation and training purposes. Furthermore, we propose self-alignment with memory, i.e., fine-tuning the model via preference learning on self-generated pairwise data from FactualBench. Extensive experiments show that our method significantly enhances LLM's performance on FactualBench, with consistent improvements across various benchmarks concerning factuality, helpfulness and multiple skills. Additionally, different post-training techniques and tuning data sources are discussed to further understand their effectiveness.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 论文关注**大语言模型（LLM）的事实幻觉问题**：尽管 LLM 在很多任务上表现优异，但其输出仍无法保证准确、与客观事实一致，这些幻觉难以被用户察觉，容易误导缺乏相关知识的人。
- 现有缓解事实幻觉的**后训练方法**存在两个主要问题：
  - **诚实性与帮助性之间的权衡**：过于强调“说不知道”会降低回答有用性；
  - **缺乏泛化性**：在特定场景或数据集上改进后，难以推广到更广泛的场景。
- 论文提出从根本上提升 LLM **利用内部记忆 / 预训练知识**的能力，而不是依赖外部检索，从而在保持帮助性的同时缓解事实幻觉。

## 2. 论文提出的方法论

- **核心思想**：通过后训练阶段的“自我对齐”，让模型更好地调用自己从预训练数据中获得的知识，使回答更符合客观事实。
- **关键组成**：
  1. **FactualBench 数据集**：
     - 一个面向中文生成式问答的综合事实 QA 数据集；
     - 包含近 **20 万**条问答数据；
     - 覆盖 **21 个领域**；
     - 同时用于**评估和训练**。
  2. **带记忆的自我对齐（Self-Alignment with Memory）**：
     - 基于 FactualBench，让模型生成**成对的候选回答**；
     - 通过偏好学习（preference learning）对模型进行微调，使其偏向更忠实于事实的回答；
     - 该方法强调对**内部记忆**的再利用，而非引入外部知识库。
- **可概括的算法流程**（文中未给公式，据描述）：
  - 构造事实性 QA 数据集 → 模型自生成候选答案 → 构造偏好对 → 使用偏好优化目标微调模型 → 获得更“忠实”的模型。

## 3. 实验设计

- **主要基准**：论文提出的 **FactualBench**，包含约 200k 中文 QA，覆盖 21 个领域，既作为训练集也作为评估集。
- **其他评估场景**：多个关于以下维度的基准测试：
  - **事实性（factuality）**；
  - **帮助性（helpfulness）**；
  - **多种技能（multiple skills）**。
- **对比方法**：与不同的**后训练技术**和不同的**训练数据来源**进行比较，以分析不同策略的有效性。
- **说明**：摘要中未给出具体基线模型名称、对比算法及评估指标的细节，需要阅读原文进一步确认。

## 4. 资源与算力

- 论文内容中**未明确说明**使用了多少算力资源，例如：
  - GPU 型号与数量；
  - 训练时长；
  - 总计算成本。
- 因此无法基于当前文本评估该方法的资源开销。

## 5. 实验数量与充分性

- 摘要称进行了“大量实验”（Extensive experiments），并且结果在多个基准上表现一致，说明实验覆盖了：
  - 主要基准 FactualBench；
  - 事实性、帮助性、多技能等不同维度；
  - 同时还包括了针对后训练技术和数据来源的对比分析，可作为消融性研究。
- 从摘要看，实验设计具备一定系统性；
- 但由于信息有限，无法判断：
  - 具体实验次数；
  - 是否有完整消融；
  - 训练/评估集是否存在重叠或数据泄漏风险；
  - 在英文或多语言场景上的验证是否充分。

## 6. 论文的主要结论与发现

- 所提“带记忆的自我对齐”方法能够**显著提升 LLM 在 FactualBench 上的事实问答能力**；
- 该方法在**事实性、帮助性和多种技能**等各个基准上均带来一致提升；
- 表明通过增强模型对内部记忆的利用，可以在缓解事实幻觉的同时**避免过度牺牲帮助性**；
- 不同后训练技术和数据来源对最终效果有明显影响，值得进一步研究。

## 7. 优点

- 提出一个面向事实问答的**大规模中文基准 FactualBench**，规模大、领域跨度广，兼具训练与评估价值；
- 方法**不依赖外部检索**，而是增强模型对预训练知识的内部利用能力，思路更贴近模型自身机制；
- 使用**偏好学习 + 自生成数据**进行自我对齐，无需额外人工标注大量偏好对；
- 实验覆盖多个维度（事实性、帮助性、多技能），结果一致性较好，支持方法有效性。

## 8. 不足与局限

- 当前摘要和元数据中未提供方法细节、模型参数规模等，难以复现或深入了解机理；
- 基准和实验主要围绕**中文问答**，对英文及其他语言、其他任务类型的泛化能力尚不明确；
- 自生成数据依赖“模型自己判断事实性”，可能受原始模型已有偏见的限制；
- “内部记忆”的增强机制并未在摘要中进行解释，例如如何区分“记错了”的内部知识和真正的记忆缺失；
- 未与基于外部检索（RAG）等方法进行对比，无法明确该方法相比检索增强方案的优势边界；
- 缺少算力、扩展性、实际部署成本的讨论，也缺乏对潜在失败案例和安全边界的分析。

（完）
