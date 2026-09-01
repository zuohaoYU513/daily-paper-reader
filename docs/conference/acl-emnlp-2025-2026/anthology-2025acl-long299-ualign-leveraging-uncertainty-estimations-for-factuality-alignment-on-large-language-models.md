---
title: "UAlign: Leveraging Uncertainty Estimations for Factuality Alignment on Large Language Models"
title_zh: UAlign：利用不确定性估计实现大语言模型事实对齐
authors: "Boyang Xue, Fei Mi, Qi Zhu, Hongru Wang, Rui Wang, Sheng Wang, Erxin Yu, Xuming Hu, Kam-Fai Wong"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.299.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用不确定性估计指导事实对齐
tldr: 为改善大模型在知识边界模糊时的事实表达，提出UAlign框架。该方法先计算置信度与语义熵两种不确定性来表征知识边界，再将其显式加入提示词指导模型对齐事实知识。实验显示该方法能显著提升知识问答中的事实准确性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 676, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1583, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 752, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 775, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 576, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 781, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1456, \"height\": 2123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1580, \"height\": 1680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 605, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 606, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long299/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 606, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1602, \"height\": 1023, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 765, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1347, \"height\": 929, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 702, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 729, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 566, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 660, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 550, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1646, \"height\": 974, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long299/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1653, \"height\": 666, \"label\": \"Table\"}]"
motivation: 大模型在知识边界模糊时难以准确表达已知事实。
method: 利用置信度和语义熵表示知识边界，将其作为提示特征引导模型与事实知识对齐。
result: 实验表明UAlign明显提升模型的事实表达能力。
conclusion: 展示了不确定性估计用于事实对齐的有效性。
---

## Abstract
Despite demonstrating impressive capabilities, Large Language Models (LLMs) still often struggle to accurately express the factual knowledge they possess, especially in cases where the LLMs’ knowledge boundaries are ambiguous. To improve LLMs’ factual expressions, we propose the UAlign framework, which leverages Uncertainty estimations to represent knowledge boundaries, and then explicitly incorporates these representations as input features into prompts for LLMs to Align with factual knowledge. First, we prepare the dataset on knowledge question-answering (QA) samples by calculating two uncertainty estimations, including confidence score and semantic entropy, to represent the knowledge boundaries for LLMs. Subsequently, using the prepared dataset, we train a reward model that incorporates uncertainty estimations and then employ the Proximal Policy Optimization (PPO) algorithm for factuality alignment on LLMs. Experimental results indicate that, by integrating uncertainty representations in LLM alignment, the proposed UAlign can significantly enhance the LLMs’ capacities to confidently answer known questions and refuse unknown questions on both in-domain and out-of-domain tasks, showing reliability improvements and good generalizability over various prompt- and training-based baselines.

---

## 论文详细总结（自动生成）

# UAlign（UA LIGN）论文总结

## 1. 核心问题与研究动机

- **背景问题**：大语言模型（LLMs）虽然预训练阶段习得了大量事实知识，但在知识边界模糊时，往往无法准确表达自己“已知但不确定”的知识，甚至会对不熟悉的问题表现出过度自信并产生幻觉。这种“已知”与“表达”之间的差距严重影响了模型的可靠性与可用性。
- **关键洞察**：模型的知识并非简单的“已知/未知”二分，而是存在一个“弱已知”的模糊区域（论文以光谱图示意）。已有对齐工作很少显式利用知识边界信息来引导模型，导致模型无法区分“该自信回答”与“该拒绝回答”的问题。
- **研究目标**：通过显式建模模型自身的知识边界，设计对齐方法，使 LLM 能对已知问题自信作答、对未知问题明确拒绝，从而缩小“已知”与“表达”之间的差距，提升事实性和可靠性。

## 2. 方法论：UAlign 框架

### 核心思想
利用两种不确定性估计（置信度 + 语义熵）表征 LLM 的知识边界，并将这些估计值作为额外输入特征注入提示词，通过 SFT 和 PPO 两阶段训练实现事实性对齐。

### 关键技术细节与流程

**（1）数据集准备**
- 对每个问题采样 K=10 个响应：使用 10 个不同的 1-shot 提示模板、温度 T=0.2，在“准确性与多样性”间折中。
- 对每个问题计算两个不确定性指标：
  - **置信度（Confidence）**：基于采样答案与标准答案的匹配准确率，公式为：
    \( c_i = \frac{1}{K}\sum_{k=1}^{K} \mathbf{1}(\hat{y}_i = y_i^{(k)}) \)
  - **语义熵（Semantic Entropy）**：对语义等价的答案聚类后计算熵，衡量答案分布离散度：
    \( e_i = -\sum_s p(s|x_i)\log p(s|x_i) \)
- 标注规则：若至少一个采样答案正确，则该问题视为“已知”；若全部错误则视为“未知”，并将其标准答案改写为“Sorry, I don't know.”，以训练模型学会拒绝未知问题。

**（2）UAlign SFT 阶段**
- 训练两个不确定性估计模型 τ、μ：分别以问题 \(x_i\) 为输入，预测置信度和语义熵，损失为交叉熵 \(L_\tau\)、\(L_\mu\)。
- 训练奖励模型 θ：以 (问题 \(x_i\)、置信度 \(c_i\)、语义熵 \(e_i\)、生成答案 \(y_i^{(k)}\)) 为输入，预测答案正确性，使用二元交叉熵损失 \(L_\theta\)。

**（3）UAlign PPO 阶段**
- 将问题与预测的置信度、语义熵拼接成提示，喂给策略模型 πθ 生成回答。
- 奖励函数由两部分构成：
  \( r = \theta(x, y, c, e) - \beta \cdot \mathrm{KL}[\pi_\theta(x,c,e)\,\|\,\pi_o(x)] \)
  其中第一部分来自奖励模型的奖励信号 r1，第二部分为 KL 惩罚 r2，防止策略偏离原始模型过远。
- 使用 PPO 算法迭代优化策略模型参数。

## 3. 实验设计

### 数据集
- **训练集（In-domain）**：TriviaQA（TVQA）、SciQ、NQ-Open 三个知识密集型问答数据集。
- **测试集（In-domain）**：各数据集的验证/测试集。
- **OOD 测试集**：LSQA（多语言、语言特定知识问答数据集），用于评估泛化能力。

### 评估指标
- **Precision**：已知问题中被正确回答的比例，衡量“准确表达已知知识”的能力。
- **Truthfulness**：正确回答已知问题 + 正确拒绝未知问题占全部问题的比例，衡量模型的诚实度。
- 采用字符串匹配变体 \(y \in \hat{y} \lor \hat{y} \in y\) 而非严格 exact match，并通过人工评估验证了该指标的有效性。

### 对比方法
- **Prompt-based**：ICL、ICL-IDK（含拒绝示例）、ICL-CoT（思维链）。
- **SFT-based**：标准 SFT、R-Tuning（未知问题训练拒绝回答）。
- **RL-based**：RL-PPO、RLKF（知识反馈强化学习）、RL-DPO（直接偏好优化）。
- **Inference-based**：ITI（推理时激活干预）。

### 基础模型
- Llama-3-8B 与 Mistral-7B，均使用 LoRA 微调。

## 4. 资源与算力

- **硬件**：所有实验在 4 张 NVIDIA A100-40GB GPU 上进行，模型以 fp16 加载。
- **数据构建成本**：以 10,000 条 QA 样本为例：
  - Llama-3-8B：采样 10 次约需 25 分钟；
  - Llama-3-70B：采样 10 次约需 2 小时 12 分钟。
- **推理成本**：UAlign 推理需先预测两个不确定性 token 再生成答案，时间略有增加，例如 TVQA 上从 58 分钟增至 1 小时 6 分钟，增量很小。
- **额外参数量**：不确定性估计模型为 LoRA（rank=4）插件，额外参数不足基础模型参数的 1%。
- **说明**：论文未给出 PPO/SFT 训练的完整总时长和能耗数据，仅提供了数据采样与推理的时间成本分析。

## 5. 实验数量与充分性

### 实验规模
- **主实验**：2 个基础模型 × 4 个测试集（3 个 in-domain + 1 个 OOD）× 2 个指标，与 9 类基线全面对比。
- **消融实验**：
  - 去除置信度/去除语义熵的变体（w/o Conf.、w/o Entro.）对比；
  - 奖励模型在四种不确定性特征组合下的准确率对比（✓✓ / ✓✗ / ✗✓ / ✗✗）；
  - 采样数量 K=1/4/7/10 对性能和计算成本的影响。
- **不确定性估计可靠性实验**：AUROC 对比概率法、p(True)、言语化（Verbalized）等基线方法，覆盖多个数据集（主文展示 TVQA，其余见附录）。
- **人工评估**：对多种 EM 变体进行人工标注，以选择最优正确性判定指标。

### 充分性与客观性评价
- 实验设计较为系统：覆盖 prompt、SFT、RL、推理干预四大类方法，且包含消融与泛化测试，结论可信度高。
- 但实验范围局限于实体级知识问答任务，未覆盖长文本生成、开放式指令跟随等复杂场景；评估指标依赖字符串匹配，对表达形式多样的回答可能不够鲁棒。

## 6. 主要结论与发现

- **显著提升**：UAlign 在 Llama-3 和 Mistral 上均一致优于所有基线，ID 与 OOD 测试集上的 Precision 和 Truthfulness 均取得最优或接近最优结果。
- **置信度是关键**：奖励模型消融实验显示，置信度（Conf.）对准确率提升贡献最大；语义熵单独使用不稳定，但与置信度联合使用可达到最佳效果。
- **能挖掘“弱已知”知识**：语义熵帮助模型识别“虽然置信度低但答案分布相对确定”的情况，从而避免将已知但不确定的问题误判为未知并拒绝回答。
- **不确定性估计更可靠**：UAlign 学到的置信度和语义熵在 AUROC 上优于概率、p(True)、言语化等基线方法。
- **泛化能力强**：多数训练型基线在 OOD（LSQA）上性能下降，而 UAlign 表现稳定，接近或超过 prompt-based 方法。
- **采样数量收敛**：K=10 已能较好逼近真实知识边界，继续增大 K 收益递减，是性能与成本的合理折中。

## 7. 优点

- **方法新颖**：据论文所述，这是首个显式将不确定性估计作为知识边界表征引入 LLM 对齐工作的研究，为后续研究开辟了新方向。
- **思路清晰**：将“知识边界”转化为可计算、可训练的两类不确定性数值（置信度 + 语义熵），并贯穿数据集构建、奖励模型训练和策略优化全过程。
- **实验严谨**：覆盖多种主流基线、双模型验证、多数据集评估、OOD 泛化测试、奖励模型内部消融、采样数影响分析以及人工评估，论证链条完整。
- **工程实用性强**：额外参数占比极低，推理时间开销小，并提供了不同采样规模的时间成本与加速方案分析，具备实际部署可行性。
- **具有可解释性**：通过“置信度低但语义熵高”的案例说明模型如何被引导输出不确定但正确的知识，机制直观。

## 8. 不足与局限

- **任务覆盖有限**：仅在封闭式事实知识 QA 上验证，未涉及开放式指令跟随、长文本传记生成、多步推理等场景；这些场景中不确定性估计本身更困难，方法有效性尚未证明。
- **计算成本偏高**：数据构建依赖多次采样（K=10），成本随采样数线性增长；虽采用 LoRA、vLLM 等加速手段，但扩展到更大模型或更大规模数据时开销仍然可观。
- **模型规模有限**：实验仅使用 8B/7B 级别的模型，未在更大模型（如 70B 及以上）上验证可扩展性与收益。
- **评估指标局限**：正确性判定基于字符串包含关系，可能对同义改写、间接回答等处理不佳；知识边界标注依赖“采样是否含正确回答”，采样随机性可能引入噪声。
- **潜在偏差风险**：知识边界是模型在特定采样配置下的近似估计，不同提示模板、温度设置可能影响标注质量；训练集由三个数据集混合组成，各数据集的分布差异可能影响模型对齐效果。
- **未报告全部训练成本**：缺少 SFT/PPO 阶段的精确 GPU 时长与能耗数据，不利于完整评估方法的综合开销。

（完）
