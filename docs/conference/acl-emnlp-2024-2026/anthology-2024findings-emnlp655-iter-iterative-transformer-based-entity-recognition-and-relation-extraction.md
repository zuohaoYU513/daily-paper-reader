---
title: "ITER: Iterative Transformer-based Entity Recognition and Relation Extraction"
title_zh: ITER：迭代式Transformer实体识别与关系抽取方法
authors: "Moritz Hennen, Florian Babl, Michaela Geierhos"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.655.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 高效并行化实体识别与关系抽取方法，可作为关系抽取模型基础
tldr: 实体识别与关系抽取常通过自回归方式生成结构化输出，耗时且计算量大。ITER提出编码器式的三阶段并行化方法，将任务拆解为可并行步骤，在保持强抽取性能的同时大幅提升吞吐量。该工作说明自回归生成并非关系抽取的必需条件，为高效构建实体关系抽取系统提供了一种可行范式。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp655/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp655/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 779, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp655/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 754, \"height\": 656, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1134, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 996, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 824, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 828, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp655/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1658, \"height\": 1406, \"label\": \"Table\"}]"
motivation: 自回归式结构化预测在实体识别与关系抽取中效率低、开销大。
method: 用编码器模型以三个可并行步骤完成实体识别和关系抽取，避免逐词自回归。
result: 在大模型上实现每秒600余样本的推理吞吐，同时保持优异抽取性能。
conclusion: 并行化的编码器迭代可替代高成本自回归，用于高性能关系抽取系统。
---

## Abstract
When extracting structured information from text, recognizing entities and extracting relationships are essential. Recent advances in both tasks generate a structured representation of the information in an autoregressive manner, a time-consuming and computationally expensive approach. This naturally raises the question of whether autoregressive methods are necessary in order to achieve comparable results. In this work, we propose ITER, an efficient encoder-based relation extraction model, that performs the task in three parallelizable steps, greatly accelerating a recent language modeling approach: ITER achieves an inference throughput of over 600 samples per second for a large model on a single consumer-grade GPU. Furthermore, we achieve state-of-the-art results on the relation extraction datasets ADE and ACE05, and demonstrate competitive performance for both named entity recognition with GENIA and CoNLL03, and for relation extraction with SciERC and CoNLL04.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义（研究动机与背景）

- 实体识别（NER）与关系抽取（RE）是文本结构化信息提取中的核心任务。
- 近年来，主流方法逐渐倾向于将此类结构化预测问题建模为**自回归生成任务**：模型逐个 token 地生成携带实体边界、类型和关系信息的输出字符串。例如 (m)REBEL、TANL、ASP 等。
- 尽管自回归方法在任务灵活性上表现良好（源/目标词汇表无需对齐），但其存在显著缺陷：
  - 推理过程无法沿序列维度并行化，每个 token 的生成依赖之前所有 token，导致**推理吞吐量低**；
  - 输出序列通常不短于输入序列，计算开销随输入长度增大而急剧增加；
  - 随着模型规模增长至数十亿甚至更大，训练和部署成本令人难以承受。
- 因此，作者提出一个根本问题：**是否必须使用自回归语言建模才能达到可比性能？**
- 为回答该问题，论文提出 **ITER（Iterative Transformer-based Entity Recognition and Relation Extraction）**——一个纯编码器架构的关系抽取与实体识别模型，仅通过三个可并行化步骤完成结构化输出，避免逐 token 生成，从而在保持甚至超越 SOTA 性能的同时大幅提升推理速度。
- 整体含义：该工作为高效、低延迟、高吞吐的端到端信息抽取系统提供了一种新的非自回归范式，并证明了自回归生成并非结构化抽取任务的必要条件。

## 论文提出的方法论

### 核心思想
- ITER 将自回归模型 ASP 中的“动作序列生成”过程，转换为**三个顺序执行、但每一步可在序列维度高度并行化的分类/配对步骤**。
- 三个步骤分别对应：
  1. 判断哪些位置是一个命名实体的**开始**（`is_left`）；
  2. 将左侧括号与后续位置配对，形成**实体跨度（span）并赋予实体类型**（`is_span`）；
  3. 对所有识别出的实体对进行**关系分类**（`is_link`）。
- 模型使用**门控前馈网络（Gated FFN）**作为分类头，基于 Transformer 编码器产生的上下文表示进行分类。

### 关键技术细节
- 对传统括号动作的改进：允许同一位置同时执行 `[` 和 `]` 动作，以正确处理**单 token 实体**；每个位置的动作集定义为幂集形式：
  - \(Y_n = \wp(A) \times \wp(B_n)\)，其中 \(A = \{[, ]\}\)。
- 跨度配对时，允许同一右括号位置与多个左侧括号位置配对，并为每个配对赋予独立的实体类型，从而支持一定程度的嵌套实体（通过参数 \(\omega\) 控制嵌套深度）。
- 三个关键函数：
  - `is_left(h_n)`：输出布尔值，判断位置 \(n\) 是否为实体起点。
  - `is_span(h_m, h_n)`：结合已标记的左括号位置，判断从 \(n\) 到 \(m\) 是否构成某类实体；输出为基于 sigmoid 的多类判断。
  - `is_link(h_i, h_j)`：对两个实体（位置对）进行关系分类，输出多标签布尔向量；关系有方向性，因此 `is_link(h_i,h_j) ≠ is_link(h_j,h_i)`。
- 训练时同时优化三个阶段损失（`is_left`、`is_span`、`is_link`），避免流水线式错误传播；总损失为每个位置三类损失之和。
- 推理算法（以非嵌套 \(\omega=1\) 为例）：
  - 先将输入编码为上下文向量；
  - 并行预测所有位置的左括号动作；
  - 对每个位置找出其前面最近的左括号位置，并行判断是否构成实体以及实体类型；
  - 组合所有实体对，通过 `is_link` 判断关系。
- 计算复杂度：
  - 步骤1和2均为线性时间 \(O(N)\)（在 \(\omega=1\) 时，\(\omega > 1\) 时为 \(O(N\omega)\)，\(\omega \ll N\)）；
  - 步骤3为 \(O(E^2)\)，其中 \(E\) 是实体数，通常 \(E \ll N\)；
  - 总体复杂度为 \(O(N + E^2)\)，明显低于传统自回归生成。

### 与现有方法的差异
- 不同于表填充（table-filling）和纯 span 枚举法（如生成所有候选 span 再分类），ITER 仅需线性时间生成离散的实体跨度，不需要构建巨大的候选矩阵或标记集合。
- 不同于 PL Marker 等需要将大量标记 token 插入输入序列的方法，ITER 不改变输入长度，因此效率更高。
- 不同于自回归生成模型，ITER 在推理过程中无需逐 token 解码。

## 实验设计

### 数据集与 Benchmark
论文在 6 个数据集上评估模型，覆盖 NER 和 RE 任务：

- **CoNLL03**：新闻领域 NER；
- **GENIA**：生物医学领域 NER（含嵌套实体）；
- **CoNLL04**：新闻领域 RE；
- **ACE05**：新闻领域 RE（含实体+关系）；
- **ADE**：生物医学领域药物不良反应 RE；
- **SciERC**：科学文献领域 RE。

数据集统计包括样本数、开发/测试划分、嵌套实体比例等，详情见原文 Table 2。

### 实验设置
- 数据预处理与划分遵循文献中常见方案；ADE 无官方划分，使用 10 折交叉验证；GENIA 的训练和开发集被合并（沿用 Shen et al. 的设置）。
- 主要采用 **micro F1** 作为评估指标。
- 对 RE 采用严格评价（RE+）：只有当关系两端的实体 span 和类型均正确时，才算预测正确。
- 对于对称关系评估，由于部分基线（PL Marker、Wang et al.）将对称关系输出两次并重复计分，作者也实现了带 `*` 的相应评估方式以进行公平比较。

### 对比方法
- 自回归 / seq2seq 方法：ASP（T5 base/large/3b）、REBEL、TANL、DeepStruct、UIE、LasUIE、ATG 等；
- 编码器/span 方法：PL Marker、DiffusionNER、PFN、Wang and Lu、UniRel 等；
- 使用了不同预训练模型作为编码器：FLAN-T5（large、xl）、T5、BART、DeBERTaV3（large）、BERT（large-cased）、ALBERT（xxlarge-v2）等。

### 主要结果
- **ACE05**：ITER + FLAN-T5（xl）获得 RE+ F1 71.9，创 SOTA（+1.4）；NER F1 91.9（使用 DeBERTaV3）也创 SOTA；
- **ADE**：ITER + FLAN-T5（xl）获得 NER F1 92.2 和 RE+ F1 85.6，均为新 SOTA；
- **CoNLL04**：与 SOTA 竞争，略逊于 ASP + T0（3b）、DeepStruct、ATG，但后两者参数规模大 7~25 倍；
- **SciERC**：表现与近期强基线相近（如 DeBERTaV3 版本）；
- **CoNLL03**：性能与 ASP 相当，未达到领域内最高 SOTA；
- **GENIA**：与其他 SOTA 模型相比具有竞争力；
- **吞吐量实验**：ITER + T5 large 在 ACE05 上达到 392.9 samples/s，而 ASP + T5 large 为 34.8 samples/s，提升 11 倍以上；在 CoNLL04 上，ITER + T5 large 达 605 samples/s，ASP + T5 large 仅 27 samples/s，提升约 22 倍；最大提升可达 42 倍（FLAN-T5 large vs ASP + T5 large）。
- 具体逐 seed 的 precision/recall/F1 标准误见原文 Table 6。

## 资源与算力

- 论文明确报告了推理实验所用的 GPU：
  - 大部分吞吐对比使用单张 **NVIDIA RTX 4090**（batch size 64）；
  - CoNLL03 文档级长文本实验使用单张 **NVIDIA H100**（batch size 8）；
  - 模型规模 ≥1.3B 参数时使用单张 H100。
- 但关于**训练阶段**的 GPU 型号、数量、训练时间、总 FLOPs 等信息，论文**没有明确说明**，也未报告训练成本估算。
- 模型参数规模：
  - ITER + FLAN-T5 large：393M；
  - ITER + FLAN-T5 xl：1.3B；
  - ITER + DeBERTaV3 large：476M；
  - ITER + T5 large：410M；
  - 对比的 ASP + T5 3b：2.9B；DeepStruct：10B。
- 因此，论文主要展示了推理效率优势，但训练算力成本未充分披露。

## 实验数量与充分性

### 实验数量
- 共在 **6 个公开数据集**上进行评估，涵盖新闻、生物医学、科学文献等领域，任务包含 NER、RE 和嵌套 NER。
- 每个模型在多个 seed（通常 5 个种子）上重复，报告均值和标准差；部分消融实验用 3 个种子。
- 使用 **FLAN-T5 large / xl、T5 large、BERT large、BART large、ALBERT xxlarge、DeBERTaV3 large** 等多个预训练编码器进行对比，考察不同模型族的影响。
- 进行了 **超参数搜索**（SMAC3 贝叶斯优化），搜索空间包括学习率、学习率调度、warmup、权重衰减、batch size 和激活函数等。
- 进行了 **迁移学习消融实验**：利用 CoNLL03 训练好的 checkpoint 初始化 CoNLL04 和 ACE05，观察迁移效果。
- 进行了 **阈值敏感性实验**：在 ACE05 上绘制不同 \(\lambda\) 下的 precision/recall/F1 曲线。
- 进行了 **吞吐量测量**：不同模型规模、不同输入长度下的对比。

### 充分性与公平性评价
- **优点**：
  - 多数据集、多模型族、多 seed 重复实验，统计可靠性较好；
  - 公平性考虑较周到：明确指出 PL Marker / Wang et al. 在对称关系评估中的特殊计分方法，并复现了带 `*` 的评估模式，便于与基线对比；
  - 吞吐量测量包含了不同硬件条件，并给出明确批次大小；
  - 不仅报告 F1，还报告 precision/recall 和方差，信息完整。
- **不足**：
  - 训练资源、训练时长未报告，导致无法评估整体计算成本；
  - 对嵌套实体的实验证据较弱：只有 GENIA 中包含一定比例嵌套实体，其他数据集嵌套比例极低或受到限制，作者也承认缺少大规模嵌套实体基准；
  - 部分结果未达到 SOTA（如 CoNLL03、SciERC），作者在部分情况下归因于模型规模和任务特性，但缺乏深入的误差分析；
  - 与 DeepStruct（10B）等超大模型相比，虽在参数效率上有优势，但公平性上仍存在预训练数据、训练策略等不可控差异。

## 主要结论与发现

- ITER 作为**非自回归、编码器式三阶段模型**，可以替代自回归生成方法完成实体识别与关系抽取，并在多数数据集上达到或超越 SOTA。
- ITER **在推理效率和性能之间取得了更好的权衡**：在单张消费级 GPU 上，大型模型吞吐量可达每秒 600 个以上样本，相比 ASP 最高加速约 23~42 倍，相比 PL Marker 也有数倍提升。
- 在 ACE05 和 ADE 上，ITER 同时刷新了 NER 和 RE 的 SOTA；在 CoNLL04、SciERC、GENIA、CoNLL03 上具有竞争力，尤其考虑到模型参数远小于许多对比模型。
- **FLAN-T5 的编码器**在 ITER 框架中表现优异，可与 BERT 族编码器媲美甚至更好，表明**自回归模型的编码器部分也可用于判别式结构化预测**，鼓励进一步研究。
- 具有相对位置编码的模型（T5 族、DeBERTa）比绝对位置编码的模型（BERT、ALBERT）更适应 ITER 的位置配对需求。
- 使用 CoNLL03 预训练 checkpoint 可小幅提升 CoNLL04 的 F1（+0.6），但对 ACE05 无益（-1.8），说明模型迁移在不同数据集上效果不一致。

## 优点

- **高效性突出**：三阶段并行化设计带来了线性复杂度的实体识别流程，打破了自回归生成的效率瓶颈。
- **设计简洁且模块化**：方法由 `is_left` / `is_span` / `is_link` 三个清晰模块组成，可自由替换底层预训练编码器，便于复现和扩展。
- **性能优秀且均衡**：在多数据集上均达到或逼近 SOTA，且没有依赖百亿级超大模型。
- **公平性意识强**：对比基线时考虑并实现了不同评估协议（如对称关系重复计分），实验结果更可信。
- **分析维度丰富**：涵盖性能、吞吐量、不同预训练编码器、超参数影响、迁移效果等，提供了较为全面的实证视角。
- **代码与 checkpoint 开源**，有利于后续研究复现。

## 不足与局限

- **无法生成输入中不存在的实体名称**：模型的实体跨度完全从输入 token 中选取，不能进行规范化或生成式实体链接；不过论文指出其使用的数据集中没有出现这种需求。
- **嵌套实体支持有限**：算法通过 \(\omega\) 参数控制最大嵌套深度，实际推理默认 \(\omega=1\)；虽然 GENIA 等数据集包含嵌套实体，但实验中对嵌套场景的专门评测薄弱，缺少大规模嵌套基准。
- **训练成本未披露**：论文重点强调推理速度快，但对训练的 GPU 时长、硬件配置和能耗没有报告，无法全面评估该方法的总体可持续性。
- **部分数据集落后于 SOTA**：CoNLL03 上未能接近最佳结果；SciERC 上的表现也相对一般。论文未给出完整误差分析，限制了方法适用性的判断。
- **比较基线存在不公平因素**：部分对比模型（如 DeepStruct、T0-3B）拥有数倍乃至数十倍参数量，且预训练语料和训练策略不同，直接比较性能并不完全公平。
- **阈值依赖**：关系判断依赖 sigmoid 之后的手动阈值 \(\lambda\)，虽然可以调节 precision/recall，但实际应用中需要针对新数据进行调参，带来了实用性上的额外负担。
- **未来工作未涉及零样本/少样本泛化的深入验证**：作者仅展望了方向，未进行跨数据集零样本迁移实验。

（完）
