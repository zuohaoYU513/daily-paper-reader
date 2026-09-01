---
title: Detecting Hallucinations in Retrieval-Augmented Generation via Semantic-level Internal Reasoning Graph
title_zh: 基于语义级内部推理图检测检索增强生成中的幻觉
authors: "Jianpeng Hu, Yanzeng Li, Jialun Zhong, Lei Zou, Wenfa Qi"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1385.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 基于语义级内部推理图检测RAG中的忠实性幻觉
tldr: 检索增强生成虽能减少事实性幻觉，但忠实性幻觉仍然存在，现有检测方法未能捕捉模型内部推理过程。该工作将层间相关性传播从token级扩展到语义级，构建基于归因向量的内部推理图。基于该图的判别器能更好学习幻觉特征，显著提升忠实性幻觉检测效果，并增强RAG系统的可信度。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 836, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1635, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1385/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 473, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 1035, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 847, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1385/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 157, \"label\": \"Table\"}]"
motivation: RAG中忠实性幻觉仍待解决，已有检测方法未充分利用内部推理过程。
method: 将层间相关性传播扩展至语义级，构造内部推理图供判别器学习。
result: 实验表明该方法在检测忠实性幻觉上优于此前方法。
conclusion: 语义级推理图为RAG幻觉检测提供了新的有效方案。
---

## Abstract
The Retrieval-augmented generation (RAG) system based on Large language model (LLM) has made significant progress. It can effectively reduce factuality hallucinations, but faithfulness hallucinations still exist. Previous methods for detecting faithfulness hallucinations either neglect to capture the models’ internal reasoning processes or handle those features coarsely, making it difficult for discriminators to learn. This paper proposes a semantic-level internal reasoning graph-based method for detecting faithfulness hallucination. Specifically, we first extend the layer-wise relevance propagation algorithm from the token level to the semantic level, constructing an internal reasoning graph based on attribution vectors. This provides a more faithful semantic-level representation of dependency. Furthermore, we design a general framework based on a small pre-trained language model to utilize the dependencies in LLM’s reasoning for training and hallucination detection, which can dynamically adjust the pass rate of correct samples through a threshold. Experimental results demonstrate that our method achieves better overall performance compared to state-of-the-art baselines on RAGTruth and Dolly-15k. Implementation available here: https://anonymous.4open.science/r/SIRG-1022.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：检索增强生成（RAG）虽能有效缓解大语言模型（LLM）的**事实性幻觉**（输出与真实世界事实不一致），但**忠实性幻觉**（生成内容与用户提供的上下文不一致）仍然普遍存在。
- **问题根源**：忠实性幻觉主要源于LLM在推理时仅利用表面知识（如实体流行度），将**实质性词元**错误地当作**连接性词元**处理，导致生成内容未真正依赖用户提供的上下文。
- **现有方法的不足**：
  - 基于LLM后验证的方法（如SelfCheckGPT）需要多次调用LLM，资源消耗大且会放大模型偏差；
  - 基于内部嵌入的方法缺乏可解释性，判别器难以学习抽象特征；
  - 基于输出归因的方法（如LRP4RAG）直接累加token级归因向量，引入了大量噪声，处理粒度较粗。

## 2. 方法论：SIRG（Semantic-level Internal Reasoning Graph）

### 核心思想

通过对LLM自回归推理过程的语义级归因分析，构建一个**语义级内部推理图**，忠实反映模型生成每个语义片段时对上下文及其他响应片段的依赖关系。利用该图训练轻量级判别器实现幻觉检测。

### 关键技术细节

1. **贡献分数计算（LRP扩展）**：
   - 利用Attention-aware Layer-wise Relevance Propagation（AttenLRP）计算每个生成token对上下文中各token的相关性向量；
   - 按层自定义传播规则（MLP、Softmax、矩阵乘法、LayerNorm），保证守恒性质，忠实反映模型真实计算过程。

2. **语义片段划分与实体提取**：
   - 使用换行符和Spacy句切分将上下文与响应划分为语义片段集合 `S_c` 与 `S_a`；
   - 使用Spacy和Stanza提取名词、动词、名词短语、否定词和命名实体作为"实质性内容"集合 `E`，过滤连接性噪声。

3. **语义级相关性矩阵构建（公式4）**：
   - 对目标语义片段 `s_{a,i}`，选取其包含实体对应的归因向量，对实体取平均、对源片段内token取最大，得到语义级相关性矩阵 `W ∈ R^{n_a × (n_a + n_c)}`；
   - 该矩阵为下三角结构，反映"先前的片段可以归因于之后的片段"的因果时序。

4. **内部推理图构建**：
   - **Top-k方法**：按归因分数降序选取前k个源片段作为入边；
   - **自适应方法**：对归因分数序列计算离散梯度，以最大梯度点区分重要/非重要源片段，自适应确定入边数量。

5. **幻觉判别**：
   - 将每个响应片段及其入边源片段线性化为prompt，输入小型预训练语言模型（ALIGNSCORE / RoBERTa架构）进行二分类微调；
   - 通过阈值α控制整体响应判断的宽松程度：若幻觉片段占比超过α，则判定整个响应存在幻觉。

## 3. 实验设计

### 数据集

| 数据集 | 模型 | 幻觉样本 | 正常样本 |
|---|---|---|---|
| RAGTruth (Llama-7B) | Llama-7B | 510 | 479 |
| RAGTruth (Llama-13B) | Llama-13B | 399 | 590 |
| Dolly-15k | Qwen2.5-3B/7B | 使用GPT-4与标准答案对比自动标注 | — |

### 对比方法（Baselines）

- **Prompt**（Niu et al., 2024）：人工设计prompt让LLM识别幻觉；
- **SelfCheckGPT**（Manakul et al., 2023）：多轮采样一致性检验；
- **Fine-tune**（Niu et al., 2024）：微调Llama-7b和Qwen-7b检测幻觉；
- **EigenScore**（Chen et al., 2024）：基于响应协方差矩阵特征值的语义一致性度量；
- **SEP**（Kossen et al., 2024）：在LLM隐状态上训练的线性探针；
- **LRP4RAG**（Hu et al., 2024）：直接使用LRP贡献分数+分类器/LLM。

### 评估指标

精确率（Precision）、召回率（Recall）、F1分数。

## 4. 资源与算力

- 文中未明确说明训练所使用的GPU型号、数量及训练时长；
- 在**计算延迟**实验中，作者提到使用**A100显卡**测试平均推理时间（100个样本）：
  - SIRG整体平均处理时间为 **39.76秒/样本**；
  - 其中LRP计算占比最高（**25.49秒**），生成阶段12.12秒，实体提取0.59秒，图构建0.05秒，判别阶段1.51秒；
  - 相比SelfCheckGPT（71.19秒）和LRP4RAG（56.40秒），SIRG具有显著耗时优势，但高于Prompt（13.89秒）。
- 使用VLLM加速框架时，Prompt和SelfCheckGPT可分别降至5.73秒和31.93秒，而LRP-based方法的GPU显存占用较高（文中用"−−"表示无法在VLLM上直接运行）。

## 5. 实验数量与充分性

### 实验组数概览

| 实验类型 | 具体内容 | 数量 |
|---|---|---|
| 主实验（主表对比） | RAGTruth Llama-7B/13B + Dolly Qwen2.5-3B/7B 共4个场景 | 4组 |
| 无偏性/忠实性验证 | 基于扰动的生成与剪枝测试（100个样本） | 2类扰动 |
| 超参数分析 | α阈值扫描（0~0.4）+ Top-k取值（5/10/15/20/自适应） | 2组 |
| 计算延迟对比 | 4种框架（无不使用VLLM）、2种模式（有/无VLLM） | 多组 |
| 消融实验（实体提取） | 7种配置（Only noun/Only verb/Only adj-adv/All text/0.33/0.66/Original） | 7组 |
| 消融实验（切分策略） | 4种策略（平均切分/固定切分/Qwen切分/原始方法） | 4组 |

### 充分性评估

- **优点**：实验覆盖两个主流数据集、多种LLM类型（Llama/Qwen）、多种baselines（LLM-based、表示-based、归因-based），并包含消融分析、扰动测试和延迟分析，整体设计较为全面、客观；
- **不足**：
  - Dolly-15k的标注依赖GPT-4自动评估，可能存在标注噪声；
  - 未覆盖更多样化的LLM（如GPT系列或更大规模模型），泛化性有待验证；
  - 对α和Top-k的敏感性分析仅在一个数据集上进行，缺乏跨数据集验证；
  - 延迟测试中的样本量为100，规模偏小。

## 6. 主要结论与发现

1. **SIRG在所有对比方法中取得最优F1**：
   - RAGTruth Llama-7B：F1 **76.61%**，较最优基线LRP4RAG（73.54%）提升 **3.07%**；
   - RAGTruth Llama-13B：F1 **81.84%**，较LRP4RAG（75.86%）提升 **5.78%**；
   - Dolly Qwen2.5-3B：F1 **82.17%**，较LRP4RAG（81.71%）提升；
   - Dolly Qwen2.5-7B：F1 **89.71%**，较LRP4RAG（80.80%）大幅提升。
2. **忠实性幻觉的成因解释**：LLM在推理过程中将实质性语义片段错误地当作连接性片段处理，表现为归因分布上对先前生成内容的过度依赖和对上下文依赖不足；
3. **语义级推理图忠实有效**：扰动测试证明LRP构建的推理图能准确识别对目标片段影响最大的源片段；
4. **阈值α可动态调节**：通过调整α可灵活控制正确样本的通过率，适应不同可靠性需求的场景；
5. **轻量判别器即可达到LLM级性能**：使用仅1.24亿参数的ALIGNSCORE判别器，即可获得优于LLM-based检测框架的效果。

## 7. 优点

1. **方法创新性强**：首次将LRP从token级扩展至语义级，构建内部推理图，比直接累加token级归因更细腻、噪声更少；
2. **可解释性好**：内部推理图能直观展示语义片段间的依赖关系和归因权重，帮助人类理解LLM的推理决策过程；
3. **轻量高效**：判别器仅需一个小型PLM，不需要多次调用LLM，计算成本远低于SelfCheckGPT和LRP4RAG；
4. **动态阈值控制**：α参数允许用户根据具体场景灵活调节"通过率—精确率"的权衡；
5. **实验设计较完整**：包括多数据集验证、消融分析、扰动测试和延迟对比，验证了方法的有效性和可靠性。

## 8. 不足与局限

1. **计算开销仍偏高**：LRP需要为每个token计算内部梯度，单样本LRP计算耗时25.49秒，是整个框架的性能瓶颈；
2. **图拓扑利用不充分**：当前仅将入边线性化为prompt输入PLM，忽略了多跳依赖关系和错误传播信息，作者提到未来可探索基于图神经网络的自适应节点聚合；
3. **阈值依赖**：α的选取需要人工设定，不同场景需调参，未提供自适应确定α的方法；
4. **训练数据依赖**：判别器需要在特定LLM生成的数据上微调，对新模型可能需要重新训练，泛化性受限；
5. **消融实验中切分策略的对比**：Qwen3-14B切分策略的F1（78.08%）略高于原始方法的76.61%，在无标注成本敏感场景下，使用大模型切分可能更优，但会增加额外计算开销；
6. **多语言与多领域通用性不足**：实验中仅使用英文数据，未验证跨语言和跨领域（如医学、法律）场景下的有效性。

（完）
