---
title: "Confidence Under the Hood: An Investigation into the Confidence-Probability Alignment in Large Language Models"
title_zh: 外壳之下的置信：大语言模型置信度与概率对齐的探究
authors: "Abhishek Kumar, Robert Morabito, Sanzhar Umbet, Jad Kabbara, Ali Emami"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.20.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 考察模型内部token概率置信度与言语表达自信之间的一致性，直接关联置信度校准与真实正确性。
tldr: 随着大模型应用增多，生成回答中的自我置信判断与真实可靠性密切相关。该论文提出“置信度-概率对齐”概念，将模型内部的token概率置信度与模型在明确被询问时所表达的确定度联系起来。基于多种数据集和内省式提示方法，研究者系统探测了内部置信与该两维度上表达出的置信之间的对应情况，揭示二者的一致与偏差，为如何理解和校准模型自我报告置信度提供了分析框架。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 648, \"height\": 1011, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 947, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 756, \"height\": 801, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 755, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1212, \"height\": 231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1216, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 737, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1441, \"height\": 2259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1187, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1212, \"height\": 768, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 755, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1449, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long20/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 739, \"height\": 486, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1376, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1666, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1064, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 1756, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1659, \"height\": 1112, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1660, \"height\": 1346, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1661, \"height\": 2284, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1656, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long20/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1659, \"height\": 572, \"label\": \"Table\"}]"
motivation: 大语言模型被询问确定度时给出的置信与其内部令牌概率之间未必一致，但二者共同影响输出可靠性。
method: 提出置信-概率对齐概念，并设计结构化评分尺度和内省式提示来对比内部置信与显式置信。
result: 在不同数据集上测得内部与显式置信的对齐程度，并识别出影响对齐的因素。
conclusion: 仅看表面置信或仅看内部概率都不充分，理解二者的对齐关系才能更好校准大模型可信度。
---

## Abstract
As the use of Large Language Models (LLMs) becomes more widespread, understanding their self-evaluation of confidence in generated responses becomes increasingly important as it is integral to the reliability of the output of these models. We introduce the concept of Confidence-Probability Alignment, that connects an LLM’s internal confidence, quantified by token probabilities, to the confidence conveyed in the model’s response when explicitly asked about its certainty. Using various datasets and prompting techniques that encourage model introspection, we probe the alignment between models’ internal and expressed confidence. These techniques encompass using structured evaluation scales to rate confidence, including answer options when prompting, and eliciting the model’s confidence level for outputs it does not recognize as its own. Notably, among the models analyzed, OpenAI’s GPT-4 showed the strongest confidence-probability alignment, with an average Spearman’s ̂𝜌 of 0.42, across a wide range of tasks. Our work contributes to the ongoing efforts to facilitate risk assessment in the application of LLMs and to further our understanding of model trustworthiness.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

大语言模型（LLM）已被广泛应用于医疗、法律、教育等高风险领域，用户往往依赖模型自我报告的置信程度来评估输出的可靠性。然而实践中发现，模型在生成文本中“口头表达”的确定度与其真实的内部概率可能并不一致，这种不一致可能导致幻觉问题（如自信地引用不存在的参考文献）被掩盖。基于此，论文提出 **置信-概率对齐（Confidence-Probability Alignment）** 这一核心概念：将 LLM 的**内部置信（internal confidence）**——以答案 token 概率为量化指标——与模型在明确被询问时所表达的**确定性/置信度（verbalized certainty）** 联系起来考察其相关性。作者强调：如果两者不对齐，诸如 Self-Consistency、Tree of Thoughts 等依赖模型自我评估的提示技术可能产生误导性结果；理解这种对齐关系也是评估 LLM 可信度与风险的基础。这是本文的出发点与核心贡献所在。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

> 核心思想：用 token 概率量化“内部置信”，用结构化内省式提示引出“言语化确定度”，再以秩相关衡量二者的一致性。

具体方法可分为四步：

**（1）响应生成（结构化问答）**
- 对每个问题 Q 配上选项集合 O_set（如 A–E 五选一），拼接为形如 `Q + "\n" + Option A + ... + "\nAnswer: "` 的提示；
- 从模型生成的文本中提取所选答案 a_i（属于 O_set），作为后续置信度评估的基础。

**（2）内部置信度（Internal Confidence）的量化——算法 1**
- 逻辑：将 log 概率或 logits 转成标准 token 概率：
  - GPT 系列：P(T_i) = exp(log P(T_i));
  - 开源模型（提供 logits）：P(T_i) = e^{L(T_i)} / Σ_j e^{L(T_j)}（softmax）；
- 引入“调整后答案 token 概率”（adjusted answer token probability）以规避 token 歧义（如大小写 `B` vs `b`）：
  - 对每个选项，找出其对应的一组 token 并取其中的**最大概率**作为该选项的代表概率 P_O；
  - 将所有选项的代表概率求和得 P_S；
  - 用所选答案的最大概率 P_M 除以 P_S，得到归一化的内部置信度 **P_IC**。
- 该归一化做法理论上能过滤“选项间整体概率基础率”差异带来的影响。

**（3）言语化确定度（Verbalized Certainty）的获取——置信查询提示（CQP）**
- 采用**第三人称视角（TPP）**（让模型评价一个被提问的“语言模型”的答案，而非自身）以减轻自我偏好偏差；
- 使用**选项上下文化（OC）**（在询问置信度时仍展示原始全部选项，帮助模型进行比较与校验）；
- 使用**李克特式定性量表（LSU）**：`a. Very Certain / b. Fairly Certain / c. Moderately Certain / d. Somewhat Certain / e. Not Certain / f. Very Uncertain`，随后映射到数值 1.0/0.8/0.6/0.4/0.2/0；
- 论文通过预实验比较了数值量表、定义式选项、严格语法等替代方案，最终确定上述 CQP 设计。

**（4）对齐评估**
- 使用 **Spearman 秩相关系数 ρ** 衡量内部置信与言语化确定度在同一组问答样本上排序的一致性：ρ = 1 − 6Σd_i² / [n(n²−1)]，d_i 为两者秩次之差；
- 秩相关无需假设分布，符合 token 概率与言语量表的非正态特性。

## 3. 实验设计：使用数据集/场景、基准、对比的方法

- **数据集（5 个多选知识推理基准）**：
  - CommonsenseQA（CSQA，常识问答）
  - QASC（多句组合推理问答）
  - RiddleSense（谜语推理）
  - OpenBookQA（开放科学知识问答）
  - ARC（AI2 推理挑战）
- **模型（6 个，兼顾专有与开源）**：
  - OpenAI：GPT-3（text-davinci-001）、InstructGPT-3（text-davinci-002）、InstructGPT-3 + RLHF（text-davinci-003）、GPT-4（gpt-4-0613）
  - 开源：Microsoft Phi-2-2.7B、HuggingFace Zephyr-7B
- **评估协议**：对所有问题统一生成答案并采集 token 概率——按算法 1 得到 P_IC；再用 CQP 提示模型输出言语化确定度；最后计算两者的 Spearman ρ，并做了以下不同实验模块：
  - 数据集粒度对齐评估（表 1）
  - 温度参数对言语化确定度稳定性的影响（图 3）
  - 正确性与置信度/确定度的综合分析（矩阵图）
  - 三种提示组件的消融分析（TTP、OC、LSU 的组合对照）
  - 对齐类型的定性误差分析（一致对齐、内部过度自信、外部过度自信、一致不一致四种类型）

就“对比方法”而言，本文提出的是一个新的评估框架而非新的生成方法，因此较量的不是不同生成方法，而是不同模型、不同数据集和不同提示成分下的对齐程度。

## 4. 资源与算力

论文简要提到：“为进行所有实验，共消耗约 132.5 个计算小时（compute hours）”；GPT 系列使用 OpenAI 公共 API，开源模型（Phi-2、Zephyr-7B）未明确指定 GPU 型号与数量。总体而言，**文中没有披露具体 GPU 型号、数量和训练/推理的精细时长**，只给出了一个粗略的总量级，因此无法据此评估算力配置的细节。

## 5. 实验数量与充分性

- **数量**：实验覆盖 6 个模型 × 5 个数据集的主对齐评估；此外还有温度稳定性实验、正确性-置信度矩阵分析、完整三组件及其组合的消融实验（多组提示配方对比）、以及大量定性实例分析（对齐类型与失败案例分析）。论文附带的表格与可视化内容较丰富，共 20 页（含附录）。
- **充分性**：从覆盖面上看，跨模型（专有 vs 开源、不同 RLHF 程度）与跨数据集（常识、科学、谜语、推理）的设计比较全面，消融分析也为提示设计的内在贡献提供了证据；所有表格中的 ρ 值显著性均有标注（p < 0.01）。不过由于提示设计完全依赖人工构造、未在更多基座模型上验证，且论文承认无法获取 PaLM、Chinchilla 等模型的内部概率，所以实验的广度仍受限制。总体而言，就“提出概念并提供初步证据”的目的来说实验是充分的，但就“推广结论”而言尚有欠缺。

## 6. 论文的主要结论与发现

1. **GPT-4 的对齐最强**：在不同数据集上 Spearman ρ 从 0.35（ARC）到 0.47（QASC），平均约 0.42；与之相比，GPT-3 的对齐接近 0 甚至为负，表明模型代际与对齐水平明显相关。
2. **RLHF 变体对齐更好**：InstructGPT-3 + RLHF 明显优于没有 RLHF 的 InstructGPT-3，提示 RLHF 训练与置信度校准之间存在潜在关联。
3. **开源小模型表现差**：Phi-2 与 Zephyr-7B 的对齐很差甚至为负，且常无法生成有效的言语化确定度答案（反复给出解释、重复选项而不做出量表选择）——小模型在“同时生成和评估”任务上能力不足。
4. **正确性与置信度正相关**：在 GPT-4 上，越“确定/置信”的回答往往是正确答案；这与 Meister et al. 观察到的 probability-quality paradox 形成补充，显示至少在多项选择任务上高置信度与高正确率有关。
5. **温度的影响因数据集而异**：温度升高普遍增大言语化确定度的波动，但不同任务敏感度差别显著（如 QASC 较稳定，RiddleSense/OpenBookQA 更易波动），提示需要按数据集调整温度。
6. **三种提示组件全部组合效果最佳**：TPP 与 OC 单独作用有限或依数据集而异，而 LSU 的加入持续提升对齐程度。

## 7. 优点

- **概念创新且实用**：将“行为层面语言化置信”与“机制层面 token 概率”关联起来的对齐指标，为“模型自我报告是否值得相信”提供了可量化、可复现的评估标尺，直接回应了 LLM 可可靠性评估的紧迫需要。
- **多模型、多数据集的系统化评测**：综合专有与开源模型、老至新代际以及多个不同难度的 QA 数据集，结论具有较好的横向可比性。
- **算法与提示设计有细节**：
  - 算法 1 处理了 token 歧义（大小写、多种 token 表示），提高了内部置信度量化的鲁棒性；
  - 设计第三人称视角降低自偏好偏差、选项上下文化以让模型在比较中给出确定度的思路，均有其理论依据。
- **消融实验规范**：对每个提示组件（TTP/OC/LSU）进行单独与组合的消融，并报告了不同配方在多个数据集上的效果，让“提示设计”从技巧变为可审计的设计选择。
- **定性错误分析**：总结出四种对齐类型（一致对齐、内部过度自信、外部过度自信、一致不一致），以及小模型失败案例的类型学，便于后续针对校准做细粒度改进。
- 附带了开源代码与互动样例，有助于结果复现与后续研究。

## 8. 不足与局限

- **内部概率获取限制**：无法获取 PaLM 2、Chinchilla 等模型内部的 logits/log-probs，因此结论的适用范围限于可访问内部置信的模型，外部效度有限。
- **语言局限**：实验仅使用英语，对形态更丰富、句法更复杂的语言未必适用，跨语言可靠性还需验证。
- **元层面推理的固有风险**：要求模型评估“自己的答案”涉及元认知层面的推理，此过程可能与基础推理的置信度不耦合；TPP 虽可缓释部分自我偏好偏差，但难以完全消除。
- **对提示的高度依赖**：言语化确定度完全依赖人工设计的 CQP，不同的提示措辞、量表粒度和顺序可能造成对齐指标波动；论文已做部分设计探索，但未用更系统的提示敏感性分析（如多种随机重复）来提高稳健性。
- **模型准确性并非优化的目标**：论文聚焦“对齐”而非“提高正确率”，因此对于模型的准确性反馈与自适应校准策略留白。
- **伦理风险**：揭示置信度-概率不对齐可能被滥用（如更逼真地生成貌似自信的错误内容）；用户仍需批判性审视输出，需要更强的伦理准则与缓解机制。
- **计算与复现透明度有限**：未明确给出 GPU 型号、数量或逐任务/逐模型的成本拆分，整体“约 132.5 小时”的统计口径偏粗。
- **对齐程度仍不理想**：即使表现最好的 GPT-4，其平均 ρ 也仅在 0.42 左右，属于中等相关，表明大模型距离“所说即所想”仍相距甚远。

（完）
