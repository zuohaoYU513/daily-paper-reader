---
title: Enhancing Factuality through Consensus and Consistency in Summarization Using Minimum Bayes Risk Decoding
title_zh: 利用最小贝叶斯风险解码的共识与一致性增强摘要事实性
authors: "Riza Setiawan Soetedjo, Yusuke Sakai, Hidetaka Kamigaito, Jingun Kwon, Manabu Okumura, Taro Watanabe"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2071.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 结合最小贝叶斯风险共识与事实性指标重排候选摘要以提升事实性
tldr: 自动生成的摘要仍面临事实性不足的问题，仅以源文档为指导重排候选结果并不可靠。本文提出 ConSUM，在重排时同时考虑候选摘要与源文档的一致性以及候选集合之间的多数一致性，利用最小贝叶斯风险解码建立共识。实验证明该方法相比只用源文档的重排更有效地提升了摘要事实性。这为摘要生成中的候选选择提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 725, \"height\": 919, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 654, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 1001, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 1116, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 739, \"height\": 992, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1651, \"height\": 1079, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2071/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 784, \"height\": 599, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 922, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 932, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 732, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1443, \"height\": 911, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1651, \"height\": 983, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 630, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 714, \"height\": 909, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 595, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1654, \"height\": 1443, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1654, \"height\": 1463, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1650, \"height\": 2346, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1651, \"height\": 2304, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1650, \"height\": 855, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2071/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1650, \"height\": 841, \"label\": \"Table\"}]"
motivation: 摘要重排仅依赖源文档作为指导，难以选出事实性足够高的候选，需要同时利用多个候选中反映的共识信息。
method: 提出 ConSUM，基于 MBR 解码在生成的候选中建立一致性共识，并用事实性感知指标比对源文档，对候选摘要进行重排。
result: 实验显示该方法能显著提升摘要事实性，优于仅以源文档为引导的重排方法。
conclusion: 共识与源一致性结合的重排策略是大模型摘要事实性提升的有效手段。
---

## Abstract
Improving the quality of model-generated summaries, especially factuality, the accuracy of a summary with respect to its source content, remains a challenge. While reranking could select the optimal output from multiple generated candidates, it is limited to only using the source as guidance, resulting in unreliable summaries. To address this limitation, we propose ConSUM that reranks candidate summaries by considering two factors: consistency to the source document and consensus among the other candidates. Consensus is established using Minimum Bayes Risk (MBR) decoding over the set of generated summaries, while ensuring consistency by employing factuality-aware metrics that compare the summary against the source. Rigorous testing demonstrates that our system is competitive with existing methods, with human evaluations further confirming that its generated summaries are preferred over those from other systems.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

文档摘要生成的核心目标之一，是确保生成的摘要在事实层面与源文档保持一致，即“事实性”（factuality）。然而，即便在预训练语言模型（PLM）和大型语言模型（LLM）取得显著进展的背景下，模型生成的摘要仍不可避免地出现幻觉（hallucination），即摘要中包含源文档中不存在、甚至相矛盾的事实信息。

现有提升摘要事实性的方法，尤其是**候选摘要重排（reranking）**策略，通常依赖唯一信号——源文档——作为“无参考”（reference-free）评估的基准。即：通过某种无参考的事实性指标（如 FENICE、FIZZ），从多个候选摘要中选出与源文档一致性最高的那一个。这种范式存在以下局限：

- **过度依赖源文档**：无参考指标的打分粒度有限，往往无法捕捉具体的事实性错误（例如图 1 所展示的案例），无法细粒度地惩罚生成错误。
- **无法使用高质量参考摘要**：依赖基于参考（reference-based）的指标需要人工撰写的“Gold”摘要，获取成本极高，且学界已证明这些数据集中所谓金标摘要质量本身不高（Zhang et al., 2024）。
- **指标偏见**：仅优化某一个单一的无参考指标，容易导致该次优（overfitting）指标固有的偏见被放大。

针对上述问题，论文提出了 **ConSUM（Consistency and Consensus in Summarization）**——一种新颖的、结合“共识”与“一致性”的重排方法。其核心假设是：**最佳的摘要不仅要忠实于源文档（源一致性），还应当最能代表模型自身输出分布的多数共识**。ConSUM 利用最小贝叶斯风险（Minimum Bayes Risk, MBR）解码，以模型自身采样生成的伪参考摘要集为代理基准，捕捉模型分布上的共识信息；同时利用事实性感知的无参考指标衡量候选与源文档的一致性。

---

## 2. 方法论

ConSUM 由三个步骤组成：

### 2.1 生成候选摘要与伪参考
从同一个源文档出发，论文生成两种集合：
- 候选摘要集 `Y = {y1, ..., y|Y|}`：作为潜在输出集（“参赛者”）。
- 伪参考摘要集 `R = {r1, ..., r|R|}`：作为模型真实概率分布的代理“参考答案”。

模型使用**不同的解码策略**分别采样这两个集合（`θ_cand` 与 `θ_ref`），将二者解耦是为防止“自我强化偏见”（self-bias）。

### 2.2 打分：一致性评分与共识评分
每个候选摘要 `y_i` 被两个独立的信号评分：

**① 源一致性评分（Ssis）**
\[
S_{\text{sis}}(y_i, s) = F_M(y_i, s)
\]
其中 `F_M` 是无参考的事实性指标。论文选择 FENICE 和 FIZZ 作为背骨指标——二者都属于“声明抽取 → NLI 蕴含校验”的两阶段式事实性度量。

**② 共识性评分（Ssen，基于 MBR 解码）**
\[
S_{\text{sen}}(y_i, R) = \frac{1}{|R|}\sum_{j=1}^{|R|} u(y_i, r_j)
\]
其中效用函数 `u` 在论文中固定为 **MENLI**（一个 SOTA 的 NLI 基础摘要评估指标）。也就是说：收益是衡量候选摘要与 64 条伪参考在 NLI 事实蕴含维度上的平均匹配度。

### 2.3 归一化与重排
计算公式为：
\[
S_{\text{final}}(y_i) = w \cdot \text{Z-score}(S_{\text{sen}}) + (1-w) \cdot \text{Z-score}(S_{\text{sis}})
\]
并用 z-score 归一化统一量纲，`w`（权重，超参数）作为共识性与一致性之间的平衡系数。最终选择使 `S_final` 最大的候选摘要输出。

### 2.4 核心区别
- 区别于传统重排（只用源文档）；  
- 区别于仅把 MBR 与 BERTScore/ROUGE 等词面语义工具结合的方法；  
- 引入 MENLI 强化**事实共识**，而非词面共识。

---

## 3. 实验设计

### 3.1 数据集
- **CNN/DailyMail（CNN/DM）**：以抽取式摘要为主（摘要句子多直接取自原文）。
- **XSum**：以高度抽象式、单句摘要著称，幻觉频率高（Maynez et al., 2020）。
两个数据集均以英文新闻为主。

### 3.2 基座模型
- **PLMs**：BART-Large、PEGASUS 和自行微调的 T5-Large（微调配置见下）。
- **LLM**：Llama-3-8B-Instruct。

### 3.3 解码策略
- **Epsilon Sampling**（PLM）。
- **Diverse Beam Search（DBS）**：衍生出三种配置：beam-sim（沿用 Liu & Liu 2021 设定）、beam-div、beam-dbl。
- **Nucleus Sampling**（LLM）。
共计 5 组设置。

### 3.4 评估指标
- **质量组（参考基）**：ROUGE-1/2/L、BERTScore、MoverScore。
- **事实性组（参考基）**：MENLI（entailment、contradiction、summarization 三个子分数）。
- **事实性组（无参考）**：UniEval、FENICE、FIZZ。
- **基线对比系统**：Baseline（无重排）、FENICE-0.0（仅 FENICE）、FIZZ-0.0（仅 FIZZ）、SimCLS（监督重排模型）。

### 3.5 Hyperparameter 与消融设置
- 候选摘要数：16；伪参考数：64。
- 默认权重 w：0.75（即共识性 : 一致性 = 75 : 25）。
- 为确认权重影响，对不同 w 值 {0.0, 0.25, 0.5, 0.75, 1.0} 进行了大规模消融。

---

## 4. 资源与算力
论文中提供的算力/资源信息与 T5 模型微调有关，此前提到了一共 4 块 RTX A6000 GPUs、训练 5 epochs，但这些表述有歧义，需要特别注意。**更核心的算力问题，如 MBR 解码的计算负载（O(n²)）在实验中如何分配、重排过程中使用了多少 GPU 总量、推理耗时是多少，正文均未明确说明**。论文只在 Limitations 一节承认：MBR 采用 O(n²) 计算，候选或伪参考增多时资源消耗随平方级上升；FENICE 和 FIZZ 在大规模处理时存在计算负担，限制了对它们的深度参数探索。

---

## 5. 实验数量与充分性

### 5.1 实验规模
实验覆盖面较为丰富：
- **2 个数据集（CNN/DM、XSum）**；
- **5 种候选采样配置 × 4 个模型（T5-Large 因部分策略结果异常，单独分析）**；
- **多种重排配置（MBR-1.0、FENICE-0.75、FIZZ-0.75、FENICE-0.0、FIZZ-0.0）**；
- 从验证集上开展了 3 组初步研究：① 候选数量（1→64）；② 伪参考数量与策略（对比“自我参考”）；③ 权重 w 敏感性；
- 测试集上给出全 12 项指标的详细对比；
- **带显著性检验**：paired-bootstrap 重采样（10,000 次），显著水平 p < 0.05，并经 Bonferroni 校正；
- **引入了 Oracle 上限**（在候选池内挑真最优）作为理论上界参照；
- 最终附加了 **人工标注评估**：50 个源文档、5 个系统（Gold 摘要、Baseline、3 个重排系统）、每个摘要由 3 名 MTurk 标注者进行 5 级 Likert 评分和排序。

### 5.2 充分性与公正性评价

**优点**
- 对比基线设置合理（不仅对比无重排，也对比仅依赖源文档的无监督一致性重排）；
- 显著性检验齐全，证明结论不是随机波动；
- 从多方面（质量、事实性、人类偏好、长度、fact 提取数量分析）交叉验证；
- 计算了 Oracle 分数，给“当前方法离理论上界还有多远”提供了基准。

**不足 / 值得警惕之处**
- **论文自身对 FENICE 与 FIZZ 在重排时跳过相同指标的评测**（在表 3 表格中以 “—” 标注），意味着重排器使用 FENICE 时，没有给出 FENICE 的评估分（有轻微循环论证嫌疑）；
- XSum 数据集中，beam-sim 设置下 Baseline 质量指标 (ROUGE) 全面优于重排方法，作者虽解释为“不牺牲”事实性，但也表明该方法的稳定性有限；
- 两个公开数据集均为英文新闻文本，缺少多语言、多文档或对话摘要等其他文本类型的验证；
- 论文承认 Oracle 分数远高于目前方法，说明“从候选池中挑出最佳摘要”这一问题仍未解决。
- 由于候选池最多仅为 16，为验证达到最好质量所需的候选数量是否能贴合真实应用规模，论文并未充分深入。作者只考察到最大个数（64 参考/16 候选）后便定案。

---

## 6. 主要结论与发现

1. **ConSUM 全面提升了摘要事实性**：尤其在 XSum 上（高幻觉率的抽象式摘要任务）表现亮眼。例如在 XSum 上，FENICE-0.75 将 FIZZ 分数从 16.91（Baseline）提升至 27.79；在 CNN/DM 上，MENLI-Entailment 从 4.46 升至 10.44（epsilon 设置）——这类大提升表明共识机制确实能过滤幻觉性信息。

2. **事实性提升不以牺牲整体文本质量为前提**：在多数设定下 ROUGE、BERTScore 分数不降反升或保持竞争性。

3. **伪参考文献集的“多样性”与“外部性”至关重要**：扩充候选集之外的外部伪参考（64 条、由 Epsilon 采样生成）显著优于使用候选自身作为参考（self-reference），验证了“解耦生成”设计的必要性。

4. **共识的一致性重排优于纯粹一致性（consistency-only）和纯共识（consensus-only）**：权重组合分析发现，w=0.75 是总体最优平衡点。

5. **人工评估确认了机器的判断**：标注者明显偏好 ConSUM 的生成结果（FENICE-0.75、MBR-1.0 排名最高且统计一致性最高）；且标注者认为 CNN/DM 的 Gold 摘要质量偏差——佐证了 Zhang et al. (2024) 对“低质参考摘要”的观察。

6. **参考摘要质量问题的侧面验证**：在 LLM 生成设定中（Llama-3 未微调），ConSUM 达到较显著质量提升，结合 Gold Reference 的低评价，作者推断其机制是通过模型共识“纠正”了低质候选摘要的外部诱发幻觉。

---

## 7. 方法亮点

- **共识信号与一致性信号正交互补**：既考虑了“源文本说了什么”，又考虑了“模型整体分布内部在达成什么共识”，有效规避单一信号漏洞。
- **候选集与伪参考集解耦**：明确区分“参赛者”和“评委/参考答案”的不同角色，是设计上的创新亮点，避免低估多巴胺式的自我强化循环。
- **引入事实层面效用函数（MENLI）而不是文本相似度（ROUGE/BERTScore）**：重排不再偏向“更长的、词面大众脸”的摘要，而是偏向“在 NLI 层面相互支撑”的摘要。
- **彻底消融各类关键组件**：数量、伪参考来源、权重 w、解码算法、模型、显著性检验、Oracle 上限，给读者提供了完整的验证链。
- **公开代码与模型配置**，提升了社区可复现性。

---

## 8. 不足与局限

### 8.1 计算成本与可扩展性
- MBR 的 **O(n²) 计算复杂度**是天然瓶颈：候选数为 16、伪参考为 64 即需 1,024 次 MENLI 打分；未来若候选数量扩大，资源将迅速不堪重负。
- FENICE/FIZZ 等指标依赖 LLM（如 TikTok 用 T5/Orca-2）完成声明分解，长文摘要场景的规模化部署受限。

### 8.2 实验覆盖有限
- 仅适用**两种英文新闻基准**、**一个数据域（新闻）**。作者自己承认 XSum 与 CNN/DM 上的权衡表现分歧表明：方法在不同文本类型或语言上的效果可能需要调整（如 w 值）。
- 单语言实证带来说明书的外推性受限；多文档摘要、对话摘要、医学/法律长文档摘要有待验证。

### 8.3 存在乐观偏差风险
- 评估端与重排端使用同类指标（如用 FENICE 做重排时跳开 FENICE 自评），缺乏完全第三方指标独立验证（好在有 MENLI/human 做补充）。
- **Oracle 与最终值的巨大鸿沟**说明：即便有 16 条候选，目前的重排方法仍选不出其中的最优选项；该方法的“天花板”依然受制于底库生成质量。

### 8.4 评测缺陷
- ROUGE 在 LLM 生成长文摘要上分数偏低，传统 n-gram 重叠指标对被改写过的长摘要是否仍能准确反映语义质量，值得商榷。
- 人工评估只有 50 个样本，且部分标注者一致性分布离散度在研究备注（Gold/Baseline 排名“方差很大”）中暴露出不确定因素。

---

综上，ConSUM 将 MBR 共识与参考无关的事实一致性有机融合，获得了跨模型跨数据集的事实性改善，并通过人类评分验证了其重要性。但它的成功仍建立在“有限尺寸候选池 + NLI 评分模型 ”的组合之上，距离高效、大规模、全语言的理想摘要重排方案仍有一段距离。

（完）
