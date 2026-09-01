---
title: Improving Model Factuality with Fine-grained Critique-based Evaluator
title_zh: 使用细粒度批评式评价器提升模型事实性
authors: "Yiqing Xie, Wenxuan Zhou, Pradyot Prakash, Di Jin, Yuning Mao, Quintin Fettes, Arya Talebzadeh, Sinong Wang, Han Fang, Carolyn Rose, Daniel Fried, Hejia Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.400.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过细粒度声明级反馈提升语言模型输出的事实性
tldr: 语言模型生成的事实性错误需要被准确评估并反馈给模型，才能系统地改进事实性。本文训练了一个细粒度评价器 FenCE，它能够对生成回复中的每个声明给出事实性评分和文本批评，并基于多种工具获取的源文档进行声明级判断。随后利用 FenCE 对候选回复进行修订和打分，构建高质量训练数据并训练生成器。实验结果显示，该闭环框架能够有效提升语言模型的事实性，且批评文本提供了可解释的改进依据，为事实性增强提供了一种细粒度、可操作的新方向。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1656, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1660, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 766, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1632, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long400/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 800, \"height\": 428, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long400/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 799, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long400/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long400/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long400/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long400/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1401, \"height\": 660, \"label\": \"Table\"}]"
motivation: 语言模型输出常含事实错误，需要可操作的细粒度反馈来指导模型改进。
method: 训练批评式评价器 FenCE，对声明级事实性进行打分和文本批评，并据此构建训练数据。
result: 实验表明该框架能有效提升生成模型的事实性，并给出可解释的批评依据。
conclusion: 提供了一种数据驱动、声明级反馈的事实性增强方法，可推广到不同语言模型。
---

## Abstract
Factuality evaluation aims to detect factual errors produced by language models (LMs) and hence guide the development of more factual models. Towards this goal, we train a factuality evaluator, FenCE, that provides LM generators with claim-level factuality feedback. In particular, we train FenCE to (1) generate textual critiques along with scores and (2) make claim-level judgment based on diverse source documents obtained by various tools, via data augmentation on a combination of public judgment datasets. We then present a framework that leverages FenCE to improve the factuality of LM generators by constructing training data. Specifically, we generate a set of candidate responses, ask FenCE to revise and score each response without introducing lesser-known facts, and train the generator by preferring highly scored revised responses. Experiments show that our data augmentation methods improve the evaluator’s accuracy by 2.9% on LLM-AggreFact. With FenCE, we improve Llama2-7B-chat/Llama3-8B-chat’s factuality rate by 16.86%/14.45% on FActScore, outperforming state-of-the-art factuality finetuning methods by 8.83%/6.96%.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）在生成文本时存在严重的“幻觉”（hallucination）问题，即生成看似合理但实际错误的信息。这种错误源于模型难以区分预训练中记住的事实与其他“听起来合理”的信息，尤其在模型不熟悉的主题上表现更明显。
- **已有方法的不足**：
  - 推理期解码策略或后编辑方法会引入严重延迟，不适合实时应用。
  - 基于训练的方法（如偏好训练、事实性微调）要么受限于生成器自身能力，要么在修正错误时可能引入“鲜为人知的事实”（lesser-known facts），反而加剧幻觉。
  - 使用专有模型（如 GPT-4）受限，用生成器自评则存在自我偏置（self-bias），判断不准确。
  - 现有评价器训练数据来源单一（多为新闻或维基百科），且大多数标注仅提供离散标签，缺乏细粒度、可解释的反馈。
- **整体含义**：本文旨在训练一个开源、细粒度、基于文本批评（critique）的事实性评价器 **FenCE**，它能够对生成回复中的每个声明（claim）给出事实性评分和文本解释，并以此为依据构建高质量训练数据，最终提升生成模型的事实性。这为事实性增强提供了一条数据驱动、声明级反馈、可解释的新路径。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

**核心思想**：训练一个能够输出“评分 + 文本批评”的声明级事实性评价器 FenCE，并用它来修订、评分生成器的候选回复，构建 SFT + DPO 训练数据，从而让生成器学会只输出“高置信、易验证”的事实。

### 2.1 FenCE 评价器训练

- **输入与输出**：给定声明 c 和源文档 d，输出标签 l ∈ {Supported, Contradictory, Unverified} 以及文本批评 r。
- **标签增广（Textual Critique Augmentation）**：
  - 使用指令微调模型（Llama3-70B-chat）对每个 (claim, document) 生成 10 个候选“批评 + 标签”。
  - 仅保留预测标签与原始数据集标注一致的样本，将对应的批评作为训练目标；否则丢弃该样本。
  - 这样保证了批评与标签的一致性，并过滤掉部分噪声标注。
- **源文档增广（Tool-based Source Augmentation）**：
  - 调用三种工具获取更多样化的源文档：Bing 搜索 API（搜索引擎）、Wikipedia（知识库）、Google Knowledge Graph API（知识图谱）。
  - 让指令模型生成工具调用（如搜索查询、维基页面名、实体名），对返回结果用文本嵌入（GTR-T5-Large）按余弦相似度重排序，取 top-5 文档。
  - 若工具文档上判断出的标签与原数据集标签一致，则加入训练集；否则丢弃。直觉：若声明可被某些文档支持，工具大概率能找到其他支持性来源；若声明是幻觉，任何工具都难以找到支持证据。
- **训练目标**：最大化条件语言模型似然：

  \[
  \max_{E} \mathbb{E}_{(c,d),(r,l)\sim \mathcal{T}_{\text{Eval}}} \log P_E(r, l \mid c, d)
  \]

- **最终数据规模**：77.2% 的训练样本附带文本批评，54.1% 的样本获得工具扩展文档；人工抽样检查显示批评准确率 95.6%，工具文档标签准确率 97.8%。

### 2.2 利用 FenCE 提升生成器事实性

整体流程分三步（对每个 prompt 迭代执行）：

1. **评估（Evaluate）**：用指令模型将生成回复分解为声明；对每个声明调用工具获取证据文档，用 FenCE 给出判断（标签 + 批评）。
2. **修订（Revise）**：
   - 若声明被判定为“unverified”或“contradictory”，先判断其是否属于“鲜为人知的事实”：
     - 向生成器提问“Is this claim factual?”，若输出“unknown”则认为是少见的、模型未记住的事实。
   - 若是少见事实：从回复中删除该虚假信息。
   - 若不是少见事实（即属于常见事实但生成错误）：让生成器基于 FenCE 的批评进行修正。
3. **继续生成（Generate）**：将修订后的段落作为前缀，继续生成下一段落，迭代进行多轮以减少错误传播。

**生成器训练**：
- **SFT 阶段**：用 FenCE 对每个原始/修订回复计算事实性占比（% facts），选择 top-k 回复作为监督目标，进行标准语言模型微调。
- **DPO 阶段**：基于 SFT 模型作为参考策略，构造偏好对：
  - 对于每个 prompt，从 top-k 回复中选择 y_w（被偏好），较低得分回复作为 y_l。
  - 可生成 \( \binom{2N}{2} - \binom{2N-k}{2} \) 个偏好对。
  - 优化 DPO 损失（公式（2）），使模型倾向于生成事实性更高的回复。

## 3. 实验设计：数据集、Benchmark 与对比方法

### 3.1 评价器实验（RQ1）

- **训练数据**：多个公开人工标注事实性判断数据集，包括：
  - 摘要：XSum Hallucination、QAGS、FRANK、RAGTruth（CNN/DM）
  - 问答：RAGTruth（MSMARCO）、FActScore（WikiBio）
  - 对话：Q2、FaithDial、BEGIN、CMU-DoG
- **评估基准**：LLM-AggreFact 测试集，包含 10 个数据集（事实验证、摘要、长问答），覆盖 AGGREFACT、TOFU、EVAL、WICE、REVEAL、CLAIMVERIFY、FACTCHECK、EXPERTQA、LFQA、CNN、XSum、MediaSum、MeetB 等子集。
- **对比方法**：
  - 基线：Llama3-8B-chat、Mistral-8x7B、Llama3-70B-chat、Mistral-123B、Gemini-Pro、GPT-3.5、Claude-2.1、Claude-3 Opus、MiniCheck-FT5、GPT-4。
  - 消融：FenCE (Vanilla SFT)、FenCE (Critique Only)、FenCE (Full)。
- **指标**：平衡准确率（BAcc）。

### 3.2 生成器事实性实验（RQ2、RQ3）

- **数据**：
  - FActScore：从 unlabeled 子集中随机划分 400 个训练 prompt、100 个测试 prompt（自建划分）。
  - TruthfulQA：从 38 个类别中各选 3 个作为训练集，剩余 703 个作为测试集。
- **评价指标**：FActScore 上的 % Facts；TruthfulQA 上的 % True\*Info（真实且有信息量）。
- **基线方法**：
  - SFT（用生成器自评选择最优响应进行微调）
  - FactTune-FS（全候选 SFT + DPO，基于检索上下文打分）
  - Self-Eval-SKT（用模型自身知识自我训练评价器，构造偏好对）
  - EVER-Pref（迭代评估和修正错误信息，构建偏好数据）
- **消融实验**（均替换为 FenCE 作为评价器）：
  - SFT + FenCE（仅 SFT）
  - Edit（EVER-Pref 式修正 + FenCE）
  - Coarse（FactTune-FS 式粗粒度打分 + FenCE）
  - Edit + Coarse（修正所有错误，不区分是否 rare fact）
  - **E/R + Coarse**（完整方法：Edit/Remove + Coarse）

## 4. 资源与算力

- **论文中未明确说明**具体的 GPU 型号、数量、训练时长、显存占用等算力资源信息。
- 仅能推断使用的模型规模：FenCE 基于 Llama3-8B-chat；批评生成和声明分解使用 Llama3-70B-chat；生成器为 Llama2-7B-chat、Llama3-8B-chat；工具调用涉及 Bing API、离线 Wikipedia 副本、Google Knowledge Graph API。
- 文档离线版为 2023/04/01 版本；检索编码器为 GTR-T5-Large。研究由 Meta GenAI 与 CMU 支持，但无具体算力数据。

## 5. 实验数量与充分性

**实验组数较多，整体充分**：

- **评价器实验**：在 LLM-AggreFact 的 10 个数据集上对比 10+ 个基线模型 + 3 个消融变体，并额外做了：
  - 人工抽样 45 例（每个标签 15 例）检验批评和工具文档质量；
  - 3 个典型 case studies（批评一致性、多工具文档获取、知识图谱/百科/搜索格式多样性）。
- **生成器实验**：2 个生成器（Llama2-7B-chat、Llama3-8B-chat）× 2 个基准（FActScore、TruthfulQA）× 4 个基线 + 5 个消融，共约 18 组主要训练配置；另有：
  - 按实体流行度（very rare → very frequent）的分组分析（分布、拒绝率、% facts）；
  - 按主题（education、birthday、awards、family、nationality、organization、occupation）细分的事实性对比；
  - 超参数分析：修订迭代次数（1-6）、top-k 选择（1/3/5）。
- **客观性与公平性**：
  - 所有基线均用相同工具、相同分解模型、相同采样数（N=5）进行训练；
  - 消融逐一更换组件，区分了 Edit/Remove 和 Coarse 的各自贡献；
  - 对比时不考虑 RAG 方法（因为推理期需额外检索，不算公平比较）；不比较推理期方法（存在延迟、可正交结合），做法合理。
  - 但训练/测试 prompt 划分是作者自建（Tian et al. 未公开划分），可能导致与部分文献不可直接比较。

## 6. 论文的主要结论与发现

1. **FenCE 评价器有效性**：
   - 相比 Vanilla SFT，数据增广带来平均 +2.9% BAcc；在 8/10 数据集上一致提升。
   - FenCE 以 8B 参数超越所有开源模型（包括 Mistral-123B），并超过 Claude-3 Opus 等专有模型，接近 GPT-4 水平。
   - 批评文本和工具文档增广均有效（Critique Only 介于 Vanilla 与 Full 之间）。
2. **生成器事实性提升显著**：
   - Llama2-7B-chat 在 FActScore 上 +16.86%（38.57%→55.43%），TruthfulQA 上 +17.64%。
   - Llama3-8B-chat 在 FActScore 上 +14.45%（50.96%→65.41%），TruthfulQA 上 +8.25%。
   - 超过 SOTA 微调方法：FActScore 上领先 8.83%（Llama2）和 6.96%（Llama3）；TruthfulQA 上领先 3.99%。
3. **行为分析**：
   - 训练后模型对不熟悉实体生成更少内容、对热门实体生成更多内容，学会了“不知为不知”。
   - 对稀有实体拒绝回答的比例显著上升，而高频实体几乎不拒绝。
   - 各实体流行度分组和所有主题下事实性均有一致提升。
4. **训练策略结论**：
   - “只修正常见事实，删除少见事实”显著优于“一律修正”（Edit+Coarse），验证了避免引入 lesser-known facts 的重要性。
   - 用 FenCE 替代生成器自评可提升所有基线方法（如 SFT +3.74%）。
   - 修订迭代超过 3 次后测试性能收敛，训练数据越“完美”不一定越好。

## 7. 优点

- **细粒度、可解释**：不仅给出标签，还生成文本批评，信息量远高于单一分数，便于定位和修正错误声明。
- **数据增广设计巧妙**：利用指令模型生成批评、用多工具扩展证据源，并仅保留与原始标签一致的样本，既提高数据量又保证质量，且人工抽检准确率 >95%。
- **避免自偏置**：使用独立开源的 FenCE 作为评价器，替代生成器自评或专有模型，降低训练信号偏差。
- **规避 rare-fact 风险**：在修订阶段显式检测“鲜为人知的事实”，删除而非强行修正，从根本上缓解了以往微调方法加剧幻觉的问题。
- **推理零开销**：训练后模型在推理时与普通模型完全一致，无额外延迟。
- **实验分析细致**：对实体流行度、主题、修订轮数、top-k 等均做了系统分析，结论稳健且可解释性强。
- **可扩展性**：训练只需大量 prompts，无需标注数据，易于扩展到任意领域。

## 8. 不足与局限

- **算力信息缺失**：未报告 GPU 数量、训练天数、能耗等，不利于复现成本评估。
- **评价器训练数据覆盖有限**：
  - 仅基于人工标注的模型回复判断数据集，未纳入合成数据或人工撰写声明数据集；
  - 未覆盖数学推理、编程等也被视为“事实性”的任务；
  - 工具类型仍限于三种（搜索、知识库、知识图谱），未涵盖其他知识来源。
- **生成器实验领域较窄**：
  - 主要使用 FActScore（传记生成）和 TruthfulQA，任务类型相对有限；
  - 未在开放式问答、摘要、对话等更广泛场景验证训练配方；
  - 训练/测试划分由作者自行生成并公开，但与部分文献划分不统一，跨论文直接比较需谨慎。
- **依赖外部工具与指令模型**：
  - 数据构建阶段依赖 Llama3-70B-chat 做声明分解、查询生成、批判筛选，其自身偏见可能传递到评价器；
  - 工具调用（搜索、百科、知识图谱）可能失败或返回未覆盖信息，对判断质量有影响。
- **自偏置未完全消除**：虽然评价器独立，但“是否为 lesser-known fact”的判定仍依赖生成器自身输出（“unknown”），可能出现误判。
- **理论与泛化性**：对“模型如何学习只输出已记忆事实”缺乏机制性解释，结论主要基于统计观察。
- **未与 RAG 方法对比**：作者说明不公平而未对比，但这也意味着无法判断本方法相对检索增强方法的优劣；且本方法可视为“无检索时的替代方案”，边界明确。

**（完）**
