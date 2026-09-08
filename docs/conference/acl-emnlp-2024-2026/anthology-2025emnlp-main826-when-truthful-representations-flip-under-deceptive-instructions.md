---
title: When Truthful Representations Flip Under Deceptive Instructions?
title_zh: 真实表示何时会在欺骗性指令下翻转？
authors: "Xianxuan Long, Yao Fu, Runchao Li, Mu Sheng, Haotian Yu, Xiaotian Han, Pan Li"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.826.pdf"
tags: ["query:metacognitio"]
score: 7.0
evidence: 用线性探针与稀疏自编码器从内部表示预测真实/欺骗性输出
tldr: 大语言模型会被恶意指令诱导生成欺骗性回答，但其内部表示如何从真实翻转为欺骗仍不清楚。该文在Llama-3.1-8B-Instruct与Gemma-2-9B-Instruct的事实验证任务上分析表示翻转，发现线性探针可基于内部表示预测模型被指示的True或False输出，并进一步用稀疏自编码器定位翻转特征。研究显示真实与欺骗信号在内部状态中可被探测，对理解模型事实判断与伪装机制具有启示意义。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main826/fig-001.webp\", \"caption\": \"\", \"page\": 6, \"index\": 1, \"width\": 2000, \"height\": 1333}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main826/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 2000, \"height\": 547}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main826/fig-003.webp\", \"caption\": \"\", \"page\": 19, \"index\": 3, \"width\": 1152, \"height\": 672}]"
motivation: 欺骗指令如何改变LLM内部真实表示尚未被理解，仅看输出层分析不足。
method: 在两个指令模型的事实验证任务上用线性探针跨条件预测被指示输出，并用稀疏自编码器分析表示翻转。
result: 探针能依据内部表示预测True/False输出，并定位与欺骗相关的特征单元。
conclusion: 内部真实到欺骗的翻转可被探测和局部分析，有助于揭示LLM在恶意指令下的事实判断变化。
---

## Abstract
Large language models (LLMs) tend to follow maliciously crafted instructions to generate deceptive responses, posing safety challenges. How deceptive instructions alter the internal representations of LLM compared to truthful ones remains poorly understood beyond output analysis. To bridge this gap, we investigate when and how these representations “flip”, such as from truthful to deceptive, under deceptive versus truthful/neutral instructions. Analyzing the internal representations of Llama-3.1-8B-Instruct and Gemma-2-9B-Instruct on a factual verification task, we find the model’s instructed True/False output is predictable via linear probes across all conditions based on the internal representation. Further, we use Sparse Autoencoders (SAEs) to show that the Deceptive instructions induce significant representational shifts compared to Truthful/Neutral representations (which are similar), concentrated in early-to-mid layers and detectable even on complex datasets. We also identify specific SAE features highly sensitive to deceptive instruction and use targeted visualizations to confirm distinct truthful/deceptive representational subspaces.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

大语言模型（LLMs）在指令跟随方面表现出色，但也带来了安全隐患：当模型遭遇恶意构造的指令（如被明确要求“撒谎”或“必须具有欺骗性”）时，倾向于生成与事实相悖的虚假回答。已有研究多停留在**输出层面**（即评估模型最终说谎与否），而关于此类欺骗性指令如何**在内部表示层面**改变模型的信息编码，仍缺乏深入理解。

本论文的核心问题是：**模型的内部表示从“真实”（truthful）翻转为“欺骗”（deceptive）这一过程究竟发生在何时（哪些层）、以及如何发生（哪些特征层面）？** 这一研究与模型的“知识感知”（knowledge awareness）和“道德诚实机制”密切相关——模型在恶意指令下是否仍保留对事实的判断，只是在输出阶段被“翻转”，还是中间层表示本身就被系统性扭曲？回答这一问题，对于设计可解释的欺骗检测器、进行模型编辑与安全对齐具有重要意义。

## 2. 论文提出的方法论

### 2.1 核心思想
论文将“指令如何重塑内部表示”这一宏观问题，拆解为两个可验证的子问题：
1. 模型的最终“True/False”输出是否始终可从内部激活中**线性解码**（无论指令是诚实、中性还是欺骗）？
2. 在更细粒度的**稀疏特征空间**中，不同指令条件是否导致系统性的表示偏移？

### 2.2 技术路线

**（1）任务框架与提示条件**
- 将任务设定为**二值事实验证**：给定陈述，模型输出“True”或“False”。
- 设计三种指令条件：
  - **Truthful**（诚实）：要求始终诚实并正确判断
  - **Neutral**（中性）：仅要求输出“True/False”
  - **Deceptive**（欺骗）：明确要求“不诚实、必须欺骗、错误判断”

**（2）表示提取**
- 提取每个 Transformer 层残差流中、模型生成输出 token **前一位**的激活向量 \(x_l \in \mathbb{R}^d\)（末 token 位置）。

**（3）线性探针（Linear Probing）**
- **LR（逻辑回归，Logistic Regression）**：训练线性分类器预测目标输出：\(P(y=\text{True}|x_l) = \sigma(w_l^\top x_l + b_l)\)。
- **TTPD（Truth and Polarity Direction，真值与极性方向训练）**：按 Bürger et al. (2024) 的方式建模激活：\(\hat{x}_{ij} = \mu_i + \tau_{ij} t_G + \tau_{ij} p_i t_P\)，分别估计通用方向 \(t_G\) 与极性敏感方向 \(t_P\)，用 \(t_G\) 做分类。TTPD 作为对 LR 的稳健性补充。

**（4）稀疏自编码器（SAE）特征分析**
- 使用预训练 SAE 套件（Llama Scope 的 LXR-32x-TopK SAE，128k 特征；Gemma Scope 的 JumpReLU SAE，16,384 特征/层）将激活 \(x_l\) 分解为高维稀疏特征向量 \(f(x_l) \in \mathbb{R}^{d_{SAE}}\)。
- 对比不同指令条件下的平均 SAE 特征向量，量化三类指标：
  - **L2 距离**：\(\| \bar{f}_{decep}(x_l) - \bar{f}_{truth}(x_l) \|_2\)
  - **余弦相似度**：两个平均特征向量的夹角余弦
  - **特征重叠率（Overlap Ratio）**：高于阈值 \(\epsilon = 10^{-6}\) 的活跃特征集合的 Jaccard 相似度
- 同时计算逐特征的激活差异，识别“**欺骗敏感特征**”。

**（5）可视化**
- 用 PCA 降维查看全局几何结构（用于模板化数据集展示）；
- 用欺骗敏感特征的二维散点图与小提琴图（violin plot）展示特定特征的激活分离模式。

## 3. 实验设计

### 3.1 模型
| 用途 | 模型 |
|---|---|
| 主机制分析 | Llama-3.1-8B-Instruct、Gemma-2-9B-Instruct（因其指令跟随能力好且有对应 SAE 套件） |
| 行为参考（输出层准确率评估） | 另覆盖 Llama-3.1-70B-IT、Gemma2-2B-IT、Mistral-7B-v0.3、Qwen2.5-7B/14B-Instruct（共 4 个 LLM 家族） |

### 3.2 数据集（Benchmark）
论文将数据划分为两个层次：

**(a) Curated Logical-Bench（人工模板数据集）**
- 主题模板集：cities（城市/国家）、sp_en_trans（西班牙语翻译）、element_symb（元素符号）、animal_class（动物分类）、inventors（发明者国籍）、facts（科学事实）
- **逻辑变体**：negated（否定）、conjunction（合取）、disjunction（析取）
- **数字比较**（Number）：larger_than、smaller_than

**(b) Open-Domain Fact-Bench（开放域自然数据）**
- **common_claim_true_false**：GPT-3 生成的常识性陈述（真/假二值标注，共 4450 条）
- **counterfact_true_false**：事实召回类陈述（含真实与虚假版本，共 ~31,960 条）

该划分的核心设计在于区分：**模板数据**（语法同质、词法噪声小）与**无筛选开放域数据**（主题多样、噪声大），以检验欺骗引发的变化是仅在简单可控环境下出现，还是在复杂、真实场景下依然稳健。

### 3.3 对比与评估框架
- **探针对比**：LR vs. TTPD（评估真值方向是否仅依赖表层特征）。
- **条件对比**：Truthful vs. Neutral vs. Deceptive（三种提示）。
- **几何方法对比**：PCA vs. SAE 特征分析。
- **泛化测试**：在 6 个训练主题（肯定+否定）上训练探针，在 14 个未见数据集（各主题额合取/析取变体 + 开放域数据集）上评估。
- 探针实验中还采用 leave-one-topic-pair-out 交叉验证避免词法记忆，并使用每层 z-score 标准化。

## 4. 资源与算力

论文**未明确报告**所用 GPU 型号、数量及训练/推理时长等具体算力信息。文中仅涉及对预训练模型的推理与探针/SAE 分析（无需重新训练大模型），从实验量级（两个模型 × 32 层 × 三种提示条件 × 多数据集）推断，计算开销主要来自激活提取与 SAE 前向传播。但对于具体的硬件配置和运行时间，作者没有在文末指明（该缺失也应在复现时加以注意）。

## 5. 实验数量与充分性

实验数量与维度较丰富，可概括为：
- **多层全扫描**：对两个模型的全部 32 层逐层进行探针与 SAE 指标分析。
- **行为基线**：表 1 报告了 4 个模型家族、7 个模型在 7 类数据集（肯定/否定/合取/析取/数字/两个开放域）× 3 种提示下的输出准确率，提供被广泛的行为证据。
- **探针泛化实验**：全面覆盖未见主题/逻辑结构/开放域数据，防御了词法记忆干扰。
- **多种几何度量交叉验证**：L2、余弦、重叠率三指标一致指向相同结论。
- **逐神经元可视化**：在 LLaMA 上展示了多个层（8/16/32）、两个数据集（common_claim、counterfact）的散点图与分布图。

总体评估：
- **优点**：实验设计具有较好的**层次感**——从行为→线性可解码性→全局几何→特征级翻转，逐步深入；且刻意在“简单/复杂”两类数据上同时验证，增强了结论的robustness。
- **不足**：主机制分析仅集中在两个模型（虽然行为数据扩展到更多模型）；没有针对探针的超参数敏感性进行消融；没有进行因果干预实验（如激活修补），因此结论主要是**相关性**而非严格的因果性。

## 6. 主要结论与发现

1. **输出的线性可解码性**：无论指令是诚实、中性还是欺骗，模型被指示的“True/False”输出始终可被线性探针从中间层激活中高精度解码。准确率峰值约在 Llama-3.1-8B 的第 14-16 层、Gemma-2-9B 的第 21 层左右，且层间曲线形态与指令条件无关。这表明模型在早中期就已完成事实判断的编码，“欺骗”更可能是在后续 token 选择阶段针对输出概率的调整，而非抹除事实内容。

2. **欺骗性指令引起显著的特征空间偏移**：基于 SAE 的分析显示，Deceptive vs. Truthful 的余弦相似度骤降、L2 距离骤升、特征重叠率下降，且偏移集中在**早期到中层**（LLaMA 的第 10-16 层、Gemma 的第 16-21 层区间）；相比之下 Truthful vs. Neutral 的偏移很小（相似度 >0.95），说明中性/诚实指令内部表示基本一致，欺骗指令是特异的扰动。

3. **这种特征级翻转在复杂开放域数据上依然存在**：尽管 PCA 在 open-domain 数据（common_claim、counterfact）上无法区分 True/False 类别（由于特征叠加与主题多样性干扰），SAE 指标却依然稳定地检测到 Deceptive vs. Truthful 的显著偏离。该发现强调了 SAE 相对全局线性降维方法的优势。

4. **识别出少量“欺骗相关”稀疏特征**：在每一层，少数（top-2 等）SAE 特征在真实与欺骗指令间呈现近二值激活模式——某个特征仅在诚实条件下激活、在欺骗下被抑制（或反之）。这些特征可被视作一个紧凑的“诚实/欺骗子空间”，为未来的欺骗检测与模型编辑提供了可操作的候选靶点。

5. **层特定模式**：真实-欺骗的最强分离点与探测准确率峰值所在层高度重合，暗示模型在中间层完成了“事实编码”与“指令驱动的输出翻转”之间的交互。

## 7. 优点

- **问题选择具有安全意义**：将可解释性工具直接用于 LLM 的安全漏洞——被指令诱导说谎——这一问题，超越了单纯的输出层评估。
- **方法组合得当**：线性探针（考察线性可解性）+ SAE（细粒度单义特征）+ 多指标几何度量（L2/余弦/Jaccard）构成一个多尺度分析体系，既能给出全局规律也可定位具体特征。
- **数据难度分层设计巧妙**：将模板数据与开放域的数据对比分析，证伪了“仅能在同质数据上观测到效应”的潜在质疑，大幅增强结论可信度。
- **探针泛化测试严谨**：使用留一主题对交叉验证、在未知逻辑形式与开放域数据集上评估，比仅报告同分布准确率更有说服力。
- **代码开源**：提供了完整的复现路径，提升可复现性。
- **清晰的“关键层”定位**：通过跨方法交叉验证的方式（探针峰值层 = PCA分离层 = SAE偏移最强层），令人信服地定位了欺骗处理的关键深度。

## 8. 不足与局限

**（1）因果性缺失**
- 论文只提供了**相关性证据**（表示在欺骗下发生偏移、某特征与欺骗相关），未进行激活修补（activation patching）、因果干预或模型编辑验证，无法确定这些特征是否**导致**了欺骗输出，而非仅仅是伴随现象。

**（2）范围受限**
- 仅针对**英文陈述句**和**二值事实判断**（True/False）任务，未推广到多语言、多模态或含分级真实度（graded truthfulness）的场景。
- 仅研究了**冻结权重**的模型，未分析 RLHF/安全训练过程中的表示变化。
- 欺骗场景由显式指令触发（“请撒谎”），与更隐蔽的现实操纵（如提示注入、思维链伪装、策略性欺骗）存在差距。

**（3）模型覆盖有限**
- 主机制分析（探针+SAE）仅在 Llama-3.1-8B 和 Gemma-2-9B 两个模型上运行，虽然行为表格覆盖到更多模型，但从“机制”层面的普遍性结论来说覆盖仍显不足。SAE 的可用性是这一限制的重要原因，作者也未讨论如何将分析扩展到无 SAE 套件的模型。

**（4）SAE 特征语义的近似性**
- 论文使用的是预训练 SAE 套件，特征解释依赖于各自训练数据和稀疏性目标，不同配置下特征含义可能漂移；论文也承认这一点，但没有进一步验证关键欺骗相关特征的稳健性（例如更换 SAE 宽度或训练 seed 后，识别的特征是否稳定）。

**（5）对“为什么”的回答仍较浅**
- 论文回答了欺骗性翻转**在何种条件下、哪些位置**发生，但未能阐明**上游的注意头/前馈网络如何通过指令 token 连锁触发这些特征变化**——即完整的因果回路仍未揭开。

**（6）算力信息披露不足**
- 未报告 GPU 型号、推理与分析时长，对复现的工程成本估计构成障碍。

**（7）对抗性测试缺失**
- 作者坦诚未测试对抗性提示重组（prompt recombinations）、后缀攻击等场景。欺骗指令被设计为显式且透明，因此论文对于实际越狱/隐蔽欺骗的防御启示仍需后续工作验证。

---

（完）
