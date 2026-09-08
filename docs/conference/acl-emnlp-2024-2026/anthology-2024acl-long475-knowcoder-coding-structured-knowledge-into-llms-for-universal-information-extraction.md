---
title: "KnowCoder: Coding Structured Knowledge into LLMs for Universal Information Extraction"
title_zh: KnowCoder：将结构化知识编码进大模型用于通用信息抽取
authors: "Zixuan Li, Yutao Zeng, Yuxin Zuo, Weicheng Ren, Wenxuan Liu, Miao Su, Yucan Guo, Yantao Liu, Xiang Li, Zhilei Hu, Long Bai, Wei Li, Yidan Liu, Pan Yang, Xiaolong Jin, Jiafeng Guo (嘉丰 郭), Xueqi Cheng (程学旗)"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.475.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 通过将信息抽取结构编码为代码使大模型统一支持事件和关系等抽取任务
tldr: 通用信息抽取需要处理实体、关系、事件等异构结构化输出，现有模型往往任务隔离、泛化受限。KnowCoder提出将抽取模式和输入文本编码为程序代码，让大模型以代码化方式进行结构化知识抽取，从而覆盖事件和关系等任务并提升统一处理能力。这一思路为证据型长文档中的事件与关系抽取提供了可借鉴的模型基础。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long475/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long475/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long475/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 763, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long475/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 755, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long475/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 627, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1341, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1667, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 713, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 769, \"height\": 994, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 693, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 649, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 693, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1401, \"height\": 955, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1032, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 786, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 623, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1658, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 459, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1659, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 804, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long475/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 793, \"height\": 1230, \"label\": \"Table\"}]"
motivation: 为让大模型统一支持多种信息抽取任务并理解结构化模式，提出代码化知识表示方式。
method: 通过代码式模式构造和文本-代码对齐训练，引导大模型按结构生成抽取结果。
result: 作为一种通用抽取框架，可覆盖实体、关系、事件等多种任务的抽取需求。
conclusion: 将结构化知识代码化是增强大模型通用信息抽取能力的有效途径。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

# KnowCoder: Coding Structured Knowledge into LLMs for Universal Information Extraction

## 1. 核心问题与研究背景

- **问题定义**：通用信息抽取（UIE）旨在用一个统一模型处理多种抽取任务（实体识别、关系抽取、事件检测与论元抽取等）。现有模型面临两大挑战：
  1. **缺乏统一且对大模型友好的模式表示**：已有方法用分类标签、关键词或专门设计的规范语言表示抽取模式，难以捕获概念之间的分类体系（如 fairytale 是 written work 的子类）、概念间约束（如 spouse 关系的头尾实体都必须是 Human）、概念定义等丰富信息，也不利于大模型理解与遵循。
  2. **缺乏有效的模式学习框架**：已有方法通常直接在少量数据集上进行指令微调，难以覆盖包含数万种概念的开放模式空间。

- **整体含义**：论文提出将信息抽取模式编码为 Python 代码，把 UIE 转化为“面向对象编程”任务，使大模型能够统一理解并生成结构化知识抽取结果，从而覆盖实体、关系、事件等多类任务。

## 2. 方法论核心内容

### 2.1 代码风格的模式表示（KnowCoder Schema）

- 以三个基类 `Entity`、`Relation`、`Event` 为根，将每个概念定义为 Python 类。
- 关键设计特征：
  - **类继承**：表达概念层级/分类体系，子类继承父类成员。
  - **类注释**：给出概念的自然语言描述和示例实例，帮助模型理解概念。
  - **类型提示（Type Hint）**：在 `__init__` 函数中定义关系头尾实体的类型约束（如 `PlaceOfBirth` 的头实体必须是 `Human`）。
  - **类方法**：用于对抽取结果进行后处理，按任务特定规则过滤/修正输出（如过滤代词、去除“such as”后内容）。
- 基于 Wikidata 构建了包含 **29,177 个实体类型、876 个关系类型、519 个事件类型** 的大规模代码风格模式库，是目前最大的 UIE 模式库之一。

### 2.2 两阶段学习框架

1. **模式理解阶段（Schema Understanding）**
   - 目标：让模型理解大量概念的定义和实例。
   - 数据：模式定义代码 + 实例代码，实例代码包含“句子 + import 语句 + 实例化语句”，基于 KELM 语料自动构建，约 **15 亿 tokens**。
   - 设计细节：采用“Sentence-First”的 import 位置（先给句子再 import 类），避免模型对重复定义代码过拟合。
   - 训练方式：常规代码预训练（语言建模）。

2. **模式遵循阶段（Schema Following）**
   - 目标：让模型按照给定模式进行抽取。
   - 数据：指令调优代码样本，由“指令代码 + 输入代码 + 输出代码”组成。
    - 指令包括模式定义与任务描述，输入为 `sentence = “...”`，输出为 `results = [...]`。
    - 数据来源：UniversalNER（NER）、InstructIE（RE）、LSEE（EE）。
    - 负类采样：对每个样本额外采样占正类数量 20% 的负类，并构造 5% 的全负样本。
   - 训练方式：LoRA 指令微调。

### 2.3 精炼阶段（Refinement）

- 在人类标注数据集上进行进一步指令微调，统一用代码模式表示。利用数据集名称前缀（如 `from DATASET ACE05`）解决不同数据集对同名概念的标注差异。

## 3. 实验设计

### 3.1 评测场景与数据集

- **Few-shot（模式理解阶段后）**：在 7 个零样本 NER 数据集上使用每类 5 条训练数据作为示例。
- **零样本（Zero-shot）**：
  - NER：CrossNER 的 5 个领域（AI、文学、音乐、政治、科学）+ MIT Movie + MIT Restaurant。
  - RE：GIDS。
  - ED：CASIE。
- **低资源（Low-resource）**：CoNLL03（NER）、CoNLL04（RE）、ACE05 ED、ACE05 EAE，分别使用 1%/5%/10% 的训练数据。
- **监督设置（Supervised）**：使用自建的 KnowCoder Benchmark（由于原始测试集评估成本高，从 18 个 NER 数据集和 8 个 RE 数据集中对每种类型采样，s=14 和 s=4），另加 ED/EAE 的 ACE05 与 CASIE 完整测试集。

### 3.2 对比方法

- **Few-shot**：LLaMA2-7B、LLaMA2-13B。
- **零样本**：无精炼方法（Vicuna-7B/13B、ChatGPT、UniNER-7B）、有精炼方法（InstructUIE-11B、GoLLIE-7B/13B、UniNER-7B refined）。
- **低资源**：UIE-base、LLaMA2-7B 直接微调。
- **监督**：SoTA 列表示此前各数据集的先进结果（来自 UIE、USM、Code4UIE、InstructUIE、GoLLIE、UniNER 等方法），以及 KnowCoder-7B 自身。

### 3.3 评测指标

- 均使用基于边界/触发词/论元匹配的 span-level Micro-F1。

## 4. 资源与算力

- 论文明确提到基础模型为 **LLaMA2-base-7B**。
- 训练框架：Megatron-LM（模式理解）、LoRA（模式遵循与精炼）。
- 超参数：模式理解阶段 context length=2048，学习率 5×10⁻⁶，global batch size=1M tokens，max step=4500；模式遵循与精炼阶段 LoRA rank=32，alpha=64，学习率 3×10⁻⁴，序列长度 4096，batch size=256，训练样本数分别约 510K 与 1.9M。
- **但文中未明确报告 GPU 型号、GPU 数量、训练时长等算力信息**，无法定量评估训练成本。

## 5. 实验数量与充分性

- 实验数量较为丰富，主要覆盖：
  - 4 种评测设置（few-shot、zero-shot、low-resource、supervised）下 33 个具体领域数据集；
  - 大量消融/分析实验：模式导入方式分析（Import-First vs Sentence-First vs Whole）、去除模式理解（w.o. SU）、去除模式遵循（w.o. SF）、去除指导信息（w.o. GI）、类方法来去除实验、负采样消融、提示词风格对比（Code vs IE）、类名对齐影响验证、不同随机种子下的 benchmark 稳定性验证。
- **充分性与客观性**：
  - 比较对象设置较合理，特意区分了是否经过人类数据精炼的基线，避免不公平对比。
  - 存在一定不足：监督设置下 SoTA 基线并非所有方法在统一 benchmark 上重新实现（部分沿用原论文数据），可能存在实现与脚本差异；且评测集合采用采样而非完整测试集，虽然验证了种子稳定性，但依然有精密度损失风险。

## 6. 主要结论与发现

- 模式理解阶段显著提升泛化能力：仅用 5-shot 示例，KnowCoder（SU. only）比 LLaMA2-7B 平均相对提升 **49.8% F1**。
- 零样本设置下，KnowCoder 在 NER 上平均 F1 达 60.1（相对提升 12.5%），超过未精炼基线，甚至优于部分精炼后模型。
- 低资源设置下，KnowCoder 在 1% 比例时平均 F1 相对 UIE 提升 **21.9%**。
- 监督设置下，KnowCoder 在 NER 平均提升 1.1%、RE 平均提升 **7.5%**；在 ED 和 EAE 上首次使得 LLM 基数的方法超过 UIE 等小模型（ED 74.2 vs UIE 73.4；EAE 70.3 vs UIE 69.3）。
- 零样本 ED 上不经过精炼时弱于 GoLLIE（使用人类标注数据训练），但用 ACE05 精炼后 CASIE F1 可达 72.0，超过 GoLLIE 的 59.3（相对提升 21.4%）。
- 人类标注数据精炼对于棘手的任务（如事件抽取）仍很重要。

## 7. 优点与亮点

- **统一且富有表达力的模式表示**：代码天然具备层级、继承、类型约束、可执行后处理，比纯文本或分类标签更能引导 LLM。
- **大而全的模式库与自动构造数据**：基于 Wikidata 构建超过 3 万种概念类型；训练数据全程自动构造，规模可达数十亿 tokens，无需大规模人工标注。
- **两阶段课程式学习设计**：先单独“理解概念”，再“遵循模式”，理解困难与任务分解清晰，实验表明该机制有效。
- **广泛应用于多任务的统一框架**：支持实体、关系、事件检测与事件论元抽取，具有跨任务通用性，且可直接与多个数据集同时精炼。
- 开源 schema library、训练数据、代码及模型，增强可复现性。

## 8. 不足与局限

- **模式库噪声**：模式主要来自 Wikidata，部分概念缺少规范描述/层级，需补充生成（如用 GPT-4），过程可能引入错误。
- **自动构造训练数据噪声大**：基于 KELM 与远程监督方式自动构造，存在标注不完全一致或错误样本的风险。
- **零样本泛化仍有提升空间**：特别是在关系抽取与事件相关任务（不精炼时较弱），说明自动数据不足以完全取代高质量人工数据。
- **评测框架限制**：
  - 监督 setting 使用采样子集作为 benchmark，而非完整测试集（尽管做种子稳定性分析）；
  - 部分 SoTA 基线结果直接引用原始文献，并非全部在同一代码/脚本下重测，可能造成不一致；
  - 只覆盖英文（除个别多语言数据集），跨语言能力未验证。
- **7B 规模模型的指令遵循能力不够强**：论文在研究限制里也承认模型没有指令调优时无法 zero-shot 完成任务，需依赖后续大规模微调。
- **算力与复现成本未披露清楚**，未给出 GPU 数/训练时间等指标，不利于他人评估复现代价。

（完）
