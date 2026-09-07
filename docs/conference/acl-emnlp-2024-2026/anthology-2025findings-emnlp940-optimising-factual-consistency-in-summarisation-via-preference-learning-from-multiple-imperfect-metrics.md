---
title: Optimising Factual Consistency in Summarisation via Preference Learning from Multiple Imperfect Metrics
title_zh: 通过多个不完美评估指标的偏好学习优化摘要事实一致性
authors: "Yuxuan Ye, Raul Santos-Rodriguez, Edwin Simpson"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.940.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 把多个不完美事实评估指标映射成偏好并去噪后用偏好学习优化摘要，缓解摘要中的事实幻觉
tldr: 摘要事实一致性评估指标往往本身存在噪声，单个指标无法可靠指导模型优化。本文提出一个自动化训练流程：将多个弱评估指标的分数映射为偏好对，并过滤掉高分歧样本，再通过偏好学习优化摘要模型。该流程无需复杂奖励塑形，能集成多种指标的互补优势。实验表明，聚合多个不完美指标可以有效提升摘要的事实一致性，为偏好优化在忠实摘要中的应用提供了实用方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 756, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 755, \"height\": 847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 148, \"height\": 88, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 588, \"height\": 154, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 610, \"height\": 149, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 629, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 638, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 536, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp940/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 638, \"height\": 440, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 992, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 739, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 648, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 741, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp940/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 372, \"height\": 195, \"label\": \"Table\"}]"
motivation: 单个摘要事实一致性指标不可靠，难以作为奖励信号稳定优化模型。
method: 提出自动化训练流程，将多个不完美指标映射为偏好对并过滤高分歧样本，再用偏好学习进行优化。
result: 实验证实基于多个弱指标汇总的偏好学习能提升摘要事实一致性。
conclusion: 聚合弱评估指标的偏好学习是一种无需复杂奖励塑形的忠实摘要优化策略。
---

## Abstract
Reinforcement learning with evaluation metrics as rewards is widely used to enhance specific capabilities of language models. However, for tasks such as factually consistent summarisation, existing metrics remain underdeveloped, limiting their effectiveness as signals for shaping model behaviour.While individual factuality metrics are unreliable, their combination can more effectively capture diverse factual errors. We leverage this insight to introduce an automated training pipeline that improves factual consistency in summaries by aggregating scores from different weak metrics. Our approach avoids the need for complex reward shaping by mapping scores to preferences and filtering out cases with high disagreement between metrics. For each source document, we generate lexically similar summary pairs by varying decoding strategies, enabling the model to learn from factual differences caused by subtle lexical differences. This approach constructs a high-quality preference dataset using only source documents.Experiments demonstrate consistent factuality gains across models, ranging from early encoder-decoder architectures to modern large language models, with smaller models reaching comparable factuality to larger ones.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## **Optimising Factual Consistency in Summarisation via Preference Learning from Multiple Imperfect Metrics**

---

## 1. 核心问题与整体含义（研究动机与背景）

- **摘要生成中的事实一致性挑战**：大型语言模型生成的摘要流畅且连贯，但时常包含与原文不一致的幻觉内容，即"表面合理但事实上错误"的表述。保持忠实性与事实一致性仍是摘要任务中的关键难题。
- **现有评估指标不可靠**：事实一致性评估指标，即使是最先进的，也常难以捕捉细微的不一致，甚至可能错误地惩罚本身事实正确的输出。直接将单一指标当作标量奖励用于强化学习（RL），会导致训练不稳定，且对奖励塑形非常敏感。
- **人类偏好反馈的局限**：基于人类反馈的强化学习（RLHF）依赖人工标注，但标注者的整体性判断往往包含对流畅性、可读性、个人偏好等因素的权衡，加上已有RLHF数据集普遍忽视事实性，导致其偏好信号无法可靠反映事实一致性。此外，构造事实性专用的偏好数据集需要大量专业标注资源，难以规模化。
- **核心思想**：

  作者提出一种**无需人工标注、无需参考摘要、无需复杂奖励塑形**的全自动化训练流程，其关键前提是：**单一弱指标不可靠，但组合多个弱指标可以获得互补的错误覆盖能力**，从而更有效地刻画不同类别的真实事实错误。

- **实践效果**：该方法在多个不同架构、不同规模的模型上取得了稳定的事实性提升；小型旧模型（BART）在事实性上能达到与显著更大、更新的模型相近的水平，具有重要的计算资源节约意义。

---

## 2. 方法论

### 2.1 核心思想

将**多个不完美的事实性评估指标**合并为训练信号，通过以下步骤完全自动化地构建高质量偏好数据集：

1. **生成总结对**
2. **用多个指标打分**
3. **转换为二元偏好并过滤冲突样本**
4. **使用 DPO（直接偏好优化）训练模型**

### 2.2 步骤一：总结对生成（Summary Generation）

为了让模型专注学习**由细微词汇差异引起的事实性差异**，而不被风格/结构差异干扰，作者生成**词汇相似度高**的摘要对。

- **束搜索（Beam Search）**：输出词序列整体概率最高的摘要，记作 `y_beam`：

  ```
  y_beam = arg max Σ_t log P(y_t | y<t, x)  （在候选束集合中搜索）
  ```

- **束搜索第2候选（BS#2）**：在束搜索中选取**第二高概率**的完整输出序列，记为 `y_beam'`，从而与BS#1构成词法高度相似的配对。

- **贪心解码（Greedy Decoding）**：在每个时间步选取概率最大的token：

  ```
  y_t = arg max log P(y_t | y<t, x)
  ```

  贪心输出与束搜索输出词法上较相似，但因为偏向局部最优token选择，事实一致性通常低于束搜索。

- **随机采样（Random Sampling）**：从温度缩放后的softmax分布中采样token：

  ```
  y_t ~ softmax(LM(y_t | y<t, x) / τ)
  ```

  主要用于对比实验，不属于主要配对策略。

最终论文主要采用两种配对方式：(BS#1, BS#2) 和 (BS#1, Greedy)。实验显示两者配对在词法相似度上显著高于 (BS#1, RS#1)，可有效排除风格差异的混淆。

### 2.3 步骤二/三：多指标评分 + 偏好聚合与冲突过滤

每个事实性度量 `m_i` 对摘要 `y` 和源文档 `x` 输出分数 `S_mi(y, x)`：

1. **各指标独立给出二元偏好标签**：

   ```
   P_mi(y1, y2, x) = sign(S_mi(y1, x) − S_mi(y2, x))
   ```

2. **冲突过滤器**：仅当所有指标对同一对摘要给出**一致的偏好方向**时，该样本才被保留用于训练；若指标之间存在分歧，说明该样本的标注信号本身存在噪声，直接丢弃。

通过这种"以一致性换可靠性"的策略，作者将多个弱信号的输出转化为高质量偏好标签，避免了多指标直接数值加权时的量纲不一致和权重人工设定问题。

### 2.4 步骤四：DPO训练

采用 **Direct Preference Optimization（DPO）** 而非经典RL，省去独立奖励模型，降低训练复杂度和算力需求：

```
L(θ) = E_{(x, y_w, y_l)} [ log σ( β ( f_θ(x, y_w) − f_θ(x, y_l) ) ) ]
```

其中 `y_w` 为获胜（chosen）摘要，`y_l` 为失败（rejected）摘要，`f_θ` 为模型赋予摘要的对数概率，`β` 为温度参数。DPO直接提升“赢得偏好”的摘要概率、降低“输掉偏好”的摘要概率，从而引导模型生成事实性更强的文本。

---

## 3. 实验设计

### 3.1 数据集与Benchmark

| 数据集 | 用途 | 源文档平均词数 | 摘要平均词数 | 压缩比 |
|---|---|---|---|---|
| XSUM | BBC新闻摘要 | 430（测试集433） | 23 | 5.35% |
| TL;DR | Reddit帖子摘要 | 313 | 31 | 9.90% |

- 服从既有公平比较的惯例，与Choi et al. (2024)保持一致。
- **事实性评估指标**：AlignScore、FactCC。
- **质量保持指标**：ROUGE-L、BARTScore。
- 另用 **ChatGPT-4o-mini** 进行两种人工近似评估：
  - 摘要整体质量的成对比较（Win Rate）；
  - 事实错误类型频度分析。

### 3.2 模型覆盖

| 模型 | 参数量 | 架构 | 预训练方式 | 微调方式 |
|---|---|---|---|---|
| BART-large | 406M | Encoder-Decoder | SFT | 全参数微调 |
| GPT-J | 6B | Decoder-only | SFT | LoRA |
| LLaMA-3.2-3B | 3B | Decoder-only | SFT+RLHF | LoRA |
| DeepSeek-R1-Distill-Qwen-7B | 7B | Decoder-only | SFT+RL | LoRA |

覆盖了从早期encoder-decoder模型到现代纯decoder大模型的多种架构，验证方法泛化能力。对于GPT-J，先进行摘要SFT。

### 3.3 对比基线

- **SFT**：监督微调，使用金标准参考摘要（模型自身的原始微调目标）。
- **RLHF**：基于人类偏好数据（如trl-lib/tldr-preference）进行RL训练，若不适用于DeepSeek/XSUM则省略。
- **MPO**（Choi et al. 2024）：假设束搜索输出恒优于其他解码输出，以启发式规则构造偏好，无需评分指标。

### 3.4 评价设置

- 5种事实错误类型（Intrinsic, Extrinsic, Noun, Predicate, Quantifier）由ChatGPT标注频次。
- 偏好冲突过滤率在27.3%~37.3%之间，至少有60%以上的数据保留可用。

---

## 4. 资源与算力

- **论文未明确报告GPU型号、GPU数量、训练时长、显存消耗等具体算力信息**。
- 仅提及使用了**Isambard-AI 英国国家AI研究资源（AIRR）**，由Bristol大学运营。
- 对DeepSeek-R1等较大模型使用了**LoRA**适配器训练，以减少显存与计算消耗；BART采用全参数微调。

**注**：论文缺少量化计算资源的表格或描述，若需复现需要自行估算算力成本。

---

## 5. 实验数量与充分性

### 论文进行了较充分的实验，主要包含：

1. **两种解码配对策略**：(BS#1,BS#2) 与 (BS#1,Greedy) 分别训练与评估；
2. **4种模型 × 2个数据集**的组合实验，主评估表涵盖64个数据点以上；
3. **3条基线对比**：SFT/RLHF/MPO；
4. **消融实验**：
   - 单一指标（SBERTScore 或 SummaC） vs. 双指标 vs. 双指标+冲突过滤；
   - 不同相似度层级摘要对的对比；(BS#1,BS#2)、(BS#1,Greedy)、(BS#1,RS#1)
5. **ChatGPT 整体质量对决评估**：每数据集随机抽样500篇，共4个模型 × 2个数据集，多个win rate数据点；
6. **错误类型频次分析**：共8张柱状图，统计训练前后各错误类型变化；
7. **训练动态指标**：展示DPO训练期间评估准确性变化曲线。

### 充分性分析

- **优点**：模型多样性好（早期小模型到现代7B推理模型）；覆盖两个性质不同的数据集（新闻文章与Reddit帖子）；消融实验足以验证各设计组件（多指标、过滤、相似配对）的独立价值；多处结论通过交叉比较（如与MPO的效果对比、与Choi et al.结果参考对照）增强了可信度。
- **不足风险**：作者未提供多组随机种子的均值/方差信息，也缺少显著性检验，统计稳健性有待确认。
- **客观性考量**：为与Choi et al. (2024)公平比较，评估指标选择与之一致；决策采用同一编码器/解码策略进行最终评估；ChatGPT评估时尽量统一提示词。然而，**评测指标的可靠性本身存在局限**，AlignScore/SummaCSBERTScore可能隐含系统性偏差，这是该领域普遍面临的挑战。由于TL;DR数据集的SummaC Conv模型在跨域场景中的泛化性不确定，对TL;DR上的事实性判定可能引入系统性偏差。

---

## 6. 主要结论与发现

1. **多弱指标聚合配合偏好过滤，显著提升事实性**：在所有四个模型、两个数据集上，使用SBERTScore+SummaC并加上冲突过滤的方案均一致优于SFT、RLHF和MPO，AlignScore全面提升。
2. **小模型的"复活"效果**：
   - BART 在 XSUM 上 AlignScore从61.9提升至86.6（**+24.7**），超过原始LLaMA-3.2（86.1）与DeepSeek-R1（82.5）的SFT基线；
   - BART在TL;DR上以94.2的AlignScore达到/超过LLaMA、DeepSeek水平。
   - 这意味着**较小的旧模型在事实性方面可以超越现代大模型**，大幅降低了计算成本门槛。
3. **RLHF和MPO可能降低事实性**：RLHF在多个模型上导致AlignScore下降（如GPT-J上降低8.1）；MPO在LLaMA两个数据集上均降低AlignScore。MPO在相似的摘要对上甚至出现事实性崩塌现象，说明启发式偏好不可靠。
4. **偏好对之间的词法相似度是有效学习的必要条件**：
   - 与随机采样配对的低相似度样本(BS#1,RS#1)即便使用本方法训练，其提升效果（+10.1）明显不如高相似度的(BS#1,BS#2)（+24.7）。
5. **多指标融合与过滤缺一不可**：
   - 单一指标训练有时会导致退化（例如LLaMA在与某些指标下AlignScore下降）；
   - 多指标联合+冲突过滤在所有实验中达到最优。
6. **权衡问题**：
   - ROUGE-L的略降意味着事实性与参考摘要相似度之间存在固有trade-off；作者引用了Maynez et al.(2020)的发现——人工参考文献有时自带幻觉，因此认为该权衡是可以接受的。
   - ChatGPT对整体质量的偏好中，SFT和RLHF摘要获胜率高于本方法，主要是因为SFT/RLHF生成的摘要包含更多细节、更丰富，并非因更准确。这也再次印证"整体人类偏好经常忽视事实性是系统性偏差"这一观点。

---

## 7. 方法/实验的亮点（优点）

1. **完全自动化且低成本**：只用源文档即可构造偏好数据集，不需要人工标注或参考摘要，可扩展到任意规模的文档集合。
2. **规避奖励塑形复杂性**：通过将异构分数映射为偏好而非标量加权，绕开了指标量纲/权重设计问题；结合冲突过滤，大幅降低了噪声。
3. **同类配对设计**：词法相似的摘要对让模型专注学习"事实性差异"而非风格差异，更利于从细微解码差异中捕捉错误模式。
4. **对"模型在训练中崩溃"问题的稳健性**：对比Roit et al.(2023)需要大模型作为奖励模型的方案，本文方法从未出现灾难性遗忘，训练过程更稳定。
5. **较好的泛化能力与可迁移性**：从BART-large到7B的DeepSeek-R1都有效，验证跨架构和跨规模适应性，具备很强的实用价值。
6. **多指标决策鲁棒性原理清晰**：各指标存在不同的互补偏差，单一指标的误判无法主导整体信号，冲突过滤保证了"赢家"至少被多数指标一致认可。
7. 对小模型的提升具有**实际应用价值**——在资源受限环境中无需部署数百亿参数模型也能生成高事实性摘要。

---

## 8. 不足与局限

1. **仅使用两个事实性指标**：SBERTScore与SummaC代表两类方法，但更丰富的指标（QA-based方法、AlignScore等更强检测方法）未纳入实验。虽然这主要是为了控制计算成本，但减弱了结论对不同评分函数的普适性证明。论文没有测试若更换为更强或更弱的指标时效果是否一致。
2. **缺少RL直接奖励的对照实验**：作者早期探索时发现用标量指标奖励进行RL在中小模型上极易发生灾难性遗忘，需要极大模型和极致算力才可稳定。虽然解释合理，但没有报告这些对照数据，减弱了基于RL基线比较的系统性。
3. **未报告统计显著性检验与重复实验方差**：没有执行不同随机种子下的稳定性验证，也没有提供置信区间，无法判断观察到的提升差异是否具有统计显著性。
4. **DL/DeefSeek模型上增益相对有限**：DeepSeek-R1只有0.7~1.8的AlignScore提升。作者推测原因是其长链思维中的推理错误无法被面向最终摘要的指标捕获，但这一假设未做进一步实验验证。
5. **整体质量的退化风险**：ChatGPT的对比评估显示本方法摘要的总体偏好度低于SFT/RLHF。虽然实验分析显示这主要归因于风格（细节少）而非法事实性，但摘要"简洁度"与"事实性之间"的权衡仍需面向具体应用场景仔细斟酌；过度追求事实性可能使摘要过度保守、信息量不足。
6. **推理模型的适用性尚不充分**：DeepSeek-R1的思维链过程被绕过/过滤，忽略推理过程中的事实错误，存在改进空间；
7. **跨语言/跨域泛化问题未涉及**：论文仅在英文新闻（XSUM）和英文Reddit帖子（TL;DR）上验证，尚无证据表明方法在中文等多语言、科学文献等其他领域的有效性。
8. **无法摆脱对评估指标质量的依赖性**：虽然比单指标强，但聚合指标仍受各指标系统性偏误影响；若所有指标同时失效（如面对极高抽象度的总结），整个管道质量将无从保证。

---

（完）
