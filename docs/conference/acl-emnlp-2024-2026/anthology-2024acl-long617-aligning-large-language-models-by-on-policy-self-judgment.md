---
title: Aligning Large Language Models by On-Policy Self-Judgment
title_zh: 通过在线策略自我评判对齐大语言模型
authors: "Sangkyu Lee, Sungdong Kim, Ashkan Yousefpour, Minjoon Seo, Kang Min Yoo, Youngjae Yu"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.617.pdf"
tags: ["query:metacognitio"]
score: 4.0
evidence: SELF-JUDGE使单一模型同时作为策略与评判器，自我评判当前策略生成的回复，属于对自身回答的评估
tldr: 本文针对现有对齐方法需要额外奖励模型进行在线策略学习的局限，提出SELF-JUDGE框架。它通过Judge-augmented监督微调将成对回应选择任务视为指令跟随的特殊情况，训练同一模型既作策略又作评判器。该模型能对当前策略即时生成的回应进行偏好判断，从而实现参数高效且无需独立奖励模型的在线策略对齐。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 769, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1671, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 815, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 548, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long617/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1667, \"height\": 970, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 712, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 817, \"height\": 669, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 812, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 802, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 811, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 780, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 787, \"height\": 723, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 583, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1664, \"height\": 865, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long617/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1665, \"height\": 973, \"label\": \"Table\"}]"
motivation: 现有LLM对齐需额外奖励模型，存在权衡与参数开销。
method: 将成对判断建模为指令跟随任务，通过监督微调训练单一模型承担策略与评判双重角色。
result: 无需独立奖励模型即可进行在线策略对齐，且参数高效。
conclusion: 自我评判可以作为在线策略对齐的有效替代奖励信号。
---

## Abstract
Existing approaches for aligning large language models with human preferences face a trade-off that requires a separate reward model (RM) for on-policy learning. In this paper, we present a novel alignment framework, SELF-JUDGE that (1) does on-policy learning and 2) is parameter efficient, as it does not require an additional RM for evaluating the samples for on-policy learning. To this end, we propose Judge-augmented Supervised Fine-Tuning (JSFT) to train a single model to act as both a policy and a judge. Specifically, we view the pairwise judgment task, choosing the better response from a response pair, as a special case of the instruction-following task. The resulting model can judge preferences of on-the-fly responses from current policy initialized from itself. Experimental results show the efficacy of SELF-JUDGE, outperforming baselines in preference benchmarks. We also show that the rejecting sampling by itself can improve performance further without an additional evaluator.

---

## 论文详细总结（自动生成）

# 论文总结：Aligning Large Language Models by On-Policy Self-Judgment

## 1. 论文的核心问题与整体含义

**研究动机与背景：**

- 现有大语言模型（LLM）对齐方法面临一个重要权衡：基于人类反馈的强化学习（RLHF）虽然能进行**在线策略学习**（on-policy learning），但需要训练一个**额外的奖励模型（Reward Model, RM）** 来评估采样响应，导致训练流程复杂、内存开销大。
- 为规避 RM 的开销，后续研究走向另一极端：
  - **离线学习**（如 DPO、IPO）虽无需 RM，但仅基于静态数据集优化，缺乏探索，易产生次优结果；
  - **离策略学习**（如 RSO、RAFT、ReST）需借助独立评判器构造偏好数据，若不仔细管理经验回放缓冲，可能导致性能退化。
- 核心矛盾：如何在不引入额外参数评估器（RM）的前提下，实现**在线策略上的自我改进**。

**整体含义：**

本文提出的 **SELF-JUDGE** 框架将 LLM 自身同时训练为“策略模型（policy）”和“评判模型（judge）”，使模型能够对**当前策略（itself）** 生成的响应对进行偏好判断，利用判断结果以偏好优化目标（如 DPO）进行**自我在线训练**。该方案在参数高效性（不引入独立 RM）与在线探索优势之间取得了平衡。

## 2. 论文提出的方法论

**核心思想：**

将成对偏好比较任务（从两个响应中选出更好者）视为**指令跟随任务的特例**，并通过一种新的监督微调方式训练单一模型同时兼备响应生成与偏好评判两种能力，从而实现“以自我判断促自我改进”。

**关键技术细节：**

1. **Judge-augmented Supervised Fine-Tuning (JSFT)**：
   - 在普通 SFT 数据（prompt x → 优选响应 y_w）基础上，额外加入判断任务样本。
   - 判断任务被建模为：给定判断模板 C(x, y_w, y_l)，模型需生成对应的判断 token J∈{A, B}，标识更优响应；
   - 判断模板可扩展为**原则感知（principle-aware）** 形式（针对具体原则如 honesty、helpfulness 进行评判），可进一步加入**理由/解释（rationale）** 作为目标序列的一部分；
   - 通过 JSFT 得到的模型称为 **Judge Model (JM)**，具备“既能生成回答、又能成对评判”的双重能力。

2. **基于在线策略判断的自我训练（Self-Training by On-Policy Judgment）**：
   - 将同一个 JSFT 模型同时初始化为当前策略 π_θ 和冻结的参考策略 π_ref；
   - 从当前策略 π_θ 中对每个 prompt 采样两个响应 y_a、y_b；
   - 使用冻结的参考策略 π_ref（作为评判角色）通过判断模板决定两者偏好顺序 (x, ŷ_w, ŷ_l)，形成伪偏好三元组；
   - 利用 DPO（Direct Preference Optimization）等**偏好序优化目标**更新当前策略 π_θ（无需点估计奖励值）：
     
     loss = -E[ log σ( β log(π_θ(ŷ_w|x)/π_ref(ŷ_w|x)) − β log(π_θ(ŷ_l|x)/π_ref(ŷ_l|x)) ) ]
   - 为缓解位置偏差，判断时会同时使用交换 A/B 位置的模板取平均。

3. **基于锦标赛的自我拒绝采样（Self-Rejection by Tournament）**：
   - 推理阶段，从当前策略中采样 N 个响应，构建**锦标赛树**；
   - 用模型自身的判断能力对树中节点的两个子节点响应进行成对比较，逐步决出最终胜者；
   - 只需 O(N) 次前向传播，与带独立 RM 的 Best-of-N 采样成本相同，却无需独立 RM。

## 3. 实验设计

**数据集：**

- **Anthropic-HH（HH-Helpful）**：人类偏好对话数据集，重点关注帮助性原则（为隔离变量、避免与无害性原则的冲突）。
- **UltraFeedback**：AI 反馈数据集（GPT-4 按 4 项原则：helpfulness、honesty、instruction following、truthfulness 评分并附理由）。

**评测基准：**AlpacaEval（GPT-4 对比胜率）、VicunaEval（相对 SFT 模型的胜率）、MT-Bench（多维多轮评分）。

**对比方法（基线）：**

- SFT（无偏好优化）
- DPO（离线偏好优化）
- RSO（离策略、利用 JM 作独立评判器的统计拒绝采样）
- ReST/RAFT（基于 RM 的离策略自我模仿学习方法）
- RLHF（基于 RM 的在线强化学习）

**此外还进行了大量变体分析：**不同训练策略（仅判断任务 vs. JSFT）、不同评估器（RM vs. JM 在 RLHF 中）、不同学习范式（在线 vs. 离线 vs. 离策略）、原则与理由的使用消融、迭代训练效果、参数规模的影响及动态评估器 vs. 静态评估器对比等。

## 4. 资源与算力

文中明确记载的训练资源信息如下：

- 硬件：最多使用 **8 张 NVIDIA A100 80GB VRAM GPU**；
- 最长训练时长：**约 90 小时**；
- 基础模型：Llama-2-7B（主实验）、Llama-2-13B（参数规模分析）；
- 方法上采用了 **LoRA** 低秩适配进行参数高效微调（但 SFT、RM、JM 的初始训练使用全参微调）。

## 5. 实验数量与充分性

- 主实验覆盖两个数据集（HH-Helpful、UltraFeedback）的人类/AI 偏好对齐场景；
- 在 HH-Helpful 上进行了精细的消融分析：JSFT 对判断准确率和策略胜率的作用、不同 JSFT 组合（base、base+online）、JM 作为 RLHF 奖励源的适配性、在线/离线/离策略学习对比；
- 在 UltraFeedback 上进行了原则感知与理由消融、自拒绝采样规模效应（N=1~16）、迭代训练轮次效果等分析；
- 此外还探讨了模型参数规模（7B vs 13B）对 JSFT 的功效影响、用策略模型自身 vs. 冻结参考模型作为判断者的效果差异；
- 总体而言，实验设计**全面且层次清晰**，既验证了框架整体有效性，又剖析了各组件（JSFT、原则、理由、在线策略、锦标赛自拒）的个体贡献。不过主实验集中于 7B 参数规模模型（仅 13B 用于分析），且深度分析主要在 HH-Helpful 上展开，对更大模型和行为安全维度的覆盖有限。

## 6. 论文的主要结论与发现

1. **SELF-JUDGE 是强效且参数高效的对齐方法**：在 HH-Helpful 的 AlpacaEval（44.88% 胜率）、VicunaEval（76.25%）和 MT-Bench（4.80）上全面超过 DPO、RSO、ReST、RAFT 和 RLHF 等基线，且无需任何额外 RM；
2. **JSFT 提升了模型的判断能力**：与仅做判断任务训练相比，JSFT 带来的“模仿学习到判断任务的迁移”显著提升了判断准确率；
3. **对 JM 而言，基于偏好序的在线学习是最佳策略**：JM 的 token 似然不适合作为 RLHF 的点估计奖励（效果低于 RM+RLHF），而使用偏好序目标（如 DPO）并在在线策略环境中训练可获得最佳结果；
4. **在线策略学习优于离线与离策略学习**：在使用同一 JM 的情况下，自训练的 AlpacaEval 胜率：在线 44.88% > 离策略 32.03% > 离线 28.57%；
5. **原则感知 + 理由显著提升评判能力**：加入原则和理由后 JM 的判断测试准确率从 80.5% 提升至 84.0%，且具有更优质的自拒表现——胜率随 N 增大可靠提升、响应更简洁、重复度更低；
6. **迭代训练可弥补原则感知模型初始策略性能的下降**，且一轮自我训练后模型评判能力仍保持，支持多轮持续自我优化。

## 7. 优点

- **思路新颖**：将“判断任务”重构为“指令跟随任务”，让同一模型直接内化评判能力，避免了传统 RM 的额外训练阶段和内存负担；
- **框架简洁、通用**：SELF-JUDGE 的训练可复用于不同偏好数据集，模型经 JSFT 后可集“策略—参考—评判”于一体；
- **有效结合在线学习与参数效率**：同时具备在线策略探索的优势和无需新增参数存储的优点，架构上优于 RLHF 或需独立评判器的方案；
- **多种自我改进路径**：除在线自训练外，在推理阶段利用自锦标赛实现自我拒绝采样，且计算成本与 Best-of-N 相当；
- **分析全面、实践性强**：不仅给出主结果，还细致分析了训练数据构成、判断模板设计（原则/理由）、学习策略差异、迭代可行性、参数规模效应以及评判时位置偏差缓解等工程细节；
- 善于利用生成式评判的灵活性，把多维人类偏好原则结构化地用于判断任务中，同时通过加入理由缓解任务分布偏移带来的策略退化。

## 8. 不足与局限

- **依赖偏好数据集**：JSFT 的训练前提是有高质量的人类偏好数据（如 Anthropic-HH）或强教师模型生成的 AI 反馈数据（如 UltraFeedback）；若完全没有偏好数据集则无法应用，相比 Constitutional AI 等自对齐方法存在应用边界；
- **安全维度未展开**：论文实验未聚焦安全/无害性指标，模型输出在缺少安全防护审查时可能产生不当内容，应用时需要额外安全护栏；
- **模型规模覆盖面有限**：主要实验仅基于 Llama-2-7B，虽附有 13B 扩展观测，但对更大规模模型（如 70B）下方法的可靠性和收益尚待验证；
- **评估指标受评判模型偏差影响**：依赖 GPT-4 或自身作为评估者的结果，可能引入语言风格、长度偏好等偏差。尽管论文通过对比响应长度和重复度侧面说明了自我拒绝对比 LLM 评估者的长度偏好具有鲁棒性，但并未完全消除这一偏差风险；
- **当前自我改进循环的泛化边界尚不明确**：静态（冻结参考模型）与动态（策略自身作评判者）的效果差异仅做了初步观测，迭代轮次增加后是否会长期保持改进趋势或引发奖励攻击（reward hacking）仍需更多实验；
- **理论解释有限**：为何 JSFT 与在线策略判断结合能显著超越基线缺少更深入的理论机制分析，各组件功效的交互解释多为经验性推测。

（完）
