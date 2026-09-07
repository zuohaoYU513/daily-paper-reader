---
title: Fact-Checking the Output of Large Language Models via Token-Level Uncertainty Quantification
title_zh: 基于词元级不确定性量化的大语言模型输出事实核查
authors: "Ekaterina Fadeeva, Aleksandr Rubashevskii, Artem Shelmanov, Sergey Petrakov, Haonan Li, Hamdy Mubarak, Evgenii Tsymbalov, Gleb Kuzmin, Alexander Panchenko, Timothy Baldwin, Preslav Nakov, Maxim Panov"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.558.pdf"
tags: ["query:faithfulness"]
score: 6.0
evidence: 利用token级不确定性量化进行事实验证与幻觉检测，定位生成内容中不可靠片段
tldr: 大模型输出中偶尔的事实错误常被成段正确文本掩盖，用户难以发现。本文提出一种基于token级不确定性量化的幻觉检测流程，通过模型输出概率或隐层特征计算不确定性分数，定位不可靠生成。实验结果显示该方法能有效区分虚假内容，为缺乏外部知识源的场景提供了自动事实核查手段。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1565, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1498, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1662, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1626, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1659, \"height\": 807, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 807, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 810, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl558/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 770, \"height\": 498, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1263, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1257, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 718, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 615, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 642, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 714, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1655, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 594, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1141, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 633, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl558/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 626, \"height\": 210, \"label\": \"Table\"}]"
motivation: 大模型输出真假混杂难以人工识别，现有服务缺少自动检测不可靠片段的手段。
method: 利用token级不确定性量化，从模型输出或隐层特征计算分数以构建事实验证检测流程。
result: 实验表明不确定性分数能可靠识别不可靠生成，实现自动事实核查。
conclusion: 模型自身不确定性可作为无需外部知识的幻觉信号，为大模型输出核验提供轻量方法。
---

## Abstract
Large language models (LLMs) are notorious for hallucinating, i.e., producing erroneous claims in their output. Such hallucinations can be dangerous, as occasional factual inaccuracies in the generated text might be obscured by the rest of the output being generally factually correct, making it extremely hard for the users to spot them. Current services that leverage LLMs usually do not provide any means for detecting unreliable generations. Here, we aim to bridge this gap. In particular, we propose a novel fact-checking and hallucination detection pipeline based on token-level uncertainty quantification. Uncertainty scores leverage information encapsulated in the output of a neural network or its layers to detect unreliable predictions, and we show that they can be used to fact-check the atomic claims in the LLM output. Moreover, we present a novel token-level uncertainty quantification method that removes the impact of uncertainty about what claim to generate on the current step and what surface form to use. Our method Claim Conditioned Probability (CCP) measures only the uncertainty of a particular claim value expressed by the model. Experiments on the task of biography generation demonstrate strong improvements for CCP compared to the baselines for seven different LLMs and four languages. Human evaluation reveals that the fact-checking pipeline based on uncertainty quantification is competitive with a fact-checking tool that leverages external knowledge.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

### 研究动机与背景
- **大语言模型幻觉问题的严重性**：LLM 在生成文本时常产生“幻觉”（hallucination），即包含事实性错误的输出。这类幻觉具有高度隐蔽性——偶发的事实错误很容易被大段正确文本掩盖，用户极难识别，可能造成误导性信息传播。
- **现有服务的不足**：当前基于 LLM 的服务通常**不提供**任何检测不可靠生成内容的手段，用户缺乏自动预警机制。
- **现有事实核查方法的局限**：传统事实核查通常依赖外部知识库和复杂系统，存在知识源不完整、存储开销大、计算成本高等问题。
- **核心论点**：关于生成内容是否为幻觉的信息本身就蕴含在模型输出中，可以通过**不确定性量化（UQ）** 提取，从而无需外部资源即可进行事实核查。

### 研究目标
- 提出一种基于**词元级（token-level）不确定性量化**的幻觉检测与事实核查流水线，用于定位并高亮 LLM 输出中的不可靠片段，实现“白盒”模式下的轻量级自动核查。

## 2. 论文提出的方法论

### 2.1 整体事实核查流水线
论文提出一个四阶段流水线：
1. **文本拆分**：将生成文本分解为原子声明（atomic claims），例如使用 GPT-4 完成。
2. **词元匹配**：将每个原子声明中的词映射回原始文本，以获取对应位置的概率分布。
3. **不确定性计算**：计算词元级不确定性分数，聚合为声明级不确定性分数。
4. **阈值判定与高亮**：通过与验证集上的阈值比较，将被判定为不可靠的声明标记出来；若某个词元同时属于可靠与不可靠声明，则不做标记。

### 2.2 核心方法：Claim-Conditioned Probability（CCP）

**理论动机——区分三类不确定性：**
- **声明类型/顺序不确定性（Claim type/order uncertainty）**：模型在当前步骤犹豫要生成哪类信息（如毕业年份还是专业方向）。此不确定性不影响事实性，应忽略。
- **表面形式不确定性（Surface form uncertainty）**：模型在同义词/上下位词之间犹豫（如"art" vs."painting"）。此不确定性反映风格变化而非事实差异，也应忽略。
- **声明值不确定性（Claim uncertainty）**：模型对某一具体信息取值不确定（如专业方向究竟是"painting"还是"acting"）。这种不确定性直接与事实错误相关，是唯一的关注目标。

**CCP 的定义公式**：
\[
CCP(x_j) = \frac{\sum_{x_j^k \in \mathcal{M}(x_j)} P(x_j^k \mid x_{<j})}{\sum_{x_j^l \in \mathcal{CT}(x_j)} P(x_j^l \mid x_{<j})}
\]
其中分子为与原始预测**蕴涵**（同义）的词候选概率之和，分母为与原始预测**属于同一声明类型**（蕴涵或矛盾）的词候选概率之和。

**实现细节（基于 NLI）**：
- 使用 **beam search（K=10）** 获取当前位置词的 Top-K 替代候选（GPT-3.5/GPT-4 因 API 限制仅取 5 个）。
- 每个候选替换原词后形成新文本，用 **NLI（自然语言推理）模型**判断新文本与原文本的关系：
  - **entail（蕴涵）** → 候选与原词含义相同，同义且同声明类型；
  - **contradict（矛盾）** → 候选与原词含义不同，但属于同一声明类型；
  - **neutral（中性）** → 候选不属于同一声明类型。
- 功能词（从 NLTK 停用词表判定）的 CCP 值直接设为 1。
- 声明级 CCP 分数取声明内所有词 CCP 值的乘积：\( CCP_{claim}(C) = 1 - \prod_{j \in C} CCP_{word}(x_j) \)。

### 2.3 对比基线方法
- **Maximum Probability**：基于最大概率词的不确定性。
- **Perplexity**：基于词元平均负对数概率。
- **Token Entropy（最大值聚合）**：取声明中最大词元熵。
- **P(True)**：让 LLM 自行判断声明真假，利用首词为"True"的概率（需两次模型推理）。

## 3. 实验设计

### 3.1 任务与基准（Benchmark）
- **任务场景**：人物传记生成。向 LLM 询问 100 位（GPT-4 列举的 1900 年以来）名人的传记。
- **自动标注基准 FactScore**：英文实验中将每个原子声明用 FactScore（retrieval + ChatGPT + Wikipedia）标注为 supported / not supported。
- **人工标注**：对英文、中文、阿拉伯语、俄语的子集进行双人标注，仅当两名标注者均判为"supported"时才算正确，用于评估自动标注质量和 UQ 方法表现。

### 3.2 模型与语言覆盖
| 语言 | 模型 |
|------|------|
| 英文 | Vicuna 13b、Mistral 7b、Jais 13b、GPT-3.5-turbo |
| 中文 | Yi 6b |
| 阿拉伯语 | Jais 13b、GPT-4 |
| 俄语 | Vikhr-instruct-0.2 7b |

### 3.3 对比方法与评价指标
- **对比方法**：CCP vs. Maximum Probability、Perplexity、Token Entropy、P(True)；另与 FactScore 本身对比。
- **评价指标**：ROC-AUC 与 PR-AUC（以 not supported 为正类）。
- **NLI 模型**：默认使用 microsoft/deberta-large-mnli（350M 参数）。

### 3.4 数据集规模
- 英文自动标注：Mistral 7b 3,824 条声明、Vicuna 13b 3,617 条、Jais 13b 1,407 条、GPT-3.5-turbo 3,875 条。
- 人工标注：英文 100 条（Vicuna）、中文 1,603 条（Yi）、阿拉伯语 186 条（Jais）+ 200 条（GPT-4）、俄语 146 条（Vikhr）。

## 4. 资源与算力

论文在 **Appendix F** 中有明确的算力说明：
- 单次完整实验（数据生成 + UQ 方法评估）约需 **12 天 Nvidia A100 GPU** 计算时间。
- OpenAI API 费用：用于声明拆分和匹配，所有英文模型合计 **$40**；GPT-3.5-turbo 生成英文传记费用 **$13**。
- 运行时对比实验（Mistral 7b + 100 篇传记，两张 32GB V100 GPU）：Maximum Probability 耗时 18.5±0.8 秒；CCP（350M NLI 模型）20.1±0.9 秒；CCP（22M NLI 模型）仅 19.1±0.8 秒（较 MP 仅增加 3% 开销）。

## 5. 实验数量与充分性

### 实验组数量
1. **英文 FactScore 标注实验**：4 个 LLM，报告 ROC-AUC 和 PR-AUC。
2. **按句子位置分桶评估**：分析只考虑前 2 句、前 5 句和全部句子时的性能变化。
3. **多语言人工标注实验**：中文（Yi 6b）、阿拉伯语（Jais 13b、GPT-4）、俄语（Vikhr 7b）以及英文（Vicuna 13b 人工标注子集）。
4. **与 FactScore 的对比实验**：在 Vicuna 13b 人工标注上对比不同 UQ 方法与 FactScore。
5. **五项消融研究**：
   - 词级 CCP 的聚合方式（乘积 vs. 归一化乘积 vs. 最小值 vs. 平均值）；
   - NLI 模型大小与类型（7 种不同 NLI 模型，22M~350M 参数）；
   - NLI 输入上下文（无上下文 vs. 句子前缀 vs. 声明前缀）；
   - 功能词处理方式（忽略 vs. 设为 1）；
   - Top-K 候选数量 K 的影响（K=2~10）。
6. **定性分析**：多组可视化案例比较。

### 实验充分性评估
- **优点**：覆盖 7 个 LLM、4 种语言，基线方法多样（5 类），既有人工标注也有自动标注交叉验证，消融研究较为系统全面，实验中还加入了对标注工具（FactScore）自身误差的分析。
- **不足**：任务类型单一（仅传记生成），未覆盖问答、摘要、翻译等更广泛的生成任务；未测试更大规模的商用模型（除 GPT 系列 API 外）；人工标注规模较小（除中文外仅 100-200 条），统计功效受限。

## 6. 主要结论与发现

- **CCP 方法显著优于基线**：在英文 FactScore 标注下，CCP 在所有 4 个 LLM 上的 ROC-AUC 均领先；以 Jais 13b 提升最大（较最接近基线高 0.07 ROC-AUC / 0.09 PR-AUC）。唯一的例外是 PR-AUC 指标下 GPT-3.5-turbo 上 P(True) 更高，归因于 OpenAI API 仅能获取 5 个 token 候选，限制了 CCP 的性能。
- **多语言场景同样领先**：在中文 Yi 6b 上 CCP 比最强基线高 0.01-0.12 ROC-AUC；阿拉伯语 Jais 13b 高 0.05；俄语 Vikhr 高 0.05；英文人工标注 Vicuna 上高 0.09~0.11。
- **UQ 可媲美甚至超越外部事实核查工具**：基于 CCP 的流水线在 Vicuna 13b 人工标注上的 ROC-AUC（0.78）甚至超过 FactScore 自身（0.72），且无需任何外部知识源。
- **生成早期可靠性高于后期**：模型前面句子产生的声明正确率更高，越往后越容易产生错误信息；所有 UQ 方法在仅用前 2 句时表现最好。
- **CCP 的计算开销可忽略**：最小 NLI 模型下仅比最简基线慢 3%，适合实际部署。
- **影响 CCP 性能的关键因素**：声明前缀作为 NLI 上下文最重要；功能词置 1 带来 0.03 的提升；K=8 后性能趋于饱和。

## 7. 优点

- **方法创新性强**：CCP 是首个系统性地将声明生成中的不确定性分解为“声明类型/顺序”、“表面形式”和“声明值”三类，并显式排除前两类噪声的方法，学术框架清晰、理论动机充分。
- **实用价值突出**：仅需白盒模型内部信息即可完成事实核查，免除了外部知识库的存储和检索成本，计算开销极低（可低至推理时间的 3%）。
- **实验设计较严谨**：采用 FactScore 自动标注与人工标注双重验证；对自动标注工具进行了错误分析（如表 8 所示）增强了结论可信度；多语言/多模型覆盖增强了结论的普适性。
- **代码开源，可复现性好**：方法已集成到 LM-Polygraph 库中，代码和数据公开。
- **消融研究非常详尽**：对方法各个组件的影响（聚合方式、NLI 模型、上下文、功能词、K 值）进行了逐一分析提供了很好的工程参考。

## 8. 不足与局限

### 方法层面
- **依赖 NLI 模型质量**：CCP 的核心依赖于文本蕴涵分类器，但该模型为通用任务预训练，在特定领域/体裁上的可靠性有待进一步验证。
- **功能词处理较粗糙**：依赖 NLTK 停用词表来判定功能词（适用于英文），对其他语言可能不准确/不适用。
- **白盒限制**：方法需要访问 token 概率分布，无法直接应用于闭源模型（如仅通过 API 使用且不暴露 logits 的场景）。GPT-3.5/GPT-4 的 API 限制（5 个候选）也削弱了 CCP 效果。
- **外部依赖**：声明拆分和匹配环节使用 OpenAI GPT 模型，在真实应用中可能带来额外成本和不可控性。
- **文本粒度问题**：以词元为基本分析单位，语言学上可能不如以短语为单位合理。

### 实验与评估层面
- **任务单一**：仅在传记生成任务上验证，未涉及问答、摘要、翻译等更常见的幻觉场景。
- **人工标注规模有限**：除中文外，人工标注仅 100-200 条声明，可能不足以得出统计上稳健的结论。
- **校准问题未讨论**：CCP 分数的概率校准（calibration）未做分析与后处理，会影响阈值设置的可靠性。
- **无法检测超出模型知识范围的内容**：对超出模型时间截止点或模型基于错误训练数据产生的“自信幻觉”无能为力。

### 应用与伦理层面
- **缺乏幻觉自动修正能力**：方法仅能高亮可疑内容，无法在去除幻觉片段的同時保证文本连贯性。
- **误用风险**：该方法可能被用于不公平的内容审核，论文作者也对此提出警示。

（完）
