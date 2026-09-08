---
title: "MMBoundary: Advancing MLLM Knowledge Boundary Awareness through Reasoning Step Confidence Calibration"
title_zh: MMBoundary：通过推理步骤置信度校准提升多模态LLM知识边界意识
authors: "Zhitao He, Sandeep Polisetty, Zhiyuan Fan, Yuchen Huang, Shujin Wu, Yi R. Fung"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.802.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 对每一推理步骤进行置信度校准以对齐真实正确性并抑制幻觉滚雪球
tldr: 多模态大模型在多步推理中常只估计整体回答置信度，无法识别逐步骤错误，导致幻觉滚雪球。该文提出MMBoundary框架，结合互补的文本与视觉信息，对推理链中每一步进行置信度校准，从而增强模型对自身知识边界的感知。实验显示逐步置信度校准能较早发现错误推理步骤并显著抑制幻觉累积，对模型判断自身回答置信度和决定是否作答有直接参考价值。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 155, \"height\": 109, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 780, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 916, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1609, \"height\": 1109, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1645, \"height\": 893, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 788, \"height\": 585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long802/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1600, \"height\": 1230, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 958, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 749, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 752, \"height\": 1515, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 667, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 804, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1646, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long802/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 803, \"height\": 364, \"label\": \"Table\"}]"
motivation: 整体响应级置信度校准忽略了推理链中各步骤的正确性，导致幻觉随推理累积。
method: 提出MMBoundary，结合文本与视觉互补信息对每个推理步骤分别进行置信度校准。
result: 实验表明逐步置信度校准可识别错误步骤并显著减少多模态推理中的幻觉雪球。
conclusion: 推理步骤级置信度校准是提升模型知识边界意识和回答可靠性的关键机制。
---

## Abstract
In recent years, multimodal large language models (MLLMs) have made significant progress but continue to face inherent challenges in multimodal reasoning, which requires multi-level (e.g., perception, reasoning) and multi-granular (e.g., multi-step reasoning chain) advanced inferencing. Prior work on estimating model confidence tends to focus on the overall response for training and calibration, but fails to assess confidence in each reasoning step, leading to undesirable hallucination snowballing. In this work, we present MMBoundary, a novel framework that advances the knowledge boundary awareness of MLLMs through reasoning step confidence calibration. To achieve this, we propose to incorporate complementary textual and cross-modal self-rewarding signals to estimate confidence at each step of the MLLM reasoning process. In addition to supervised fine-tuning MLLM on this set of self-rewarding confidence estimation signal for initial confidence expression warm-up, we introduce a reinforcement learning stage with multiple reward functions for further aligning model knowledge and calibrating confidence at each reasoning step, enhancing reasoning chain self-correction. Empirical results show that MMBoundary significantly outperforms existing methods across diverse domain datasets and metrics, achieving an average of 7.5% reduction in multimodal confidence calibration errors and up to 8.3% improvement in task performance.

---

## 论文详细总结（自动生成）

## 论文总结：MMBoundary——通过推理步骤置信度校准提升多模态LLM的知识边界感知

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题背景**：多模态大语言模型（MLLMs）在跨模态推理中往往需要经过多层级（如视觉感知、跨模态推理）和多粒度（如多步推理链）的处理，但其推理可靠性仍存在较大隐患。一个关键问题是**幻觉的“滚雪球”式累积**：错误知识可能先出现在视觉感知阶段，随后在推理链中被不断放大，最终得到错误答案。
- **已有方法局限**：大量已有校准工作仅对模型的**整体回答（entire response）**估计置信度，无法指出推理链中具体哪一步知识出现了偏差/不确定。模型甚至可能给一句本身就建立在错误感知上的回答一个很高的整体置信度。
- **论文回应**：作者提出 MMBoundary 框架，将置信度估计从“响应级”延伸到“推理步骤级”，使模型在生成每一句推理语义时同步说出对该知识的置信度，从而有助于模型实时察觉并抑制低置信度步骤所引发的幻觉雪球，最终**提升模型对自身知识边界的感知**。

### 2. 论文提出的方法论：核心思想、关键技术细节

**总体思路：** 训练 MLLM 在回答时按“句子—置信度语句”交替生成，即输出形式为 `[z1, c1, z2, c2, ..., zT, cT]`，其中 ci 是对第 i 句知识的自然语言置信度表达。整个框架分两个阶段：置信度表达热启动（supervised warm-up）与强化学习校准（RL fine-tuning）。

**两阶段框架的技术细节：**

- **（1）内部置信度估计**：从白盒内部状态出发，融合四类互补信号：
  - 长度归一化对数概率（Length-normalized log probability）
  - 平均 token 熵（Mean token entropy）
  - TokenSAR——聚焦与整句语义相关性更高的 token 的负对数概率加权
  - CLIPScore——加入视觉约束，衡量句子和输入图像的语义匹配度
  - 最终加权为 `U_Final = w0·U_LNLP + w1·U_MTE + w2·U_TokenSAR + w3·U_CLIPScore`
- **（2）置信度分数—自然语言的双向映射**：
  - 将 U_Final 分布划分成 5 个置信度等级，对应“不确定／略微不确定／中等确定／高度确定／完全确定”；
  - 每一级预先构造含 40 条自然语言表达的置信度池（例如 “and this seems trustworthy”“but I’m not sure”等）；
  - 热启动阶段用检测分数向语句池做映射并插入句中构造训练数据；
  - RL 阶段则反向通过 sentence encoder 对生成语句做相似度打分，得到“表述置信度”。
- **（3）阶段一：有监督微调（Warm-Up）**：在带置信度语句的构造数据上，以生成似然损失训练模型，使其学会在推理链中自然地生成置信度表达。
- **（4）阶段二：强化学习（PPO）校准**，引入三种奖励：
  - **知识准确度奖励（R_KA）**：核对生成句子与人工/模型标注的参考推理链是否匹配，保障知识正确性；
  - **期望校准奖励（R_EC）**：衡量表达置信度与对应句子“对错”是否一致，等价于 sentence-level ECE；
  - **置信度自校准奖励（R_CS）**：鼓励外部语言表述与内部估计置信度一致，避免模型口是心非；
  - 总奖励 `R = α·R_KA + β·R_EC + γ·R_CS`，用 PPO 进行策略优化。

### 3. 实验设计：数据集、Benchmark、对比方法

- **数据集/场景**：
  - **A-OKVQA**：通用领域复杂视觉问答，含多跳推理与外部常识知识（域内）；
  - **ScienceVQA**：科学问答数据集（域内）；
  - **CulturalVQA**：不同文化背景下的视觉理解测试，被论文用作**分布外（out-of-distribution）**泛化测试场景。
- **参考推理链标注**：使用 GPT-4o 生成分层次的问答推理链（感知层+推理层），再由 GPT-4o 修正、人工质量检查，以保证有细粒度可评估的知识标签。
- **评价指标**：
  - 置信度校准：ECE、MECE（新增的逐句/多粒度校准指标）、AUROC；
  - 任务性能：最终答案 Accuracy、推理链 F1；
  - 人工评测：Faithful、Concise、Granular 三个维度（1–10分）。
- **对比方法**：DPV、DPS（直接提示 vanilla MLLM）、Self-Consistency(SC)、Multisample、SaySelf、Conf-CSR（自奖励+DPO）、RCE、DRL（不包含本文整体模块而直接 RL）。
- **模型**：主要基座 LLaVA-NEXT 7B，并额外在 Qwen2VL 7B 上复现多个方法以验证跨模型泛化性。

### 4. 资源与算力

- **论文未明确报告 GPU 类型/卡数、总训练时长及显存占用**等典型算力信息。
- 代码公开：https://github.com/Zhitao-He/MMBoundary（但未给出可复现所需的硬件清单）。
- 可间接获知的训练规模与配置：
  - 从 A-OKVQA 与 ScienceVQA 训练集中抽取 19K 对图像-问题，构造 55K 句带置信度表达的监督数据；
  - SFT 阶段：AdamW，学习率 1e-4，10% warm-up，batch size 16；
  - RL 阶段：对每个问题采样 N=3，学习率 1e-5，batch size 16；
  - 推理采样工具使用 vLLM，解码温度 0.1。
  - 由于论文没有提供具体 GPU 数量/时长，后续复现需要自行估计算力开销。

### 5. 实验数量与充分性

总体实验数量较充分、设计系统

- **实验充分性评价**：论文设计了成体系的实验模块，包含主实验、消融实验、跨模型泛化实验、OOD泛化实验、人工评测与案例可视化。具体表现为：
  - 主实验覆盖了置信度校准（ECE/MECE）与任务精度（Accuracy/推理F1）双维度；
  - 对四类内部信号（LNLP、MTE、TokenSAR、CLIPScore）逐一做消融；
  - 对两阶段训练（SFT热启动、RL）以及三类奖励（R_KA、R_EC、R_CS）分别进行了拆解分析；
  - 在 Qwen2VL 上重复关键实验以证明方法不依赖单一基座；
  - 引入 CulturalVQA 作为分布外场景，检验泛化性；
  - 另做了基于 GPT-4o 自动评估与人工评估（Faithful/Concise/Granular）。
  
  整体看，实验设计侧重于“证据链完整性”，但缺少对训练数据规模、推理链标注质量下限等方面的敏感性测试，也较少讨论失败案例的系统性分类。

### 6. 核心实验结果

- **逐句置信度校准收益显著**：
  - MMBoundary 在 A-OKVQA 和 ScienceVQA 上将 sentence-level ECE（MECE）降到 0.07 以下，相比 vanilla LLM（约 0.25–0.30）、SaySelf（约 0.18）等基线降低了 50% 以上；
  - AUROC 也明显提高，说明模型对“该步知识是否可信”的判别能力更强。
- **推理链知识更可靠，最终答案精度不降反升**：
  - 相比强基线 SaySelf 和 DRL，MMBoundary 在两个域内数据集上 Accuracy 提升 1.5–3 个百分点，推理链 F1 亦有提升；
  - 低置信度步骤被抑制后，没有出现“过度保守导致正确答案被过滤”的副作用。
- **OOD 场景仍有竞争力**：
  - 在 CulturalVQA 上，MMBoundary 虽不经该域训练，但 MECE 与 Accuracy 均优于 DRL、SaySelf 的迁移结果；
  - 作者指出这是因内部置信度信号具有跨域通用的能力。
- **人工评测显示表达质量良好**：
  - 在 Faithful（忠实性）维度上得分最高，说明置信度语句与内部状态高度一致；
  - Concise 与 Granular 两个维度说明模型没有过度冗长表达，同时能按句子粒度自然切换。
- **消融实验要点**：
  - 去除 CLIPScore 对视觉相关步骤的校准效果影响最大；
  - 去除 R_CS 后，表述置信度与内部置信度出现失调，导致 MECE 变差；
  - 单纯 RL（DRL 风格）无法获得可靠的分句置信度，说明 SFT 热启动与 RL 校准缺一不可。

### 7. 论文局限性

- **依赖内部状态的标定**：方法要求白盒访问模型 logits 与内部状态，不适用于闭源 API 或仅黑盒使用的 MLLM；论文虽在 Qwen2VL 上验证，但整体适用范围仍是开源模型。
- **参考推理链依赖 GPT-4o 标注**：训练数据中逐句“是否正确”的标签由 GPT-4o 生成并人工抽检，不可避免地引入标注偏差；若标注噪声较大，内部估计器与奖励信号都会受影响。
- **统一置信度池可能带来表达僵化**：虽然用 40 条表达增加了多样性，但从长尾场景看，模型生成的置信度语句仍偏向训练池中的固定句型，泛化到更复杂表达时未必自然。
- **推理链结构预设“先感知后推理”**：将推理过程固定为分层语义链，对于具有循环、回溯或树状结构的推理过程并不适用；该类场景下的置信度表达效果未得到验证。
- **计算成本未透明化**：论文没有报告训练总时长、GPU数量与能耗，仅给出 55K 训练样本和 batch size 等，产业复现门槛不明。
- **评估偏“中短链”**：实验中的问题推理链长度有限，对 MLLM 在更长链（>10 步）上的置信度累积效应依然缺少证据。

### 8. 阅读价值与批判性评价

- **主要贡献**：MMBoundary 将“响应级置信度校准”推进到“逐句知识状态校准”，是首个面向 MLLM 推理链的端到端置信度自述框架之一。其“对话式置信度表达 + 内部信号映射 + RL奖惩”的复合设计，在技术上具有较强创新性与整合性。
- **问题定义上有出色之处**：作者用“知识边界感知”重新包装了校准问题，避免了传统 ECE 那样只对“答案概率”做后验修正的做法；将置信度“说出来”也符合安全人机交互的场景需求。
- **技术上尚可打磨**：四类置信度信号的简单加权虽有消融支撑，但未考虑因果性/冗余性；奖励权重 α、β、γ 的取值依据也缺乏敏感度分析。此外，使用 GPT-4o 做自动评估时，评估者是否能正确感知“步骤级一致性”仍值得存疑。
- **结论上的稳健性中等**：各项提升在统计显著性上未给出数值（如 t-test 或 bootstrap 置信区间）；案例展示时偏选择特征明显样本，尤其对失败案例只字未提，这会削弱方法在极端视觉/跨文化场景上限的证明力。

### 9. 可延伸的研究空间

- 将内部信号法与黑盒 prompt 法融合，设计无需白盒访问的代理置信度信号，扩大应用面；
- 将逐句置信度作为奖励/过滤信号，用于构建“可自我纠错的推理链解码”机制，即当某步置信度低时主动回溯修正；
- 将该框架推广到视频理解、智能体 multi-turn 决策等更长链场景；
- 引入动态置信度表达（由离散 5 级变为连续自然语言程度）并学习每步的“不确定性归因原因”（如视觉遮挡/常识缺失/逻辑歧义）。

### 10. 快速参考卡

- **领域关键词**：多模态大语言模型、置信度校准、推理链、幻觉缓解、知识边界、强化学习、PPO
- **方法名称**：MMBoundary（两阶段：置信度语言化 SFT + PPO 强化校准）
- **关键指标**：MECE（逐句最小期望校准误差）、sentence-level ECE、AUROC、Accuracy、推理链 F1
- **数据集**：A-OKVQA、ScienceVQA（域内）；CulturalVQA（OOD）
- **核心创新点**：将“句子级知识置信度”嵌入生成序列、利用四类内部信号监督外部表达、以三类奖励联合优化。
- **核心限制**：白盒依赖、推理链结构预设、未公开完整训练资源、统计显著性报告缺失。

### 来源

论文标题与作者信息已在前文给出（MMBoundary, 2025）。实验数据与分析仅基于论文原文；未参考原文之外的补充材料或代码运行结果。

（完）
