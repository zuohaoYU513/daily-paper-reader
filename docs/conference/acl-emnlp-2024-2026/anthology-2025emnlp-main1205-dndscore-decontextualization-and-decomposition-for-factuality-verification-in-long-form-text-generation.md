---
title: "DnDScore: Decontextualization and Decomposition for Factuality Verification in Long-Form Text Generation"
title_zh: DnDScore：通过去上下文化与分解对长文本生成进行事实性验证
authors: "Miriam Wanner, Benjamin Van Durme, Mark Dredze"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1205.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 对LLM长文本生成做分解与去上下文化后逐条考证，直接面向生成与源文本的事实一致性评测
tldr: 长文本事实核查中的分解与去上下文化虽被分别使用，但其冲突关系未被系统研究。DnDScore将声明拆分为原子事实，同时补充必要上下文以便脱离原文独立验证，并据此对生成内容打分。实验表明该方法能更准确地识别长文本中缺乏依据的句子，为LLM幻觉评测提供了新范式。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1205/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1570, \"height\": 668, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1589, \"height\": 1369, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 626, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1473, \"height\": 914, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1332, \"height\": 2383, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1194, \"height\": 1895, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1205/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1202, \"height\": 2400, \"label\": \"Table\"}]"
motivation: 长文本事实核查需拆分与补充上下文，但二者互相矛盾，缺少统一建模，生成的验证不够可靠。
method: 首先分解子声明，再对每个子声明去上下文化，使其脱离原文也可验证，最后聚合得到事实性分数。
result: 在长文本生成上的实验显示所提方法比已有基线更准确可靠，能够有效识别幻觉内容。
conclusion: 合理设计分解与去上下文化能提高LLM生成事实核查的有效性。
---

## Abstract
The decompose-then-verify strategy for verification of Large Language Model (LLM) generations decomposes claims that are then independently verified. Decontextualization augments text (claims) to ensure it can be verified outside of the original context, enabling reliable verification. While decomposition and decontextualization have been explored independently, their interactions in a complete system have not been investigated. Their conflicting purposes can create tensions: decomposition isolates atomic facts while decontextualization inserts relevant information. Furthermore, a decontextualized subclaim presents a challenge to the verification step: what part of the augmented text should be verified as it now contains multiple atomic facts? We conduct an evaluation of different decomposition, decontextualization, and verification strategies and find that the choice of strategy matters in the resulting factuality scores. Additionally, we introduce DnDScore, a decontextualization aware verification method that validates subclaims in the context of contextual information.

---

## 论文详细总结（自动生成）

以下是对论文《DNDS CORE : Decontextualization and Decomposition for Factuality Verification in Long-Form Text Generation》（EMNLP 2025 Main）的详细中文总结。

## 1. 核心问题与整体含义（研究动机和背景）

- 在长文本生成的事实性评估中，主流的“分解后验证”（decompose-then-verify）框架先将模型生成文本分解为原子性子声明（atomic subclaims），再逐条与可信来源（如 Wikipedia）进行核对。
- 已有工作分别验证了“分解”和“去上下文化”（decontextualization）的独立价值：分解用于提取孤立原子事实，去上下文化则用于补充必要的实体与背景信息，使子声明可脱离原文独立核实。
- 然而，两者的交互尚未被系统研究，并且存在本质性冲突：
  - 分解强调“原子性”，而去上下文化会不断插入相关信息，使原本孤立的原子事实被“扩写”为包含多个事实的文本，导致“到底该验证哪一部分”的歧义。
  - 顺序执行“分解→去上下文化”或“去上下文化→分解”都会引入冗余、失焦或信息重复等问题，可能使事实性分数虚高或失真。
- 论文的核心问题是：如何在同一条验证管线中同时处理分解和去上下文化的相互影响，并设计一种“在上下文语境中验证原子子声明”的分数，从而获得更可靠的长文本事实性评估。

## 2. 论文提出的方法论

### 2.1 总体框架

- 延续 decompose-then-verify 框架，但显式建模“分解”和“去上下文化”之间的交互。
- 提出两种新的系统组件：
  1. **DnD**（Decontextualization and Decomposition）：一种“联合分解 + 去上下文化”的提示方法，通过一次 LLM 调用同时输出两组对应文本：
     - 子声明集合（原子性较高）
     - 每个子声明对应的去上下文化版本（补充必要语境）
  2. **DNDS CORE**（Decomposition and Decontextualization Score）：一个“去上下文化感知”的验证方法，它同时接收参考文档、待验证的原子子声明、以及该子声明的去上下文化形式作为上下文，要求验证器判断**指定的原子子声明**是否被参考文档支持。

### 2.2 方法与关键实现细节

- **分解方法（DR-ND）**：沿用 Wanner et al. (2024) 提出的、基于 Russellian 和 Neo-Davidsonian 理论的提示式分解方法，使用 `gpt-3.5-turbo-instruct` 模型。
- **去上下文化方法（Molecular Facts）**：采用 Gunjal and Durrett (2024) 的两步提示方法：
  1. 先用 LLM 识别句中歧义（如指代、同名实体等），提取歧义字典；
  2. 再用 LLM 根据这些歧义信息对句子做去上下文化。使用 `GPT-4o mini`。
- **联合方法 DnD**：参考 Molecular Facts 的歧义标注和 DR-ND 的分解示例，设计统一提示，一次性输出“子声明列表 + 歧义解释 + 子声明/去上下文化版本对照列表”，从而减少顺序执行造成的两次独立 LLM 调用与信息丢失。
- **验证方法 FA CT SCORE 基线**：采用原版 FActScore（Min et al. 2023），其验证器为 Inst-LLAMA（基于 LLaMA 7B 在 Super Natural Instructions 上训练），并使用“检索 + NPM”的设定进行验证。
- **验证方法 DNDS CORE**：对原 FActScore 提示进行改造——提示中额外加入“去上下文化声明”作为上下文，让验证器“在给定上下文的条件下”判断“原子子声明”的真假。这样做既能利用语境消除指代歧义，又不会被额外插入的可能错误内容所干扰。

### 2.3 评测顺序组合

论文比较了多种“分解/去上下文化”的组合方式：
1. Decomp Only（仅分解）；
2. Decomp → Decontext（先分解后去上下文化）；
3. Decontext → Decomp（先去上下文化后分解）；
4. DnD Subclaim（联合方法输出的子声明集合）；
5. DnD Decontext（联合方法输出去上下文化版本集合）；
6. DNDS CORE 在不同上下文条件下的验证（原始句子作为上下文、去上下文化的句子作为上下文、DnD 的去上下文化子声明作为上下文等）。

## 3. 实验设计

### 3.1 数据集 / Benchmark

- **FActScore 数据集**：来自 Min et al. (2023)，包含 12 个不同规模和来源的语言模型生成的维基百科式人物传记，实体覆盖从罕见到高频、多种国籍；以对应实体的 Wikipedia 页面作为参考来源。
- **LFQA 数据集（ELI5）**：来自 Chen et al. (2023a)，是 Reddit “Explain Like I’m Five” 上的长形式问答测试集；参考来源由人工、模型或随机方式检索；论文使用 Tang et al. (2024) 收集的测试划分。

### 3.2 对比方法

- **基线分解验证方法**：FActScore（分解后独立验证）。
- **顺序组合方法**：Decomp → Decontext、Decontext → Decomp。
- **联合方法**：DnD Subclaim / DnD Decontext。
- **上下文验证方法**：DNDS CORE（用于上述各种组合产生的原子子声明+上下文）。
- **消融/扩展设置**：对所有方法额外使用 CORE（Jiang et al. 2024）进行子声明去重，报告去重后的事实性分数。

### 3.3 主要评价指标

- **DECOMP SCORE**：衡量分解产生的子声明与原句的蕴含一致性（via NLI），即生成的子声明有多少被原句支持。
- **FActScore**：传统“分解后验证”分数。
- **DNDS CORE**：使用上下文验证的分数。
- **CORE 去重后的平均子声明数**：用于分析冗余现象。

## 4. 资源与算力

- 论文在附录 A.6 中提到：所有分解/去上下文化实验均在带有 Quadro RTX 6000 的 GPU 集群上运行，估计总耗时约 **400 GPU-hours**。
- 具体使用的 GPU 数量、并行配置、推理细节未明确给出；也未提到 DnD、DNDS CORE 的训练过程（因为它们都是基于提示的零样本方法），因此算力主要用于大量 LLM 调用和验证器推理。

## 5. 实验数量与充分性

### 5.1 实验覆盖

- 在两种数据场景（FActScore 传记和 LFQA）上进行了测试；
- 每种场景覆盖 12 个语言模型生成（FActScore 部分）；
- 对比了 5 种分解/去上下文化组合 × 2 种验证方式（FActScore 和 DNDS CORE）；
- 额外使用 CORE 进行了全子声明集的去重过滤分析；
- 提供了定量判断变化分析（如“false→true”、“true→false”的比例、代词替换的影响）；
- 提供了定性案例分析（表 4 中的多个具体实例）；
- 在 LFQA 数据上进行了 100 条子声明级别的人工评估（附录 C.3）；
- 在附录中给出全部 LLM 分模型的全表结果（12 行 × 多种设置），以及 DECOMP SCORE 分模型结果。

### 5.2 充分性与公平性评价

- **优点**：实验设计较为系统和透明，既包含定量统计、又包含人工标注和具体案例；对 FActScore 和 LFQA 两类长文本都进行了覆盖；对验证框架中每一步的贡献都做了拆分与对比。
- **潜在不足**：
  - 人工评估样本量较小（100 条），且仅针对判断发生翻转的实例；
  - 数据集类型偏向“人物传记 + 科普问答”，领域多样性有限；
  - 验证所用参考文档均为预提供的静态来源，没有评测实际检索错误对 DNDS CORE 的影响；
  - 论文未报告 DNDS CORE 在不同提示模板、不同验证器（如 GPT-4 等）下的鲁棒性，只使用了 Inst-LLAMA。

## 6. 主要结论与发现

- 分解与去上下文化之间的交互会显著影响最终事实性分数，**选择何种组合方式至关重要**。
- 仅使用“原子子声明”会导致验证因缺少上下文而失败；仅使用“去上下文化声明”会因包含多个原子事实而模糊待验证对象，且新增信息错误时可能掩盖原子事实的正确性。
- DNDS CORE 通过“在上下文约束下验证指定原子子声明”有效解决上述矛盾：
  - 能够避免去上下文化引入的错误信息影响原子事实本身（例如 Fuerza Guerrera 的例子）；
  - 能够利用指代消解信息提高验证准确率；
  - 判断从 false→true 的比例远高于 true→false（16.25% vs. 3.26%），说明补足上下文主要是让“假阴性”变为“真阳性”，而不是引入更多误判。
- 冗余分析显示：
  - 去上下文化会带来大量重复事实；使用 CORE 去重后事实性分数整体变化较小（多数在 2% 内），但 Decontext → Decomp 方法在去重后分数下降约 4%，说明顺序先去上下文化再分解会造成重复的必须上下文，稀释事实性分数。
- 在两种数据（传记与 QA）上，DNDS CORE 都比对应 FActScore 设置得分更高（例如 FActScore 数据中最高 61.51% vs. FActScore 的 45.97%），且 LLM 排名顺序保持稳定，说明方法在提高验证准确性的同时不会混淆模型之间的相对事实性排序。

## 7. 优点

- **问题切入有价值**：首次系统研究分解与去上下文化在完整验证管线中的交互，指出传统 decompose-then-verify 中“有上下文缺失”和“有上下文但无法定位被验证原子事实”的矛盾。
- **方法引入合理**：DnD 通过联合提示一次获得原子子声明及其上下文版本，减轻顺序调用带来的信息重复/丢失；DNDS CORE 将“上下文”作为验证条件，而非仅扩展待验证文本，设计上有效避免了“错误上下文掩盖正确子声明”的问题。
- **实验设计丰富**：组合了多种分解/去上下文化顺序、两种验证器、去重过滤、定量判断变化分析、定性案例与人工评估，分析较全面、可解释性强。
- **分析深入细致**：包括“判断变化方向和比例”、“代词替换与 wrong→right 之间的关系”、CORE 去重后的冗余评估，能帮助读者看清分数变化来源。
- **良好展示了应用价值**：DNDS CORE 在传记和 LFQA 两个不同来源的长文本上均能提高验证可靠性，且不会改变模型相对排序。

## 8. 不足与局限

- **应用领域有限**：仅在人物传记和 ELI5 类长回答上实验，未测试新闻、多实体复杂叙述、科学文献、多 hop 事实验证等场景。论文也承认未考虑观点性、争议性声明。
- **检索过程缺失**：参考文档被当作固定已知来源，未与真实的信息检索（IR）管线结合；生产中若检索到错误文档，DNDS CORE 的表现可能与当前结果存在较大差异。
- **验证器单一**：DNDS CORE 的最终验证仍基于 Inst-LLAMA，未对比 GPT-4、其他小型验证器等；DnD 模块与验证模块使用不同 LLM，可能引入模型间的偏差。
- **提示工程依赖较高**：DnD 和去上下文化提示中包含较多示例与歧义定义，若应用到其他域、语言或更细粒度场景，可能需要重新调整提示。
- **人类评估规模较小**：论文只对 100 条 LFQA 中判断翻转的样本做了人工标注，无法全面反映方法在所有样本上的一致性表现。
- **去上下文化过程仍可能引入幻觉**：DnD 和 Molecular Facts 都会补充额外信息，尽管 DNDS CORE 能缓解该问题，但如果上下文中的错误信息误导验证器，仍可能产生错误判断。论文中约有 3% 的 case 存在这类风险。
- **未对端到端完整系统做大规模公正性评测**：例如缺少最终 DNDS CORE 与人工评分的整体相关度统计报告（除少量实例分析），也未与其他近期的开源/商用验证器（如 VERISCORE、Self-Checker、MiniCheck）进行统一基准下的对比。

（完）
