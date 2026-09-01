---
title: "TPA: Next Token Probability Attribution for Detecting Hallucinations in RAG"
title_zh: TPA：用于检测RAG中幻觉的下一词元概率归因
authors: "Pengqian Lu, Jie Lu, Anjin Liu, Guangquan Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1159.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 将下一词元概率归因到七个来源以检测RAG幻觉
tldr: 现有RAG幻觉检测方法常将幻觉归因于内部知识与检索上下文的二元冲突，忽视查询、先前词元等组件影响。本文提出TPA，将每个词元的概率系统地归因到查询、RAG上下文、先前词元等七个来源，量化各组件对生成结果的贡献。该归因方法能更完整地捕捉幻觉成因，提升检测准确性，为理解LLM生成机制提供了细粒度分析工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 1294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1648, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1159/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1646, \"height\": 631, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1675, \"height\": 1239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 747, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 753, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1159/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1626, \"height\": 1983, \"label\": \"Table\"}]"
motivation: 现有RAG幻觉检测仅考虑内部知识与检索上下文的二元冲突，因而不完整。
method: 提出TPA将每个词元概率归因到查询、RAG上下文、历史词元等七个来源，量化各自贡献。
result: 更全面地捕捉幻觉成因，提升了RAG场景下的幻觉检测性能。
conclusion: 为RAG幻觉检测提供细粒度的概率归因新方法。
---

## Abstract
Detecting hallucinations in Retrieval-Augmented Generation remains a challenge. Prior approaches attribute hallucinations to a binary conflict between internal knowledge stored in FFNs and the retrieved context. However, this perspective is incomplete, failing to account for the impact of other components of the LLM, such as the user query, previously generated tokens, the self token, and the final LayerNorm adjustment. To comprehensively capture the impact of these components on hallucination detection, we propose TPA which mathematically attributes each token’s probability to seven distinct sources: Query, RAG Context, Past Token, Self Token, FFN, Final LayerNorm, and Initial Embedding. This attribution quantifies how each source contributes to the generation of the next token. Specifically, we aggregate these attribution scores by Part-of-Speech (POS) tags to quantify the contribution of each model component to the generation of specific linguistic categories within a response. By leveraging these patterns, such as detecting anomalies where Nouns rely heavily on LayerNorm, TPA effectively identifies hallucinated responses. Extensive experiments show that TPA achieves state-of-the-art performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

检索增强生成（Retrieval-Augmented Generation, RAG）通过在生成时引入外部检索证据来缓解大语言模型的幻觉问题，但RAG系统本身仍可能产生幻觉，例如忽略或曲解检索到的信息。在高风险场景（如临床决策支持、法律研究助手、自主智能体）中，幻觉的后果尤为严重。

现有主流幻觉检测方法存在以下问题：
- **基于不确定性或一致性的代理度量**（如语义熵、自一致性检查）只能测量幻觉的“症状”（如输出方差、表层置信度），而非潜在的结构性成因，因此在模型“自信但错误”时常常失效。
- **基于内部机制的检测方法**（如ReDeEP）假设幻觉源于 FFN 中存储的参数化知识与检索上下文之间的二元冲突。但这一视角**不完整**，它忽略了LLM其他组件的影响，如用户查询、先前生成的词元、当前词元本身（Self Token）以及最终 LayerNorm 的调整。

论文的核心主张是：仅关注 FFN 与 RAG 之间的二元冲突不足以全面解释 RAG 幻觉的成因，需要将生成概率分解到所有源头上，以捕捉完整的内部机制。为此，作者提出了 **TPA（Next Token Probability Attribution）** 框架，将生成下一词元的概率精确归因到七个不同来源，从而为幻觉检测提供细粒度的、机制层面的特征依据。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 2.1 总体框架

TPA 采用三阶段流水线，可通过**单次完全并行的 teacher-forced 前向传播**实现，同时提取所有位置的隐藏状态和注意力图，无需自回归重采样。

### 2.2 粗粒度分解（Coarse-Grained Decomposition）

基于 Transformer 的残差流加性结构，利用**探针函数**（Probe Function）Φ(h, y) = [Softmax(hW_U)]_y（类似于 logit lens），将最终词元概率精确分解为：

- **ΔP_initial**：初始嵌入（Initial Embedding）的基线贡献
- **ΔP_att^(l)**：每一层注意力块的贡献
- **ΔP_ffn^(l)**：每一层 FFN 块的贡献
- **ΔP_LN**：最终 LayerNorm 的调整量

**Theorem 1（完备概率分解）**：最终概率恰等于初始嵌入贡献、所有层 Attention 与 FFN 贡献之和、以及最终 LayerNorm 调整量之和（残差流的 telescoping 级数性质保证精确成立）。

### 2.3 细粒度归因（Fine-Grained Attribution）

由于 Softmax 的非线性，无法直接通过逐头探测获得注意力的头部贡献，作者将分解转移到 **logit 空间**：
- 计算每个注意力头对目标词元 logit 的标量贡献：Δz_h,y = (o_h W_O^(l,h)) · w_U,y
- 通过一阶泰勒展开（Proposition 1）建立 logit 贡献与概率贡献的线性关系，并用 **Softmax 归一化的对数贡献权重**（式 11）将注意力块的总概率贡献按比例分配给各注意力头，既保证数值稳定性，又保持逐层归因总量守恒。

### 2.4 上游源映射与七源拆分

将因果注意力范围 [1, n_t] 划分为四个不相交且完备的索引集合：
- **IQry**（查询词元）
- **IRAG**（检索上下文词元）
- **IPast**（先前生成的词元）
- **ISelf**（当前位置词元本身）

结合注意力权重将每个头的贡献映射到这四个源，最终形成七个归因源：Query、RAG、Past、Self、FFN、Final LayerNorm、Initial Embedding。七源得分之和精确等于词元的最终输出概率。

### 2.5 语法感知特征工程（Syntax-Aware Feature Engineering）

原始词元级归因分数缺乏上下文语义：FFN 贡献高对“the”“of”等虚词是正常的，但对命名实体则可疑。TPA 使用 **SpaCy 的 POS 标注**对归因分数进行聚合：
- **Tag 传播策略**：将子词词元继承其父词的 POS 标签，解决 LLM 分词粒度与 POS tagger 词级粒度不匹配的问题。
- **聚合方式**：对每个 POS 类别计算七源归因的均值向量，拼接得到 7×18=126 维特征向量（18 个通用 POS 标签）。

这使检测器能够识别特定词性类别上的异常归因模式（如名词过度依赖 LayerNorm、数字词元上 RAG 贡献过低），同时忽略良性的语法模式。

## 3. 实验设计：数据集、Benchmark 与对比方法

### 3.1 数据集

- **RAGTruth**：包含 Llama2-7B、Llama2-13B、Llama3-8B 和 Mistral-7B 的响应，另新增 Qwen3-8B 生成数据。
- **Dolly (AC)**：包含 Llama2-7B/13B、Llama3-8B 的响应（规模较小，N=100）。

### 3.2 基准与评估协议

- 幻觉检测被建模为**有监督二分类任务**；分类器为 5 个不同随机种子的 XGBoost 集成。
- 评估指标：AUC、Recall、F1。
- 三种评估协议：
  - **Protocol I**：标准划分（RAGTruth Llama2-7B/13B、Mistral），Optuna 自动调参 + 5 折交叉验证 + 85/15 内部划分 + Early Stopping。
  - **Protocol II**：分层 20 折交叉验证（RAGTruth Llama3-8B，因无官方训练/测试划分）。
  - **Protocol III**：嵌套留一交叉验证（Dolly，N=100，外层 LOO + 内层 Optuna 调参）。
- 每次实验用 5 个外层随机种子重复，显著性检验采用单样本 t 检验（p<0.05）。

### 3.3 对比基线（三个类别）

1. **不确定性/代理度量**：SelfCheckGPT、Perplexity、LN-Entropy、Energy、Focus、P(True)、EigenScore/INSIDE、SEP。
2. **基于 LLM 的评估**：RAGTruth Prompt、ChainPoll、RAGAS、Trulens、RefCheck。
3. **内部激活探测/机制分析**：SAPLMA、ITI、ReDeEP、TSV、Novo。

## 4. 资源与算力

论文在附录中明确说明了计算资源：
- **硬件**：单张 NVIDIA A100 (40GB) GPU，200GB RAM；CUDA 12.8，Python 3.10，PyTorch 2.x，HuggingFace Transformers 4.56.1。
- **实现方式**：因 40GB 显存限制，采用**顺序 prefix-replay（逐词元）**实现而非并行 teacher-forced；作者强调两者数学等价（利用因果掩码机制），不影响归因值。
- **运行时间**：
  - 特征提取：每个响应约 20 秒（顺序实现）；
  - 总成本：每个数据集/每个模型约 17 GPU-hours（数据集少于 3000 个样本）；
  - 分类器推理：每个响应低于 1 秒，总分类成本仅数个 CPU-hours。
- **复杂度分析**（附录 E 给出完整推导）：总复杂度为 O(L·T·|V|·d + L·T·d² + L·H·T²)，分别对应概率分解、头部归因、源映射三个阶段。

## 5. 实验数量与充分性分析

### 5.1 实验数量

- **主实验**：RAGTruth 上 4 个模型（Llama2-7B/13B、Llama3-8B、Mistral-7B）+ Dolly 上 3 个模型（Llama2-7B/13B、Llama3-8B）+ 新增 Qwen3-8B，共 8 个 backbone-dataset 设置。
- **消融研究**：
  - 七个归因源逐一剔除实验（在 RAGTruth 的 4 个模型上）；
  - 三种特征聚合策略对比（TPA-POS vs. TPA-Mean vs. TPA-Stat，覆盖 7 个设置）。
- **可解释性分析**：SHAP 特征重要性分析（覆盖 Llama2-7B、Llama2-13B、Llama3-8B、Mistral-7B 四个模型）。
- 每个实验均重复 5 个种子，报告均值和标准差，并附 t 检验 p 值。

### 5.2 充分性与公平性评估

**充分性较强的方面：**
- 模型覆盖范围广：涵盖 LLaMA 系列、Mistral（滑动窗口注意力）、Qwen3 等多种架构，验证了跨架构泛化性。
- 统计严谨性：5 种子重复、显著性检验、严格数据隔离（防止泄漏）、针对小数据集的嵌套 LOO 协议。
- 在 Mistral 和 Qwen3 上部分基线（如 ReDeEP、SEP、ITI）因缺乏相应检查点/头部选择而无法公平运行，论文对此做出了明确交代，比较范围合理。

**存在的不足：**
- Dolly 数据集 N=100，规模过小；论文也承认在 Dolly 上消融实验不稳定，故未进行细粒度消融，这限制了跨数据集验证的完整性。
- LLM-as-judge（Claude Opus 4.6）用于 Qwen3 标注，虽然在 RAGTruth 人工标注集上验证（0.82 准确率、0.83 F1、0.64 Cohen's κ），但仍存在额外验证成本与自动标注可能引入的偏差。

## 6. 论文的主要结论与发现

1. **TPA 达到 SOTA 性能**：在 RAGTruth 的 Llama2-7B/13B 上取得统计显著的 Rank-1 AUC 和 F1；在 Mistral-7B 上 F1 达 0.8702，超过最强基线 Novo 约 7%；在 Qwen3-8B 上 F1/AUC/Recall 全面超越 TSV 和 Novo。在 Dolly 上随模型能力增大表现增强，在 Llama2-13B 和 Llama3-8B 上取得 Rank-1。
2. **细粒度归因是必要的**：SHAP 分析显示，分类器频繁依赖超出 FFN-RAG 二元冲突的特征（如 LN_NUM 在 Llama2-7B 上是关键信号），证实仅用 FFN-RAG 冲突不足以稳健检测幻觉。
3. **语法聚合捕捉模型特异的“接地逻辑”**：Llama2 和 Mistral 依赖 RAG_NOUN，而 Llama3-8B 更依赖 RAG_ADP（介词等关系结构）；POS 聚合对于捕捉这些差异至关重要。
4. **幻觉的“指纹”因架构而异**：例如 LN_NUM 高归因在 Llama2-7B 上是幻觉信号，但在 Llama2-13B 上方向反转（高归因反而对应事实正确），说明幻觉信号并非通用，需要可学习的方法而非静态启发式。

## 7. 优点

- **完整的机理解释**：TPA 首次将词元概率完备地分解为七个来源，精确满足守恒原则（分解之和恰等于最终概率），在机制层面覆盖了此前方法忽略的组件（LayerNorm、Query、Self Token 等）。
- **理论严谨性**：提供了定理 1 的精确证明和 Proposition 1 的泰勒展开推导；Softmax 归一化的权重分配保证数值稳定性与总量守恒。
- **语法感知的检测特征**：利用 POS 聚合解决“同源不同义”的歧义问题（同一归因模式对虚词正常、对实体可疑），是一个巧妙的特征工程设计。
- **跨架构泛化能力**：在 Llama、Mistral、Qwen3 等多种架构上均取得最佳或接近最佳效果，远超仅针对 LLaMA 架构设计的基线。
- **透明的可解释性**：通过 SHAP 自动揭示新的机制性信号（如 LayerNorm 的异常贡献），超越了传统的 FFN-RAG 二元冲突视角，为后续研究提供了新方向。
- **实验严谨**：多种子、显著性检验、严格防泄漏、针对小数据量的嵌套 LOO 协议，并完整报告标准差与 p 值。

## 8. 不足与局限

- **白盒访问需求**：TPA 要求访问模型内部残差流状态、注意力权重、嵌入矩阵等，无法应用于闭源 API 模型。
- **计算开销较高**：相比简单标量探测（如 SEP、Novo），TPA 的特征提取开销明显更大（每响应约 20 秒，每数据集约 17 GPU-hours），论文虽给出了复杂度上限对比，但未提供与其他基线在同等硬件下的直接运行时间对比。
- **依赖外部语言学工具**：POS 标注依赖 SpaCy，在代码生成、科学文本等专业领域泛化受限；多语言场景也需额外适配（如多语言 SpaCy 或 AST 节点类型），论文已将其列为未来工作。
- **小数据集上的表现不稳定**：Dolly 上 Llama2-7B 效果不及 ReDeEP（虽然这与数据规模小、协议严格有关）；论文也承认 Dolly 样本量过小导致无法进行完整的消融验证。
- **Mistral 和 Qwen3 上基线比较不完整**：部分基线（如 ReDeEP、SEP、ITI）由于未提供相应模型检查点而无法参与比较，可能使对比的“全面性”略显不足。
- **Qwen3 标注依赖 LLM-as-judge**：虽然通过人工标注验证，但 judge 本身存在偏差可能；另外 Qwen3 响应是论文自行生成而非原始 RAGTruth 标注，评估范式与其他模型（使用官方标注）不完全一致。
- **缺乏端到端效率优化**：虽然理论上可并行实现，实际因显存限制采用顺序执行，也尚未将 POS 聚合扩展到短语/片段级别以进一步提升效率。

（完）
