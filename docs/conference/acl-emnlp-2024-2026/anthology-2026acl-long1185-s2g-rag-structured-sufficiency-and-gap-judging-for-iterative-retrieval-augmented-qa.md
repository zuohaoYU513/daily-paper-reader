---
title: "S2G-RAG: Structured Sufficiency and Gap Judging for Iterative Retrieval-Augmented QA"
title_zh: "S2G-RAG: 面向迭代检索问答的结构化充分性与缺口判断"
authors: "Minghan Li, Junjie Zou, Xinxuan Lv, Chao Zhang, Guodong Zhou (周国栋)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1185.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 迭代检索问答中显式判断证据充分性并识别证据缺口，避免基于不足证据生成无依据回答
tldr: RAG 可以用外部证据约束生成，但多跳问答中如何判断证据是否足够并决定下一步检索仍是难点。S2G-RAG 设计了显式控制器 S2G-Judge，每轮判断当前证据记忆是否足以回答，不能则输出结构化缺口描述并映射到后续检索。该方法系统性地避免了因证据链不完整而给出无依据答案，也减少了冗余干扰文本的累积。实验表明其有效提升了证据充分性判断和最终回答的事实性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1185/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1622, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1185/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1185/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1185/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1185/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 493, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1071, \"height\": 631, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 824, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 854, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 806, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 493, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 430, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 813, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1657, \"height\": 729, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1650, \"height\": 1364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1185/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1663, \"height\": 611, \"label\": \"Table\"}]"
motivation: 多跳 RAG 问答常因证据链不完整而过早回答，或累积冗余及干扰文本影响后续推理。
method: 提出 S2G-RAG，在每个迭代通过 S2G-Judge 控制器判断当前证据是否充分，若不充分则输出结构化缺口项目，再映射为检索请求。
result: 实验验证了该方法能改进证据充分性判断，减少基于不完整证据的回答并提升回答质量。
conclusion: 结构化充分性判断是提升证据约束生成忠实度的有效机制，可用于不断迭代的 RAG 问答系统。
---

## Abstract
Retrieval-Augmented Generation (RAG) grounds language models in external evidence, but multi-hop question answering remains difficult because iterative pipelines must control what to retrieve next and when the available evidence is adequate. In practice, systems may answer from incomplete evidence chains, or they may accumulate redundant or distractor-heavy text that interferes with later retrieval and reasoning. We propose S2G-RAG (Structured Sufficiency and Gap-judging RAG), an iterative framework with an explicit controller, S2G-Judge. At each turn, S2G-Judge predicts whether the current evidence memory supports answering and, if not, outputs structured gap items that describe the missing information. We map these gap items into the next retrieval query, producing stable multi-turn retrieval trajectories. To reduce noise accumulation, we maintain a sentence-level Evidence Context by extracting a compact set of relevant sentences from retrieved documents. Experiments on TriviaQA, HotpotQA, and 2WikiMultiHopQA show that S2G-RAG improves multi-hop QA performance and robustness under multi-turn retrieval. Furthermore, S2G-RAG can be integrated into existing RAG pipelines with a lightweight component, without modifying the search engine or retraining the generator.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **研究领域**：检索增强生成（RAG）将大语言模型（LLM）与外部证据锚定，已成为知识密集型问答的标准方法。但对于多跳问答，模型往往需要跨多个文档、经历多轮检索与推理才能组合出最终答案，这促使了迭代式 RAG（iterative RAG）的出现。
- **核心痛点——检索控制瓶颈**：在每一轮迭代中，系统必须回答两个关键问题：
  1. 当前已累积的证据是否足以支撑最终作答？（停止条件）
  2. 若不足，下一步应该检索什么？（下一跳目标）
- **现有方法的三个不足**：
  1. **控制隐式化**：决策与自由文本生成纠缠，难以审计，在干扰项干扰下可能不稳定。
  2. **信息需求表达欠结构化**：下一跳需要什么信息往往表达为自由文本，易漂移、重复或过度泛化。
  3. **上下文噪声累积**：多轮检索自然会产生长而嘈杂的上下文，直接拼接会使推理与控制失稳；同时，中间状态标注昂贵，难以获得高质量的轮次级监督。
- **论文意义**：提出一种将检索控制显式化、模块化的迭代 RAG 框架，使系统在证据不充分时不会贸然作答，并能明确知道还缺什么信息，从而提高多跳问答的准确性、鲁棒性和可审计性。

## 2. 论文提出的方法论

### 2.1 整体框架（S2G-RAG）
- **核心思想**：将每轮迭代的检索控制转换为两个显式结构化输出——
  1. **充分性判断**（sufficiency decision）\(s_t \in \{true, false\}\)：当前证据上下文是否足以回答问题；
  2. **结构化缺口项**（structured gap items）\(G_t\)：若不足，具体缺少哪些信息。
- **推理循环**（最多 \(T\) 轮）：
  1. **S2G-Judge** 读入 \((q, C_t)\)（问题+当前证据上下文），输出 \(y_t = (s_t, G_t)\)；
  2. 若 \(s_t = true\)，调用 **Reasoner** 基于 \((q, C_t)\) 生成最终答案；
  3. 否则，由 \(G_t\) 构造下一轮检索查询 \(\tilde{q}_t\)，经检索器取得文档 \(D_t\)；
  4. **句子级证据抽取器** 从 \(D_t\) 中选出与 \((q, G_t)\) 相关的句子，形成紧凑证据块 \(E_t\)，追加到证据上下文：\(C_t = C_{t-1} \oplus E_t\)；
  5. 循环直至充分或达到预算上限 \(T\)。

### 2.2 S2G-Judge 的结构化输出
- 每个缺口项 \(g \in G_t\) 采用四字段规范化结构：
  - **category**（类别）：取值于 {bridge_entity（桥梁实体）, attribute（属性）, relation（关系）, evidence_span（证据片段）, other（其他）}；
  - **target**：待查询的实体；
  - **slot**：粗粒度的属性或关系名；
  - **description**：简短自然语言澄清。
- 显式施加“上下文唯一”约束：判断充分性时只能依据 \(C_t\) 中的证据，不能依赖参数化记忆（避免模型凭“记忆”认定证据充分）。

### 2.3 训练：基于执行轨迹的蒸馏（Trajectory Distillation）
- 在训练问题上运行迭代检索与证据累积流程，记录每一轮的状态快照 \((q, C_t)\)；
- 由强教师模型（GPT-4o-mini）在“上下文唯一”约束下为每个快照标注充分性判断和缺口项；
- 过滤冲突/格式错误标签后，用 LoRA 对小型 judge 模型做监督微调，损失为：
  \[
  L(\phi) = -\sum_{(x_t,y_t)} \sum_{i=1}^{|y_t|} \log p_\phi(y_{t,i} \mid y_{t,<i}, x_t)
  \]
- 最终训练数据：共 2,804 个快照（充分 1,396 / 不充分 1,408），按 90%/10% 划分训练/验证集。

### 2.4 查询构建与证据压缩
- **Gap-guided query construction**：将缺口项映射为查询短语——优先拼接 target + slot，否则使用 description；取最多 \(K\) 个有效短语附加到原问题后形成检索查询。
- **句子级证据抽取**（Sentence-level Evidence Extractor）：从新检索文档中切分句子，由 LLM（提示词约束只能输出句子索引、不得改写生成）根据 \((q, G_t)\) 选择重要句子，保留来源文档标题以供溯源。该方法具有指针式（pointer-based）的可审计性，且能显著压缩上下文规模。

## 3. 实验设计

### 3.1 数据集
| 数据集 | 类型 | 特点 |
|---|---|---|
| TriviaQA | 单跳问答（开放域） | 答案通常只需单篇 Wikipedia 文章支持 |
| HotpotQA | 多跳问答 | 需跨多文档组证、有无桥接型/比较型问题 |
| 2WikiMultiHopQA | 多跳问答 | 强调实体消歧与细粒度证据组合 |

所用语料库为各数据集提供的 Wikipedia dump 官方开发集。

### 3.2 检索配置
- **稀疏检索**：Pyserini 实现的 BM25；
- **密集检索**：E5-base-v2；
- 默认检索预算 \(T = 4\) 轮，每轮 top-\(k = 6\) 篇文档，并对标题去重。

### 3.3 模型配置
- Reasoner 与 Evidence Extractor：Llama-3-8B-Instruct；
- S2G-Judge：Llama-3.2-3B-Instruct，LoRA 微调（r=16，α=32）；
- 教师模型：GPT-4o-mini（仅用于标注训练数据）。

### 3.4 对比基线
- **NaiveGen**：无检索直接作答；
- **Standard RAG**：单轮检索后生成；
- **IR-CoT**：检索与中间推理链交错；
- **FLARE**：基于生成时不确定性触发检索；
- **ReSP**：迭代式 retrieve–summarize–plan；
- **Self-RAG**：反思 token 控制检索行为；
- **SIM-RAG**：训练轻量 critic 判断是否继续检索；
- **RAG-Critic**：基于错误分类学提供细粒度反馈的 agentic RAG。

### 3.5 主要对比结果摘要
- **BM25 设置下（与 SIM-RAG 等对比）**：
  - TriviaQA：EM 72.0 / F1 77.9（+1.3 EM / +2.3 F1）；
  - HotpotQA：EM 43.3 / F1 56.5（+10.6 EM / +13.2 F1，提升最大）；
  - 2WikiMultiHopQA：EM 41.7 / F1 48.6（+7.6 EM / +8.4 F1）。
- **E5 密集检索设置下**：在三个数据集上均为该面板最优，优于 RAG-Critic 等强基线。
- 额外实验（附录）：使用更强推理器 GPT-4o-mini 的变体下，HotpotQA EM 达 51.0–51.5、2Wiki EM 达 53+。

## 4. 资源与算力

- 论文未详细列出 GPU 型号、数量及精确训练时长，仅说明：
  - 训练涉及对 Llama-3.2-3B-Instruct 的 LoRA 微调（可参数高效完成）；
  - 实验中使用的硬件大约为 **2 × vGPU-48G 或等效配置即可复现**；
  - 使用 FP16 精度，训练 3 个 epoch，学习率 \(1\times10^{-4}\)，梯度累积 8，最大序列长度 2048，LoRA rank=16。
- 因此**具体算力信息和时间成本并未完全披露**。

## 5. 实验数量与充分性

实验设计较为全面，主要分为以下层次：

1. **主实验**：三个数据集 × 两种检索器（BM25/E5）× 多基线对比；
2. **消融实验**（HotpotQA/BM25）：
   - 去除 S2G-Judge（-15.8 EM）；
   - 用未微调 judge 替换（-4.1 EM）；
   - 去除句子级证据抽取器（-3.8 EM）；
3. **Sufficiency 判断可靠性分析**：二分类混淆矩阵（FPR 仅 6.44%）；
4. **上下文压缩效率分析**：压缩比、延迟对比（比原始拼接提速 17.7%）；
5. **压缩方法对比**：LLM summarization、ReComp（extractive/abstractive）与句子指针法对比；
6. **教师-学生差距扫描**：改变最大检索轮数 \(T \in \{0,\dots,5\}\)；
7. **鲁棒性测试**：检索宽度 top-k ∈ {2,4,6,8,10,20}、抽取上限 Ke 变化、不同 judge 骨干（Llama-3.2-3B vs Qwen-3-4B）；
8. **查询构造变体**：自由文本 vs 结构化缺口；K=1/2/3；
9. **HotpotQA 问题类型拆分**：Bridge 类型与 Comparison 类型；
10. **案例分析**：成功案例（两跳正确回答）与失败案例（检索覆盖不足）。

**总体评价**：
- 实验数量充足、覆盖面广，从“控制模块是否有效”“训练是否有用”“压缩是否有效”“结构化的价值”“对检索器/骨干的泛化性”等多个角度交叉验证；
- 消融设计干净：去除某一组件时固定其余组件（检索器、预算、推理器）；
- 对比方法在同一 Retrieval 设置和同一 Reasoner 下进行，总体公平（ReSP 例外，因结果引自原文，兼容性稍差）；
- 测试数据来自官方开发集，没有做测试集调优的迹象。

## 6. 主要结论与发现

1. **结构化显式控制有效**：将迭代 RAG 的控制转化为“充分性判断 + 结构化缺口预测”，能以轻量模块显著提升多跳 QA 的 EM/F1。
2. **轨迹蒸馏可行**：基于真实管线执行轨迹进行教师标注与学生微调，即使只用 Llama-3.2-3B 作为 judge，也能逼近 GPT-4o-mini 教师控制器的效果。
3. **句子级证据上下文有明显收益**：压缩比约 4.5×–6.4×，降低延迟同时提升准确率，缓解了长上下文的“lost in the middle”问题与干扰文本影响。
4. **跨检索器泛化性好**：在 BM25 与 E5 两种检索器下均有效，说明控制接口不依赖特定检索器。
5. **无训练时结构化接口也有价值**：即使不微调 judge，仅靠 prompt 与结构约束，效果已超过多数BM25下的多轮基线（说明显式 schema 本身能减少漂移与重复）。
6. **judge 倾向于保守**：不足判充分的错误率（FPR）仅为 6.44%，即不大可能在不充分时“过早收手”；尚有 31.60% 的已充分样例被误判为不足，存在校准提升空间。

## 7. 优点

- **控制显式、可审计**：区别于隐式 critic 或自由文本反思，S2G-Judge 输出结构化字段，检索轨迹可逐轮检查，缺口可追溯。
- **模块化设计，集成成本低**：judge 与 answer reasoner 解耦、检索器不参与训练，可轻量插入已有 RAG 流水线，无需重训生成器或改变搜索引擎。
- **可复现、资源要求友好**：采用 LoRA 微调 3B 模型，48G vGPU×2 即可复现训练实验。
- **有效利用中等成本监督**：通过执行轨迹蒸馏获得轮次级监督，且用“检索是否命中黄金支持文档”这一弱标签进行低成本过滤，不把黄金文档信息泄漏到模型输入中。
- **证据上下文设计精良**：句子级指针抽取保留可审计性（对应文档标题），避免了摘要式压缩导致的证据编造风险，同时大幅降低噪声累积。
- **分析详实**：不仅报告端到端指标，还深入分析控制器行为（混淆矩阵）、上下文压缩率、时间延迟、检索鲁棒性、教师-学生差距等，对实际工程部署有参考价值。

## 8. 不足与局限

- **缺口 schema 的表达能力受限**：四字段结构（category/target/slot/description）难以覆盖多实体连接、时间约束、跨多跳的复合关系等复杂查询，需要进一步扩展或引入结构化中间程序。
- **抽取-召回权衡**：句子级抽取虽然压缩了上下文、减少了干扰，但可能丢掉消歧所需的周边上下文，或遗漏跨句才成立的证据链。
- **sufficiency 预测偏保守**：近三分之一已充分上下文会被判为不足，导致多做无效检索、增加延迟；论文只给出方向性建议（校准则更好），并没有给出校准方案。
- **训练依赖较强的教师模型（GPT-4o-mini）**：虽然学生是 3B 轻量模型，但蒸馏流程需要调用专有模型，存在 API 成本和时间开销；论文未披露完整的教师标注预算。
- **教师-学生差距分析只有 F1 维度**：缺少对“结构化缺口本身”质量（准确率/召回率）的详细度量，教师与学生的行为差异不一定完全体现在端到端问答得分上。
- **实验语料局限于维基百科域问答**：未在更开放的工业级知识库（如网页搜索、结构化知识图谱）或更复杂的时间敏感推理任务中验证。
- **ReSP 基线未复跑**，其结果引自论文原文，与其它方法可能并非完全同设置，对比的公平性稍有折损。

**（完）**
