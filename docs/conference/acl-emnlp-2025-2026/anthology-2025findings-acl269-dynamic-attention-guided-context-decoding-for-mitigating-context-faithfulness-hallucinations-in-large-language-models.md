---
title: Dynamic Attention-Guided Context Decoding for Mitigating Context Faithfulness Hallucinations in Large Language Models
title_zh: 动态注意力引导的上下文解码以缓解大语言模型上下文忠实性幻觉
authors: "Yanwen Huang, Yong Zhang, Ning Cheng, Zhitao Li, Shaojun Wang, Jing Xiao"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.269.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过注意力引导解码缓解上下文忠实性幻觉，提升对检索内容的忠实度
tldr: LLM常因上下文整合不完整而产生上下文忠实性幻觉。本文发现注意力机制编码了上下文利用信号，据此提出轻量级单遍解码框架DAGCD，利用注意力分布和不确定性信号引导生成。在开放域问答实验上，DAGCD显著提升忠实性和鲁棒性，为缓解幻觉提供高效方案。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 277, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1666, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1665, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1558, \"height\": 774, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1592, \"height\": 691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1588, \"height\": 1104, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1585, \"height\": 1161, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 774, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 770, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 817, \"height\": 682, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl269/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1634, \"height\": 1147, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl269/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 829, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl269/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 642, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl269/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 728, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl269/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl269/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1331, \"height\": 409, \"label\": \"Table\"}]"
motivation: LLM输出常偏离检索信息，上下文忠实性幻觉源于不完整的上下文整合。
method: DAGCD在单遍解码中结合注意力分布与不确定性信号来引导生成。
result: 在开放域QA上显著改善输出忠实性和鲁棒性。
conclusion: 注意力引导解码能有效缓解上下文忠实性幻觉。
---

## Abstract
Large language models (LLMs) often exhibit Context Faithfulness Hallucinations, where outputs deviate from retrieved information due to incomplete context integration. Our analysis reveals a strong correlation between token-level uncertainty and hallucinations. We hypothesize that attention mechanisms inherently encode context utilization signals, supported by probing analysis. Based on these insights, we propose Dynamic Attention-Guided Context Decoding (DAGCD) , a lightweight framework that leverages attention distributions and uncertainty signals in a single-pass decoding. Experiments on open-book QA datasets demonstrate DAGCD’s effectiveness, yielding significant improvements in faithfulness and robustness while preserving computational efficiency.

---

## 论文详细总结（自动生成）

# 动态注意力引导的上下文解码以缓解大语言模型上下文忠实性幻觉（DAGCD）——中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：大语言模型（LLMs）在依赖外部检索信息的场景（如检索增强生成 RAG）中，常出现“上下文忠实性幻觉”（Context Faithfulness Hallucinations），即模型输出偏离检索到的上下文，输出在字面上流畅但事实上与给定证据不一致。这类幻觉严重削弱了 RAG 系统的可靠性。
- **问题定位**：现有缓解方法（如 CAD、COIECD）通过对比“有无上下文”的概率分布，或引入不确定性信号来调整解码，但存在三大缺陷：
  - 可解释性有限；
  - 上下文相关与无关输出的差异较大时性能退化；
  - 需要多次解码（多趟前向），计算开销高。
- **核心发现（论文的实证基础）**：
  - 模型在生成错误答案时，token 级概率分布的归一化熵（NE）更高、最大软概率（MSP）更低（如错误答案平均 NE=0.36 vs 正确答案 0.29；MSP=0.25 vs 0.41），说明**不确定性幻觉强相关**；
  - 在错误回答中，66% 的情况下金标答案 token 位于概率分布的前 10 名之内，但并未被赋予最高概率，说明**模型其实“识别”了相关上下文，却未能有效优先化/整合它**；
  - 通过探针分析（逻辑回归 + 注意力比率特征）发现，**注意力机制本身内在地编码了“上下文利用”信号**，跨数据集、跨模型、跨提示词均能高精度识别被利用的上下文 token。
- **整体含义**：论文主张通过内在的注意力信号与不确定性信号，在解码过程中动态放大与上下文相关的 token，从而缓解上下文忠实性幻觉，且不引入额外解码开销——这就是 DAGCD 框架。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想
- DAGCD 借鉴 copy-generator（复制生成）机制，利用注意力分布估计“检索上下文中的哪些 token 正在被模型利用”，并结合 token 级不确定性信号动态调整生成概率，使输出更紧密对齐检索上下文。
- 整个过程**单遍解码**，无后处理或多趟前向，理论上保持贪婪解码的时间复杂度。

### 2.2 关键技术细节

#### (1) 上下文利用检测（Context Utilization Detection）
- 使用**逻辑回归（LR）分类器**作为轻量检测器，基于注意力比率特征：
  - 注意力比率 \( r_{j}^{l,h} = a_{j}^{l,h} / \sum_{j\in C} a_{j}^{l,h} \)，用于消除非上下文 token（如分隔符）的注意力汇（attention sink）噪声；
  - 通过分析 LR 系数，筛选出最重要的 **Top-K 注意力头**（实验取 K=10），并仅使用这些头的注意力比率作为特征向量 \( v_j^{(K)} \)。
- 在解码每一步收集当前最后一个 token 的注意力映射，过滤非上下文 token，输入检测器，得到被利用的上下文 token 集合。

#### (2) 利用分布构建（Utilization Distribution Construction）
- 对每个上下文 token j，计算利用分数：
  \[
  s_j = \sum_{k=1}^{K} (r_j^{h_k} \times w_k), \quad w_k = c_k / \sum_{k=1}^{K} c_k
  \]
  其中 \( c_k \) 是 LR 分类器中学到的注意力头权重，被分类为非利用的 token 的 \( s_j=0 \)；
- 归一化得到上下文上的概率分布 \( U = [u_1, ..., u_N] \)；
- **Top-Rank 约束（Top-Rank Constraint）**：仅保留生成分布中排名前 R（R=10）的 token 对应的利用分布 \( U_{\text{top}} \)，避免放大无关或荒谬的 token。

#### (3) 生成分布调整（Generating More Faithful Answers）
- 使用归一化熵 \( H_{\text{norm}}(P) \) 度量 token 级不确定性；
- 引入缩放因子 α（预训练模型 α=2，指令微调模型 α=4，需按模型调节）补偿熵的模型特异性差异；
- 调整公式：
  \[
  P' = P + \alpha H_{\text{norm}}(P) \cdot U_{\text{top}}
  \]
- 只有在 \( U_{\text{top}} \) 与原始概率分布中排名靠前的 token 有重叠时才进行调整，否则保持原始分布。

### 2.3 算法流程（文字描述）
1. 输入：检索上下文 C、问题 Q、当前解码步骤的注意力映射；
2. 根据 Top-K 注意力头与注意力比率构造每个上下文 token 的特征向量；
3. 用 LR 检测器判定哪些 token 被利用（s_j > 0）；
4. 计算利用分布 U，并施加 Top-Rank 约束得到 \( U_{\text{top}} \)；
5. 计算生成分布的归一化熵，乘上缩放因子 α；
6. 将 \( \alpha H_{\text{norm}}(P) \cdot U_{\text{top}} \) 加到原分布上，得到调整后的分布 \( P' \)；
7. 采样/取 argmax \( P' \) 生成下一个 token，重复直至停止。

## 3. 实验设计

### 3.1 数据集与 Benchmark
- **开放域 QA（主要基准）**：7 个数据集，统一使用 MrQA 规范格式：
  - 多跳推理：HotpotQA；
  - 长文检索问答：TriviaQA、SearchQA；
  - 单段落抽取：SQuAD、NewsQA；
  - 文档级问答：NQ；
  - 模拟冲突（对抗性）：NQ-Swap（实体替换制造上下文冲突）。
- **摘要任务（额外验证）**：CNN/DailyMail（随机抽样 500 条，评估 ROUGE-L、factKB、BERTScore）。

### 3.2 评估指标
- 主要指标：Exact Match（EM）与 F1；
- 摘要任务：ROUGE-L、factKB、BERTScore；
- 探针实验：分类精度 ACC 与 AUC。

### 3.3 对比方法
- Greedy Decoding（基线）；
- CAD（Context-Aware Decoding，α=1）；
- COIECD（Contextual Information-Entropy Constrained Decoding，λ=0.25，α=1）；
- 所有基线在相同设置下复现，均使用统一提示模板（Prompt 1）与贪婪解码。

### 3.4 模型
- LLaMA2-7B、LLaMA2-13B 及其 Chat 版本（共 4 个）；
- Mistral-7B、Mistral-7B-Instruct（共 2 个）；
- 覆盖不同模型家族、不同规模（7B/13B）、是否经过指令微调。

### 3.5 探测/分析实验
- 注意力利用率分类器跨域验证：6 个 MrQA 子数据集两两交叉验证；
- 训练数据量验证（100/200/300/500/1000 等）；
- 不同提示模板验证（4 种 prompt）；
- 特征重要性分析：Top-K 与 Bottom-K 特征、单头性能、弱头互补性；
- Spearman 相关性分析（不确定性 vs 回答准确率）。

## 4. 资源与算力

- 文中仅明确提到：“All models run on NVIDIA A100 GPUs.”
- **未说明** GPU 数量、具体型号（A100 40G/80G）、训练探针分类器所需时长、推理时间开销等细节。因此无法给出确切的算力总量或训练/推理时间。

## 5. 实验数量与充分性

### 5.1 实验数量
- 主对比实验：6 个模型 × 7 个数据集 × 4 种解码方法（Greedy、CAD、COIECD、DAGCD），每个单元格含 EM 和 F1，即至少 168 组数值；
- 消融实验 3 组（检测器训练数据量、Top-Rank 约束、缩放因子 α），另补充 Mistral 系列的 α 敏感性；
- 注意力信号分析实验：跨域验证、数据量验证、提示模板验证、特征 Top-K/Bottom-K、单头分布、弱头组合；
- 摘要任务附加实验：1 个数据集 × 2 个模型 × 4 种解码方法；
- 提示模板鲁棒性实验：2 个数据集 × 2 个模型 × 多 prompt。

### 5.2 充分性与公平性
- **较为充分**：覆盖了不同模型（LLaMA/Mistral）、不同规模（7B/13B）、不同调校（base/chat/instruct）、不同任务类型（多跳、长文、单段、文档级、对抗），评估指标全面（EM/F1，以及摘要的三项指标）；
- **公平性较好**：所有基线在相同设置下复现，使用统一提示模板；NQ-Swap 用于测试鲁棒性；
- **存在局限**：主要验证集中在 QA，摘要仅作为辅助；未与其他较新的方法（如 Lookback Lens、ADACAD）进行直接对比；注意力检测器训练数据来自 MrQA，可能偏向该数据分布。

## 6. 主要结论与发现

- **不确定性幻觉相关**：token 级归一化熵与回答准确率显著负相关（Spearman 相关系数在含上下文时最高为 -0.53），上下文忠实性幻觉伴随更高的不确定性与更低的置信度。
- **模型并非完全忽略上下文**：错误回答中金标 token 常排在前 10，但未被优先选择；平均概率差距较小（排名 2–4 时仅 0.14），说明上下文整合不完整。
- **注意力编码上下文利用信号**：LR 探针分类器跨数据集平均 AUC>0.99；仅 100 个训练样本时 AUC 仍 >0.96；交叉提示模板下 ACC>0.97、AUC>0.99。
- **DAGCD 有效性**：
  - 在预训练模型上平均 EM 提升 17.67%；
  - 在指令微调模型上平均 EM 提升 2.25%；
  - Mistral-7B 上提升最明显：HotpotQA EM +18.80%、NQ EM +71.46%、NQ-Swap EM +74.52%；
  - 摘要任务上 ROUGE-L、factKB、BERTScore 均有提升（如 LLaMA2-7B-Chat ROUGE-L 0.2368→0.2426）。
- **鲁棒性与可扩展性**：对训练数据量不敏感（100 样本即可）、对 prompt 变化稳健、在对抗性 NQ-Swap 上表现突出。
- **效率**：单遍解码，理论复杂度与贪婪解码相同，同时具有可解释性（LR 系数对应注意力头重要性）。

## 7. 优点

- **轻量高效**：不依赖多遍解码或额外对比生成，适合实时推理场景；
- **可解释性强**：通过注意力头权重量化“上下文利用”程度，直观明晰；
- **内驱信号**：从模型内部注意力入手，而非外部启发式规则，具有机制性依据；
- **数据效率**：检测器仅需少量训练样本（100 条）即可跨域泛化，实用价值高；
- **分析充分**：对注意力头的“集中性”和“互补性”进行了详细剖析，为后续研究提供新的视角；
- **实验规模大**：在 6 个模型、7 个 QA 数据集上验证，并补充了对抗性场景、摘要任务、多种消融和 prompt 鲁棒性测试。

## 8. 不足与局限

- **对分类器准确性敏感**：在超长上下文、复杂多轮对话、含干扰噪声的场景中，注意力比率分类器可能误判，导致错误放大或关键 token 被抑制；对抗性/噪声输入的鲁棒性尚未充分验证；
- **缩放因子需要经验调优**：α 依模型（预训练 vs 指令微调）而异，需人工校准，未建立熵与不确定性的精确数量关系，可能增加部署成本；
- **任务覆盖有限**：主要聚焦开放域 QA，对对话生成、长文档摘要等其他输出结构复杂的任务研究不足；注意力分类器可能需针对新任务重新训练或改进；
- **算力信息缺失**：未报告 GPU 数量、训练时间、推理耗时对比，难以精确评估其相对计算成本；
- **基线对比不够全面**：未与 Lookback Lens、ADACAD 等最新方法直接比较，也未报告置信区间或方差分析；
- **评估指标以 EM/F1 为主**，对答案语义多样性（如同一正确答案不同表述）可能不够公允。

（完）
