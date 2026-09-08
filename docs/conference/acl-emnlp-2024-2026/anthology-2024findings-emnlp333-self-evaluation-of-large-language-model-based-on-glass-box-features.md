---
title: Self-Evaluation of Large Language Model based on Glass-box Features
title_zh: 基于玻璃箱特征的大语言模型自我评估
authors: "Hui Huang, Yingqi Qu, Jing Liu, Muyun Yang (杨沐昀), Bing Xu, Tiejun Zhao (赵铁军), Wenpeng Lu"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.333.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 让模型利用softmax分布等玻璃箱特征评价自身输出，属自评方向。
tldr: 针对依赖外部评判者评估大语言模型的既有范式，本研究在自评价场景中系统考察模型自身的玻璃箱特征，即让模型利用内部信息评判自己的输出。实验发现softmax分布可作为可靠的生成质量指标，公开基准上的结果表明，基于玻璃箱特征进行自评价是可行且有效的。该工作为无外部监督的模型自我评估提供了新路径。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 708, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1286, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1280, \"height\": 868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1282, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1277, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp333/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1283, \"height\": 606, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp333/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 1171, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp333/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 764, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp333/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 746, \"height\": 863, \"label\": \"Table\"}]"
motivation: 现有评估大多依赖外部评估器或训练提示，忽略了模型内部玻璃箱特征的自我评估价值。
method: 系统考察多种玻璃箱特征，如softmax分布，在大语言模型对自身输出的自评价中的表现。
result: 在公开基准上的实验显示，softmax分布可以作为稳健的自评估质量指示器，验证了方法的可行性。
conclusion: 模型自身的内部特征能够支撑可靠的自评估，减少对外部评估模型的依赖。
---

## Abstract
The proliferation of open-source Large Language Models (LLMs) underscores the pressing need for evaluation methods. Existing works primarily rely on external evaluators, focusing on training and prompting strategies. However, a crucial aspect – model-aware glass-box features – is overlooked. In this study, we explore the utility of glass-box features under the scenario of self-evaluation, namely applying an LLM to evaluate its own output. We investigate various glass-box feature groups and discovered that the softmax distribution serves as a reliable quality indicator for self-evaluation. Experimental results on public benchmarks validate the feasibility of self-evaluation of LLMs using glass-box features.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

本文针对大语言模型（LLM）评估这一核心问题展开研究。研究背景与动机如下：

- **现有评估方法的局限**：传统评估指标（如 BLEU、ROUGE）只能捕捉生成文本的有限方面；基于外部大模型（如 GPT-3.5、GPT-4）的评估方法存在隐私泄露风险和评估不可复现问题；微调开源模型作为专用评估器的方法受限于底层模型能力，在泛化性和公平性上明显不如 GPT-4。
- **提出一个新的研究问题**：LLM 是否具备**自我评估（Self-Evaluation）**能力？
- **核心思路**：不同于依赖外部评估器的范式，论文主张利用**模型自身的"玻璃箱特征"（Glass-box Features）**——即模型在生成过程中产生的内部信息（如 softmax 分布、不确定性、注意力分布）——来评估其自身输出的质量。
- **整体含义**：这项工作探索了一条不依赖外部评估 API、无需额外微调评估器的新路径，为 LLM 的自我反思、奖励建模等下游应用提供了可行基础。

## 2. 方法论

论文提出了基于玻璃箱特征的 LLM 自我评估框架，具体包含以下核心组成部分：

### 2.1 三类玻璃箱特征

**（1）Softmax 分布特征**

- 观测来源：模型每一步解码时输出的词汇概率分布 p(yₜ)。
- **Softmax-Ent（熵）**：对每个解码步的 softmax 分布计算熵并取句子级平均。若概率质量集中在少数词汇上，说明模型对生成内容有信心，响应质量可能较高；若分布接近均匀分布，则生成质量预期偏低。
- **Softmax-Var（方差）**：计算响应中各词级概率的方差，捕捉熵在平均化时可能丢失的概率离散度信息。
- **Softmax-combo**：将二者归一化后相加融合。

**（2）不确定性估计**

- 核心原理：若模型对生成内容有信心，多次前向传播得到的概率分布应高度集中、彼此差异小。
- 由于 LLM 通常在没有 dropout 的情况下训练，论文提出两种注入随机性的策略：
  - **解码集成（Decoding-based Ensemble）**：采用随机 top-k 采样进行多次推理；
  - **提示集成（Prompt-based Ensemble）**：从一个预设计的系统提示池中随机选取系统提示进行多次推理。
- 通过多次前向传播得到句子级概率后，计算其期望（Unt-Exp）和方差（Unt-Var）作为不确定性度量。

**（3）注意力分布特征**

- 计算注意力权重分布的熵（AttnEnt），并总结不同层和头的注意力熵——取最小值（AttnEnt-Min）或平均值（AttnEnt-Avg）。

### 2.2 参考增强策略（Self-Evaluation with Reference）

当存在参考答案时，论文提出两种利用参考增强评估的方法：

**（1）上下文示例（In-Context Illustration）**

- 将"指令+参考回答"作为 in-context demonstration 拼接到待评估的指令和响应之前参与模型推理，从而让模型在评估时有一个隐含的语义参照；
- 模型需要基于既定上下文去生成当前答案时，其产生的 softmax 分布差异就能反映当前回答和参考回答之间的差距，作为质量指标。

**（2）概率校准（Probability Calibration）**

- 由于参考回答理应得到最高质量分，可通过对模型预测参考回答的对数概率（SentProb-Ref）来衡量模型自身的偏差；
- 将当前响应的评估结果减去参考回答的该项值，从而缓解评估偏差。

## 3. 实验设计

### 3.1 数据集与基准（Benchmark）

- **MT-Bench**：涵盖 80 个问题，涉及多样领域；
- **Vicuna-Bench**：同样涵盖 80 个问题；
- 两个基准均按各基准的官方评估器设置，使用 **GPT-4** 对模型生成的响应进行标注，作为评估的"金标准"。论文明确指出由于时间和资源限制，没有使用人类标注。
- 获取各模型在基准上的响应，均遵循 MT-Bench 默认设置。

### 3.2 评估模型

- **Vicuna-7B**
- **LLaMA2-7B-Chat**

两者均具备指令跟随能力。

### 3.3 对比方法与指标

- **对比基线**：
  - **GPT-3.5-Turbo**：闭源 LLM，经过精心设计的提示词后作为评估器；
  - **Auto-J**：针对 LLM 评估任务专门微调过的开源评估器；
  - **Self-Generation**：直接提示模型对自己的响应打 1~10 分的生成式自评估；
  - 此外还对比了 **SentProb**（简单生成概率）等变体。
- **评估指标**：以 **Pearson 相关系数**为主要指标，辅以 **Spearman 秩相关系数**与 **Kendall Tau 秩相关系数**。

## 4. 资源与算力

论文原文中**没有明确报告使用了多少 GPU 型号、数量、训练时长等具体算力资源**。从文中的一些描述侧面可以推断：

- 实验只涉及两个 7B 规模的模型推理，且不确定性集成方法需要多次前向传播（文中设置为 10 次 forward pass）；
- 作者提到"考虑到多次前向传播过于耗时"，说明计算成本是作者考虑实际应用性的一个重要因素；
- 因此，该工作在 7B 模型上的推理级成本相对可控，但具体硬件信息无从得知。

## 5. 实验数量与充分性

### 实验数量和结构

论文的实验布局主要包含三部分：

1. **主实验**：在 MT-Bench 和 Vicuna-Bench 两个基准 × 两个模型（LLaMA2-7B-Chat 和 Vicuna-7B）上，对比了 12 种方法的性能（包括 Auto-J、GPT-3.5-Turbo、Self-Generation、SentProb、Softmax-Ent、Softmax-Var、Softmax-combo、各类不确定性方法和注意力方法）；
2. **参考增强实验**：在 Vicuna-Bench 上针对 Softmax-Ent 和 Softmax-Var 分别检验了 "+illustration"（上下文示例）和 "+calibration"（概率校准）两种策略的效果；
3. **两组软max特征的融合改进**（Softmax-combo）。

每组报告了 Pearson、Kendall、Spearman 三个相关性指标，因此总共约有 2（模型）× 12（方法）× 2（基准）= 48 组主实验数据，加上 8 组参考增强消融数据，实验规模在学术论文中属中等范畴。

### 充分性与公平性评估

- **充分的地方**：对比方法覆盖面较广，兼顾了闭源大模型（GPT-3.5）、专用微调评估器（Auto-J）和自生成评估等多种范式；相关性指标多样。
- **不够充分的地方**：
  - 仅用了两个 7B 模型，没有覆盖更大规模的模型，泛化结论受限；
  - 金标准标注依赖 GPT-4 而非人类标注，存在系统性偏差风险；
  - 生成式基线（Self-Generation、Auto-J、GPT-3.5）用的是 1~10 打分格式，而本文方法输出的是连续实数，作者承认用秩相关系数对比并不完全公平；
  - 参考增强实验仅在一个基准（Vicuna-Bench）上进行，广度有限；
  - 不确定性集成中 forward pass 次数固定为 10，没有进行灵敏度分析。

## 6. 主要结论与发现

1. **Softmax 分布是可靠的自我评估质量指示器**：在三组玻璃箱特征中，softmax 分布相关特征（尤其是 Softmax-Var）与标注结果的相关性最高，且效果超过 Auto-J 和 GPT-3.5-Turbo，验证了"模型置信度与响应质量强相关"这一假设。
2. **融合熵与方差（Softmax-combo）可进一步提升效果**：两者互补性强，融合后比单独使用任一指标都更好。
3. **不确定性集成方法实际效果有限**：尤其是基于方差的变体效果较差，原因可能在于 10 次前向传播不足以可靠量化不确定性；多次前向传播的时间成本也让该方法实践性不佳。
4. **注意力分布不适合作为 LLM 响应的质量指标**：注意力熵在 LLM 自回归生成场景中与响应质量无明显关联，这与机器翻译质量估计场景不同。
5. **参考信息对自我评估有重要价值**：两种参考增强策略都能有效提升评估准确性，其中**概率校准**方法效果更好，说明通过减去参考响应对数概率来校准偏差是一种有效手段。
6. **LLM 具备自我评估的潜力**：玻璃箱特征方法不受被评估模型自身能力限制，在 7B 规模模型上就能超越 GPT-3.5 等强外部评估器。

## 7. 优点

- **方向新颖**：将"玻璃箱特征"引入 LLM 自评估场景，打破了以往依赖外部评估器或独立评估模型的固有范式，为该领域提供了全新视角；
- **成本效益显著**：不需要调用外部 API（避免隐私泄漏和不可复现），也不需要微调额外评估器；作为模型生成的副产品即可获得特征；
- **简单有效**：方法核心是基于 softmax 熵和方差的统计量，无需复杂训练或提示工程，却在 MT-Bench / Vicuna-Bench 上超过 GPT-3.5-Turbo 与 Auto-J，显示出惊人简洁性；
- **可解释性强**：特征本身具有概率语义，能够从模型"信心"角度解释为什么响应好或不好；
- **参考增强策略设计巧妙**：特别是概率校准，针对自回归语言模型的固有偏差提出了具有理论依据的修正方案；
- **代码开源**：便于后续研究复现与扩展。

## 8. 不足与局限

1. **缺乏人类评估验证**：论文主要依赖 GPT-4 作为元评估标注，而 GPT-4 自身也存在偏见和误差，使用人类评估者会使结论更可靠；
2. **模型规模覆盖面窄**：仅在 7B 版本模型（LLaMA2-7B-Chat、Vicuna-7B）上验证，更大规模模型（如 13B、70B）中的表现尚未验证，限制了结论的外推性；
3. **与生成式评估方法的比较不完全公平**：作者自己也承认，生成式方法输出的是离散分数（1~10），而玻璃箱方法是连续实数，用秩相关系数对比不占优势；
4. **无法预测并列分**：基于玻璃箱特征的方法不能有效生成相等分数，在排序类场景中表现受限；
5. **参考增强实验不完整**：参考增强实验仅在一个 benchmark（Vicuna-Bench）上进行，泛化性未知；
6. **方法在什么条件下失效不清晰**：如对于已高度对齐且自信但实际输出有误（幻觉）的情况，softmax 置信度是否能保持可靠，仍待进一步研究；
7. **不确定性估计的集成次数没有敏感性分析**：固定为 10 次前向传播的依据不足，是否需要更多前向传播、是否存在效率与效果的 Pareto 最优平衡点均未探究；
8. **对下游应用的拓展验证不足**：作者提出该方法可服务于自我反思、奖励建模等下游任务，但未提供实际验证。

（完）
