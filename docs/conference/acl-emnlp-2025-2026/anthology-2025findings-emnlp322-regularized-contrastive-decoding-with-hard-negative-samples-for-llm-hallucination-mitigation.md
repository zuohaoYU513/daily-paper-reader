---
title: Regularized Contrastive Decoding with Hard Negative Samples for LLM Hallucination Mitigation
title_zh: 基于难负样本的正则化对比解码用于大模型幻觉缓解
authors: "Haonan Sheng, Dou Hu, Lingwei Wei, Wei Zhou, Songlin Hu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.322.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 采用难负样本的正则化对比解码缓解大模型幻觉
tldr: 大模型在生成时仍会出现复杂形式的幻觉，现有对比解码方法对简单幻觉有效但难以应对多样模式。该工作利用难负样本构造事实性更弱的模型，提出正则化对比解码(RCD)，通过对抗式学习捕捉更多样的幻觉信号。实验表明RCD在多个基准上优于现有幻觉缓解方法，提升生成可靠性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1476, \"height\": 982, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 770, \"height\": 412, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 621, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1600, \"height\": 463, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 721, \"height\": 758, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 700, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 795, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 524, \"height\": 251, \"label\": \"Table\"}]"
motivation: 现有对比解码方法多局限于简单幻觉，难以有效缓解复杂幻觉。
method: 使用难负样本构造事实性更弱的模型，并引入正则化对比解码信号。
result: 实验证明RCD能更全面地缓解大模型幻觉。
conclusion: 难负样本与正则化结合能显著增强推理时幻觉缓解。
---

## Abstract
Large language models are prone to generate hallucinations, which can undermine their reliability in high-stakes applications. Some works on LLM hallucination mitigation use the model’s internal signals to contrast different output during inference stage. However, these works often focus on simple forms of hallucinations, and struggle to effectively mitigate hallucinations. To address the issue, this paper exploits hard negative samples to construct a factually weaker model for improving contrastive decoding. We propose a new inference-time method, Regularized Contrastive Decoding (RCD), to capture correct hallucination signals for mitigating hallucinations in LLMs. RCD learns more diverse hallucination patterns via adversarial-aware fine-tuning and mitigates hallucinations via contrastive decoding. Experiments on four hallucination benchmarks demonstrate that our method achieves better LLM hallucination mitigation performance. Further analysis shows RCD generalizes well across different model sizes, task formats, perturbation methods and training data sizes.

---

## 论文详细总结（自动生成）

# 《基于难负样本的正则化对比解码用于大模型幻觉缓解》论文总结

## 1. 核心问题与研究动机

- **大模型幻觉问题**：大型语言模型（LLMs）在生成文本时，经常产生与事实不符或偏离输入上下文的"幻觉"（hallucination）内容，在医疗咨询、法律建议、专业技术支持等高风险场景中带来严重风险。
- **现有对比解码（CD）方法的局限**：
  - 已有基于模型内部信号的对比解码方法（如 DoLa、CD、AD、ICD 等）通常只在简单幻觉上有效，难以应对与真实答案语义接近的"细微幻觉"。
  - 部分方法利用已有幻觉数据集训练模型来提供幻觉信号，但这些数据往往包含**显式、易识别**的幻觉模式，容易导致模型过拟合特定模式和有限数据的偏差，无法泛化到复杂场景中的细微幻觉。
- **核心研究问题**：如何在推理阶段获取更准确、更多样化的幻觉信号，从而更有效地抑制大模型的幻觉生成？

## 2. 方法论：正则化对比解码（RCD）

RCD 是一种**推理时（inference-time）** 的幻觉缓解方法，核心思想是**利用难负样本（hard negative samples）构造一个"事实性更弱"的模型**，再通过与原始模型的对比解码来过滤幻觉内容。

### 2.1 阶段一：基于 LoRA 的对抗感知微调

- 使用 LoRA（低秩适配）参数高效微调，冻结基础模型参数 θ，仅更新增量参数 Δθ，通过最小化负对数似然预估：
  - **min** Δθ Σᵢ −log p(yᵢ | xᵢ; θ + Δθ)
- 引入**快速梯度法（FGM）**在词嵌入层生成 L2 归一化的对抗扰动 rᵢ = −ϵ·gᵢ/‖gᵢ‖₂，其中 gᵢ 是对输入的梯度。
- 采用**最大-最小（min-max）训练策略**构建难负样本，联合优化原始样本与对抗样本的损失：
  - **L_total = ½(L(x, y) + L_adv(x+r, y))**
- 对抗扰动作为一种**隐式正则化机制**，迫使模型在细微分布偏移下更好地泛化，从而捕捉更多样的幻觉模式、生成更难识别的难负样本。

### 2.2 阶段二：与事实较弱模型的对比解码

- 将原始强模型与对抗微调后的弱势（幻觉）模型在每个时间步的 log 概率做对比：
  - **F_t = log p(xₜ|x<ₜ; θ) − λ·log p(xₜ|x<ₜ; θ+Δθ)**
  - λ 控制对比强度。
- 采用**自适应相对顶部过滤（adaptive relative top filtering）机制**：
  - 根据强模型概率确定有效候选集 V_valid，再对 F_t 分数做 softmax 归一化。
- 弱势模型由于经过对抗微调，倾向于生成**更多样、更准确**的幻觉信号，使原始模型的输出分布更可靠、事实性更强。

## 3. 实验设计

### 3.1 数据集与 Benchmark

| 数据集 | 类型 | 规模/说明 |
|--------|------|-----------|
| **TruthfulQA** | 真实性问答 | 817 个选择题（38 个类别）+ 开放生成任务 |
| **FACTOR** | 事实性补全 | Wiki（2,994 样本）、News（1,036 样本）、Expert（236 样本） |
| **TriviaQA** | 知识问答 | 约 650K 问答对 |
| **Natural Questions (NQ)** | 知识问答 | 约 300K 人工生成问题 |

### 3.2 评估指标

- TruthfulQA：MC1 / MC2 / MC3 准确率；开放生成任务用 GPT-3.5 打分（truth、info、truth×info、reject 率）
- FACTOR：准确率
- TriviaQA 与 NQ：Exact Match（EM）和 F1

### 3.3 对比方法

| 方法 | 简述 |
|------|------|
| Greedy | 贪心解码基线 |
| ITI | 推断时干预（内部激活偏移） |
| CD | 强/弱模型对比解码 |
| DoLa | 层间对比解码 |
| AD | 激活解码（基于熵校准） |
| ICD | 诱导幻觉后对比解码（强基线） |

### 3.4 主要设置

- 原始模型：Llama2-7B-Chat；弱势模型：在 HaluEval 数据集上微调的 Llama2-7B-Base。
- 微调数据：HaluEval 的 QA、Sum、Dialog 及 All 子集（共 30K 条）。
- 扰动半径 ϵ 在 {0.01, 0.1, 1} 中搜索。

## 4. 资源与算力

- 实验使用**单个 NVIDIA Tesla A100 80GB GPU** 完成。
- 未在正文中明确报告具体训练时长、GPU 数量或总体算力消耗，仅提及使用 LLaMA-Factory 框架实现 LoRA 微调。这属于论文中一项信息缺口。

## 5. 实验数量与充分性

论文共包含约 **10 组以上**不同维度的实验，覆盖面较广：

| 实验 | 说明 |
|------|------|
| 判别式评估（主实验） | 4 个基准 × 多个指标，对比 7 种方法 |
| 生成式评估 | TruthfulQA 开放生成任务 |
| 消融实验 | ① 用随机扰动替代对抗扰动；② 完全去除扰动 |
| 任务格式实验 | QA / Sum / Dialog / All 四种微调数据格式 |
| 训练数据比例实验 | 20%–100% 不同采样比例 |
| 扰动方法实验 | FGM vs. PGD |
| 扰动半径参数分析 | ϵ ∈ {0.01, 0.1, 1} |
| 模型规模实验 | Llama2-7B / 13B / 70B-Chat |
| 整体能力评估 | MMLU 和 ARC-Challenge |
| 案例研究 | 对 NQ 具体例子的 token 概率分析 |
| 效率分析 | 延迟对比（附录） |
| λ 缩放因子分析 | λ ∈ [1.0, 2.0]（附录） |

- **充分性评价**：实验设计整体较为全面和客观，覆盖了方法的不同组件、不同数据条件、不同模型大小和多种扰动策略，且与最先进的 ICD 方法进行了直接对比。每个基准上选择最优任务格式和扰动半径，可能带来一定程度的"选择性报告"偏差。

## 6. 主要结论与发现

1. **RCD 在四个基准上全面优于现有方法**：
   - TruthfulQA：MC1 提升 +12.44%（相对 Greedy）、MC2 提升 +19.75%。
   - FACTOR Expert：准确率提升 +12.71%。
   - TriviaQA：EM 提升 +4.67%，F1 提升 +4.42%。
2. **对抗扰动是关键组件**：消融实验表明，替换为随机扰动或去除扰动后性能显著下降（如 TruthfulQA MC2 从 74.35 降至 65.56 与 69.08）。
3. **RCD 在不同任务格式、训练数据大小、扰动方法下均有较好的泛化能力**，且随模型规模增大性能持续提升。
4. **RCD 不损害 LLM 的通用能力**：在 MMLU 上保持基线水平（0.472），在 ARC-Challenge 上略优于基线。
5. **推理延迟可接受**：RCD 延迟约为基线 2.78 倍（384.7s vs 138.4s），比 ICD 的 2.91 倍略低，同时取得更好效果。

## 7. 方法优点

- **创新性强**：首次将"难负样本"概念引入幻觉缓解的对比解码框架，通过对抗训练构造更贴近决策边界的幻觉样本，而非从静态数据中学习显式幻觉。
- **隐式正则化机制**：对抗扰动不是简单的数据增强，而是让弱势模型学会在细微分布偏移下产生更精确的幻觉信号，从而在对比解码中更好地抑制伪造内容。
- **即插即用的推理时方法**：无需外部检索或额外推理基础设施，易于部署。
- **综合实验设计**：实验规模大、维度多，涵盖模型规模、数据格式、扰动方法、训练数据比例、参数分析和效率分析，验证了方法的鲁棒性和通用性。
- **案例研究直观**：通过具体实例（"rock and roll hall of fame" 中 1986 vs 1995）清楚地展示了 RCD 与 ICD 在幻觉信号质量上的差异。

## 8. 不足与局限

- **计算开销**：需要额外训练一个事实性较弱的模型，且对抗微调过程需要计算梯度扰动，增加了一定的训练成本；推理时也需要同时运行两个模型。
- **模型覆盖有限**：仅在 Llama-2 系列上验证，未扩展到 GPT、Mistral、Qwen 等其他主流架构，泛化性仍有待验证。
- **硬件资源要求**：需要 A100 级别 GPU 才能较好运行，且未提供训练时长、GPU 数量等成本指标，无法全面评估资源效率。
- **效率分析配置不一致**：CD 使用 13B+7B 配置，ICD 和 RCD 使用 7B+7B 配置，导致延迟对比不是严格公平的对照实验。
- **任务范围局限**：幻觉缓解主要验证了问答和补全任务，未涉及多轮对话、长文档生成、翻译等更多样的任务形态。
- **伦理风险**：训练得到的事实较弱模型本身可能被滥用，用来故意生成和传播虚假信息，需要有安全管控。

**（完）**
