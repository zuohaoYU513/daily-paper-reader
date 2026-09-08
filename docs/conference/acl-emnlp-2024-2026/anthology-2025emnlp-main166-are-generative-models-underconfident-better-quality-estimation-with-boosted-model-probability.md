---
title: Are Generative Models Underconfident? Better Quality Estimation with Boosted Model Probability
title_zh: 生成模型是否过于保守？利用提升模型概率改进质量估计
authors: "Tu Anh Dinh, Jan Niehues"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.166.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 指出存在多个合法答案时模型概率会显得偏低，并提出提高概率估计以改进质量评估
tldr: 在没有参考答案的生成推理场景中，质量估计常依赖模型输出概率，但每一步若有多个正确选项会让概率分布分散，导致模型显得不自信，低概率并不必然表示低质量。论文提出BoostedProb方法，在存在多个可行答案时提高模型概率估计，从而获得更准确的质量得分。与简单概率基线相比，该方法在不增加复杂度的情况下显著提升质量估计效果，对置信度估计与任务选择具有实用价值。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1634, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 660, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 678, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 766, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 764, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 765, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 582, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main166/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 752, \"height\": 556, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 781, \"height\": 569, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1604, \"height\": 787, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 823, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 756, \"height\": 569, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 672, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 801, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 797, \"height\": 133, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1568, \"height\": 1457, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main166/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 743, \"height\": 134, \"label\": \"Table\"}]"
motivation: 当输出位置存在多种合法选项时概率分布分散，使得输出概率低估了结果质量，影响无参考答案的质量估计。
method: BoostedProb在生成步骤中识别存在多个合理候选的情况，并相应提升模型概率，以校正概率与质量的失配。
result: 与原始输出概率和质量估计基线相比，BoostedProb在多个任务上取得显著更优的质量估计性能。
conclusion: 通过补偿多候选带来的概率低估，可以低成本获得更好的模型输出品质评估信号。
---

## Abstract
Quality Estimation (QE) is estimating quality of the model output during inference when the ground truth is not available. Deriving output quality from the models’ output probability is the most trivial and low-effort way. However, we show that the output probability of text-generation models can appear underconfident. At each output step, there can be multiple correct options, making the probability distribution spread out more. Thus, lower probability does not necessarily mean lower output quality. Due to this observation, we propose a QE approach called BoostedProb, which boosts the model’s confidence in cases where there are multiple viable output options. With no increase in complexity, BoostedProb is notably better than raw model probability in different settings, achieving on average +0.194 improvement in Pearson correlation to ground-truth quality. It also comes close to or outperforms more costly approaches like supervised or ensemble-based QE in certain settings.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- 论文聚焦于**无参考答案条件下的输出质量估计**，这是许多实际场景中的关键需求。
- 目前最直接、零成本的质量估计方式是从生成模型的输出概率分布中派生分数，前序研究大多指出神经模型概率容易**过度自信**，但本文发现并论证了另一个方向的问题：当输入对应**多个合理的输出选项**（比如翻译中存在多种正确的表达方式）时，概率分布会在多个合理令牌间分散，导致模型概率**显得不够自信**，因此单个令牌的低概率并不一定代表低质量输出。
- 这一发现将一种属于“数据内在不确定性的场景”（比如对话歧义、翻译多译、开放式生成）暴露出来，即模型概率在含有歧义的任务中作为质量估计器具有系统性偏差。
- 基于此，作者提出 BoostedProb，一种在具有多个有效选择时提升模型置信度的方法，用几乎不增加额外成本的方式显著提高了质量估计性能。

## 2. 论文提出的方法论

- 总体思想：当输出令牌是当前输出分布中的**主导令牌（dominant token）**时，不应将该令牌自身的概率作为质量得分，而应使用**主导集群（dominant cluster）的总概率质量**，从而保留所有合理选择带来的信息，削弱多选一造成的“概率低估”。
- 关键步骤分为两个环节：

**(1) 寻找主导令牌——jump-cut 启发式算法：**

- 对一个输出步的概率分布排序后，计算相邻概率之间的差异；
- 若差异同时满足相对阈值 `p(i) − p(i+1) > p(i) × x%` 和绝对阈值 `p(i) − p(i+1) > ϵ` 两个条件，则认为该处是一次显著下降；
- 选择**最靠后的显著下降位置**作为切割点，切割点以上的令牌构成主导集群；
- 该方法比原先用于采样的 top-k、top-p、epsilon-cut 等策略更严格——后者可能将极低概率令牌也纳入主导集合，在 QE 场景下会导致误导性的置信度提升；文中也明确表示该方法可更稳健地区分主导与非主导令牌。

**(2) 输出得分计算：**

- 若最终选中的令牌属于非主导区域，则质量分数为该令牌的原始概率；
- 若最终选中的令牌属于主导集群，则质量分数为该集群中所有令牌概率之和：
  - `BoostedProb(w(i)) = p(i)` 当 `i > c`（非主导）；
  - `BoostedProb(w(i)) = Σ_{j≤c} p(j)` 当 `i ≤ c`（主导）。
- 序列级质量得分是对所有令牌级分数求平均。
- 理论方面，论文在附录中论证：softmax 概率存在上界，该上界受制于输出步中正确令牌的个数 k——每个正确令牌的概率至多为 1/k，这就解释了为何存在多选项时模型会显得不够自信；而 BoostedProb 用集群总概率替代，理论上可使每个正确令牌得到接近 1 的分值，从而化解这一问题。

## 3. 实验设计

- 实验覆盖四类文本生成任务：
  - **语音翻译**：Fleurs 数据集上的 vi-en、de-en、es-en、zh-en 四个语言对，模型为 Whisper Large V3；
  - **文本/机器翻译**：ParaCrawl（超参调优）与 WMT22 General 数据集上的 en-de、zh-en；模型包括 DeltaLM Large、NLLB 3.3B、Tower 7B；还包括基于 Prism 和 NLLB 的参考-free 场景；
  - **摘要**：XSum，模型包括 Bloomz 560M、Llama 3.2 3B、Llama 3.3 70B；
  - **问答**：GSM8k（数学）与 SciEx（大学考试），模型同上。
- 用于评价的“黄金质量”有两种来源：
  - **自动代理指标**：翻译用 XCOMET-XL，摘要/问答用 BARTScore，并补充 ROUGE-L、BERTScore 和 LLM-as-a-Judge 的交叉验证；
  - **人工标注**：WMT22 General 具备句子级人工分数，HJQE 具备词级 OK/BAD 标注。
- 对比基线分三个层次：
  - 概率类：raw model probability、probability entropy；
  - 昂贵无监督法：Monte Carlo sequence entropy、Perturbation-based QE；
  - 监督法：CometKiwi DA，以及 LLM self-judge 基线。
- 额外实验还包括：
  - Prism 评分设置下评估其他翻译系统的输出；
  - HJQE 上的词级 OK/BAD 标注（MCC 指标）；
  - Whisper 不同规模（Tiny→Large）上模型质量与 QE 的关系；
  - 不同主导集群搜索方法的消融对比（top-k、epsilon-cut、eta-cut、top-p、min-p vs. jump-cut）。

## 4. 资源与算力

- 论文只在附录 I 提到所有实验使用 A100 GPU（每卡 40GB 内存），并用 HuggingFace、Fairseq、LM-Polygraph 等工具实现；
- 没有提供 GPU 数量、训练时长、总计算量的明确描述，也未见对推理成本做系统化的能耗或时间统计，因此算力信息较有限。

## 5. 实验数量与充分性

- 实验覆盖了四种任务类型、近十种模型（Whisper 多个版本、DeltaLM、NLLB、Tower、Bloomz、Llama 系列）和多种语言对组合，并使用了多来源黄金标签（自动代理指标与人工标注），整体实验面较广。
- 论文包含两类主要消融：一个是主导集群搜索策略的对比，另一个是不同序列集总方式（均值、中位数、最小值、主导令牌计数）的比较；并讨论了推理随机性（5 个不同随机种子重复实验）。
- 还特别设计了“其他模型的输出用 Prism 打分”和“词级 QE”等间接场景，对实际使用有较大参考价值。
- 公平性方面：
  - 高开销基线的排布大体客观（如 Monte-Carlo 熵、LLM self-judge 在对应表中与 BoostedProb 对照）；
  - 超参数在开发集上完成调优后才用于测试集，且跨语言与模型时多数取同一组超参，这点设计较规范；
  - 但主要集中在“翻译类任务”，因为这类任务的黄金标签最可靠、任务歧义也最高。Summarization 与 QA 易出现所有参考方法得分都极低的情况，一定程度上限制了结论的泛化可比性。

## 6. 论文的主要结论与发现

- 对含歧义的开放式文本生成任务，模型概率分布会自然在多个同样正确的选项之间扩展，从而导致概率低估，出现 Underconfidence——这个现象在语音翻译中常见，而在转录这种近于无歧义的任务中很少见；
- BoostedProb 相比 raw probability 平均提升 +0.194 的 Pearson 相关系数，相比 probability entropy 亦有平均 +0.065 的显著增益；
- 面对概率熵和方法失效的极端案例（如 zh-en 方向、DeltaLM 等），BoostedProb 仍可保持较高相关度，例如 DeltaLM zh-en 上达到 0.688；
- 在 Prism 场景和词级 QE 场景下，该方法能够明显缩小 Prism 概率与监督式 CometKiwi 之间的性能差距；
- 在部分配置下可以超越更昂贵的 Monte-Carlo 序列熵或 LLM self-judge 基线，且不需要多次推理；
- 模型越强时 BoostedProb 越能改善模型的自我评估能力，弱模型也可能被该方法强化原有的过度自信问题。

## 7. 优点

- **方法极简而成本低**：相比需要额外前向推理的 Monte-Carlo 序列熵，以及需要大量训练数据和专门模块的监督式 QE，BoostedProb 只利用模型自身的单次概率分布，改动简单、可复现性强；
- **跨任务通用**：不依赖训练数据，无需手工标签，适用于翻译、摘要、问答等多种任务类型；
- **直觉清晰且有理论支撑**：论文先有具体的翻译样例与统计分析（歧义任务上出现多于 1 个正确令牌）为动机，又以 softmax 的上界分析解释了为何多数正确选项必然伴随概率低；
- **实验范围较丰富**：包含多任务、多模型、纯自动与人工标签、词级与句级评估、辅助不同模型输出的 Prism 场景等；补充材料也较为充分。

## 8. 不足与局限

- **对弱模型有害**：如 Whisper Tiny 这类翻译质量很差的模型，其生成错误时也会呈现明显的主导集群（例如输出“There we have it”的语境），BoostedProb 反而会强化这些错误令牌的置信度，从而削弱 QE 有效性；
- **适用范围受限**：对几乎无歧义的任务（如 ASR、单项选择题式 QA）看不出显著改进，因为主导集群基本只含一个令牌，算法退化为原概率；
- **黄金标签本身有限**：摘要和数学问答中使用的 BARTScore 未必能很好地评估 QE 指标，其对与不对的区分不充分，导致部分配置的所有方法相关度都很低，这是实验设计层面未完全解决的问题；论文通过在附录补充 ROUGE-L、BERTScore、LLM-as-a-judge 的方式做了一定弥补；
- **超参数仍需人工设定**：虽然实验显示固定 x%=30%、epsilon=0.005 已经有很强的鲁棒性，但仍需要启发式调节，对分布差异非常大的输入未必处处最优；
- **缺乏多语言或更多样式的经验证分析**：对总体歧义更高（如对话式、开放域生成）的任务没有覆盖；
- 论文未报告精确的计算量、训练/推理开销对比或 GPU 总时数，在工程落地的成本评估上留下空间。

（完）
