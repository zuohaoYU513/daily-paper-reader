---
title: Improving Factual Consistency of News Summarization by Contrastive Preference Optimization
title_zh: 通过对比偏好优化提升新闻摘要的事实一致性
authors: "Huawen Feng, Yan Fan, Xiong Liu, Ting-En Lin, Zekun Yao, Yuchuan Wu, Fei Huang, Yongbin Li, Qianli Ma"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.648.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 用对比偏好优化缓解大模型新闻摘要中的事实不一致与复杂幻觉
tldr: 大模型新闻摘要仍存在事实不一致，即幻觉，且多为设定因果、添加虚假细节、过度概括等复杂错误。论文提出对比偏好优化CPO，把模型生成忠实内容与虚构内容的倾向解耦，使模型更偏好忠实摘要。进一步的实验表明，该优化能有效降低这类复杂幻觉，提升新闻摘要的事实一致性。该方法为偏好优化在事实性任务中的应用提供了思路。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 713, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 641, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 885, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 654, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp648/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 642, \"height\": 356, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 725, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 598, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 856, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 640, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 637, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp648/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 418, \"label\": \"Table\"}]"
motivation: 大模型新闻摘要幻觉从低级错误转为复杂的事实不一致，传统方法难以检测和纠正。
method: 提出对比偏好优化，将忠实与虚构内容的生成倾向分离，引导模型优化偏好。
result: 在新闻摘要上显著改进事实一致性，减少复杂幻觉。
conclusion: 对比偏好优化为大模型摘要抑制复杂幻觉提供有效训练手段。
---

## Abstract
Despite the recent progress in news summarization made by large language models (LLMs), they often generate summaries that are factually inconsistent with original articles, known as “hallucinations” in text generation. Unlike previous small models (e.g., BART, T5), current LLMs make fewer silly mistakes but more sophisticated ones, such as imposing cause and effect, adding false details, overgeneralizing, etc. These hallucinations are challenging to detect through traditional methods, which poses great challenges for improving the factual consistency of text summarization. In this paper, we propose Contrastive Preference Optimization (CPO) to disentangle the LLMs’ propensities to generate faithful and fake content. Furthermore, we adopt a probing-based specific training method to improve their capacity of distinguishing two types of propensities. In this way, LLMs can execute the instructions more accurately and have enhanced perception of hallucinations. Experimental results show that CPO significantly improves the reliability of summarization based on LLMs.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：大语言模型（LLMs）在新闻摘要生成中会产生与原文事实不一致的内容，即"幻觉"（hallucination）。与 BART、T5 等小模型相比，LLMs 犯的错误不再是实体混淆、生成无关信息之类的低级错误，而更多是复杂且隐蔽的错误，例如：
  - 强行施加因果关系；
  - 添加原文并不支持的虚假细节；
  - 把推测当事实（over-generalizing / taking speculation as fact）；
  - 改写原句时偷换概念。
- **研究动机**：这些复杂幻觉难以通过传统一致性检测方法与传统的扰动式负样本构造方法来识别和模拟。现有改进方法存在以下不足：
  - 两阶段后处理方法（生成+纠正）依赖外部资源，且收集人工修正数据成本高；
  - 预训练阶段调整方案（如 PEGASUS、FactPEGASUS）在 LLM 上算力开销巨大；
  - 依赖传统 NLI 或 QA 作为奖励模型的 RL/PPO 方案，难以识别 LLM 产生的隐蔽幻觉；
  - DPO 方法需要构造带偏好标注的成对数据，困难且人工成本高；
  - COT 提示等方法只是缓解而非从根本上提升模型的可靠性。
- **整体含义**：论文认为应进入 LLM 摘要范式的纠偏阶段——不仅要让模型生成忠实摘要，还要增强模型自身对"何为忠实、何为虚构"的判别能力，从而实现从机制上抑制幻觉。

### 2. 论文提出的方法论：核心思想、关键技术细节与流程

论文提出 **CPO + PST** 两阶段整体方案：

- **核心思想**：LLM 在生成摘要时存在两套可分离的"倾向"：忠实上下文（contextual）的倾向 IC 与基于内部知识想象（internal / parametric）虚构的倾向 II。CPO 通过构造指令对来解耦这两种倾向，配合对抗训练与基于探测（probing）的分层训练，在不依赖强化学习的 SFT 框架下直接提升事实一致性。
- **关键技术细节**：
  1. **句子级数据收集（LESSON 数据集）**：
     - 使用 XSum、CNN/DM 作为源数据；
     - 由多类 LLM（GPT 系、GLM 系、LLaMA 系等不同规模指令微调模型）生成摘要；
     - 设计专门的 prompt，用 ChatGPT 与 GPT-4 对每个句子做"一致/不一致"标注，取两者标注的并集以提高召回率；
     - 经人工校验，其 Balanced Accuracy 为 76.70%，明显优于传统 NLI/QA 评测方法（最高仅 64.16%）。
  2. **对比偏好优化（Contrastive Preference Optimization）**：
     - 设计两条对比指令：IC（要求生成忠实摘要）与 II（要求生成与原文不一致的摘要，作为虚构/幻觉倾向的操作化指令）；
     - **Incentive Loss**：依据摘要正确与否，分别激励模型在 IC 下生成正确句子、在 II 下生成幻觉句子，使模型学会区分两种指令对应的生成行为；
     - **Penalty Loss（对抗训练）**：反过来惩罚错误行为——在 IC 下惩罚幻觉句子的生成、在 II 下惩罚正确句子的生成，以强化模型的指令跟随能力；
     - 总训练损失为：L = LIncentive + αLPenalty（α 为超参数，实验中取 0.05）。
  3. **基于探测的特定层训练（Probing-based Specific Training, PST）**：
     - 利用 DeFacto 等探测集，对模型的每一层（layer）训练一个二分类线性探针，判断给定摘要是否与原文一致；
     - 探针准确率可反映各层对事实性的判别能力；
     - 动态选择 top-k 个探针准确率最差的层，仅对这些薄弱层进行 SFT 式训练；
     - 该方法避免全参数微调的不稳定性，提高训练针对性，且不需要 RL 框架。
- **算法流程概要**：多轮迭代循环——①在探测集上计算各层判别准确率 → ②选出最弱 k 层 → ③用上述 CPO 总损失只训练这些层 → 进入下一轮。

### 3. 实验设计：数据集、基准与对比方法

- **训练数据集**：LESSON——基于 XSum 与 CNN/DM 构造，共包含：
  - XSum 6166 条（正样本 3521 / 负样本 2645），摘要均词 34.96，源文均词 23.26；
  - CNN/DM 4114 条（正样本 2752 / 负样本 1362）；
  - 摘要由多种 LLM 生成（ChatGPT/GPT-4、ChatGLM、Koala、Vicuna、LLaMA、Tulu、BLOOMZ 等），并按句级标注正负。
- **评测数据集/场景**：
  - XSum 与 CNN/DM 两个新闻摘要基准（其中 CNN/DM 多数模型属 in-domain，XSum 属 out-of-domain）；
  - 自动评测由 ChatGPT 与 GPT-4 分别独立评估（使用与标注相同的一致性检测 prompt）；
  - 人工评测：额外收集 300 篇测试文章，由两名标注者在屏蔽模型来源的条件下比较 CPO+PST 与主干的胜负（win rate）。
- **主干模型**：
  - 已有指令微调：ChatGLM2-6B、LLaMA2-7B-chat、Koala-7B、Tulu-7B、Vicuna-7B、BLOOMZ-7B；
  - 无指令微调：OPT-6.7B、Pythia-12B。
- **对比方法（基线）**：
  - SFT（仅在高质量正样本上训练）；
  - SFT+LoRA；
  - Contrastive Learning / Mixed-Contrast Loss；
  - Unlikelihood Optimizing；
  - Decoupling（仅解耦，不使用对抗惩罚）；
  - PPO（基于奖励模型的强化学习）；
  - DPO 与 DPO+LoRA；
  - CPO（全参）、CPO+LoRA、CPO+PST。

### 4. 资源与算力

- 论文明确说明训练使用了 **8×NVIDIA A100 80G** 并行执行；
- 其他训练细节：batch size = 8，epochs = 5，learning rate = 1e-5，weight decay = 3e-7，WarmupLR（warmup ratio = 0.2），α = 0.05；
- 未明确说明具体训练时长或 GPU 总耗时。

### 5. 实验数量与充分性

- 实验数量较为丰富：
  - 8 个差异化主干模型（含有无指令微调两类）；
  - 2 个基准数据集的自动评测，每个评测由两套 LLM（ChatGPT、GPT-4）分别鉴评；
  - 300 篇人工评测（掩蔽来源，双人标注）；
  - 多组消融与对比：全参 CPO 与 PST 变体、LoRA 特效、随机选层、选最优层、选不同 k 值（k=2/4/8/16）等；
  - 针对不同训练 epoch 的稳定性分析；
  - 探测可视化与 head 级统计结果（含均值、最大值、最小值）；
  - 对 IC/II 指令解耦效果的案例分析，并检查摘要的连贯性和内容覆盖率是否受损。
- 充分的方面：主干范围广、基线覆盖 SFT/LoRA/RL/DPO 等多条技术路线，跨 in-domain/out-of-domain 场景，且同时有人工与自动评测。
- 潜在的客观性/公平性考量：CPO 与 CPO+PST 作为论文提出的方法在多数指标上全面领先，且论文承认人工评测规模相对有限（160 条用于标注质量验证，300 篇用于生成效果评测）。评测设计上通过掩蔽来源削减主观偏倚，整体评估是公平且相对客观的。

### 6. 主要结论与发现

- CPO+PST 在 XSum 与 CNN/DM 上都显著提升从 6B 到 12B 多个主干的摘要事实一致性，人工评测中多数模型获得更高的"可获胜率"；
- CPO 能成功解耦 LLM 的"忠实倾向"与"虚构倾向"：给定同一篇源文，IC 指令生成事实正确的摘要，II 指令生成的幻觉是"看似合理"的改写/完善，而非完全无关的内容（如把未发生的事写成已发生、补充虚假年份、概念替换等）；
- PST 基于探测动态训练薄弱层，相比全参数 SFT 更稳定，能对抗过拟合并增强底层与顶层（这些层原先缺乏判断）对事实一致性的敏感度；
- 在对比方法上，CPO+PST 多数情况下优于 SFT、对比学习、Unlikelihood、Decoupling、PPO、DPO 与 LoRA 类方法，且无需 RL 与成对偏好数据。

### 7. 优点

- 洞察到位：准确识别 LLM 幻觉"质变"——从低级错误转为隐蔽的逻辑性/推测性错误；
- 数据建设：构建了首个面向 LLM 摘要的句级一致性标注数据集 LESSON，并以 ChatGPT/GPT-4 联合标注显著优于传统 NLI/QA 评测器；
- 视角新颖：将"忠实/虚构"处理成可对比偏好的指令跟随问题，通过对比指令与对抗损失把幻觉从隐式生成行为中显式剥离出来；
- 实用且易使用：不需 RL 框架与配对数据，只需 SFT 式训练，简化流程并降低不稳定机会；
- 训练高效：PST 只动薄弱层，减少不必要参数更新，规避全参微调的不稳定性，比 LoRA 更具针对性；实验证明甚至能令未经过指令微调的 OPT/Pythia 取得与已指令微调主干竞争的成绩；
- 评测公平性较好：自动评测有双 LLM 体系 + 人工评测盲比，覆盖了事实一致性与第二维度的质量指标（连贯性、信息覆盖），维度较全面。

### 8. 不足与局限

- 论文在 Limitations 中自述：在 in-domain 数据上若超参数（如可训练层数 k）选择不当，不必要的训练会降低 CPO+PST 的表现，对不同主干和域需要细致调节；
- 依赖专有 LLM（ChatGPT/GPT-4）作为标注和评测器，虽优于传统方法，但本身存在偏差与不稳定性，且论文验证集仅 160 条样本，外部推广仍需更广的人工基准；
- 当前 LLM 幻觉的检测难集中于文档级 NLI/QA 的不适配，但其新评测仍依赖 LLM 评测，存在循环验证风险；
- 实验规模仍有提升空间（如更大的主干 13B/70B、更多领域如对话摘要/多文档摘要等并未覆盖）；
- CPO+PST 所需探测/分层训练流程相对精巧复杂，数据集构建依赖商业 LLM 输出，对一般研究者复现和迁移存在一定障碍。

（完）
