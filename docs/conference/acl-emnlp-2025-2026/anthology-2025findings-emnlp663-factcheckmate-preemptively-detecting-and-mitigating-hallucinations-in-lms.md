---
title: "FACTCHECKMATE: Preemptively Detecting and Mitigating Hallucinations in LMs"
title_zh: FACTCHECKMATE：预先检测并缓解语言模型幻觉
authors: "Deema Alnuhait, Neeraja Kirtane, Muhammad Khalifa, Hao Peng"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.663.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用隐藏状态分类器预先检测并缓解语言模型幻觉
tldr: 针对语言模型幻觉难以提前发现的问题，提出FactCheckmate方法。它基于输入上的隐藏状态学习分类器，在解码前预测模型是否可能产生幻觉；若检测到幻觉，则通过调整隐藏状态进行干预，引导模型生成更事实性的输出。实验证明这种方法能有效提前发现并缓解幻觉，为白盒幻觉干预提供了新思路。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 211, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1277, \"height\": 2257, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 656, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 661, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1272, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp663/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1482, \"height\": 384, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 808, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1649, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 771, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1567, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 769, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1637, \"height\": 1106, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1561, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1213, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp663/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1651, \"height\": 263, \"label\": \"Table\"}]"
motivation: 现有幻觉检测多在生成后进行，缺乏解码前的预防手段。
method: 学习基于隐藏状态的分类器，预测幻觉并在解码前调整隐藏状态进行干预。
result: 在多个任务上证明能够预先检测幻觉并提升生成事实性。
conclusion: 揭示了隐藏状态可用于幻觉的预防性检测与干预。
---

## Abstract
Language models (LMs) hallucinate. We inquire: Can we detect and mitigate hallucinations before they happen? This work answers this research question in the positive, by showing that the internal representations of LMs provide rich signals that can be used for this purpose. We introduce FactCheckmate, which preemptively detects hallucinations by learning a classifier that predicts whether the LM will hallucinate, based on the model’s hidden states produced over the inputs, before decoding begins. If a hallucination is detected, FactCheckmate then intervenes by adjusting the LM’s hidden states such that the model will produce more factual outputs. FactCheckmate provides fresh insights that the inner workings of LMs can be revealed by their hidden states. Practically, both its detection and mitigation models are lightweight, adding little inference overhead; FactCheckmate proves a more efficient approach for mitigating hallucinations compared to many post-hoc alternatives. We evaluate FactCheckmate over LMs of different scales and model families (including Llama, Mistral, Qwen and Gemma), across a variety of QA datasets from different domains. Our results demonstrate the effectiveness of FactCheckmate, achieving over 70% preemptive detection accuracy. On average, outputs generated by LMs with intervention are 34.4% more factual compared to those without.

---

## 论文详细总结（自动生成）

## 详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：语言模型（LMs）在生成文本时经常产生“幻觉”（hallucination），即输出看似合理但事实上错误或误导性的内容。现有幻觉检测与缓解方法大多为**事后反应式**（post-hoc / reactive），即模型生成完内容后再进行检测与纠正，例如重采样新输出或借助外部工具/外部LM验证，推理开销较高且将模型视为黑盒。
- **研究动机**：已有研究（如Azaria & Mitchell, 2023；Burns et al., 2022；Marks & Tegmark, 2023）表明LM的**内部隐藏状态**中蕴含着关于输出事实性的有效信号，甚至事实性与非事实性陈述的隐藏状态在几何上呈线性可分。但这些研究大多聚焦于“事后”检测，缺乏对“解码前预测幻觉”的探索。
- **本文研究问题（RQ）**：**能否在模型开始解码之前，仅利用模型在输入（问题）上产生的内部隐藏状态，预先预测该模型是否即将产生幻觉，并通过干预隐藏状态来缓解幻觉？**
- **整体回答**：论文以积极的实验结果回答了这一研究问题，提出 **FACT CHECKMATE** 框架，证明隐藏状态中存在早期预警信号——模型在处理输入时就已经“知道自己可能出错”，这为幻觉的预防性干预提供了全新思路。

### 2. 提出的方法论

**总体框架**：FACT CHECKMATE 包含两个核心组件：①预检测分类器 fθ；②干预模型 gϕ。推理时先在输入上收集隐藏状态，用 fθ 判断是否可能产生幻觉；若判定风险高（置信度 α ≤ 0.3），则用 gϕ 调整输入最后 token 的隐藏状态，再进行解码。

**（1）预检测分类器 fθ（Preemptive Detection）**

- 输入：LM 在输入问题（仅输入部分，不含输出）上产生的隐藏状态序列 {h_i^(l)}，其中 h_i^(l) 为第 l 个 Transformer 层的 FFN 输出在第 i 个 token 的 d 维向量。
- 网络结构：两层 ReLU-MLP + sigmoid 函数，输出 [0,1] 标量，表示“模型将产生幻觉”的概率。
- 公式：`fθ({h_i^(l)}) = σ(ReLU-MLP(A({h_i^(l)})))`，其中 A 为池化函数（mean / max / 取最后 token），实证表明**均值池化**效果最佳。
- 输出层选择：l 通过验证集经验确定，通常在模型的中后层效果最好。
- 训练数据：用少量示例（few-shot）提示 LM 回答问题，对模型输出与标准答案做**精确匹配（EM）**，错误回答关联的隐藏状态标记为非事实，正确回答标记为事实；正负样本平衡后训练。
- 设置变体：仅用输入（I，预检测）、用输入去掉最后 n 个 token（I−n，更强的预检测）、用输入+输出（I+O，反应式/作为性能上限参照）。

**（2）干预模型 gϕ（Preemptive Mitigation）**

- 当 fθ 检测到高幻觉风险时，gϕ 生成一个 d 维向量并加到输入最后 token 的隐藏状态 h_I^(l) 上，得到调整后状态：
  π h̃_I^(l) = h_I^(l) + gϕ(h_I^(l))
- 该调整后的状态替代原状态继续参与后续解码，以把模型的生成方向“拉向”更可能导向事实输出的目标隐藏状态。
- **确定性版本**：三层 ReLU-MLP，训练目标为最小化调整后隐藏状态与目标隐藏状态之间的 MSE。
- **随机版本（stochastic）**：将调整向量视为多元高斯随机变量，用重参数化技巧 gϕ(h) = μ(h) + ε ⊙ σ(h) 进行训练，推理时可多次采样（1/10/20/30 次），用 fθ 选出使“事实概率”最高的干预向量。
- 训练数据：当模型回答正确时，目标隐藏状态就是它自己的最终隐藏状态；当回答错误时，目标隐藏状态设为“输入+金标准答案”对应的最终隐藏状态。
- 干预只在**第一个解码步骤**执行一次，且仅在 fθ 置信度 α ≤ 0.3 时触发。

### 3. 实验设计

- **数据集**：
  - **NQ-open**（Wikipedia 开放域问答）
  - **MMLU**（STEM 多选考试题，转换为问答形式）
  - **MedMCQA**（医疗入学考试，转换为问答形式）
  - **GSM8K**（小学数学应用题，取最终答案）
  - 数据划分为 Train 70% / Val 15% / Test 15%。
- **模型**：覆盖多种规模与家族——Llama2（7B/13B，含 base 和 chat）、Llama3（8B/70B，含 base 与 Instruct）、Llama3.1（8B/70B）、Mistral-7B（含 Instruct）、Gemma-7B（含 it）、Qwen2.5（7B/32B，含 Instruct）。
- **检测评估设置**：主要报告分类准确率。对比“仅输入（I）”“输入去掉最后 1/2/3 个 token（I−1/2/3）”与“输入+输出（I+O，反应式，作为天花板参照）”。
- **跨模型泛化**：在 Llama-2-7B、Llama-3.1-8B、Mistral-7B 的隐藏状态上联合训练，测试在其他模型上的迁移能力。
- **跨数据集泛化**：在多数据集上联合训练后测试各数据集表现，包括对域外数据的泛化（附录 G）。
- **缓解评估**：由于 EM 无法捕捉部分修正，改用 **GPT-4o 作为评判者**评估两个回答的事实性（比较“干预后”与“基线”输出的胜负与平局比例）；作者人工评估与 GPT-4o 判断的 Cohen's Kappa = 0.6（高度一致），支持该评估方式的可靠性。
- **推理开销评估**：在 Llama-2-7B / Llama-3-8B / Llama-3.1-8B 上各运行 3 次、每次处理 400 条 few-shot 提示，比较有无 FACT CHECKMATE 的推理时间。
- **额外实验/消融**：
  - 使用词嵌入层（非上下文化）训练分类器，排除“题目难度驱动分类”的解释（准确率约 50%，接近随机）。
  - 对比三种池化方式（mean / max / last token）。
  - 对非幻觉类问题的影响分析（假阳性分析，使用混淆矩阵）。
  - 比较仅用分类器做采样（不干预）与基线采样，证明干预的必要性。

### 4. 资源与算力

- 论文**未明确说明**训练分类器/干预模型所用的 GPU 型号、数量及具体训练时长。
- 致谢部分提到使用了 **Delta 先进计算与数据资源**（由美国国家科学基金会 OAC 2005572 资助）以及 **Illinois Computes** 项目；并感谢 SambaNova 提供对 Llama 系列模型的访问。因此可以推断实验在 HPC 集群上完成，但缺少精确的算力明细。

### 5. 实验数量与充分性

- **量级较大且覆盖面广**：主表（Table 1）涵盖 4 个数据集 × 16 个模型变体，每个都报告 I+O 与 I/I−1/I−2/I−3 共 5 组准确率，数量可观；另有跨模型（Table 2）、跨数据集（Table 3）、附加大模型（Table 8/9）、词嵌入层分析（Table 5）、推理开销（Table 4）、多种干预设置比较（Figure 4）、MedMCQA 干预结果（Figure 6）、定性示例（Table 11）、混淆矩阵与假阳性分析（Table 10）、采样消融（Figure 7）、池化方式消融（Table 14）等。
- **充分性评估**：实验基本充分，尤其在“检测”环节验证扎实；但“缓解”环节主要依赖 GPT-4o 主观评判，EM 不再作为指标；跨模型迁移在未见过的模型上表现接近随机（Table 13），暴露了泛化局限。总体而言实验设计较系统、评估较客观，但**缓解实验的对比基线**多为“无干预”自身对照，缺少与主流解码/编辑类方法的直接基准对比（论文承认如 DoLa、TruthX 等方法因设定不同难以直接比较）。

### 6. 主要结论与发现

- **预检测可行且有效**：仅基于输入问题的隐藏状态，FACT CHECKMATE 即可达到 70% 以上的幻觉预测准确率，显著超过 50% 随机基线；在部分设置下与使用输入+输出的反应式检测准确率差距极小（如仅差 1%）。
- **跨数据集/跨模型训练具有实用性**：在多模型/多数据集上联合训练的分类器在相关模型和域内数据上表现良好，是一种实用的泛化路径；但对完全未见过的模型迁移表现不佳。
- **干预显著提升事实性**：所有被干预模型的输出胜率均高于基线，平均比无干预模型高出 **34.4%**；随机干预模型可通过多次采样 + fθ 选择进一步提升效果。
- **非幻觉答案几乎不受影响**：假阳性分析表明，在 1,362 条回答中只有 9 个假阳性，其中仅 2 个导致输出退化，干预对正确回答影响极小。
- **推理开销可忽略**：平均仅增加约 **1.2%** 的解码时间。
- **隐藏状态而非题目本身驱动分类**：词嵌入层分类准确率≈50%，排除了“题目难度”作为混淆变量的解释；真正起到判别作用的是经过上下文编码后的深层隐藏状态。

### 7. 优点

- **视角新颖**：首次系统性地提出并验证“解码前预测幻觉”的可行性，将幻觉检测的时机从事后提前到生成之前。
- **轻量高效**：检测与干预模块均为小型 MLP，推理开销极低（~1.2%），适合集成到现有 LM 推理管线。
- **覆盖广**：实验跨度大——模型规模从 7B 到 70B、多个模型家族、四种不同领域 QA 数据集，结论更具普适性。
- **方法透明度高**：利用模型内部结构（FFN 输出）而非把模型当黑盒，为理解 LM 内部工作机制和幻觉成因提供了新证据。
- **严谨的控制实验**：通过输入前缀截断（I−n）、词嵌入层对照、假阳性分析、池化消融、采样消融等实验设计，排除了多种混淆解释，增强结论可信度。
- **自动化评估的可靠性验证**：报告了 GPT-4o 与人工判断的较高一致性（Cohen's Kappa = 0.6），为大规模自动评估提供依据。

### 8. 不足与局限

- **任务范围有限**：实验仅覆盖短答案 QA，无法直接推广到长文本生成（摘要、对话、开放生成等），因为长文本中“幻觉从哪里开始”难以精确定位，且 EM 不再适用。
- **黑盒模型不可用**：方法需要访问模型内部隐藏状态，不适用于仅暴露 API 的黑盒 LM。
- **跨模型迁移性弱**：在未见过的模型上分类准确率接近随机（约 50%），说明分类器对具体模型架构和表征空间的依赖较强。
- **评估指标两难**：EM 过于严格（无法反映部分修正），而 GPT-4o 主观评估存在评估偏差风险，虽有人工验证但范围有限。
- **训练标签的噪音问题**：以 EM 作为“是否幻觉”的黄金标签不够精细（例如“部分正确”被归为错误），可能给分类器训练带来噪音。
- **干预触发阈值固定**：α ≤ 0.3 的阈值经验设定，未充分讨论不同阈值对缓解效果和误报率的影响。
- **缓解效果评估缺乏与其他方法的直接对比**：论文明确承认与 DoLa、TruthX 等现有方法不可直接比较，因此读者难以判断其相对优势有多显著。
- **算力细节缺失**：未报告精确的 GPU 使用情况，不利于可复现性和资源评估。

（完）
