---
title: "The Law of Knowledge Overshadowing: Towards Understanding, Predicting and Preventing LLM Hallucination"
title_zh: 知识遮蔽定律：理解、预测并预防大语言模型幻觉
authors: "Yuji Zhang, Sha Li, Cheng Qian, Jiateng Liu, Pengfei Yu, Chi Han, Yi R. Fung, Kathleen McKeown, ChengXiang Zhai, Manling Li, Heng Ji"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1199.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 用知识遮蔽机制解释、预测和预防LLM事实幻觉
tldr: 大模型即使使用高质量数据训练仍持续产生事实性幻觉，论文提出知识遮蔽概念解释这一悖论：主导知识会掩盖次要知识从而生成不准确细节。基于此建立量化框架，用对数线性定律刻画事实幻觉速率，并可用于预测和预防幻觉。该工作加深了对幻觉机制的理解，为从模型内在机制层面治理幻觉提供了理论基础。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1199/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 836, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1199/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1604, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1199/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1645, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1199/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 524, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1199/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 769, \"height\": 283, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1537, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 779, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1600, \"height\": 609, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 572, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1466, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1286, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1199/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 816, \"height\": 398, \"label\": \"Table\"}]"
motivation: 即便训练数据质量高，大模型仍会生成扭曲事实，缺乏对幻觉内在机制的深入理解。
method: 提出知识遮蔽概念与对数线性定律，建立量化框架对事实幻觉进行解释、预测和预防。
result: 证明了知识遮蔽与对数线性规律能有效刻画并预测大模型事实幻觉的发生率。
conclusion: 从知识遮蔽机制入手可理解并预防大模型幻觉，为幻觉治理奠定理论基础。
---

## Abstract
Hallucination is a persistent challenge in large language models (LLMs), where even with rigorous quality control, models often generate distorted facts. This paradox, in which error generation continues despite high-quality training data, calls for a deeper understanding of the underlying LLM mechanisms. To address it, we propose a novel concept: knowledge overshadowing, where model’s dominant knowledge can obscure less prominent knowledge during text generation, causing the model to fabricate inaccurate details. Building on this idea, we introduce a novel framework to quantify factual hallucinations by modeling knowledge overshadowing. Central to our approach is the log-linear law, which predicts that the rate of factual hallucination increases linearly with the logarithmic scale of (1) Knowledge Popularity, (2) Knowledge Length, and (3) Model Size. The law provides a means to preemptively quantify hallucinations, offering foresight into their occurrence even before model training or inference. Built on overshadowing effect, we propose a new decoding strategy CoDa, to mitigate hallucinations, which notably enhance model factuality on Overshadow (27.9%), MemoTrap (13.1%) and NQ-Swap (18.3%). Our findings not only deepen understandings of the underlying mechanisms behind hallucinations but also provide actionable insights for developing more predictable and controllable language models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **背景**：大语言模型即使使用经过严格质量控制的高质量训练数据，仍然会持续产生事实性幻觉（hallucination），即生成与事实不符的内容。这一悖论表明，幻觉并非仅仅源于低质量数据，而是与模型内部的机制密切相关。
- **核心问题**：为什么在高质量数据下模型仍会产生事实扭曲？能否提前预测幻觉的发生，并进而预防或消除幻觉？
- **核心含义**：论文提出“知识遮蔽”（Knowledge Overshadowing）概念来解释这一现象——在文本生成过程中，模型中的主导知识会抑制或掩盖较为次要的知识，导致模型忽略部分约束条件，从而编造出不准确的细节。该研究为理解、预测和预防LLM幻觉提供了新的理论视角和可操作的解码策略。

## 2. 方法论

### 2.1 知识遮蔽的建模

- **知识对定义**：将训练语料中的知识表示为成对的知识集合 \( K_A \)（主导知识，m 个样本）和 \( K_B \)（次要知识，n 个样本），二者共享部分 token 序列 \( X_{\text{share}} \)，但各有独特的 token 序列 \( x_a \) 和 \( x_b \) 以及对应的输出 \( Y_a \) 和 \( Y_b \)。
- **遮蔽发生**：当模型面对包含 \( x_b \) 的提示时，由于 \( K_A \) 更强势，模型错误地输出 \( Y_a \)，形成事实幻觉。
- **幻觉率度量**：定义相对幻觉率 \( R = HR / RR \)，其中 \( RR \) 是正确回忆主导知识的召回率，\( HR \) 是次要知识被遮蔽后产生幻觉的概率。

### 2.2 对数线性定律（Log-linear Law）

- 通过系统性实验，论文发现事实幻觉率与三个变量之间存在对数线性关系：
  - **相对知识流行度** \( P = m/n \)（全局视角：知识在训练语料中的频次比例）
  - **相对知识长度** \( L = (\text{len}(X_{\text{share}}) + \text{len}(x_b)) / \text{len}(x_b) \)（局部视角：上下文长度相对被约束 token 长度的比例）
  - **模型规模** \( S \)（参数量）
- 形式化表述：
  \[
  R(P) = \alpha \log(P/P_c),\quad R(L) = \beta \log(L/L_c),\quad R(S) = \gamma \log(S/S_c)
  \]
- 该定律使得在模型训练或推理之前即可量化预测幻觉率。

### 2.3 理论解释

- 论文将幻觉解释为“记忆-泛化-幻觉”过程的副产品：模型在记忆大量知识后，泛化过程中对主导知识的过度平滑和压缩会遮蔽次要知识。
- 推导了自回归语言模型的泛化误差上界，证明相对知识流行度 \( m \) 和长度 \( L \) 增大时，泛化误差界降低（泛化能力增强），与幻觉率上升的趋势一致，从而为对数线性定律提供理论支撑。

### 2.4 CoDA 解码策略

- **识别遮蔽知识**：通过逐 token 掩码构造变体提示 \( X' \)，比较原提示与掩码提示的输出概率分布，计算相对逐点互信息（R-PMI），并引入“逃逸 token”（\( V_{\text{esc}} \)）机制和逃逸奖励机制（ERM），得到遮蔽知识指示器。
- **放大遮蔽知识**：采用对比解码，从原提示的对数概率中减去掩码提示引入的偏差，从而降低主导知识的影响并放大被遮蔽知识的贡献。该方法无需额外训练。

## 3. 实验设计

### 3.1 训练数据与场景

- **合成数据集**：从零开始预训练LLM，严格控制变量（P、L、S），用于发现对数线性定律。
- **自然语言任务微调**：在时间、地点、性别、否定、数学、逻辑推理、知识冲突等任务上微调多种开源模型，验证定律在微调模型上的适用性。
- **SOTA 模型案例**：对 GPT-4o、DeepSeek-V3、Qwen 等闭源模型，通过控制输入长度进行定性案例研究。

### 3.2 Benchmark

- **MemoTrap**：测试模型是否过度依赖预训练知识而忽略上下文（如成语/谚语补全）。
- **NQ-Swap**：将自然问题中的实体替换为冲突实体，考察模型是否会输出替换后的答案。
- **Overshadow**：论文基于 COUNTERFACTUAL 数据构建的自有数据集，包含时间、地点、性别、否定、逻辑、数学、知识冲突等子任务。

### 3.3 对比方法

- Greedy decoding、Chain-of-Thought (CoT)、Self-Reflection (SR)、USC、DoLa 等。

## 4. 资源与算力

- **硬件**：A-100 GPU（80GB 显存）。
- **训练耗时**（论文附录 A.2 提及）：
  - 在四块并行 A-100 GPU 上，对 Phi-2.8B 在合成数据集上训练一个 epoch 约需 1 小时，总计约 40 小时。
  - 对 Llama-2-7B 在四块并行 GPU 上微调合成数据集超过 100 小时。
  - 推理阶段使用单块 GPU 即可运行 Pythia 至 Llama 系列模型。
- 总体而言，算力投入较大，但论文未对所有实验的总算力给出完整汇总。

## 5. 实验数量与充分性

- **实验数量丰富**：包括：
  - 从零预训练多个模型（Pythia 系列 160M–2.8B、Phi、GPT-J、Mistral、Llama 系列等）。
  - 微调任务涵盖 8 种以上自然语言推理类型，模型规模从 160M 到 13B。
  - 在三个 benchmark 上对比 5 种基线方法，每个实验重复 5 次取平均。
  - 消融分析涉及 P 和 L 不同取值（2:1 到 100:1）对 CoDA 性能的影响。
  - 额外对比了不同 token 掩码选择策略（Flair、NLTK、Spacy、StanfordNLP、Vanilla）。
- **充分性评估**：
  - 优点：控制变量法设计严谨，从合成数据到真实数据、从预训练到微调、从开源到闭源模型，覆盖面广。
  - 可能不足：由于闭源模型训练语料不可得，无法定量分析其 P 和 S 的影响；真实语言数据中的知识流行度和长度难以精确量化，预测误差为 8.0%，仍有波动。

## 6. 主要结论与发现

- **知识遮蔽是幻觉的重要成因**：即使训练数据完全真实，知识间的不平衡仍会导致事实性幻觉。
- **对数线性定律成立**：幻觉率随相对知识流行度、相对知识长度、模型规模的增大而对数线性上升。
- **模型规模的反直觉效应**：更大模型更容易遮蔽次要知识，与“更大的模型更可靠”的普遍假设相悖。
- **CoDA 有效提升事实性**：在 Overshadow、MemoTrap、NQ-Swap 上分别相对 greedy 提升 27.9%、13.1%、18.3%，优于现有解码方法。
- **预测幻觉成为可能**：利用预训练阶段拟合的定律，可在微调后模型上预测其幻觉率，平均相对预测误差为 8.0%。

## 7. 优点

- **提出新概念与理论框架**：首次系统性提出“知识遮蔽”概念，并用对数线性定律定量刻画幻觉，从现象走向可预测。
- **理论与实验结合**：不仅做了大规模实证，还推导了泛化误差界，为经验定律提供理论依据。
- **方法实用且高效**：CoDA 无需额外训练和数据，适用于现有模型，可即插即用。
- **研究范式创新**：将幻觉检测从“事后检测”转向“事前预测与预防”，具有前瞻性。
- **覆盖面广**：从合成数据到自然语言，从预训练到微调，从开源小模型到闭源 SOTA 模型，验证了现象和定律的普适性。

## 8. 不足与局限

- **闭源模型语料不可达**：无法精确分析 GPT-4o、DeepSeek 等模型的训练数据变量，只能进行定性实验。
- **真实数据量化困难**：语言本身的模糊性和噪声使得精确计算真实语料中的知识流行度和长度非常困难，影响预测精度。
- **微调数据仍受预训练知识干扰**：虽然使用反事实数据，但自然语言表达可能仍带有预训练知识痕迹，导致 P 和 L 的预测误差比 S 更高。
- **CoDA 的局限**：只聚焦解码阶段，未深入模型内部表征；对于复杂、复合的知识遮蔽场景（多个知识同时遮蔽）处理能力有限。
- **评估范围**：基准数据集规模有限（如 Overshadow 每个子任务约 1980 个样本），对于更广泛和多样化的幻觉场景覆盖不足。

（完）
