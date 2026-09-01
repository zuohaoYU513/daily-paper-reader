---
title: "The Illusion of Progress: Re-evaluating Hallucination Detection in LLMs"
title_zh: 进步的幻象：重新评估大语言模型中的幻觉检测
authors: "Denis Janiak, Jakub Binkowski, Albert Sawczyn, Bogdan Gabrys, Ravid Shwartz-Ziv, Tomasz Jan Kajdanowicz"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1761.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 对大模型幻觉检测方法的评测进行再审视，指出ROUGE指标误导
tldr: "现有幻觉检测方法大多用ROUGE等词面重叠指标评测，但这些指标与人类判断不一致。通过大规模人类研究，论文发现ROUGE虽然召回率高但精确率极低，导致检测性能被严重高估：多个已建立方法的性能在改用LLM-as-Judge等人对齐指标后最高下降45.9%。研究还发现响应长度等简单启发式就能匹敌复杂检测方法，提示该领域需要重新设计评测基准。这一结果为幻觉检测研究提供了重要的评测反思。"
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 233, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 723, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1761/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 222, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 827, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 552, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 820, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 824, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 497, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 817, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 815, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 815, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 816, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 820, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1652, \"height\": 826, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 805, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 811, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1652, \"height\": 825, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 781, \"height\": 594, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 817, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1652, \"height\": 825, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 820, \"height\": 605, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 821, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1653, \"height\": 834, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1761/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 821, \"height\": 132, \"label\": \"Table\"}]"
motivation: 现有幻觉检测评测依赖ROUGE，但该指标与人类判断不一致，可能严重高估检测方法的真实表现。
method: 通过多项人类研究，将ROUGE与LLM-as-Judge等人对齐指标对比，并检验长度启发式等简单基线。
result: "发现多种既有检测方法在人类对齐评测下性能最高下降45.9%，简单长度特征即可媲美复杂方法。"
conclusion: 幻觉检测领域需要采用更可靠的人类对齐评测指标，避免被词面重叠的虚假进步误导。
---

## Abstract
Large language models (LLMs) have revolutionized natural language processing, yet their tendency to hallucinate poses serious challenges for reliable deployment. Despite numerous hallucination detection methods, their evaluations often rely on ROUGE, a metric based on lexical overlap that misaligns with human judgments. Through comprehensive human studies, we demonstrate that while ROUGE exhibits high recall, its extremely low precision leads to misleading performance estimates. In fact, several established detection methods show performance drops of up to 45.9% when assessed using human-aligned metrics like LLM-as-Judge. Moreover, our analysis reveals that simple heuristics based on response length can rival complex detection techniques, exposing a fundamental flaw in current evaluation practices. We argue that adopting semantically aware and robust evaluation frameworks is essential to accurately gauge the true performance of hallucination detection methods, ultimately ensuring the trustworthiness of LLM outputs.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景：** 大语言模型（LLM）在实际部署中常出现"幻觉"（即生成流畅但事实错误的内容），无监督幻觉检测方法因此受到广泛关注，试图在无需人工标注的情况下评估模型输出的可信度。
- **核心问题：** 现有大量幻觉检测方法的评估普遍依赖 ROUGE 这一基于词面重叠的指标，而 ROUGE 本质上衡量的是词汇相似度，并不能真正反映事实正确性。论文认为，**这种评测方式与人类判断严重不一致，导致该领域出现"虚假进步"（Illusion of Progress）**——大量看似有效的检测方法，在人类对齐的评测标准下表现大幅缩水。
- **核心发现概述：** 通过大规模人类评估，论文证明 ROUGE 虽然召回率高，但精确率极低；改用与人类判断更一致的 LLM-as-Judge 指标后，多个已建立的检测方法性能下降最高达 45.9%。此外，论文发现简单的"响应长度"启发式方法即可匹敌甚至超越复杂检测技术，根本性地挑战了当前评测实践与检测方法设计的合理性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想：** 首先验证 ROUGE 等词面重叠指标不足以评估幻觉检测的真实性能，然后以经过人类验证的 LLM-as-Judge 作为替代基准，系统性复评现有检测方法，并通过受控实验探索响应长度与幻觉之间的因果关系。
- **人类评估（Human Evaluation）：**
  - 从 Mistral 模型在 NQ-Open 上的回答中随机选取 200 对（问题—答案），刻意确保其中包含 ROUGE 与 LLM-as-Judge 判断冲突的样本；
  - 每份答案由 3 名标注者按照标准化指南判定为"正确/错误/拒绝"，拒绝视为幻觉；
  - 标注者间一致性 Cohen's Kappa = 0.799，确认人类判断可靠。
- **评测指标的对比与选择：**
  - 对比 ROUGE-L（阈值 0.3）与 LLM-as-Judge（以 GPT-4o-Mini 为裁判模型，提示词借鉴 Orgad et al., 2025 的方法）对人类标签的吻合度；
  - 结果：LLM-as-Judge 的 F1 为 0.832、Agreement 0.723，远超 ROUGE 的 0.565 与 0.142，因此论文将其作为后续复评的基准。
- **系统复评现有方法：**
  - 在 ROUGE 和 LLM-as-Judge 两种标签体系下，评估每种检测方法的 AUROC 与 PR-AUC，量化两种评测间的性能差异（∆%）。
- **长度启发式基线：**
  - 提出三种简单基线：单次生成的长度（Len）、多次生成的平均长度（Mean-Len）、多次生成长度的标准差（Std-Len）；
  - 与复杂方法直接对比，展示其竞争性，从而质疑复杂技术的必要性。
- **受控因果实验：**
  - **重复实验（Repetition Experiment）：** 在保持事实内容不变的前提下，反复复制模型输出的句子，观察 ROUGE 评分的 AUROC 变化，证明词面指标可被琐碎操纵；
  - **长度干预实验（Controlled Intervention）：** 用四种不同提示词（Concise、Short、Regular、Verbose）引导模型在保持同一核心内容的前提下生成不同长度的答案，检验长度与幻觉率的关系；
  - **输入扰动实验（Deconstructing Hallucination Triggers）：** 对 TriviaQA（1000 个样本）构造两种扰动——"含糊输入"（将问题改写得更间接、开放性更强）和"干扰上下文"（在问题前添加含正确与误导信息的段落），比较两者对响应长度与幻觉率的影响。
- **附带探索：** 比较 GPT-4.1 与 GPT-4o-Mini 判断的一致性（Cohen's Kappa），发现 TruthfulQA 的一致性较低（0.714），因此将该数据集排除，体现对数据质量的谨慎。

### 3. 实验设计：数据集、基准与对比方法

- **数据集（主实验）：**
  - NQ-Open（3,610 对，真实搜索查询）
  - TriviaQA（3,842 对，知识性问答）
  - SQuAD（4,150 对，较长、较复杂问答）
- **扩展数据集：**
  - HaluEval（包含摘要、对话、QA 三类任务，用于验证长度—幻觉模式是否跨任务泛化）
  - TruthfulQA（初步探索后因标注者间一致性低而排除）
- **模型：**
  - LLaMA 3.1-8B-Instruct
  - Mistral-7B-Instruct-v0.3
  - 均在 zero-shot 和 few-shot（k=5）两种设置下评估。
- **对比的检测方法（基线）：**
  - 基于不确定性的方法：Perplexity、Length-Normalized Entropy（LN-Entropy）、Semantic Entropy（SE）；
  - 基于内部表征一致性的方法：EigenScore、LogDet、Effective Rank（eRank，论文提出的改编指标）。
- **对比的评测指标：**
  - 主评测：ROUGE-L（词面重叠）vs. LLM-as-Judge（语义/人类对齐）；
  - 辅助评测：BLEU、BERTScore、SummaC、UniEval-fact 等常见词面/语义指标与 LLM-as-Judge 标签的一致性。
- **最终评估指标：** AUROC 和 PR-AUC（后者对类别不平衡更稳健）。

### 4. 资源与算力

- **明确说明：** 数据生成使用 Nvidia A40（40GB VRAM）GPU，其余计算在 CPU 上完成。
- **未明确说明：** GPU 数量、训练时长、总计算量（FLOPs）等具体信息论文未公开。
- **说明一点：** 论文方法为纯推理（无参数训练），因此算力需求主要来自多次采样生成（每个 prompt 生成 10 样本）与 LLM-as-Judge 调用。

### 5. 实验数量与充分性

- **实验数量：**
  - 人类评估研究 ×1（200 个样本、3 标注者）；
  - 主实验：2 模型 × 3 数据集 × 2 设置（zero/few-shot） × 6-9 种检测方法 × 2 种评测指标（ROUGE vs. LLM-as-Judge，AUROC+PR-AUC）；
  - 替代评价指标的一致性对比 ×5 种指标；
  - 长度相关性分析（各方法 vs. 长度）；
  - 长度基线（Len/Mean-Len/Std-Len）与复杂方法的全面对比；
  - 重复实验 ×3 数据集 × 3 重复倍数；
  - 长度干预实验（4 种 verbosity 条件）；
  - 输入扰动实验（含糊/干扰上下文 ×1,000 样本）；
  - HaluEval 泛化验证 + GPT-4.1 与 GPT-4o-mini 一致性检验。
- **充分性与客观性评估：**
  - 实验总体规模大、覆盖多维度，设计缜密；以人类共识作为"金标准"对比了多种评测指标，同时对检测方法家族（不确定性、一致性、内部表征）做了系统覆盖；
  - 但存在一定局限：人类评估样本量仅 200 且刻意偏重冲突样本，不能代表自然分布；仅有 2 个开源模型、3 个问答数据集，结论向其他模型与任务的推广性有限；评测者对 LLM-as-Judge 的依赖本身也带有偏差风险。

### 6. 论文的主要结论与发现

- **ROUGE 与人类判断严重错位：** ROUGE 具有高召回（0.957）与极低精确率（0.401、F1=0.565），大量非幻觉内容被误判为错误；LLM-as-Judge 在各项指标上全面胜出（F1=0.832、Agreement=0.723）。
- **现有方法性能被系统性高估：** 改用 LLM-as-Judge 后，零样本下多种方法 AUROC 大幅下降，例如 Mistral 的 Perplexity 下降 45.9%、Eigenscore 下降 30.4%、eRank 下降 36.4%；PR-AUC 下差距进一步拉大。ROUGE 与 LLM-as-Judge 的 AUROC 相关度仅 r=0.55。
- **简单长度启发式即可匹敌复杂方法：** 幻觉响应通常更长、长度方差更大；Mean-Len（平均长度）和 Std-Len（长度标准差）能匹配甚至超过 Eigenscore、LN-Entropy 等复杂方法的 AUROC。
- **更长的回答更容易诱发事实漂移：** 控制内容不变的条件下，要求模型生成更长回答会提高幻觉率（准确率从 0.697 降至 0.604）。
- **输入歧义比干扰上下文更容易诱发幻觉：** 含糊问题大幅增加幻觉率（准确率 0.564 vs. 0.664），并生成更长响应；而干扰上下文即使添加了误导细节，对准确率影响甚微。
- **ROUGE 暴露于简单操纵：** 通过对同一事实内容进行逐句重复，ROUGE 评估的 AUROC 可从 0.85 升至 0.96，说明这类词面指标根本无法抵御表面性的文本改动。
- **领域整体呼吁：** 幻觉检测领域必须转向语义感知、人类对齐且对抗性鲁棒的评测框架，否则"进步"可能只是假象。

### 7. 优点

- **研究视角新颖且高影响力：** 首次系统、大规模地质疑 ROUGE 在 QA 幻觉检测中的适用性，直接揭露领域存在的"虚假进步"现象，具有重要的学术反思价值。
- **以人类判断为锚：** 通过人类评估验证 LLM-as-Judge 的可信度（Kappa=0.799），使得后续复评具备扎实的"金标准"依据，而非简单地以新指标替换旧指标。
- **多维度的实验设计：** 不仅报告了性能下降，还用相关性分析、长度基线对比、受控重复/干预/扰动实验等手段多层次检验"长度—幻觉"关系，兼顾相关性与因果性的探索。
- **简单基线的引入：** 将长度启发式作为下界与复杂方法对照，延续并强化了"简单基线竞争力"的研究传统，对社区有警示意义。
- **诚实的负面报告：** 承认 eRank 在人类对齐指标下效果不佳、TruthfulQA 因低一致性被剔除，展现了客观求真的态度。
- **覆盖广谱评测指标：** 除 ROUGE 外还考察了 BLEU、BERTScore、SummaC、UniEval 等，证明问题并非 ROUGE 独有，增强了批评的普遍性。

### 8. 不足与局限

- **评测覆盖有限：** 仅使用 2 个开源模型（LLaMA 3.1-8B、Mistral-7B）和 3 个短问答数据集，未覆盖商业模型、更大规模模型、长文档/对话等更复杂任务，结论的推广性有待验证；HaluEval 上的验证仅用于长度模式的辅助性分析，并非主实验。
- **人类评估规模偏小且采样非随机：** 200 个样本刻意选取 ROUGE 与 LLM-as-Judge 冲突的区域，可能放大两者差距；标注者为非专业人员、无报酬、来自单一地区（波兰），且未记录人口学信息，标注质量与可复现性受限。
- **LLM-as-Judge 本身有偏差风险：** 论文证明了它比 ROUGE 更接近人类，但没有系统性检验其在所有数据/模型上的稳定性（附录 M 中亦承认 GPT-4o-mini 标注存在偶发错误）。
- **"长度—幻觉"的因果结论仍需谨慎：** 论文的干预实验通过提示词操纵长度，但更长的回答本身可能改变内容复杂度、引入额外信息，无法完全排除混杂因素；论文也在第 6.4 节和附录 N 中承认，长度更多是潜在推理过程的表征而非直接原因。
- **重复实验仅证明 ROUGE 易被操纵，** 但未测试 LLM-as-Judge 或其他语义指标对类似操纵的鲁棒性，缺少对称性验证。
- **未提供可用的新评测工具或新检测方法：** 论文侧重诊断和批判，但并未给出一个更好的、可直接落地的评测框架或检测算法，实践层面的贡献略显不足。
- **计算细节缺失：** 未报告 GPU 数量、推理耗时、API 调用成本等，影响复现与成本评估。

（完）
