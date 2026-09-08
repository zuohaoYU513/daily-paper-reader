---
title: Enhancing Language Model Factuality via Activation-Based Confidence Calibration and Guided Decoding
title_zh: 通过基于激活的置信度校准与引导解码增强语言模型事实性
authors: "Xin Liu, Farima Fatahi Bayat, Lu Wang"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.583.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 提出基于激活的置信度校准方法，对齐语言模型置信度与真实答案正确性
tldr: 为应对语言模型置信度与实际正确性失配导致的幻觉问题，该文提出基于激活的置信度校准方法ActCab。它通过在模型内部表示上训练线性层获得更可靠的置信度信号，并将其引入解码过程以提升事实性。与传统logit和自一致性方法相比，该方法在保持有用性的同时减少低置信过滤的副作用，拓展了置信度信号用于幻觉缓解的路径。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main583/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main583/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 583, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 618, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1251, \"height\": 1098, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 817, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 817, \"height\": 159, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main583/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1230, \"height\": 705, \"label\": \"Table\"}]"
motivation: 现有置信度校准方法要么推理效率受限，要么信号信息量不足；简单过滤低置信度回答还会误伤正确输出。
method: 提出ActCab，在语言模型内部激活上训练一层线性校准器以估计回答正确性，并利用该置信度指导解码过程。
result: 该框架在提升生成事实性与校准质量方面优于以往方法，同时避免过度过滤带来的有用性损失。
conclusion: 激活层面的校准信号可以有效利用来增强LLM事实性，为后续置信度导向的解码提供了可行框架。
---

## Abstract
Calibrating language models (LMs) aligns their generation confidence with the actual likelihood of answer correctness, which can inform users about LMs’ reliability and mitigate hallucinated content. However, prior calibration methods, such as self-consistency-based and logit-based approaches, are either limited in inference-time efficiency or fall short of providing informative signals. Moreover, simply filtering out low-confidence responses reduces the LM’s helpfulness when the answers are correct. Therefore, effectively using calibration techniques to enhance an LM’s factuality remains an unsolved challenge. In this paper, we first propose an activation-based calibration method, ActCab, which trains a linear layer on top of the LM’s last-layer activations that can better capture the representations of knowledge. Built on top of ActCab, we further propose CoDec, a confidence-guided decoding strategy to elicit truthful answers with high confidence from LMs. By evaluating on five popular QA benchmarks, ActCab achieves superior calibration performance than all competitive baselines, e.g., by reducing the average expected calibration error (ECE) score by up to 39%. Further experiments on CoDec show consistent improvements in several LMs’ factuality on challenging QA datasets, such as TruthfulQA, highlighting the value of confidence signals in enhancing the factuality.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机与背景）
大语言模型（LMs）在开放域问答等任务中虽然表现出色，但其生成内容的真实性仍存在隐患：模型生成“幻觉”内容（hallucinated content），使得回答与其内部掌握的知识之间存在错位。为了提升对模型输出的信任度，一个重要的途径是对模型的响应进行**置信度校准（confidence calibration）**，使模型输出的置信度尽可能与实际正确率匹配。然而现存的方法各有不足：

- **训练无关方法**（如 verbalization、self-consistency）依赖模型的指令遵循能力或对多次采样做语义聚类，推理代价往往过大；
- **基于 logit 的方法**（如序列似然、温度缩放、LitCab）虽然高效，但只关注单个 token 的预测概率，难以捕捉整段回答的正确性；
- 简单地将低置信度答案过滤掉（selective generation），虽然提升了可信度，却牺牲了模型的有用性（helpfulness）和覆盖率，尤其是正确答案被过滤时更加得不偿失。

因此，论文的核心挑战在于：设计一种既高效、又能反映回答级真实置信度、并将置信度信号用于提升模型事实性而非简单过滤答案的完整方案。

### 2. 方法论：ActCab 与 CoDec
#### （1）ActCab：基于激活的置信度校准方法
- **核心思想**：借鉴了“模型内部激活中能够编码知识/真实性方向”的相关工作（如 ITI、RepE），认为**模型的最后一层隐藏层激活比 logits 包含更丰富的知识表示**，更适合用于回答级置信度估计。
- **模型结构**：在 LM 的最后一层（feed-forward 之后）得到每个输出 token 的激活 \( h_i \)，将其序列取平均后送入一个**单层线性分类器**：
\[
p_\theta(y|x) = \sigma\left(W \cdot \frac{1}{|y|}\sum_{i=1}^{|y|} h_i + B\right)
\]
其中 \( W, B \) 为可学习参数，\( \sigma \) 为 sigmoid 函数。该分类器参数规模小于原模型参数的 0.001%，极大地保留了推理效率。
- **软标签构造（K-fold Cross-validation + ECE Loss）**：直接使用“正确/不正确”的二元标签会导致过度自信或不够自信、校准不佳。论文提出一种基于 K 折交叉验证的软标签构造方法：将其划分为 K 折，训练 K 个分类器，对每个训练实例，取其所在验证折上该分类器给出的预测置信度。接着将所有样本按照预测置信度分为 10 个等间隔 bin（如 [0,0.1), [0.1,0.2), …），用所在 bin 中全部样本的实际准确率（accuracy）作为该样本的软标签：
\[
\text{acc}(B_{(x,y)}) = \frac{1}{|B_{(x,y)}|}\sum_{y \in B_{(x,y)}} \mathbb{1}(y\text{ is correct})
\]
最终训练的 ECE loss 是预测置信度与软标签的 MSE：
\[
\mathcal{L}_{\text{ECE}} = \frac{1}{|D|}\sum_{(x,y) \in D} \left(\text{acc}(B_{(x,y)}) - p_\theta(y|x)\right)^2
\]
该方法直接优化“估计置信度”和“真实正确率”之间的差距，从而提升整体校准性能。

#### （2）CoDec：置信度引导的解码策略
- 将 ActCab 的置信度分数引入生成过程：
  - 每一步贪心解码时，取 LM 预测概率最高的 top 7 个 token 作为候选；
  - 将每个候选 token 送入模型并提取其激活，通过 ActCab 分类器计算该 token 的置信度；
  - 最终 token 得分是 LM token 概率和 ActCab 置信度的加权和：
\[
s(y_t^*) = \lambda \cdot \log P_{\text{LM}}(y_t^*) + (1 - \lambda)\cdot \sigma(W \cdot h_t^* + B)
\]
其中 \( \lambda \) 为平衡超参数（设置为 0.3）。
- **回答级过滤与保留**：整个回答生成完成后，再次用 ActCab 计算整句回答的置信度，如果该置信度高于标准贪心解码所生成回答的置信度，则保留；否则回退使用贪心解码结果。这样保证了模型的生成可靠、不损失覆盖率。
- 与干预型方法（ITI、RepE）不同，CoDec 不改变模型内部激活，仅调整输出分布，因此不影响模型原有的推理过程，性能更稳定。

### 3. 实验设计
论文的实验主要围绕两个任务：**校准效果评估**与**事实性（factuality）提升评估**。

- **数据集**：使用 CaT（Calibration Training/Test benchmark）数据集中的五个开放式问答 benchmark，包括：
  - TruthfulQA
  - TriviaQA
  - SciQ
  - Natural Questions（NQ）
  - WikiQA
  各数据集的规模约为训练集 2K（TruthfulQA 397、WikiQA 1040），测试集约 293–1K。
- **测试设置**：校准实验在 Llama2-7b 上进行；事实性实验在 Llama2-7b、Llama2-13b、Llama3-8b 三个模型上评估；均采用 in-context learning（少样本）设置。
- **回答正确性标注**：短回答任务使用 ROUGE 分数（阈值 0.3）；句子级回答任务（TruthfulQA、WikiQA）邀请 GPT-4 做语义等价判断。
- **校准基线**：
  - Verbalization（提示模型自我表达置信度）
  - Self-consistency（多次采样语义一致性）
  - Sequence Likelihood（响应 token 几何平均概率）
  - Temperature Scaling
  - LitCab（logit 校准）
- **事实性基线**：
  - Greedy Decoding
  - Selective Generation（多次采样并选最高置信度输出）
  - ITI（Inference-Time Intervention）
  - RepE（Representation Engineering）
- **评估指标**：ECE、Brier Score（校准）；Accuracy、Truthfulness、Informativeness、True.*Info.（事实性）。

### 4. 资源与算力
论文明确提到以下资源信息：
- ActCab 仅训练了一个线性层，总训练时间（每个任务）在单张 A6000 GPU 上不到 1 小时；
- Llama2-7b 与 Llama3-8b 使用 FP32，Llama2-13b 使用 FP16 以节省显存；
- 解码速度实验在单张 A100 GPU 上对比 CoDec 与 Greedy、ITI 的吞吐率。

论文并未提及其他任务或模型在整个实验过程中的总体 GPU 算力需求（如总 GPU hours 或集群规模等），仅给出了主要方法本身的训练开销。

### 5. 实验数量与充分性
论文实验数量较为充足：
- 校准实验涵盖 5 个数据集 × 多种基线（verbalization、self-consistency、logit 类以及温度缩放等）；
- 事实性实验覆盖 3 个 LM（Llama2-7b、Llama2-13b、Llama3-8b）× 5 个数据集 × 4-5 种对比方法；
- 包含消融实验：ActCab w/o ECE loss（验证软标签是否起作用）；
- 额外进行了基于“人类编写正确/错误答案”的 TruthfulQA 实验（表 5），弥补了初版实验中使用模型采样答案可能引入噪声的不足；
- 另外评估了解码速度（throughput），验证了方法效率。

**充分性与公平性评估**：整体实验设计比较全面，包括了主要 SOTA 方法、消融、跨模型跨数据集泛化与效率对比。不过部分对比（如 ITI、RepE）存在训练数据来源不同的情况，文中也专门补充了基于人类标注成对答案的实验。整体而言实验控制相对严谨客观；但对 SciQ 上较差的性能，论文主要归因于模型知识不足，解释较为定性，缺乏进一步深入分析。

### 6. 主要结论与发现
1. ActCab 在所有 5 个 QA 数据集上均取得最好的校准效果，**平均 ECE 较 logit 类最具竞争力的 LitCab 进一步下降约 39%**；
2. ECE loss（基于 K-fold 的软标签）显著优于普通 MSE/binary label 训练，平均 ECE 从 0.080 降至 0.054（降幅 48%）；
3. 将 ActCab 的置信度嵌入解码过程（CoDec）有效提升了模型的事实性，特别是在 TruthfulQA 上提升显著（True.*Info. 在 Llama2-7b 上提升约 50%）；
4. 与 ITI、RepE 这类直接干预激活的方法相比，CoDec 不改变模型内部推理，在不同模型与不同训练数据来源下性能都更稳定；
5. CoDec 弥补了 selective generation 的不足——不放弃对问题的回答，在保持有帮助性的同时提升事实性。

### 7. 优点
- **方法创新**：将内部激活用于回答级置信度校准，并提供了一种基于 ECE 思想构造软标签的方法，在设计上有新意；
- **推理高效**：ActCab 仅增加一个线性层，比 self-consistency 等方法大幅减少推理开销；
- **实用价值**：CoDec 区别于简单的选择式过滤，能让模型继续作答，同时引导高置信度生成，真正实现了"利用置信度提升事实性"的目标；
- **研究严谨性**：在多模型、多数据集、人类标准答案/模型生成答案两种来源下均做了验证，比较公平；同时对解码速度进行了分析，可复现性和工程实践友好性较高；
- 论文提供了代码 URL，便于二次开发。

### 8. 不足与局限
- **可迁移性受限**：ActCab 与 CoDec 均需访问模型内部激活，因此无法适用黑盒大模型（如 GPT-4 API 等仅提供文本输出的场景）；
- **未探索长文本任务**：论文仅对 phrase 级与 sentence 级 QA 做了验证，尚未评估多句/段落级生成任务中存在多 claim 的情况，而长文本的事实性风险通常更大；
- **性能依赖模型知识**：当模型本身不具备相关知识（如 SciQ）时，仅靠单层线性分类器的置信度引导无法补足知识缺口，甚至可能降低准确率；
- **可解释性不足**：论文提出的方法虽然能够提升置信度与事实性，但并未解答“模型评估高置信度的依据是什么”以及“某一条回答为什么被判定为更可信”等可解释性问题；
- **训练标签获取依赖外部模型**：在句级答案上使用 GPT-4 人工判断语义等价，存在一定标注偏差或噪声；
- **超参数与阈值设定**：λ（权重系数）与 top-k 候选 token 数需要人为在验证集上调节，对不同任务可能存在最优值漂移。

（完）
