---
title: "GenProve: Learning to Generate Text with Fine-Grained Provenance"
title_zh: GenProve：学习生成带细粒度溯源信息的内容
authors: "Jingxuan Wei, Xingyue Wang, Yanghaoyu Liao, Jie Dong, Yuchen Liu (刘雨辰), Caijun Jia, Bihui Yu, Junnan Zhu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.228.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 生成时输出句子级溯源三元组，区分引用压缩与推理，从机制上减少无依据内容
tldr: 仅给LLM生成结果添加引用仍难以让用户核实来源如何支撑主张，现有方法粒度较粗且无法区分直接引用与复杂推理。GenProve提出生成时细粒度溯源任务，要求模型在生成流畅文本的同时输出结构化句子级三元组。论文构建专家校验的ReFInE数据集，区分引用、压缩与推理三类证据关系。实验显示该方法显著提升生成内容的可归因性、透明度和可验证性，为减少无依据生成提供了可行的机制。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 770, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1633, \"height\": 870, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 675, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1638, \"height\": 966, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1638, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 789, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 785, \"height\": 906, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 788, \"height\": 716, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1633, \"height\": 1152, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 789, \"height\": 986, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 773, \"height\": 982, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 770, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1642, \"height\": 1585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1646, \"height\": 996, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 796, \"height\": 911, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 800, \"height\": 914, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long228/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 791, \"height\": 906, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 583, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1657, \"height\": 971, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1645, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long228/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 980, \"label\": \"Table\"}]"
motivation: 传统引用无法说明来源如何支撑具体生成主张，粗粒度溯源难以满足可信生成和可追责需求。
method: 提出生成时细粒度溯源任务，让模型在生成时输出句子级溯源三元组，并构建ReFInE数据集辅助训练与评测。
result: 实验表明细粒度生成溯源有效提升输出可验证性和可解释性，降低幻觉带来的信任风险。
conclusion: 句子级来源三元组是实现可审计且可验证的LLM生成的重要方法。
---

## Abstract
Large language models (LLM) often hallucinate, and while adding citations is a common solution, it is frequently insufficient for accountability as users struggle to verify how a cited source supports a generated claim. Existing methods are typically coarse-grained and fail to distinguish between direct quotes and complex reasoning. In this paper, we introduce Generation-time Fine-grained Provenance, a task where models must generate fluent answers while simultaneously producing structured, sentence-level provenance triples. To enable this, we present ReFInE (Relation-aware Fine-grained Interpretability Evidence), a dataset featuring expert-verified annotations that distinguish between Quotation, Compression, and Inference. Building on ReFInE, we propose GenProve, a framework that combines Supervised Fine-Tuning (SFT) with Group Relative Policy Optimization (GRPO). By optimizing a composite reward for answer fidelity and provenance correctness, GenProve significantly outperforms 14 strong LLMs in joint evaluation. Crucially, our analysis uncovers a reasoning gap where models excel at surface-level quotation but struggle significantly with inference-based provenance, suggesting that verifiable reasoning remains a frontier challenge distinct from surface-level citation.

---

## 论文详细总结（自动生成）

# GenProve：学习生成带细粒度溯源信息的内容——详细中文总结

## 1. 论文的核心问题与整体含义

- **核心问题**：大型语言模型（LLM）在生成文本时存在严重的幻觉（hallucination）问题。为缓解这一问题，业界普遍采用添加引用的方式（如 RAG、citation generation），但论文指出这些传统方法存在根本性不足：
  - **粒度太粗**：现有引用通常停留在文档级或段落级，无法精确到具体是哪一句来源句支持了生成的哪一句主张。
  - **没有类型区分**：无法说明某一来源究竟是被直接引用（Quotation）、被压缩概括（Compression），还是基于其做了逻辑推理（Inference）。
  - **可验证性不足**：用户即便看到引用列表，也难以确认"该来源到底如何支撑了生成内容"，导致无法有效核验和追责。
- **论文整体含义**：论文主张从"生成后补引用"的粗粒度模式转向 **"生成时细粒度溯源"（Generation-time Fine-grained Provenance）** 范式，即要求模型在生成流畅答案的同时，为每一个生成的句子同步产出结构化的溯源三元组 `(DocID, SentID, Relation)`，明确指出支持该句的证据句，并标注证据使用关系类型。该范式试图从机制上减少无依据内容的产生，将引用从"装饰性元素"转化为生成过程中的内在推理约束。

## 2. 论文提出的方法论

### 2.1 核心思想

论文提出两阶段训练框架 **GenProve**，结合：

1. **SFT（监督微调）**：让模型学会指令遵循和结构化溯源标签（[PROVE]）的格式生成。
2. **GRPO（Group Relative Policy Optimization，组相对策略优化）强化学习**：在SFT提供的稳定策略基础上，通过复合奖励进一步优化内容的忠实度与溯源的正确性。

### 2.2 关键技术细节

**任务定义**：
- 输入：问题 Q 和一组来源文档 D = {d₁, ..., dₘ}。
- 输出：答案 A = (t₁, ..., tₙ)，每个句子 tⱼ 带一个溯源集合 Pⱼ。
- Pⱼ 中的每个三元组为 (doc_id, sent_id, r)，其中 r ∈ {Quotation, Compression, Inference}。
- 结构化格式为：`句子内容 + [PROVE: ("doc_id", "sent_id", "relation")]`；同一句子若有多个证据，合并到一个 PROVE 标签中。

**SFT 阶段**：
- 最大化参考输出（带溯源标注的答案）的条件似然：
  \[
  \mathcal{L}_{SFT}(\theta) = -\sum_{i=1}^{N} \log p_\theta(A^{ref}_i \mid Q_i, D_i)
  \]
- 作用：提供稳定的策略初始化，让模型学会产出语法有效的溯源标签和内容相关的答案。

**GRPO 阶段**：
- 目标函数：
  \[
  J(\theta) = \mathbb{E}_{(Q,D) \sim \mathcal{D}_{GRPO}} \left[ \mathbb{E}_{A \sim \pi_\theta(\cdot|Q,D)} [R(A, A^{ref})] \right]
  \]
- 奖励函数由两个模块组成：

  **Reward A：句子匹配内容相似度奖励**
  - 将生成句子与参考句子用 Sentence-Transformer 编码后计算余弦相似度，找到最佳匹配对。
  - 若最佳相似度低于阈值 τ_c = 0.45，则该句奖励为 0；否则计算匹配句对之间的 ROUGE-L。
  - 内容奖励为所有句子得分的平均值。

  **Reward B：参考引导的溯源 F1 奖励**
  - 反向对齐：每个参考句子找最接近的生成句子（余弦相似度阈值 τ_p = 0.50）。
  - 比较匹配对的溯源集合，计算句子级精度和召回率，进而得到 F1：
    \[
    F1_k = \frac{2 \cdot Prec_k \cdot Rec_k}{Prec_k + Rec_k + \epsilon}
    \]
  - 溯源奖励为所有参考句子的平均 F1（排除匹配失败的句对）。

  **复合奖励**：
  \[
  R(A, A^{ref}) = \alpha \cdot R_{sim}(A, A^{ref}) + \beta \cdot R_{prov}(A, A^{ref})
  \]
  - 该设计可惩罚两类典型错误：内容与证据不匹配（幻觉）和关系类型标错（如把 Compression 错标为 Quotation）。

### 2.3 ReFInE 数据集的构建

论文还构建了一个专家校验的数据集 **ReFInE**，作为训练和评测的基础，构建流程分为三个阶段：
1. **预处理**：将长答案和来源文档切分为句子，为每个来源句分配唯一的 (DocID, SentID)。
2. **GPT-4o 辅助标注**：让 GPT-4o 预测每个目标句子的溯源三元组，再由人工筛选质量。
3. **重建与专家校验**：将句子级标注重建为完整实例，由专家进行双重校验，验证证据充分性和关系类型正确性，不合格样本被修改或丢弃。

**ReFInE 数据集规模**：
- SFT 子集：12,540 条
- GRPO 子集：5,256 条
- EVAL 子集：4,838 条
- 平均每个答案含 3.96 个 PROVE 标签，每个标签平均聚合 1.98 个溯源三元组。
- 关系分布上，Quotation 占比最高，GRPO 子集中 Inference 和 Compression 的占比高于 EVAL。

## 3. 实验设计

### 3.1 评测数据集与场景
- 主评测：在 ReFInE 的 EVAL 集上进行。
- 任务条件：输入包含用户问题+多篇来源文档，要求模型输出带 [PROVE] 溯源标签的格式化解答。

### 3.2 对比方法

论文对比了 **14 个强 LLM**：
- **开源模型**：Baichuan2-7B、Vicuna-7B-v1.5、InternLM2.5-7B、Hunyuan-7B、Yi-1.5-9B、Llama-3.1-8B-Instruct、GLM-4-9B、Qwen3-8B、Gemma-3-12B-it、Qwen3-14B、GLM-4.5-355B。
- **闭源模型**：Gemini 2.5 Pro、GPT-5、Kimi。
- 所有模型使用统一的输入提示格式（问题+来源文档）。

### 3.3 评测指标
- **回答质量**：ROUGE-L、BLEU、METEOR、BERTScore、MoverScore（评分前剔除溯源标签）。
- **溯源准确度**：利用精确匹配比较文档ID、句子ID和关系类型，计算句子级精确率、召回率和 F1。
- **格式合规率**：输出是否严格遵循溯源 schema 的百分比。
- **LLM 评判**：将文本质量与溯源质量分离评判，综合给出 1–5 分。
- **人工评估**：3 位专家对 200 个抽样实例进行评分。

### 3.4 具体实验组

论文做了以下主要实验：
1. **主对比实验**：GenProve vs. 14 个基线模型，在所有指标上对比优劣。
2. **文档级引用 benchmark**：将句子级溯源降维为文档ID后，与已有文档级引用方法（VANILLA、SUMM、SNIPPET、APO、VeriCite、GERE）对比。
3. **消融实验**：
   - 去掉 GRPO（仅 SFT）
   - 去掉溯源奖励（只剩内容相似度奖励）
   - 去掉相似度奖励（只剩溯源 F1 奖励）
4. **按关系类型的细粒度诊断分析**：报告 Quotation / Compression / Inference 三类各自的 F1 热力图。
5. **GRPO 训练动力学分析**：观察训练过程中总奖励、内容相似度奖励和溯源 F1 奖励的变化趋势。
6. **LLM 评判与人工评判的一致性分析**：计算 Pearson 相关系数。
7. **定性错误分析**：展示错误案例，如错误关系类型、不同步溯源、溯源覆盖不完整、溯源定位错误等。

## 4. 资源与算力

- **论文未明确报告**使用的 GPU 型号、GPU 数量或具体训练时长。
- 仅提及训练配置细节：基础模型为 Qwen3-8B，使用 AdamW 优化器、学习率 2×10⁻⁵、最大序列长度 2048、梯度累积有效批次大小 16；GRPO 温度设为 1、β = 0.02、每轮更新迭代 4 次。
- 由于论文未披露完整算力开销，读者无法从文中获知训练 GenProve 的具体硬件成本。

## 5. 实验数量与充分性

### 5.1 数量评估

实验较为丰富：
- 覆盖 14 个不同规模的基线模型（7B 到 355B，含闭源模型）；
- 主结果表包含 10 项指标，全景对比了回答质量、溯源精度、格式合规与 LLM 评判；
- 有消融实验（3 个变体）、文档级跨粒度评测、按关系类型分解的 F1 分析、训练动力学分析、人工/自动评判一致性检验、多人错误案例分析。

### 5.2 充分性与公平性分析

- **充分**：整体实验设计覆盖了训练范式验证、跨粒度对比、消融验证、诊断分析和主观评判，逻辑链条完整。
- **较公平**：
  - 所有对比模型都使用统一输入提示格式；
  - 同时使用自动指标和 LLM/人工评判，降低单一指标的偏差；
  - LLM评判和人工评分高度相关（r = 0.9395），验证了自动评价的可靠性。
- **不足**：
  - 消融实验中去除内容相似度奖励后的 F1 反而更高（60.32 vs. 51.21），说明两目标之间存在一定权衡，论文对此的解释是"仅溯源匹配可由对参考答案忠实度较低的输出来满足"，但未能给出直观示例——这种"高溯源F1但低质量答案"的情况值得更深入的分析；
  - 只以 Qwen3-8B 作为训练基座，不同基座（如更大模型）上的迁移效果未做验证；
  - 没有报告多次随机种子的方差，统计显著性检验也未见描述。

## 6. 论文的主要结论与发现

1. **GenProve 全面领先**：在 ROUGE-L（57.25）、BLEU（42.22）、溯源 F1（51.21）、LLM 评判分数（3.14）等全部指标上超过了 14 个强 LLM 基线，建立了新的 SOTA。
2. **GRPO 对齐是关键**：去掉 GRPO 后评判分数从 3.14 降至 2.62，内容质量虽然接近但端到端综合质量大幅下降。
3. **复合奖励缺一不可**：二者的贡献是互补的——内容相似度奖励保障答案忠实度，溯源 F1 奖励保障句级证据定位与关系标注的正确性。
4. **存在"推理鸿沟"（reasoning gap）**：几乎所有模型在 Quotation 上表现较好，但在 Inference 和 Compression 上显著下降。GenProve 虽在这两类上提升最大，但 Inference F1 仍远低于 Quotation F1，说明可验证的逻辑推理依旧是尚未解决的前沿难题。
5. **句子级溯源可以向下兼容**：即使把句子级溯源压缩为文档级引用评价，GenProve（Doc-F1 92.43）也远超已有文档级引用方法（最高 GERE 81.10）。
6. **评判一致性高**：LLM 评判与人工评判在模型层面高度一致（r = 0.9395），说明自动评判在细粒度溯源评估中有效。

## 7. 优点

- **问题定义新颖且有现实价值**：将溯源从文本修饰性引用提升为生成的内在约束和结构化的句子级归因，尤其增加关系类型区分，"生成时"定位使验证路径更透明。
- **高质量数据集**：不是简单地用启发式或大模型自动标注，而是采用 LLM 提议+多阶段专家校验（含证据充分性和关系正确性双重核验）的闭环管线构建 ReFInE，提高了数据可依赖度。
- **奖励设计精细**：基于句对齐的内容相似度奖励与溯源 F1 奖励的组合，刻意惩罚"证据相关但关系类型错误"和"内容不支持证据"两类失败模式；且对齐阈值、相似度阈值等均有明确设定。
- **实验覆盖全面**：14 个基线、多维指标、多种分析视角（关系类型分解、训练动态、跨粒度迁移、人工评判一致性）等多种实验手段结合，验证较为立体。
- **诊断分析有洞察力**：准确定位了当前模型的薄弱环节（Inference vs. Quotation 的推理鸿沟），为后续研究指明方向。

## 8. 不足与局限

### 实验设计的不足
- **仅使用 Qwen3-8B 作为训练基座**：无法回答该方法在大模型或不同模型族上的迁移性。
- **缺少方差信息与显著性检验**：未报告多次运行的标准差，也未说明改进幅度的统计显著性。
- **消融中一个反直觉结果未被充分讨论**：去掉相似度奖励后溯源 F1 为 60.32（完整模型仅 51.21），说明单纯优化溯源 F1 可以在与参考答案对齐较差时反而取得更高 F1，论文的机制解释（"输出对参考答案忠实度不足也可以满足溯源匹配"）需要更多辅助证据才更有说服力。
- **文档级对比范围有限**：表 2 的对比基线为 2022–2025 年间更新的方法，没有包含更新的文档级引用 RAG 系统（如 2025 年底或 2026 年的工作），可能削弱跨粒度对比的时效性。

### 数据集的偏差与局限
- **单一语言**：ReFInE 只有英文，Quotation/Compression/Inference 分类间的边界在其他语言中何保持一致性没有验证。
- **QA 语料来源单一**：建立在 Yehudai 等（2024）的长式问答语料上，由 GPT-4o 建议、专家校验的标注流程仍可能受模型先验和注释者主观判断的影响，尤其 Inference 这类较难的情形更难保证判定的一致性。
- **剔除 "Other" 类别**：论文将这视为避免长尾模糊，但这也可能掩盖某些无法纳入三分类的证据与句子关系，从而在真实场景中暴露出分类覆盖度不足的问题。

### 工程部署与潜在风险
- **推理延迟增大**：需额外生成溯源三元组，输出 token 增加，实时场景下存在时延代价。
- **检索依赖性**：如果检索到的文档本身不包含答案，模型无法生成有效 provenance，端到端上限受制于检索质量。
- **误导信任风险**：正确格式的 provenance 并不能完全保证内容在事实层面或上下文层面适用，可能误导用户产生过度的信任感；有"错误的完整性"被隐藏的风险。

### 主要局限总结列表
- 全部实验和评测为英文，跨语言适用性未知。
- 单一的 Qwen3-8B 基座限制泛化结论。
- 缺乏多次运行的方差报告。
- 推理开销与实时性能未量化。
- 对检索器质量过于敏感（继承 RAG 通病）。

（完）
