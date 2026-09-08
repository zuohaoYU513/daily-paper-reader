---
title: Evidence Retrieval is almost All You Need for Fact Verification
title_zh: 证据检索几乎是事实验证的全部所需
authors: "Liwen Zheng, Chaozhuo Li, Xi Zhang, Yu-Ming Shang, Feiran Huang, Haoran Jia"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.551.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 强调通过证据检索将声明连接到源证据
tldr: 该论文指出事实验证常见的两阶段模式中，证据检索重要性常被忽视，现有相似度启发式检索无法提供任务相关的证据。为此提出检索增强验证框架RAV，包含混合证据检索与联合事实验证：先用高效检索器初筛候选，再以任务导向方式细化证据。结果表明，改进证据检索能比单纯堆叠复杂验证模块带来更显著的事实核查性能增益，为声明级证据关联提供了通用组件。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl551/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 724, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl551/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1341, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl551/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 727, \"height\": 368, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl551/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 724, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl551/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 730, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl551/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 727, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl551/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 650, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl551/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 847, \"label\": \"Table\"}]"
motivation: 事实核查中的证据检索常被忽略，简单相似度检索得不到任务相关证据，制约验证效果。
method: 构建混合证据检索模块和联合验证框架RAV，综合高效初筛与精细证据选择。
result: 在事实核查任务上，更准确的证据检索大幅提升验证性能，证明检索重要性。
conclusion: 证据检索应是事实核查研究的重点方向，为可归因验证提供基础能力。
---

## Abstract
Current fact verification methods generally follow the two-stage training paradigm: evidence retrieval and claim verification. While existing works focus on developing sophisticated claim verification modules, the fundamental importance of evidence retrieval is largely ignored. Existing approaches usually adopt the heuristic semantic similarity-based retrieval strategy, resulting in the task-irrelevant evidence and undesirable performance. In this paper, we concentrate on evidence retrieval and propose a Retrieval-Augmented Verification framework RAV, consisting of two major modules: the hybrid evidence retrieval and the joint fact verification. Hybrid evidence retrieval module incorporates an efficient retriever for preliminary pruning of candidate evidence, succeeded by a ranker that generates more precise sorting results. Under this end-to-end training paradigm, gradients from the claim verification can be back-propagated to enhance evidence selection. Experimental results on FEVER dataset demonstrate the superiority of RAV.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义（研究动机与背景）
- 事实验证（Fact Verification）的主流范式是“先检索证据，再验证声明”的两阶段流程。
- 现有研究大量聚焦于**声明验证模块**的改进，却普遍低估了**证据检索环节**的重要性。
- 传统证据检索多采用基于语义相似度的 KNN 启发式策略，存在两大问题：
  1. **语义相似不等于任务相关**：检索到的证据可能与声明表面相似，但缺少支撑判定的关键信息。
  2. **检索与验证相互割裂**：验证损失无法回传至检索编码器，导致检索嵌入与验证目标不匹配，证据质量受限。
- 论文的核心观点是：**证据检索是事实验证性能的关键瓶颈**，若证据不佳，再复杂的验证模型也难以给出正确判断，因此“证据检索几乎是事实验证的全部所需”。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式/算法流程
论文提出 **RAV（Retrieval-Augmented Verification）** 框架，包含两大部分：

#### （1）混合证据检索（Hybrid Evidence Retrieval）
- **Retriever（检索器）**：
  - 采用 **Bi-Encoder** 架构，对声明和证据分别进行编码，计算余弦相似度。
  - 负责从大规模候选中**快速粗筛**，将 n 个候选缩减至 p 个。
  - 推理阶段时间复杂度 O(m + n)，可结合近似最近邻（ANN）技术进一步加速。
- **Ranker（排序器）**：
  - 采用 **Cross-Encoder** 架构，将声明与证据拼接后共同编码，以捕捉细粒度语义交互。
  - 在 retriever 输出的 p 个证据中精排，选出最相关的 q 个（q < p ≪ n）。

- **联合优化（Joint Optimization）**：
  - 由于 retriever 与 ranker 结构不同，梯度不可直接回传。
  - 使用 **KL 散度**衡量 retriever 的相关性分布与 ranker 的选择概率分布之间的差异，作为监督信号优化 retriever：
    - L_kl = D_KL( ˜S ∥ ˆS )，其中 ˆS 为 retriever 的余弦相似度归一化分布，˜S 为 ranker 的选择概率分布。

#### （2）联合事实验证（Joint Fact Verification）
- RAV 是**通用框架**，可与已有验证模型（如 GEAR、GAT、KGAT 等）集成。
- 以 GEAR 为例：构建全连接证据图，将声明与经 ranker 筛选的证据拼接作为节点表示，通过图消息传播与池化得到最终表示，再由分类器输出预测标签。
- Ranker 与分类器基于**交叉熵损失**联合训练：
  - L_v = −( y log(y*) + (1 − y) log(1 − y*) )，y 为声明真实标签。

#### （3）异步训练算法
- 为提高效率，采用异步参数更新：
  - 每个迭代内，大部分训练步骤固定 retriever 参数，联合训练 ranker 与分类器。
  - 在迭代最后一步，固定 ranker/分类器参数，使用 KL 损失单独更新 retriever。
- 训练过程如 Algorithm 1 所示（详见论文附录 A）。

### 3. 实验设计：数据集、Benchmark 与对比方法
- **数据集**：FEVER（Thorne et al., 2018）
  - 185,455 条标注声明，5,416,537 篇 Wikipedia 文档。
  - 预处理的实体链接选取 20 篇相关文档，再用改进 ESIM 生成每条声明 30 条候选证据。

- **评测指标**：
  - 声明验证：Label Accuracy（LA）和 FEVER Score。
  - 证据检索：在给定金证据下，计算 Precision、Recall、F1。

- **对比方法**：
  - **声明验证基线**：以 GERE（生成式证据检索）为主，并与若干事实核查基座模型结合：
    - BERT Concat
    - GAT
    - GEAR
    - KGAT
    - 以及各自 + GERE / + RAV 的变体。
  - **证据检索基线**：TF-IDF、ESIM、BERT、XLNet、RoBERTa，均与 RAV 对比。

### 4. 资源与算力
- 论文在正文及附录中**未明确提及 GPU 型号、数量或训练时长等算力细节**。
- 仅在效率研究部分给出训练和推理时间的相对数值（见第 6 章），但没有说明具体硬件环境。
- 因此，无法从文本中获得完整的算力配置信息。

### 5. 实验数量与充分性
实验比较丰富，主要包含五类：
1. **声明验证性能实验（Table 1）**：
   - 对比了 4 个基础验证模型（BERT Concat、GAT、GEAR、KGAT），每个模型分别比较了原始版本、+GERE、+RAV 在 Dev 和 Test 上的 LA 与 FEVER Score。
2. **证据检索性能实验（Table 2）**：
   - 与 TF-IDF、ESIM、BERT、XLNet、RoBERTa 对比 Precision/Recall/F1。
3. **消融实验（Table 3）**：
   - 移除 ranker（-w/o Ranker）、移除 retriever（-w/o Retriever），与完整模型对比。
4. **超参数敏感性分析（Figure 3）**：
   - 分别考察 p（retriever 保留数）和 q（ranker 保留数）对准确率的影响。
5. **案例研究（Figure 4）**：
   - 通过两个例子展示 RAV 相对 KNN 检索的优势，如识别“sound-based”与“audio”等同义表达。

**充分性评估**：
- 从“证据检索 + 验证”双端评价来看，覆盖充分。
- 消融实验客观验证了 retriever 和 ranker 各自的贡献；其中“-w/o Retriever”更好说明 cross-encoder 对验证任务帮助更大。
- 但实验仅在 **FEVER 一个数据集**上进行，缺乏跨数据集泛化验证（如 Feverous、HoVer 等），公平性虽可接受，但外部效度受限。
- 效率实验只比较了相对训练/推理时间，缺少与 GERE 等其他模型的系统对比，亦未说明具体耗时分布。

### 6. 论文的主要结论与发现
- RAV 在声明验证和证据检索上均优于 GERE 及传统检索方法。
- 将 RAV 集成到现有验证模型（BERT Concat、GAT、GEAR、KGAT）中，均可**显著提升性能**。
  - 例：GEAR+RAV 在 Test 上的 LA 从 71.60 提升至 79.91，FEVER Score 从 67.10 提升至 74.19。
  - KGAT+RAV 达到最高 Test LA 80.23、FEVER Score 76.45。
- 证据检索模块的质量直接影响验证结果；**检索与验证联合训练**能够产生任务相关证据，并非简单地“语义相似”证据。
- Retriever 与 Ranker 的混合结构在保证效率的同时提高了证据选择的精度，消融实验证实二者均不可或缺。

### 7. 优点
- **问题定位准确**：指出现有研究忽视检索端、验证性能受限于检索质量的痛点，具有较强的现实意义。
- **方法设计新颖且实用**：Bi-Encoder 粗筛与 Cross-Encoder 精排的组合兼顾效率与精度，KL 散度衔接两阶段梯度，实现了端到端优化。
- **通用性强**：RAV 可插拔地集成到各类协议验证模型中，无需大改架构。
- **实验设计较规范**：在多个验证基座上对比 GERE，涵盖了主流的 BERT、GAT、GEAR、KGAT，并补充了消融、超参分析与案例研究。
- **案例直观**：展示了同义词推理和跨句证据关联等 KNN 难以捕捉的场景，有力说明联合训练的优势。

### 8. 不足与局限
- **数据集单一**：仅在 FEVER 上评估，未在 FEVEROUS、HoVer 等更复杂或领域不同的数据集上验证，结论的泛化性有待佐证。
- **未报告算力细节**：缺少 GPU 型号、数量等硬件信息，难以准确评估资源需求与可复现性。
- **限定的候选范围**：论文在预处理中已用实体链接和 ESIM 限制了候选证据数（20 文档 → 30 句），不能完全反映大规模真实场景下的检索压力。
- **验证模型未做进一步改进**：作者明确表示未对验证模块本身进行探索，使用现有模型作为验证器，可能限制了 RAV 的最终性能上限。
- **效率分析不深入**：效率研究只比较自身变体，未与 GERE 等对比的耗时进行比较，且未报告具体实现细节（如 batch size、训练轮数）。
- **局限性声明中提及**：未来可通过更复杂推理模型生成更优监督信号，当前框架对监督信号的依赖程度尚未细致分析。

（完）
