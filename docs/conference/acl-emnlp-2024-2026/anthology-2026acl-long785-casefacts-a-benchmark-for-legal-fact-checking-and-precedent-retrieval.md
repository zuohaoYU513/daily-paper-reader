---
title: "CaseFacts: A Benchmark for Legal Fact-Checking and Precedent Retrieval"
title_zh: CaseFacts：法律事实验证与先例检索基准
authors: "Akshith Reddy Putta, Jacob Devasier, Chengkai Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.785.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 面向最高法院先例的法律事实验证基准，含时间效力判定的主张核查数据
tldr: 自动事实核查大多针对静态常识语料，法律领域主张随时间演变且语义复杂，模型需要弥合普通人表述与专业判例的鸿沟。CaseFacts基准包含6294条口语化法律主张，以美国最高法院先例为依据判断其为支持、反驳或推翻。构建时使用LLM多阶段流程从专家案件摘要合成主张并纳入时间效力判断。该资源推动法律事实核查与先例检索等证据型评估研究。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long785/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1546, \"height\": 1133, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long785/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1238, \"height\": 643, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 623, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 823, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 815, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1663, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 810, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long785/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1673, \"height\": 903, \"label\": \"Table\"}]"
motivation: 法律事实验证需弥合普通人陈述与技术判例的语义差异，并考虑法律随时间被推翻等情况，现有基准难以覆盖。
method: 用多阶段LLM流水线从案件摘要合成口语化法律主张，并以最高法院先例为标准标注为支持、反驳或推翻。
result: 获得6294条主张，按Supported、Refuted或Overruled分类，可用于评测法律主张的时间效力和先例检索。
conclusion: 为法律领域证据型事实验证提供数据集与任务基准，推进证据问答和时效法律推理研究。
---

## Abstract
Automated Fact-Checking has largely focused on verifying general knowledge against static corpora, overlooking high-stakes domains like law where truth is evolving and technically complex. We introduce CaseFacts, a benchmark for verifying colloquial legal claims against U.S. Supreme Court precedents. Unlike existing resources that map formal texts to formal texts, CaseFacts challenges systems to bridge the semantic gap between layperson assertions and technical jurisprudence while accounting for temporal validity. The dataset consists of 6,294 claims categorized as Supported, Refuted, or Overruled. We construct this benchmark using a multi-stage pipeline that leverages Large Language Models (LLMs) to synthesize claims from expert case summaries, employing a novel semantic similarity heuristic to efficiently identify and verify complex legal overrulings. Experiments with state-of-the-art LLMs reveal that the task remains challenging; notably, augmenting models with unrestricted web search degrades performance compared to closed-book baselines due to the retrieval of noisy, non-authoritative precedents. We release CaseFacts to spur research into legal fact verification systems.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

自动事实核查（Automated Fact-Checking, AFC）已在常识领域取得较多进展，但普遍低估了法律这一高风险领域中的特殊性。法律语境中的“真”是**动态演化**的——先例可被后续判决推翻；同时普通人的口语化主张与法院判决书之间存在显著的**语义鸿沟**。现有法律基准如 LegalBench、CaseHOLD 采用的是“法言法语到法言法语”的映射，缺乏对日常法律话语与先例检索、时效判断之间断层的研究。**本文提出 CaseFacts，一个用于验证公众口语化法律主张的基准**，以美国最高法院（SCOTUS）判例为证据库，为法律事实核查提供了新的任务定义与资源。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程（用文字说明即可）

**核心思想**：利用 LLM 从专家摘要生成法律主张（claims），并通过多级过滤与验证，将主张标注为 Supported、Refuted、Overruled，以此评测模型在语义桥梁、证据检索与时效判断上的能力。

**主要流程（文字描述）**：
- **数据来源**：以 Oyez 案例库的 3,299 个 SCOTUS 案例的 “facts”“question”“conclusion” 作为证据基础。
- **主张生成（Claim Generation）**：使用生成模型（Qwen3-Next-80B-A3B-Thinking），被要求生成口语化、非具体指代性的通用法律原则，避免案例名称和法院叙事风格。
- **类内验证（Intra-Case Validation）**：
  - 事实性检查（Factuality Check）：LLM-as-a-Judge，基于闭世界假设检验主张是否与案例证据一致；
  - 矛盾与重叠检测与消解：移除同一案例内部互相矛盾或语义冗余的 claims。
- **类间验证（Inter-Case Validation）**：
  - 用语义相似度启发式（范围：矛盾 0.70–0.95，重叠 0.80–0.97）筛选跨案例需比对的 claim 对，大幅降低计算规模；
  - 对检测到的矛盾对，借助裁决日期与判决结果元数据判断是否构成 “overruling”，进而构建 Overruled 类别；
  - 对重叠对进行合并处理，扩展多案例支持的 Ground truth cases。
- **Refuted 负样本生成**：将支持的主张进行“似真否定”（两步走：合理否定生成 + 长度裁剪和泛化提炼），而非机械添加“not”，以避免模型利用长度与条件词进行捷径判断。
- **人工验证**：测试集的 574 条主张经由 2 位标注者及独立律师审核，Cohen's Kappa 为 0.637。

### 3. 实验设计：使用了哪些数据集/场景，它的 benchmark 是什么，对比了哪些方法

**数据集与测评基准**：
- 总数据集：6,294 条（训练集 5,794，测试集 500）
- 标签分布：Supported（训练 2,605 / 测试 280）、Refuted（训练 2,732 / 测试 177）、Overruled（训练 457 / 测试 43）
- 每条 claim 附有 ground-truth SCOTUS 案例证据，证据评分要求 Recall@5 ≥ 0.5 才计入证据分。

**评测方法**：
- Evidence Score（基于案例检索召回）；
- Verdict Accuracy；
- 最终主指标：Verdict Score = Evidence Score × Verdict Accuracy（整体得分）。

**对比方法**
- **LLM 基线**：GPT-4o 在 Naive（无外部检索）和增强搜索（web search）模式下对比。
- **语义相似度模型微调**：对 BM25、ColBERT，以及多种稠密检索预训练模型（bge-base-en-v1.5、MiniLM-L6-v2、Qwen3-Embedding-0.6B），在不同训练轮数下进行对比。
- **NLI 模型测试失败**：初始使用 textattack/bert-base-uncased-MNLI 模型进行跨案验证，但其无法有效识别法理矛盾，弃用。

### 4. 资源与算力

论文**没有明确列出 GPU 型号、数量、训练时长等具体算力参数**。只在数据生成方面提到使用了 Qwen3-Next-80B-A3B-Thinking 与 gemma-3-27b-it（提示词进行判断），并控制了 temperature/top-p。在微调语义相似度模型时同样未报告具体计算资源配置，因而从可复现性角度看，仍需要作者进一步补充训练环境的细节。

### 5. 实验数量与充分性：这些实验是否充分、是否客观、公平

- 实验数量较为可观，覆盖了三大类测评：
  1. 基线与检索增强对比（Naive vs Search）；
  2. 多种 denses 检索模型微调对比（三种 base model，每个训练 1/3/5 epochs，共 9 组对比实验）；
  3. 对 LLM 判断器在 Factuality、Contradiction、Overlap 三项任务上进行人工一致性评测。
- 同时测试了模型在仅含实体（如 “United States”）的子集上的性能，检验信息移除的有效性。
- 在公平性方面，论文使用了与生成、验证模型族不同的 GPT-4o 进行基线评测，合理规避“自偏好偏差（self-preference bias）”。

**总体评价**：实验在任务定义、多模型对比、人工质控等维度较充分；但缺乏对不同提示策略、超参数选择的敏感性分析，对 embedding retrieval 的效果也主要依赖 Recall@k，未充分分析其对不同标签类型的差异。

### 6. 论文的主要结论与发现

- **任务仍然具有挑战性**，尤其体现在证据召回环节：LLM 的 Verdict 预测准确率（0.574–0.600）明显高于 Evidence Score（0.212–0.232），说明模型能“猜对结论”但找不准先例。
- **开放域检索反而降低性能**：接入 Web search 的 GPT-4o 在全部三项指标上均低于无检索基线，原因是检索到的判例不权威或与金标证据偏差大。
- **该训练集对于 embedding 微调有效**：如 Qwen3-Embedding-0.6B 在 Recall@1 上提升 +24.1 个点，验证了 CaseFacts 对检索模型训练的正面作用。
- **LLM-as-a-Judge 一致性较好**：在人工已审核的基准上，三项子任务达到 95.5%～97.4% 的一致性。
- **标准 NLI 方法无法胜任跨案例法理逻辑推理**，因此其转而被更灵活的 LLM 判定与语义阈值的结合方式取代。

### 7. 优点

- **创新性任务定位**：首次同时强调“口语化表达 → 判例证据”、“临时否定判断 → 随时间演进”，使法律事实核查站在更贴近真实舆论环境的视角。
- **较严格的数据质量控制**：不仅考察事实验证，还细致处理相互矛盾、冗余 claim，经过多轮删重与语义判别。
- **高效构造方法**：用语义相似度区间+分位统计替代全量 pairwise LLM 判断，在控制成本的前提下兼顾召回。
- **评测机制严格**：提出 Evidence Score 阈值，防止模型借“随机命中”获得高分，并采用 Verdict Score 作为更据说服力的联合指标。
- **开源性**：发布代码与数据，支持今后研究者复现及扩展。

### 8. 不足与局限

- **案例摘要依赖**：采用 Oyez 摘要而非原文，缺乏复杂长文本推理挑战，简化了真实检索难度。
- **忽略成文法与下级法院判例**：仅覆盖最高法院判例，无法识别因立法取代而失效的情形。
- **地域局限**：仅基于美国，且未考虑其他国家法域。
- **同类案例人工判定难度较高**：Overruled 类人工通过率（74%）低于其他两类（90%），表明其固有的复杂性和标注主观性。
- **生成伪负样本可能过于狭化**：Refuted 类以语义“否定”为主，不包含对法律引用失当或脱离上下文的真实误导。
- **无大规模正式算力评审信息**：限制了关于可扩展性、运行成本和技术可行性的外部判断。
- **模型与任务偏见风险**：数据中的历史性不公正判决虽辅以 Overruled 标注，但可能触发法律和伦理上的传播风险，评测模型带有潜在时代偏见可能被强化。

（完）
