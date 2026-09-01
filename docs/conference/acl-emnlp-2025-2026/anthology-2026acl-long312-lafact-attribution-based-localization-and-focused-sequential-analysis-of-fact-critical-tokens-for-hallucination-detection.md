---
title: "LAFaCT: Attribution-based Localization and Focused Sequential Analysis of Fact-Critical Tokens for Hallucination Detection"
title_zh: LAFaCT：基于归因定位与事实关键令牌聚焦序列分析实现幻觉检测
authors: "Xin Wang, Jiahao Li, Licheng Zhang, Zhendong Mao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.312.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过事实关键令牌定位进行白盒幻觉检测
tldr: 现有白盒幻觉检测方法依赖隐藏状态，但未聚焦事实关键令牌。论文提出LAFaCT框架，先利用基于特征归因的事实关键性指标定位事实关键令牌，再对这些令牌的隐藏状态进行聚焦序列分析。在八个基准和多个模型族上的实验表明，该方法达到新的最优幻觉检测性能，并验证了各模块的有效性。该框架将定位与分析解耦，为后续可解释幻觉检测提供了新范式。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1628, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 730, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 280, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 791, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long312/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 785, \"height\": 566, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 1548, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1689, \"height\": 1298, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1419, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 814, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 775, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 778, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 575, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 811, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 814, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long312/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1655, \"height\": 623, \"label\": \"Table\"}]"
motivation: 白盒幻觉检测方法虽用隐藏状态，却缺乏对事实关键令牌的聚焦，导致检测精度受限。
method: 提出LAFaCT两阶段框架，用特征归因指标Factual Criticality定位事实关键令牌，再做聚焦序列分析。
result: 在八个基准和多个模型族上取得幻觉检测新最先进结果，模块分析验证了方法的有效性。
conclusion: 先定位后分析的策略能显著提升大模型幻觉检测的准确率与可解释性。
---

## Abstract
Large Language Models (LLMs) suffer from hallucinations, severely undermining their reliability. While white-box hallucination detection methods that leverage hidden states prevail, they fail to identify and focus on fact-critical information when analyzing token sequences. To address this, we propose LAFaCT, a Localize-then-Analyze detection framework. It first localizes fact-critical tokens using Factual Criticality, a novel metric derived from feature attribution. A subsequent stage then performs a focused sequential analysis on their hidden states. Extensive experiments on eight benchmarks and multiple model families confirm LAFaCT as the new state-of-the-art, with in-depth analyses validating the effectiveness of its core token-localization strategy.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

**研究动机与背景：**
- 大语言模型（LLM）在实际应用中普遍存在“幻觉”问题，即生成事实错误或虚构内容，严重削弱了模型在高风险场景（如医疗、金融）中的可靠性。
- 幻觉检测方法可分为三类：
  - **黑盒方法**（如 SelfCheckGPT）：依赖多次采样响应的自一致性，计算开销大，且在模型系统性错误时失效；
  - **灰盒方法**（如 Semantic Entropy、SAR）：基于输出概率或熵，但受限于 LLM 固有的过度自信；
  - **白盒方法**：直接分析模型内部隐藏状态，被认为编码了更直接、更根本的事实性信号，是目前最有前景的方向。
- **核心问题**：现有白盒方法在分析 token 序列时未能识别并聚焦**事实关键（fact-critical）信息**，具体表现为两类缺陷：
  1. **单 token 探测**（如 Factoscope、HaloScope）：仅分析固定位置（如最后一个 token）的隐藏状态，视角不完整；
  2. **全局聚合**（如 EigenScore、PoLLMgraph、MIND）：不加区分地聚合所有 token 的隐藏状态，引入了大量与事实无关的噪声，稀释了关键事实信号。

**整体含义**：论文提出通过“先定位、后分析”（Localize-then-Analyze）的策略，只对最具有事实关键性的 token 的隐藏状态进行聚焦分析，从而同时规避上述两类缺陷，显著提升幻觉检测性能。

---

## 2. 论文提出的方法论

### 2.1 核心思想
LAFaCT 是一个两阶段框架：
- **阶段一（定位）**：使用基于特征归因的新指标 **Factual Criticality** 从生成的响应中定位少量事实关键 token；
- **阶段二（分析）**：对这些关键 token 的隐藏状态进行**聚焦序列分析**，得到最终幻觉分数。

### 2.2 关键技术细节

**（1）代理分类器（Proxy Classifier）**
- 将提示词与响应拼接序列 `[P_prompt; X_response]` 输入 LLM，提取**中间层**最后一个 token 的隐藏状态 \( h_{n-1}^{(l)} \)；
- 训练一个两层 MLP 作为代理分类器 \( C_{proxy} \)，输出事实性概率 \( o_p \)，使用二元交叉熵损失；
- 该分类器**主要服务于归因信号提取**，而非独立检测器。

**（2）Factual Criticality 指标**
- 定义端到端计算路径 \( F \)：从输入 token 嵌入 \( E \) → 前 l 层 Transformer → 代理分类器 \( C_{proxy} \) → 事实性概率 \( o_p \)；
- 使用 **DeepLIFT** 算法将 \( o_p \) 归因回每个 token 的嵌入，以 `<pad>` token 嵌入序列作为基线；
- 每个 token 的归因分数 \( S(x_i) \) 为其各维度归因值的 L2 范数；
- 经 softmax 归一化得到 Factual Criticality 分数：
  \[
  C(x_i) = \frac{\exp(S(x_i))}{\sum_j \exp(S(x_j))}
  \]
- 采用 **Top-p 策略**（\( p=0.8 \)）从响应中选择关键 token 子集。

**（3）聚焦序列分析（Focused Sequential Analysis）**
- 使用 **Bi-GRU** 编码器对关键 token 的隐藏状态序列进行建模，保留原始顺序；
- 为每个 token 计算**相对位置编码**（基于与上一个选中 token 的相对距离，使用正弦函数）；
- 将隐藏状态与位置编码拼接后经 MLP 投影为特征向量 \( v_i \)；
- 双向 GRU 输出拼接得到最终事实性表示 \( e_x \)。

**（4）Angular Triplet Loss（角度三元组损失）**
- 将表示归一化到单位超球面上；
- 对每个锚点样本，构造同类的正样本和异类的负样本，计算锚点与正负样本之间的角度 \( \theta_p \) 和 \( \theta_n \)；
- 损失函数：
  \[
  L_{AT} = \max(0, \cos(\theta_n) - \cos(\theta_p + m))
  \]
- 该损失在角度空间中强制类间分离、类内紧凑，学习高度判别性的事实性表示。

**（5）推断阶段**
- 对测试样本生成事实性表示后，计算其与训练集中 top-5 最近邻的“事实”和“幻觉”样本的平均余弦相似度；
- 将样本分类到平均相似度更高的类别。

---

## 3. 实验设计

### 3.1 数据集与评测场景
论文在 **8 个基准**上评估，涵盖三类任务：

| 任务类别 | 数据集 | 说明 |
|---------|--------|------|
| 问答（QA） | TruthfulQA, TriviaQA, CoQA, GSM8K, MedQuad | 主要测试平台，覆盖常识、事实知识、对话、数学推理、医疗 |
| 文本摘要 | XSum, FRANK | 源依赖生成任务，评估摘要事实性 |
| 传记生成 | WikiBio GPT-3 | 数据到文本场景，包含句子级人工标注 |

### 3.2 目标模型
- LLaMA-2-chat-hf（7B、13B）
- Qwen-2.5-Instruct（8B、14B）
- LLaMA-3-Instruct-8B
- Mistral-Instruct-7B

### 3.3 对比方法
- **黑盒**：SelfCheckGPT
- **灰盒**：Semantic Entropy、SAR
- **白盒单 token 探测**：LLM Factoscope、HaloScope（含半监督变体 HaloScope*）
- **白盒全局聚合**：EigenScore、PoLLMgraph
- **白盒混合**：MIND
- **并行的 2025 年方法**：SATMD、LapEigvals、Focus（WikiBio 场景）

### 3.4 评测指标
- 主要指标：**AUROC**（问答、摘要任务）
- WikiBio 传记任务：**AUC-PR**（含 NonFact、NonFact*、Factual 三个子指标）

---

## 4. 资源与算力

**论文明确说明（见 Appendix K）：**
- 所有实验在一台配备 **4 张 NVIDIA A40 GPU** 的服务器上进行；
- 总计约 **300 GPU 小时**；
- 代码使用 Python 3.8.2 和 PyTorch 2.4.1 实现。

**时间成本分析（见 Appendix F.6）：**
- 在 Llama2-7B 上，LAFaCT 相对响应生成的额外开销仅为 **5.6%**；
- 在 Qwen2.5-14B 上开销峰值约为 **8.4%**；
- 最近邻推断数据库极为轻量：1 万个样本仅需不到 **20 MB** 存储空间。

---

## 5. 实验数量与充分性

### 5.1 实验数量概览
论文进行了**大量且系统性**的实验，包括：

1. **主实验**：在 3 个模型（Llama2-7B、Llama3-8B、Qwen2.5-8B）× 5 个 QA 数据集上的完整对比（表 1）；
2. **补充模型实验**：Mistral-7B、Llama2-13B、Qwen2.5-14B（表 8）；
3. **模型规模泛化实验**：7B→13B、8B→14B（图 3）；
4. **OOD 泛化实验**：留一法跨数据集评估（表 2）；
5. **摘要任务实验**：XSum、FRANK 两个基准 × 2 个模型（表 3）；
6. **传记生成实验**：WikiBio 三个指标 × 2 个代理模型（表 4）；
7. **定位策略对比**：无定位、启发式定位、归因定位共 8 种方法对比（表 5）；
8. **定性分析**：Factual Criticality 的可视化案例（表 6、表 17）；
9. **定量验证**：GPT-4 标注关键 token 的 Factual Criticality 分数分布分析（图 4）；
10. **代理分类器消融**：4 种代理架构 × 全框架对比（图 5）；
11. **分析阶段消融**：损失函数（Angular Triplet vs. Triplet vs. CE）、位置编码（相对 PE vs. 绝对 PE vs. 无 PE）（表 7）；
12. **归因细节消融**：嵌入范围、归因目标（表 11）；
13. **层选择分析**：不同层、不同隐藏状态类型的敏感性（图 6、表 12）；
14. **数据效率实验**：12.5%–100% 训练数据比例（图 7、表 13）；
15. **序列建模架构消融**：MLP、Uni-GRU、Transformer Block、Bi-LSTM、Bi-GRU（表 14）；
16. **计算效率分析**（表 15）；
17. **标签阈值敏感性分析**（表 16）；
18. **k 折交叉验证**（图 8）；
19. **与 2025 年并发方法对比**（表 9）。

### 5.2 充分性与公平性评估
- **充分性**：实验覆盖 3 大类任务、8 个基准、4 个模型族、6 种以上基线方法，以及覆盖方法各模块的消融分析，整体实验设计非常充分；
- **客观性**：主实验均使用三次随机种子取平均，数据划分受随机种子控制；对标签合成（AlignScore）进行了阈值敏感性分析，并对无专用训练集的基准进行了 k 折交叉验证，增强了结果的可信度；
- **公平性**：监督基线在同一数据集上重训；对需要监督的基线（如 HaloScope）区分了半监督和全监督变体；对比时明确控制训练数据量。

---

## 6. 论文的主要结论与发现

1. **LAFaCT 达到新的最先进水平**：
   - 在 Llama2-7B 上，平均 AUROC 超过最强基线 **3.2 个点**；
   - 在 Llama3-8B 和 Qwen2.5-8B 上，优势分别为 **2.6** 和 **2.1** 个点；
2. **在复杂推理任务上优势最明显**：GSM8K 和 MedQuad（平均响应长度超过 100 token）上，对最强基线的领先分别达 **4.2** 和 **4.5** 个点；
3. **OOD 泛化能力强**：留一法分析中，LAFaCT 平均超过第二好基线 **4.1** AUROC 点，在 GSM8K 上领先 **5.7** 个点；
4. **关键 token 定位策略有效**：消融实验证明选择性分析显著优于非选择性方法，归因方法优于启发式方法，DeepLIFT 表现最佳；
5. **Factual Criticality 具备准确定位能力**：能准确锁定错误来源（如错误前提、错误实体）和逻辑主干词汇；定量验证显示 GPT-4 标注的关键 token 的 Factual Criticality 分数显著更高；
6. **框架对代理分类器架构不敏感**：不同代理架构下 LAFaCT 表现稳定，且远优于单独使用代理分类器；
7. **具有数据效率**：仅用 12.5% 训练数据仍显著优于多个强基线。

---

## 7. 优点

**方法设计方面：**
1. **问题洞察准确**：精准指出了现有白盒方法的“两难困境”（单 token 探测视角不完整 vs. 全局聚合引入噪声），并提出了“先定位后分析”的统一解；
2. **创新指标 Factual Criticality**：将特征归因（DeepLIFT）引入事实关键 token 定位，属于新颖的方法论贡献；
3. **Angular Triplet Loss**：在角度空间中学习判别性表示，相比传统分类损失和欧氏距离三元组损失更有效，且提升了 OOD 泛化和数据效率；
4. **框架模块化、可解释性强**：定位阶段输出的 token 级归因分数可直接用于可视化，增强了检测过程的可解释性；
5. **计算开销低**：相比黑盒多次采样方法（140% 开销），LAFaCT 额外开销仅 5.6%–8.4%，实用性强。

**实验验证方面：**
1. 覆盖任务类型广（问答、摘要、传记生成）和多个模型族（Llama、Qwen、Mistral）；
2. 消融实验设计完备，从定位策略、归因方法、损失函数、位置编码、序列建模架构到计算效率均有系统性验证；
3. 对标签噪声、数据划分方式、训练数据量等潜在偏差来源进行了专门的鲁棒性分析。

---

## 8. 不足与局限

**论文明确指出（见 Limitations 节）：**
1. **监督依赖**：LAFaCT 是监督方法，依赖标注数据，缺乏无监督方法的即插即用性，在标注稀缺场景下应用受限；
2. **标签噪声**：开放生成任务（如摘要）的标签依赖启发式合成（AlignScore 阈值化），可能引入标注噪声。

**实验覆盖方面的潜在局限：**
1. **生成配置单一**：所有响应均使用贪心解码生成（表 10），未检验在不同解码策略（如核采样、束搜索）下的检测稳定性；
2. **模型覆盖仍有限**：未覆盖 GPT 等闭源模型（仅在 WikiBio 中用开源模型作为代理）以及更大规模（如 70B+）模型；
3. **推理基准偏少**：主要依赖 GSM8K 作为复杂推理的代表，未覆盖更多推理类型（如常识推理、多跳推理）；
4. **阈值选择的任意性**：虽然进行了敏感性分析，但 AlignScore 阈值（QA 0.3、摘要 0.9）的选取仍存在一定的主观性；
5. **最近邻推断策略**：依赖训练集嵌入存储，虽然存储开销小，但在极少标注数据的极端场景下，top-5 最近邻策略的可靠性未被充分验证。

**失败案例分析发现的边界（见 Appendix I）：**
1. 当响应中大量中间步骤正确、仅少数计算步骤出错时，正确 token 的分数可能稀释错误信号，导致漏检；
2. 当模型对常见误解有极强的内部信念时，隐藏状态缺乏典型的“编造”模式，系统可能将幻觉当作事实接受。

---

## 总结

LAFaCT 通过“先定位事实关键 token、后聚焦序列分析”的策略，系统性地解决了白盒幻觉检测中长期存在的“分析不聚焦”问题。其核心贡献在于提出了基于 DeepLIFT 归因的 Factual Criticality 指标和基于 Angular Triplet Loss 的判别性表示学习，实现了八个基准上多个模型族的最先进性能。实验设计全面、消融充分、分析深入，方法具有较高的实用价值。主要局限在于监督依赖、开放任务标注噪声以及有限生成配置下的泛化验证，未来可向半监督/无监督方向拓展。

（完）
