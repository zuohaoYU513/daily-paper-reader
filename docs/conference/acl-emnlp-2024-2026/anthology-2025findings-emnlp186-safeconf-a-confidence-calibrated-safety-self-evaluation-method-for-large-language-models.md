---
title: "SafeConf: A Confidence-Calibrated Safety Self-Evaluation Method for Large Language Models"
title_zh: SafeConf：一种置信度校准的大语言模型安全自评估方法
authors: "Bo Zhang (波章,), Cong Gao, Linkang Yang, Bingxu Han, Minghao Hu, Zhunchen Luo, Guotong Geng, Xiaoying Bai, Jun Zhang, Wen Yao, Zhong Wang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.186.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 面向LLM自身安全评估中的过度自信，用置信度校准与自一致性提升自评估准确性
tldr: 面向大模型在安全自评估中过度自信、评估结果失真问题，提出SafeConf方法。它通过对原始安全问题做语义变异并采用自一致性策略，基于回答正确性来量化置信度，从而校准安全自评估。实验证明该方法在提升安全自评估准确性的同时缓解了过度自信，为大模型安全可控生成提供了保障。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp186/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 744, \"height\": 1071, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp186/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 689, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp186/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1668, \"height\": 1297, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp186/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 814, \"height\": 738, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1639, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 822, \"height\": 923, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 760, \"height\": 502, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 789, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp186/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 761, \"height\": 274, \"label\": \"Table\"}]"
motivation: 大模型对自身生成内容的安全评估常存在过度自信，这会影响安全自评估的可靠性。
method: 通过语义变异生成自一致性样本，以答案一致性量化置信度，并用其校准大模型的安全自评估结果。
result: 在安全评测中，SafeConf能有效降低过度自信程度并提高安全自评估的准确性。
conclusion: 置信度校正是提升LLM安全自评估能力的重要途径，可支撑安全可控的内容生成。
---

## Abstract
Large language models (LLMs) have achieved groundbreaking progress in Natural Language Processing (NLP). Despite the numerous advantages of LLMs, they also pose significant safety risks. Self-evaluation mechanisms have gained increasing attention as a key safeguard to ensure safe and controllable content generation. However, LLMs often exhibit overconfidence, which seriously compromises the accuracy of safety self-evaluation. To address this challenge, we propose SafeConf , a method to enhance the safety self-evaluation capability of LLMs through confidence calibration. The method performs semantic mutations on the original safety evaluation questions and adopts a self-consistency strategy to quantify confidence based on answer accuracy on the mutated questions. Finally, these confidence scores are used to construct a dataset for fine-tuning. We conducte experiments on both Chinese and English datasets. The results show that SafeConf improves self-evaluation accuracy by an average of 5.86% and 7.79% over the state-of-the-art baseline methods on Qwen2.5-7B-Instruct and Llama3-8B-Instruct models, respectively, without affecting the general capabilities of the models.

---

## 论文详细总结（自动生成）

# SafeConf: 置信度校准的安全自评估方法——论文详细中文总结

## 1. 核心问题与整体含义

- **研究背景**：大语言模型（LLM）在 NLP 等领域取得重大进展，但伴随显著安全风险（价值偏差、隐私泄露、恶意攻击等）。为保障模型可靠部署，需对其安全性进行全面评估。
- **关键挑战**：“LLM-as-a-judge”自评估范式虽受关注，但 LLM 普遍存在**严重过度自信（overconfidence）**，导致安全自评估结果不可靠、准确性受损，因此亟需置信度校准（confidence calibration）来提升安全自评估能力。
- **核心洞察**：现有基于训练（training-based）的置信度校准方法，仅从单一视角和单一表达形式生成置信度分数，量化效果欠佳。作者假设：**在安全评估问题中引入语义多样性（diversity），进行多视角评估，可增强置信度校准的有效性**。

## 2. 方法论：SafeConf

SafeConf 的核心思路与流程如下：

1.  **多样化语义变异（Diverse Semantic Mutation）**：
    - 使用 GPT-4o mini 对原始安全评估多选题进行语义改写，生成语义变体 {Qi1…Qik}，保持题目核心含义与作答选项不变；
    - 设计了**三档变异强度提示词**（低/中/高多样性），控制变异幅度；
    - 观察实验（图 2、附录 D）发现**高多样性变异生成的训练数据可使模型的 ECE 最低**，校准效果最好。
2.  **置信度量化（Confidence Quantification）**：
    - 用 GPT-4o mini 对原始问题和变异后的问题分别进行推理作答；
    - 基于**自一致性策略（self-consistency）**，以变异问题上回答与标准正确答案 R*i* 的匹配程度（正确率 Acci）来量化置信度分数 Confi，计算公式如下：

    > Acc_i = Σ I(R_ij = R*_i) / k

    即：在 k 次变异问题上，回答与标准答案一致的比例，即为置信度分数。
3.  **微调数据集构建（Dataset Construction）**：
    - 每条训练样本包含五个要素：指令 Inst、安全问题 Qi、模型答案 Ri、评估结果 Evali、置信度 Confi；
    - 采用**置信度阈值策略**（confidence thresholding）：仅保留「判定为安全（safe）且置信度 > 0.5」或「判定为不安全（unsafe）且置信度 < 0.5」的样本，以强化置信度与安全判断之间的判别一致性；
    - 指令将安全性判断与置信度融合：回答安全则置信度应高，不安全则置信度应低；
    - 训练数据量被刻意限制（570 条），在提升能力的同时尽量减少对基础模型固有能力的干扰。
4.  **训练与安全自评估**：
    - 使用 LLaMA-Factory 进行**监督微调（LoRA）**，对齐模型的置信度表达与实际正确率；
    - 微调后模型在安全评估数据集上进行自评估，输出「安全/不安全」标签及 0-1 置信度分数。

## 3. 实验设计

### 3.1 数据集

| 用途 | 数据集 | 说明 |
|---|---|---|
| 构造微调训练集 | CValues（29,132 条） | 安全域对齐数据集，筛选后微调数据 570 条 |
| 选择题安全测试 | SafetyBench（11,434 条） | 多元安全知识多选题 |
| 开放问答安全测试 | S-eval（10,000 条）、JADE（2,000 条）、DAN（935 条） | 开放域安全问答 |
| 通用能力评测 | MMLU、GSM8K、CMMLU | 检验微调是否损伤常识、数学与中文推理能力 |

实验中使用了中英文双语的多种安全评测场景，覆盖选择题与开放问答两种形式。

### 3.2 模型

- Qwen2.5-7B-Instruct、Qwen2.5-32B-Instruct（验证可扩展性）、Llama3-8B-Instruct。

### 3.3 对比基线

- **Verbalize Confidence**（口头置信度）
- **First Token Probability**（首 token 概率）
- **Self-consistency**（自一致性）
- **Intention Analysis**（意图分析）
- **Self-Defense**（LLM 自防御）
- **SafeConf-01**（作者自设简化变体，安全即为 1、不安全即为 0 的硬标签置信度）

### 3.4 评估指标

- **ACC**（自评估准确率）
- **ECE**（期望校准误差，越低校准越好）
- **CS**（余弦相似度，衡量语义变异多样性）
- **ASR**（攻击成功率，越低越安全）

## 4. 资源与算力

- **论文正文未明确给出**所使用的 GPU 型号、数量以及训练时长。
- 仅从附录可获知微调参数：使用 **LoRA**（rank 16，alpha 未明确），学习率 5e-5，**训练 25 个 epoch**，batch size 16，bf16 精度，使用 LLaMA-Factory 框架完成。
- 注释/变异生成环节使用了 OpenAI 的 **GPT-4o mini** 作为辅助模型，但未报告其推理调用量与费用。

## 5. 实验数量与充分性

论文做了较为充分的系列实验，可归纳为以下 **7 类**：

1.  **主结果（表 2、3）**：在 Qwen2.5-7B、Llama3-8B 上对比 6 种基线的 ECE 与 ACC，覆盖 SafetyBench、S-eval、JADE/DAN。
2.  **校准可视化（图 4）**：细粒度对比微调前后置信度-准确率的分布。
3.  **消融/机制分析（表 4）**：剔除置信度信息后的 SFT 对比，验证置信度分数的作用。
4.  **多样性参数分析（表 5）**：3 变异强度 × 4 变异次数（k=3/5/7/10）的语义相似度实验。
5.  **安全性影响评估（表 6）**：微调前后 ASR 对比，共 2 模型 × 3 数据集。
6.  **通用能力评估（表 7）**：微调前后在 MMLU、GSM8K、CMMLU 的表现。
7.  **规模扩展性（附录 E）**：在 Qwen2.5-32B-Instruct 上验证 SafeConf 效果。

**总体评价**：
- 优点：覆盖了多模型、中英文、多题型、多任务场景，包含消融、安全性影响与泛化能力验证，整体设计较为系统；人工注释一致性以 Cohen's kappa（0.90+）佐证了数据可靠性。
- 不足：多样性分析仅测了语义相似度单一维度和单一源数据集，未深入分析变异选项的多样性分布；置信度数据完全依赖 GPT-4o mini 产生，虽有 kappa 报告但抽样与标注细则有限；无统计显著性检验报告。

## 6. 主要结论

1.  **提高安全评估问题的语义多样性可有效提升置信度校准效果**——三个多样性档位中，高多样性数据集训练的模型 ECE 最低（SafetyBench 上低至 0.0509，而低多样性仅 0.1301）。
2.  **SafeConf 显著改善置信度校准能力**：Qwen2.5-7B-Instruct 在 SafetyBench 上 ECE 从 0.2989/0.1643（基线）降至 0.0509；Llama3-8B 上同样大幅下降（如 SafetyBench 上从 0.2243/0.2610 降至 0.2085）。
3.  **置信度校准有效提升安全自评估准确率**：与最强基线（即未微调的原始模型/Verbalize 等）相比，Qwen2.5-7B-Instruct 平均提升 **5.86%**，Llama3-8B-Instruct 平均提升 **7.79%**；在 SafetyBench 选择题上的增益尤其显著（可达 +10% 以上）。
4.  **置信度标签是效果提升的关键**：带置信度训练的模型显著优于仅带安全标签（safe/unsafe）训练的模型（表 4），说明置信度信号为安全自评估提供了更具判别力的训练信息。
5.  **微调不损害模型原有安全性与通用能力**：ASR 在多数数据集上反而下降，MMLU、GSM8K、CMMLU 分数基本持平。
6.  **该方法在更大模型（Qwen2.5-32B）上同样有效**（SafetyBench 达 0.7701，优于所有基线）。

## 7. 优点与亮点

- **方法创新性良好**：将「语义变异多样性」引入训练数据的构建流程，与现有仅靠单一问题多采样的自一致性方法形成鲜明对比——SafeConf 从不同表述和语义上下文中综合评估原始问题，能更全面捕捉概率不确定性。
- **设计精巧**：三档变异 prompt + 阈值筛选策略（safe>0.5 与 unsafe<0.5）构建判别性训练样本，方法具有较好的逻辑解释性。
- **实验设计较完备**：系统回答 5 个关键研究问题（是否有效、为何有效、多样性参数影响、是否损伤安全性、是否影响通用能力），逻辑闭环严谨。
- **评估可靠性较好**：对 GPT-4o-mini 的安全标注进行了 3 人独立人工一致性检验（Cohen's kappa 0.903-0.916，极为接近完全一致），增强数据可信度。
- **兼顾安全与通用性双重考量**：附加 ASR 与基础 benchmark 检测，排除微调带来的副作用。
- **跨规模验证**：在 7B、8B、32B 三种模型上验证方法的可扩展性。

## 8. 不足与局限

- **扩展性有限**（作者自述）：处理复杂文本/长文本时效率受限，可能影响复杂场景下的置信度校准与安全评估质量。
- **资源成本较高**（作者自述）：与免训练方法相比需要 GPU 资源进行微调及多次推理生成，实际部署成本偏高。
- **依赖 GPT-4o mini**：变异样本生成与推理过程依赖外部大模型，存在一定的封闭生态依赖，且论文未详细评估不同辅助模型对结果的影响（如 GPT-4o vs GPT-4o-mini vs 开源模型的差异）。
- **多样性指标较单一**：仅用余弦相似度（CS）判断语义多样性，未结合人工评价或更丰富的文本多样性指标（如词法/句法/语义多维度差异）进行验证，且多样性分析未比较不同变异来源。
- **训练数据规模较小（570 条）**，虽是有意控制，但其多样性和覆盖度是否足以推广到更多安全场景仍有待进一步探讨。
- **统计严谨性**：未报告多次运行的方差、显著性检验（如配对 t 检验或 bootstrap），结论的稳健性证据略显不足。
- **通用性局限**：结果表明 SafeConf 对选择题和开放题的提升幅度不一致（选择题上的增益更大），且实验数据多为由标准答案或 GPT-4o mini 标注的合成评估结果，真实场景下无标准答案的自评估性能有待实证。
- **多语言覆盖有限**：论文声称中英文双语，但总体以中文数据集（CValues、JADE 等）为训练基础，英文数据的语义变异质量与多语言泛化性缺少深入分析。

---

（完）
