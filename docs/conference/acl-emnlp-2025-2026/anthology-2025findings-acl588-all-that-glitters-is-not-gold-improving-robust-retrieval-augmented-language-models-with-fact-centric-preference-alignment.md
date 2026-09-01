---
title: "All That Glitters is Not Gold: Improving Robust Retrieval-Augmented Language Models with Fact-Centric Preference Alignment"
title_zh: 闪光的未必是金：通过以事实为中心的偏好对齐改进鲁棒检索增强语言模型
authors: "Jia Hao, Chunhong Zhang, Jiarun Liu, Haiyu Zhao, Zhiqiang Zhan, Zheng Hu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.588.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 面向检索增强语言模型的抗噪改进，采用事实中心偏好对齐
tldr: 检索增强语言模型易受检索结果中噪声文档影响，已有过滤器或微调方法可能丢失关键信息，且难以处理高语义相关但具干扰性的文档。论文提出以事实为中心的偏好对齐训练方法FPA，增强大模型直接从噪声检索结果中提取有用信息的能力，避免引入额外过滤器。实验表明该方法能提升模型在含噪检索场景下的鲁棒性和事实准确性，为RAG落地提供了重要改进。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 768, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 81, \"height\": 98, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 765, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 765, \"height\": 490, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 715, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1586, \"height\": 671, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1642, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1640, \"height\": 1340, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1631, \"height\": 1677, \"label\": \"Table\"}]"
motivation: 检索增强语言模型面对含噪检索文档很脆弱，现有过滤与微调方法会丢失关键信息且难处理高相关干扰项。
method: 提出基于事实中心偏好对齐FPA的训练方法，使模型直接从噪声检索结果中提取有用信息。
result: 实验证明FPA能提升RALM在噪声检索条件下的鲁棒性与事实准确性。
conclusion: 以事实为中心的偏好对齐能显著增强检索增强语言模型抗噪能力，对知识grounding实际应用具有重要意义。
---

## Abstract
Retrieval-augmented language model (RALM) relies on retrieved external knowledge to generate responses, resulting in vulnerability in the face of retrieval results with noisy documents. Previous works integrate additional filters or finetune Large Language Models (LLMs) to learn adaptive retrieval to reduce the performance damage of noisy documents. However, prior noise filtering may lead to the loss of crucial information, and these methods do not focus on distracting documents with high semantic relevance, which is the most challenging problem. In this study, we propose a training method for fact-centric preference alignment (FPA) to improve the ability of LLMs to directly extract useful information from noisy retrieval results without prior filtering. Our method performs positive document mining based on factual consistency and uses LLMs self-generated synthetic data as training data without manual annotation. We evaluate our FPA on four question answering benchmarks, and the experimental results demonstrate that our method achieves significant improvement with a small scale of training data.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与整体含义（研究动机与背景）

- **研究背景**：检索增强语言模型（RALM）通过引入外部检索知识来缓解 LLM 的知识缺失与幻觉问题，但检索结果天然含有噪声与不相关内容，这些噪声文档会误导 LLM 生成错误答案。
- **核心问题**：已有改进方法存在两方面不足：
  1. **后置过滤/压缩方法**（如 rerank、compress）可能导致关键信息丢失，反而损害性能；
  2. **适应性检索微调方法**（如 Self-RAG、RetRobust、InstructRAG）未聚焦于提升 LLM 对"高语义相似但事实无关"的**干扰性文档（distracting documents）** 的辨别能力，而这恰恰是最具挑战性的问题。
- **关键洞察**：文档是否包含答案字符串（如常见年份、国家名）并不等于文档与问题真正相关；判断文档相关性的更可靠维度是**事实层面的蕴含关系**，而非表面语义相似度。
- **论文立场**：与其额外增加过滤器，不如直接训练 LLM 从含噪上下文中提取有用信息、忽略干扰信息，并在检索结果信息不足时调用内部知识作答。

## 二、方法论：FPA（Fact-centric Preference Alignment）

### 1. 核心思想

FPA 以**事实一致性（factual consistency）** 为标准来判断文档相关性，并利用该标注构建**偏好数据（preference data）**，通过**直接偏好优化（DPO）** 微调 LLM，使其在含噪检索结果中更倾向于引用正文档、回避负文档。

### 2. 关键技术细节

**（1）以事实为中心的正文档挖掘（§3.2）**

- 将问题 q 与标准答案 â 构造成事实陈述 s = f(q, â)。
- 将"文档与事实陈述是否一致"转化为**文本蕴含识别（RTE）**任务：文档为 premise、事实陈述为 hypothesis。
- 使用 NLI 模型（BART-Large-MNLI）预测蕴含关系，若 Entailment 概率最高，则判定文档为**正文档**（事实一致）；否则为负文档。
- 初步实验中用 LLM 对文档进行四分类（相关 / 潜在不相关 / 不相关 / 干扰性文档），统计发现：RAG 答错时，**干扰性文档**占比显著更高，验证了该分类视角的有效性。

**（2）偏好数据构造（§3.3）**

- 从训练集中取 top-ks 检索文档（种子集合 Ds），筛选出包含至多 kt-1 个正文档的训练文档集合 Dt（实验设为 ks=8、kt=5）。
- **随机打乱文档顺序**，打破位置偏差，使正文档位置分布均衡。
- 通过提示中的**文档索引触发器**（如“According to documents 1 and 5”）控制模型引用的文档：
  - **chosen 响应**：引用全部正文档索引，仅保留回答正确的响应；
  - **rejected 响应**：依次加入单个负文档索引触发采样，仅保留回答错误的响应；
  - 构造多种噪声比例与正文档位置的偏好对。

**（3）引用错配数据增强（citation mismatch augmentation）**

- 将 chosen 响应中的引用索引改为未被引用的文档索引，构造成 rejected 响应，以缓解 LLM 引用幻觉问题。

**（4）训练目标**

- 使用 DPO 目标函数：
  - L_DPO = −E[log σ(rθ(x, y_w) − rθ(x, y_l))]
  - 其中 rθ(x,y) = β log(πθ(y|x)/πref(y|x))，x 为指令+文档+问题。

**（5）自适应检索提示（§3.4）**

- 在推理指令中提示 LLM：若检索文档不包含足够有用信息，可基于内部知识补充作答，增强模型在检索质量差时的鲁棒性。

## 三、实验设计

### 1. 数据集与 Benchmark

| 数据集 | 类型 | 检索器 | 训练/测试规模 |
|---|---|---|---|
| NQ | 短答案 QA | DPR | 79,168 / 3,610 |
| PopQA | 短答案 QA | Contriever | 12,868 / 1,399 |
| TriviaQA | 短答案 QA | Contriever | 78,785 / 11,313 |
| ASQA | 长答案 QA（带引用） | GTR | 4,353 / 948 |

### 2. 对比方法

- **无检索**：LLM 直接基于参数知识作答
- **无微调**：Vanilla RAG、RAG w/ rerank（RankT5-large）、RAG w/ compress（LongLLMLingua）
- **有微调**：Self-RAG、RetRobust、InstructRAG-FT（以及仅在 NQ 上训练的 InstructRAG-FT†）

### 3. 评估指标

- 短问答：精确匹配准确率（EM）
- ASQA：str-em、引用精确率（pre）、引用召回率（rec）

## 四、资源与算力

- **模型**：Llama-3-8B-Instruct 作为生成器，BART-Large-MNLI 作为 NLI 标注器。
- **训练配置**：LoRA 微调，2 张 NVIDIA RTX 4090 GPU，5 个 epoch，耗时约 3.5 小时。
- **训练数据规模**：仅构造 5,000 条偏好数据（取自 NQ 训练集子集），无需人工标注、无需 GPT-4。

## 五、实验数量与充分性

### 已进行的实验组别

1. **主实验**：4 个 QA 基准上对比 8 种基线方法。
2. **消融实验**：偏好对齐、自适应检索提示、引用错配数据增强三组件的单独/组合效果。
3. **鲁棒性分析**：
   - 不同噪声比例下的准确率；
   - 相关文档在不同位置时的准确率（Lost in the Middle 检验）；
   - 不同检索文档数量（k=1, 5, 10）的泛化性。
4. **内部知识与证据利用辨析**（w/ vs. w/o evidence）。
5. **效率对比**：训练数据量、是否需要额外模型、是否需要 GPT-4。
6. **案例研究**：含中文/英文示例多个，展示模型在检索结果无信息和有信息两种情况下的行为。

### 充分性与客观性评估

- **优点**：实验覆盖了多数据集、多检索器、跨领域泛化（短问答→长问答），消融充分，鲁棒性分析角度多样，且对公平性做了处理（对比了 InstructRAG-FT 仅在 NQ 上训练的外推表现）。
- **不足**：部分基线结果直接引用其他论文（标记 †），未完全复现；所有实验基于单一模型（Llama-3-8B），未验证在其他规模/架构 LLM 上的可迁移性。

## 六、主要结论与发现

1. FPA 在 NQ 上达到 66.9% EM、PopQA 上 67.1%、TriviaQA 上 78.7%、ASQA 上 48.8% str-em，四项均超过或追平最强基线 InstructRAG-FT。
2. 仅用 5k 偏好数据（远少于 Self-RAG 的 150k 和 InstructRAG 的 70k）即实现最优性能，数据效率显著更高。
3. 偏好对齐有效提升模型从噪声上下文中提取有用信息的能力；自适应检索提示在检索质量差时显著改善表现；引用错配增强提升引用准确性。
4. FPA 在不同噪声比例、不同相关文档位置、不同检索数量下均表现出优于基线的鲁棒性，且对相关文档的位置不敏感（缓解了 vanilla RAG 的 lost-in-the-middle 现象）。
5. 消融结果显示 FPA 模型确实在"分析证据"而非单纯依赖内部记忆——去掉证据后准确率大幅下降（如 NQ 从 66.9% 降到 49.9%）。

## 七、优点与亮点

1. **新颖的文档相关性判别视角**：以事实蕴含关系代替表面语义相似度，从"是否包含答案"转向"事实是否一致"，更本质地区分干扰性文档。
2. **全自动数据构造流程**：无需人工标注、无需 GPT-4，仅依赖 NLI 模型 + LLM 自生成响应，成本低、可复现。
3. **偏好对齐引入 RAG 鲁棒性优化**：将 DPO 应用于"引用正文档/回避负文档"的偏好学习，思路新颖且有效。
4. **引用错配数据增强**：针对 LLM 引用幻觉的巧妙的负样本构造策略。
5. **随机文档顺序打乱**：有效缓解位置偏差，提升模型对不同上下文位置的鲁棒性。
6. **自适应检索提示**：以零成本的方式补充了模型在检索信息不足时的应对能力。
7. **数据效率出色**：5k 训练样本即达到 SOTA 级效果，具有较强实用性。
8. **实验分析细致**：包含噪声比例、文档位置、文档数量等多维度鲁棒性分析，验证充分。

## 八、不足与局限性

1. **检索质量极差时改进有限**：论文自述当检索结果几乎完全不相关时，FPA 的增益会大幅受限，仍依赖检索器本身的性能上限。
2. **任务覆盖有限**：仅在单跳开放域 QA（短问答 + 长问答）上验证，未涉及多跳推理、领域特定任务或更复杂的知识密集型场景。
3. **单一模型架构**：所有实验基于 Llama-3-8B-Instruct，未验证方法在更大/更小或不同架构（如 Mistral、Qwen）上的通用性。
4. **依赖标准答案标注**：正文档挖掘需要 ground truth 答案来构造事实陈述，在无标准答案的真实场景中应用受限。
5. **NLI 模型能力瓶颈**：BART-Large-MNLI 对复杂事实蕴含的判断准确性可能成为标注质量的瓶颈，且论文对 NLI 误判的影响缺乏误差分析。
6. **基线对比公平性存疑**：部分基线结果直接引用原论文数字，各方法使用的检索器、训练数据规模不完全一致，可能影响对比的严格公平性。
7. **训练数据来源偏窄**：仅在 NQ 子集上构造偏好数据，虽然外推实验表现良好，但对其他数据分布的自适应能力缺乏更系统的验证。
8. **引用质量**：ASQA 上的引用精确率（58.3%）并非最优（低于 Self-RAG 的 69.7%），因为偏好数据鼓励引用尽量多的正文档而非最小充分子集，这在追求精确引用的应用场景中可能不理想。
9. **单次运行**：论文声明所有结果为单次运行，未报告多次运行的方差（可能受限于算力）。

（完）
