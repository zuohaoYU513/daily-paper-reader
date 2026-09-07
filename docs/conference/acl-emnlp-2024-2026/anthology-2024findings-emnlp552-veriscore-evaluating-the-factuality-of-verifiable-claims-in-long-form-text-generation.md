---
title: "VeriScore: Evaluating the factuality of verifiable claims in long-form text generation"
title_zh: VeriScore：评估长文本生成中可验证主张的事实性
authors: "Yixiao Song, Yekyung Kim, Mohit Iyyer"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.552.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 提出VERISCORE指标以评估长文本生成中可验证主张的事实性
tldr: FActScore、SAFE等事实性指标假定每条被分解出的原子主张都可被维基百科等知识源验证，因而不适合包含不可验证内容的长文本生成。针对该问题，作者提出VERISCORE：它只对文本中可验证的主张进行事实性评分，并兼容闭源与微调开源语言模型实现。人工评估显示VERISCORE抽取的主张更合理，能更好地刻画真实长文本生成任务中的事实性。该指标是对既有一次性事实性评测的重要补充。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1618, \"height\": 625, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 615, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1598, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp552/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 755, \"height\": 489, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 639, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 740, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 712, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1343, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1668, \"height\": 1819, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1667, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 779, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1665, \"height\": 1456, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 801, \"height\": 876, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1668, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp552/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1664, \"height\": 450, \"label\": \"Table\"}]"
motivation: 现有长文本事实性指标假定所有原子主张可验证，不适合包含不可验证内容的生成任务。
method: 引入VERISCORE，对可验证主张而非全部内容进行事实性评分，可基于闭源或微调开源模型实现。
result: 人工评估显示VERISCORE抽取的主张更合理，并在混合可验证与不可验证内容上优于现有指标。
conclusion: 长文本事实评测应将可验证与不可验证内容分开处理，避免指标误用。
---

## Abstract
Existing metrics for evaluating the factuality of long-form text, such as FACTSCORE (Min et al., 2023) and SAFE (Wei et al., 2024), decompose an input text into “atomic claims” and verify each against a knowledge base like Wikipedia. These metrics are not suitable for most generation tasks because they assume that every claim is verifiable (i.e., can plausibly be proven true or false). We address this issue with VERISCORE,1 a metric for evaluating factuality in diverse long-form generation tasks that contain both verifiable and unverifiable content. VERISCORE can be effectively implemented with either closed or fine-tuned open-weight language models. Human evaluation confirms that VERISCORE’s extracted claims are more sensible than those from competing methods across eight different long-form tasks. We use VERISCORE to evaluate generations from 16 different models across multiple long-form tasks and find that while GPT-4o is the best-performing model overall, open-weight models such as Mixtral-8×22 are closing the gap. We show that an LM’s VERISCORE on one task (e.g., biography generation) does not necessarily correlate to its VERISCORE on a different task (e.g., long-form QA), highlighting the need for expanding factuality evaluation across tasks with varying fact density.

---

## 论文详细总结（自动生成）

# 论文总结：V ERI SCORE（VeriScore）

## 1. 核心问题与研究动机

- 现有长文本事实性评估指标（如 FActScore 和 SAFE）均采用同一思路：将文本分解为“原子主张”，再逐一与维基百科或搜索引擎结果比对验证。
- 这种思路隐含一个不现实的假设：**输入文本中的所有内容都可以分解为可验证的原子主张**。但在真实的长文本生成任务（如长问答、解释性回答、创意写作、“傻瓜模式解答”等）中，输出往往混有：
  - **不可验证内容**：个人经验、主观感受、虚构比喻、假设、建议等；
  - **复杂断言**：不能简单“原子化”而不丢失语境的长论述；
  - **代词/指代不清、上下文依赖型语句**。
- 因此，FActScore 与 SAFE 会错误地将不可验证内容也当作事实来抽取和验证，导致误差和不公平的模型惩罚。
- 本文提出 **VERI SCORE**：一个专门针对“可验证主张”进行事实性评估的指标，适用于**同时包含可验证与不可验证内容**的多样化长文本生成场景。

## 2. 方法论：核心思想与技术细节

### 2.1 核心思想

- 只对**可验证主张**（verifiable claims）打分，忽略主观、虚构、假设等不可验证内容。
- 主张定义基于语言学语义框架：描述**单一事件或单一状态**，并包含必要的时地修饰，能够被可靠外部信源支持/反驳。
- 解决了 FActScore 和 SAFE 的三类缺陷：
  1. 代词/指代解决：FActScore 不解决代词；VeriScore 通过前文上下文解析；
  2. 不抽取不可验证内容：SAFE 会抽取“甜菜碱就像超级英雄斗篷”这种文本；
  3. 去掉高成本的“主张修改 + 相关性检查”步骤。

### 2.2 流程

整体流程分三步：

1. **主张抽取（claim extraction）**
   - 使用 few-shot prompting，模型逐句对响应进行分解；
   - 采用**滑动窗口**：当前句前后各取 0–3 和 0–1 句作为上下文；
   - QA 任务将问题前置，长段落将段落首句前置，以便解决指代歧义；
   - 输出为自包含、无代词、只含可验证内容的“细粒度事实”列表。

2. **证据检索（evidence retrieval）**
   - 直接用抽取出的主张作为搜索引擎查询词；
   - 通过 Serper API 调用 Google Search，取前 n≤10 条结果的标题、摘要和链接作为证据。

3. **主张验证（claim verification）**
   - 用 LLM 对每个主张判定四大类：支持（supported）、反驳（contradicted）、无法判定（inconclusive-a：部分无证据）和相互矛盾（inconclusive-b：不同证据支持与反驳并存）。
   - 形式化定义：如果主张所有部分均被证据支持且无矛盾则支持；只要有部分被反驳则反驳；若某部分既无支持亦无反证则 inconclusive-(a) 等。

4. **分数计算**
   - 采用 SAFE 的 **F1@K** 指标，同时贴近事实精度（P）与事实召回（R）。
   - 对每个数据集，K 取所有模型响应中抽取的事实数的中位数；
   - 公式：S(r)=被支持主张数；P=S/|C|；R=min(S/K, 1)；F1@K = 2PR/(P+R)，若 S=0 则 F1=0。

### 2.3 实现方式

- 初期用闭源 LLM（GPT-4 与 Claude 3）few-shot 实现；
- 随后用 GPT-4/GPT-4o 生成数据，微调开源模型（Llama3-8B-Instruct 与 Mistral-7B-Instruct-v0.2），形成**便宜、开源可复现**的流水线。

## 3. 实验设计：数据集、场景与对比方法

### 3.1 数据集 / 场景（共 8 个领域）

| 数据集 | 性质 | 用途 |
|---|---|---|
| Biography | 人物生成长文本（fact-dense） | HE / Dev |
| ELI5 | 面向外行的开放式解释 | HE / Dev |
| AskHistorians | 历史问答 | HE / Dev |
| ShareGPT | 开放指令对话 | HE / Dev |
| WritingPrompts | 创意故事（虚构）写作 | HE / Dev |
| FreshQA | 动态知识问答（回答可随世界变化） | Dev |
| FreshBooks | 2023–2024 年出版物段落续写（本文构建） | Dev |
| Scruples / CommonCrawl / wikitext-103 | 主观判断/通用网络文本/百科 | 仅 HE 抽取评估部分 |

- 其中前四项用于查验抽取质量；“Dev”用于开发、验证与构建微调训练数据。
- VerRatio 数值（每句可验证主张数）在事实密集域如 FreshBooks（2.31）与事实稀疏域如 WritingPrompts（0.03）差异很大，证明了抽取器能有效区分两类内容。

### 3.2 评估的模型

- 16 个模型：GPT-3.5-turbo（两个版本）、GPT-4-0125-preview、GPT-4o、Claude-3-Haiku/Sonnet/Opus、Mistral-7B-Instruct-v0.1/v0.2、Mixtral-8x7B、Mixtral-8x22B、OLMo-7B、DBRX-Instruct（132B）、Qwen1.5-1.8B、Gemma-2B、Vicuna-7B。
- 生成时采用默认超参数，最大 token 长度为 1024，每域 50 条提示。

### 3.3 对比方法与基准

- 主张抽取：**VeriScore（GPT-4/Claude 3） vs. SAFE 抽取+修改流程**，由人类评估配对偏好。
- 主张验证：**Mixtral-8×22B、Claude-3-Opus、GPT-4、GPT-4o** 在 320 条人工标注验证数据上的表现。
- 最终基准：6 个长文本事实追寻数据集 + FreshQA 与 WritingPrompts 的独立报告，跨模型做排序与相关性分析。

## 4. 资源与算力

- 原文没有完整交代 GPU 型号、数量及总训练时长等细节。
- 提到观测性数据：
  - 闭源模型跑 400 条 GPT-4o 生成数据的 few-shot 评估耗资约 **$1,038**；
  - SAFE 的修改/相关性检查步骤处理 100 条主张约花费 **35 分钟**和 **$1.7** 的 API 成本；
  - 微调基于 **LoRA** 与 Unsloth 进行，以降低显存和时间开销，但未给出具体轮数/卡时（只写了抽取与验证模型各自训练数个 epoch）；
  - 在单张 RTX8000 上，未并行抽取 400 条 GPT-4o 回答中的主张约需 **4 小时**，验证约 10k 条主张约需 **2 小时**。
- 人工标注部分支付标注者 18 美元/小时，按小时计酬。

## 5. 实验数量与充分性

- **主张抽取人工评估**：8 个领域各 15 个样本，3 位标注者共 360 条判读；标注者两两一致性高（Fleiss κ=0.766），且 120 个样本中有 99 个三位标注者完全一致。
- **主张验证人工研究**：320 条提取的 claims 配 google 检索证据；其中 50 条做三方一致性检验（82% 一致，Fleiss κ=0.7316），另 270 条分配至三人分头标注（90×3）。
- **微调数据**：抽取数据约 99,592 个输入输出对（其中一类多数为“无可验证主张”响应被 50% 随机抽样）；验证数据从 GPT-4o 生成并采样 13,403 份；训练/验证/测试划分合理。
- **大规模评测**：16 个模型 × 8 个数据集 × 50 样本 = 每个模型的评分来自 400 条生成；除主指标外还拆分了精度、召回和响应长度。
- **消融与分析**：验证器二分类/三分类对比；对不同检索位置的信息量（前 5 条>后 5 条）做了检测；增量加入了无人标注的 FreshBooks 与 WritingPrompts 作为“非公式化”领域，覆盖面非常广。
- 结论的客观性与公平性：实验设计的人为偏好测试、三标注者一致性、对闭源与开源模型分别验证，可控性好；但未报告全部模型的响应温度下置信区间，且模型使用的提示策略不完全统一（仅保证默认 system 设置），存在一定可变性。

## 6. 主要结论与发现

- **人类验证确认**：VeriScore 抽取的主张比 SAFE 在 8 个任务中更合理，用户偏好度中 VeriScore 的胜率压倒性（360 项中 SAFE 仅被偏好 26 次，且其中 19 次为“勉强偏好”），即使是 biography 任务亦如此。
- **验证任务**：GPT-4o 是最接近人类性能的自动验证器（在支持/不支持类别上都高：总 F1=0.841）。
- **最终评测**：
  - 总体而言 GPT-4o 是最好的模型；开源模型中 **Mixtral-8×22B-Instruct** 最强，在部分领域与闭源接近。
  - 模型规模与性能明显相关（小模型如 Gemma-2b 在几乎所有数据集上都最差）。
  - **不同任务上的事实性排名相关性不高**：如 LongFact 与 ELI5 在上位相关性较弱，表明模型在不同任务上具有不同的事实性能力，单一领域评估不足以综合排名。
- **复杂主张难以验证**：
  - 非实体中心的长文断言（如“旅行者和十字军在中世纪依赖基础设施……”)无法简单拆分，导致大量主张被判为“inconclusive”；
  - 开放领域验证不能仅靠关键词/语义匹配，有些主张的证明需要专业推理和长链条证据，超出 Google 摘要能提供的范围，因此可能“无支撑”而非真正幻觉。

## 7. 优点与亮点

- **真正解决了可验证性与不可验证内容混存**的现实问题，使指标可用于更多非传记型长文本生成任务（解释性、历史问答、书籍续写等）。
- 对**指代处理**提出可行的滑动窗口抽取机制，省去 SAFE 昂贵且易错的“修改+相关性检查”循环。
- 提供了**闭源与开源**两条可用实现路径，大幅降低待测方使用成本，便于社区复用。
- 多研究者/多标注者的人工研究相当扎实，报告了弗莱斯 κ、分歧来源与错误例，为下游使用给出指导。
- 将评测范围扩展到 6+2 个领域，用 Kendall’s τ 展示了跨域相关性不高的发现，指出多任务评测的必要性。
- 形式化定义了支持/冲突/无法判定的四个正交类别（含“部分支持/部分反对”的特殊情况），促使判断更加精细。

## 8. 不足与局限

- **可验证主张缺乏严格形式定义**：仍属于工作定义而非可计算定义；例如“Chuck Norris 的夺冠固化了其大师声誉”到底是一个状态还是多个事实，容易有主观分歧。
- **长串联型主张很难可靠评估**：许多长句可拆分出较短的子命题，但验证这些子命题并不等于验证原句（如“固化”这类语义派生关系），造成大量“inconclusive”结果，降低指标的可区分性。
- **检索依赖 Google 摘要**：前 5 条结果较有用，第 10 条效用骤降；复杂主张可能根本无直接匹配语境，把“缺乏证据”与“实质幻觉”混淆。
- **速度与成本偏高**：滑动窗口方式解码缓慢（单卡 RTX 8000 上 400 条响应约 4 小时），跨域大规模评测仍需要较大资源，未公布优化的并行化方案。
- **无法判断主张与问题的相关性**：指标能检验生成是否“支持”某事实，但不能判断该事实是否偏离了用户的提问意图（后续可由 Chiang & Lee 的工作扩展）。
- **只对部分模型做了系统超参搜索**：开源模型微调采用固定 epoch/LoRA 配置，可找到更优的可能参数但没有进行大范围探索。
- **模型响应长度影响 F1@K**：对本身就应简短回答的提示（如 FreshQA），生成更长但更全面的模型占据优势，对简洁的准确回答不公平；引入 K 中位数只部分缓解。
- **创意写作等极端非事实内容**：虽然主实验表明这些数据大部分主张是“不可验证”的，但少量不可验证主张仍可能混入评分中（作者说明此场景在系统目的中非主要关注，视作次要限制）。

总的来说，VERI SCORE 在衡量“可验证性”方面做出了重要且实用的修正，并在多种真实长文本生成任务上得到人工验证支持，但其在复杂主张的验证精确度上仍留有较大改进空间。

（完）
