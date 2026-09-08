---
title: "LePaRD: A Large-Scale Dataset of Judicial Citations to Precedent"
title_zh: LePaRD：大规模司法引证先例数据集
authors: "Robert Mahari, Dominik Stammbach, Elliott Ash, Alex Pentland"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.532.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 大规模联邦司法引证数据集LePaRD，任务是从先例判决中检索相关法律段落
tldr: "法律实践需要从冗长的先例判决中定位与当前论证相关的段落，但相关大规模资源很少。LePaRD利用数百万条美国联邦法官在上下文中引用先例的实例，构建法律段落检索任务，目标是针对给定论证上下文预测应先例中的哪些段落。评测显示分类式检索方法表现最好，但在对应最高频一万个段落的数据上召回率仍仅59%，证明任务极具挑战。该数据集为法律证据检索与引用推荐提供海量高质量语料。"
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long532/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long532/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1589, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long532/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1436, \"height\": 727, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long532/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1604, \"height\": 1987, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1680, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1581, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 718, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1617, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 746, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long532/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1316, \"height\": 1327, \"label\": \"Table\"}]"
motivation: 法律论证中定位相关先例段落是实践常用技能，但缺少覆盖真实引证情境的大规模检索数据。
method: 从联邦法院裁判文书中抽取法官在具体上下文中引用的先例，定义法律段落检索任务并评测多种检索方案。
result: "分类式检索优于其他方法，但即使针对最高频的一万段落训练，召回率也只有59%，显示问题难度大。"
conclusion: 为法律段落检索提供大规模高质量基准和基线，是支持证据定位和预检索的基础资源。
---

## Abstract
We present the Legal Passage Retrieval Dataset, LePaRD. LePaRD contains millions of examples of U.S. federal judges citing precedent in context. The dataset aims to facilitate work on legal passage retrieval, a challenging practice-oriented legal retrieval and reasoning task. Legal passage retrieval seeks to predict relevant passages from precedential court decisions given the context of a legal argument. We extensively evaluate various approaches on LePaRD, and find that classification-based retrieval appears to work best. Our best models only achieve a recall of 59% when trained on data corresponding to the 10,000 most-cited passages, underscoring the difficulty of legal passage retrieval. By publishing LePaRD, we provide a large-scale and high quality resource to foster further research on legal passage retrieval. We hope that research on this practice-oriented NLP task will help expand access to justice by reducing the burden associated with legal research via computational assistance. Warning: Extracts from judicial opinions may contain offensive language.

---

## 论文详细总结（自动生成）

# LePaRD: A Large-Scale Dataset of Judicial Citations to Precedent——详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 在普通法司法辖区（覆盖全球约三分之一人口），法律论证依赖先例，法官与律师必须大量引用既往判决。美国联邦法院已出版约 170 万份判决意见，产生数千万条可能被引用的法律规则与解释段落。
- 面对海量先例，法律检索高度耗时且昂贵：商业检索服务单次可达 100 美元。高昂成本加剧了“司法可及性差距”：约 90% 低收入者的民事法律问题未获充分法律帮助。
- 现有法律检索研究存在三个断层：(1) 缺少大规模**法律段落级**数据集，而非整案检索；(2) 许多高质量标注数据为商业专有、不公开；(3) 已有任务（如 COLIEE）规模有限且与真实司法实践中的专家决策方式存在距离。
- 论文核心贡献是构建并发布 LePaRD（Legal Passage Retrieval Dataset）：约 430 万条“论证上下文 → 目标先例段落”训练实例，覆盖约 180 万个被引用过的独特段落。任务定义上侧重模拟真正的法律实践需求——给定一段论证语境，从先例判决中预测会被引用的**具体段落**（而非整篇判决），这对法律检索、证据定位与法律推理研究均有价值。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思路**：利用真实法官写作中对先例的引用行为作为天然监督信号，而不是人工标注或合成查询。
- 数据来源：哈佛 Case Law Access Project（CAP），约 170 万份联邦法院意见（含最高法院、13 个上诉法院、94 个地区法院）。
- 构建流程（文字说明）：
  1. **预处理**：用基于 RoBERTa 的法律文本句子边界识别模型对每份判决分句；清理重复引用与自我引用；将多种异名引用映射到统一 case_id。
  2. **抽取引用上下文**：用正则找出判决文本中所有带引号的引文（超过 5 个词），在引文之前截取至多 300 词的“前置语境”（避免多引文重叠语境）。
  3. **将引文匹配至来源段落**：利用目标判决中的法律引用，候选来源判决，通过模糊字符串匹配将引文与来源判决中的单个句子对应，得到“目标段落”。
  4. 为每个实例附加元数据：目标法院、来源法院、目标判决日期、来源判决日期。
- 该流程同时产生多个规模版本（10K / 20K / 50K 个最高频引用段落）以及全量段落版本以支持一次性检索研究。
- 评估任务定义：给定法律语境 xi，从候选集合 {y1, ..., yn} 中检索正确目标段落 yi。

## 3. 实验设计

- **数据集/场景**：
  - 三个受控规模版本（10K / 20K / 50K 个被引用最多的目标段落），训练集占 90%，开发 5%，测试 5%；其中 10K 版约 52 万训练实例、20K 约 70 万、50K 约 103 万。
  - 含专家评估：一位执业律师审核 100 个随机样本。
  - 附录 C 中补充了“去引用”版本：用 ChatGPT-3.5 做起始标注，再训练 RoBERTa token 分类器识别引用并从上下文删除后重跑核心实验，以避免标签泄漏。
- **对比方法/基线**：
  - BM25（稀疏词法检索，Anserini）；
  - 通用 SBERT 语义嵌入（all-mpnet-base-v2）+ FAISS 最大点积检索；
  - 微调 SBERT（用 Multiple Negatives Ranking Loss 微调）；
  - 分类式检索：以每个目标段落为唯一类别标签，用上下文预测标签——分别是 LEGAL-BERT 分类器和 DistilBERT 分类器。
- **指标**：召回率 rc@1、rc@10、NDCG@10、MAP（开发/测试集，pytrec_eval）。
- **数据质量检验**：专家对 100 个样本判断 (1) 是否干净无错误 (2) 前置语境是否足以判断目标段落相关性。
- **去引用消融**：用 1500 条样例训练 RoBERTa 识别引用串，移除后再跑基线；附带了与主结果表的对比。

## 4. 资源与算力

- 论文**未明确说明具体的算力与训练资源**（未列出 GPU 型号、数量或训练时长）。
- 仅知：句子边界模型使用 Huggingface Trainer 默认超参；SBERT 微调沿用其仓库预设超参；分类模型同样使用 Trainer 标准超参。全部模型为中小型 transformer（DistilBERT、LEGAL-BERT、SentenceBERT），未使用大模型或大算力实验——作者明确表示这是为了让资源有限的学术研究者也能复现。

## 5. 实验数量与充分性

- **实验体量与广度**：覆盖三大候选集规模（10K/20K/50K）下的 5 类方法组合，且同时报告 dev/test 的 4 项指标；另含专家质量评估与去引用消融组、关于长尾分布/法院结构/时间跨度/共聚类几个数据分布分析测量——整体实验布局结构化且规模充分。
- **充分性评价**：
  - 客观方面：对比了同一指标下统一度量的多个经典检索框架（BM25、SBERT、微调 SBERT、分类法），设定同数据集同分割，较公平。
  - 不足方面：分类法对比仅止于两个 BERT 级模型，未尝试更大的生成式模型、重排序模型、晚交互等论文中提及的技术；对数据构建中的参数（如引文长度阈值、模糊匹配严格度）缺少敏感性分析/端到端消融；10K/20K/50K 都是最高频子集，50K 已是质量/性能上限，而非全量 180 万候选集上的评测——实验设计的内部一致性较好，但覆盖面仍有提升空间。

## 6. 论文的主要结论与发现

- **任务具有高难度**：即使最佳方法（DistilBERT 分类器，在最高频 10K 段落上），测试集召回率 rc@10 仅 59.12%；在 50K 版本降至 39.34%，说明任务对技术仍有挑战。
- **分类式检索 > 稠密检索 > 稀疏检索**：BM25 表现最弱（rc@10 约 13-20%），说明上下文与目标段落间的词汇重叠非常有限；微调 SBERT 使稠密检索性能翻倍以上，但仍明显低于分类法。
- 通用预训练模型（SBERT、LEGAL-BERT）对法律段落检索的迁移性较差，领域特化微调是关键；但 LEGAL-BERT 反而不如更通用的 DistilBERT，可能是预训练域与“美国联邦先例检索”任务不完全匹配。
- 引证满足长尾分布：1% 最高频段落占到总引证的 18%，64% 段落仅获 1 次引用——类别不平衡是内在难点。
- 专家评估表明：100 个样本全部无标注性错误（仅存在 OCR 噪声），其中 99% 语境足以支撑目标输出判断，数据质量有保障。
- 先例平均持续被引用约 10 年（最长逾 150 年），高频引用的段落集中于最高法院与上诉法院；区块法院极少自引，符合普通法体系结构。段落共现聚类中可见“总结判决”“破产法”等自然类簇。
- “去引用”消融提示：引文对 BM25/稠密模型而言更像噪声（去掉后分数略升），但对分类模型略有助于预测（去掉后分数略降），总体影响小。

## 7. 优点

- **生态效度高**：不依赖人工标注或合成查询，而是直接利用真实法官在真实论证语境中对先例段落的引用行为，与律师实务操作高度接近，数据天然含法律论证的“相关性”真实定义。
- **大规模**：约 430 万训练实例、180 万个被引用的去重段落，显著优于现有 COLIEE 等研究型数据规模。
- 明确针对“段落级”而非“整案级”检索，避免了整篇判决涵盖多主题、难以比较语义关联的问题，也更贴近实务中的重点定位需求。
- 提供完整元数据（法院、日期），有利于未来考虑“绑定先例”的约束规则。
- 质量控制较严谨：专业律师人工审核、模糊匹配、去 OCR 错误的多重策略、长尾处理以及“去引用”检查都在论文中做了明确交代。
- 附带标准切分、代码、指标与基线（BM25、SBERT、后两种监督模型均有详尽报告），可复现性好；且全量数据纳入引文极少的“长尾”以支持一次性检索研究。

## 8. 不足与局限

- 数据层：
  - CAP 数据本身存在 PDF 转文本引入的 OCR 噪声，不能直接用于正式司法文书。
  - 匹配依赖模糊字符串匹配，可能漏掉大量加省略号或多句的引文（也排除了 5 词以下的短引文）；若 A 引 B、B 引 C，可能出现源头分配歧义。
  - 仅覆盖美国联邦法院，暂不适用于其他普通法或大陆法系，需进一步扩展。
- 任务层：
  - 分类式检索虽在实验中最优，但随着候选段落增加性能骤降（10K→50K rc@10 从 59% 降到 39%），无法直接扩展到全量 180 万段落，新增先例难以在线更新，存在偏见风险；长尾部分不会有良好效果。
- 实验层：
  - 未全部覆盖全量语料的评测，未对更大模型（如 LLama 2 等生成式检索）、重排序交互模型进行实验，也未报告训练计算资源来源。
  - 未进行数据构建关键参数的敏感性分析；LEGAL-BERT 训练数据的管辖权差异与检索任务匹配的干扰因素被简单归因但未系统性验证。
- 伦理应用方面：模型可能继承偏差、可能被用于滥诉；虽建议以“辅助、不替代人”方式部署，但缺少针对具体保护机制的鲁棒缓解验证。

（完）
