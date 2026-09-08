---
title: Document-level Claim Extraction and Decontextualisation for Fact-Checking
title_zh: 面向事实核查的文档级主张抽取与去语境化
authors: "Zhenyun Deng, Michael Schlichtkrull, Andreas Vlachos"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.645.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 从整篇文档抽取可核查主张并去除上下文依赖，利于主张与证据段落关联
tldr: 人工事实核查需要在包含多个主张的长文档中挑选值得核查的声明，现有方法多聚焦单句。论文将文档级主张抽取重构为抽取式摘要，先识别中心句，再对识别出的主张做去语境化，使其脱离原文仍可被理解。该方法为将主张关联到证据段落和后续事实核查提供了实用基础。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long645/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1589, \"height\": 960, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long645/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 362, \"height\": 150, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1182, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 677, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1655, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 750, \"height\": 159, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 535, \"height\": 1264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long645/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1262, \"height\": 522, \"label\": \"Table\"}]"
motivation: 现有主张抽取多聚焦单句，难以从多句长文档中提取完整可核查的主张。
method: 将文档级主张抽取转化为抽取式摘要以定位中心句，再对主张进行去语境化处理。
result: 在文档级主张抽取与去语境化任务上验证了有效性，可降低人工核查前筛选成本。
conclusion: 文档级抽取与去语境化能为可核查主张的证据化流水线提供重要前端支持。
---

## Abstract
Selecting which claims to check is a time-consuming task for human fact-checkers, especially from documents consisting of multiple sentences and containing multiple claims. However, existing claim extraction approaches focus more on identifying and extracting claims from individual sentences, e.g., identifying whether a sentence contains a claim or the exact boundaries of the claim within a sentence. In this paper, we propose a method for document-level claim extraction for fact-checking, which aims to extract check-worthy claims from documents and decontextualise them so that they can be understood out of context. Specifically, we first recast claim extraction as extractive summarization in order to identify central sentences from documents, then rewrite them to include necessary context from the originating document through sentence decontextualisation. Evaluation with both automatic metrics and a fact-checking professional shows that our method is able to extract check-worthy claims from documents at a higher rate than previous work, while also improving evidence retrieval.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 论文的核心问题与整体含义（研究动机与背景）

- **研究背景**：事实核查人员每天需要从海量信息中筛选值得核查的主张（claim），这是一个极其耗时且影响核查效果的关键步骤。现实中的信息源通常是多句文档，而非孤立单句，这对自动化的主张抽取提出了更高要求。
- **核心问题**：现有主张抽取（Claim Extraction, CE）方法存在两个主要局限，均阻碍其在真实场景中的落地应用：
  - **局限性一：局限于句子层面**。现有方法往往只判断“某个句子是否包含值得核查的主张”（如Claimbuster），或在句子内识别主张边界。它们没有考虑文档的整体语境，容易抽取多个语义冗余或与文档中心思想无关的句子，造成核查资源浪费。
  - **局限性二：忽视主张的可读性与自包含性**。从文档中抽取出的主张若包含人称代词、模糊时间地点或隐式指代，则脱离原文后会产生歧义，难以被独立理解和核查，也因此不利于后续的证据检索环节。
- **本文定位与整体含义**：作者提出首个面向事实核查的**文档级主张抽取与去语境化（Document-level Claim Extraction and Decontextualisation）**框架。目标是：从多句文档中抽取与文档中心思想相关的、值得核查的主张，并将其改写为**脱离原文仍可无歧义理解**的自包含句，从而有效支撑后续证据检索和人工核查。

---

### 2. 论文提出的方法论

整个方法框架由四个模块串联组成，可简述为“先选句，再补充语境，后改写，最后定取舍”。以下按流程说明核心思想与技术细节：

#### 2.1 句子抽取（Sentence Extraction）
- **核心思想**：事实核查者选择的观点主张一般来自文档的中心句。因此，本文把文档级 CE 的任务重构为**抽取式摘要（extractive summarization）**问题，目标是找出与文档主旨相关的 k 个中心句，同时避免抽取到语义重复的句子。
- **模型与方法**：
  - 使用 **BertSum**（Liu and Lapata, 2019）作为抽取式摘要模型。它将文档 `D = {s1, ..., sn}` 拼接为 `[CLS] s1 [SEP] ... [CLS] sn [SEP]` 格式，经BERT编码后，每个 `[CLS]` 向量经由一层线性层+sigmoid得到其作为摘要句的分数。
  - 为了避免排名靠前的句子出现高冗余问题，引入蕴含模型 **DocNLI**（Yin et al., 2021）计算句子之间的蕴含/冗余关系，通过迭代删除与高分句语义等同的句子，最终保留 k 个互不冗余的中心句。

#### 2.2 语境生成（Context Generation）
- **核心思想**：中心句中的指代词（如“he”“they”）、名词短语（如“the government”）等信息单元脱离全文语境后很难理解。本模块目的是为目标句中的可疑信息点生成**特化且高质量的语境**，而不是像Choi et al. (2021)那样把整段上下文搬来。
- **具体流程分为三步**：
  1. **问题生成（Question Generation）**：用 Spacy 抽取句中可能歧义的信息单元 `Ui`（如命名实体、代词、名词、名词短语、动词等），用预训练的问题生成器 MixQG（Murakhovs'ka et al., 2022）为每个信息单元生成以该单元为答案的问题。
  2. **问题回答（Question Answering）**：先用 BM25 从整篇文档检索与问题相关的证据段落，再使用 UnifiedQA-v2 回答问题，以得到信息单元在文档层面的完整形式（例如将“He”补全为实际人名）。
  3. **QA 转语境（QA-to-Context Generation）**：将 QA 对输入到基于 BART 微调在 QA2D 数据集上的模型，转换成为陈述句，拼接成一个语境集合 `C'i`。

#### 2.3 句子去语境化（Sentence Decontextualisation）
- **目的**：将上一步生成的语境与原始候选句拼接，利用模型改写句子，使得原始句中所有歧义信息得到澄清，同时尽量保持原意。
- **模型与方法**：使用 Choi et al. (2021) 提出的 seq2seq 去语境化模型（基于T5）。输入序列为“`[CLS] 语境句1 [SEP] 语境句2 ... [SEP] 待改写句`”，输出重写后的去语境化句子。
- **分类处理**：若句子“可行”则输出改写句；“不可行”则保留原句；“无需改写”则直接输出原句。

#### 2.4 核查价值估计（Check-Worthiness Estimation）
- **核心思想**：检查价值必须在去语境化之后评估—有些主张在补充语境前“表面上不值得查”，但补充后可能突显其可核查性与公共价值。
- **模型与方法**：使用在 ClaimBuster 数据集上微调过的 DeBERTa 分类器，将去语境化后的候选句分为“值得核查的事实句（CFS）”、“不重要的事实句（UFS）”和“非事实句（NFS）”三类。最后从候选去语境化句子中选取得分最高者作为最终的文档级主张。

---

### 3. 实验设计

#### 3.1 数据集与 Benchmark
- **核心数据集**：作者从 **AVeriTeC**（Schlichtkrull et al., 2023）中派生出一个文档级 CE 数据集，命名为 **AVeriTeC-DCE**。AVeriTeC 收集自 50 个不同事实核查组织的真实核查样本，每条样本含“事实核查者输出并脱语境化的声明”和原始来源URL。作者爬取这些URL得到文档，过滤掉无法抓取或纯图片/音视频的样本后得到1231个样本。
- **样本属性**：其中训练样本不另设划分，因为所用组件均为预训练模型（BertSum等）或无监督检索方法（BM25），无需端到端重新训练；Med. 文档句数为5~9句，claim 平均长度约16-17词。
- **附加验证场景**：CLEF-2021 CheckThat! Lab 子任务1B（check-worthiness estimation in tweets and political debates）。

#### 3.2 对比方法概述
- **句子抽取对比基线**：Lead Sentence（首句）、Claimbuster、LSA、TextRank、BertSum。
- **去语境化对比基线**：原始句、基于 SpanBERT 的指代消解模型、Choi et al. (2021) 的基于段落上下文的 Seq2seq 模型。
- **整体文档级 CE 对比基线**：将不同抽取方法（Claimbuster/Lead/LSA/TextRank/BertSum/Our）与本文去语境化、检查价值估算两个模块组合进行端到端对比。

#### 3.3 评价方式
- **自动评估**：句子抽取质量通过 P@1/P@3/P@5/P@10 衡量，即以“与人工主张句的 chrF 最高”的句子是否在前 k 位内为准；文档级 CE 质量用 chrF（主指标）+ SARI/ BERTScore（附录辅助）来衡量。
- **人工评估**：请一位事实核查专业人员对“抽出的句子是否值得核查（IsCheckWorthy）”和“是否与文章中心思想相关（IsCentralClaim）”进行判断。
- **检索式评估**：为验证去语境化的实际价值，用 BM25 以不同句子（原始句 vs 去语境化句）为查询，在 AVeriTeC 的证据池中检索黄金证据，以 P@3/P@5/P@10 检验。

---

### 4. 资源与算力

- 论文**未在正文或附录中明确说明**所需的 GPU 型号、数量或训练时长等信息。因为本文事实上是一个用现有预训练组件拼装起来的标准 pipeline，没有披露推理与评估的底层硬件配置。
- 唯一可间接推断的是，文中使用的全部模型方式均有公开来源：BertSum、DocNLI、MixQG、UnifiedQA-v2、T5 去语境化模型、DeBERTa (ClaimBuster) 等均为中等体量预训练模型，理论计算开销不算大，且不需要针对任务的全模型再训练。

---

### 5. 实验数量与充分性

#### 5.1 实验组数概览
- **句子抽取**：6个方法在 AVeriTeC-DCE 全量测试上做 P@1/3/5/10 自动对比，附加50样本人工评估（有专业事实核查者参与），实验数量基本达标。
- **去语境化**：4种句子（原句/指代消解/seq2seq上文/本文QA语境）在检索证据场景上做 P@3/5/10 对比；附加三个典型 linguistic phenomena（指代消解、限定范围、桥接回指）的案例展示。
- **整体文档级CE**：主报告用 chrF 对比，附录补 SARI 与 BERTScore，且有总体统计（仅 10%句子可改写、80%无需改写等）。
- **跨数据集验证**：在 CLEF-2021 CheckThat! 1B 上与 Claimbuster 对比一次。
- **消融性验证**：缺乏严格的系统化消融（例如——去掉 DocNLI 对句子的影响、去掉 check-worthiness classifier 的效果），附录测试了 ChatGPT 去语境化结果，对比较为粗浅。

#### 5.2 客观性与公平性评价
- **优点**：检索式评价（P@3 等）相比用单一参考句做文本生成评测能更好体现“去语境化对下游有什么用”；人类评估邀请真实行业核查人员，而非众包学生。
- **不足**：句子抽取的“自动评估”依赖 chrF 先找最佳句，这一做法有较强的代理假设——认为事实核查者的声明应当来自与它文本 n-gram 最相近的原句；但在真实核查中声明由人工重新撰写的比例可能较高，因此 chrF 不一定等同于中心句。

---

### 6. 论文的主要结论与发现

1. **句子抽取层面**：BertSum + DocNLI 的组合在 AVeriTeC-DCE 上取得 P@1=47.8%，显著超过 Claimbuster（37.8%），也优于其他摘要基线。说明“先抽取文档中心句”的思路对文档级 CE 行之有效。
2. **人工评估层面**：事实核查专业人员的审计结果显示，本文 top-1 句子中有 68% 与文档中心思想相关（Claimbuster 为 24%），44% 被判定为值得核查（Claimbuster 为 36%），证实了中心相关性与可核查性并不等同，必须同时考虑上下文和中心性。
3. **去语境化效果层面**：本文的 QA-to-Context 去语境化在证据检索上的 P@3/P@5/P@10均优于核心指代消解和语境拼接等方法，平均提升精确率 1.08；在21个可去语境化句子中，17句的证据检索结果得到改善（平均提升1.21）。
4. **端到端文档级 CE 层面**：整个框架在端到端测试中 chrF 达 26.4，超过所有基线。同时在 CLEF-2021 subtask 1B 上 P@1/3/5/10 均高于 Claimbuster，说明方法在跨场景上也有效。

---

### 7. 优点

- **任务与场景选型直面实践问题**：论文明确指出并解决现有工作“只抽句子不抽文档、抽取出来的主张有歧义”的痛点，对照真实事实核查端到端生产场景，任务立意清晰。
- **方法论组装视角富有启发性**：将“主张抽取”拆为“摘要抽取→语境生成→句子去语境化→检查价值估计”，模块边界清楚，各环节可独立替换升级，工程落地弹性好。
- **QA 驱动的语境生成具有新意**：与以往直接拿原文上一段做语境的方法相比，QA 过程能够窄化到潜在歧义信息本身，得到的语境更紧凑、信噪比更高，是去语境化研究中的一个亮点。
- **评价机制兼顾自动与人工、上游与下游**：既用自动指标衡量生成相似度，也设了“human-verifier”维度评估；还巧妙利用 evidence retrieval 做下游成效检验，避免单靠文本重合度量带来的偏差。
- **验证了“中心句→中心主张”的结构性假设**，同时发现与中心思想相关的句子未必本来就值得核查——去语境化能显式提升某些句子的可核查性，这一观察对后续方法设计启发很大。

---

### 8. 不足与局限

- **依赖文档可抓取性与HTML质量**：AVeriTeC-DCE 的构建依赖 Web Scraper，部分样本因无法爬取而被过滤。数据集中 twitter/facebook 占比较大（约38%），而社交帖子往往比新闻文章更短、观点更集中，所以结论能否平滑推广到新闻长文仍需进一步验证。
- **10%左右句子完全无法去语境化**：若文档上下文本身就没有足够的信息来澄清歧义（比如指代，或涉及单一事实核查组织内部知识），方法将直接输出原句，无法保证“out-of-context”可理解。论文就此只是承认局限，没有给出替代恢复方案。
- **自动评估与真实标注存在结构性差异**：AVeriTeC 的黄金声明可能是事实核查者结合核查文章、调查线索后撰写的，并不完全包含于来源文章，所以 chrF/SARI/BERTScore 并不能衡量“文本含义上等价而措辞完全不同”的主张。
- **Check-worthiness 的主观性**：不同事实核查机构对什么值得检查的判断不同（有的机构会查讽刺或戏仿文章）。模型基于 ClaimBuster 单一标准的分类器承接此项任务，未必能迁移到所有核查机构。论文在 limitation 中坦诚承认了这一问题。
- **缺少系统化消融实验**：没有单列——例如“去掉 DocNLI 冗余消除”“去掉 QA 语境生成而用整段上文”“去掉 check-worthiness 估算层”对照——这使得读者很难确认四个组件的相对贡献边界与正交性。
- **算力与复现细节披露不足**：论文没有说明所使用的 GPU 型号、显存、执行时间、大批量输入时的效率损失等；对于想在生产环境复刻的读者，缺少资源预算参考。

---

（完）
