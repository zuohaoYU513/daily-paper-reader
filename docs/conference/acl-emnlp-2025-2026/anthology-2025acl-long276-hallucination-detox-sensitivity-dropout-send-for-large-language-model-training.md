---
title: "Hallucination Detox: Sensitivity Dropout (SenD) for Large Language Model Training"
title_zh: 幻觉解毒：面向大语言模型训练的敏感性丢弃（SenD）
authors: "Shahrad Mohammadzadeh, Juan David Guerra, Marco Bonizzato, Reihaneh Rabbany, Golnoosh Farnadi"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.276.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 提出敏感性丢弃训练策略，降低大模型训练中的幻觉方差
tldr: 大模型的幻觉常与训练动态中的不确定性相关。该工作基于Pythia套件分析训练过程中的幻觉趋势，发现显著方差并据此提出敏感性丢弃(SenD)训练协议，确定性丢弃易变异的嵌入维度以降低幻觉方差。此外还设计了无监督幻觉度量。实验表明该方法能减少训练中的幻觉波动，提高模型可靠性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 815, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1665, \"height\": 772, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 771, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 768, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 804, \"height\": 1119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 794, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 811, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 774, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long276/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 664, \"height\": 2162, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long276/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 1275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long276/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1511, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long276/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 734, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long276/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1101, \"height\": 863, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long276/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1151, \"height\": 663, \"label\": \"Table\"}]"
motivation: 训练动态中的不确定性会导致幻觉涌现，现有方法缺少对这些信号的有效利用。
method: 提出SenD，通过对高变异嵌入索引进行确定性丢弃来降低幻觉方差。
result: 实验显示SenD降低了训练过程中的幻觉方差并提升可靠性。
conclusion: 关注训练动态方差是减少大模型幻觉的有效途径。
---

## Abstract
As large language models (LLMs) become increasingly prevalent, concerns about their reliability, particularly due to hallucinations - factually inaccurate or irrelevant outputs - have grown. Our research investigates the relationship between the uncertainty in training dynamics and the emergence of hallucinations. Using models from the Pythia suite and several hallucination detection metrics, we analyze hallucination trends and identify significant variance during training. To address this, we propose Sensitivity Dropout (SenD), a novel training protocol designed to reduce hallucination variance during training by deterministically dropping embedding indices with significant variability. In addition, we develop an unsupervised hallucination detection metric, Efficient EigenScore (EES), which approximates the traditional EigenScore in 2x speed. This metric is integrated into our training protocol, allowing SenD to be both computationally scalable and effective at reducing hallucination variance. SenD improves test-time reliability of Pythia and Meta’s Llama models by up to 17% and enhances factual accuracy in Wikipedia, Medical, Legal, and Coding domains without affecting downstream task performance.

---

## 论文详细总结（自动生成）

# 论文核心问题与整体含义

- **研究背景**：大语言模型（LLM）在广泛应用中暴露出严重的幻觉问题（即生成与事实、用户输入或训练数据不一致的内容）。本文特别关注“虚构型幻觉”（confabulation）——模型对相同或相似输入产生不一致回答，使输出在正确与错误之间摇摆，带来可靠性风险。
- **核心问题**：现有研究大多聚焦于幻觉的**事后检测与缓解**，而**训练过程本身对幻觉的影响**尚未被充分理解。本文提出关键问题：训练过程中的不确定性（uncertainty）与幻觉涌现之间是否存在系统性关联？仅依赖训练损失收敛是否可以保证幻觉减少？
- **整体含义**：作者通过实证验证了幻觉在训练中呈现**振荡行为**（oscillatory behavior），即损失收敛并不对应幻觉稳定下降。由此主张应从**训练内部动态**入手，通过识别并压制高变异的嵌入维度来降低幻觉方差，从而提升模型在测试时的可靠性和事实准确性。

# 方法论

## 核心思想

- 提出 **Sensitivity Dropout (SenD)** 训练协议：在训练过程中**确定性丢弃**那些在检查点之间表现出显著波动的嵌入索引（Sensitive Embedding Indices, SEIs），以减少幻觉相关的方差，使模型学习更加“自信”，而非单纯追求损失最小化。
- 为保证SenD的计算可扩展性，提出 **Efficient EigenScore (EES)**，一种近似传统 EigenScore 的无监督幻觉检测指标，计算速度提升约 2 倍。

## 关键技术细节

- **Sentence Embedding Vector（定义3.1）**：将模型的倒数第二层激活矩阵（penultimate layer）转换为低维句嵌入向量，用于后续变异分析。
  - 公式：\( e_k = \frac{1}{2} \left( \frac{1}{m} \sum_{i=1}^m H_i^{N-1} + H_m^{N-1} \right) \)
- **Net Change Formula（定义3.2）**：计算相邻检查点之间同一嵌入索引的绝对变化量，用于刻画振荡。
- **Sensitive Embedding Indices（定义3.3）**：选取最近 C 个检查点中总变异性最高的 top K% 嵌入索引（本文默认 K=20%，C=3）。变异性公式：\( V_i = \text{Var}(e_i) \cdot \sum_{t=T-C+1}^{T} \Delta e_i^t \)，然后选取超过给定百分位阈值的索引。
- **EigenScore（定义3.4）**：通过高温度采样（temperature=0.5）生成多个输出，利用其句嵌入协方差矩阵的 log 特征值均值作为幻觉风险度量。
- **EES 近似（Algorithm 1）**：
  - 使用**密度状态（DOS）** 和**切比雪夫多项式（Chebyshev Polynomials）** 以及**核多项式方法（KPM）**，避免显式构造协方差矩阵和特征分解。
  - 核心推导：\(\text{trace}(\log(H)) = \sum_i \log(\lambda_i)\)，结合 DOS 性质 \(\int \log(\lambda)\mu(\lambda)d\lambda\)，最终将 EigenScore 近似为 \(\frac{1}{K} \sum_{m=0}^{M} d_m c_m\)，其中 \(d_m\) 用随机迹估计计算，\(c_m\) 为切比雪夫系数。
  - 将矩阵归一化到谱区间 \([0,1]\)，输出尺度为 \([-1,1]\)，与传统 EigenScore 的 \([0,\infty)\) 不同，但趋势高度相关。
- **SenD 训练流程（Algorithm 2）**：
  - 将训练集划分为 α% 的训练子集和 (100−α)% 的跟踪子集。
  - 每个检查点记录模型在跟踪子集上的倒数第二层表示，计算 SEIs。
  - 在后续 T 个检查点（本文 T=3）中确定性丢弃这些 SEIs，循环直到损失和 EES 达到收敛阈值。
  - 实验中使用持续训练（continual training）模式，并冻结部分层以缓解遗忘。

# 实验设计

## 数据集 / 场景

- **幻觉振荡验证**：使用 Pythia 套件（70M 到 12B，共 16 个模型，20 个均匀间隔检查点），在 HaluEval（QA）、SelfCheckGPT（自一致性）、XSum（摘要，Rouge1）、perplexity 上进行评估。
- **SEI 影响实验**：使用 HELM 数据集（由 50,000+ Wikipedia 文章生成的模型输出），对 Pythia 1B 在 133k–143k 训练步的检查点进行 SEI dropout 实验。
- **SenD 训练实验**：在四个域上持续训练 Pythia 1B、Llama 3.2 1B 和 Llama 3.1 8B：
  - HELM（Wikipedia）
  - MedHALT（医学领域）
  - LegalBench（法律推理）
  - CodeSearchNet（代码生成）
- **下游评估**：HellaSwag、MMLU（通用语言理解），FactScore、HaluEval（事实性幻觉指标），Token 熵（模型置信度），以及 RAG 对比。

## Benchmark 与对比方法

- 幻觉检测基准：EigenScore（作为主要度量），EES（近似度量），SelfCheckGPT，HaluEval，FactScore，Semantic Entropy。
- SenD 对比：普通持续训练（Normal training）；随机嵌入索引 dropout 作为 SEI dropout 的基线；RAG 作为事后幻觉缓解方法进行联合对比。

# 资源与算力

- 文中**未明确说明 GPU 型号、数量或总训练算力**，仅提到使用 Compute Canada 和 Mila 集群。
- 给出了一项具体开销数据：在 HELM 数据集 2,000 个数据点上用 Llama 8B 训练一个 epoch，正常训练约 55 分钟，SenD 训练约 61 分钟，额外开销约 **11%**，作者认为值得。
- 由于算力限制，SenD 仅在**持续训练**（continual training）上验证，未应用于从头预训练。

# 实验数量与充分性

- **实验数量**：
  - 振荡行为验证：Pythia 套件 16 个模型 × 20 个检查点，覆盖多种幻觉指标，是一组大规模实证。
  - SEI dropout 实验：跨不同模型大小、不同输出类型（幻觉 vs 正确）的对比。
  - EES 效率实验：矩阵大小扫描（图3）、moments 扫描（图9），以及与 EigenScore 轨迹的相关性验证（图10）。
  - SenD 训练：3 个模型 × 4 个数据集，共 12 组持续训练实验，加上仔细的消融（K 和 Threshold）和多次运行平均。
  - 下游评估：HellaSwag、MMLU、FactScore、HaluEval、Token 熵，以及 RAG 联合效果，覆盖多个模型。
- **充分性评价**：
  - 整体实验设计**较充分**：从现象验证、机制分析、高效近似到训练协议集成，逻辑链条完整；多模型（Pythia 1B, Llama 1B, Llama 8B）、多领域（百科、医学、法律、代码）的验证增强了泛化性。
  - **存在客观性不足**：SenD 是首个训练阶段的幻觉缓解方法，没有与现有的训练中正则化/幻觉缓解方法直接对比；与 RAG 的比较仅用于说明互补性，而非公平竞争。
  - 部分结论的显著性不强：HaluEval 指标在 SenD 与普通训练之间几乎无差异；FactScore 在 Pythia 1B 上绝对值极低（0.05 vs 0.07），可能受模型能力限制，而非方法本身的有效性。
  - 消融实验（图11、图12）给出了平均多次运行的结果，增强了可靠性，但未说明随机种子方差范围。

# 主要结论与发现

- 幻觉行为在训练过程中存在**持续振荡**，且模型规模增大并不自动消除这种振荡；仅以训练损失收敛作为停止标准不可靠。
- 内部状态分析显示，存在**敏感嵌入索引（SEIs）**，这些索引在检查点之间大幅波动，与幻觉风险密切相关。
- **SEI dropout** 能显著降低 EigenScore，且对幻觉输出的影响大于对正确输出的影响，表明可以在不伤害正常回答的情况下降低虚构概率。
- **EES** 能很好近似 EigenScore 轨迹，同时在矩阵规模增大时大幅降低计算时间（约 2 倍加速），使大规模训练中的幻觉监控成为可能。
- 在所有测试模型和领域上，**SenD 训练均降低了 EES 及其训练波动性**，最终模型的幻觉风险低于普通训练。
- SenD **不损害下游性能**（HellaSwag/MMLU 与普通训练基本一致），并提高测试时置信度（Token 熵降低，最高约 17%）。
- FactScore 在 Llama 8B 上提升约 11%（无 RAG）和 10%（使用 RAG）；SenD 可与 RAG **互补**，共同提高事实准确率。
- 总体主张：**训练动态方差是幻觉的重要来源，针对性正则化（SenD）是减少幻觉的有效路径**。

# 优点

- **切入点新颖**：将幻觉缓解从推理/事后阶段前置到训练阶段，关注训练动态方差这一此前较少探索的维度。
- **方法可解释**：基于嵌入索引的变异性提出 SEIs，概念清晰，并与 EigenScore 等内部状态指标建立了直接联系。
- **工程高效**：EES 避免显式特征分解，将 EigenScore 计算复杂度从 O(N³) 降至 O(N²)，实际速度提升约 2 倍，使训练内监控可行。
- **实验系统性强**：从现象验证到方法设计再到多域评估，覆盖多个模型规模（1B–8B）和领域，消融实验较完整。
- **实用性强**：SenD 以持续训练方式可直接用于现有模型微调/适配，额外计算开销仅约 11%，且可与 RAG 等事后方法叠加使用。

# 不足与局限

- **训练阶段覆盖有限**：SenD 仅在持续训练中验证，未应用于大规模从头预训练；作者也承认这是计算限制所致，其效果在预训练场景下仍未知。
- **计算资源描述不透明**：未提供 GPU 型号、数量和总训练算力，难以评估方法的实际计算门槛和能耗。
- **缺乏同阶段 baseline**：SenD 是首个训练中的幻觉缓解方法，没有与其它训练期正则化（如 dropout 变体、对比学习等）直接比较，公平竞争证据不足。
- **性能提升不一致**：HaluEval 相关指标在 SenD 与普通训练间无差异；FactScore 在 Pythia 1B 上非常低（约0.05–0.07），说明对小模型的事实性改善有限。
- **近似失真风险**：EES 输出尺度与 EigenScore 不同，且依赖归一到 [0,1] 的谱区间，若嵌入分布变化较大可能影响近似精度；文中未讨论极端情况下 EES 的鲁棒性。
- **超参敏感性**：K 和 Threshold 需要针对模型大小调整（如 Llama 8B 需 K=30%），作者虽做了消融，但未提供自动选择或自适应策略。
- **泛化性风险**：SEIs 的计算基于特定跟踪子集（如 HELM 的 Wikipedia 文本），对领域偏移较大的数据（如代码、医学）可能不够稳定，文中对跨域 SEIs 的迁移性缺乏深入分析。

（完）
