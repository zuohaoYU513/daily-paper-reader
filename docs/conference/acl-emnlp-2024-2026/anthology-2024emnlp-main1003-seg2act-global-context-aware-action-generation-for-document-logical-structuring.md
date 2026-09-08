---
title: "Seg2Act: Global Context-aware Action Generation for Document Logical Structuring"
title_zh: Seg2Act：面向文档逻辑结构的全局上下文动作生成
authors: "Zichao Li, Shaojie He, Meng Liao, Xuanang Chen, Yaojie Lu, Hongyu Lin, Yanxiong Lu, Xianpei Han, Le Sun"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.1003.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 用动作生成方式重建长文档章节层级逻辑结构
tldr: 文档逻辑结构化旨在恢复长文档的层次结构，传统方法难处理复杂多变的文档。Seg2Act将逻辑结构抽取转化为动作生成问题，由全局上下文感知模型迭代输出动作并同步维护已生成结构，从而端到端地重建段落层级。在ChCatExt和HierDoc等中文文档结构数据集上显示了该方法对长文档逻辑结构抽取的有效性。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1003/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1003/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1529, \"height\": 704, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1003/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 726, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1003/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 676, \"height\": 920, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1633, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 778, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1552, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 829, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 789, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 703, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1003/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 665, \"height\": 274, \"label\": \"Table\"}]"
motivation: 长文档逻辑层次复杂多变，传统方法难以端到端处理全局结构。
method: 将逻辑结构抽取视为动作序列生成，用全局上下文模型迭代生成动作并更新结构。
result: 在ChCatExt与HierDoc数据集上的实验表明该方法能有效完成长文档逻辑结构抽取。
conclusion: 生成式全局结构建模为长文档层级信息组织和下游抽取提供了新工具。
---

## Abstract
Document logical structuring aims to extract the underlying hierarchical structure of documents, which is crucial for document intelligence. Traditional approaches often fall short in handling the complexity and the variability of lengthy documents. To address these issues, we introduce Seg2Act, an end-to-end, generation-based method for document logical structuring, revisiting logical structure extraction as an action generation task. Specifically, given the text segments of a document, Seg2Act iteratively generates the action sequence via a global context-aware generative model, and simultaneously updates its global context and current logical structure based on the generated actions. Experiments on ChCatExt and HierDoc datasets demonstrate the superior performance of Seg2Act in both supervised and transfer learning settings.

---

## 论文详细总结（自动生成）

# 论文《Seg2Act：面向文档逻辑结构的全局上下文动作生成》详细总结

## 1. 论文的核心问题与整体含义

- **研究背景**：文档逻辑结构化（Document Logical Structuring）旨在从文本片段中恢复文档隐含的层次化逻辑结构（即由标题节点和段落节点构成的逻辑树），是文档智能领域的基础性任务，可有效支撑信息检索、摘要生成与长文档问答等下游应用。
- **核心问题**：传统方法在处理多页、长篇幅、结构复杂多变的真实文档时面临三重挑战：
  - OCR切分产生的文本片段往往不是完整的语义单元（短行、跨行），片段与真实层次结构不对齐，编码时造成语义丢失；
  - 现有方法通常将任务拆解为特征提取、标题检测、节点关系预测等多个子任务，以流水线方式串联，存在误差传播且难以统一设计最优组合架构；
  - 不同文档类型（如金融报告、学术文献）的逻辑结构差异大，人工设计的规则或组合结构难以跨类型泛化。
- **论文回应**：提出**Seg2Act**，首次将文档逻辑结构抽取重新定义为一次性的“动作生成”任务，采用端到端生成式框架，并用全局上下文栈来建模长距离依赖，从而提升结构预测的准确性和跨领域的泛化能力。

## 2. 方法论：核心思想、关键技术与算法流程

- **核心思想——逻辑结构抽取作为动作生成**：
  - 输入为文本片段序列 X = x₁, …, x_N，模型逐段输出动作序列 Y = y₁, …, y_N，动作用于在文档逻辑树中定位并“安置”对应的文本片段，实现边生成、边建树。
  - 每个片段与一个动作一一对应，直接映射到逻辑树的某个具体位置（无需像 shift-reduce 那样多次参与操作），减少预测次数、提升效率。
- **三种基础动作**：
  - **New Level-k Heading**：用 k 个连续“+”表示，将当前片段作为新的第 k 层标题节点插入，父节点为最近添加的 (k-1) 层标题；
  - **New Paragraph**：用“*”表示，将当前片段作为新的段落节点，父节点为最近添加的标题；
  - **Concatenation**：用“=”表示，将当前片段作为前一个文本的延伸，追加到最后一个节点（用于拼接同行所属的连续残缺片段）。
- **全局上下文栈（Global Context Stack, GCS）**：
  - 栈中存放已构建结构中与当前决策最相关的路径节点（栈顶为最近添加的节点，向下依次为回溯路径上的各级标题），每次根据生成的动作同步更新。
  - 用与动作相同的符号标记来组织栈内容，将文本与结构标记一起作为模型的输入，将“长距离依赖”集中化表征，在有限输入长度内有效传递全局上下文。
- **Multi-segment multi-action 策略**：
  - 在实际场景中（如 HierDoc 平均每篇 853 个片段）若逐段处理，既难以获取完整语义又太慢。
  - 因此设定输入窗口 w_I 与输出动作窗口 w_O（默认 w_I = w_O = 3），一次读取多个连续片段并同时输出多个动作，扩大模型的裁决视野并加速生成。
- **训练**：基于 teacher-forcing 交叉熵损失进行优化：
  
  L = -Σᵢ log P(y_{i:i+wI−1} | sᵢ, x_{i:i+wI−1}; Θ)
  
  其中 sᵢ 为当前全局上下文栈状态；训练阶段默认 w_I = w_O。
- **推理（Algorithm：Text segments to logical structure）**：
  - 初始化根节点与栈；
  - 循环取 w_O 个片段+上下文窗口 w_I 的文本，由模型生成动作；
  - 解析各动作并调用对应更新函数，更新逻辑树和全局栈；
  - 全部片段处理完后返回完整逻辑树。
  - 使用 **硬约束**（如禁止输出预定义集合以外的 token、空栈时禁止“=”、禁止跳级建立标题等）保证生成动作的可解析性；若生成动作数不匹配则跳过若干片段继续执行（容错处理）。
- **与 TRACER 的变体对比（Seg2Act-T）**：使用 Seg2Act 的生成模型作为动作解析器、但仍保留 TRACER 的 shift-reduce 动作，以单独检验全局栈与新型动作各自的效果归属。

## 3. 实验设计：数据集、场景与对比方法

- **数据集**：
  - **ChCatExt**（Zhu et al., 2023）：650 篇中文金融/文档语料，带完整层次逻辑树标注，包含标题与段落两类节点；训练时按先序遍历将逻辑树转换为(片段, 动作)对。
  - **HierDoc**（Hu et al., 2022b）：650篇英文科学文献，带目录结构（ToC）标注，只包含标题标注，用于标题检测与目录抽取。
  - **Wiki 语料**：用于 transfer learning 的预训练数据。
  - **ChCatExt 三个子集**：BidAnn（100篇）、FinAnn（300篇）、CreRat（250篇），用于迁移实验。
- **Benchmark / 指标**：
  - 标题节点、段落节点、总节点的 **F1-score**；
  - **TEDS**（用于 HierDoc 的 ToC 抽取质量）；
  - **DocAcc**（新增指标）：要求整篇文档的逻辑树与标注**完全一致**才算正确。
- **对比方法**：
  - **文本-only 基线**：TRACER（transition-based extraction，基于预训练模型编码局部片段对）；
  - **多模态基线**：MTD（multi-modal tree decoder，用视觉+文本+位置信息）、CMM（cascade move/delete式树修正）；
- **主干模型选择**：RBT3、GPT2-Medium、Baichuan-7B、Baichuan-13B、Qwen1.5 系列（0.5B/1.8B/4B）等。
- **数据场景**：
  - 监督学习：ChCatExt 完整语料、HierDoc 完整语料；
  - 迁移学习设定：零样本（zero-shot）、少样本（few-shot，3-shot/5-shot）、全样本（full-shot），在三个子集间两两迁移（表4给出从表头训练到各测试集的多组合结果）。

## 4. 资源与算力说明

- 论文明确写出：**实验基于 NVIDIA A100 GPU 完成**；
- 训练超参：AdamW 优化器、学习率 3×10⁻⁴、训练 10 epochs、batch size 128；
- 采用 **LoRA**（rank r=8，alpha α=16）以降低 Baichuan-7B 显存开销；
- transfer 设置中 Wiki corpus 上预训练 10,000 步；
- 但论文**没有明确报告具体的 GPU 数量、单卡还是多卡、总训练时长或能耗**。推理时间方面，有给出单篇文档的平均推理时间（如 Baichuan-7B 下默认设为 8.13 秒/篇），用于效率对比，但训练侧总资源未作量化说明。

## 5. 实验数量与充分性

- **实验组数量**（从表/图看，至少在十组以上）：
  1. ChCatExt 上三种骨干（RBT3/GPT2-Medium/Baichuan-7B）下的监督对比（Table 2）；
  2. HierDoc 上标题检测 F1 与 ToC TEDS 同多模态方法的对比（Table 3）；
  3. 迁移学习的零/少/多样本多组合矩阵（Table 4，覆盖 BidAnn/FinAnn/CreRat 三个域）；
  4. 消融全局栈（Table 5，分别移除符号、移除文本、仅保留符号等）；
  5. 多段多动作中 w_I 与 w_O 从 1 到 5 的窗口滑移实验（Table 6，含效率指标）；
  6. 文档逻辑深度与 token 长度的切层分析（Figure 3）；
  7. 案例研究（Table 7）；
  8. 附录中模型尺寸影响分析（Baichuan-13B 与 Qwen1.5 系列，Table 9 & 10）。
- **充分性评价**：从“骨干模型覆盖（小到 RBT3，大到 13B 级大模型）”、“结构难度分层”、“长度切层次分析”、“跨域方向迁移组合”等多维度设计来看，实验覆盖面较宽，较好地回答了“方法是否有效且泛化”的核心问题。
- **客观公平性**：总体较规范（同一骨干下做对比；每个实验取五个随机种子的平均结果），但少样本/全样本的子集切换数量并不大（最大 300 篇），且表 4 中各子细胞的样本量相差悬殊，个别跨域迁移结果存在不稳定性，因此存在受抽样随机性影响的风险。鉴于表 4 中的数字在零样本栏下可见不少类别结果差异很大（例如零样本时 BidAnn 从 TRACER 的 2.7 到 Seg2Act 的 56.25），即便按五个种子取均值，分布偏态仍可能致使均值代表性偏弱。

## 6. 论文的主要结论与发现

- **Seg2Act 在监督设定下显著优于基线**：ChCatExt 上以 Baichuan-7B 为骨干，Seg2Act 的标题/段落/总节点 F1 分别达 96.01 / 94.19 / 92.63，DocAcc 达 63.69，较同骨干 TRACER 高 +9.84 DocAcc；GPT2-Medium 与 Baichuan 骨干下也全面领先。
- **仅用文本即可超越多模态方法**：在 HierDoc 上，Seg2Act（纯文本）的 ToC TEDS 达 96.3%（GPT2）与 96.3%（Baichuan-7B 为 96.3、FinDoc? 实为 96.3 但对齐上文献表格中 Baichuan 对应 96.3 vs CMM 88.1），显著高于 MTD 与 CMM，说明结构语义的端到端生成比“视觉模态不可用时的布局依赖”更有通用性优势。
- **全局栈是真因**：将全局上下文栈移植到 TRACER（即 Seg2Act-T）也能带来 1~3 个百分点的总节点提升，显示全局信息是关键模块；
- **符号化结构表征的价值与权衡**：删除结构符号会显著降低文档级准确率（-6.46 DocAcc），说明符号化的层级表达能有效帮助模型感知全局结构；但加入符号后模型倾向“层级判别”和“段落拼接”之间存在细微此消彼长。
- **多段多动作策略兼顾性能与效率**：与 (1,1) 模式相比，(3,3) 在总 F1 上提高 1.07、推理时间降至约 0.28 倍；
- **鲁棒的数据稀缺应对**：5-shot 相对全样本仅平均下降约 3.98，优于基线。
- **长文档处理优势**：Seg2Act 在长 token 高深度文档上的性能衰减小于基线，印证了一对一逻辑树动作设计的合理性。

## 7. 优点与亮点

- **问题重新定义的简洁性**：将复杂的多级标题 + 段落结构建模压缩为三种字符动作的组合，统一表达“层级、归属和续接”，算法思想清晰、易实现且不依赖视觉形态特征。
- **生成模型与树结构维护的深度融合**：全局上下文栈用紧凑符号对已构造结构进行选择与浓缩，让语言模型在自回归解码时“看得见”文档此前层次路径，极大缓解了长文档不可穷尽长度下的上下文瓶颈。
- **一次映射、在线更新的推理特性**：无需先检测标题再判断关系等多次往返；w_I/w_O 可自由伸缩，给精度/效率提供可控调节维度，更加工程友好。
- **丰富的多角度验证**：在监督、迁移（零/少/多样本）、消融、结构深度、文档长度、推理速度、模型规模等多条证据链上递进检验，使方法结论的可信度较强。
- **通用性与易用性统一**：附录公开代码（GitHub 链接），报告了约束实现细节（不同 tokenizer 下的 logits 控制等），可复现性强；论文用了一个新增的文档级 DocAcc 指标，更严格地度量逻辑树整体正确性，具有参考价值。

## 8. 不足与局限

- **不可解析风险的客观存在**：生成式模型虽受硬约束保护，但 w_I≠w_O 等情况下仍无法保证动作序列的数量永远精确匹配，论文采取“失败跳过该批次”的办法，相当于一种硬截断，可能在边缘情形丢失部分内容，略微降低系统可用性。
- **不利用视觉与版面信息**：Seg2Act 仅适用正常线性排序的文本片段；面对版面乱序（多栏、OCR错位、表格内文本拆分等）无法直接应对，而现实扫描文档中版面噪声常见，作者也在限制中明确承认这一点，并将其指为未来探索方向。
- **训练数据规模与跨子型差异敏感**：迁移实验中的某些目标子集零样本效果仍偏低（如 FinAnn 于 BidAnn 预训练时个体表现波动明显），说明“文档类型与结构风格”迁移依然有限制；需要更多多样本库才能稳妥泛化。
- 缺乏对算力和环境开销的完整量化披露（GPU 卡数、时长、能耗等未给出），不利于资源弹性的学术复现对比。
- 在模型大小与效果关系上，作者虽验证了 Qwen1.5-4B 等较小模型的可行性，但同样承认大模型参数量增大带来的收益非线性（7B→13B 收益有限），意味着实际部署时还需权衡成本。

（完）
