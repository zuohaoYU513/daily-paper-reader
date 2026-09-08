---
title: "Factual Confidence of LLMs: on Reliability and Robustness of Current Estimators"
title_zh: 大语言模型的事实置信度：当前估计器的可靠性与鲁棒性研究
authors: "Matéo Mahaut, Laura Aina, Paula Czarnowska, Momchil Hardalov, Thomas Mueller, Lluís Màrquez"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.250.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 系统比较事实置信度估计器并特别考察隐藏状态探针，关乎置信度与实际正确性的校准可靠性
tldr: 针对LLM事实性置信度估计方法缺乏系统比较的问题，该研究建立了统一实验框架，在事实核验与问答任务上评估多类估计器。结果显示，经过训练的隐藏状态探针给出的置信度最可靠，但需要访问模型权重与监督数据。还分析了现有估计器在不同条件下的鲁棒性，为如何选择和使用LLM事实置信度信号提供了实证指导。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 763, \"height\": 876, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 824, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 762, \"height\": 762, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1467, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1468, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long250/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1466, \"height\": 737, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1506, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 789, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 679, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 692, \"height\": 463, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1584, \"height\": 558, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1663, \"height\": 1393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long250/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1595, \"height\": 557, \"label\": \"Table\"}]"
motivation: 事实性回答不可靠且现有置信度估计器缺少系统比较，使用者难以确定哪种估计更可信。
method: 设计公平实验框架，统一比较logit、自一致性与隐藏状态探针等多类事实置信度估计器，并检验可靠性与鲁棒性。
result: 实验表明隐藏状态探针的置信度估计最可靠，但受限于权重与监督数据需求，其他估计器性能与鲁棒性各有差异。
conclusion: 建议在可获得权重的场景优先使用隐藏状态探针，为LLM事实置信度选择提供实证依据。
---

## Abstract
Large Language Models (LLMs) tend to be unreliable on fact-based answers.To address this problem, NLP researchers have proposed a range of techniques to estimate LLM’s confidence over facts. However, due to the lack of a systematic comparison, it is not clear how the different methods compare to one other.To fill this gap, we present a rigorous survey and empirical comparison of estimators of factual confidence.We define an experimental framework allowing for fair comparison, covering both fact-verification and QA. Our experiments across a series of LLMs indicate that trained hidden-state probes provide the most reliable confidence estimates; albeit at the expense of requiring access to weights and supervision data. We also conduct a deeper assessment of the methods, in which we measure the consistency of model behavior under meaning-preserving variations in the input. We find that the factual confidence of LLMs is often unstable across semantically equivalent inputs, suggesting there is much room for improvement for the stability of models’ parametric knowledge.

---

## 论文详细总结（自动生成）

# 《Factual Confidence of LLMs: on Reliability and Robustness of Current Estimators》详细总结

## 1. 核心问题与研究动机

- **背景问题**：大语言模型（LLMs）在生成事实性内容时不可靠，容易产生"幻觉"（hallucination），即自信地输出虚假或不确定的信息。这在信息传播和用户信任方面存在严重风险。
- **研究缺口**：学界已提出多种估计LLM"事实置信度"（factual confidence）的方法，但由于缺乏**统一的实验框架**和**系统性比较**，无法确知：
  - 不同方法之间相对表现如何？
  - 哪种方法在不同模型上最为可靠？
  - 各方法的估计在不同输入表述下是否稳健？
- **核心研究问题**：
  1. 当前哪些方法能最可靠地估计LLM对事实的置信度？
  2. 在不同模型、不同任务设定下，何种方法泛化性最好？
  3. LLM对同一事实的不同语言表述（释义/翻译）是否表现出**一致的置信度**？

## 2. 方法论：核心思想与关键技术

### 2.1 概念框架：两种置信度度量

论文定义了两种相互补充的置信度度量形式：

- **P(True)——P(T)**：模型认为输入**陈述句为真**的概率。用于**事实验证**（fact-verification）场景。通过向模型输入完整陈述句（如"巴黎是法国的首都"）来判断其真假。
- **P(I Know)——P(IK)**：模型认为自己能**正确回答一个查询**的概率。用于**问答**（QA）场景。仅输入问题，判断模型是否有把握产出正确答案。

作者指出，此前每种方法通常只处理其中一种度量，但**大多数方法可以同时适配两种设定**，只是可靠性可能存在差异。

### 2.2 五类置信度估计方法

论文通过综述将现有方法划分为五大类：

#### (1) 训练型探针（Trained Probes）
- **核心思想**：从模型内部隐藏状态（hidden states）中提取置信度信号，认为内部表征比表面输出更能反映真实的事实置信度。
- **技术实现**：采用**3层全连接前馈网络**，输入第24层Transformer（倒数第二层附近）的隐藏状态，训练10个epoch，输出二分类判断（陈述为真/假）。在QA场景中，训练目标改为预测模型"贪心解码"答案是否正确。
- **前置要求**：需要访问**模型权重** + 需要**监督训练数据**。

#### (2) 序列概率（Sequence Probability）
- **核心思想**：将输出token的平均对数概率作为置信度。
- **局限**：反映的是"表述方式的概率"而非"事实本身的置信度"；不同表述方式可能带来不同的概率，容易过度自信。

#### (3) 语言化置信度（Verbalization）
- **核心思想**：直接让模型用文字输出置信水平。
- **技术实现**：采用Tian et al. (2023)的prompt模板，让模型在1.0~10.0的尺度上输出置信度分数，过滤非数值输出并归一化。
- **适用性**：对指令微调后的模型效果较好。

#### (4) 替代令牌概率（Surrogate Token Probability）
- **核心思想**：向模型提问（如"Is the statement true?"），以"Yes"令牌的对数概率作为置信度。
- **本质**：介于序列概率与语言化方法之间的**混合方法**。

#### (5) 输出一致性（Consistency / Self-Consistency）
- **核心思想**：对同一问题多次采样输出，认为一致输出对应高置信度。
- **技术实现**：10次采样（τ=1，最多25个token），用NLI模型计算两两语义蕴含分数，取均值。
- **关键限制**：只能用于P(IK)，无法评估P(T)，因为该方法依赖生成过程。

## 3. 实验设计

### 3.1 使用的数据集与场景

| 任务 | 数据集 | 说明 |
|------|--------|------|
| P(T) 事实验证 | **Lama T-REx** | 基于Wikipedia三元组<subject, relation, object>构建陈述句；为每个真实陈述构造一个同关系随机替换实体的假陈述，形成50/50平衡数据集；34K三元组，80%训练 / 20%测试（6.8K真 + 6.8K假） |
| P(IK) 问答 | **PopQA** | 短问答数据集，答案含同义短语变体信息，覆盖不同流行度的实体；14K问题，80%训练 / 20%测试（2.8K）；标签由模型贪心解码是否正确决定（正例比例约11%~27%，因模型而异） |

### 3.2 测试的模型组合

共测试**8个公开可访问权重的LLM**：

| 模型 | 参数量 | 架构 | 是否指令微调 |
|------|--------|------|-------------|
| Falcon 40B | 40B | Dense | 否 |
| Falcon Instruct 40B | 40B | Dense | 是 |
| Falcon 7B | 7B | Dense | 否 |
| Falcon Instruct 7B | 7B | Dense | 是 |
| Mixtral 8x7B | 46.7B | SMoE | 否 |
| Mixtral Instruct 8x7B | 46.7B | SMoE | 是 |
| Mistral 7B | 7B | Dense | 否 |
| Mistral Instruct 7B | 7B | Dense | 是 |

模型覆盖不同规模（7B-46.7B）、不同架构（Dense/SMoE）和不同训练范式（原始版/指令微调版）。

### 3.3 评估方法

- 使用 **AUPRC**（Precision-Recall曲线下面积）作为主要性能指标，反映方法在区分真/假陈述或正确/错误答案方面的排序能力，同时不受数据不平衡影响。
- 报告P@90、P@70、P@50等具体精度和召回率辅助分析。
- **评估目标**对P(IK)而言即"预测未来正确性"的能力——直接检验方法在幻觉缓解场景中的有效性。

### 3.4 跨域与跨语言的额外实验

1. **探针跨域泛化**：将T-REx训练的P(T)探针直接应用于将PopQA改写为真/假陈述的测试集上。
2. **释义（Paraphrasing）鲁棒性**：用Mixtral-8x7B-Instruct为每个输入生成10个释义（经NLI双向蕴含验证后平均保留约8个），组成10个释义集测试方法稳定性。
3. **翻译（Translation）鲁棒性**：将Lama T-REx数据翻译为法语（高资源语言）和波兰语（低资源语言），测试跨语言泛化。

## 4. 资源与算力

- 论文**未明确报告具体的GPU类型、数量、训练时长与总体算力消耗**。
- 仅可推断：评测了8个参数从7B到46.7B的开源LLM，涉及推理和探针训练、释义生成（共约14K问题 × 10个释义）以及翻译评估；Mixtral-46.7B这类大模型的推理成本不可低估。
- 整体实验规模较大且计算密集，但不涉及从头训练或大规模微调LLM本身（仅训练轻量级的小型探针网络）。

## 5. 实验数量与充分性

### 主要实验矩阵
- **P(T)实验**：4种方法 × 8个模型 × T-REx测试集
- **P(IK)实验**：5种方法 × 8个模型 × PopQA测试集（此为8组主实验）
- **跨领域泛化实验**：探针迁移到8个模型的PopQA改写版（8组实验）
- **释义鲁棒性测试**：P(T)和P(IK)各10个随机释义集 × 8模型
- **翻译鲁棒性测试**：法语/波兰语 × 8模型 × 4方法
- **额外分析**：置信度稳定性分布（图4）、Spearman相关性分析、Friedman检验、P@不同召回率分析

### 充分性评估
- **优点**：模型种类广（规模、架构、微调状态），方法覆盖全面，评估维度多（多任务、多语言、多域），实验设计系统，交叉验证充分。
- **潜在的客观性考量**：验证集采用T-REx的对应假陈述替换策略可能使得真假区分相对容易；PopQA的P(IK)标签依赖贪心解码的正确性，可能引入噪声（模型可能"碰巧猜对"）。作者对此明确承认。

## 6. 主要结论与发现

### 结论一：训练型探针（Trained Probe）是最可靠的置信度估计器
- 在P(T)和P(IK)两种设定下，**所有模型上均表现最佳**，在T-REx上平均优于序列概率方法约0.3 AUPRC。
- 跨域泛化（T-REx → PopQA）：AUPRC降至0.62~0.81区间，虽有下降但仍然表现**实质性的泛化能力**。
- 跨语言泛化：英文训练的探针在法语中达到0.73~0.91 AUPRC，波兰语中0.61~0.91，说明模型以**类似方式编码不同语言的事实置信度**。
- **代价**：需要访问模型权重与监督训练数据。

### 结论二：非训练型方法表现较弱且不稳定
- **语言化置信度和替代令牌概率**在**指令微调模型**上表现尚可，是可行的替代方案；但在非指令微调模型上效果明显下降。
- **序列概率**方法在非指令模型上相对一致但总体较弱。
- **一致性方法**在P(IK)上多数模型上接近或低于随机水平。
- 大多数非训练方法在P(IK)上的表现接近或低于基线（chance level 0.11~0.27），说明它们作为幻觉缓解工具并不可靠。

### 结论三：对释义和翻译的稳健性
- 所有方法在两种语言变换下，AUPRC的标准差仅为5-10%，表明**在平均性能层面**这些方法相对不受释义和翻译影响。
- 方法的跨语言泛化均有高于随机水平的表现，但语言化方法在部分模型上失效。

### 结论四：模型的"事实编码"并**不是**完全稳定的
- **重要发现**：尽管方法平均AUPRC对释义稳定，但个别置信度分数在语义等价的输入变体之间显示出**显著波动**（标准差最高可达0.5以上）。
- LLM并未完全以"对事实的抽象"的方式存储知识，部分内容仍是**表面形式的记忆**，模型的置信度与正确性会随措辞而变化。
- 跨语言相关分析相关系数较高（40B以上模型Spearman ρ > 0.7），但Friedman检验揭示差异在统计上显著，即跨语言置信度不完全一致。

## 7. 方法论的优点

1. **系统性强**：首次在一个统一框架下实现对五类估计器的全面比较，明确区分P(T)和P(IK)两种互补置信度概念，使每种方法的适用条件一目了然。
2. **可实现性好**：详细给出了每类方法的具体实现细节（Prompt内容、层数、epoch、采样次数等），提高了结果的可复现性。
3. **模型覆盖面广**：涵盖8个模型，包含不同规模（7B~46.7B）、不同架构（Dense/SMoE）和不同训练范式（原始版/指令版），增强了结论的一般性。
4. **多维度评估**：同时评估了方法在区分真假（判别能力）、对未来回答正确性的预测能力、对释义的抗扰动能力、跨领域迁移能力、跨语言迁移能力和对事实编码的稳定性，形成了较全面的评估矩阵。
5. **跨域与跨语言验证**：探针的跨语言迁移实验设计（利用事实置信度在不同语言之间的内在一致性）具有较强的说服力。
6. **开源代码**：提供代码仓库，便于复现和扩展。

## 8. 不足与局限性

1. **原子事实局限性**：仅聚焦于"最小原子事实"（如三元组和简单问答）。对于复杂推理、非原子性事实、多跳问答、上下文学习等更高阶设定，结论是否成立仍然未知。
2. **P(IK)标签噪声**：使用贪心解码的正确性作为标签，无法区分"真正知道"与"碰巧猜对"，导致P(IK)评估存在噪声。
3. **一致性方法未测试P(T)**：由于一致性方法的设计限制（需要采样生成过程），无法在事实验证设定下与其它方法比较，故上述结论是在实验场景限制下得出的。
4. **训练数据分布风险**：探针方法的训练数据（如T-REx或PopQA）可能包含BERT时代的流行实体，训练分布与实际开放世界中的事实分布可能存在偏差。
5. **涉及跨语言鲁棒性测试的语言有限**：仅覆盖了法语和波兰语——两种印欧语系语言，对非印欧语系缺乏代表性。
6. **黑盒限制未解决**：最强的可靠方法（训练型探针）需要访问模型的权重和内部表征，而在商业闭源模型和不开放权重的服务中无法使用。作者承认黑盒方法目前仍然存在较大的可靠性差距。
7. **指令微调模型性能差异的归因模糊**：例如Mistral-7B-Instruct在部分任务上的具体表现与其构型有关（如改进的指令跟随能力），作者认为差异可能与模型训练细节有关，但无法确认。
8. **伪随机成分**：翻译质量虽有人工验证，但仅覆盖100个样本，可能存在未发现的质量问题。

## 代码与资源
- 论文代码开源地址：https://github.com/amazon-science/factual-confidence-of-llms （已包含在正文中）

## 总体评价

本文提供了目前学界急需的LLM事实置信度估计方法系统比较研究，方法分类清晰、实验设计严谨、多维度评估齐全。核心发现在实践层面具有较强的指导意义：如果追求最可靠的事实置信度，训练型探针是当前最优方案；但如果只能使用黑盒接口，指令微调后的语言化方法是较现实的替代——尽管可靠性有限。更具价值的发现是，方法层面的鲁棒性与其在**个别事实层面的稳定表现**并不相同：语言模型即使在"平均"水平上对措辞稳健，对**单个事实的置信度**仍极不稳定。这一发现揭示了模型在事实编码（而非仅表面记忆）方面的结构性弱点，为未来提升LLM事实一致性的研究指明了方向。

（完）
