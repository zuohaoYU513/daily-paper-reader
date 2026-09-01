---
title: Hallucination Detection in LLMs Using Spectral Features of Attention Maps
title_zh: 利用注意力图谱谱特征检测大语言模型幻觉
authors: "Jakub Binkowski, Denis Janiak, Albert Sawczyn, Bogdan Gabrys, Tomasz Jan Kajdanowicz"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1239.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 基于注意力图谱谱特征的LLM幻觉检测
tldr: 现有基于注意力图的大模型幻觉检测方法效果有限。论文将注意力图视为图的邻接矩阵，提出LapEigvals方法，把由注意力图导出的拉普拉斯矩阵的top-k特征值作为幻觉检测探针的输入。实验表明该方法在基于注意力的幻觉检测方法中达到最优性能，揭示了谱特征对幻觉检测的价值。该工作为轻量白盒幻觉检测提供了新的特征表示思路。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 651, \"height\": 790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1527, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 771, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 784, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1652, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1631, \"height\": 1686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1665, \"height\": 2164, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 738, \"height\": 1724, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 785, \"height\": 1860, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1239/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1659, \"height\": 1483, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 902, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 1385, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 572, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1648, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1457, \"height\": 2554, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 973, \"height\": 2549, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1638, \"height\": 1521, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1638, \"height\": 1764, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1642, \"height\": 1336, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1655, \"height\": 1042, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1647, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1642, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1239/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1640, \"height\": 304, \"label\": \"Table\"}]"
motivation: 基于注意力图的幻觉检测效果有限，注意力图中蕴含的图结构信息未被充分利用。
method: 提出LapEigvals，将注意力图视为图结构，提取拉普拉斯矩阵前k个特征值供检测探针使用。
result: 实证评估表明该方法在基于注意力的幻觉检测方法中达到最优性能。
conclusion: 注意力图谱特征能有效刻画幻觉模式，为白盒幻觉检测提供轻量而有效的新特征。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable performance across various tasks but remain prone to hallucinations. Detecting hallucinations is essential for safety-critical applications, and recent methods leverage attention map properties to this end, though their effectiveness remains limited. In this work, we investigate the spectral features of attention maps by interpreting them as adjacency matrices of graph structures. We propose the LapEigvals method, which utilises the top- k eigenvalues of the Laplacian matrix derived from the attention maps as an input to hallucination detection probes. Empirical evaluations demonstrate that our approach achieves state-of-the-art hallucination detection performance among attention-based methods. Extensive ablation studies further highlight the robustness and generalisation of LapEigvals, paving the way for future advancements in the hallucination detection domain.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：大型语言模型（LLM）在众多自然语言处理任务中表现优异，但在生成过程中极易产生“幻觉”（hallucination），即生成内容与事实或给定上下文不符。由于幻觉无法被彻底消除，安全关键型应用对幻觉检测方法提出了迫切需求。
- **现有问题**：已有基于注意力图的幻觉检测方法（如 AttentionScore）能力有限，未能充分利用注意力图内蕴含的结构信息。与此同时，图神经网络领域的研究表明，图的谱特征（如拉普拉斯矩阵特征值）能够刻画信息流瓶颈、连通性等关键性质。
- **核心动机**：本文假设幻觉可能源于 LLM 内部信息流的中断或瓶颈，而这种结构异常可通过注意力图的拉普拉斯谱特征进行捕获。论文由此提出一种全新的、利用注意力图谱特征进行幻觉检测的方法。

## 2. 论文提出的方法论

- **核心思想**：将 LLM 每层每个注意力头的注意力矩阵视为加权有向图的邻接矩阵，节点对应 token，边权重为注意力分数；借助图拉普拉斯矩阵的谱特征（top-k 特征值）作为幻觉检测探针的输入。
- **技术细节**：
  - 定义注意力矩阵 \(A^{(l,h)}\)（行随机、下三角、非负）。
  - 构建有向图的拉普拉斯矩阵：\(L^{(l,h)} = D^{(l,h)} - A^{(l,h)}\)，其中 \(D^{(l,h)}\) 为**出度矩阵**（入度因 softmax 恒为 1，不具备区分性），出度按后续 token 数归一化：  
    \[
    d_{ii} = \frac{\sum_u a_{ui}}{T - i}
    \]
  - 该拉普拉斯矩阵为下三角矩阵，因此其特征值即为其对角元素；对每个 head 和 layer 取前 k 个最大特征值，拼接所有层和头的特征得到高维向量。
  - 使用 PCA 将特征向量降到 512 维，输入逻辑回归（logistic regression）探针，输出幻觉/非幻觉预测。
- **方法名称**：LapEigvals（Laplacian Eigenvalues）。
- **优势**：由于特征值直接来自对角线，计算复杂度低，且理论证明拉普拉斯特征值有界于 [-1, 1]，最后一位 token 对应特征值恒为 0，具有良好数值性质。

## 3. 实验设计

- **数据集**：7 个公开问答数据集：
  - 短上下文：NQ-Open、TriviaQA
  - 长上下文：CoQA、SQuADv2
  - 其他：HaluEvalQA（QA 部分）、TruthfulQA（生成部分）、GSM8K（数学应用题，精确匹配评估）
- **LLM 配置**：5 个开源模型（Llama-3.1-8B、Llama-3.2-3B、Phi-3.5、Mistral-Nemo、Mistral-Small-24B），每个模型采用两种采样温度（temp=0.1 和 1.0），共 10 种生成配置。
- **标签生成**：除 GSM8K 使用精确匹配外，其余数据集采用 GPT-4o-mini 作为“LLM-as-judge”自动标注，并验证与 GPT-4.1 的一致性（Cohen’s Kappa 落在可接受范围）。
- **基线方法**：
  - AttentionScore（无监督，仅作为参考）
  - AttnLogDet（AttentionScore 的监督版，使用每头 log-行列式）
  - AttnEigvals（直接使用原始注意力矩阵特征值，作为对照）
  - 附录中还对比了基于隐藏状态的探针（HiddenStates）
- **评估指标**：主要使用 AUROC，补充 Precision/Recall。

## 4. 资源与算力

- 论文在 **实现细节** 部分明确说明：
  - LLM 推理及注意力图提取：使用单张 NVIDIA A40（40GB VRAM），Mistral-Small-24B 使用单张 NVIDIA H100（96GB VRAM）。
  - 幻觉探针训练：仅使用 CPU。
- 未提及具体的 GPU 数量、训练时长、总 GPU 小时数等量化信息；只给出了大致硬件类型。成本分析部分仅估算了 LLM-as-judge 标注 API 费用，未提供完整训练算力预算。

## 5. 实验数量与充分性

- **主实验**：5 个 LLM × 7 个数据集 × 2 个温度 × 3 个基于注意力的方法（LapEigvals 与两个监督基线），共约 210 组 AUROC 结果，另附 Precision/Recall 表。
- **消融实验**：
  - 特征数量 k 的影响（k∈{5,10,25,50,100}）；
  - 使用所有层 vs 单层（per-layer vs all-layers）；
  - 采样温度对检测性能的影响（temp∈{0.1,0.5,1.0,2.0}）；
  - 跨数据集泛化（训练集与测试集来自不同 QA 数据集）；
  - 不同提示词（4 种 prompt）下的稳定性；
  - 扰动鲁棒性（高斯噪声）、训练集规模影响、特征可靠性分析。
- **总体评价**：实验设计较为充分，覆盖了多种模型规模、多种数据集、多种温度以及多个维度的消融；但部分消融仅基于单一模型（如 Llama-3.1-8B）或单一数据集（如 TriviaQA），可能会限制结论的普适性。整体上，实验数量丰富且对比公平（基线均适配为监督/无监督同协议），具备较强的说服力。

## 6. 论文的主要结论与发现

- LapEigvals 在 7 个数据集中有 6 个取得最优 AUROC，在全部 5 个 LLM 上表现稳定，达到基于注意力方法的 SOTA。
- 使用拉普拉斯特征值（LapEigvals）显著优于直接使用原始注意力矩阵特征值（AttnEigvals），说明“拉普拉斯变换”是提取有效特征的关键。
- 统计检验（Mann-Whitney U）显示，拉普拉斯特征值在幻觉与非幻觉样本之间的差异显著性比例高于 AttentionScore，表明其是更强的预测信号。
- 利用所有层的信息比仅用单层更好，且避免了逐层搜索最优层的开销。
- 更高采样温度下，所有方法性能均提升，但 LapEigvals 始终优于基线。
- 跨数据集泛化方面，LapEigvals 性能下降幅度与基线相当，且在多个场景中表现最好；但在 TruthfulQA 和 GSM8K 上泛化困难，分别归结于小样本/类别不平衡和领域差异。
- 方法对特征扰动具有较强的鲁棒性（小噪声几乎不降低性能），且对训练数据规模不敏感，仅需少量标注样例仍能保持合理表现。

## 7. 优点

- **新颖的图论视角**：将注意力图解释为有向图，并利用拉普拉斯谱特征——这在幻觉检测领域是首次尝试，提供了新的理论支撑。
- **计算高效**：利用注意力矩阵的下三角结构，特征值直接来自对角线，无需昂贵矩阵分解；特征提取可与 LLM 推理融合，内存开销可控。
- **特征信息量高**：拉普拉斯特征值比 AttentionScore 或原始注意力特征值更具区分度，且在所有层、所有头上拼接能利用全局信息。
- **实验严谨全面**：包括多模型、多数据集、多温度、多提示词，并附带消融、泛化、鲁棒性、成本等分析，开源实现。
- **可解释性与可扩展性**：谱特征对应信息流瓶颈，为理解幻觉产生机制提供了新方向。

## 8. 不足与局限

- **监督依赖**：需要人工或 LLM 生成的标注来训练探针，引入潜在噪声且存在过拟合风险。
- **架构不通用**：方法要求 LLM 具有明确的分层、多头结构，不同架构（head/layer 配置不同）需重新训练；无法直接用于闭源 API 模型。
- **最小长度限制**：计算 top-k 特征值要求 token 数不少于 k（如 k=100 需要至少 100 个 token），短文本场景受限。
- **验证范围有限**：仅在英语 QA 数据、选定的开源 LLM 上测试；不同领域、任务和语言的表现未验证，存在迁移风险。
- **公平性/客观性问题**：部分消融仅在单一 LLM 或单一数据集上进行，且 LLM-as-judge 标签存在主观性（虽然验证了与 GPT-4.1 的 Kappa 一致性）。数据集类别不平衡（如 HaluEvalQA、TruthfulQA）可能影响部分结论。
- **与隐藏状态方法的比较**：虽然附录中对比了 HiddenStates，但未与最新最先进的白盒方法（如 Semantic Entropy Probe、INSIDE 等）进行直接比较，基线选择仍有一定局限性。

---
（完）
