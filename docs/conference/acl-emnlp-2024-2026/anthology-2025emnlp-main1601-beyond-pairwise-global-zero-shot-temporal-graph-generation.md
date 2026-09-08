---
title: "Beyond Pairwise: Global Zero-shot Temporal Graph Generation"
title_zh: 超越成对分类：全局零样本时序图生成
authors: "Alon Eirew, Kfir Bar, Ido Dagan"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1601.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 直接生成文档级时序图并通过约束优化维护时间一致性
tldr: 时序关系抽取多采用成对分类，既低效又难以保证文档时间图全局一致。该文提出零样本全局时序图生成方法，直接一步生成完整文档事件时间图，再施加时间约束优化以修正关系、维护传递性与无环性。同时引入OmniTemp新基准，实验显示全局生成在零样本时序抽取中具有较强一致性优势。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 763, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 995, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 764, \"height\": 1184, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 722, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 759, \"height\": 1173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1640, \"height\": 1408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1139, \"height\": 1006, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1648, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1601/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1610, \"height\": 848, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 535, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1164, \"height\": 1036, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 613, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 645, \"height\": 140, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 804, \"height\": 147, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 587, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1601/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1333, \"height\": 778, \"label\": \"Table\"}]"
motivation: 成对时序分类忽略全局一致性且计算效率低，限制大模型时序抽取能力。
method: 在单次解码中生成文档完整时序图，并用时间约束优化进行全局一致性推理。
result: 在OmniTemp等测试上验证了全局生成方法的零样本时序关系抽取能力。
conclusion: 时序图生成加约束优化为时间感知抽取提供高效且全局一致的方案。
---

## Abstract
Temporal relation extraction (TRE) is a fundamental task in natural language processing (NLP) that involves identifying the temporal relationships between events in a document. Despite the advances in large language models (LLMs), their application to TRE remains limited. Most existing approaches rely on pairwise classification, where event pairs are classified in isolation, leading to computational inefficiency and a lack of global consistency in the resulting temporal graph. In this work, we propose a novel zero-shot method for TRE that generates a document’s complete temporal graph in a single step, followed by temporal constraint optimization to refine predictions and enforce temporal consistency across relations. Additionally, we introduce OmniTemp, a new dataset with complete annotations for all pairs of targeted events within a document. Through experiments and analyses, we demonstrate that our method outperforms existing zero-shot approaches and offers a competitive alternative to supervised TRE models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **时序关系抽取（TRE）** 是 NLP 中的基础任务，目标是识别文档中事件之间的时序关系（如 before、after、equal、vague 等）。
- **核心问题**：现有方法主要采用**成对分类（pairwise classification）**范式，即对每个事件对独立分类，存在两大缺陷：
  - **计算效率低**：对 n 个事件需进行 O(n²) 次推理调用，在 LLM 场景下成本极高。
  - **缺乏全局一致性**：独立分类忽略了文档的整体时序结构，容易产生矛盾或冲突的时序图。
- 尽管 LLM 具有强大的语言理解和时序常识推理能力，但其在零样本 TRE 中的应用此前被认为效果不佳。
- **本文核心主张**：突破成对范式的局限，提出**全局零样本时序图生成**方法——让 LLM 在单次推理中直接生成文档的完整时序图，再通过时序约束优化来保证全局一致性，从而在零样本条件下实现可媲美监督模型的性能。

## 2. 提出的方法论

**核心思想**：使用 LLM 一次性生成整个文档所有事件对的时序关系图，而非逐对分类。

**关键技术细节（GlobalConsistency 方法）**：

1. **提示结构（两阶段提示）**：
   - 首先提示模型生成**自由形式的文档事件时间线摘要**，引导模型在做出具体分类前先建立对事件顺序的整体理解。
   - 然后指示模型对**所有事件对**预测时序关系，输出格式为 **DOT 图语言**（事件为节点、关系为边），便于解析且抑制多余文本。
   - 对于事件数过多的文档，将完整事件对集合均匀分割后分批处理，每批共享相同指令与全文标记事件，最后合并结果。

2. **多次采样与分布聚合**：
   - 每个文档运行模型 M=5 次（实验表明 5 次后性能饱和）。
   - 将每次生成的标签转化为 one-hot 向量并求和归一化，得到每个事件对上的标签分布 pᵢⱼ。

3. **时序约束优化（ILP）**：
   - 定义二元决策变量 Iᵣ(i,j)∈{0,1}，表示事件对 (eᵢ,eⱼ) 是否被赋予关系 r。
   - 目标函数为最大化模型预测分布的加权和：
     max Σᵢ≠ⱼ Σᵣ Iᵣ(i,j) · dᵣⁱʲ
   - 约束条件：
     - **唯一性**：每对事件只能有一个关系标签；
     - **对称性**：反向事件对需满足互逆关系（如 before 对应 after）；
     - **传递性**：若 A→B、B→C，则 A→C 必须成立（基于 Allen 传递律）。
   - 使用 Gurobi 优化器求解，输出全局一致的最终时序图。

4. **消融变体设计**：
   - **ZSL-Global**：单次直接生成完整图，无时间线提示、无后处理。
   - **ZSL-Timeline**：有时间线提示，但无 ILP 后处理。
   - **SelfConsistency**：无 ILP，仅用 5 次生成的多数投票。

## 3. 实验设计

**数据集**：

| 数据集 | 标注范围 | 关系类型 | 说明 |
|---|---|---|---|
| **OmniTemp（新构建）** | 全部事件对（完整） | 4 类（before/after/equal/vague） | 30 篇新闻摘要，470 个事件，3,483 个关系；采用 MATRES 简化标注规范；3 名非专家标注者，多数投票定标签，Kappa=0.72 |
| **MATRES** | 仅相邻句事件对 | 4 类 | 部分标注 |
| **TB-Dense** | 仅相邻句事件对 | 6 类 | 部分标注 |
| **NT-6**（NarrativeTime 处理版） | 全部事件对（完整） | 6 类 | 移除 overlap 关系以适配约束优化；每篇随机抽取 18 个事件以适应上下文限制 |

**对比方法**：
- **监督基线**：RoBERTa（Tan et al.）、Bayesian-Translation（Tan et al.）、Bayesian + Constraints。
- **零样本基线**：CoT 方法（Yuan et al.，2023）——最强的零样本成对基线，用 GPT-4o 和 DeepSeek-R1 复现。
- **本文方法**：ZSL-Global、ZSL-Timeline、SelfConsistency、GlobalConsistency。

**指标**：
- **F1**（依据 Ning et al. 2019 定义，vague 不计入真正例）。
- **时序不一致性（TI）**：应用传递闭包后计数矛盾边数。

**额外实验**：
- 在其他 LLM（DeepSeek-V3、GPT-o3-mini、Llama-3.1 405B、Llama 3.3 70B、Gemini Flash 2.0）上评估 GlobalConsistency。
- 在 MAVEN-ERE 数据集（Wikipedia 领域）上评估方法的跨域迁移能力。

## 4. 资源与算力

- **监督模型训练**：在单个 A100 GPU 上训练，每个完整训练 episode 约需 **1 到 20 小时**（取决于训练集大小），总共进行 50 epochs，并做了超参数网格搜索。
- **LLM 推理成本**：
  - GlobalConsistency：每个测试集 5 次完整时序图生成。例如：MATRES 约 6–9 美元，TB-Dense 约 9–17 美元，NT-6 约 15–23 美元，OmniTemp 约 12–23 美元。
  - CoT 基线：成本约为 GlobalConsistency 的 **7 倍**（如 NT-6 使用 DeepSeek-R1 时：CoT 为 21 美元，Global 为 23 美元；但时间上 CoT 为 838 分钟 vs. Global 为 110 分钟）。
- **总研究成本**：使用 OpenAI、Google 和 Together.ai 的 LLM API，总计约 **400 美元**。
- **标注成本**：OmniTemp 标注总耗时 85 小时，按每人每小时 15 美元支付。

## 5. 实验数量与充分性

**主要实验规模**：
- 4 个数据集 × 2 个 LLM（GPT-4o、DeepSeek-R1）× 多种方法，构成 Table 2 的主结果。
- 3 组核心消融实验（ZSL-Global、ZSL-Timeline、SelfConsistency vs. GlobalConsistency），验证了各组件贡献。
- 2 个分析实验（事件对距离影响、标签一致性影响）。
- 额外模型评估：6 个其他 LLM 的对比实验。
- 额外数据集实验：MAVEN-ERE 验证集上的跨域验证。

**关于充分性的评估**：
- **优点**：实验覆盖多个数据集（部分标注 vs. 完整标注，新闻 vs. Wikipedia），多个模型系列，并有监督模型作为上界参照，整体较为充分。每种消融配置用了 5 次生成的均值与标准差（如 ZSL-Global 和 ZSL-Timeline 报告了 ± 标准差），透明度较好。
- **不足**：CoT 基线在每个数据集上只跑了一次评估（未做多次平均），自述原因是预算有限；主结果表中的 SelfConsistency 和 GlobalConsistency 也只各跑了一次（未多次取均值），这些在统计可靠性上略弱。另外，CoT 在 MATRES/TB-Dense 上未报告 TI 指标（因为只对黄金标注的事件对预测，无法构建完整图），所以与全局方法的对比在这两个数据集上不完整。NT-6 上随机抽取 18 个事件，可能引入采样偏差。

## 6. 主要结论与发现

1. **全局生成显著优于成对零样本基线**：在 GPT-4o 上，GlobalConsistency 除 TB-Dense 外全面超越 CoT 基线；使用 DeepSeek-R1 时在全书密集标注数据集（NT-6：64.1 vs. 57.9；OmniTemp：79.2 vs. 78.4）上优于 CoT。
2. **接近监督模型性能**：DeepSeek-R1 驱动的 GlobalConsistency 在 NT-6（64.1 vs. 65.6）和 OmniTemp（79.2 vs. 80.7）上接近 Bayesian + Constraints 监督模型，且 TI 为 0，图一致性更优。
3. **时间线提示有帮助**：ZSL-Timeline 普遍优于 ZSL-Global，说明先构建自由形式时间线再分类可提升效果。
4. **ILP 约束优化的价值显著**：GlobalConsistency 在所有数据集上 TI=0，并在大多数配置下优于 SelfConsistency（纯多数投票），证明全局约束推理优于孤立聚合。
5. **事件数量影响性能**：文档事件数越多，GlobalConsistency 性能下降越明显（图 2），说明全局方法对信息负载更敏感。
6. **标注距离范围影响评估公平性**：在仅标注相邻句子的数据集上评估零样本模型可能产生误导；模型在相邻句子对的性能表现系统性优于长距离对，但 CoT 在 OmniTemp 上各距离表现较平均——这可能反映了不同方法对局部线索的依赖差异。
7. **数据集标注不一致影响零样本评估**：MATRES 与 TB-Dense 在同一个语料上的标签严重不一致（尤其在 vague 和 equal 关系上），由于零样本模型没有学习特定数据集的标注偏差，这解释了部分性能差距——提示用部分标注或不一致的数据集评估零样本方法可能不够可靠。

## 7. 优点

- **范式创新**：突破传统 pairwise 分类，将 TRE 重构为单步文档级图生成任务，避免了 O(n²) 推理调用。
- **方法有效性**：两阶段提示（时间线推理 + 图生成）+ DOT 图输出 + 多轮自一致性 + ILP 约束优化的组合设计合理，且每个组件均有消融来验证。
- **全局一致性保障**：ILP 显式编码唯一性、对称性、传递性约束，生产的时序图传递不一致性为 0，对下游时间线应用至关重要。
- **新数据集贡献**：构建 OmniTemp，是少数对全部事件对进行四类时序关系标注的文档级资源，填补了完全标注数据集的空白。
- **深刻的评估分析**：论文讨论了标注范围（相邻句子 vs. 全文）和数据标注不一致对零样本评估带来的问题，对后续研究具有方法学价值。
- **成本视角完整**：对比了时间、金钱成本，证明全局方法相比 CoT 基线成本大幅降低（约 7 倍差距）。

## 8. 不足与局限

- **数据污染风险**：GPT-4o、DeepSeek-R1 等闭源模型的训练数据不透明，MATRES、TB-Dense、NarrativeTime 测试集可能已出现在训练语料中。作者自行构建的 OmniTemp 不受此影响，但其他数据集的结果无法彻底排除该偏差。
- **长距离关系仍不稳定**：即使有自一致性缓解随机性，对于长距离依赖或模糊的事件关系，模型输出仍可能不一致。
- **全局方法对事件数量敏感**：文档事件越多性能下降越明显（可能因跨度的注意力分散或上下文长度限制），实际应用中可能制约其规模。
- **计算成本仍未彻底解决**：虽然比成对方法便宜得多，但在大文档上的多次采样生成依然耗时耗钱。
- **OmniTemp 规模有限**：只有 30 篇新闻摘要，覆盖面有限；且来自单一领域（新闻）、单一语言（英语），泛化性未经证实。
- **NT-6 的局限**：随机抽 18 个事件改变了文档的事件集，可能影响全局结构评估和传递性效果，并非对 NarrativeTime 的完整评估。
- **标注质量问题**：虽然 Kappa=0.72 属高度一致，但非专家标注和 majority vote（平票即 vague）仍可能造成噪声；对 "salient events" 的选择本身就有主观性。
- **CoT 基线的成本限制**：由于预算，某些实验只运行一次，统计显著性验证不足。

（完）
