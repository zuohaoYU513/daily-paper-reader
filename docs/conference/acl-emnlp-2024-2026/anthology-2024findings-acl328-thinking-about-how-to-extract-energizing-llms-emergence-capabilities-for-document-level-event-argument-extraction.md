---
title: "Thinking about how to extract: Energizing LLMs’ emergence capabilities for document-level event argument extraction"
title_zh: 思考如何抽取：激发大语言模型在文档级事件论元抽取中的涌现能力
authors: "Kai Shuang, Ji Zhou, Qiwei Wang, Jinyu Guo"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.328.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 面向文档级事件论元抽取，缓解长文档关键特征遗忘与跨事件论元混淆
tldr: 文档级事件论元抽取存在关键特征遗忘和跨事件论元混淆两大难题。论文提出EAESR，利用大语言模型的涌现能力生成引导式摘要，以压缩长事件上下文并保留关键事件特征，再通过推理厘清多个事件之间显式和隐式的联系。实验显示该方法能有效改善文档级长文本事件论元抽取，说明引导式摘要与推理可以互补。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl328/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 780, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl328/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl328/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 726, \"height\": 714, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl328/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 735, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl328/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 752, \"height\": 272, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1161, \"height\": 769, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1136, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl328/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1448, \"height\": 1532, \"label\": \"Table\"}]"
motivation: 文档级事件论元抽取面临长文档关键特征遗忘和跨事件论元混淆两大挑战。
method: 提出EAESR方法，用LLM生成摘要压缩事件上下文，并借助推理澄清事件间的显式与隐式关联。
result: 实验表明该方法可明显减轻关键信息丢失与跨事件混淆，提升文档级论元抽取性能。
conclusion: 引导式摘要结合推理能够激发大模型在长文档事件抽取上的涌现能力。
---

## Abstract
There are two key challenges remaining for the document-level event argument extraction (D-EAE) tasks: key feature forgetting and cross-event argument confusion. The emergence capability of large language models (LLMs) holds promise for solving the above two challenges. In this paper, we propose a document-level event argument extraction method based on guided summarization and reasoning (EAESR), which leverages the emergence capabilities of LLMs to highlight key event information and to clarify the explicit and implicit association between multiple events. Specifically, we generate document summarization information that shorten the length of the event context while preserving the key event features. In addition, we generate inter-event reasoning information, which helps EAESR make sense of the correlations between events and reduces their dependence on the event context, especially to better cope with the few-shot D-EAE task. Then, we obtain named entity information to enable EAESR to learn argument boundary features to improve the sensitivity of its argument boundary recognition. Eventually, we fused the above features and sentence features to make EAESR have summarizing and reasoning capabilities simultaneously. Extensive experiments on WIKIEVENTS and RAMS have shown that EAESR achieves a new state-of-the-art that outperforms the baseline models by 1.3% F1 and 1.6% F1, respectively, and averages 11% F1 in few-shot settings.

---

## 论文详细总结（自动生成）

## 摘要
> 本文提出 EAESR（Event Argument Extraction based on guided Summarization and Reasoning），一种面向文档级事件论元抽取（D-EAE）的新方法。其核心思路是利用大型语言模型（LLMs）的涌现能力，生成引导式摘要和事件间推理信息，以缓解长文档中“关键特征遗忘”和“跨事件论元混淆”两大挑战，并在 RAMS 和 WIKIEVENTS 基准上取得新的 SOTA 结果。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务背景**：文档级事件论元抽取（D-EAE），即给定文档、触发词和事件类型，抽取出每个事件对应的论元角色及其文本跨度。相比句子级 EAE，D-EAE 需要考虑跨句信息，更具挑战性。

- **核心问题 1：关键特征遗忘（Key Feature Forgetting）**
  - 若将整个文档直接编码，大量与事件无关的信息会干扰事件特征建模；
  - 若使用固定窗口只编码部分文本，又会丢失窗口之外的论元信息；
  - 因此模型难以在“保留全局信息”和“过滤无关信息”之间取得平衡。

- **核心问题 2：跨事件论元混淆（Cross-event Argument Confusion）**
  - 文档中多个事件可能共享显式论元（如同一时间、地点），也可能存在需要推理的隐式关联（如“第二天”指代前文某一天）；
  - 现有基于图或序列的模型容易识别显式共现关联，却难以推理隐式关联，导致把事件 A 的论元错误地归到事件 B 上。

- **研究动机**：LLM 虽然不适合直接生成论元（幻觉会导致输出超出原文的论元），但其涌现能力——尤其是摘要和推理能力——可以作为一种“外挂辅助”而非“抽取器”，帮助传统模型更好地建模事件结构。

- **整体含义**：提出一种“LLM 引导 + 判别式抽取”的新范式：**用 LLM 压缩和推理事件文本，用传统神经网络做精确论元边界识别**，兼顾两方优势。

## 2. 论文提出的方法论

- **核心思想**：不是让 LLM 直接输出论元，而是利用 LLM 生成三类外部辅助信息：
  1. 文档摘要信息（Summarization）：压缩上下文长度并保留关键事件特征；
  2. 事件推理信息（Reasoning）：逐步分析事件间的显式/隐式关联；
  3. 实体信息（Entity）：识别句子中的命名实体，约束论元边界。

- **方法名称**：EAESR（document-level Event Argument Extraction based on guided Summarization and Reasoning）

- **整体框架**：三个核心模块 + 一个融合抽取模块，整体流程如下：
  
  1. **Summarizing feature extraction（摘要特征提取）**
     - 设计摘要 Prompt（SP），输入事件类型 + 长度限制 + 原文给 ChatGPT，生成文档摘要；
     - 对摘要使用 AMR（Abstract Meaning Representation）解析器生成语义图，将边类型聚类为 8 大类别（空间、时间、方式、修饰、算子、介词、核心角色、其他），构成异质图；
     - 使用 3 层 GCN 在异质图上学习图中节点（token）之间的交互权重，得到全局特征 \(f_g\)。
  
  2. **Reasoning feature extraction（推理特征提取）**
     - 设计推理 Prompt（RP），让 LLM 逐步分析事件论元的关联和推理步骤，得到推理信息 \(F_r\)；
     - 设计实体抽取 Prompt（EP），让 LLM 抽取句子中的实体，得到实体信息 \(F_e\)；
     - 使用 BERT 分别编码 \(F_r\)、\(F_e\)，得到推理特征 \(f_r\) 和实体特征 \(f_e\)。
  
  3. **Event argument extraction（事件论元抽取与特征融合）**
     - 用 BERT 编码原句得到句子特征 \(f_s\)；
     - **Attention fusion layer**：利用类层归一化结构分别融合：
       - 句子特征 + 全局特征 → \(F^{g}_{cln}\)（用于缓解关键特征遗忘）；
       - 句子特征 + 推理特征 → \(F^{r}_{cln}\)（用于缓解跨事件论元混淆）；
     - 随后用多头自注意力机制级联融合各特征（实体特征作为 V 参与注意力，直接作用于边界识别）：
       - \(F^{s}_{sa} = SA(F^{g}_{cln}, f_s, f_e)\)
       - \(F^{rg}_{sa} = SA(F^{s}_{sa}, F^{r}_{cln}, f_e)\)
     - 引入残差连接 + LayerNorm + GeLU 得到最终融合特征 H；
     - 论元边界预测：将任务建模为起始/结束位置预测的 span 抽取，用两个二元交叉熵损失共同训练。

- **公式要点**：
  - GCN 更新：\( h_u^{(l+1)} = \sigma(\sum_{k \in K} \sum_{v \in N_k(u) \cup \{u\}} \frac{1}{c_{u,k}} W_k^{(l)} h_v^{(l)}) \)
  - 特征融合采用类似 FiLM 的特征调制方式：
    \( F_{cln} = \gamma \cdot \frac{f - mean(f)}{std(f)} + \beta \)
  - 最后采用 Sigmoid + 二元交叉熵计算 start/end 位置概率。

## 3. 实验设计

- **数据集**：
  - RAMS：139 种事件类型、65 种论元角色，平均文档长度约 134 词（短文档）；
  - WIKIEVENTS：50 种事件类型、59 种论元角色，平均文档长度约 789 词（长文档）；
  - 两个数据集均覆盖论元跨句的 D-EAE 场景。

- **评价指标**：
  - **Arg-I（Argument Identification F1）**：仅要求预测论元跨度与真实标签匹配；
  - **Arg-C（Argument Classification F1）**：要求论元跨度与角色类型同时匹配（更严格的主指标）。

- **对比方法**（共 12 种基线，涵盖三大类）：
  1. **Span 边界预测**：FEAE、BERT-CRF、TSAR（AMR增强）；
  2. **QA/MRC 模型**：EEQA、EEQA-BART、DocMRC；
  3. **生成式模型**：BART-Gen、PAIE、UnifiedEAE、Memory-DocIE、APE、RA-DocEAE。
  - 此外还对比了直接使用 LLM（GPT3.5、ChatGLM2-6B）做 EAE 的效果。

- **实验设置**：
  - 所有模型的 PLM 均使用 base 版本（BERT-base / BART-base 等）；
  - 优化器：AdamW；学习率 1e-5；batch size 2；训练 30 epochs；warmup 0.1；
  - 跨数据集预训练设置：在 RAMS 上训练时加载 WIKIEVENTS 的 BERT 参数，反之亦然（利用数据集间的重叠知识）。

## 4. 资源与算力

- 论文在正文实现细节中提到：使用 **NVIDIA A40（48GB）GPU** 训练模型；
- 在 Limitations 中明确提到：用 LLM 为 WIKIEVENTS 生成摘要、推理和实体辅助信息约耗时 **30 小时（单卡 A40）**；
- 但关于训练多少张 GPU、并行策略、单次训练的 GPU 时数等未给出具体说明，因此算力总消耗不完全透明。

## 5. 实验数量与充分性

- **实验组数（从正文可得的共 6 组）**：
  1. 主实验：RAMS 和 WIKIEVENTS 上全量数据对比 12 个基线；
  2. LLM 直接抽取 vs. EAESR 对比实验（GPT3.5 和 ChatGLM2-6B）：
  3. 消融实验（移除 \(f_g\)/\(f_r\)/\(f_e\)）：
  4. few-shot 实验（RAMS 上 10/50/100/200 样本）：
  5. 提示词的影响分析（带事件信息 vs. 不带事件信息）：
  6. 案例研究（case study，2 个典型示例）。
  - 此外还包括附录中的幻觉与过抽取错误统计分析（ChatGLM2-6B vs EAESR）。

- **充分性分析**：
  - 覆盖较为系统，同时包含全量、少样本、消融和案例分析，论证链条完整；
  - 从**实验设计的绝对数量**来看，约 6 组实验不算多，但每组实验的对照设计较严整；
  - 公平性方面整体较好：所有基线 PLM 均统一使用 base 版本；统一了数据集和评估脚本；
  - 但仍存在部分风险：
    - 少样本实验只在 RAMS 上做，未在长文档 WIKIEVENTS 上验证；
    - 消融实验中各模块的 F1 波动其实不大（如在 RAMS 上移除全局特征仅降 0.3% Arg-C），对结论的支撑力有一定局限；
    - 案例分析为人工挑选，样本数量少，难以完全消除选择性偏差。

## 6. 论文的主要结论

- 主实验结论：EAESR 在 RAMS 与 WIKIEVENTS 上均取得最优结果：
  - RAMS：Arg-I 60.2、Arg-C 53.2，较第二名 APE 提高 1.6% F1；
  - WIKIEVENTS：Arg-I 71.3、Arg-C 67.6，较第二名 TSAR 提高 1.3% F1；
- 消融研究结论：三个外部特征（全局、推理、实体）均有效，其中推理特征对 RAMS 和 WIKIEVENTS 的增益一致且与文档长度无关；
- 少样本结论：EAESR 在 RAMS 的 few-shot 场景下，用 10 个样本即超过 APE 用 200 个样本的效果；在 10/50/100/200 训练样本下平均提升约 11% F1；
- LLM 对比结论：直接使用 GPT3.5/ChatGLM2-6B 做 EAE 效果远差于 EAESR（其中幻觉是主要原因之一），说明 **LLM 适合做辅助推理而不适合直接生成论元**；
- 从学习目标来看，将“学习事件特征”转变为“学习事件推理特征”可有效降低对大规模标注数据的依赖。

## 7. 优点与创新点

- **架构设计新颖**：将 LLM 从“端到端抽取器”降级为“外部辅助特征生成器”，扬长避短：
  - 用 LLM 的摘要能力解决长文档编码冗长问题；
  - 用 LLM 的推理能力建模跨事件隐式关联；
  - 用 BERT/GCN 承担精确的论元边界预测任务。
- **学习目标的转变**：由“事件特征学习”转为“事件推理特征学习”，显著提高了少样本学习能力；
- **三种特征有明确分工**：
  - 全局特征（摘要+AMR+GCN）→ 解决关键特征遗忘；
  - 推理特征（逐步推理）→ 解决跨事件论元混淆；
  - 实体特征 → 提高论元边界预测准确性；
- 在两个不同长度的数据集（短文本 RAMS、长文本 WIKIEVENTS）上均有明显增益，说明方法具有跨场景适应性；
- 对 LLM 幻觉问题做了定量统计（如解析错误 1.70%、幻觉 15.23% 导致的精度损失），分析较严谨。

## 8. 不足与局限

- **计算开销大**：使用 ChatGPT 生成辅助信息成本较高，WIKIEVENTS 需约 30 小时（单张 A40），且依赖外部 API 调用，部署与复现门槛较高；
- **误差级联**：EAESR 依赖 AMR parser 的输出质量，AMR 图的误差会传播到后续 GCN 编码模块，可能降低模型的鲁棒性；
- **消融实验增益有限**：在 RAMS 上移除全局/实体特征的 F1 差异较小，有一些统计显著性不足的风险；
- **少样本泛化验证不足**：few-shot 实验仅基于 RAMS，未在文档更长的 WIKIEVENTS 上复现，泛化结论有待加强；
- **外部依赖强**：摘要和推理信息的质量完全取决于 LLM 的指令跟随能力，论文在 ChatGPT/GPT-3.5 之外缺少更多 LLM 后端（如开源模型的变体）的敏感度分析；
- **幻觉问题只是减轻而非根除**：虽然 EAESR 避免了 LLM 直接生成论元的幻觉，但 LLM 在摘要和推理产物本身仍有臆造信息的可能；
- **实验数量有待扩充**：仅两个数据集（RAMS、WIKIEVENTS），未在其他语种或领域（如生物医学、金融）的文档数据集上验证。

（完）
