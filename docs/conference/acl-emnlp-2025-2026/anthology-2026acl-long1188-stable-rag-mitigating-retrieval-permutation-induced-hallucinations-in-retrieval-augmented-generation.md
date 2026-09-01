---
title: "Stable-RAG: Mitigating Retrieval-Permutation-Induced Hallucinations in Retrieval-Augmented Generation"
title_zh: Stable-RAG：缓解检索增强生成中由检索排列引起的幻觉
authors: "Qianchi Zhang, Hainan Zhang, Liang Pang (庞亮), Hong-Wei Zheng, Zhiming Zheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1188.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 针对检索文档顺序敏感性的RAG幻觉缓解方法
tldr: 检索增强生成（RAG）虽有助减少幻觉，但检索文档的排列顺序会显著影响大语言模型的回答，甚至在金文档固定在首位时也存在较大波动。本文通过实验揭示了这一曾被忽视的对检索排列的敏感性，并提出 Stable-RAG 来缓解由此引发的幻觉。该方法在不需要改进检索质量的前提下，增强了模型对检索列表排列的鲁棒性。实验结果显示了其在多种设置下稳定地减少幻觉，为 RAG 的可靠性提供了新的保障视角，与现有聚焦低质检索和位置偏置的方法形成互补。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1570, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1583, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1630, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 769, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1656, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 639, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1661, \"height\": 1671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1188/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1659, \"height\": 1807, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 761, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 828, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1468, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1188/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 775, \"height\": 217, \"label\": \"Table\"}]"
motivation: RAG中检索文档的排列顺序会改变模型答案，引发被忽视的幻觉隐患。
method: 识别检索排列敏感性问题，提出 Stable-RAG 方法增强模型对排列的鲁棒性。
result: 实验表明 Stable-RAG 能显著减少检索排列引起的幻觉，且不依赖更高质量的检索。
conclusion: 揭示了 RAG 中新的幻觉来源，并提供轻量有效的缓解手段。
---

## Abstract
Retrieval-Augmented Generation (RAG) has become a key paradigm for reducing factual hallucinations in Large Language Models (LLMs), yet little is known about how the order of retrieved documents affects model behavior. We empirically show that under a Top-5 retrieval setting with the gold document included, LLM answers vary substantially across permutations of the retrieved set, even when the gold document is fixed in the first position. This reveals a previously underexplored sensitivity to retrieval permutations. Although existing robust RAG methods focus primarily on enhancing LLM robustness to low-quality retrieval and mitigating positional bias to distribute attention fairly over long contexts, neither approach directly addresses permutation sensitivity. In this paper, we propose Stable-RAG, which exploits permutation sensitivity estimation to mitigate permutation-induced hallucinations. Stable-RAG runs the generator under multiple retrieval orders, clusters hidden states, and decodes from a cluster-center representation that captures the dominant reasoning pattern. It then uses these reasoning results to align hallucinated outputs toward the correct answer, encouraging the model to produce consistent and accurate predictions across document permutations. Experiments on three QA datasets show that Stable-RAG improves answer accuracy, reasoning consistency, and generalization across datasets, retrievers, and input lengths compared with strong baselines.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **背景**：检索增强生成（RAG）通过引入外部文档来降低大语言模型（LLM）的事实性幻觉，但其自身仍存在未被充分认识的脆弱性。
- **核心发现**：论文通过实验证明，在 Top-5 检索设置下、即使“金文档”（gold document）被固定在第一位置，仅改变其余文档的排列顺序，LLM 的答案也会出现显著差异，甚至产生与证据相矛盾的幻觉输出。作者将这种现象命名为 **排列诱导幻觉（Permutation-Induced Hallucinations）**。
- **问题根源**：这种敏感性并非源于检索质量低（文档集完全相同），也并非长上下文位置偏置（Top-5 文档总长不超过 1000 token），而是源于 LLM 内部推理动力学的**结构不稳定性**——随着模型层数加深，不同文档排列会引发越来越分化的推理轨迹，并在中高层出现明显分支。
- **整体意义**：现有鲁棒 RAG 方法主要针对低质量检索增强鲁棒性，或缓解长上下文中的位置偏置，均未直接解决排列敏感性问题。该研究揭示了一个以往被忽视的幻觉来源，并提出新的缓解思路，对提升 RAG 系统的可靠性具有重要价值。

## 2. 方法论：Stable-RAG

Stable-RAG 通过三个关键阶段显式建模并缓解排列敏感性：

- **阶段一：隐状态聚类（Hidden State Clustering）**
  - 对每个查询，枚举检索文档集合 \(S=\{d_1,\dots,d_n\}\) 的全部排列（\(N=n!\) 种），对每种排列运行模型。
  - 提取模型在生成回答前最后一层的最后一个 token 的隐状态 \(h^{(i)} \in \mathbb{R}^d\)，构成矩阵 \(H\in\mathbb{R}^{N\times d}\)。
  - 对 \(H\) 进行**谱聚类**：基于余弦距离构造相似度矩阵 \(A\)，计算归一化图拉普拉斯 \(L\)，通过特征间隙（eigengap）自适应确定聚类数 \(K\)。
  - 每个聚类代表一种“潜在推理模式”；对每个聚类，选取距离质心最近的隐状态作为代表，解码得到候选答案。
  - 这样做将实际解码次数从 \(N=n!\) 降到 \(K\)，显著降低计算和标注成本。

- **阶段二：偏好数据构建（Preference Data Construction）**
  - 将上述代表解码结果与标准答案比对，将样本分为四类：
    - **FC（完全正确）**：所有排列下均正确，样本稳定，不参与训练。
    - **PC（部分正确）**：不同排列下既有正确也有错误答案；取出现频率最高的正确答案作为 \(y_w\)，频率最高的错误答案作为 \(y_l\)。
    - **FU（完全错误且不可回答）**：所有排列均错误且文档中无金答案；设置 \(y_w=\)“I don’t know”，鼓励模型弃权，\(y_l\) 为最常见的错误答案。
    - **FA（完全错误但可回答）**：所有排列均错误但文档中存在金答案；设置 \(y_w\) 为金答案，\(y_l\) 为“I don’t know”。

- **阶段三：DPO 对齐（Alignment with DPO）**
  - 使用直接偏好优化（Direct Preference Optimization）在构造的偏好元组 \((x,y_w,y_l)\) 上微调模型。
  - 目标函数为标准的 DPO 损失：最大化 \(y_w\) 相对 \(y_l\) 的可能性，同时以参考模型 \(\pi_{\text{ref}}\) 为基准，超参数 \(\beta\) 控制偏好强度。
  - 该过程促使模型在不同文档排列下优先输出语义一致、事实正确的答案，从而抑制排列诱导的幻觉。

## 3. 实验设计

- **数据集**：
  - 单跳开放域问答：NaturalQuestions（NQ）、TriviaQA。
  - 多跳问答：HotpotQA。
  - 三种数据集覆盖不同推理复杂度，用于评估方法的普适性。

- **检索器与文档设置**：
  - 使用 DPR 和 Contriever-MS MARCO 两种检索器，统一采用 Top-5 文档。

- **骨干模型**：LLaMA3-8B-Instruct 和 Qwen3-8B，验证模型无关性。

- **评估指标**：Substring Exact Match（SubEM）和 F1。

- **对比基线**：
  - Vanilla：Direct Generation、Vanilla RAG、Vanilla SFT。
  - 鲁棒 RAG：RetRobust、ATM、RAAT。
  - 位置偏置方法：Pos2Distill、Ms-PoE。
  - 额外对照：标准 DPO（用于隔离顺序稳定性机制的贡献）。

## 4. 资源与算力

- 论文在附录 A.3 中明确说明：训练使用 **2 张 NVIDIA RTX PRO 6000 GPU**。
- 训练配置：LoRA（rank=128, alpha=128, dropout=0），学习率 \(5\times10^{-6}\)，batch size 2 + 梯度累积 8，DPO 超参数 \(\beta=0.4\)。
- 训练时长：LLaMA-3-8B-Instruct 训练 1 epoch，Qwen3-8B 训练 2 epochs，每个 epoch 约 **2 小时**。
- 此外，数据构建阶段需要枚举全部 5! = 120 种排列并提取隐状态，但通过代表解码可将解码次数从 120 降到聚类数 K，从而减少资源开销。

## 5. 实验数量与充分性

- **主实验**：表 2 给出了两个骨干模型 × 两个检索器 × 三个数据集的完整结果，覆盖 8 种基线方法，实验规模较大。
- **消融实验**：表 3 分别移除 PC、FA、FU 三类组件，验证各组件必要性，并报告弃权率（AR）。
- **与标准 DPO 对比**：表 4 控制偏好优化框架不变，仅加入顺序稳定性约束，证明该机制的有效性。
- **泛化实验**：
  - 跨数据集泛化：在不同训练/测试数据组合下评估。
  - 跨检索器迁移：DPR 训练后用 Contriever 测试（以及反向迁移）。
  - 跨 Top-K 鲁棒性：在 Top-5 训练，测试不同 K 值。
  - 训练数据量影响：从 1k 到 30k 样本的性能变化。
- **行为分析**：包括层内隐状态聚类数变化、DPO 训练前后模型内部行为对比、外部位置鲁棒性（PSR）、原始 vs. 洗牌顺序对比等。
- **充分性与公平性**：所有方法在相同测试集和检索文档集上评估，对比相对公平。实验覆盖了方法有效性、组件贡献、泛化能力、内部机制和鲁棒性，整体较充分；但缺少更大规模模型（如 70B）与更大 n（如 Top-10 以上）的实验验证。

## 6. 主要结论与发现

- **排列敏感性是 RAG 的普遍脆弱性**：在 LLaMA3 和 Qwen3 系列多个规模模型上均观测到，较小模型更敏感，较大模型仍有明显波动。
- **分歧出现在中高层**：浅层隐状态聚类混合，中层开始分歧，高层明显分离；高敏感样本的分歧程度远大于低敏感样本。
- **Stable-RAG 可有效缓解幻觉**：在三个 QA 数据集、两个检索器、两个骨干模型上，该方法在 SubEM 和 F1 上均一致优于所有强基线。
- **泛化能力强**：跨数据集、跨检索器、跨 Top-K 均保持稳定提升；训练数据量仅需约 15k 即可达到饱和性能。
- **内部机制改善**：DPO 对齐后，高敏感样本的推理轨迹聚类数显著下降，模型对排列的敏感性降低，同时保留低敏感样本的多样性。

## 7. 优点

- **问题新颖且有实证支撑**：系统性地揭示了 RAG 中“排列诱导幻觉”这一被忽视的脆弱性，并通过层内聚类可视化与量化分析给出可信证据。
- **方法与现有工作互补**：不依赖提升检索质量或修改位置编码，而是直接建模排列敏感性，可独立或与既有方法叠加使用。
- **模型无关**：在两个不同架构的 8B 模型上均有效，具备通用性。
- **成本可控**：谱聚类 + 代表解码将解码次数从 120 次降至 K 次，比全排列解码减少约三倍标注开销。
- **设计兼顾可信度**：通过“弃权”机制（FU/FA 处理）增强模型对自身能力边界和证据可用性的感知。
- **实验设计全面**：涵盖主结果、消融、标准 DPO 对比、跨数据集/检索器/Top-K 泛化、训练数据规模、内部行为分析等多个维度，结论扎实。

## 8. 不足与局限

- **仅约束最终层表示**：论文在 Limitation 中承认，Stable-RAG 只对最后层隐状态进行聚类与对齐，未显式约束中间层的推理轨迹；若能加入逐层约束或轨迹级对齐，可能进一步提升稳定性。
- **计算与标注开销仍较高**：虽然代表解码降低了部分成本，但依然需要对所有排列（120 种）运行模型并提取隐状态，预处理成本不可忽视；更高效的聚类或弱监督策略尚待探索。
- **依赖谱聚类超参数**：相似度矩阵中的 \(\sigma\) 等超参数可能影响聚类效果，论文未给出充分的敏感性分析。
- **无法保证完全正确**：方法只是降低幻觉概率，在医疗、法律、金融等高利害领域仍需谨慎使用。
- **外部文档偏差风险**：若检索文档本身包含偏见或错误，RAG 系统可能传播甚至放大这些错误；该方法并未解决文档内容质量本身的问题。
- **实验覆盖有限**：未测试更大模型（如 70B）、更大排列数 n、多语言或更复杂推理任务，结论的通用性仍有提升空间。

（完）
