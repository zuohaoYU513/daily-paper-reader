---
title: "CiteGuard: Conformal False-Discovery Control for Faithful Retrieval-Augmented Generation"
title_zh: CiteGuard：面向忠实检索增强生成的共形错误发现率控制
authors: Xiangyu Jiang
date: 2026-04-30
pdf: "https://openreview.net/pdf/bb606a1bc395e469f66ab6a1244f470598274f71.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 面向证据约束生成的解码层，识别无支持声明并选择保留或弃答以保证忠实性
tldr: 为解决检索增强生成即使检索质量高仍会生成无证据支持内容的问题，论文提出CiteGuard解码层，把句子级事实性建模为多重检验问题，用共形校准将声明-证据得分转化为p值，并通过错误发现率控制程序决定哪些声明可以保留并附带引用、哪些应弃答。在事实核查与问答基准上，该方法降低了被接受声明中的错误发现率，为检索增强生成的事实可靠性提供了统计保证。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 检索增强生成即使拥有强检索器，生成的句子仍可能缺乏证据支持，引用也未必反映真实出处，需要更可控的事实性保障。
method: 将句子事实性视作多重假设检验，采用共形校准与错误发现率控制把声明-证据得分转化为p值，并依据相应统计程序做保留或弃答决策。
result: 在事实核查与问答基准上，被接受声明中的错误发现率得到显著降低。
conclusion: 以统计控制方式决定哪些声明可带引用输出，能够有效提高证据约束生成中的忠实度与引用可靠性。
---

## Abstract
Large language models increasingly rely on retrieval-augmented generation (RAG) to ground responses in external corpora. Yet, even with strong retrievers, generated statements can remain unsupported, and the resulting citations are often not reliable indicators of evidence. We introduce CiteGuard, a RAG decoding layer that treats sentence-level factuality as a multiple-testing problem and combines conformal calibration with false-discovery-rate control. CiteGuard converts claim–evidence scores into p-values for the null hypothesis "unsupported" and uses BH/BY procedures to decide which claims to keep (with citations) and which to abstain on. On FEVER and Natural Questions, CiteGuard reduces the false-discovery rate among accepted claims from 28–31% (vanilla RAG) to below 10% at α=0.10, while retaining 86–92% of supported claims. This yields a user-controlled risk budget: practitioners can trade off faithfulness and coverage via α, with finite-sample guarantees under standard exchangeability assumptions.

---

## 论文详细总结（自动生成）

以下总结基于提供的论文元数据及摘要，原文 PDF 因访问限制未能取得完整内容，故部分细节（如具体算力、算法公式、详细实验设置）依据可得信息与合理推断进行说明。

# 《CiteGuard：面向忠实检索增强生成的共形错误发现率控制》中文总结

## 1. 核心问题与研究背景
- 大规模语言模型（LLM）越来越多地依赖检索增强生成（RAG）来把答案“锚定”到外部语料上，以缓解幻觉、提高可解释性。
- 然而，即使检索器非常强、检索内容高度相关，生成器仍可能输出**缺乏证据支持的句子**，而且模型给出的引用也常常**无法真实对应到支撑证据**。
- 因此，论文关注的核心问题是：能否在生成时对“每个句子是否被检索证据所支持”进行**有统计保证的判定**，从而只保留有可靠证据支撑的内容，并附上可信引用？
- 整体研究含义在于：将 RAG 的忠实性（faithfulness）从“启发式过滤”提升为“可控制错误风险”的统计推断问题，使系统在用户设定的风险预算下运行。

## 2. 方法论
### 2.1 核心思想
- 论文提出一个 RAG 解码层 —— **CiteGuard**。
- 它把“句子级事实性”看作一个**多重假设检验（multiple testing）**问题：
  - 对每个生成的句子，原假设 H₀ 为“该声明无证据支持”；
  - 备择假设为“该声明有证据支持”。
- CiteGuard 的目标是：在控制**被接受声明中“无支持”比例**（即错误发现率，FDR）的前提下，尽可能多地保留“有支持”的声明。

### 2.2 关键技术细节
1. **声明-证据打分**：
   - 使用某种打分函数衡量每条生成声明与其检索证据之间的支持程度。
2. **共形校准转 p 值**：
   - 将“声明-证据”原始得分通过共形校准（conformal calibration）转换为 p 值，使得在标准可交换性假设下 p 值具有有效的、有限样本的统计意义。
3. **FDR 控制程序**：
   - 采用 Benjamini-Hochberg（BH）或 Benjamini-Yekutieli（BY）等经典 FDR 控制方法，对句子进行多重比较校正。
4. **保留 / 弃答决策**：
   - 若某一句话对应的 p 值足够显著，则判定该句子“有证据支持”，允许输出并附带引用；
   - 若不能通过检验，则对该句子选择弃答（abstain），避免输出无根据的内容。
5. **风险预算机制**：
   - 用户通过调节显著性水平 α 控制风险：α 越小，输出越保守，FDR 越低但覆盖率可能下降；α 越大，输出越多但错误率风险升高。

> 可以粗略理解为一个带“统计质检”的生成流程：先让生成器输出候选句子，再由 CiteGuard 进行证据检验，只有“检验合格”的句子才最终交付。

## 3. 实验设计与评估场景
- **数据集 / 基准场景**：
  - FEVER：经典事实验证（fact verification）基准；
  - Natural Questions：开放域问答（QA）基准。
- **对比基线**：
  - 主要与 vanilla RAG（不经过 CiteGuard 的原始检索增强生成）进行对比。
- **主要指标**：
  - 被接受声明（accepted claims）中的错误发现率（FDR）；
  - 被保留的有支持声明的覆盖率/召回率。
- **报告结果**：
  - α=0.10 时，FDR 从 vanilla RAG 的 28%–31% 降至 **10% 以下**；
  - 同时仍保留了 **86%–92%** 的受支持声明。

## 4. 资源与算力
- 在提供的摘要和元数据中，**没有说明**使用的 GPU 型号、数量、训练时间或推理成本。
- 由于 CiteGuard 是“解码层”方法，可能在冻结的生成模型上做**后处理式的句子级判断**，其训练/推理成本大概率较低。
- 但以上只是推断，论文原文是否报告更详细的算力开销，需在完整 PDF 中核实。

## 5. 实验数量与充分性评价
- 从现有信息看，实验覆盖了**两个基准**（FEVER、NQ），属于事实核查与问答两类任务，能部分支持方法在不同范式下的有效性。
- 但是否还包括**更多消融实验**（如不同的声明-证据打分器、不同预训练模型、不同 α 取值、不同检索器、与其他忠实性方法对比）则**不清楚**。
- 对比对象目前只见 vanilla RAG，缺少与其他 RAG 事实性控制方法（如基于提示、对比解码、事实性分类器、强化学习等方法）的横向比较，因此实验的“性价比”有限。
- 总体而言：实验结果方向明确，但所披露的对比与消融范围可能不够“充分”，有待查看全文确认。

## 6. 主要结论与贡献
- CiteGuard 能够显著降低 RAG 中被接受声明中的错误发现率，同时保留大部分有支持声明。
- 将“引用是否可靠”转化为“假设检验是否通过”的框架，为 RAG 提供了**可验证的、有统计依据**的可靠性保障。
- 关键贡献是提供“用户可控风险预算”：α 参数化了忠实度与覆盖率之间的权衡，在可交换性假设下有有限样本保证。

## 7. 方法亮点
- **统计严谨性**：把共形推断与多重假设检验结合，不依赖对生成模型的内部结构做假设，只要求校准数据的可交换性。
- **模型无关/模块化**：作为解码层，可叠加到已有 RAG 系统上，不必重新训练生成模型。
- **直观的应用价值**：能够自动回答“这句话到底要不要引用、要不要撤回”，对实际产品中减少幻觉传播有帮助。
- **可解释性**：给出 p 值和显著性的概念框架，比单纯输出“置信分数”更严格。

## 8. 不足与局限
- **依赖可交换性假设**：共形校准在分布漂移、流式数据或未见过的任务迁移下，有限样本保证可能失效。
- **上游打分器依赖**：若声明-证据支持度打分本身不准确，转换出的 p 值也未必可靠，瓶颈可能从“生成器”转移到“证据分类器”。
- **实验覆盖不够广**（据可得信息）：只涉及 FEVER 和 NQ，缺少更多领域（如医疗、法律、金融）和多语言验证。
- **对比方法单一**：没有与更多现有的反幻觉/忠实性对策进行同台竞技，难以判断相对优势。
- **潜在过度保守**：在部分有支持但证据不完整的句子上可能倾向于弃答，导致信息覆盖率下降（目前保留率为 86–92%，仍存在取舍空间）。
- **引用真实性判定粒度**：句子级判断未必能细粒度处理“一句话中部分陈述有证据、部分没有”的复杂情况。
- **计算资源/推理成本**披露不详，缺少对实际落地中的时延与开销的评估。

（完）
