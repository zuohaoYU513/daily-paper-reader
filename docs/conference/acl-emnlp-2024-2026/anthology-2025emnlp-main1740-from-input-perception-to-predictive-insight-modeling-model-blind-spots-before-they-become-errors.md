---
title: "From Input Perception to Predictive Insight: Modeling Model Blind Spots Before They Become Errors"
title_zh: 从输入感知到预测洞察：在错误发生前建模模型盲区
authors: "Maggie Mi, Aline Villavicencio, Nafise Sadat Moosavi"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1740.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 仅利用输入的token似然特征在错误发生前预测模型盲区，支持对不可靠输出进行选择性弃答
tldr: 本文关注语言模型对习语、比喻等复杂输入即使生成流畅也可能误解并出错的问题，提出一种仅基于输入的方法。该方法以surprisal和均匀信息密度假设驱动的token级似然特征捕捉对输入理解的局部不确定性，从而在输出产生前预测失败。实验结果覆盖五个语言挑战数据集，表明该方法能有效预测错误，是无需输出或内部激活的轻量级错误预判工具。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1740/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1483, \"height\": 1068, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1740/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 1206, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1740/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 1297, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1740/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1740/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 295, \"label\": \"Table\"}]"
motivation: 模型常因误解输入而在后续输出中失败，希望提前发现盲区以决定是否信任。
method: 基于surprisal和均匀信息密度假设，提取输入token的似然特征来预测失败。
result: 在五个语言挑战数据集上优于标准基线，较大模型受益于局部特征，较小模型受益于全局特征。
conclusion: 输入侧似然特征可在不访问输出或隐藏状态时有效预警模型错误，支持选择性预测与拒答。
---

## Abstract
Language models often struggle with idiomatic, figurative, or context-sensitive inputs, not because they produce flawed outputs, but because they misinterpret the input from the outset. We propose an input-only method for anticipating such failures using token-level likelihood features inspired by surprisal and the Uniform Information Density hypothesis. These features capture localized uncertainty in input comprehension and outperform standard baselines across five linguistically challenging datasets. We show that span-localized features improve error detection for larger models, while smaller models benefit from global patterns. Our method requires no access to outputs or hidden activations, offering a lightweight and generalizable approach to pre-generation error prediction.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

论文关注语言模型（LM）在习语、隐喻、转喻等上下文敏感输入上的一类特殊失败：**模型并非在生成时产生明显错误，而是从一开始就误读了输入**，随后以高置信度生成一个看似流畅但语义错误的答案。作者试图回答一个关键问题——**能否在模型生成任何输出之前，仅通过模型对输入 token 的内部似然结构来预测其是否可能出错**？

该问题密切关联可靠 AI 系统的安全需求：若能在解码前识别可能出错的实例，就可以有选择性地触发人工审核、拒答或降级处理，从而服务于选择性预测（selective prediction）与模型风险控制。

### 2. 方法论

**核心思想：输入似然表面编码了模型的理解盲区。** 基于均匀信息密度（UID）假设与心理语言学中的 surprisal 研究，作者认为语言模型对非常规输入（如习语或隐喻）的理解困难会在其逐 token 的预测概率上留下可测的“扰动痕迹”，这些痕迹可作为提前预测错误的信号。

**四种信息论度量**（输入概率分布的不同刻画）：

- **Surprisal (SPR)**：`SPR(t_i) = -log2 P(t_i | t<i)`，衡量第 i 个 token 在既定上下文中的意外程度。
- **Entropy (H)**：模型在预测下一 token 时的整体不确定性（分布覆盖度）。
- **Confidence-Weighted Surprisal (CWS)**：在 surprisal 中加入 KL 散度惩罚项，用于惩罚“碰巧给出现有 token 居中概率但整体分布弥散、缺乏语义承诺”的情况。参考分布 Q 给当前已观察 token 赋 0.9 概率，其余 0.1 均匀分配。
- **Contextual Influence Score (CIS)**：条件点互信息，度量 token t_i 对预测下一 token t_{i+1} 的增量预测贡献。

**特征提取层次** （g ∈ {句子、表达式、边界、上下文}）：基于上述每种度量，文本对不同区间（整句、标注的关注 span、span 相邻边界、扣去 span 的上下文）计算均值、最大值、最小值和标准差，构成完整特征向量。

**基于语言学直觉的局部特征**（用于带有 span 标注的场景）：
- 习语固定性：单调递减特征与局部 surprisal 尖峰数量（习语后半部分通常更可预测）；
- 选择偏好违例：span 末尾到后续 token 的信息增量变化（隐喻中动词-论元语义错配）；
- 高上下文信息：全局最大信息点是否落在 span 内。

**分类器**：逻辑回归（L-BFGS，2500 次迭代）与三层 MLP（512×512 隐层、ReLU、Adam、学习率 1e-3、20 epoch），80/20 分层随机划分训练/测试集。

### 3. 实验设计

**数据集**（覆盖三类非字面语言现象）：
- **习语性**：DICE——刻意保持习语字面形式与修辞形式同形，迫使模型依赖语境而非结构线索判断；
- **隐喻**：MOH-X、TroFi——动词隐喻/字面识别；
- **转喻**：PUB 14（专名转喻，Task 14 Reference via Metonymy）、ConMeC（常用名词转喻，如 glass 指 wine）。

**被检测模型**（7 个不同规模的开放权重模型）：Llama-3.1-8B-Instruct、Llama-3.2-3B-Instruct、Llama-3.2-1B-Instruct、Qwen2-1.5B-Instruct、Qwen2.5-0.5B-Instruct、Qwen2.5-7B-Instruct-1M、Qwen2.5-14B-Instruct-1M。

**对比基线**：全局平均 log 概率、全局平均最大 token 概率、Oddballness（序列中最异常 token 的“Oddball 分数”）。

**评估指标**：错误检测的 F1 分数（两个分类器各自独立评估，三次运行取平均）。

### 4. 资源与算力

论文明确说明使用了 **2 张 A100 GPU** 完成全部特征提取环节（对模型进行提示，并从模型获取各 token 的 logits）；分类器（逻辑回归/MLP）在 CPU 上即可运行。论文未提供 GPU 总时长、总训练时长或能耗的统计报告，也未报告确切推理预算。

### 5. 实验数量与充分性

论文实验覆盖面较广，主要包括：

- 5 数据集 × 7 模型 × 2 分类器（逻辑回归与 MLP）× 4 种特征配置的对比矩阵；
- 3 种基线的系统对比（单基线 + 联合基线组合）；
- 针对 4 个信息度量的逐一消融（去掉 CWS / Surprisal / CIS / Entropy），并分别报告两个分类器上的 F1 差异；
- 句子级特征与语言学局部化特征的对比分析。

**评价**：实验矩阵跨模型尺度和语言学现象，设计较客观，重复三次取平均增加稳定性，并采用分层抽样防止类别不平衡扭曲结果。不过所有评测均在英语数据上进行，且仅覆盖开放权重模型，因此外推到其他语言和 API 黑盒模型仍有待验证。

### 6. 主要结论与发现

- **输入侧似然特征确实能先于生成预测错误**。在粗粒度全局指标（log 概率、max token 概率、Oddballness）几乎失效的场景（多个模型在 DICE 与 TroFi 上的 F1=0）中，结构化句子级特征普遍产生显著提升，将“零信号”转化为有意义的检测性能。
- **全局模式与小模型更契合**。句子级特征对较小模型（0.5B–1.5B）已可捕获大部分信号。
- **局部化到标注 span 对大型模型增益显著**（如 Qwen2.5-7B、Qwen2.5-14B 在 ConMeC 上获得大幅提高），说明大模型更需要有针对性的局部测量来暴露理解盲区。
- **特征重要性受分类器影响**：逻辑回归主要利用 Surprisal/Entropy；MLP 等高容量非线性模型则更多利用 CIS 与 Entropy 的交互。CWS 与 Surprisal/Entropy 高度共线，边际增加最小。
- 分类器选择对结果影响有限，但 MLP 在难度更高、非线性更强的任务（TroFi、ConMeC）上表现通常更稳定。

### 7. 方法优点

- **纯输入侧 + 预生成定位**：仅需输入 token 的登录概率，不需要输出、logits 或隐藏激活，与现有输出级/激活级探测器可正交组合，也天然兼容黑盒 API（只需暴露 token 对数概率）。
- **轻量且可解释**：特征建立在明确的语言学与心理语言学理论之上（surprisal、UID、选择偏好约束），具备较强的可解释性。
- **兼具泛化性与扩展性**：句子级全局特征不依赖任务标注，可直接部署；跨习语、隐喻、转喻三类非字面现象一致性验证了方法普适性。
- **清晰的部署指引**提出实用性配方：默认使用句子级特征；当目标区域可推断或可标注时附加 span 局部特征，可针对大型模型获得额外增益。

### 8. 不足与局限

- **语言覆盖受限**：只在英语上验证，缺乏多语言语境下的证据。
- **未覆盖闭源/商用模型**：受研究预算约束未评估 GPT-4 类闭源模型，而这类模型恰恰是现实部署中最普遍的，其黑盒性使得输入侧信号在它们上面尤其有价值却也最不确定。
- **超小型模型被排除**：低于 2B 的模型（如 SmolLM）在所有任务上都无法给出任何正确输出，无法用于错误检测分类器的训练与评测，造成能力谱系不完整。
- **对标注的依赖**：span 局部化需要任务/数据集相关的表达式边界标注，在无标注的现实环境中不能直接使用，须结合自动定位方案。
- **提示敏感性与统一性**：论文未进行提示工程优化，但不同任务的自有指令格式（如多项选择与自由作答）可能影响概率分布形态，削弱跨任务的可比性。
- **缺少实际推断成本报告**：并未系统性报告 API 调用开销或时间成本，在需要大规模工业部署时，该方法的性价比仍有待进一步说明。

### 一句话总结

本文提出一种仅基于输入 token 似然结构即可在生成前预判语言模型错误风险的框架，系统性证明“模型怎么读输入”本身就能比“模型怎么说”更提前地暴露深层语义理解的盲区。

（完）
