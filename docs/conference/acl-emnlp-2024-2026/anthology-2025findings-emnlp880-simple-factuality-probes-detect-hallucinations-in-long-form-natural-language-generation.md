---
title: Simple Factuality Probes Detect Hallucinations in Long-Form Natural Language Generation
title_zh: 简单事实性探针检测长文自然语言生成中的幻觉
authors: "Jiatong Han, Neil Band, Muhammed Razzak, Jannik Kossen, Tim G. J. Rudner, Yarin Gal"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.880.pdf"
tags: ["query:metacognitio"]
score: 10.0
evidence: 用轻量级探针读取隐藏状态以检测长文生成中的事实错误
tldr: 大语言模型常以高度自信的方式产出幻觉内容，现有检测方法需要多次采样，成本高昂。论文提出仅一次采样即可借助隐藏状态上的轻量探针预测生成文本的事实正确性，从而检测长文生成中的幻觉。实验证明该简单基线在效果上与多采样方法相当，为推理时幻觉检测提供了低成本高效方向。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1317, \"height\": 631}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1564, \"height\": 486}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1576, \"height\": 550}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1328, \"height\": 838}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1515, \"height\": 544}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 687}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1653, \"height\": 434}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 1002}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 968}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 576}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 471}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1655, \"height\": 768}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 558}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 883}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1661, \"height\": 1213}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 478}]"
motivation: 大语言模型长文生成中幻觉频发，现有检测需大量采样，成本高且随模型规模增长不可行，亟需单样本低成本检测方案。
method: 利用生成时隐藏状态中包含的事实性信息训练轻量分类探针，在推理时基于单次生成结果预测整段输出的事实正确性。
result: 在多种长文生成基准上，单样本隐藏状态探针性能与昂贵的多采样方法相当，验证了该思路的有效性。
conclusion: 隐藏状态探针为长文幻觉检测提供简单高效的基线，可作为推理时事实性评估与可信取舍的实用工具。
---

## Abstract
Large language models (LLMs) often mislead users with confident hallucinations. Current approaches to detect hallucination require many samples from the LLM generator, which is computationally infeasible as frontier model sizes and generation lengths continue to grow. We present a remarkably simple baseline for detecting hallucinations in long-form LLM generations, with performance comparable to expensive multi-sample approaches while drawing only a single sample from the LLM generator. Our key finding is that LLM hidden states are highly predictive of factuality in long-form natural language generation and that this information can be efficiently extracted at inference time using a lightweight probe. We benchmark a variety of long-form hallucination detection methods across open-weight models up to 405B parameters and demonstrate that our approach achieves competitive performance with up to 100x fewer FLOPs. Furthermore, our probes generalize to out-of-distribution model outputs, evaluated using hidden states of smaller open-source models. Our results demonstrate the promise of hidden state probes in detecting long-form LLM hallucinations.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：前沿 LLM 越来越多地被应用于长文生成任务（代码库级修改、多页技术报告、推理/证明辅助等），输出可达数万 token。在这种规模下，模型即使大都生成准确内容，也常以**高度自信的方式产生幻觉**，误导用户。
- **现有瓶颈**：当前主流的长文幻觉检测依赖**多次采样**方法，如语义熵、自洽性、图不确定性等。这些方法在段落级输出上有效，但对数百亿参数的旗舰模型、每次生成上万 token 的场景，计算量过高（多次调用昂贵推理模型），难以实用。
- **论文切入点**：作者提出，LLM 的**隐藏状态中已经编码了关于自身生成内容事实性的信息**，可以用一个极轻量的“事实性探针”（Factuality Probes）在**仅一次采样**后，对生成文本中的原子断言语义级事实性给出量化评分。
- **整体含义**：该方法提供了目前极其简单、高效的长文幻觉检测基线，性能与昂贵得多、需要多次采样的检测方法相当，且计算开销可降低约两个数量级（100× FLOPs）。论文结果是“隐藏状态探针可作为长文生成实时事实性评估的实用工具”的有力证据。

## 2. 方法论

### 2.1 核心思想

- 关键假设：LLM 在对一个“原子声明”（atomic claim）进行处理时，其**最后一个 token 的隐藏状态**会携带该声明是否被模型内部“认定”为事实的信号。
- 流程：
  1. 生成模型 π_gen 对 prompt 做**单次长文采样**；
  2. 辅助 LM π_aux 把长文分解为**原子声明**（self-contained claims），并为每个声明在原文中找到支撑 token span；
  3. 将每个声明输入编码 LM（可以是生成模型本身或一个更小模型 π_small），提取隐藏向量 h_c；
  4. 用训练好的轻量分类器 f 输出该声明为真的概率 p̂_c；
  5. 把 p̂_c 通过 span 归属映射回原文，形成“红色–绿色”热力图式细粒度置信度可视化。

### 2.2 训练过程（Alog1）

- **阶段1：生成监督的事实性训练集**
  - 用 π_gen 生成每个 prompt 的长文本输出 z；
  - 用 π_aux 将 z 分解为原子声明集合 C；
  - 对每个声明 c，用 π_enc=π_gen 或 π_small 获取隐藏状态 h_c；
  - 使用检索增强验证器 f_ret（如 FActScore 的维基百科文档检索、LongFact 的搜索引擎）给出二元真实标签 y_c∈{0,1}；
  - 收集 (h_c, y_c) 对形成数据集 D_probe。

- **阶段2：拟合探针分类器**
  - **稀疏逻辑回归**：L1 惩罚，目标是 `min_θ 1/|C| Σ L(y_c, f(h_c;θ)) + λ||θ||₁`，其中 L 为 logistic loss，λ 控制稀疏度；
  - **XGBoost**：可捕获隐藏状态维度间非线性依赖的梯度提升树；
  - 两者都是极轻量的分类器。

### 2.3 推理阶段（Alog2）

- 与训练类似的步骤：单次生成 → 声明分解与 span 归属 → 隐藏状态提取 → 探针打分 → 用 span 可视化文本事实性。
- 关键差异：推理时不用检索验证器，也没有多次采样；只对每个声明做一次 forward pass。

## 3. 实验设计

### 3.1 数据集与验证场景

- **训练数据来源**：LongFact（Wei et al., 2024）数据集中的多个主题的 LLM 长文生成；标签由基于网页检索的评估器给出。
- **测试数据来源**：
  - **域内/跨域**：使用基于维基百科实体（FActScore）生成的人名问答，训练与测试主题分布差异较大，从而考察领域泛化性（训练目标与测试目标不同：LongFact 主题，FActScore 人物）。
  - **闭源模型输出**：GPT-4o-mini、InstructGPT、ChatGPT、PerplexityAI 的输出。
- 训练/测试规模见表 5，例如 Llama3.1-8B 训练样本 3,374 条 / 50 个主题，测试 1,732 条 / 30 个实体等。
- 所有生成长度限制在 512 token，采样温度为 0.7，top-k=50。

### 3.2 对比基线

- **Semantic Entropy (SE)**：对声明生成问题再做高温度多次回答，计算语义熵；
- **P(True)**：问题生成 + 多候选答案与自身比较打分；
- **SelfCheckGPT**：让模型根据上下文自检声明正确性；
- **Graph-based Uncertainty**：对 k 个高温度响应 + greedy 响应构二部图，使用集中度 / 接近中心性测量，包含 SC+VC（自洽性 + 言语置信度）和 Closeness Centrality；
- **Verbalized Confidence**：直接问模型自身声明的正确概率；

所有方法都统一进行声明分解、修正等预处理，保证公平比较。

### 3.3 评估方式与探针配置

- 指标：AUROC；同时对比所需 FLOPs（计算量）；
- 用 3-fold 交叉验证训练探针，重复 / bootstrap 求标准误差；
- 探针输入位置：首 token（FT）、末 token（LT）、倒数第二 token（SLT）；可采用单层或 5 层/3 层 hidden states 连接；
- 基分类器：Logistic Regression (LR) 与 XGBoost。

## 4. 资源与算力

- 论文在**主文中没有给出 GPU 型号与训练时长**；在附录 D 中说明了：
  - 全部实验约消耗 **440 GPU hours（基于 A100 节点）**，来自 OATML 实验室机器及第三方云；
  - 总体计算量约 2×10²⁰ FLOPs（文中估计）；
  - 由于前端模型包括 405B 参数，训练成本尚难精确拆分为每项方法或每个探针的独立开销；
  - 大量的对比集中在 **测试时单次生成 vs 多次采样的 FLOPs 差异**，统计图中明确展示了“相似 AUROC 下 Fact Probe 需要的 FLOPs 比 SE/P(True)/SelfCheckGPT/SC+VC 等低数个数量级”。

## 5. 实验数量与充分性

- **实验相当充分**：
  - **模型规模维度**：覆盖 Llama3.2-3B、Llama3.1-8B、Llama3.1-70B、Llama3.1-405B 以及 Gemma2-9B，共 5 个开放权重模型 + 多个闭源模型测试；
  - **跨域维度**：跨主题训练、维基百科人物测试；还加入了“反向跨域”实验（训练与测试数据集颠倒），显示泛化受限的情形；
  - **跨模型维度**：小模型探针评估更大模型 / 闭源模型，并测试了同一模型系列内固定探针的 OOD 性能；
  - **超参消融**：不同 token 位置（FT/LT/SLT）、不同层组大小（1/5），LR vs XGBoost 均进行了对比；
  - **数据过滤消融**：主观性过滤（subjectivity filtering）的影响；
  - **校准实验**：rejection ratio 与保留数据准确率的关系；
  - **额外因果分析**：附录中识别“事实性神经元”并对其进行 clamping/steering，显示可提升生成事实性，从而为隐藏状态中的事实性信号提供更内在解释。

- **公平性讨论**：
  - 对于计算开销极高的 SE，作者仅对约 20% 的测试样本进行随机抽样，这在一定程度上可能让 SE 的指标估计波动更大，但也说明 SE 的负担确实很高；
  - 所有方法共用同样的声明分解/预处理管道，使比较专注于“置信度估计”环节；
  - 报告了 bootstrap 标准误，说明稳定性。

总体而言，实验覆盖了方法性能、规模扩展性、泛化性、校准性和可解释性，数量充分且设计较为客观公正，但有些对比（SE 抽样）比例并不完美，不过已作出了合理权衡说明。

## 6. 主要结论与发现

1. **隐藏状态探测有效**：训练在 LLM 隐藏状态上的轻量线性探针能在长文生成中对原子声明做准确的事实性预测，效能不逊于多采样方法；
2. **计算量优势显著**：相比语义熵、自洽性等文本级方法，要获得相当的 AUROC，本方法往往少用 1–2 个数量级（最多约 100×）的 FLOPs；
3. **规模规律清晰**：在 3B 到 405B 的 Llama 模型范围内，探针 AUROC 随模型规模近似对数线性增长，较大的模型对事实性信号的编码更鲜明/线性化；
4. **泛化能力强**：
   - 跨域：在 LongFact 多样的主题上训练，在 FActScore 人物上测试，性能仍很好；
   - 跨模型：探针可从小模型输出迁移到大模型（如 3B 探针评估 405B 输出），甚至从开放权重模型迁移到闭源模型生成；
   - 闭源泛化稳定性：InstructGPT > ChatGPT > PerplexityAI。
5. **校准较好**：对 8B 以上模型，探针置信度与实际正确率高度相关；将低置信度声明剔除后保留数据准确率持续提升；
6. **末 token 隐藏状态最有效**：探针在最后 token 处提取特征效果优于首 token/倒数第二 token；
7. **该方法在使用同一分解管道时所需的后处理步骤最少**，且对非定义类复杂断言也有效，不像 SE/P(True) 那样对问题生成质量敏感。

## 7. 优点

- **简单**：将长文幻觉检测问题转化为“在隐藏状态上训练轻量分类器”，仅需一次生成调用，无需检索外部知识或多次采样；
- **可解释**：探针稀疏/LR 本身具有较好的可解释性；定位出的“事实性神经元”还支持因果的激活干预，进一步揭示了隐藏状态编码的信息；
- **高效**：训练/推理成本低，易于在实时或大规模场景中部署；
- **泛化性惊人**：利用同一模型家族内小模型输出训练出的探针，在极大模型（如 405B）甚至闭源模型上依然鲁棒，说明事实性表示具有一定跨模型一致性；
- **系统全面**：广泛覆盖 3B 到 405B、跨域/跨模型、评估测量与校准以及消融实验，结论支持充分；
- **面向应用**：其 span 级可视化输出能直接帮助用户判断哪些段落更可信，比给一个单一置信度更实用。

## 8. 不足与局限

- **依赖辅助模型分解**：事实性探针依赖于 π_aux 的声明分解与语句修正质量；若分解粗糙、claims 间上下文丢失或判断主观，会直接影响探针效果；
- **忽略声明间依赖**：当前探针把声明独立看待，没有利用长文中许多事实互为条件的关系；未来可以考虑用上下文/结构化依赖增强；
- **事实性定义受限**：使用检索/搜索验证器作为真实标签，对需要深层推理或多跳验证、不确定性很强的陈述，标签可靠性和覆盖度可能不充分；
- **模型输出分布偏移**：主实验基于百科类主题（人物传记等），对于高度专业性、数据稀缺性领域，性能可能并不显著；正常训练和反向跨域实验结果也表明数据分布会影响泛化；
- **计算量对比的完整性**：虽然强调 FLOPs 节省很多，但没有讨论隐藏层获取、缓存和部署内存开销，尤其是许多场景中编码模型与生成模型共用可能带来额外内存/运行调度成本；
- **样本/数据量偏小**：训练样本最多几千条，外部因素（如搜索库标注的不一致）可能导致标签噪声；测试集也主要来自百科实体类问答；
- **潜在安全/依赖风险**：论文在附录明确指出，恶意使用者可利用对隐藏状态的了解干扰校准，所谓“对抗攻击”可能使模型对错误内容显得更自信。

**总结**：这篇论文提出了一种极其简单、高效且在多项基准上可与昂贵多采样方法媲美的长文幻觉检测技术，验证了 LLM 隐藏状态中蕴含有可迁移的事实性信号。虽然依赖辅助分解，并且覆盖场景偏百科类，但在当前长文生成规模不断增长的背景下，作为实时细粒度幻觉检测的基线和框架，具有非常明显的实用价值及研究启发意义。

（完）
