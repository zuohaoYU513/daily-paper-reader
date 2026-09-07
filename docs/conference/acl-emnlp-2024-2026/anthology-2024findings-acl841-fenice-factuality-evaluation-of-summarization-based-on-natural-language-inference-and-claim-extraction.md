---
title: "FENICE: Factuality Evaluation of summarization based on Natural language Inference and Claim Extraction"
title_zh: "FENICE: 基于自然语言推断和主张抽取的摘要事实性评测"
authors: "Alessandro Scirè, Karim Ghonim, Roberto Navigli"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.841.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 基于自然语言推断与主张抽取的摘要事实一致性评测方法
tldr: 针对自动摘要中普遍存在的事实不一致与幻觉问题，现有评测指标缺乏可解释性且聚焦新闻短文本，计算开销大。FENICE 通过将摘要拆分为原子命题并结合自然语言推断判定是否被原文支持，提供可解释且高效的事实性评测。实验表明其与人工判断相关性较好，可用于大模型生成摘要的忠实度评估。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl841/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1542, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl841/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 100, \"height\": 74, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl841/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 2163, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 837, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 841, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 791, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 733, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 674, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 785, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 646, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 766, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 790, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl841/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 430, \"height\": 169, \"label\": \"Table\"}]"
motivation: LLM 生成的摘要普遍存在事实不一致或幻觉，已有评测指标可解释性差、偏重新闻短文本且计算成本高。
method: 提出 FENICE，先抽取摘要中的原子主张，再用自然语言推断模型判断每条主张能否由源文档蕴含，从而得到事实一致性评分。
result: 相比同类指标，FENICE 更可解释且计算可行，在与人工判断的相关性上表现良好。
conclusion: FENICE 提供了一种面向摘要事实性的解释性评测方案，可服务于大模型摘要的忠实度评估。
---

## Abstract
Recent advancements in text summarization, particularly with the advent of Large Language Models (LLMs), have shown remarkable performance. However, a notable challenge persists as a substantial number of automatically-generated summaries exhibit factual inconsistencies, such as hallucinations. In response to this issue, various approaches for the evaluation of consistency for summarization have emerged. Yet, these newly-introduced metrics face several limitations, including lack of interpretability, focus on short document summaries (e.g., news articles), and computational impracticality, especially for LLM-based metrics. To address these shortcomings, we propose Factuality Evaluation of summarization based on Natural language Inference and Claim Extraction (FENICE), a more interpretable and efficient factuality-oriented metric. FENICE leverages an NLI-based alignment between information in the source document and a set of atomic facts, referred to as claims , extracted from the summary. Our metric sets a new state of the art on AGGREFACT, the de-facto benchmark for factuality evaluation. Moreover, we extend our evaluation to a more challenging setting by conducting a human annotation process of long-form summarization. In the hope of fostering research in summarization factuality evaluation, we release the code of our metric and our factuality annotations of long-form summarization at https://github.com/Babelscape/FENICE .

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- 自动文本摘要系统中普遍存在事实不一致问题（如幻觉），即使在 LLM 时代依然严重，制约了真实场景应用。
- 已有事实性评测指标存在多重局限：
  - 可解释性差：只给整体分数，无法定位摘要中哪些部分是事实错误或可被源文档支持；
  - 评测范围窄：主要面向新闻等短文档摘要；
  - 计算成本高：尤其是基于 LLM 的评测方法，依赖闭源大模型，复现性差。
- 论文提出 **FENICE**（Factuality Evaluation of summarization based on Natural language Inference and Claim Extraction），旨在提供一种**更具可解释性、更高效、同时保持高准确性**的摘要事实性评测指标。

## 2. 方法论

- **核心思想**：
  1. 从待评测摘要中抽取一组“原子事实”（简称 **claims**）；
  2. 分别将每个 claim 与源文档的不同粒度文本片段进行基于 NLI 的对齐和蕴含判定；
  3. 对每个 claim 打分，取所有 claim 的平均作为整体一致性分数——这使结果天然具备细粒度可解释性，可指出支撑某 claim 的文档句子/段落，或显示无对应支撑（即幻觉）。
- **关键步骤与公式**：
  - **Claim 抽取**：将抽取视为自回归生成任务，使用 LLM（GPT-3.5-turbo）根据提示词输出 JSON 格式的 claim 列表；同时训练一个 `T5-base` 蒸馏模型（`T5_dist_GPT`）近似 LLM 输出。
  - **NLI 打分**：给定源文档句子 s 和 claim c，定义 `NLIScore(s,c)=P_entailment - P_contradiction`；对 claim c，选择文档所有句子中得分最高者作为对齐句：`FENICE_sent(D,c)=max NLIScore(s,c)`。
  - **共指消解增强**：当 claim 与文档句子中同一实体使用不同表面形式（如“Billy Vunipola”vs“the 24-years-old player”）时，用 FastCoref/F-Coref 找出共指span，并替换到被对齐的句子中重新计算得分，得到 `FENICE_coref`。
  - **多粒度对齐**：为避免单一句子上下文不足，进一步允许 premise 为连续 k 句段落或整个文档，通过 `FENICE_mul` 获取更高得分；最终对每个 claim，若共指增强分数低于阈值 T（实验中 T=0.8）则改用多粒度计算结果，否则保留核心版本；段落长度 j=5。
  - **最终分数**：`FENICE(D,C,j,T)=平均 FENICE_cl`，即所有 claim 分数取均值。

## 3. 实验设计

- **Claim 抽取评估**：
  - 使用 **ROSE** 数据集的“人类标注 claims”作为参考；
  - 与蒸馏 T5 对比 GPT-3.5 的结果；
  - 评价指标：基于 ROUGE-1 或 BERTScore 的 easiness Precision/Recall/F1。

- **摘要事实性评测基准**：
  - 主要使用 **AggreFact**（当前事实性评估的标准 benchmark），含新闻摘要数据集（CNN/DailyMail、XSum）以及三种系统划分：**FTSOTA**（当前最优预训练摘要系统）、**EXFORMER**（早期 Transformer 摘要）、**OLD**（更旧方法）。
  - 在 FTSOTA 分裂上还采用**单阈值设置**，即跨 CNN/XSum 使用统一阈值进行二分类。

- **长文档摘要测评**：
  - 基于 Echoes from Alexandria 资源构建 26 本英文书的故事文本 + 参考摘要，并加入 12 个书籍摘要系统生成的摘要，共形成 **338 个“文本-摘要”对**；
  - 两位专家进行人工二分类标注（factual / non-factual），其中 52 个用于计算 Cohen's kappa（0.74）；
  - 用测试集比较各 metric 与人类标签的一致程度（平衡准确率）。

- **对比方法**：
  - NLI 类：AlignScore、MENLI、SummaC-ZS、SummaC-Conv、DAE；
  - QA 类：QAFactEval；
  - LLM/提示类：ChatGPT-ZS、ChatGPT-CoT、ChatGPT-DA、ChatGPT-Star；
  - 其他：TrueTeacher-11B。

- **消融实验**：
  - `NLI_sent`：以摘要句子为 hypothesis 的句级对齐；
  - `NLI_claim`：改为用抽取出的 claim 作为 hypothesis；
  - `NLI_coref`：加入共指消解增强；
  - `FENICE`：进一步加入多粒度文档对齐；
  - 另测试替换 NLI backbone 为 RoBERTa 的效果。

## 4. 资源与算力

- 论文明确说明：训练蒸馏 claim extractor（T5-base）使用 **单块 NVIDIA GeForce RTX 3090**，共 **1M 步**，优化器 AdaFactor，学习率 1e-5。
- 运行时使用的模型参数规模约 **700M**（DeBERTa-v3-large 系列 NLI 模型 + T5-base 等），属于可复现、可部署的规模。
- 论文**未明确报告**使用 GPT-3.5 API 的调用次数、token 消耗或总预算，也未说明长摘要人工标注的具体费用/时长等财务细节。

## 5. 实验数量与充分性

- 实验覆盖较全面：
  - Claim 抽取：在 ROSE 上比较 LLM 抽取与 T5 蒸馏版本，并在自建蒸馏测试集上验证 T5 对 GPT-3.5 的模仿能力；
  - AggreFact 标准评测：含 CNN/XSum × FTSOTA/EXFORMER/OLD 多组结果；
  - 单阈值评测：评估跨数据集泛化能力；
  - 消融实验验证各组件贡献；
  - 附加 NLI backbone 消融（DeBERTa vs RoBERTa）；
  - 提出并测试长文档摘要人工标注集。
- 充分性评价：
  - 主流 benchmark 都有覆盖，对比方法全面，结果表格也提供了统计信息；
  - 长摘要评估属于较新领域，但样本量相对较小（338 对，且大部分为“非事实”类）；
  - 消融实验充分证明了设计决策的价值；
  - 在 AggreFact 上的结果与现有 SOTA（AlignScore）差距很小且通过多次运行报告了置信区间，整体上实验设计较客观、公平。

## 6. 主要结论与发现

- **FENICE（GPT-3.5 claims 版）在 AggreFact 测试集上取得最高平均平衡准确率（72.7%）**，超过 AlignScore（71.5%）等所有对比方法；蒸馏 T5 版也达到了 70.0%，优于多数基线。
- 在 AggreFact-FTSOTA 单阈值设置中，FENICE_GPT_claims 同样获得最佳平均结果（71.6%），特别在 XSum 这种高抽象性摘要上优势明显。
- 消融结果显示：
  - 将评测单元从句子换成 claims 可提升约 2.9 点；
  - 共指消解增强可再提升 2.7 点；
  - **多粒度文档对齐是最关键的组件，额外贡献 10.1 点**。
- NLI backbone 选择影响明显：DeBERTa 比 RoBERTa 平均高约 4.3 点。
- 蒸馏 T5 claim extractor 在 ROSE 上与 GPT-3.5 水平接近（F1：73.4 vs 74.9；BERTScore F1：94.7 vs 95.0），证明“LLM 只用于蒸馏、推理时不依赖闭源 API”是可行的。
- 在长文档摘要评测上，FENICE 的两种变体（66.2 和 65.7 平衡准确率）都优于 AlignScore（61.3）、MENLI（61.7）和 DAE（51.4），说明其具有扩展到长文档场景的适应性。

## 7. 优点

- **设计新颖**：将可解释的“主张抽取 + 多粒度 NLI 对齐”引入事实性评测，既提高性能又让用户能看到具体支撑证据或定位幻觉。
- **可解释性强**：每个 claim 都有对应的文档片段或者无对应，输出从黑盒分数变成细粒度验证结果。
- **计算高效**：运行时不依赖 GPT-3.5/GPT-4 等大型闭源模型，而是使用约 7 亿参数的模型蒸馏方案，重新部署和复现成本较低。
- **组件可叠加增强**：共指消解、多粒度对齐等设计都被消融实验证明有效，解释清楚。
- **拓展到长文档评测**：为长文摘要人工标注了 338 个实例，展示 metric 在长文本上的优势，弥补既有基准过于偏重新闻短文本的不足。
- **代码与数据开源**：便于领域内后续研究和对比。

## 8. 不足与局限

- 论文自身指出：系统由 NLI、共指消解、claim extractor 等多个组件组成，任一组件的误差都会影响最终结果，增加整体复杂性。
- 所有组件和评测均面向**英文**，多语言场景未做验证。
- 可解释性虽然增强，但**缺乏量化评估方法**来衡量解释质量，用户仍需自行查看对齐内容。
- 长文档摘要评测的规模有限（338 对、26 本故事），且标注类别明显不平衡（事实类 66、非事实类 273），可能对泛化性和稳定性产生一定影响。
- 对 LLM 的依赖并未完全消除：蒸馏数据来自 GPT-3.5，其输出质量会间接影响最终的 claim 抽取效果，论文也未报告 API 成本或随机性的详细影响。
- 在 AggreFact 上实验使用验证集调阈值；虽然在单阈值设置上做了额外验证，但跨领域/跨分布的迁移能力仍有待更多探索。
- 总体而言，实验充分性和公平性较好，但长文档场景的标注标准“由原文明确或隐含包含”本身可能因文本过长而带有主观性。

（完）
