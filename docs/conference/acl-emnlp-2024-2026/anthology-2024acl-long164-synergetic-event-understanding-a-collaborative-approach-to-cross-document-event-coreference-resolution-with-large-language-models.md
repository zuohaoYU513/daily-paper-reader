---
title: "Synergetic Event Understanding: A Collaborative Approach to Cross-Document Event Coreference Resolution with Large Language Models"
title_zh: 协同事件理解：基于大语言模型的跨文档事件共指消解协作方法
authors: "Qingkai Min, Qipeng Guo, Xiangkun Hu, Songfang Huang, Zheng Zhang, Yue Zhang"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.164.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 面向跨文档事件共指消解提出LLM协作式方法，协同处理事件提及聚类
tldr: 跨文档事件共指消解需要把不同文档中指向同一真实世界事件的事件提及聚合起来。微调BERT等小模型容易学习上下文共现等浅层线索，而ChatGPT等大模型虽上下文理解能力强，却很难直接适配细粒度事件抽取任务。本文提出一种协同式方法，让LLM与任务知识或小型模型协作完成跨文档事件共指簇判别，在复杂语境与任务定向之间取得平衡。该协同策略为用LLM处理特定信息抽取任务提供了新思路。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 758, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 648, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 647, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1617, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1629, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long164/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 707, \"height\": 539, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 554, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 1259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 684, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1640, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 521, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 681, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 728, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 593, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1643, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1614, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 808, \"height\": 132, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 807, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1659, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1637, \"height\": 716, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long164/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1645, \"height\": 396, \"label\": \"Table\"}]"
motivation: 跨文档事件共指消解中，小模型受多样上下文干扰易学共现，LLM又难以单独适配特定事件抽取任务。
method: 提出LLM协同式框架，结合大模型对复杂语境的语义理解和具体事件共指任务约束，实现跨文档事件共指聚类。
result: 协同框架可缓解小模型过拟合共现和大模型任务适配性不足的问题，提升跨文档事件共指判别的可靠性。
conclusion: 展示了LLM与任务知识协作处理跨文档事件共指的可行性，推进大模型在事件抽取场景中的实用化。
---

## Abstract
Cross-document event coreference resolution (CDECR) involves clustering event mentions across multiple documents that refer to the same real-world events. Existing approaches utilize fine-tuning of small language models (SLMs) like BERT to address the compatibility among the contexts of event mentions. However, due to the complexity and diversity of contexts, these models are prone to learning simple co-occurrences. Recently, large language models (LLMs) like ChatGPT have demonstrated impressive contextual understanding, yet they encounter challenges in adapting to specific information extraction (IE) tasks. In this paper, we propose a collaborative approach for CDECR, leveraging the capabilities of both a universally capable LLM and a task-specific SLM. The collaborative strategy begins with the LLM accurately and comprehensively summarizing events through prompting. Then, the SLM refines its learning of event representations based on these insights during fine-tuning. Experimental results demonstrate that our approach surpasses the performance of both the large and small language models individually, forming a complementary advantage. Across various datasets, our approach achieves state-of-the-art performance, underscoring its effectiveness in diverse scenarios.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究任务**：跨文档事件共指消解（Cross-Document Event Coreference Resolution, CDECR），即把分散在不同文档中指向同一真实世界事件的提及（event mention）自动聚类。
- **核心难点**：
  - **挑战1**：不同文档中描述的不同事件可能在外观和语境上非常相似（尤其同类事件），模型容易把它们误判为同一事件；
  - **挑战2**：同一事件在不同文档中的表述方式可能差异很大，模型难以识别它们之间的共指关系。
- **现有方法的不足**：
  - 小语言模型（SLM，如 BERT/RoBERTa）通过微调学习事件表示，但面对复杂多样的上下文时，容易学习“简单共现”等伪特征，而非真正与共指相关的深层证据；
  - 大语言模型（LLM，如 GPT-4）虽具备强大的上下文理解能力，但在信息抽取等任务上难以仅靠提示（或少量示例）达到监督式 SLM 的精度，尤其 CDECR 涉及超长多文档输入与结构复杂输出，直接预测性能很差。
- **论文的核心主张**：LLM 与 SLM 的能力具有互补性——LLM 擅长通用语义理解与信息提炼，SLM 擅长通过充分微调适配特定任务结构。两者协作可实现“协同事件理解”，同时缓解两种模型的各自短板。

## 2. 论文提出的方法论：核心思想、关键技术细节与流程

### 2.1 总体框架

- 提出 **SECURE**（Synergetic Event Understanding）协作式框架，结构为：
  - **LLM 做通用任务**：对每个事件提及所在的上下文进行“总结/阐述”，生成有助于区分与识别事件的浓缩信息；
  - **SLM 做特定任务**：将 LLM 生成的总结与原始文档拼接，通过联合表示学习微调 SLM，完成候选检索与成对分类，最终形成共指聚类。

### 2.2 LLM 总结：两步式通用提示工作流

- **设计原则**：不使用任务特定的 in-context learning 或微调，仅让 LLM 完成“通用任务”，避免被复杂标注规范束缚，同时防止语义偏移。
- **第一步——事件阐述**：
  - 输入：整篇文档 + 事件提及所在句子；
  - 指令：让 LLM “elaborate” 该事件提及，自动从文档中挑选与事件相关的细节（上下文词、实体、其他事件等）；
  - 采用“elaborate”而非“summarize”，强调基于提及自身概念的解释性行为，减少模板偏差。
  - 附带一个预处理：先做依存句法分析，再让 LLM 基于分析结果阐述，以提升准确性。
- **第二步——实体细节扩展与时间推理**：
  - 输入：第一步生成的阐述结果；
  - 指令：利用文档内的实体共指解析，进一步补充第一步中实体对象的细节；要求依据新闻发表日期进行时间推断/补充；
  - 目的：解决事件关键实体信息分散在文档各处的问题。
- **格式控制**：要求输出中保留与原始文档一致的提及短语 span，降低生成难度，并便于 SLM 对齐原始语境与总结。

### 2.3 SLM 集成：联合表示学习

- 采用 Held et al. (2021) 的两模块基线：候选检索 + 成对分类，均基于 RoBERTa LARGE 编码器。
- 对每个提及 \(m_{ij}\)，将其原始文档 \(D_i\) 与对应 LLM 总结 \(S_{ij}\) 拼接成新文档 \(D'_i\)，编码后得到两个向量表示：
  - \(h_{ij}\)（原始上下文中的提及向量）
  - \(h^{(s)}_{ij}\)（总结中的提及向量）
- 将二者拼接为融合表示：
  \[
  h'_{ij} = \text{concat}(h_{ij}, h^{(s)}_{ij})
  \]
  该向量可直接替换原基线中的表示，输入后续分类/聚类模块。
- 通过同一注意力空间内联合编码原始语境与总结，使 SLM 能相互学习、聚焦于真正与共指判断相关的信息。

### 2.4 与直接使用 LLM 预测结构的关系

- 论文同时测试了 GPT-4 直接进行 CDECR 结构预测（few-shot / zero-shot）的能力，但因其上下文长度限制、任务复杂度等原因，效果远低于协作式方法，作为对照存在的“下界”，用于佐证协作框架的有效性。

## 3. 实验设计

### 3.1 数据集与基准

- 使用三个公开 CDECR 数据集：
  - **ECB+**（Event Coreference Bank Plus）：多主题新闻语料，含类似子主题（如同为“6.1级地震”的不同事件），用于考验模型区分相似事件；
  - **GVC**（Gun Violence Corpus）：单一主题（枪击暴力事件），含多个子事件；
  - **FCC**（Football Coreference Corpus）：单一主题（足球赛事），文档长、事件连续性强、上下文相似度高。
- 统计规模：ECB+ 982 篇文档 / 6833 个提及；GVC 510 篇 / 7298 个提及；FCC 451 篇 / 3563 个提及。
- **评估指标**：MUC、B\(^3\)、CEAF\(_e\)、CoNLL F1（前三者平均）、LEA；分析时主要采用 B\(^3\) F1。

### 3.2 对比方法

- 传统与神经基线：Barhom et al. (2019)、Cattan et al. (2020)、Bugert et al. (2021)、Caciularu et al. (2021)、Held et al. (2021)、Hsu and Horwood (2022)、Yu et al. (2022)、Ahmed et al. (2023)、Chen et al. (2023)。
- 直接使用 GPT-4（采用不同 in-context learning 设置）作为对照。
- 复现的 baseline（基于 Held et al. 2021，更新超参数）。
- 自建消融变体（见下）。

### 3.3 实现细节

- LLM 使用 **GPT-4-0613**（总结）与 **GPT-4-Turbo-Preview**（直接预测结构），temperature=0；
- SLM 使用 RoBERTa LARGE 微调；三个数据集共用一套超参数（候选检索：lr=1e-5, batch=16, epochs=50；成对分类：lr=6e-6, batch=16, epochs=20，含 early stopping）；
- 每组实验独立运行 3 次取均值。

## 4. 资源与算力

- 论文**未明确报告**使用的 GPU 型号、数量、训练时长或总体计算量。
- 仅能推断：
  - SLM 微调基于 RoBERTa LARGE，训练规模不大；
  - LLM 调用依赖 OpenAI API（GPT-4-0613 / GPT-4-Turbo-Preview），并报告了 token 消耗：在 ECB+ 测试集上，LLM 总结流程消耗输入约 658k 以上 tokens、输出 213k 以上 tokens，API 调用次数超过 400 次；而直接提示 GPT-4 预测结构仅需约 166k 输入/25k 输出 tokens、10 次调用。
- 说明：论文对算力/资源使用的披露不足，难以复现其完整计算成本。

## 5. 实验数量与充分性

### 5.1 主要实验

- 在 **3 个数据集**（ECB+、GVC、FCC）上与 **10+ 种方法**进行对比，报告了多种指标，并给出 3 次独立运行的平均结果与显著性检验（p < 0.01）。
- 额外进行了“不含 singleton”的评估（ECB+）、API 效率统计等补充实验（见附录）。

### 5.2 消融与分析实验

- **LLM 总结 vs. LLM 改写**（paraphrase）：用于验证提升来自信息筛选而非单纯增加文本多样性；
- **两步骤工作流消融**：分别检验 Step 1 与 Step 2 的贡献，并考察两步合并成一步时的性能损失；
- **错误类型分析**：将链接错误划分为 FPA（同类型但参数不同导致的假阳性）、FPT（事件类型不同导致的假阳性）、FN（漏报），对比不同方法在各错误类型上的数量变化；
- **GPT-4 直接预测深入分析**：对比 few-shot/zero-shot、不同上下文范围（全上下文 vs. 仅含提及的句子）、不同演示数量对性能的影响；
- **长度分析**：统计每一步生成摘要的长短与相对原始文档的比例。

### 5.3 充分性与公平性评价

- **优点**：实验覆盖面广，数据集差异化明显（多主题 vs. 单主题；短文档 vs. 长文档），错误类型分析具体，消融设计能清晰分离各组件贡献，且对 GPT-4 的失败模式进行了剖析，有助于验证“LLM 总结 + SLM 微调”这一设计逻辑。
- **不足**：
  - 表 2 中部分基线的 F1 复现结果与原文不一致（作者说明可能归因于随机性），但削弱了对照的绝对公平性；
  - 对 Ahmed et al. (2023) 排除了其 oracle 设置下的结果，存在选择性比较的争议；
  - 关于 GPT-4 的评估受输入长度限制，不得不截断或按主题拆分，导致其性能被低估，不能完全反映 LLM 上限；
  - 每次实验仅 3 次重复，数量略少，在消融中未报告方差。

## 6. 论文的主要结论与发现

- **协作式方法全面优于单模型**：在 ECB+、GVC、FCC 上分别比复现 baseline 提升 CoNLL F1 约 1.5%、2.7%、7.0%，均达到新的 state-of-the-art。
- **LLM 总结的价值在于“提炼可区分信息”**：最显著减少的错误是 FPA（错误地把相似但不同的事件当作同一事件），说明总结能帮助 SLM 区分“表现相似但实为不同事件”的语境；文中以两则相似“6.1级地震”报道为例，总结能提取日期、地点等关键区分信息。
- **两步式总结的作用不同**：
  - Step 1 主要减少 FPA 错误；
  - Step 2（实体信息扩展+时间推理）主要减少 FN 错误（漏报），两者不可或缺；
  - 将两步合并成一步会导致性能下降，说明分解复杂任务很重要。
- **LLM 直接预测 CDECR 结构不可行**：GPT-4 即使采用最优的 few-shot + 仅含提及句子的上下文设置，也只有约 77.2 B\(^3\) F1（ECB+），显著低于协作式方法（87.8）；增加演示数量收益有限，而使用完整上下文反而使性能下降，暴露其对长上下文的利用能力不足。
- **适用场景**：对于文档内部信息充分的相似事件区分（挑战1）提升显著；对同一事件表述差异极大或原始上下文信息过少（挑战2）帮助有限，需要额外数据或外部信息检索。

## 7. 优点

- **任务分解巧妙**：让 LLM 只做“事件阐述/实体补全”等通用任务，发挥其强语义理解能力，又避免其与复杂标注规范直接对抗；SLM 则用微调处理结构化分类，实现“1+1>2”的互补效果。
- **提示设计具有通用性与低偏差性**：不依赖特定事件类型模板，可扩展到任意事件类型（ECB+ 有 400+ 事件类型），实际应用潜力大。
- **强调“faithfulness”的总结准则**：禁止 LLM 自行补全文档中不存在的信息，减少幻觉导致的语义漂移。
- **对比实验设计较严谨**：既有 SLM 重建基线，又包含“LLM 改写”对照，证明收益来自信息筛选而非文本多样性；错误类型统计支持分析结论。
- **性能提升幅度大且稳定**：尤其在中长文档、事件相似度极高的 FCC 数据集上提升 7% CoNLL F1，说明方法针对核心难点有效。

## 8. 不足与局限

- **算力与资源披露不足**：无 GPU 数量/型号/训练时长信息，LLM API 成本仅部分列出（token/次数），难以为他人复现或估算总体开销提供依据。
- **对 LLM 的选择单一**：仅验证 GPT-4-0613，未评估开源 LLM（如 LLaMA、Mistral 等）或不同规模的 LLM 下的稳健性。
- **复现基线的公平性问题**：部分基线结果与其原始论文存在差异；在排除 oracle 结果或调整超参数后的对比可能不够完全客观。
- **直接对比 GPT-4 的方式受长度限制干扰**：由于输入/输出长度限制，GVC 和 FCC 上 GPT-4 只能截断输入，导致其出现接近 0 的异常分数；这使得“LLM 不如协作方法”的结论带有一定的“不公平性”，论文虽在附录中说明，但主表呈现方式可能引发误读。
- **长上下文仍构成瓶颈**：协作式方法需要对每个文档中所有提及调用 LLM 总结，当文档或提及数量大增时，API 调用成本与 token 消耗会线性甚至超线性上升，且 FCC/GVC 这类单主题超长语料的处理对直接评估不友好。
- **对“信息不足型”FN 问题改善有限**：若文档本身不含足够事件细节（如用户主观描述而无地点时间），仅靠忠实总结无法补足缺失证据，论文自身也承认这是未来需结合外部知识检索的方向。
- **潜在偏差风险**：
  - 采用 LLM 生成的总结作为训练信号，若 LLM 偶发错误或幻觉（即使要求忠实），可能向 SLM 注入系统性噪声；
  - 使用 OpenAI API 在测试期间模型版本变化，可能影响实验可重复性——论文提到部分实验已从 GPT-4-0613 迁移至 GPT-4-turbo-preview，但并未全部重新执行，存在版本不匹配的干扰。

---

（完）
