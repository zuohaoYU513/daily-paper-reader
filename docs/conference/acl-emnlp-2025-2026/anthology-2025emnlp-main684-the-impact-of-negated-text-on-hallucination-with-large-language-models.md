---
title: The Impact of Negated Text on Hallucination with Large Language Models
title_zh: 否定文本对大规模语言模型幻觉的影响
authors: "Jaehyung Seo, Hyeonseok Moon, Heui-Seok Lim"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.684.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 研究在否定文本中LLM的幻觉检测，直接涉及幻觉检测方法
tldr: 已有幻觉研究大多忽略否定文本的影响。本文提出三个研究问题，构建NegHalu数据集，将现有幻觉检测数据集重构为否定表达，系统评估LLM在否定语境下的幻觉识别能力。实验表明，LLM难以有效检测否定文本中的幻觉，常产生逻辑不一致或错误输出，凸显了否定对幻觉检测的挑战。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main684/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main684/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main684/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main684/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1635, \"height\": 1605, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 725, \"height\": 765, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1651, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1327, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 721, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 737, \"height\": 798, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 730, \"height\": 893, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1314, \"height\": 818, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1312, \"height\": 931, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1627, \"height\": 1014, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main684/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1651, \"height\": 1555, \"label\": \"Table\"}]"
motivation: 否定文本对LLM幻觉的影响尚待探索，已有检测数据集缺乏否定表达。
method: 构建NegHalu数据集，并通过实验研究LLM在否定语境下识别幻觉的能力。
result: LLM在否定文本上的幻觉检测效果差，常产生逻辑不一致的输出。
conclusion: 否定表达显著影响幻觉检测，需要专门的数据集和方法来应对。
---

## Abstract
Recent studies on hallucination in large language models (LLMs) have been actively progressing in natural language processing. However, the impact of negated text on hallucination with LLMs remains largely unexplored. In this paper, we set three important yet unanswered research questions and aim to address them. To derive the answers, we investigate whether LLMs can recognize contextual shifts caused by negation and still reliably distinguish hallucinations comparable to affirmative cases. We also design the NegHalu dataset by reconstructing existing hallucination detection datasets with negated expressions. Our experiments demonstrate that LLMs struggle to detect hallucinations in negated text effectively, often producing logically inconsistent or unfaithful judgments. Moreover, we trace the internal state of LLMs as they process negated inputs at the token level and reveal the challenges of mitigating their unintended effects.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：近年来，关于大语言模型（LLM）幻觉的研究在 NLP 领域日益活跃。现有幻觉检测研究（如 HaluEval、SelfCheckGPT、BamBoo 等基准）大多聚焦于如何识别模型输出中与上下文不忠实或与事实矛盾的内容。然而，**否定文本（negated text）对幻觉检测的影响几乎未被探索**。
- **核心问题**：否定标记（如 "not"、"never"、"no"、"without"）虽然只是单 token，却能从根本上改变句子的事实含义；而现有研究表明，LLM 对否定表达的处理能力普遍不足——它们往往将否定当作词法修饰符而非逻辑算子，导致逻辑推理出错、产生新型幻觉。
- **本文的核心目标**：系统性地回答三个研究问题：
  - **RQ1**：LLM 在否定文本中能否像肯定文本一样可靠地区分幻觉与忠实陈述？
  - **RQ2**：在幻觉检测过程中，模型内部能否识别否定引起的语义差异？
  - **RQ3**：定向干预策略（如上下文学习、思维链、知识编辑）能否改善否定文本中的幻觉检测？
- **整体含义**：否定表达是日常交流中的常见语言现象，若 LLM 在否定语境下系统性失效，将严重影响其在法律、医疗、科学等高可靠性场景中的落地应用。本文首次系统性揭示了否定文本对幻觉检测的深层影响，为该领域提供了新的研究方向和评估资源。

---

### 2. 方法论：核心思想、关键技术细节与流程

#### 2.1 总体思路
通过将已有的幻觉检测数据集重构为带否定表达的形式，引入 **NegHalu** 数据集，使模型在"前否定（pre-negated）"与"后否定（post-negated）"两种场景下重新进行幻觉判定，从而量化否定对检测能力的影响。

#### 2.2 NegHalu 数据集构建流程
- **源数据集**：选用三个主流幻觉检测基准：
  - HaluEval（QA、Dialogue、Summarization 三个子集）
  - BamBoo（AbsHallu、SenHallu 两个子集）
  - SelfCheckGPT-WikiBio（传记生成句级标注）
- **后否定变换（Post Negation）**：对关键字段（如 Halu-QA 的答案、Halu-Dialogue 的回复、Halu-Sum 的摘要、BamBoo 的假设、SelfCheckGPT 的生成文本）进行否定重构，要求**仅插入一次 "not"**，使原有标签发生翻转（忠实→幻觉，或幻觉→忠实），且新句子须符合真实世界事实与常识。
- **两轮生成流程（Round 1）**：使用 GPT-4o API，根据给定上下文和标签，生成逻辑连贯的后否定文本和新标签。提示词明确要求："通过仅添加一次 'not' 将 [C] 重构为否定陈述 [NEW C]，使 [Label] 相应变化。"
- **数据验证（Round 2）**：三个不同温度（0、0.7、1.2）的 GPT-4o 模型独立评估，标准包括：
  - **Logical Negation**：后否定文本是否逻辑地改变了原文本含义；
  - **New Label Validity**：新标签是否匹配后否定文本。
  - 仅当三者一致通过 [Pass, Pass] 才保留样本，确保数据质量。
- **人类评估**：作者对全部 1,950 个样本进行人工审核，修正了 13 个 HaluEval、11 个 SelfCheckGPT-WikiBio、3 个 BamBoo 中的无意义或事实错误样本；对 2 个双重否定案例进行了改写。
- **标签平衡**：HaluEval 与 SelfCheckGPT 中保持幻觉/忠实各 50% 的平衡比例；BamBoo 因样本量小不强行平衡。

#### 2.3 分析方法与干预策略
- **Logit Lens 观测**：通过将模型各层内部隐状态投影到词表空间，逐层追踪输入末尾 token 和首个生成 token 的概率变化，对比前/后否定输入下模型内部决策的动态差异，以判断模型是否能内在地区分否定带来的语义转变。
- **In-Context Learning（ICL）**：采用 0-shot、2-shot、4-shot 三种设置，2-shot 为默认；4-shot 包含前/后否定与幻觉/非幻觉的平衡示例。
- **Chain-of-Thought（CoT）推理**：在 2-shot 和 4-shot 基础上增加逐步推理提示，要求模型先说明判断理由再给出幻觉标签。
- **知识编辑（Knowledge Editing）**：采用 AlphaEdit（零空间约束的知识编辑方法），将参数更新投影到保留知识的零空间，避免破坏既有肯定知识。编辑语料包括：
  - **KE 1000**：来自 ROME 数据集的 1,000 条事实陈述；
  - **Atomic Fact**：从各数据集给定知识中解析出的原子事实，经 GPT-4o 转换为否定知识。
  - 基于 100,000 条 Wikipedia 三元组构建保留知识基，通过因果追踪确定编辑层（Llama3 的 4–8 层）。

---

### 3. 实验设计：数据集、基准与对比方法

#### 3.1 数据集与任务场景
| 数据集 | 子集 | NegHalu 样本数 | 任务类型 |
|---|---|---|---|
| HaluEval | QA | 400 | 问答幻觉检测 |
| HaluEval | Dialogue | 400 | 对话回复幻觉检测 |
| HaluEval | Sum | 400 | 摘要幻觉检测 |
| BamBoo | AbsHallu | 152 | 抽象级摘要幻觉判定 |
| BamBoo | SenHallu | 136 | 句级事实性判定 |
| SelfCheckGPT-WikiBio | — | 462 句（由 238 个段落拆分） | 传记生成句级幻觉判定 |

#### 3.2 评估模型
- **Llama-2-7B-Chat**
- **Llama-3-8B-Instruct**
- **Mistral-7B-Instruct-v0.3**
- **Qwen3-4B**

均为开源社区广泛使用的基准模型，保证结论的多样性和可复现性。

#### 3.3 指标设置
- HaluEval：Accuracy
- BamBoo：Precision / Recall / F1
- SelfCheckGPT-WikiBio：Accuracy + 模型响应平均分 + 标签与响应间绝对距离

#### 3.4 对比与消融
- **核心对比**：每组模型在 pre-negated vs. post-negated 输入下的性能差异。
- **ICL 对比**：0-shot / 2-shot / 4-shot。
- **CoT 对比**：2-shot+CoT / 4-shot+CoT。
- **知识编辑对比**：无编辑 / KE 1000 编辑 / Atomic Fact 编辑。
- **否定类型扩展（NegHalu+）**：将原 HaluEval 中 5% 的显式否定替换为隐式否定（如 doubt, hardly, unlikely that, questionable whether）和形态否定（如 un-, in-, im-, dis-, -less），验证结论对多样否定形式的普适性。

---

### 4. 资源与算力

- **文中明确说明**：
  - 实验使用**单块 NVIDIA A6000 GPU（48GB 显存）**，搭配 **AMD EPYC 7513 32 核 CPU**。
  - 所有数据集均采用**贪心解码**，不使用采样方法。
  - 最大输出长度：HaluEval 为 4096，BamBoo 为 32，SelfCheckGPT-WikiBio 为 5。
- **未明确提供的细节**：具体训练/推理时长、总 GPU 小时数、以及更大规模模型的对比实验均未给出。作者在局限性中坦承，受计算资源限制未能验证更大参数的模型。

---

### 5. 实验数量与充分性

#### 实验规模
- **主实验**：4 个模型 × 6 个数据集子集 × 前/后否定双场景，覆盖表 4、表 5、表 6 的完整结果。
- **ICL 实验**：4 模型 × 3 shot 设置 × 3 个数据集族（表 7）。
- **CoT 实验**：4 模型 × 2 种 shot 条件 × 3 个数据集族（表 8）。
- **知识编辑实验**：Llama3 在 3 个数据集族 × 2 种编辑语料（图 3）。
- **否定类型扩展实验**：4 模型 × 3 个 HaluEval 子集（表 9）。
- **内部状态分析**：多组 Logit Lens 可视化（图 2、图 4）。
- 合计实验规模较大，数据集来源多样、任务类型覆盖 QA / 对话 / 摘要 / 句级事实性判断，具备较好的全面性。

#### 充分性与客观性评估
- **优点**：数据构建经过了严格的自动验证（三温度模型一致通过）+ 人工审核，保证了数据质量；实验覆盖了多种模型架构和多种否定类型；同时考察了多种干预策略。
- **不足**：
  - **BamBoo 样本量较小**且存在一定标签不平衡，可能影响 F1 的稳健性。
  - **验证者与生成者同为 GPT-4o**，即便采用三温度集成，仍存在一定自偏风险（作者在局限性中已承认）。
  - 未测试更大规模模型（如 70B 及以上），外部有效性受限。
  - HaluEval 仅使用子集，可能使前否定基线结果与全量数据略有出入。
  - 知识编辑实验仅在 Llama3 上进行，未推广到其他模型。

---

### 6. 主要结论与发现

#### A1：LLM 在否定文本的幻觉检测中表现出显著的性能下降和标签偏差
- 在 HaluEval、BamBoo、SelfCheckGPT 的所有子集上，4 个模型在 18 个后否定场景中有 17 个出现性能下降。
- 模型在否定输入下明显倾向于将内容判定为"幻觉"：后否定场景中幻觉判定增加约 21%–206%，忠实判定下降约 68%–75%。
- 该现象跨任务（QA、对话、摘要、句级判断）和跨领域（通用知识、科学、传记）一致存在，表明否定对幻觉检测的影响具有**任务无关性和普适性**。

#### A2：模型内部无法清晰区分前/后否定文本
- Logit Lens 显示，模型在中间层和末层对否定输入表现出明显概率波动，但前/后否定之间的内部表示差异极小，说明模型未能将否定视为逻辑变换，而只是当作一个普通 token。
- 与肯定场景相比，后否定输入下模型对错误预测的置信度更高——即模型在"自信地犯错"，这正是幻觉风险的典型特征。

#### A3：干预策略效果有限
- **ICL**：2-shot 平均表现最佳，但增益在不同模型和数据集间不一致，更多示例不必然提升性能；说明提升主要依赖指令遵循能力的改善而非对否定的真正理解。
- **CoT**：在部分模型（Mistral、Llama2）的前否定 HaluEval 上有改进，但在后否定场景下提升微弱甚至下降，无法作为根本解决方案。
- **知识编辑（AlphaEdit）**：KE 1000 编辑能小幅改善后否定性能且对前否定知识伤害较小，但在 SelfCheckGPT 上出现了前否定性能下降；不能系统性消除由否定引发的幻觉偏差，说明否定问题已内嵌于模型深层表示之中，而不仅是知识层面的缺陷。

#### 否定类型的扩展影响
- 在加入隐式和形态否定（NegHalu+）后，整体结论不变，但不同模型展现出不同的弱点分布：Llama3 和 Qwen3-4B 在 QA 和对话任务上出现更严重的性能下降；Llama2 和 Mistral 的退化幅度略减。这说明仅用显式否定评估会低估模型的真实脆弱性。

---

### 7. 优点

- **研究选题新颖且重要**：首次系统性研究否定文本对 LLM 幻觉检测的影响，填补了该交叉领域的重要空白。
- **数据集构建方法严谨**：NegHalu 采用两轮 GPT-4o 生成与验证（三温度集成、严格 Pass/Pass 标准）+ 人工审核，最大限度保证数据质量和标签正确性；定性示例（附录 F）展示了正反案例，增强透明度和可信度。
- **多维度实验覆盖**：4 种模型 × 3 类基准 × 多任务 × 多干预策略，实验体量丰富；同时覆盖显式、隐式、形态三类否定，提高了结论的普适性。
- **内部机制分析深入**：Logit Lens 逐层追踪模型内部概率变化，从表征层面揭示了"否定未能作为逻辑算子参与推理"的根本原因，而非停留在表面性能对比。
- **客观承认局限**：文中明确列出计算资源限制、GPT-4 作为生成/评判的双重角色偏差、干预方案不完美等局限，显示了研究态度的诚实性。
- **资源开源共享**：NegHalu 数据集可复用于后续研究，为该领域的进一步探索奠定了基础设施。

---

### 8. 不足与局限

#### 实验覆盖方面
- **数据集规模与平衡性**：BamBoo 子集样本较少（152 / 136）且存在标签不平衡；HaluEval 仅取 1,500 个子集而非全量，可能使 pre-negated 基线与官方全量结果存在微小差异。
- **模型覆盖面有限**：受算力限制，未评估更大规模（≥70B）或商业闭源模型；不同规模/厂商模型可能在否定处理能力上表现截然不同。

#### 偏差风险
- **生成与评价同模型**：NegHalu 由 GPT-4o 生成，也由 GPT-4o（不同温度）验证，虽然采用三模型集成 + 人工抽查，但仍可能存在某种系统性偏好；作者据此建议后续研究中引入异源验证。
- **知识编辑的局限性**：作者在实验中排除了 ROME 和 MEMIT（因对前否定知识破坏过大），仅测试了 AlphaEdit，且仅在 Llama3 上进行，通用推广需谨慎。

#### 应用限制
- 本文着重于"诊断"问题，但在"治疗"层面未能提出根本性解决方案。ICL、CoT、知识编辑均无法彻底修复否定导致的幻觉偏差，因此面向实际应用时，否定文本场景仍缺乏可落地的缓解手段。
- NegHalu+ 的否定类型比例仅 5%，对更复杂否定（如双重否定、部分否定、嵌入否定）的覆盖仍显不足。
- 未涉及多语言场景；研究仅基于英文数据集，对中文、日语等语言中否定现象的特殊性（如没有显式否定词或语序敏感）未做探讨。

---

（完）
