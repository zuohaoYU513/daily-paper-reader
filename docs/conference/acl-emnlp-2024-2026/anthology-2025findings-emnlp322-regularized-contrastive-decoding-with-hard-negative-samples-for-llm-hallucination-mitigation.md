---
title: Regularized Contrastive Decoding with Hard Negative Samples for LLM Hallucination Mitigation
title_zh: 基于困难负样本的正则化对比解码用于大语言模型幻觉缓解
authors: "Haonan Sheng, Dou Hu, Lingwei Wei, Wei Zhou, Songlin Hu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.322.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 利用硬负样本构造弱事实模型并做正则化对比解码，正对应约束解码等幻觉缓解手段
tldr: 针对已有对比解码多只处理简单幻觉、缓解能力有限的问题，论文提出RCD。它从困难负样本学习更多样的幻觉模式，并加入正则化项约束对比解码过程，在推理阶段抑制复杂幻觉。实验结果显示RCD相比已有对比解码基线在幻觉缓解上明显更优，可作为提高大模型输出可靠性的有效解码工具。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 586}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1476, \"height\": 982}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 460}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 477}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp322/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 770, \"height\": 412}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 496}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 190}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 301}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 545}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 621, \"height\": 414}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1600, \"height\": 463}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 721, \"height\": 758}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 700, \"height\": 266}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 795, \"height\": 320}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp322/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 524, \"height\": 251}]"
motivation: 现有幻觉缓解对比解码方法处理简单幻觉有效，但面对复杂多样的幻觉模式效果有限。
method: 使用困难负样本构造事实性较弱的参照模型，通过正则化对比解码放大真实与幻觉输出的差异。
result: 在幻觉缓解实验中，RCD较已有方法更有效地降低了各类幻觉生成。
conclusion: 推理期利用困难样本与正则化对比可提升大模型幻觉抑制能力。
---

## Abstract
Large language models are prone to generate hallucinations, which can undermine their reliability in high-stakes applications. Some works on LLM hallucination mitigation use the model’s internal signals to contrast different output during inference stage. However, these works often focus on simple forms of hallucinations, and struggle to effectively mitigate hallucinations. To address the issue, this paper exploits hard negative samples to construct a factually weaker model for improving contrastive decoding. We propose a new inference-time method, Regularized Contrastive Decoding (RCD), to capture correct hallucination signals for mitigating hallucinations in LLMs. RCD learns more diverse hallucination patterns via adversarial-aware fine-tuning and mitigates hallucinations via contrastive decoding. Experiments on four hallucination benchmarks demonstrate that our method achieves better LLM hallucination mitigation performance. Further analysis shows RCD generalizes well across different model sizes, task formats, perturbation methods and training data sizes.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与研究动机

- 大型语言模型（LLM）在多种自然语言处理任务中表现优异，但仍频繁产生**幻觉**（hallucination），即生成与事实不符或与上下文不一致的内容，这在法律咨询、医疗建议、技术问答等高风险场景中会造成严重风险。
- 已有的幻觉缓解方法主要分为三类：
  - **基于检索增强生成（RAG）**：引入外部知识库，但依赖额外基础设施且对检索错误敏感；
  - **依赖模型内部信号**：如基于内部表示、注意力分布等进行干预；
  - **推理期对比解码（Contrastive Decoding, CD）**：通过强/弱模型或不同层间的输出差异来抑制幻觉输出，实现简单且部署方便。
- 但现有对比解码方法存在明显短板：**多只针对简单、显式的幻觉**，难以捕捉与真实内容语义相近的**细微（subtle）幻觉**，导致幻觉抑制效果有限。
- 进一步地，部分方法使用已有幻觉数据微调弱模型来提供对比信号（如 ICD），但这些数据往往模式单一，模型容易过拟合到有限的训练模式，**泛化能力不足**，在复杂场景下仍容易失效。
- 核心研究问题：如何为对比解码提供**更准确、更多样、更接近真实决策边界**的幻觉信号，从而更有效地缓解LLM在推理阶段的幻觉。

## 2. 研究方法论：Regularized Contrastive Decoding（RCD）

### 核心思想
- 利用**对抗训练**生成**难负样本（hard negative samples）**，据此微调一个**事实性更弱的模型（factually weaker model，即“幻觉模型”）**；
- 在推理阶段，通过**正则化的对比解码**，用原始模型与“幻觉模型”的输出分布之差来抑制幻觉token，从而保留真实内容并滤除虚假内容。
- 比普通对比解码的关键优势在于：微弱模型能学到**更多样、更精准的幻觉模式**，从而提供更可靠的“负向信号”。

### 关键步骤一：基于对抗的LoRA微调构建事实性更弱模型
- 冻结原始模型参数 $\theta$，仅通过 LoRA 训练增量参数 $\Delta\theta$，最小化原始样本上的负对数似然：
  $$ \min_{\Delta\theta} \sum_{i=1}^{m} -\log p(y_i \mid x_i; \theta+\Delta\theta) $$
- 引入**快梯度法（Fast Gradient Method, FGM, Miyato et al., 2017）**在**词嵌入层**上生成L2归一化的对抗扰动：
  $$ r_i = -\epsilon \frac{g_i}{\|g_i\|_2}, \quad g_i = \nabla_{x_i} \log p(y_i \mid x_i; \theta+\Delta\hat{\theta}) $$
- 采用 **min-max 训练策略**：目标函数为原始损失与对抗损失的平均：
  $$ \mathcal{L}_{total} = \frac{1}{2} \left( \mathcal{L}(x,y) + \mathcal{L}_{adv}(x+r, y) \right) $$
- 该对抗性扰动相当于一种**数据依赖的正则项**，防止模型只拟合原始数据，引导模型在决策边界附近学到更鲁棒的幻觉模式。

### 关键步骤二：基于事实性更弱模型的对比解码
- 在每一步解码时，用原始模型与微调后的弱模型计算对比得分：
  $$ F_t = \log p(x_t \mid x_{<t}; \theta) - \lambda \log p(x_t \mid x_{<t}; \theta+\Delta\theta) $$
  其中 $\lambda$ 控制弱模型的惩罚强度。
- 采用**自适应相对top过滤机制**（源自Li et al., 2023b），仅保留强模型概率较高的候选token集合 $V_{valid}$，再对 $F_t$ 做 softmax 得到最终分布，避免过度惩罚可能的正确token。
- 通过上述过程，RCD可以在推理阶段不额外引入外部知识库的前提下，实现更细粒度的幻觉抑制。

## 3. 实验设计

### 数据集与Benchmark
- **TruthfulQA**（MC1/MC2/MC3，开放生成任务另有 truth/info 指标）：考察LLM的真实性；
- **FACTOR**（News、Wiki、Expert三个子集）：衡量事实知识文本补全准确性；
- **TriviaQA**（EM、F1）：常识问答；
- **NQ (Natural Questions)**（EM、F1）：真实用户级事实问答；
- 此外使用 **HaluEval** 的 QA、Sum、Dialog 及其并集作为微调幻觉模型的数据来源；
- 整体效果评估还使用了通用能力benchmark：**MMLU** 与 **ARC-Challenge**。

### 对比方法
- Greedy Decoding（贪婪解码基线）
- ITI（Inference Time Intervention）
- CD（标准Contrastive Decoding）
- DoLa（层间对比解码）
- AD（Activation Decoding）
- ICD（Induce-then-Contrast Decoding，与RCD最接近的方法）

### 主要实验设置
- 原始模型为 **Llama2-7B-Chat**，弱模型为在 HaluEval 上微调的 **Llama2-7B-Base**；
- CD采用Llama2-13B-Chat与7B-Chat对比；ICD和RCD均使用7B-Chat与微调7B-Base对比；
- LoRA参数高效微调，使用Adam优化器，学习率5e-4，batch大小256，每个benchmark训练5个epoch（截断后共4个epoch？文末附录显示TruthfulQA、FACTOR、TriviaQA、NQ均为5 epochs，具体为表格中“Number of epochs 5 5 5 5”）；
- 对抗扰动半径 $\epsilon$ 在 {0.01, 0.1, 1} 中搜索，不同benchmark选择最优值。

## 4. 资源与算力

- 论文在方法部分提到“所有实验在单个 NVIDIA Tesla A100 80GB GPU 上运行”；
- 未报告具体的训练时长、GPU数量或总计算量（如FLOPs）；
- 报告了推理延迟：在某种数据规模下，贪婪解码约138.4s，CD约357.6s（2.58×），ICD约402.4s（2.91×），RCD约384.7s（2.78×）——但说明该测量只是近似趋势，因为CD使用了13B+7B的配置，ICD/RCD则用7B+7B。
- 总体而言，算力与训练成本信息较为粗略，未给出精确的GPU小时数，这是资源描述方面的一个信息不足。

## 5. 实验数量与充分性

论文开展的实验较充足，可以概括为以下几个层次：
- **主实验（4个benchmark + 指标）**：覆盖真实性（TruthfulQA、FACTOR）和知识问答（TriviaQA、NQ），并包括判别式评估和TruthfulQA开放生成评估；
- **消融研究**：分为“w/o Adv Perturb”（对抗替换为随机扰动）和“w/o Perturb”（完全去掉扰动），验证对抗样本的必要性；
- **数据task格式影响**：分别在HaluEval的Sum、Dialog、QA、All上微调弱模型进行比较；
- **数据规模影响**：在20%~100%不同比例的微调数据上测试RCD与ICD；
- **不同对抗攻击方法**：FGM vs. PGD 的对比；
- **扰动半径参数分析**：epsilon ∈ {0.01, 0.1, 1} 对四个benchmark的影响；
- **不同模型规模**：7B/13B/70B Chat模型上的推广实验；
- **对MMLU和ARC-Challenge的影响**：检验是否会损失通用模型能力；
- **案例研究**：通过实例展示RCD为何能够抑制幻觉token而保留正确答案；
- **效率分析**：比较推理延迟。

评价：
- 实验维度较全面，既包括横向比较（多个SOTA基线），也包含纵向深入分析（消融、参数、数据规模、模型规模、扰动方法）；
- 对比方法均复现自开源代码（除ITI外），公平性较好；
- 局限性：所有实验基于 **Llama-2 系列**，没有在GPT、Mistral等其他架构上验证；部分结果仅报告了最佳设置而不是平均值，可能引入选择偏差；论文未提供完整的多次运行方差或显著性检验结果；由于HaluEval与评测数据可能存在数据分布重叠，需谨慎对待泛化结论。

## 6. 主要结论与发现

- **RCD在4个幻觉benchmark上全面优于所有基线**。如在TruthfulQA MC2上比Greedy基线提高19.75个百分点，MC3提升19.86；FACTOR Expert提升12.71个百分点；TriviaQA与NQ上也稳定获得提升。
- 与最强的同类方法ICD相比，RCD在几乎所有设置和指标上均更优，说明引入难负样本生成的幻觉模式有利于对比解码。
- 生成式评测（TruthfulQA open-ended）中，RCD相比ICD在信息量(info)和truth&info指标上明显提升，同时降低拒答率，说明RCD并非靠回避作答来提升真实性。
- 消融证明：去对抗扰动后性能显著下降（甚至与ICD相若），说明**对抗扰动是有效生成多样化细微幻觉的必要成分**。
- RCD在不同数据task格式、不同训练数据比例、不同对抗方法（FGM/PGD）、不同扰动半径和**不同模型规模（7B/13B/70B）**下都能稳定提升幻觉缓解效果，展示出较好的**泛化性与可扩展性**。
- RCD不会损害LLM的一般能力：MMLU与Baseline持平，ARC-Challenge略优于Baseline和ICD。
- 方法额外计算代价相对可接受（相对贪婪解码约2.78倍延迟），且低于ICD，换取更优的幻觉抑制。

## 7. 优点

- **问题定向准确**：针对已有对比解码方法无法有效捕捉“细微幻觉”的核心瓶颈，提出用难负样本逼近真实幻觉分布的技术路线，具有较强的实际动机。
- **方法设计新颖且技术清晰**：将对抗训练（FGM/PGD）与对比解码有机结合，使得弱模型学到的“幻觉信号”更贴近决策边界；min-max训练目标也提供了明确的正则化解释。
- **实验充分、多角度验证**：不仅给出主指标提升，还通过消融、任务格式、训练数据比例、模型规模、扰动方法、通用能力benchmark等证明方法的稳健性；案例研究直观解释了对比信号为何有效。
- **不依赖外部知识库或额外推理时的大量开销**，属于推理期干预，易于嵌入已有模型。
- **透明性较好**：在附录中提供了超参、效率分析等细节，便于复现。

## 8. 不足与局限

- **模型类型覆盖单一**：实验仅用Llama-2系列验证（7B/13B/70B），未推广到Mistral、Qwen、GPT等架构，结论的通用性需要更多验证。
- **资源数据披露不足**：虽然提到单卡A100 80GB，但未给出训练总时长、微调成本或GPU卡时数；无法准确评估部署成本。
- **可能存在评测选择偏差**：文中多个实验（如task format对比、epsilon选择）只报告“在该benchmark上的最优表现”，且未提供方差、多次随机种子重复或统计显著性检验，可能削弱结论说服力。
- **微调数据来源有限**：采用HaluEval作为唯一幻觉诱导数据源，格式主要为QA、Summarization、Dialog，不覆盖所有幻觉类型（如代码、数学推理中的幻觉），且在真实数据上的迁移能力未知。
- **性能存在输入/超参敏感**：不同benchmark最优epsilon相差较大（TruthfulQA最优0.01，FACTOR最优1），表明方法对扰动强度较敏感，实际应用需要调参。
- **推理延迟仍较高（约2.78倍）**：虽然低于ICD，但仍然明显慢于贪婪解码，在实时应用场景可能受限。
- **伦理风险**：训练出的“事实性更弱模型”如果被恶意利用，可能被用于故意制造误导信息；论文对此也做了伦理声明，需要谨慎控制使用范围。

---

（完）
