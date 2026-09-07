---
title: "HalluClean: A Unified Framework to Combat Hallucinations in LLMs"
title_zh: HalluClean：一个应对大语言模型幻觉的统一框架
authors: "Yaxin Zhao, Yu Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40926/44887"
tags: ["query:faithfulness"]
score: 7.0
evidence: 利用计划-执行-修订流程识别并修正无依据声明，任务无关，契合对无支撑事实内容的检测。
tldr: 针对LLM输出常含幻觉内容且已有方法依赖外部知识或监督检测器的问题，提出任务无关的轻量框架HalluClean。它将幻觉处理显式分解为规划、执行和修订三个阶段，通过最小任务路由提示实现跨领域零样本泛化，无需外部知识源。在五个代表性任务上的评估表明，该框架能有效识别并修正无事实支持的声明。HalluClean为通用幻觉治理提供了一种低成本的统一解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: LLM生成内容常有幻觉，现有方法依赖外部知识或监督检测器，跨域泛化能力受限。
method: 采用规划、执行、修订三阶段的推理增强范式，结合最小任务路由提示识别并修正无依据声明，无需外部知识。
result: 在五个代表性任务上零样本验证了框架对幻觉检测与纠正的有效性和泛化性。
conclusion: 为无外部资源的LLM幻觉治理提供了一种轻量、任务无关的统一方案。
---

## Abstract
Large language models (LLMs) have achieved impressive performance across a wide range of natural language processing tasks, yet they often produce hallucinated content that undermines factual reliability. To address this challenge, we introduce HalluClean, a lightweight and task-agnostic framework for detecting and correcting hallucinations in LLM-generated text. HalluClean adopts a reasoning-enhanced paradigm, explicitly decomposing the process into planning, execution, and revision stages to identify and refine unsupported claims. It employs minimal task-routing prompts to enable zero-shot generalization across diverse domains, without relying on external knowledge sources or supervised detectors. We conduct extensive evaluations on five representative tasks—question answering, dialogue, summarization, math word problems, and contradiction detection. Experimental results show that HalluClean significantly improves factual consistency and outperforms competitive baselines, demonstrating its potential to enhance the trustworthiness of LLM outputs in real-world applications.

---

## 论文详细总结（自动生成）

# HalluClean：一个应对大语言模型幻觉的统一框架（论文总结）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）虽然在众多 NLP 任务中表现突出，但很容易生成与事实不符的“幻觉”内容（hallucinations），严重损害其在安全关键场景（如医疗、金融）中的可靠性和可信度。
- **已有方法的不足**：现有的幻觉缓解方法主要有两类，一是检索增强生成（RAG）类方法，依赖外部知识源的可用性和准确性；二是基于人工标注数据的监督检测类方法，标注成本高、泛化能力弱。此外，幻觉行为在不同任务中表现差异大，但以往研究多聚焦单一任务，缺乏通用、可扩展、跨任务的统一解决方案。
- **核心问题**：能否在不依赖外部知识和任务专用监督信号的前提下，构建一个轻量、任务无关、可泛化到多种任务的幻觉检测与纠正框架？
- **整体含义**：论文提出的 HalluClean 框架在零样本设定下通过结构化推理（规划、执行、修订三阶段）统一解决多个 NLP 场景中的幻觉检测与修复问题，并在不修改模型参数的前提下显著提升 LLM 输出的事实一致性，为提高 LLM 在真实应用中的可信任度提供了一种通用的轻量方案。

## 2. 论文提出的方法论

- **核心思想**：将幻觉治理视为“检测—推理—修正”的推理增强过程，而非单纯分类或生成任务。通过引导 LLM 自身进行显式的多步结构化推理，让模型自己生成可解释的检测逻辑，再依据这一逻辑有针对性地修订幻觉内容；全程无需外部知识库或任务专属训练数据。
- **任务分类**：论文将幻觉按任务划分为五类：问答（QA）中的无依据断言与事实错误、对话（DA）中的实体错配与不一致、摘要（SUM）中的未验证细节与事实虚构、数学应用题（MWPs）中的约束缺失与病态问题、以及自身矛盾（SC）中的自相矛盾内容。
- **任务示例**: 处理轮廓可见于文内“HalluClean Overview”示例图中，例如解决“矛盾文本”问题时，通过提取主体、行为、时间/关键信息并对比，来判断两条文本信息是否矛盾。
- **框架结构**：HalluClean 由两个主要模块构成：
  1. **幻觉检测模块（Hallucination Detection）**：采用结构化推理流程，不直接做二分类判断，而是引导模型按三个步骤展开——步骤 1 任务规划（Task-oriented Planning，生成任务特定的验证计划）、步骤 2 规划引导推理（Plan-guided Reasoning，按计划逐步实施验证并输出推理过程）、步骤 3 最终判定（Final Judgment，输出 Yes/No 二元结论，同时保留推理依据）。
  2. **幻觉修订模块（Hallucination Revision）**：在检测到幻觉后，模型根据步骤 2 的推理轨迹（而非直接修改原文）识别需要修改的内容并生成修订版本，从而保证修正的精准性和可控性。
- **任务导向路由提示（Task-Oriented Routing Prompts）**：每种任务配有一条简洁的任务提示（见表 1），描述“给你输入怎样的文本、输出是否含幻觉”的判断目标；这些提示充当“任务适配器”，使框架在问答、对话、摘要、数学题、矛盾检测等任务间零样本切换。
- **方法特性总结**：模块化设计支持接入不同 LLM（如 GPT-3.5-turbo、DeepSeek-V3、Llama-3-70B 等，亦兼容开源模型）；所有阶段在一次推理流程中完成，仍属单次系统性调用；同时支持后续结合检索增强、跨语言数据等外部信息进一步提升检测效果。

## 3. 实验设计

- **数据集与 Benchmark**：
  - **HaluEval**：包含 3 类任务数据——问答（QA）、知识型对话（DA）、文本摘要（SUM），提供人类标注的幻觉正负样本。
  - **UMWP**：用于数学应用题（MWPs）幻觉检测，样本为无解/条件不全的病态数学问题。
  - **ChatProtect**：聚焦自相矛盾文本的检测任务（SC）。
  - **HaluBench**：医疗与金融领域（CovidQA、PubMedQA、FinanceBench）的涉域幻觉检测基准。
  - **跨语言验证**：中文基准 HalluQA 与 CMHE-HD，各 200 样本，用于测试跨语言泛化。
- **评价指标**：
  - **幻觉降低率（R）**：对比修订前后幻觉检出比例的变化，修订后文本由 GPT-4o-mini 重新评价。
  - **修订成功率（Q）**：修订输出与金标准之间的 BERTScore > 0.85 视为修订质量可接受；MWP 任务则用无解原因类别匹配来评估。
  - **检测性能**：以 F1 值和准确率（Accuracy）衡量模型判断结果与人类标注之间的吻合度。
- **对比方法**：
  - **直接判定基线（LLM-Direct Ask）**：GPT-3.5-turbo、GPT-4o-mini、Llama-3-70B、DeepSeek-V3、DeepSeek-R1 在直接提示下做出二分类判断。
  - **推理增强基线（以 GPT-3.5-turbo 为统一骨干）**：Step-by-Step、Plan-and-Solve、ChatProtect、SelfCheckGPT 等。
- **主要实验组**：
  1. 检测性能对比实验（表 3）：HalluClean 搭配不同骨干模型（GPT-3.5-turbo、DeepSeek-V3、Llama-3-70B），在五个任务上对比已有方法；统一骨干下对照现有推理方法。
  2. 修订性能对比实验（表 2）：统一衡量不同模型的幻觉降低率与修订质量，对同骨干模型进行公平比较。
  3. 消融分析（表 4）：逐步加入 Task-oriented Routing 与 Structural Reasoning 模块，拆解各组件贡献。
  4. 领域评估（表 5）：医疗与金融基准上的检测表现。
  5. 检索增强整合（表 6）：在 QA 任务上比较 retrieval-augmented（有无外部知识）设置下的表现。
  6. 跨语言评估（表 7）：在中文数据集 HalluQA、CMHE-HD 上测试。
  7. 骨干模型适配性分析（图 2、图 3）：不同骨干下检测模块的 F1/Accuracy 增益与修订模块的 R/Q 表现。

## 4. 资源与算力

- **论文全文未提及具体的算力配置**：未给出 GPU 型号、数量、训练时长或推理成本等信息。
- 从描述推断，HalluClean 属于零样本提示方法，不需要训练阶段。运行时开销以若干步 prompt 推理代价为主，并提供开源代码实现；但论文未系统报告不同模型和模块的总推理成本或 token 开销，也未提供效率分析。

## 5. 实验数量与充分性

- **实验数量与充分性评价**：
  - 实验覆盖面较广：主实验组包含 7 类场景（通用任务 ×5、领域 ×3、跨语言 ×2）+ 消融 + 检索增强设置，在检测与修订两个维度上均有量化结果。
  - 对照组设计整体合理：直接提问（direct ask）与既有方法对比均执行统一骨干（GPT-3.5-turbo），保证了比较公平性；对比了大量基线模型（Step-by-Step、Plan-and-Solve、ChatProtect等）和骨干模型差异。
  - 消融研究充分验证了两个设计组件的必要性；领域与跨语言的评估也增加了结论的一般性；结果表格呈现了 F1 与 Acc 两维指标，较全面。
  - 局限层面：尚缺少置信度/模型不确定性分析、输出 token 成本对比、修订后再次检测的细粒度一致性审计，以及多个骨干间统计显著性（significance test）报告；这略显不足。

## 6. 论文的主要结论与发现

- HalluClean 在五个代表性任务（QA、DA、SUM、MWPs、SC）上一致优于直接 LLM 判定方法和多种现有推理增强基线。
- 在检测方面：Ours-DeepSeek-V3 在 QA（F1 71.5%）、DA（F1 77.1%）和 MWPs（F1 89.1%）上取得最高 F1，并在所有五类任务上取得最高准确率。Ours-Llama-3-70B 也取得了具有竞争力且可在开源模型中部署的能力。
- 在修订方面：每个骨干的最终修订结果（R、Q）都强于直接对照组，相比直接生成质量的修补提升显著，并且在摘要任务上增益尤其大。
- 领域评估：医疗（CovidQA、PubMedQA）与金融（FinanceBench）的检测 F1/准确率均超过了强基线（例如 CovidQA上 F1 达到 91.7%），说明框架适用于高价值、隐私敏感的真实场景。
- 组件实验显示任务路由提示与结构化推理是互补的功能模块；只有“检测推理”结合“任务规划”才能接近最佳效果。
- 检索增强整合测试结果指出方法可与外部知识库机制互补；跨语言测试显示其具备较强的泛化能力。
- 主要方法论结论是：结构化分解+显式推理是实现高质量通用幻觉治理的关键；零样本提示性方法无需外部知识与模型微调也能获得显著增益。

## 7. 优点

- **方法层面**：
  - 任务不可知、轻量、即插即用，可适配不同规模和应用场景，支持本地部署和隐私保护要求下的开源模型使用；
  - 采用显式结构化推理流程，检测结果具有可解释性和可审计性，透明度和可控性高于直接二分类提示；
  - 仅用极简任务提示即可实现多个任务的通用切换，降低了构建大规模监督检测器所需的标注成本；
  - 将“检测”和“修订”衔接起来——修订过程把检测阶段的推理作为修正依据，目标指向更精准；
  - 代码已开放（GitHub），可复现性良好。
- **实验层面**：
  - 统一的 backbone 与指标体系让不同方法在同一起点下公平比较；
  - 跨领域和跨语言测试覆盖了真实场景与泛化风险，增强可靠性；
  - 设置了消融实验和检索增强的组合场景，使结论更严谨。

## 8. 不足与局限

- **依赖底层模型的推理能力**：完全依赖 LM 自身的推理正确度与输出质量完成检测和修订，没有外部的知识校验或约束机制，系统的“天花板”受 LLM 本身能力限制。
- **修订质量的度量与阈值设定**：以 BERTScore > 0.85 表示修订质量可接受，该阈值是否对各类任务都合理存在争议，尤其对数学题等结构性任务，单纯依赖文本相似度不能完整评估“是否消除了幻觉”；而数学应用题又是用类别匹配，多个任务的度量口径不统一。
- **潜在的评价偏差**：修订后的重新幻觉检测使用了 GPT-4o-mini，且将 GPT-4o-mini 作为评审判定者，可能会带来由判断者自身不同所引入的偏差和模型偏差影响。
- **零样本性能仍有差距**：部分任务与强监督/SFT 方法相比可能仍存在差距，而论文未与需训练的复杂系统（如基于额外数据评估的模型）对比，只能对提供公平背景下的相对收益下结论。
- **数据采样有限**：跨语言测试仅使用 200 条中文样本，通用性推断需谨慎；限定领域实验中金融数据规模明显小于医疗（FinanceBench 上的各个模型准确率较低）；任务集为人工测试基准而非真实LLM产品收集线上内容。
- **未充分报告成本/效率信息**：没有阐明结构化多步推理的 token 成本公式、不同模型的推理开销和延迟延迟差异。
- **缺少系统性的鲁棒性分析**：如提示微小扰动的影响、不同温度/解码策略带来的结果变化等。


（完）
