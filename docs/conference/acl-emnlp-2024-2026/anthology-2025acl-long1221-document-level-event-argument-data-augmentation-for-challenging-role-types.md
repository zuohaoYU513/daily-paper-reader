---
title: Document-Level Event-Argument Data Augmentation for Challenging Role Types
title_zh: 面向困难角色类型的文档级事件论元数据增强
authors: "Joseph Gatto, Omar Sharif, Parker Seegmiller, Sarah Masud Preum"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1221.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 针对长文档事件论元抽取的少样本与困难角色类型设计LLM数据增强方法
tldr: 事件论元抽取在少样本跨域设置下受数据不足限制，已有增强方法难以处理超过十句的长文档和稀疏且语义边缘的角色类型。论文提出两种基于大模型的文档级抽取式事件论元数据增强方法，在零领域标注样本条件下生成训练数据。四个数据集上的实验验证了方法的通用性，为长文档事件参与者和困难角色抽取提供了实用数据补充技术。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1300, \"height\": 692, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1385, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 754, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 767, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1363, \"height\": 1063, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1641, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1633, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1632, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1221/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1641, \"height\": 1000, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 696, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 812, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 811, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1052, \"height\": 798, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1221/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1065, \"height\": 796, \"label\": \"Table\"}]"
motivation: 现有数据增强方法不适用于长文档与挑战性角色类型的少样本跨域事件论元抽取。
method: 提出两种LLM驱动的数据增强方法，在零领域训练数据下生成抽取式文档级事件论元样本。
result: 在四个数据集上验证方法泛化良好，显著提升困难角色和长文档场景效果。
conclusion: 生成式文档级样本能有效缓解长文档事件论元抽取的低资源瓶颈。
---

## Abstract
Event Argument Extraction (EAE) is a daunting information extraction problem — with significant limitations in few-shot cross-domain (FSCD) settings. A common solution to FSCD modeling is data augmentation. Unfortunately, existing augmentation methods are not well-suited to a variety of real-world EAE contexts, including (i) modeling long documents (documents with over 10 sentences), and (ii) modeling challenging role types (i.e., event roles with little to no training data and semantically outlying roles). We introduce two novel LLM-powered data augmentation methods for generating extractive document-level EAE samples using zero in-domain training data. We validate the generalizability of our approach on four datasets — showing significant performance increases in low-resource settings. Our highest performing models provide a 13-pt increase in F1 score on zero-shot role extraction in FSCD evaluation.

---

## 论文详细总结（自动生成）

### 一、论文的核心问题与整体含义

- 事件论元抽取（Event Argument Extraction, EAE） 是信息抽取领域的难点问题，在该任务的少样本跨域（Few-Shot Cross-Domain，FSCD）设置下，模型性能尤为受限。
- 常用解决方案是数据增强，但现有增强方法无法很好应对两类真实场景：
  1. **长文档建模**：文档包含超过10个句子时，论证跨度可能分布在全文档各处，现有句子级增强方式失效；
  2. **困难角色类型建模**：某些事件角色（event roles）几乎没有训练样本（如 DocEE 中的 0-shot roles），或在语义上与源域角色差异极大。

- 论文在一无领域内训练数据的前提下，设计了两类 **面向零领域样本数据的 DocEAE 数据生成框架**，用 LLM 生成抽取式文档级 EAE 样本，并希望该框架能泛化到新的事件领域、新的文档长度与不同的事件角色结构。

- 文中强调一点：已有多数 EAE 数据增强仅作用于句子级数据，已有的文档级增强要么只增强已有样本，要么依赖已标注语料的弱标注，不是真正“自动生成全新文档”。本文着眼点是零样本文档级数据生成，并为困难角色建立更公平的评测指标。

---

### 二、论文提出的方法论

#### 1. 整体思路
- 提供一个“事件模式”（event schema），即包含事件名与该事件所有可能角色（role）的列表；
- 利用 LLM 的上下文学习（In-Context Learning, ICL）从源域中，挑选k个注释示例，驱动生成目标事件类型的 **文档级抽取式事件论元样本**（文档+论元标注对）；
- 所有生成过程均不使用目标域训练数据，保持通用性。

#### 2. 两个具体生成框架

**(A) Mad Lib Generation（MLG，疯狂填词生成）**
- 核心思想：将一个文档中的论元类比为“疯狂填词游戏”中的占位符，事件角色就是需要填写的语义类别。
- 生成分为两步：
  1. **MLG Generator**：基于源域中k个上下文示例，把事件注释的文本转换为带占位符的“Mad Lib”模板；提示 LLM 生成目标事件的情境化模板文本，并将该事件所有角色都作为占位符嵌入（例如将 `New York` 换成 `[LOCATION]`）。
  2. **MLG Solver**：给 LLM 提供模板与角色示例，让 LLM 为每个占位符生成语义上合理的论元（argument），用字符串替换反填到模板中，形成可用的带标注文档。
- 质量控制：会删除包含幻觉角色的句子，或对占位符调用 SBERT/matching 回填为合法角色，对格式不正确、缺角的情况直接重采新样本。

**(B) Struct2Text（S2T，结构到文本生成）**
- 核心思想：参考 LangChain 的“structure-to-text”数据生成框架，先产生结构化的（角色→论元）记录，再将此事件记录“翻译”成自然的文本。
- 同样分三步：
  1. **Structure Generator**：利用 Pydantic 类定义空的事件记录，使用源域示例作为上下文，调用 LLM 将每个角色对应到一个论元，生成格式严格的 JSON 事件结构。
  2. **Struct2Text Generator**：将被填好的“结构字典”交给 LLM，按格式约束和风格约束（如新闻、Reddit 帖、临床报告）将角色-论元映射扩展成一段流畅的事件文档。
  3. **Struct2Text Aligner**：由于 LLM 常将事件记录中的字符串改写为别的表达，需要对论元进行“对齐”；采用语义 n-gram（最大 n=20）匹配：把结构中的论元与文档的每个 n-gram 向量化，用 SBERT 计算余弦相似度，超过设定阈值 α 的n-gram则作为与该论元对齐的文档 span；低于阈值的角色视为生成失败并被丢弃。

#### 3. 方法特点
- 两种框架均致力于生成“角色密度高”的样本（尽量覆盖该事件模式中的所有角色），从而提高少样本和零样本角色出现频率；
- 数据生成完全不使用目标领域真实样本，仅依靠事件名与角色名的语义；
- 因为是“让模板文档携带所有角色”的生成方式，天然能够迫使 LLM 生成难以刺激到的冷门角色与异常角色（这正是困难角色类型的来源）。

---

### 三、实验设计

#### 1. 主评测（DocEE）
- 使用 **DocEE** 的跨域分割：
  - 训练源域：49个事件，共 23,630 个样本；
  - 目标域：10个“Natural Disasters”事件，训练集每事件仅5篇文档，测试集较大；
  - 零标注角色（0-shot roles）**: 9个角色；
- 基准增强方法：
  - **Baseline (No Aug)**：无额外增强；
  - **Doc-MTF**（Mask-then-Fill 文档级改编版）：用 T5 模型填充文档中新的连续文本片段；与原 MTF 不同，这里为文档级版本，可在单文档中填充多个掩码，由 MultiNews 等多文档语料微调；
  - **GPT-4o 直接执行 EAE** 的输出，作为 LLM 抽取能力的参考。

- EAE 模型（文档级抽取模型）：
  1. **BERT-QA**：抽取式问答模型，BERT-base，跨文档长为 512，用滑动窗口批处理；
  2. **LongFormer-Seq（LF-Seq）**：token 级序列标注模型，Longformer-base（149M），可处理最长4096 token。
- LLM 生成器：
  - MLG：GPT-3.5、GPT-4o、Claude-3.5-Haiku、Llama-3.1-70b、Mistral-Nemo；
  - S2T：因实现对 OpenAI 模型的依赖，仅使用 GPT-3.5 和 GPT-4o。

- 评测指标（针对角色更细粒度）：
  - **F1**：经典计算，按文档级抽取三元组（事件、角色、论元）；
  - **Role-F1**：按每个角色的 F1 做宏平均（每个角色同等重要）；
  - **0-Shot F1**：对从未出现在训练中的9个角色计算 Role-F1；
  - **RDF1**：本论文新增的角色深度F1：用数据深度（statistical depth）找目标域角色中在语义上与源域角色集差异最大的25%，在此之上计算宏平均 Role-F1，以此强调对领域特有角色（如 “Maximum Wind Speed” 等）的评价。经人工验证，这些自动筛选的角色与人工筛选一致度达78%。

#### 2. 次级评测（泛化性）
- 数据集：**RAMS**（新闻的多句事件论元链接）、**DiscourseEE**（Reddit 社交媒体论元）、**PHEE**（药物警戒文本）。
- 三种数据资源设置：各取10%、50%和100%的真实训练集，并配置500个 MLG-GPT-4o 生成样本。
- 此处数据的源域上下文示例全部取 DocEE 源域，确保跨域性；
- 注意 RAMS、DiscourseEE、PHEE 均被转换为 DocEE 格式（只保留抽取论元、合并且规范化角色等）。

#### 3. 训练细节和公平性
- 模型训练于 Google Colab 的 NVIDIA A100，采用 Huggingface Trainer；
- BERT-QA：batch size 48，3个 epoch；
- LF-Seq：源域训练3个epoch，目标域再微调，最多10个epoch，用验证集保存最优；
- 报告三次随机种子重复实验的平均值，Wilcoxon 符号秩检验用来标记显著性差异。

---

### 四、资源与算力

- 文中在附录 D 中给出：
  - 所有实验均在 **Google Colab 上的单个 NVIDIA A100 GPU** 上完成；
  - 项目预计总计算使用时间约 **150 个上限总小时**；
  - 未明确说明 LLM API 调用总量、不同实验具体所需的生成 token 数，也未公开总共使用的各模型 API 总成本，只强调使用“中等长度、角色密度高的少量 ICL 示例（k=3）以控制成本”。

---

### 五、实验数量与充分性

- 实验数量较为可观，覆盖：
  - 主评测：DocEE 上、BERT-QA 与 LF-Seq × 多种增强策略（两个基线 + 五种 MLG + 两种 S2T）组合；
  - 还有增强规模对 BERT-QA 的效果曲线实验（2x、4x、5x、6x），说明小、中、大、超大增强量对整体F1和挑战角色F1之间的权衡；
  - 次级数据集（三个外部数据集 × 三档训练数据量 × 增强或不增强）；
  - 三种随机种子重复，且带统计显著性标记。

- 实验是否客观公平：
  - 主要优点：没有只在单一数据上验证，用了4个数据集、多层次资源比例；
  - 主要缺点：**并非在绝对公平条件下**
    1. S2T 只能测试 GPT-3.5/ GPT-4o，无法和其他开源生成模型相比；
    2. LF-Seq 整体表现弱于 BERT-QA，甚至低于 GPT-4o 的直接输出（虽然只用 GPT-4o 提取时也有相当的阈值问题）；
    3. 未与更强的生成基线对比（如 STAR（Ma et al. 2023b）本来为句子级抽取、但应做适配对比）以及多种文档级弱监督生成策略对比。
  - “统计显著性差异”占实验中很大部分，但与三个基准（No-Aug、Doc-MTF、GPT-4o）比较时结果较为复杂：对 BERT-QA，MLG/S2T 并不一定在总 F1 上与No-Aug差异显著，说明其作用场景是限定的。

---

### 六、主要结论与发现

1. **针对困难角色有效**：不论 BERT-QA 还是 LF-Seq，MLG/S2T 带来的 0-Shot F1 和 RDF1改善 常明显高于 No-Aug 与 Doc-MTF；比如 MLG 与 S2T 在部分指标上比3个基线都显著更好；
2. **传统 F1 评价不能真实反应复杂角色抽取能力**：常见的 Date、Location 等高频角色不因增强而改善，模型反而可在高频率的小角色集合上过拟合，使得总 F1 没有显著提升，因此文中的增强方法更适合“扩展可抽取角色多样性”的需求；
3. **增强数量存在权衡**：增强量越大对挑战性角色有增益，但对总体 F1 会有轻微降低；
4. **泛化性好**：在 DiscourseEE、RAMS、PHEE 中 MLG总体上有较大幅度提升，尤其在仅用10%的数据时非常显著，例如 DiscourseEE 上 F1可提升约13%（0.13至0.334），说明低资源下其稳定增益；
5. **两种生成路线适配不同的需求**：
   - MLG 更兼容多种开源 LLM，依赖纯粹字面占位符替换，标注位置较精确，成本低；
   - S2T 可接入 PyDantic 结构并利用自然语言语义嵌入对齐，可把额外的结构化事件元数据（类/形容描述）方便地整合进生成，但其受限于 OpenAI 的 LangChain 管道和语义对齐误差。

---

### 七、优点

- **痛点定得非常清楚**：既覆盖长文档，又覆盖有限的角色类型和语义离群角色类型；
- **采用“零领域内样本”的生成方式**，目标域数据无需人工标注、无需现有模型引导，泛化能力和可迁移性好；
- **方法不依赖复杂事件本体**：只需要事件类型与一组角色名（多数LLM本身就具备关于角色类型的先验知识），在事件模式缺失的 DocEE/DiscourseEE 等数据集中也能部署；
- **设计了新的评价维度**：0-Shot F1 与 RDF1 直面全局F1掩盖小众角色抽取效果问题，是论文亮点；
- 多种LLM联合评估（包含开源和专有模型），并复现不同资源条件下的模型性能，合理刻画低资源增强能力的边界；
- RDF1 做了人工评估验证，说明其角色筛选并非不可解释的评价指标；
- 使用 ICL 中的3-shot源域实例仅作为格式参考，而语义生成完全依赖 LLM 参数知识，从而引导跨域集成。

---

### 八、不足与局限

- **没有探索大规模增强与精细控制角色分布的能力**：本文强调重点在少量训练任务上，因此难以对生成数据进行细粒度分布控制，真正应用于大规模训练时可能导致增益消失或偏差放大；
- S2T 的实现完全绑定 LangChain/Pydantic 及 OpenAI API，重放困难和开源可重复性下降；同时对齐时会丢弃语义不匹配的角色，可能造成部分论点空洞；
- **多论元角色未充分处理**：若一个事件文档有两个相同的角色例子（例如多个“原因”、“两个受灾点”），当前模板和结构不能优雅地生成多个论元实例；
- 单事件假设限制了方法的适用范围，比如 WikiEvents 可有多事件的复杂文档，无法迁移到该场景；
- 三种外部数据集的适配中存在变量混杂：数据集本身包含多种粒度（角色名是否是语义名还是压缩词）显著影响 MLG 的表现（如 RAMS 的角色“Instrument”可能导致 LLM 误解为音乐仪器）；
- LLM 生成的论元类型多样性不够高：文中承认比如在 PHEE 中 47% 的 `pre-existing conditions` 论元为 “hypertension”，使模型在多样性高的数据集中对目标角色记忆不牢，但这种偏差并未做系统量化分析；
- 未与其他以 RAG、prompt-based、sentence-level 生成式增强（如 STAR、denoised structure-to-text）或较强文档级增强方法做全面对比；对统计显著性检验做了良好展示，但仍需考虑不同资源比例下模型的任务难度分布差异；
- S2T的实验也几乎没有展开说明过S2T各调参粒度和对齐误差的定量表现，给出的具体数据仅是数据统计栏的数据（如 “Num Sent / Num Words”）。

---

### 综合评价说明

论文整体上针对文档级 EAE 数据增强提出了一种新颖的生成范式，而对其效果的验证覆盖了多个低资源事件抽取任务以及新设计的面向困难角色的评估指标，为后续研究提供了参考数据和方法。但由于对模型灵活性的限制以及缺少大规模可用的角色分布控制策略，该成果更适用于中等规模、低资源、关注跨域冷启动和边缘角色广度增强的研究落地场景。

（完）
