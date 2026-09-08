---
title: Language Models can Evaluate Themselves via Probability Discrepancy
title_zh: 语言模型可通过概率差异进行自我评估
authors: "Tingyu Xia, Bowen Yu, Yuan Wu, Yi Chang, Chang Zhou"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.291.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 提出基于原始回答与修订版本概率差异的ProbDiff自我评估标准，让LLM无需外部模型即可自我评价
tldr: 针对大语言模型自我评估常依赖外部奖励模型或GPT-4等评判器的问题，本文提出一种仅利用模型自身概率分布的自我评估指标ProbDiff。该方法发现能给出准确回答的模型概率分布更均匀，通过计算原始生成与其修订版本之间的概率差异即可评估模型表现。实验表明，该指标能较好区分不同语言模型的性能，省去额外评估模型或外部评判器的开销。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl291/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 781, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl291/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 645, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl291/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 649, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl291/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 656, \"height\": 560, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1422, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 579, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1654, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1656, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl291/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1661, \"height\": 311, \"label\": \"Table\"}]"
motivation: 现有LLM自我评估常依赖额外奖励模型或GPT-4等外部评判器，成本高且有偏见。
method: 提出ProbDiff，利用回答准确模型概率分布更均匀的观察，计算原始与修订生成的概率差异作为自评指标。
result: 无需外部模型即可评估不同LLM的表现，与答案正确性显著相关。
conclusion: 概率差异可作为轻量自评估指标，支持大模型的自主能力评估。
---

## Abstract
In this paper, we begin by illustrating that, when presented with a query, Large Language Models (LLMs) capable of providing accurate responses tend to exhibit a more uniform probability distribution compared to their less proficient counterparts. Building upon this observation, we introduce a novel self-assessment criterion termed ProbDiff for evaluating the performance of diverse LLMs. This method eliminates the need for training an additional evaluation model or relying on external proprietary models such as GPT-4 as a judger. Instead, it solely relies on the LLMs under evaluation to compute the probability discrepancy between the original response generation and its revised versions. A higher discrepancy in two LLMs for the same query suggests a relatively weaker ability. We discover that ProbDiff yields comparable results to mainstream GPT-4-based evaluations on various scenarios including NLG tasks like translation and summarization, as well as LLM evaluation benchmarks such as AlignBench, MT-Bench, and AlpacaEval, across LLMs of different sizes.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 大语言模型（LLM）评估是当前的重要挑战。传统自动指标（如 BLEU）依赖表面文本相似度，难以与人类判断对齐；基于训练奖励模型（critique model）的方法存在模型更新滞后、奖励黑客（Reward Hacking）风险以及每次迭代都需要重新训练额外模型的高额成本；基于外部 API（如 GPT-4）的评估又面临成本、数据泄露和条款限制等问题。
- 论文提出一个核心观察：对于同一查询，能力更强的模型在生成回答时通常表现出更均匀、方差更小的对数概率分布；能力较弱的模型则概率分布更陡峭、方差更大。同时，受 DetectGPT 等工作的启发，模型生成样本往往处于对数概率函数的局部极大值附近。
- 基于这一观察，论文提出 **ProbDiff** 方法——一种完全无需额外评价模型、也不依赖 GPT-4 等外部评判器的**自我评估**方法。它利用被测 LLM 自身的概率输出来衡量其回答的置信程度，从而比较不同模型的相对能力强弱。

## 2. 论文提出的方法论

- **核心思想**：更强的模型对给定查询生成的回答概率分布更“平缓”（更均匀），因此对原始回答进行多次修订时，其修订版的概率与原始回答的概率差异较小；相反，弱模型的概率分布“陡峭”，修订版通常显著低于原始回答的概率。因此，原始回答与修订回答之间的对数概率差异（即概率差异）可用来反推模型在特定查询上的能力：差异越大，表示模型在该查询上的表现越差。

- **关键技术细节**：
  - 首先让待测 LLM α 根据查询 q 生成一个回答 x（长度为 T）。计算其平均逐 token 对数概率：
    \[
    \overline{\log p_\alpha}(x|q) = \frac{1}{T} \sum_{t=1}^T \log p_\alpha(x_t|q, x_{<t})
    \]
  - 然后通过一个“Response Refinement Prompt”要求该 LLM 对当前回答进行修订（要求在保持长度和合理性的前提下重写），得到修订版 x₁；并可重复 K 次得到 x_K。
  - 计算概率差异：
    \[
    d(\alpha, q) = \log p_\alpha(x_K|q) - \log p_\alpha(x|q)
    \]
  - 在数据集 D 上取平均得到 \(d(\alpha, D)\)，对两个模型 α 和 θ 比较 \(d\) 值即可判断相对能力：\(d\) 越大，模型能力越弱。
  - 为了输出可解释的“置信度”（confidence），可设定阈值 δ，统计每道题上 \(d(\alpha, q) \ge \delta\) 的比例作为置信度（论文中 δ 取 -0.05）。
  - 前期通过两个预实验验证假设：GPT-4 比 GPT-3.5 在多次问答中回答的相似度和精确匹配率更高；以及概率曲线形状（强模型更平缓）的直观展示。

## 3. 实验设计

- **NLG 任务**：
  - **翻译**：基于 WMT19 数据集，覆盖中文-英文（Zh-En）、捷克语-英文（Cs-En）、德语-英文（De-En）、俄语-英文（Ru-En），每方向 5000 训练对、1000 测试对。
  - **摘要**：使用 XSum 和 CNN/DM 数据集，各取 5000 训练文档、1000 测试文档。
  - **自建“小红书博客写作”任务**：从小红书 App 收集 569 条真实博客，构造指令跟随数据集（469 条微调、100 条评估），用于测试非常规、风格化生成任务。
  - 使用 Qwen-14B-Chat 作为基础模型，分别针对每个任务进行微调（记为 Qwen_ft），然后用 ProbDiff 比较微调前后模型的性能。

- **LLM 评估基准**：
  - **AlignBench**（中文对齐评估，共 683 样本，8 大子类）：使用 GPT-4 生成数据对 Qwen-14B-Chat 进行微调，然后用 ProbDiff 评估微调前后各维度能力。
  - **MT-Bench** 和 **AlpacaEval 2.0**：对这些官方排行榜上的模型（Yi-34B-Chat、Tulu-2-DPO-70B、WizardLM-70B-V1.0 和 Llama2-70B-chat）用 ProbDiff 进行评测。

- **对比方法**：
  - 官方排行榜分数（GPT-4 打分）。
  - 直接采用 GPT-4 作为评判者的两两比较（win rate）。
  - CritiqueLLM（一种可解释的 LLM-as-a-critic 方法）在 AlignBench 上提供的分数。
  - 人工评估（3 位 NLP 方向的博士、专业评分）用于考察冲突率。

## 4. 资源与算力

- 论文中**没有明确提及** GPU 型号、数量、训练时长等具体算力资源信息。
- 仅能推断实验中包含了 Qwen-14B、70B 规模的多个模型以及微调实验（每个翻译对、摘要对 5000 训练样本，AlignBench 上用 GPT-4 生成约 10245 个样本等）。

## 5. 实验数量与充分性

- **实验数量较多**：
  - NLG 任务：4 个翻译方向 ×2（原模型/微调模型）+ 2 个摘要数据集 ×2 + 1 个小红书数据集 ×2，共约 14 个任务组合，均在表格中给出概率置信度。
  - AlignBench 包括 8 个子维度，微调前后两个模型的置信度对比。
  - 官方 leaderboard 评测：MT-Bench + AlpacaEval 上 4 个开源模型，与官方分数比较。
  - 对比 ProbDiff 与 GPT-4 / CritiqueLLM / 人工评估：有 AlignBench 的细粒度对比、图 4 的 win rate 对比、表 6 的冲突程度统计。
  - 附录中包含消融实验：阈值分析（0、-0.05、-0.1）、不同 prompt 的影响、不同温度设置的影响。

- **充分性评估**：
  - 优点是覆盖了多种任务（通用 NLG、中文对齐、多轮指令跟随、英文单轮指令跟随）和多个模型（Qwen、Llama2、Yi、WizardLM、Tulu）。
  - 不足之处在于：部分评价标准与 GPT-4 在个别子任务上存在偏差（如 MT-Bench 上模型排名与官方不完全一致；AlignBench 中写作能力方向不一致），实验主要对“微调前后”模型或排行榜固定模型进行对比，没有与更多元化的考核维度（如代码、数学中的概率分析）充分展开。
  - 总体实验设计有一定层次，但对概率与人类感知之间关系的直接验证仍较初步（附录中的人工评估批次较小，只有 3 人，且未报告大规模统计显著性）。

## 6. 论文的主要结论与发现

- **核心结论**：通过测量 LLM 原始回答与修订回答之间的对数概率差异（ProbDiff），可以在不使用额外评估模型或 GPT-4 的情况下有效比较不同 LLM 的能力。
- 具体发现：
  - 在翻译、摘要、小红书写作等 NLG 任务上，经过任务微调的模型在 ProbDiff 下比未微调模型表现出更高置信度，指示微调带来的性能提升。
  - AlignBench 上：多数子任务（如数学、逻辑、专业能力等）中，ProbDiff 评估的置信度与 GPT-4 给出的分数呈现一致的改进方向。
  - 在多个开源 LLM（Llama2、Yi、WizardLM、Tulu）上，ProbDiff 的模型排序基本与官方测评结果一致（但 MT-Bench 中 Yi 和 Tulu 的顺序与官方略有差异）。
  - ProbDiff 整体上是免费的、不依赖外部模型的评估信号，可用作研究者观察模型改进趋势的辅助手段。

## 7. 优点

- **无需额外模型**：不需要训练专门的 critic/reward 模型，也不依赖 GPT-4 等 API 评判，节省成本、避免数据泄露和外部使用条款限制。
- **通用性强**：可用于任意 LLM（开放词表概率可得），可应用于传统 NLG、中文对齐、多轮对话等广泛的任务场景。
- **与人类/GPT-4评估一致性较好**：大量实验显示 ProbDiff 的方向能匹配 GPT-4 的判断，故可作为一种轻量级的自评估信号。
- **概念新颖**：从“概率分布的几何结构”（平坦/陡峭）出发解释模型能力差异，并将其与自我反思/修订联系起来，拓展了模型自评方式的思路。
- **实现简洁**：仅需模型生成初始回答及修订版，然后计算对数概率差，不涉及复杂训练或推理。

## 8. 不足与局限

- **只能给出相对趋势，无法量化为分数**：如 Limitations 所述，ProbDiff 不能明确指出模型改进的幅度，只能反映变化趋势，因此更适合作为辅助评估工具而非最终精确评分。
- **对句子长度敏感**：原始回答与修改版长度差异较大时，对数概率会产生较大波动，可能干扰评估结果。
- **多轮对话评估存在偏差**：MT-Bench 实验结果中，模型的概率信心排序与官方分数不完全一致，说明该方法在多轮交互或复杂对任务上的有效性仍需改进。
- **依赖策略假设**：方法基于“能力强的模型概率分布更均匀”这一经验假设，但该假设可能与某些生成任务（如创造性写作、长文本）不匹配；概率低并不等于质量差。
- **未给出算力资源和使用细节**：缺少关于 GPU 型号、训练时间的信息，复现成本不透明。
- **阈值 δ 的选取缺乏稳健性**：附录表 7 显示阈值变化（0、-0.05、-0.1）对结果有一定影响，说明该参数需按具体任务调优，否则会降低与 GPT-4 的一致性。
- **修订 prompt 和温度敏感性**：附录数据显示不同修订提示词和修改温度会让置信度发生一定变化，提示方法对实现细节较敏感。
- **人工评估规模较小、冲突率统计简洁**：仅 3 名人工评估者，冲突率虽小，但未展开说明误差界限或更大范围的验证。

（完）
