---
title: "FactCorrector: A Graph-Inspired Approach to Long-Form Factuality Correction of Large Language Models"
title_zh: FactCorrector：面向大语言模型长文事实性纠正的图启发方法
authors: "Javier Carnerero-Cano, Massimiliano Pronesti, Radu Marinescu, Tigran T. Tchrakian, James Barry, Jasmina Gajcin, Yufang Hou, Alessandra Pascale, Elizabeth M. Daly"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2147.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用结构化反馈对LLM事实错误进行事后纠正，提升事实性
tldr: 针对LLM生成内容的事实错误问题，提出FactCorrector事后纠正方法。它利用结构化反馈获取事实性信息并生成纠正版本，无需重新训练即可跨域适应。同时构建VELI5基准，包含系统性注入的错误和参考答案。实验证明该方法在多个长文事实性数据集上有效，为事实性纠正提供了新工具和评测基础。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 761, \"height\": 858, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1329, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 743, \"height\": 329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 708, \"height\": 353, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 810, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 694, \"height\": 2003, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 749, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 701, \"height\": 1950, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 680, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 687, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1565, \"height\": 1591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2147/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 996, \"height\": 1795, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 720, \"height\": 809, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 568, \"height\": 982, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 721, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 567, \"height\": 1048, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 566, \"height\": 982, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 569, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 766, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 779, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 587, \"height\": 1251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 796, \"height\": 1480, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1045, \"height\": 1339, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1055, \"height\": 1337, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1592, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1596, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1054, \"height\": 1335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1594, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1079, \"height\": 836, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 712, \"height\": 662, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1295, \"height\": 721, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 719, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1363, \"height\": 780, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2147/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1367, \"height\": 569, \"label\": \"Table\"}]"
motivation: LLM在知识密集任务中常产生事实错误，需要高效的事后纠正方法。
method: 基于结构化反馈的图启发式纠正，结合VELI5基准进行可靠评测。
result: 在多个长文事实性数据集上验证了纠正效果和跨域适应性。
conclusion: 为LLM事实纠正提供免训练、可跨域的后处理方案。
---

## Abstract
Large language models (LLMs) are widely used in knowledge-intensive applications but often generate factually incorrect responses. A promising approach to rectify these flaws is correcting LLMs using feedback. Therefore, in this paper, we introduce FactCorrector, a new post-hoc correction method that adapts across domains without retraining and leverages structured feedback about the factuality of the original response to generate a correction. To support rigorous evaluations of factuality correction methods, we also develop the VELI5 benchmark, a novel dataset containing systematically injected factual errors and ground-truth corrections. Experiments on VELI5 and several popular long-form factuality datasets show that the FactCorrector approach significantly improves factual precision while preserving relevance, outperforming strong baselines. We release our code at https://ibm.biz/factcorrector.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 一、核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLMs）在知识密集型应用中广泛使用，但经常生成事实错误或幻觉内容，这成为其在医疗、金融等高风控领域安全部署的重大障碍。
- **现有方法不足**：
  - **训练时纠正**（如RLHF、DPO）对闭源或超大规模模型不可行，成本过高。
  - **生成时纠正**（如generate-then-rank、反馈引导解码）依赖批评模型在解码过程中提供高质量的中间反馈，但反馈信息有限。
  - **事后纠正**（如Self-Refine、CRITIC、RAC）在完整输出生成后进行，但当前的反馈形式简单（纯文本），未能利用语句与证据之间复杂的结构关系（如蕴涵、矛盾）。
- **核心问题**：如何在无需重新训练的情况下，利用**结构化反馈**对LLM长文输出进行有效的事后事实性纠正，并确保方法能跨域、跨模型泛化。
- **整体含义**：本文提出了一种新的事后纠正范式，将图模型引入反馈机制，同时构建专门的评测基准，填补了长文事实性纠正方法在结构化反馈与评测数据两方面的空白。

---

### 二、论文提出的方法论

#### 2.1 核心思想

**FactCorrector**是一种事后（post-hoc）事实性纠正方法，核心思路是：将批评模型（Critic）判定的事实性反馈以**结构化形式**（错误原子 + 相关证据 + 关系类型）传给精炼模型（Refinement Model），引导其生成更准确且保留相关性的修正答案。方法无需重新训练，可跨域、跨模型直接应用，并支持单次或迭代纠正。

#### 2.2 关键技术组成部分

| 模块 | 功能 |
|------|------|
| **Atomizer（原子化器）** | 将输入响应分解为一系列原子单元（atomic units），每个原子代表一个单一事实/主张 |
| **Reviser（修订器）** | 将原子中的代词、未知实体或残缺名称替换为响应中对应的完整命名实体 |
| **Retriever（检索器） | 利用LLM为每个原子生成Google搜索查询，检索外部知识源中的相关上下文片段 |
| **Evaluator（评估器）** | 构建概率图模型，计算每个原子的后验边际概率 P(ai)，判定原子为True / False / Unverified |

#### 2.3 核心算法流程（Algorithm 1）

1. 评估初始响应 y 的事实精确率 Pr(y)；
2. 当 Pr(y) 低于阈值 θ 时迭代循环：
   - 将 y 分解为原子集合 Ay = {a1, ..., an}；
   - 修订原子（去上下文化）；
   - 从外部知识源 K 检索上下文集合 Cy = {c1, ..., cm}；
   - 构建图模型 G = ⟨X, D, F⟩，其中变量为原子和上下文，因子为原子-上下文间的蕴涵/矛盾关系；
   - 对每个原子 ai，计算后验概率 P(ai) 并标注为 True（>0.5）、False（<0.5）或 Unverified（=0.5）；
   - 构建**结构化反馈**：包含所有标注为 False 或 Unverified 的原子、与错误原子在图模型中相连的上下文，以及对应的关系类型；
   - 精炼模型 R 基于原始响应和结构化反馈生成修正版 y′；
   - 重新评估 Pr(y′)，若 Pr(y′) > Pr(y) 则更新 y，否则终止循环并返回当前 y。

#### 2.4 关键公式与定义

- **事实精确率**：Pr(y) = S(y) / |Ay|，其中 S(y) 为被外部知识源支持的原子数；
- **事实召回率**：R_K(y) = min(S(y)/K, 1)，其中 K 为第 K 个被支持原子；
- **F1@K**：F1@K(y) = 2·Pr·R_K / (Pr + R_K)，当 S(y) > 0 时；
- **相对增益**：G(S) = 2·(Sc − Sr) / (Sc + Sr)，用于比较修正前后同一指标 S 的变化；
- **图模型推断**：使用 Weighted Mini-Buckets（WMB）算法计算后验边际概率，i-bound 设为 6，单次推理在 0.05 秒内完成。

#### 2.5 VELI5基准数据集构建

- 基于 ELI5-Category 数据集，选取每个问题下点赞数最高的回复作为**规范回复**；
- 使用 FactCorrector 对规范回复进行修正，形成事实性纠正的参考答案；
- 使用 mixtral-8x22b-instruct-v0.1 生成**故意含有事实错误**的合成回复，与人类回复比例为 50:50；
- 最终数据集包含 **17,522 个实例**，均匀分布于 12 个类别，划分为训练（14,017）、验证（1,752）、测试（1,753）三部分。

---

### 三、实验设计

#### 3.1 数据集与评测场景

| 数据集 | 规模 | 用途与特点 |
|--------|------|-----------|
| **VELI5** | 测试子集随机采样200例 | 同时包含自然和系统注入的错误，有多种分布 |
| **Biographies（BIO）** | 183个传记段落 | 由ChatGPT生成，维基百科为知识源 |
| **AskHistorians（ASKHIST）** | 200个问答对 | 由llama-3.3-70b-instruct生成长文回答 |
| **CONFLICTS** | 100个原子声明 | 所有声明均为真，用于测试纠正器是否会错误修改正确内容（稳定性测试） |

#### 3.2 对比方法（Baselines）

| 方法 | 描述 |
|------|------|
| **CRITIC** | 基于检索的迭代提示纠正方法 |
| **RAC** | 原子级检索增强纠正方法 |
| **LLM1** | 仅依靠模型内部知识进行纠正，无外部检索 |
| **LLM2** | 仅使用为问题检索的上下文，不使用结构化关系，忽略内部知识 |
| **SFT（ours）** | 使用VELI5训练的LoRA适配器（Granite-Guardian-5B）进行纠正 |

#### 3.3 评估指标

- **事实性指标**：精确率（Pr）、召回率（R@K）、F1@K，由 FactReasoner 评估器基于 Google 搜索结果计算；
- **补充指标**：可验证性（V）、全面性（C）；
- **稳定性指标**（仅CONFLICTS）：ROUGE、BLEU、BLEURT 相似度、JUDGE（LLM-as-a-Judge 判定修正与原文是否语义等效）；
- **相对增益** G(S) 用于比较不同纠正器的改进幅度。

#### 3.4 基础模型

实验使用 4 种开源 LLM 家族：IBM Granite（granite-4.0-h-small）、Meta LLaMA（llama-3.3-70b-instruct）、MistralAI Mixtral（mixtral-8x22b-instruct-v0.1）、OpenAI（gpt-oss-120b）。

---

### 四、资源与算力

- 论文明确提到：所有 LLM 在 **A100 80GB GPU** 上远程托管，通过 litellm API 访问，服务能力为 **1,500 prompts/秒**；
- 但论文**未明确说明**具体的 GPU 数量、总训练时长或总计算成本；
- 附带的效率分析提到：FactCorrector 的纠正步骤平均耗时 2.30 秒，FactReasoner 评估平均耗时 22.37 秒；端到端延迟约 177.7 秒（30 个 VELI5 样本，llama-3.3-70b-instruct），其中评估（验证）占据主要计算开销。

---

### 五、实验数量与充分性

#### 5.1 实验组数

| 实验类型 | 数量 |
|---------|------|
| 数据集数量 | 4 个（VELI5, BIO, ASKHIST, CONFLICTS） |
| 基础模型数量 | 4 种（Mixtral, LLaMA, Granite, GPT-OSS） |
| 纠正器数量 | 6 种（CRITIC, RAC, LLM1, LLM2, FC, SFT） |
| 指标数量 | 5 个事实性指标 + 4 个稳定指标（ROUGE/BLEU/BLEURT/JUDGE） |
| SFT实验 | VELI5、BIO、ASKHIST三个数据集上的LoRA训练评估 |
| 人类评估 | 30个任务、每任务平均2.30个错误原子和4.40个正确原子 |
| 统计显著性检验 | 对 G(Pr) 进行单侧t检验，报告p值 |

#### 5.2 充分性与公正性评价

- **优点**：实验设计较为全面，覆盖自然与注入错误、同分布与跨分布数据、不同模型架构与规模；使用统一独立的测评协议（FactReasoner + Google搜索），避免评估循环性；额外进行了人类评估和统计显著性检验，增强了结论可信度。
- **潜在不足**：
  - VELI5 的实验仅使用测试集 200 个实例抽样，规模偏小；
  - 所有方法共享同一评估器，如果评估器本身有系统性偏差，会影响所有方法的横向比较；
  - LLM1/LLM2 在 VELI5 上表现突出，论文将其归因于预训练语料涵盖 Reddit 内容，但未做进一步验证；
  - 未报告在闭源模型（如 GPT-4、Claude）上的实验结果。

---

### 六、论文的主要结论与发现

1. **FactCorrector 在 VELI5 上全面领先**：在所有指标上相对增益最优，精确率宏观平均增益达 0.315，平均将精确率提升约 +0.21，超过所有基线（LLM1 +0.17、RAC +0.16）。
2. **在 BIO 数据集上表现强劲**：在 Mixtral 和 Granite 上取得最高增益，在 LLaMA 上排名第二，优于或与依赖维基百科预训练优势的 RAC/LLM2 相当。
3. **在 ASKHIST 上是最稳定的纠正器**：由于原始响应精确率本来就高（>89%），所有基线均出现负增益，而 FactCorrector 几乎总是不降低事实性，甚至略有提升。
4. **在 CONFLICTS 稳定性测试中表现优异**：在 Mixtral 和 Granite 上取得最高的 ROUGE/BLEU/BLEURT 相似度，表明它不会对正确内容进行不必要的编辑。
5. **结构化反馈的价值得到验证**：LLM2 与 FactCorrector 的持续性能差距表明：显式的关系（蕴涵/矛盾）基础比仅仅给出证据更有价值。
6. **SFT 纠正器具有较好的泛化能力**：虽然域内表现最好，但在域外的 BIO 和 ASKHIST 上大多数增益仍为非负。

---

### 七、优点

1. **创新性**：首次将概率图模型（FACTREASONER）的**结构化反馈**引入事后纠正，超越了简单的纯文本反馈模式；
2. **模块化设计**：批评模型与精炼模型分离，不绑定特定评估器；纠错过程可与不同LLM灵活组合；
3. **免训练、跨域适应**：无需微调即可在不同领域和多种模型架构上工作；
4. **提供VELI5基准**：包含系统注入的错误和参考答案，为后续研究提供可复现的评测平台；
5. **评估全面**：同时涵盖事实性、可验证性、全面性、稳定性、相似度、人类评估等多个维度，并加入统计显著性检验；
6. **实际部署友好**：提供LoRA SFT变体，只需单次LLM调用即可完成纠正，大幅降低成本；
7. **计算开销分析清晰**：明确区分了评估与纠正的成本，并提供延迟对比数据。

---

### 八、不足与局限

1. **组件对提示质量敏感**：Atomizer、Reviser、Evaluator 和 Corrector 均依赖 LLM 提示质量及 few-shot 示例，较脆弱的组件可能导致分解或评估偏差；
2. **仅覆盖开源模型**：未在闭源模型（GPT-4、Claude等）上验证，通用性受限制；
3. **分解粒度受限**：当前仅支持一次性（one-shot）分解，未探索句子级、段落级等不同粒度对纠正效果的影响；
4. **检索质量依赖**：外部证据质量取决于查询构造和 Serper API 的返回结果，可能受限于搜索引擎覆盖面和网页抓取长度；
5. **计算开销高**：完整 pipeline 需要 O(n·m) 次 LLM 调用提取原子-上下文关系（n=原子数，m=上下文数），相比 SFT 的单次调用成本高得多；
6. **迭代机制简单**：仅比较当前修正是否优于原响应（Pr比较），缺少更精细的收敛判断；
7. **部分场景改进有限**：在 ASKHIST 等原始精确率已很高的场景，收益很小；在 CONFLICTS 上使用 LLaMA 和 GPT-OSS 时表现不如 RAC；
8. **VELI5 中 LLM1/LLM2 表现优势**：论文推测与预训练语料重叠有关，但没有严格控制或排除这一混淆因素；
9. **人工评估规模偏小**：仅 30 个任务，且未报告标注者间一致性（inter-annotator agreement）；
10. **相对增益指标的潜在误导性**：当原始指标接近 0 或 1 时，相对增益可能被放大或压缩，论文未对这种边界效应进行讨论。

---

（完）
