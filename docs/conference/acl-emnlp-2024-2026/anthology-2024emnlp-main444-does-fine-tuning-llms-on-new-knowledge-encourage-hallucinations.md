---
title: Does Fine-Tuning LLMs on New Knowledge Encourage Hallucinations?
title_zh: 在微调中引入新知识会鼓励大语言模型产生幻觉吗？
authors: "Zorik Gekhman, Gal Yona, Roee Aharoni, Matan Eyal, Amir Feder, Roi Reichart, Jonathan Herzig"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.444.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 研究监督微调注入新知识对幻觉行为的影响
tldr: 大语言模型通过监督微调接触到预训练时未学过的知识，常被认为会促使模型产生幻觉。作者以闭卷问答为平台设计可控实验，改变微调样本中新知识的占比，考察模型利用已有知识的能力。结果表明模型难以经由微调获得新的事实知识，并且接触新知识可能强化其编造不正确答案的行为。该研究对理解SFT与幻觉的因果关系、控制训练数据引入新知识具有直接意义。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 728, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1632, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 727, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main444/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1637, \"height\": 642, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1666, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1659, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1652, \"height\": 592, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1654, \"height\": 631, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1656, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 801, \"height\": 103, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main444/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1659, \"height\": 311, \"label\": \"Table\"}]"
motivation: 构造受控实验，考察SFT训练包含未知新知识是否会诱发大模型幻觉。
method: 以闭卷问答为基础，改变微调数据中新知识比例并测量模型对已有知识的利用。
result: 大模型难以通过微调吸纳新知识，且接触新知识可能增强幻觉行为。
conclusion: 监督微调阶段向模型注入新知识可能得不偿失，应在训练数据上作出约束。
---

## Abstract
When large language models are aligned via supervised fine-tuning, they may encounter new factual information that was not acquired through pre-training. It is often conjectured that this can teach the model the behavior of hallucinating factually incorrect responses, as the model is trained to generate facts that are not grounded in its pre-existing knowledge. In this work, we study the impact of such exposure to new knowledge on the capability of the fine-tuned model to utilize its pre-existing knowledge. To this end, we design a controlled setup, focused on closed-book QA, where we vary the proportion of the fine-tuning examples that introduce new knowledge. We demonstrate that large language models struggle to acquire new factual knowledge through fine-tuning, as fine-tuning examples that introduce new knowledge are learned significantly slower than those consistent with the model’s knowledge. However, we also find that as the examples with new knowledge are eventually learned, they linearly increase the model’s tendency to hallucinate. Taken together, our results highlight the risk in introducing new factual knowledge through fine-tuning, and support the view that large language models mostly acquire factual knowledge through pre-training, whereas fine-tuning teaches them to use it more efficiently.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：大型语言模型（LLM）通常先通过大规模预训练嵌入大量事实知识，再经由监督式微调（SFT）或基于人类反馈的偏好学习来实现对齐。在微调阶段，训练数据中可能包含模型在预训练阶段从未见过的新事实信息。
- **核心问题**：当模型通过微调接触这些"新知识"时，这些与其预训练知识不相符的样本，是否会诱导模型产生对已有知识的幻觉（hallucination）？这与学界广为流传的猜想一致：训练模型生成其本身知识范围内不具备的内容，可能导致其学会"编造事实"的行为。
- **研究意义**：该问题直接关系到SFT的安全使用方式和幻觉治理。如果证实引入新知识有害，那么需要在微调数据中过滤与模型已有知识不一致的样本；反之，如果模型能够自然习得新知识，则可以通过微调持续更新模型的事实知识库。本研究结论支持前者。

### 2. 论文提出的方法论

- **核心思想**：提出一种知识分类体系 **SliCK（Sampling-based Categorization of Knowledge）**，将事实三元组 (subject, relation, object) 转换成的 QA 对按照模型对其答案的掌握程度进行分层，并将"新知识"定义为模型完全无法正确回答的问题（Unknown），从而可控地测量引入新知识的效应。
- **SliCK 四层知识类别**：
  - **HighlyKnown**：模型在贪心解码时始终预测正确；
  - **MaybeKnown**：模型有时预测正确，但不总是（部分样例存在不确定性）；
  - **WeaklyKnown**：贪心解码从未预测正确，但在高温度采样时偶尔能预测正确；
  - **Unknown**：无论贪心解码、采样解码还是多种few-shot样例，模型均无法给出正确答案，即该知识对模型是新的。
- **关键技术细节：PCorrect 度量与采样估计**：
  - 定义 PCorrect(q,a; M, T) 表示模型 M 在温度 T 下对问题 q 能生成正确答案 a 的概率估计；
  - 实际操作中使用 10 组随机的4-shot同关系提示（NeX=10），对每个提示用温度 T=0 做贪心解码，另用 T=0.5 采样 16 次；
  - 用正确回答比例估计 PCorrect(T=0) 和 PCorrect(T>0)，以此划分知识类别。
- **半受控实验范式**：
  - 固定微调数据集规模大小（|D| = 6142）且固定关系分布；
  - 构建不同 Unknown 比例（X%）的数据集变体 D，X 的取值覆盖0%至100%多个档位；
  - 对照设置：训练中期（EARLY_STOP）和训练至完全收敛（CONVERGENCE，即50个epoch且100%训练准确率）；
  - 设计线性回归模型刻画拟合 Knowned 与 Unknown 训练样本对测试准确率的贡献：
    - Accuracy = β₀ + β_kn · (N_kn/|D|) + β_unk · (N_unk/|D|)

### 3. 实验设计：数据集、基准与对比

- **数据集**：采用 **ENTITY QUESTIONS**（Sciavolino et al., 2021），其三元组源自Wikidata，覆盖多样化的事实关系（人物生平、地理、产权、历史等）。
  - 使用12个随机采样的关系作为训练、开发和分布内（in-distribution）测试集；
  - 预留7个关系作为 **分布外（OOD）测试集**，用于检验跨关系泛化性。
- **模型**：PaLM 2-S base 模型（中等规模）。
- **评估指标**：精确匹配（Exact Match, EM），与词级F1验证过强相关性。
- **关键对比设计**：
  - 不同Unknown比例的D（0%、25%、50%、75%、100%等）；
  - 过滤消融：D（全量） vs D_Known（剔除Unknown示例）；
  - 单类别变体：D_HighlyKnown、D_MaybeKnown、D_WeaklyKnown、D_Unknown、D_Natural（自然分布）；
  - 回答/弃答微调变体：将Unknown训练样本标注改为"I don't know"的D_IDK 对比。
  - 对比基准：与"P(True)"分类方法（Kadavath等2022）作案例比较。

### 4. 资源与算力

- 论文中没有明确报告所用 GPU 型号、卡数或精确的墙钟训练时间，但明确表示该研究是**计算密集型**工作，难以扩展到多个LLM上重复验证。
- 具体算力需求体现：
  - 微调运行时长很长——需训练50个epoch直至完全过拟合，以观测各个微调阶段行为；
  - 数据注释阶段总共执行约 **1500万 + 次推理步骤**（17个关系 × 全量样本 × 170次推理/样本）；单样本就需要170次前向推理（10组few-shot × (1个贪心 + 16个采样) = 170）。
- 作者明确承认这一算力限制是实验使用单一模型和单一场景的主要原因。

### 5. 实验数量与充分性分析

- **实验组数概况**：
  - X% Unknown 占比变化实验：多个比例（0/25/50/75/100%）× 两种训练时长（EARLY_STOP、CONVERGENCE）× 多个随机种子；
  - 过滤消融实验：D vs D_Known；
  - 单类别训练实验：5种数据集变体；
  - OOD泛化实验：分布内 + 分布外测试；
  - 两种不同学习率（1e-5和1e-4）的鲁棒性验证；
  - 不确定性标注缓解实验（D_IDK）。
- **充分性评判**：
  - 覆盖面较广，交叉验证了多种角度，在线性拟合上也取得了很高的R²（0.86、0.95）；
  - 可重复使用了多组few-shot提示和采样做稳健估计；
  - 经统计显著性检验（表2/表8）支撑，实验设计和分析相对严谨；
  - 主要短板是单一模型类型（PaLM 2-S）、单一基底（Entity Questions）、短答案开放式QA，场景生态有限。

### 6. 论文的主要结论与发现

- Unknown（预训练知识以外）的例子在微调中拟合显著慢于Known例子，说明**模型难以通过微调高效整合新事实知识**。
- 随着Unknown例子在后续训练中被逐渐拟合，模型在测试集上的准确率**线性地**下降，即模型对预训练期间本已掌握的已知事实的幻觉倾向线性上升；这种负面影响和 Known 的训练收益幅度相似、方向相反。
- 该效应跨关系泛化：在两个权重上，训练"E1位于哪里"这类Unknown问题也会损害模型回答如"谁创立了E2"这类看似不相关的问题的能力。
- 过滤掉Unknown样本（只微调Known样本）在早期停止下几乎不影响性能，却能在训练至收敛时大幅抑制过拟合与幻觉。
- 从微调数据类别角度：**MaybeKnown 样本至关重要**——仅用 HighlyKnown 微调并非最优，而加入 MaybeKnown 样本才能帮助模型在推理时正确处理中度确定的知识；而WeaklyKnown和Unknown的存在会加剧过拟合风险。
- 将 Unknown 样本重标签为"I don't know"能够有效降低微调晚期阶段的幻觉风险，保持稳定测试性能。
- 总体来看，论文支持"知识主要来自预训练、微调更多是学习如何使用已有知识"的观点。

### 7. 优点：方法或实验设计上的亮点

- 提出**SliCK知识分层体系**——从"是否掌握、掌握程度"角度对知识做更细致划分，不同于简单的二元已知/未知划分；
- 设计了**天然受控的隔离实验**：固定数据集大小、关系分布、训练时长，只改变Unknown占比，因果识别的内部效度较好；
- 对微调动态的分析具有时间维度——同时考量和对比 EARLY_STOP 与 CONVERGENCE 状态的差异，揭示未知知识的坏处主要在后期以过拟合形式出现；
- 引入线性模型对拟合量与准确率的依赖关系做了量化拟合，简洁而有解释力；
- 检验了OOD关系泛化性，证明该现象并非仅局限于与微调数据同分布的关系；
- 基于真实世界三元组做标注，并通过误差分析说明标注噪声低（90%错误分类可靠），排除了假事实方案带来的混淆因子；
- 提供了缓解策略（过滤、重标注"I don't know"）的实证评估。

### 8. 不足与局限

- **模型生态局限**：仅使用 PaLM 2-S 一个模型，未覆盖不同大小、不同预训练目标的模型，无法检验结论的模型无关性；
- **评价场景局限**：只在闭卷QA短答案生成任务上验证；长文本生成、多跳推理、对话或通用指令跟随任务中是否同样成立尚待验证；
- **数据分布局限**：仅使用 Entity Questions 这一知识密集型QA资源；关系类型和问句模板有限，且未在多任务混合典型指令微调场景下验证；
- **知识标签存在噪声**：SliCK 依赖黑盒采样推断知识，不能100%保证类别完全准确；如测试Unknown准确率有约3%余量；
- **对真实世界影响的刻画有限**：论文使用"性能下降"作为幻觉指标，不能完全区分"模型忘记""模型误导"等具体故障类型，作者在附录中有所说明但未做细化测量。
- **规避假事实不等于规避知识冲突**：论文只考察新增新知识，未研究"知识更新（旧知识被覆盖为相反事实）"这一真实业务场景中常见的情况。

（完）
