---
title: "The Digital Dunning-Kruger Effect: Decoupling Hallucinations via Geometric Hidden-state Observation for Semantic Truthfulness"
title_zh: 数字达克效应：通过几何隐藏状态观察解耦幻觉以实现语义真实性
authors: "Yueheng Mao, Min Yu, Gengwang Li, Jianguo Jiang, Gang Li, Meng Zhang, Zhen Xu, Weiqing Huang, Ming Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.993.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 提出GHOST，一种基于隐藏状态几何的白盒大模型幻觉检测框架
tldr: 针对现有幻觉检测方法在精度与开销之间的权衡问题，论文提出GHOST，一种高效的白盒幻觉检测框架。GHOST利用隐藏状态几何特征，主要识别由内部推理不稳定导致的迷惑型幻觉，并补充捕捉层间过早收敛的顽固型幻觉。该方法降低了检测成本，同时提升了检测准确性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long993/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long993/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1557, \"height\": 788, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 1914, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1663, \"height\": 625, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1659, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1490, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 800, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long993/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1500, \"height\": 672, \"label\": \"Table\"}]"
motivation: 现有幻觉检测方法中，黑盒方法精度高但计算昂贵，白盒方法难以检测顽固幻觉，存在权衡。
method: 提出GHOST框架，通过对LLM隐藏状态进行几何观测，解耦并检测迷惑型和顽固型幻觉。
result: 在保持较高准确率的同时显著降低计算开销，能有效检测两类幻觉。
conclusion: GHOST为白盒幻觉检测提供了一种高效且可解释的新方案。
---

## Abstract
Large Language Models (LLMs) often generate overconfident yet factually incorrect hallucinations. Current detection paradigms suffer from a trade-off between the high accuracy of computationally expensive black-box methods and the inability of white-box methods to detect stubborn hallucinations. To bridge this gap, we propose GHOST (Geometric Hidden-state Observation for Semantic Truthfulness), an efficient white-box framework for hallucination detection in LLMs. We primarily target confused hallucinations marked by internal reasoning instability, while also capturing stubborn hallucinations characterized by premature layer-wise convergence as a complementary signal. By integrating internal geometric dynamics with output probability distributions, GHOST constructs a high-dimensional feature space for non-linear truthfulness classification. Extensive evaluations on FinanceBench, RAGTruth, HaluEval, and PopQA show that GHOST outperforms white-box baselines and achieves competitive black-box performance while reducing computational overhead by over 90%, offering a robust solution for real-time detection.

---

## 论文详细总结（自动生成）

# 《The Digital Dunning-Kruger Effect: Decoupling Hallucinations via Geometric Hidden-state Observation for Semantic Truthfulness》详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究问题**：大型语言模型（LLM）在生成文本时经常产生**过度自信但事实错误**的幻觉（hallucination），严重阻碍其在医疗、法律、金融等高风险领域的实际部署。
- **现有检测范式的局限**：
  - **黑盒方法**（如 SelfCheckGPT、FactScore）：通过多样本采样或外部验证实现高精度，但计算开销和推理延迟巨大，难以实时部署。
  - **白盒方法**（如语义熵、INSIDE、LI）：依赖输出 logits 或单一内部指标，指标粒度粗糙，难以捕捉模型对错误知识的过度自信——即无法检测“顽固性幻觉”（stubborn hallucinations）。
- **核心洞见**：论文提出“数字达克效应”（Digital Dunning-Kruger Effect）的概念，认为 LLM 的幻觉类似于认知心理学中的达克效应——模型对自身能力存在虚高评估。具体表现为两种机制：
  - **顽固型幻觉（Stubborn Hallucinations）**：模型在缺乏事实依据的情况下过早收敛于错误结论，具有高认知过度自信，表现为层间提前收敛。
  - **迷惑型幻觉（Confused Hallucinations）**：模型在解决相互冲突的语义信号时表现出内部推理不稳定，表现为隐藏状态轨迹的剧烈波动。
- **研究目标**：填补黑盒与白盒方法之间的鸿沟，提出一种既高效又准确的白盒幻觉检测框架。

## 2. 方法论：核心思想、关键技术细节与公式

### 2.1 核心思想

GHOST 将 LLM 的推理过程概念化为高维语义流形上的动态潜在轨迹，通过量化隐藏状态在层间的几何演化特征来解耦幻觉。其核心假设是：
- **真实回答**：占据狭窄流形，轨迹平滑，语义传播稳定。
- **幻觉回答**：呈现分叉——一部分与真实轨迹聚类紧密（顽固型幻觉的“超稳定性”），另一部分在网络中间层（约50%相对深度）开始显著偏离（迷惑型幻觉）。

### 2.2 四大特征

GHOST 构建一个四维特征向量 **v = [V_turb, V_stub, V_ent, V_div]**，具体包括：

**（1）表征湍流（Representation Turbulence, V_turb）**
- 基于认知失调理论，量化相邻层间隐藏状态的方向偏离程度。
- 对第 i 个 token，计算其跨层平均余弦偏差：
  - v_turb⁽ⁱ⁾ = (1/(L_end − L_start)) · Σ [1 − (h_l⁽ⁱ⁾ · h_{l+1}⁽ⁱ⁾) / (‖h_l⁽ⁱ⁾‖ · ‖h_{l+1}⁽ⁱ⁾‖)]
- 最终特征：V_turb = (1/N) Σ v_turb⁽ⁱ⁾
- **高 V_turb 表示内部冲突与推理不稳定**，是迷惑型幻觉的计算代理。

**（2）顽固度（Stubbornness, V_stub）**
- 基于达克效应的“虚假优越感”，量化中间层状态与最终层表示之间的相似度：
  - v_stub⁽ⁱ⁾ = (1/(L_end − L_start + 1)) · Σ (h_l⁽ⁱ⁾ · h_final⁽ⁱ⁾) / (‖h_l⁽ⁱ⁾‖ · ‖h_final⁽ⁱ⁾‖)
- 最终特征：V_stub = (1/N) Σ v_stub⁽ⁱ⁾
- **高 V_stub + 低 V_turb 构成顽固型幻觉的独特几何指纹**——模型过早收敛至错误表示。

**（3）预测熵（Predictive Entropy, V_ent）**
- 基于 Top-K（K=10）候选 token 的概率分布计算香农熵：
  - V_ent = −Σ p_k · log p_k
- 经典的输出不确定性度量，但仅依赖输出概率。

**（4）语义发散度（Semantic Divergence, V_div）**
- 衡量 Top-K 候选 token 在嵌入空间中的几何离散程度（而非 token 身份差异）：
  - V_div = (1/(K(K−1))) · Σ Σ (1 − e_i · e_j / (‖e_i‖ · ‖e_j‖))
- 用于区分同义词替换与真正的语义混淆——同义候选得分低，语义上遥远的不确定预测得分高。

### 2.3 聚合与分类

- 采用 **“先计算后平均”** 策略：先对每个 token 计算几何指标，再对序列长度 N 取平均，确保覆盖整个生成链。
- 使用**非线性分类器**：对比了逻辑回归、SVM（RBF）、XGBoost 和随机森林，最终选择**随机森林**（750棵树，最大深度40），因其对几何流形中的高维非线性特征交互建模能力最强。
- 特征提取完全集成在模型的**单次前向传播**中，无需结构修改或额外采样。

## 3. 实验设计：数据集、基准与对比方法

### 3.1 数据集（Benchmarks）

| 数据集 | 规模 | 知识领域 |
|--------|------|----------|
| **HaluEval**（QA子集） | 10,000 样本 | 通用/开放域 |
| **PopQA** | 1,400 样本 | 长尾/实体中心 |
| **FinanceBench** | 1,200 样本 | 金融推理（专业领域） |
| **RAGTruth** | 2,500 样本 | 检索增强生成 |

- 所有数据集采用**分层 80/20 训练/测试划分**。
- 使用 **gpt-oss-120b** 作为自动标注器生成二元标签，并经过人工验证（Cohen's κ = 0.82），保证标注质量。

### 3.2 评估模型

覆盖四种架构多样化的 LLM：
- **Qwen2.5-1.5B-Instruct**（小模型代表）
- **Gemma-3-4B-IT**（不同架构，GeGLU 激活）
- **Mistral-7B-Instruct-v0.3**（7B 行业标准）
- **DeepSeek-R1-Distill-Qwen-7B**（推理增强模型）

### 3.3 对比方法

- **白盒基线**：Predictive Entropy、INSIDE、LI（层间信息缺失）、LapEigvals（注意力图谱拉普拉斯谱）、UTH、HIDE、LoRA probe。
- **黑盒基线**：SelfCheckGPT（N=5 采样，deberta-v3-large-mnli 作为蕴含评分器）。

### 3.4 评估指标

- **AUPRC**（主要指标，阈值无关，适用于类别不平衡）
- **F1-score**（验证阶段最优阈值下报告）

## 4. 资源与算力

论文附录中明确说明了实验环境：

- **硬件**：4 × NVIDIA GeForce RTX 3090 GPU（24GB VRAM）；2 × Intel Xeon Gold 6326 CPU。
- **软件**：Python 3.10，HuggingFace Transformers v4.40.0。
- **推理设置**：贪心解码（temperature=0），batch size=1，模拟实时流式场景。
- **总 GPU 时间**：跨 4 个数据集 × 4 个基础模型的特征提取约 **24 小时**。
- **效率对比**：GHOST 附加延迟仅 0.08s–0.18s（约为生成时间的 4.3%–4.6%）；
- **SelfCheckGPT** 附加延迟为生成时间的约 400%（如 Qwen2.5-1.5B 需额外 7.28s）。

## 5. 实验数量与充分性分析

### 实验组数量

| 实验类型 | 具体内容 | 规模 |
|----------|----------|------|
| **主实验** | 4 数据集 × 4 模型 × 10+ 方法 | 大规模全面对比 |
| **消融实验** | 逐一剔除 4 个特征组（w/o Entropy、w/o Divergence、w/o Turbulence、w/o Stubbornness） | 4 组完整实验 |
| **分类器对比** | 4 种分类器（LR、SVM、XGBoost、RF）在 Qwen2.5-1.5B 上的横向比较 | 4 组 |
| **跨数据集 OOD** | 4 个源数据集训练，评估在其余数据集上的泛化 | 12 组配置 |
| **跨模型 OOD** | 在不同模型间迁移的评估 | 隐含在主实验中 |
| **效率分析** | 4 个模型的延迟和开销对比 | 4 组 |
| **标注质量验证** | 500 样本分层子集人工评估 + 3 专家双盲评估 | 2 轮 |
| **错误分析** | 系统性检查三类失败模式 | 定性分析 |

### 充分性与客观性评价

- **优点**：覆盖多模型架构（1.5B–7B，含推理增强模型）、多领域数据集（通用、长尾、金融、RAG），对比基线涵盖主流白盒与黑盒方法；消融实验系统完整；OOD 实验揭示了泛化边界。
- **潜在不足**：
  - 数据集规模中等（PopQA 仅 1,400 样本，FinanceBench 1,200 样本），未在超大规模基准（如 TruthfulQA 全量）上验证。
  - 所有模型均为 decoder-only Transformer 架构，未覆盖 encoder-decoder 或非 Transformer 结构。
  - OOD 实验中 FinanceBench 训练迁移效果显著下降（AUPRC 最低至 0.61），说明跨领域泛化仍有局限。

## 6. 主要结论与发现

1. **数字达克效应得到实证支持**：LLM 的内部置信度常常是语义真实性的欺骗性代理——模型可能在知识不足时表现出虚高的认知自信。
2. **GHOST 显著超过白盒基线，达到与黑盒方法竞争的水平**：
   - 在 Qwen2.5-1.5B 上达到平均 AUPRC 0.9531（最佳单数据集 PopQA 0.9801）。
   - 在 DeepSeek-R1-7B 上平均 AUPRC 达 0.9819，超过 SelfCheckGPT（0.9788）。
3. **计算开销降低超 90%**：相比 SelfCheckGPT 约 400% 的附加延迟，GHOST 仅增加约 4.3%–4.6% 延迟，支持实时部署。
4. **消融实验揭示特征重要性排序**：**Turbulence 贡献最大**（去除后 AUPRC 降至 0.8862），其次为 Entropy（0.9226）、Divergence（0.9384）、Stubbornness（0.9500）。Stubbornness 作为补充信号，对提前收敛型幻觉有不可替代的识别价值。
5. **OOD 泛化具有非对称性**：训练于 PopQA/RAGTruth/HaluEval 时跨数据集迁移较稳定（AUPRC ≈ 0.80–0.89），但训练于 FinanceBench 时显著退化（低至 0.61），原因是领域专精化与幻觉先验偏移。

## 7. 优点

- **理论创新**：首次将达克效应与认知失调理论系统映射到 LLM 幻觉检测，提出了迷惑型/顽固型幻觉的新型分类法，为“高置信度错误生成”提供了理论解释。
- **方法设计巧妙**：将检测维度从静态表示推广到动态几何轨迹，通过“表征湍流”和“顽固度”两个互补特征捕捉两种不同几何机制下的幻觉。
- **效率极佳**：特征提取完全向量化，集成于单次前向传播，附加延迟极小，适合实时检测场景。
- **无需修改模型结构**：参数免费（LLM-parameter-free），无需训练模型，仅需训练一个轻量级随机森林分类器。
- **实验严谨**：包括消融、OOD 泛化、错误分析、效率分析、标注质量验证（κ=0.82 + 双盲人工评估），实验体系完整。
- **分类器选择经过系统验证**：对比了多种非线性分类器，而非随意选择。

## 8. 不足与局限

- **架构覆盖有限**：仅评估 decoder-only Transformer 架构，对 encoder-decoder 或非 Transformer 结构的适用性未知。
- **顽固型幻觉研究不充分**：论文承认缺乏专门针对“过早收敛幻觉”设计的数据集，对这类幻觉何时占主导的条件理解不足。
- **白盒访问限制**：需要访问内部隐藏状态，无法应用于闭源/API-only 场景。
- **分类法可能不完整**：当前二分法（迷惑/顽固）可能无法充分捕捉复杂推理错误（如多步逻辑谬误）。
- **OOD 泛化受领域影响显著**：跨数据集迁移性能受领域专精化影响大（FinanceBench 为极端案例），需要额外的阈值校准策略。
- **依赖标注数据**：分类器需要标注数据训练，尚未实现零样本几何指标。
- **误差模式存在固有限制**：
  - 低不稳定性幻觉（stable but wrong）仍然难以检测；
  - 复杂但正确的多步推理可能因高内部不稳定性被误判为幻觉（假阳性）。
- **数据集规模中等**：部分数据集（PopQA 1,400、FinanceBench 1,200）规模有限，统计功效可能受限。

（完）
