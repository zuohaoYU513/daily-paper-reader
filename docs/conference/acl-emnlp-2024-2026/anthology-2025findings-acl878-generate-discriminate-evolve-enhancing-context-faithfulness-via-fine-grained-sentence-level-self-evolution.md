---
title: "Generate, Discriminate, Evolve: Enhancing Context Faithfulness via Fine-Grained Sentence-Level Self-Evolution"
title_zh: 生成、判别、进化：通过细粒度句子级自我进化增强上下文忠实性
authors: "Kun Li, Tianhua Zhang, Yunxiang Li, Hongyin Luo, Abdalla Mohamed Salama Sayed Moustafa, Xixin Wu, James Glass, Helen Meng"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.878.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向RAG与长问答的句子级自进化上下文忠实性增强与幻觉缓解
tldr: 检索增强长问答与知识冲突场景中，大语言模型容易生成与给定上下文不一致的内容，造成幻觉。作者提出GenDiE自进化框架，结合生成与判别训练，在句子粒度上让模型具备自生成与自打分能力，从而定向优化上下文忠实性。该方法无需外部标注即可通过自我进化缓解幻觉，为构建更可信的RAG系统和长文档问答提供了细粒度训练范式。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl878/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl878/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl878/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 688, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 841, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 745, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl878/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 336, \"label\": \"Table\"}]"
motivation: 检索增强长问答和知识冲突场景中，模型易生成与上下文不一致的内容，需要有效的忠实性改进方法。
method: 提出GenDiE框架，在句子粒度上联合生成与判别训练，利用LLM自生成和自打分能力进行自进化优化。
result: 该方法可增强模型对给定上下文的句子级忠实性，减少幻觉并缓解知识冲突。
conclusion: 为RAG与长问答的忠实性提供无需外部标注的细粒度自进化训练方案。
---

## Abstract
Improving context faithfulness in large language models is essential for developing trustworthy retrieval augmented generation systems and mitigating hallucinations, especially in long-form question answering (LFQA) tasks or scenarios involving knowledge conflicts. Existing methods either intervene LLMs only at inference without addressing their inherent limitations or overlook the potential for self-improvement. In this paper, we introduce GenDiE(Generate, Discriminate, Evolve), a novel self-evolving framework that enhances context faithfulness through fine-grained sentence-level optimization. GenDiE combines both generative and discriminative training, equipping LLMs with self-generation and self-scoring capabilities to facilitate iterative self-evolution. This supports both data construction for model alignment and score-guided search during inference. Furthermore, by treating each sentence in a response as an independent optimization unit, GenDiE effectively addresses the limitations of previous approaches that optimize at the holistic answer level, which may miss unfaithful details. Experiments on ASQA (in-domain LFQA) and ConFiQA (out-of-domain counterfactual QA) datasets demonstrate that GenDiE surpasses various baselines in both faithfulness and correctness, and exhibits robust performance for domain adaptation.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义（研究动机和背景）

- **应用场景痛点**：在**检索增强生成（RAG）**系统中，大语言模型需要依赖外部提供的证据段落生成答案，然而模型自身的**参数化记忆**（预训练知识）与外部上下文之间常存在**知识冲突**，导致模型忽视给定上下文、过度依赖内部先验，从而生成与上下文不符的内容（即“忠实性幻觉”）。
- **现有方法的两类不足**：
  1. **仅推理期干预**（如提示工程、上下文感知解码 CAD）虽然有效，但没有从根本上修正模型的内在缺陷；
  2. **训练期方法**（如 Self-RAG、Context-DPO 等）虽然在参数层面改进忠实性，但通常只做**一轮优化**，没有充分利用模型自我提升的潜力。
- **关键盲点**：已有训练方法大多在**完整答案级别**（holistic answer level）进行整体优化。在**长文本问答（LFQA）**中，一个段落长度的答案内部各句的忠实性参差不齐，整体优化容易**漏掉不忠实的细节句子**。
- **本文目标**：提出一个**句子级、自进化**的训练与推理框架，使模型不仅可以生成忠实内容，还能对句子是否忠实于上下文进行**自我判别**，并通过迭代训练持续改进，从而缓解幻觉、增强 RAG 可信度。

## 论文提出的方法论

### 核心思想

GenDiE（**Gen**erate, **Di**scriminate, **E**volve）将训练粒度从“完整答案”下降到“句子”，将每个句子视为独立优化单元；同时结合**生成目标**与**判别目标**的多任务训练，赋予模型既会生成又会打分的双重能力，使其可以**自我生成→自我打分→自我进化**，实现免外部标注的迭代式改进。

### 学习目标（多任务训练目标）

对每个目标句子 a（给定共享前缀 A≺a）：

```
L = 语言建模目标 + λ × 判别目标
```

- **语言建模目标**：最大化生成忠实句子（来自目标答案）的对数概率；
- **判别目标**（受 ORPO 启发）：让模型给忠实句子 a 赋予的忠实度分数 Sₐ 高于负样本句子 a′，判别损失内嵌了一个类似于 odds ratio 的项，无需参考模型；
- 忠实度分数定义为句子级长度归一化对数概率：Sₐ = log Pθ(a | q, P, A≺a)；
- λ 设为 0.5，训练使用 QLoRA 参数高效微调。

### 两阶段迭代数据构建

1. **预阶段（Pre-stage，第一轮）**：
   - 使用种子数据集（ASQA）中**标准答案的句子**作为正样本；
   - **负样本**由模型在**不提供证据段落**的条件下自生成（仅给定问题和答案前缀），因为缺少外部上下文，这类句子通常不够忠实；
   - 通过一个启发式 NLL 损失下降率过滤规则（式 4）筛选负样本，确保“正样本加段落比不加段落的改善程度 > 负样本的相应改善程度”，以维护正/负优劣关系的有效性。

2. **自进化阶段（Self-evolving，后续轮次）**：
   - 不再使用标准答案句子，而是由**上一轮模型 θₜ₋₁** 自生成候选句子并使用其自打分能力评估；
   - 设计了**树状结构采样（tree-structured sampling）**：每次基于前缀采样 n 个不同的下一句，形成 n 叉树，每条根到叶的路径即一个完整答案；路径遇到 [eos] 即终止；用 EM（精确匹配）筛选最接近标准答案的路径；
   - 将该路径上的每个节点句子与其“兄弟节点”句子（共享同一前缀）配对，若正样本自打分高于负样本，则构成对比句对进入下一轮训练集。

### 推理：分层推理（Hierarchical Inference）

- **内层**：令牌级解码，可采用 beam search 等常规方法生成单个句子；
- **外层**：句子级 beam search——每步对当前每个 beam 生成 M 个候选句子，根据长度归一化的累计忠实度分数选出 Top-N 作为下一步前缀，直到全部终止，返回累积分数最高的整段答案；
- 这样让自打分能力在推理时也参与句子级搜索，而不只是训练数据构造。

## 实验设计

### 数据集与评测场景

| 数据集 | 用途 | 场景特点 |
|---|---|---|
| **ASQA** | 域内 LFQA benchmark | 基于 AmbigQA 的模糊问题长答案数据集，段落级众包答案；检索结果用 GTR 稠密检索器 |
| **ConFiQA** | 域外（out-of-domain）反事实 QA | 提供与模型参数知识相冲突的反事实段落，专门评测上下文忠实性；上下文由论文直接提供 |

- 训练仅在 ASQA 上做，ConFiQA 只用于评测，以检验模型的**域适应与泛化能力**。
- 指标包括正确性（EM Recall、Hit）与忠实性（T5-11B NLI 模型、AlignScore）。

### 对比方法

- **训练无关**：In-context Prompting（gpt-4o、Llama-3.1-8b-Instruct）、CAD（上下文感知解码）、抽取式句子选择（stella-1.5B、instructor-large）；
- **训练相关**：Standard SFT（greedy / beam3）、GenDiE 的变体——**answer-level**（答案级优化）与 **gold-answer**（始终使用标准答案句子作为正样本）、以及外部方法 **Context-DPO**。

### 训练设置

- 基础模型为 Llama-3.1-8b，使用 QLoRA（4-bit，rank 8），AdamW，lr=1e-5，总共训练 **3 轮迭代**，每轮 1 个 epoch；硬件为 NVIDIA A6000 GPU。

## 资源与算力

- 论文仅提及使用 **NVIDIA A6000 GPU** 及 QLoRA 参数高效微调，并提到“由于计算资源限制”，未对不同多任务训练目标做详尽对比；
- **未明确说明**GPU 数量、总训练时长、总计算量（FLOPs）等具体数据。

## 实验数量与充分性分析

- **主实验**：在 ASQA 与 ConFiQA 两个 benchmark 上与两大类（训练相关/无关）约 8 种方法进行了多维指标对比；
- **消融与剖析实验**：
  1. 自进化有效性对比（GenDiE vs GenDiE gold-answer 跨轮次表现）；
  2. 自打分能力有效性（用 T5-11B 外部打分替代自打分训练出 GenDiE_T5，与其迭代2对比）；
  3. 句子级 vs 答案级优化对比（跨轮次）；
  4. 预阶段负样本过滤有效性的消融（filtered vs non-filtered）；
  5. 与 Context-DPO 的额外对比实验；
  6. 推理方式对比（greedy、vanilla beam、hierarchical）。
- **公平性与客观性**：整体设计合理，控制了同训练数据、同解码方式等变量进行对比；多次采用“同 checkpoints/同数据来源”对比来排除混淆因素；还区分了 in-domain/out-of-domain 的 prompting 结果，使比较更公平；案例研究展示了句子级方法相对答案级方法在内容忠实度上的直观差异。
- **充分性判断**：实验覆盖较全面，能有力支撑核心主张；但仅在 **ASQA→ConFiQA** 一个方向做域外泛化验证（ConFiQA→ASQA 仅用于与 Context-DPO 对比），域适应方向的鲁棒性验证还可以更丰富；数据规模中等（ASQA 约 3414 个训练实例、948 个测试实例）。

## 主要结论与发现

1. GenDiE在**忠实性**和**正确性**两个维度均超越多数 baseline：在使用 greedy 时即优于大多数方法；配合 **hierarchical inference**，在 ASQA 上 AlignScore 达 84.90、T5NLI 达 82.03，均显著高于其他方法。
2. **自进化有效**：随着迭代轮次增加，GenDiE 在两个数据集上持续提升，且优于一直使用标准答案句子的 gold-answer 变体——在域外 ConFiQA 上 gold-answer 出现性能下降而 GenDiE 仍保持增长，说明自进化可以缓解域偏移的负面影响。
3. **自打分能力可靠**：以自打分构造数据训练的 GenDiE_iter2 与用外部 T5 打分训练的 GenDiE_T5 忠实性相当，说明模型内置评分器可以承担句子忠实性评估任务，且避免了外部打分为导向时正确率反而下降的问题。
4. **句子级优化优于答案级优化**：GenDiE answer-level 在 ASQA 上忠实性每况愈下（评估整段答案的对比对难以保证可靠性），而 GenDiE 因细粒度监督而持续提升；长答案场景下句子级范式尤其重要。
5. **分层推理增益显著**：训练后的模型若只用 greedy/vanilla beam 解码会浪费其打分能力；分层推理（token 级 + 句子级 beam search）带来了大幅性能提升，是一种有效的测试时扩展。
6. **域外鲁棒性**：即便是在 ASQA 上训练、ConFiQA（反事实冲突场景）上测试，GenDiE 仍优于在该数据集域内训练的 Context-DPO。

## 优点

- **细粒度的句子级训练范式**：针对长答案各句忠实性不均的特点，以句子为单元优化，监督信号更精确，且支持句子级推理搜索。
- **“生成+判别”一体化的自进化闭环**：模型既能生成句子又能自打分，两者的结合使训练数据可随迭代不断自我改进，避免了对人工标注或外部奖励模型的持续依赖。
- **训练目标设计精炼**：采用类似 ORPO 的无参考模型偏好优化目标，用长度归一化的句子对数概率做忠实度分数，简洁且与生成概率天然一致。
- **分层推理具有启发性**：将打分能力用于推理期的句子级 beam search，充分利用了模型双重能力，思路清晰；可视化的案例（Tab. 4）直观展示了每一步的候选序列选择过程。
- 消融设计较缜密，**多角度验证**了句子级粒度、自打分、自进化和推理搜索等各组件的贡献，且对结果解释到位，分析较客观。

## 不足与局限

- **泛化场景有限**：论文只在长问句QA（ASQA）和反事实QA（ConFiQA）上评测，作者也承认尚未验证在需要**快速变化的世界知识**的其他 QA 任务上的泛化性。
- **多任务训练目标探索不足**：作者自述因计算资源限制，仅测试了基于 ORPO 的目标，未比较其他多任务训练目标（如单纯 DPO、其他判别损失形式）的影响。
- **推理开销较大**：分层推理需要为每个句子生成多个候选并做句子级搜索，相比标准推理有**额外计算成本**；作者指出通过算法优化可以进一步降低，且这一测试时开销与其收益相比是合算的，但并未提供实际加速方案；树状结构采样阶段同样需要多轮生成与打分，训练成本较高。
- **两个潜在偏差风险**：
  1. 使用**标准答案/EM 匹配**作为正样本或路径选择标准，可能与数据集的参考答案有较强耦合并引入偏差；
  2. 自打分可能继承模型自身先验偏好，在判断“忠实于上下文”时也可能误把“符合模型内部知识”的句子判为忠实，对知识冲突极强或上下文本身含噪声的场景可能造成数据污染。
- **资源信息不透明**：未报告 GPU 数量、训练总时长与总能耗等具体算力细节。
- 域适应评估只覆盖了一个方向，缺少更多元领域（如医疗、法律、金融）的迁移验证。

（完）
