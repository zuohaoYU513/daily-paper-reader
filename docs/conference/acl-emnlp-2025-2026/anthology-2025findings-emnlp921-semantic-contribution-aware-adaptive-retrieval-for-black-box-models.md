---
title: Semantic Contribution-Aware Adaptive Retrieval for Black-Box Models
title_zh: 面向黑盒模型的语义贡献感知自适应检索
authors: "Qinhong Lin, Zhongliang Yang, Yuang Cai, Dingfu Yu, Xuan Xu, Yu Li, Linna Zhou"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.921.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 提出语义贡献感知的自适应检索框架，用于RAG以缓解幻觉并提升事实准确性
tldr: 针对黑盒场景中动态检索难以泛化的问题，提出语义贡献感知自适应检索框架SCAAR。它迭代地利用即将生成词语的语义重要性动态调整检索阈值和过滤信息，保留最关键的语义词构造查询。实验表明，SCAAR在多种基线上显著提升RAG的幻觉缓解效果和事实准确性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp921/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp921/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp921/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 478, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp921/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 514, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 772, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 900, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1558, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 724, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 774, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 739, \"height\": 817, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1624, \"height\": 944, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 576, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 799, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1633, \"height\": 559, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1643, \"height\": 769, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp921/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1646, \"height\": 555, \"label\": \"Table\"}]"
motivation: 现有动态检索方法在黑盒LLM场景下难以泛化，RAG的检索时机和内容决策需要更有效的自适应机制。
method: SCAAR根据待生成词的语义重要性动态调整检索阈值，并保留最关键的语义词来构造查询。
result: 综合评估显示SCAAR在多组基线上显著提升幻觉缓解与事实准确性。
conclusion: 语义感知的自适应检索能有效改进黑盒模型的RAG知识利用。
---

## Abstract
Retrieval-Augmented Generation (RAG) plays a critical role in mitigating hallucinations and improving factual accuracy for Large Language Models (LLMs). While dynamic retrieval techniques aim to determine retrieval timing and content based on model intrinsic needs, existing approaches struggle to generalize effectively in black-box model scenarios. To address this limitation, we propose the Semantic Contribution-Aware Adaptive Retrieval (SCAAR) framework. SCAAR iteratively leverages the semantic importance of words in upcoming sentences to dynamically adjust retrieval thresholds and filter information, retaining the top- 𝛼 % most semantically significant words for constructing retrieval queries. We comprehensively evaluate SCAAR against baseline methods across four long-form, knowledge-intensive generation datasets using four models. Our method achieved the highest score on each dataset with GPT-4o. Extensive experiments also analyze the impact of various hyperparameters within the framework. Our results demonstrate SCAAR’s superior or competitive performance, showcasing its ability to effectively detect model retrieval needs and construct efficient retrieval queries for relevant knowledge about problem-solving in black-box scenarios. Our code is available on https://github.com/linqinhong/SAC.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLMs）在问答、摘要、翻译等NLP任务中表现优异，但在面对时间敏感、复杂推理任务时容易产生幻觉（hallucination），即生成与事实不符或推理不一致的内容。检索增强生成（RAG）通过将外部相关知识注入模型上下文来缓解幻觉问题，提升事实准确性。
- **现有局限**：
  - 传统静态RAG（如固定间隔检索、单轮检索）无法适应长文本生成和多步推理任务，检索时机和检索内容不够精准。
  - 已有的自适应检索方法（如FLARE、DRAGIN、SeaKR）依赖模型的内部状态（注意力分数、隐藏层、token概率分布等），在**黑盒模型**（如GPT-4、GPT-4o）场景下无法有效泛化，因为这些模型不暴露内部状态。
  - 现有黑盒适配方法（如多响应一致性、语义熵）往往需要多次额外生成，计算开销大。
- **核心问题**：在仅能获取token概率信息的黑盒场景下，如何有效确定"何时检索"（检索时机）和"检索什么"（查询构建），以提升RAG的性能与效率。
- **论文的核心含义**：提出一种**语义贡献感知的自适应检索框架（SCAAR）**，通过外部轻量级encoder计算每个词的语义贡献，动态调整检索阈值并过滤低重要性词语来构建高质量查询，从而在黑盒场景实现有效、高效的自适应检索。

---

### 2. 论文提出的方法论

#### 2.1 整体框架
SCAAR 由三个核心组件构成：
- **语义贡献感知加权（SCW）** —— 用于解决"何时检索"；
- **百分位过滤查询构建（PFQ）** —— 用于解决"检索什么"；
- **生成精炼（Generation Refinement）** —— 利用检索到的知识重新生成句子。

#### 2.2 语义贡献计算（Word Contribution）
- 采用 **leave-one-out（留一法）** 方法：给定问题 $q$ 和当前生成句子 $s_t$，依次移除句子中每个词 $w_{t,i}$，得到损坏句 $s_t \setminus w_{t,i}$。
- 利用外部cross-encoder模型（如RoBERTa-large）计算原始句与损坏句的语义相似度，从而得到该词的语义贡献分数：
  $$ r(w_{t,i}; q, s_t) = 1 - f_{x\text{-enc}}([q, s_t], [q, s_t \setminus w_{t,i}]) $$
- 贡献值在0~1之间，数值越大表示该词对句子语义越重要。

#### 2.3 动态阈值缩放（Threshold Scaling）
- 对语义贡献值进行**句子级归一化**，得到语义贡献加权系数（SCW）：
  $$ r'(w_{t,i}; q, s_t) = \frac{|s_t| \cdot r(w_{t,i}; q, s_t)}{\sum_{w_{t,i} \in s_t} r(w_{t,i}; q, s_t)} $$
- 用归一化贡献值的**指数**缩放原始阈值：
  $$ \theta_{\text{scaar}}(w_{t,i}; q, s_t) = \theta(w_{t,i}; q, s_t)^{r(w_{t,i})} $$
  - 重要词获得更高阈值，更容易触发检索；次要词阈值较低，减少不必要检索。

#### 2.4 检索判定（Retrieval Determination）
- 词概率计算：词的生成概率为其所有token概率的乘积，并进行**长度归一化**（取几何平均）以避免长词概率系统性偏低：
  $$ P'(w_{t,i}|C, W, w_{t,<i}) = P(w_{t,i}|C, W, w_{t,<i})^{1/|w_{t,i}|} $$
- 当**任何词**的归一化概率低于其对应的动态阈值时，即触发检索。
- 关键：由于仅需token概率信息和外部cross-encoder（轻量级），可推广到黑盒模型。

#### 2.5 百分位过滤查询构建（PFQ）
- 当触发检索时，将当前句子中的词按语义贡献**降序排序**。
- 仅保留贡献值在**top α%**以内的词（$\alpha$-百分位过滤）。
- 再进一步剔除那些生成概率低于各自动态阈值的"幻觉词"。
- 将原始问题 $q$ 与剩余的高贡献词拼接，构成最终检索查询 $q_r$。
- 核心思想：绝对阈值（如固定去掉10%的词）无法适应分布不均匀的语义贡献，而百分位过滤提供相对标准，更好控制查询长度与质量。

#### 2.6 生成精炼（Generation Refinement）
- 若句子未触发检索，则直接作为输出；
- 若触发，则用构造的查询 $q_r$ 从知识库检索top-k文档，并结合上下文知识重新生成该句子：
  $$ C_t \sim D \mid \text{query} = \text{qry}_{\text{scaar}}(q, s_t) $$
  $$ s'_t = M(C_t, q, s'_{<t}) $$

---

### 3. 实验设计

#### 3.1 数据集（Benchmark）
- **2WikiMultiHopQA**：多跳QA数据集，需要多步推理和信息综合。
- **HotpotQA**：大规模多跳问答数据集，需要跨文档推理。
- **IIRC**：不完整信息阅读理解数据集，涉及指令理解、多文档信息整合。
- **StrategyQA**：策略推理问答数据集，答案为"是/否"，需要隐式推理和常识结合。
- 每个数据集随机选取 **300个样本** 进行评估。

#### 3.2 评估指标
- **EM（Exact Match）** 和 **F1** 分数（StrategyQA仅用EM/F1，因答案为是非格式）。
- **检索效率（$S_{\text{eff}}$）**：$S_{\text{eff}} = \Delta S / N_R$，即每次检索带来的EM/F1平均提升。

#### 3.3 使用的模型
- 开源白盒模型：Llama-2-7B、Llama-2-13B、Llama-3.1-8B（SCAAR使用时封装为API模拟黑盒）。
- 真实黑盒模型：GPT-4o。
- 外部语义encoder：RoBERTa-large（默认）、DeBERTa（替换实验）。

#### 3.4 知识库与检索器
- 知识库：Wikipedia（21,015,324个段落），每块100 token。
- 检索器：默认 **BM25**（词法匹配）；另用 **DPR**（稠密检索）做替换实验。
- 检索数量：默认返回 top-3 文档；另做了2、4、5、7的消融。

#### 3.5 对比方法（Baselines）
- **w/o RAG**：无检索的纯生成。
- **SR-RAG**（单轮RAG）：仅对初始问题检索一次。
- **FL-RAG**（固定长度RAG）：固定N个token触发检索。
- **FS-RAG**（固定句子RAG/IRCoT）：每个句子结束触发检索。
- **FLARE**：基于token置信度触发检索，固定阈值，自适应方法。
- **DRAGIN**：基于注意力分数的动态阈值，白盒自适应方法。
- 原FLARE是token级，论文将其改为词级（几何平均）以对齐比较。

---

### 4. 资源与算力

- **论文未明确说明**所用GPU型号、数量及具体训练时间（该工作无需训练，属于推理阶段方法）。
- **额外开销分析（附录G）**：
  - SCAAR使用RoBERTa-large（约340M参数）作为语义贡献计算器。
  - 与DRAGIN相比，SCAAR的额外时间开销约为：
    - Llama-3-8B上约为DRAGIN的 **1/2**（SCAAR约60min vs DRAGIN约40min，300个2WikiMultiHopQA样本）；
    - Llama-2-13B上约为DRAGIN的 **1/3**（SCAAR约200min vs DRAGIN约150min）。
  - 推理模型越大，辅助模型的相对开销越小。
  - 与self-consistency类黑盒方法相比，SCAAR只需单次生成 + cross-encoder计算，开销显著更低。

---

### 5. 实验数量与充分性

#### 5.1 实验数量概览
| 实验类别 | 具体设置 | 实验数量 |
|---|---|---|
| 主实验 | 4数据集 × 4模型（Llama-2-7B/13B、Llama-3.1-8B、GPT-4o） | 大量综合对比 |
| 初始阈值消融 | 3模型 × 3阈值（0.9/0.8/0.7） × 4数据集 | 108组配置 |
| 权重方法对比 | ORIGIN / ATTN / SCW × 不同查询方法 | 9种组合 |
| 查询构建对比 | Curr-Sent / Real-Words / PFQ | 3种方法 |
| 百分位α消融 | 不同α值（20%~100%） × 2数据集 | 多组 |
| 编码器消融 | RoBERTa vs DeBERTa | 3数据集 |
| 文档数消融 | 2/3/4/5/7 × 3模型 × 多数据集 | 大量 |
| 检索器消融 | BM25 vs DPR | 3数据集 |
| 粒度对比 | 词级 vs token级阈值 | 3模型 |

#### 5.2 充分性评估
- **充分性**：实验覆盖多个数据集、多种模型规模和类型（开放/黑盒）、多项消融（阈值、权重、查询、百分位、编码器、文档数、检索器），能够较全面验证各组件贡献。
- **公平性**：
  - 在相同初始阈值下对比三种自适应方法（FLARE、DRAGIN、SCAAR），控制了关键变量（图2），避免了"只报各方法最优结果"的不公平比较。
  - 但主实验表格中仍以各方法的最优结果为报告标准，存在一定的"最佳结果偏差"风险。
  - 消融实验中的"win count"统计方法（108配置下计算最优次数）较为客观。

---

### 6. 论文的主要结论与发现

1. **SCAAR在多数设置下优于FLARE和DRAGIN**，且不需要模型内部状态，证明基于语义贡献的检索判定和查询构建能有效感知模型的知识缺口。
2. **黑盒场景有效**：在GPT-4o上，SCAAR在全部4个数据集上取得最高分，显著优于同样适用于黑盒的FLARE（固定阈值方法），验证了动态阈值的优势。
3. **静态检索效果不佳**：FS-RAG等固定检索方法有时甚至不如无检索，因为不相关检索内容会干扰模型原有的正确推理。
4. **DRAGIN在Llama-3.1-8B上表现异常**：该模型对token赋予较高置信度，导致DRAGIN触发检索次数过少，性能退化。
5. **SCW加权优于基于注意力（ATTN）和统一权重（ORIGIN）**：在108组配置中最高胜出次数；可视化也显示SCW能有效识别"American"、"film"等关键语义词。
6. **PFQ查询构建优于其他方案**：基于α-百分位的过滤能控制查询长度和质量，显著提升检索效率。
7. **词级阈值略优于token级**：词级平均在EM/F1上略高，且保留语义完整性和生成效率。
8. **最佳文档数为3**：过多或过少的检索文档都会干扰模型推理。
9. **BM25优于DPR**：DPR在短句查询场景下难以捕捉待生成句子的语义，BM25仍是自适应RAG的更可靠选择。

---

### 7. 优点

- **黑盒兼容性**：仅依赖token概率和外部轻量级cross-encoder，不访问模型内部状态，使其可直接应用于GPT-4o等闭源模型，实用性很强。
- **动态阈值机制设计巧妙**：利用语义贡献的指数幂缩放阈值，重要词获得更高触发阈值，更可能触发检索——比FLARE的固定阈值更灵活，比DRAGIN的注意力方法更通用。
- **查询构建创新**：PFQ（百分位过滤）结合语义贡献排序和动态阈值二次过滤，同时控制查询长度和质量，较好解决了"用当前整句作查询"带来的噪声干扰。
- **检索效率指标**：引入 $S_{\text{eff}}$（每次检索的收益），不仅关注最终性能，还关注检索的经济性，评估维度更全面。
- **实验严谨**：大量消融（阈值、权重方法、查询方法、百分位、编码器、文档数、检索器、粒度）和多模型验证，且提供了相同阈值下的对比和win count统计，增强结论可信度。
- **代码开源**：代码公开在GitHub，可复现性强。

---

### 8. 不足与局限

- **额外计算开销**：虽然引入的RoBERTa-large模型相对较小，但每个词都需要一次cross-encoder前向计算（leave-one-out），实际运行时间比DRAGIN多约50%（8B模型），对延迟敏感场景不够友好。
- **启发式超参数**：百分位过滤常数α依赖人工设定，最优值随数据集变化；论文也承认需要训练分类器学习α预测，但目前未实现。
- **评估指标局限**：仅使用EM和F1作为评价指标，未使用LLM-based评估（如GPT-4评分、事实性指标），可能无法全面反映生成质量。论文在局限性部分也坦承了这一点。
- **DPR稠密检索效果不佳**：Short upcoming sentence + DPR的组合导致检索质量下降，说明SCAAR对检索器类型存在依赖，适应性有待增强。
- **词级粒度可能掩盖token级信号**：论文也承认词级概率（几何平均）可能模糊token概率差异，例如某词含一个0.

例如某词含有一个生成概率接近 0 的 token，但经由几何平均后可能被其他高概率 token 稀释，导致该词整体概率仍高于阈值，从而漏检；反之亦然，某些低概率 token 可能拉低整词均值而引发不必要的检索。

---

### 9. 总结与展望

#### 9.1 核心贡献回顾
SCAAR 面向黑盒大语言模型提出了一种语义贡献感知的自适应检索框架。其核心创新在于：

- 将“何时检索”从依赖内部状态（注意力、隐藏层）转化为依赖**外部轻量级 cross-encoder 计算的词级语义贡献**，从而在仅需 token 概率的黑盒条件下实现动态阈值触发；
- 将“检索什么”从整句或启发式截断升级为**百分位过滤 + 动态阈值二次筛选**，显著提升查询的针对性和噪声鲁棒性；
- 在检索触发后通过**重新生成精炼**，将检索到的知识真正用于修正当前句子，而非简单拼接。

#### 9.2 实验结果确认的结论
- 在 4 个多跳推理数据集、4 种模型（含闭源 GPT-4o）上，SCAAR 均取得优于或持平于现有自适应 RAG 方法的性能；
- 在相同初始阈值下，SCAAR 的胜出率高于 FLARE 和 DRAGIN，且不依赖模型内部状态，适用范围更广；
- 各组件（SCW、PFQ、词级粒度）均通过消融验证了其必要性。

#### 9.3 未来研究方向
论文提出的值得拓展的方向包括：

- **α 的自适应预测**：目前百分位参数 α 需人工设定且随数据集变化，论文建议训练一个轻量分类器，根据生成句子的语义分布自动预测最优 α，从而消除启发式调参；
- **任务泛化**：当前实验集中在多跳问答，未来可推广至长文档生成、摘要、对话系统等更依赖“知识何时缺失”的任务；
- **与稠密检索结合**：DPR 在短句查询下表现不佳，未来可探索更适配语义贡献查询的稠密检索模型或混合检索策略；
- **降低额外延迟**：leave-one-one 逐词评估存在线性开销，可探索并行化或基于采样的近似评估，使之更贴近实时应用。

#### 9.4 总体评价
SCAAR 为黑盒场景下的自适应 RAG 提供了一条切实可行的新路径。它巧妙地将解释性概念“词对语义的贡献”引入检索决策，既规避了对模型内部访问的依赖，又在性能与效率之间取得了良好平衡。尽管存在计算开销和超参数敏感性等不足，但该工作的问题定义、方法设计和实验分析都相当完整，对后续研究具有较高的参考价值。

（完）
