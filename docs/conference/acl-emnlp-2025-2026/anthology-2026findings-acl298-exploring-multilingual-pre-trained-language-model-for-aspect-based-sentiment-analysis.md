---
title: Exploring Multilingual Pre-trained Language Model for Aspect-based Sentiment Analysis
title_zh: 探索多语言预训练模型用于方面级情感分析
authors: "Ye Wang, Ruijun Jiang, Zhongqing Wang, Guodong Zhou (周国栋)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.298.pdf"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 研究多语言预训练模型用于方面级情感分析，直接贡献于NLP情感分析技术
tldr: 方面级情感分析多集中于英语，其他语言数据稀缺。本文提出跨语言知识融合框架，利用多种单轮和两轮双语预训练配置，融合原始和翻译文本，以提升多语言场景下的ABSA性能。研究为多语言情感分析提供了有效预训练策略，可迁移至金融情感分析等应用。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl298/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 560, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl298/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1242, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl298/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1181, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl298/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1431, \"height\": 763, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 748, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 665, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1637, \"height\": 688, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1527, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1384, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 807, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1479, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl298/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 485, \"height\": 378, \"label\": \"Table\"}]"
motivation: 方面级情感分析标注数据稀缺，多语言资源未被充分利用。
method: 提出跨语言知识融合框架，探索双语预训练配置以融合原语种与翻译语料。
result: 在多种语言上验证了框架的有效性，改善了多语言ABSA性能。
conclusion: 跨语言预训练可缓解低资源情感分析数据不足问题。
---

## Abstract
Aspect-based sentiment analysis has garnered increasing attention in the research community; however, most studies have predominantly focused on English datasets, with other languages such as Chinese, Japanese, and German being neglected due to the limited availability of adequately labeled data. Even within English, labeled data is scarce. To address these challenges, this study investigates the utilization of a multilingual pre-trained setting to leverage resources from diverse languages for aspect-based sentiment analysis. Specifically, we propose a Cross-lingual Knowledge Fusion framework that explores various single-round and two-round bilingual pre-training configurations. This framework utilizes both the original and translated texts, along with their corresponding labels, to pre-train the multilingual model. Evaluation results reveal that our model significantly outperforms state-of-the-art performance across multiple languages, highlighting the effectiveness of the proposed multilingual pre-trained language model for aspect-based sentiment analysis.

---

## 论文详细总结（自动生成）

以下是基于论文内容的详细中文总结：

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：方面级情感分析（ABSA）是细粒度情感分析任务，旨在识别文本中特定方面的情感信息。然而，现有研究大多集中在英语数据集上，中文、日语、德语等其他语言因缺乏充足标注数据而被忽视；即使是英语，由于每条评论需要标注四元组（aspect, opinion, category, polarity），标注成本高，数据也非常有限，导致模型性能受限（英语平均F1值甚至低于50%）。
- **整体含义**：本文旨在探索多语言预训练设置，利用不同语言的资源来增强ABSA性能。核心思想是通过跨语言知识融合，整合多种语言信息和语义关联，缓解低资源语言数据稀缺问题，并提升英语本身的模型表现。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

本文提出**跨语言知识融合框架（CKF, Cross-lingual Knowledge Fusion）**，整体流程如下：

- **第一阶段：翻译原始评论文本**
  - 利用大语言模型（LLM）将源语言评论文本翻译成多种目标语言（中、日、德等），采用**十样本提示（ten-shot prompting）**方法，确保翻译质量并保持标签对齐。
  - 提示模板明确要求模型翻译句子和对应标签，并保持翻译文本中标签的对齐关系。

- **第二阶段：双语预训练**
  - **单轮双语预训练配置**：
    - 翻译配置（TS→TT 和 TT→TS）：源语言与目标语言间的双向翻译。
    - 句子到标签配置（TS→YS 和 TT→YT）：将句子映射为其标签。
    - 翻译句子到标签配置（TS→YT 和 TT→YS）：跨语言标签分配。
    - 标签到句子配置（YS→TS 和 YT→TT）：从标签生成句子。
    - 翻译标签到句子配置（YT→TS 和 YS→TT）：实现跨语言标签与句子的映射。
  - **两轮双语预训练配置**：
    - 翻译融合（Translation Fusion）：整合 TT→TS 与 TS→TT。
    - 单语重建融合（Monolingual Reconstruction Fusion）：整合 YT→TT 与 YS→TS。
    - 跨语言重建融合（Cross-lingual Reconstruction Fusion）：整合 YT→TS 与 YS→TT，**这是论文最终采用的方案**。

- **第三阶段：方面级情感分析微调**
  - 采用基于Transformer编码器-解码器的序列到序列模型，将情感元素线性化为输出序列。
  - 输入序列 x → Encoder 得到隐藏向量 H = Encoder(x1, ..., x|x|)；Decoder自回归生成每个输出token：yi, hdi = Decoder([H; hd1, ..., hdi−1], yi−1)；整个输出序列的条件概率为：p(y|x) = ∏_{i=1}^{|y|} p(yi|y<i, x)。

- **双语训练与模型融合**：
  - 分别独立预训练源语言和目标语言模型（参数为θS和θT）。
  - 使用**LoRA（低秩适应）**方法计算低秩更新：θ′T = θT + ∆θT，θ′S = θS + ∆θS。
  - 加权合并参数：θFusion = αT·θ′T + αS·θ′S。
  - 通过加权任务损失最小化进行轻量适应：LFusion(θ) = Σ_t λ_t Σ_{(x,y)∈D_t} loss(fθ(x), y)，仅优化LoRA更新参数。

## 3. 实验设计：数据集、benchmark、对比方法

- **数据集**（涉及四种语言、不同领域）：
  - **英语**：ACOS数据集的laptop领域（2,934训练/816测试，2,934个四元组）。
  - **中文**：混合中文CCD数据集（2,798训练/799测试，11,463个四元组）。
  - **日语**：chABSA数据集的経済领域（2,566训练/642测试，6,230个四元组）。
  - **德语**：MobASA数据集的交通领域（3,119训练/1,028测试，3,572个四元组）。
  - 每个数据集按90%/10%划分训练集和验证集。

- **任务设置**：
  - 英语和中文：Aspect-Sentiment-Quad Prediction任务（四元组预测）。
  - 日语和德语：Target Aspect Sentiment Detection任务。
  - 基础模型：LLaMA-8B-Instruct（具体为Meta-Llama-3-8B-Instruct），使用Adam优化器（学习率3e-4，batch size 16，训练10个epoch），在单张NVIDIA RTX 4090 GPU上进行，每个结果取10次随机初始化运行的平均值。
  - 评价指标：结构完全匹配的Precision、Recall和F1值。

- **对比方法**：
  - **分类模型**：TAS-BERT、Extract-Classify。
  - **预训练生成模型**：GAS、Paraphrase、Seq2Path、MvP、Seq2Seq w/ CD、LACA*。
  - **大语言模型**：DeepSeek-V3、ChatGPT-5（十样本设置）、LLaMA-3.1-8B（LoRA微调）、Qwen-2.0-7B（LoRA微调）。

## 4. 资源与算力

- 文中明确说明所有实验在**单张NVIDIA RTX 4090 GPU**上完成。
- 训练时间（附录B）：
  - 基础模型LLaMA-3.1-8B：英语约41.50分钟，中文约64.57分钟，日语约56.08分钟，德语约46.54分钟。
  - 论文最终模型（Ours）：英语约129.84分钟，中文约190.48分钟，日语约160.42分钟，德语约155.42分钟。
- 峰值GPU显存：所有模型显存使用在18,241 MiB ~ 23,655 MiB之间，最终模型峰值显存与基线基本相当（没有额外增加模型参数或显存密集组件）。
- 计算成本增加主要来源于双语数据和多轮预训练带来的训练迭代次数与数据处理量增加。

## 5. 实验数量与充分性评估

论文进行了多组实验，数量和覆盖度较为充分：

- **主实验**：在英语、中文、日语、德语四种语言上对比了十几个基线模型，验证了整体有效性。
- **预训练方法消融**（表3）：系统比较了全部5类单轮配置（10种方向）和3类两轮融合配置，覆盖所有设计空间，验证了每个配置的贡献。
- **目标语言影响分析**（表4）：分别以英语、中文、日语、德语为源语言，考察不同目标语言组合的迁移效果（单个和成对组合）。
- **翻译质量分析**（表5）：对比Qwen-Plus、LLaMA-3.1-8B、ChatGPT-4o-mini和自己模型的翻译BLEU分数与下游任务F1，并人工标注500条参考翻译。
- **多语言集成方法对比**（表6）：与MultiInput、MultiOutput、MultiInOut等方法比较。
- **案例分析**（附录A）：两个具体实例展示跨语言信息如何修正错误分类。
- **计算成本分析**（附录B）：对比训练时间和显存。
- **NER泛化实验**（附录C）：在CoNLL-2003上对比Qwen-plus、DeepSeek-v3、ChatGPT-4o-mini、T5-base、LLaMA-3.1-8B。

**充分性评估**：总体上实验设计系统、覆盖全面，消融实验完整，包含多语言、多方法、多角度分析。主实验和消融实验均报告了统计显著性（p<0.05）。但存在某些不足：未报告跨不同随机种子的方差/标准差；仅采用LLaMA-8B-Instruct一个基础模型，未验证框架在其他规模模型上的通用性；消融实验以中文为目标语言，未在其他语言上验证所有配置。

## 6. 论文的主要结论与发现

- **多语言预训练显著有效**：提出的CKF框架在所有四种语言上均显著优于基线（p<0.05），英语F1达46.51（普通单语模型仅43.34），中文77.25，日语72.18，德语83.49。
- **跨语言预训练优于单语**：所有双语预训练配置均优于单语ABSA基线（日语+74.25→44.48除外不明显），验证了跨语言知识融合的有效性。
- **两轮融合优于单轮**：跨语言重建融合（Ours）组合了YT→TS和YS→TT两个方向，效果最佳，优于单轮及另外两种融合方案。
- **语言相似性影响迁移效果**：以英语为源语言时德语迁移最好（类型学相似）；日语和中文单独迁移效果一般，但组合使用反而取得最高F1，说明类型学远语言可提供互补信号；相似与远距离语言混用可能产生干扰。
- **翻译质量与下游性能正相关**：模型质量越高（BLEU分数越高），下游ABSA性能越好。
- **跨语言预训练的泛化能力**：在NER任务上同样显著超越基线（F1=82.00 vs. LLaMA-3.1-8B的79.13），说明框架具备一定的通用性。

## 7. 优点

- **问题选择有实际意义**：聚焦多语言ABSA数据稀缺问题，尝试利用丰富语言资源帮助低资源语言，研究角度新颖且具有应用价值。
- **框架设计系统全面**：系统性地设计了多种单轮和两轮预训练配置，形成完整的设计空间探索，覆盖了翻译、标签映射等多类跨语言语义对齐任务。
- **利用LoRA实现参数高效融合**：通过LoRA低秩更新和加权参数合并，在不显著增加显存的前提下实现双语知识融合，兼顾性能与效率。
- **标签感知的翻译策略**：在翻译阶段就要求保持标签对齐，确保下游监督信号不被翻译破坏，这一细节设计体现任务感知特点。
- **充分的对比实验**：覆盖分类模型、生成模型、大语言模型等不同类别基线（包括ChatGPT-5、DeepSeek-V3等流行LLM），并进行了多角度消融和分析。
- **广泛的验证场景**：除主任务外还验证了NER泛化能力，说明方法具有一定通用性。

## 8. 不足与局限

- **仅使用单一基础模型**：所有实验基于LLaMA-8B-Instruct，未验证框架在更大/更小或不同架构模型上的适用性，结论的普适性有限。
- **翻译依赖与人工成本**：高质量翻译需要人工验证，增加了时间消耗和人工成本；论文使用LLM进行翻译可能引入噪声，影响跨语言标签对齐质量。
- **数据规模有限**：四种语言的数据集规模较小（训练集约2,500~3,100条），领域各不相同（笔记本、混合、经济、交通），无法完全排除数据领域差异对结果的干扰。
- **实验配置不对称**：不同语言采用不同任务（英语/中文四元组预测，日语/德语TASD），跨语言对比的公平性有待商榷；消融实验仅以中文为目标语言，可能存在语言偏向。
- **标签组合的探索有限**：虽然在目标语言影响分析中测试了成对组合，但未探索三种以上语言同时融合的效果，无法确定最优语言组合策略。
- **未报告方差与错误分析**：缺少多次运行的标准差/方差报告，以及系统性的错误分析（除两个案例分析外）。
- **计算开销较大**：多语言预训练增加了训练时间（约为基线的2~3倍），扩展到更多语言时资源受限环境下面临挑战。
- **LoRA融合策略较简单**：加权求和（αT·θ′T + αS·θ′S）的融合方式较为朴素，可能不是最优的参数融合策略，论文未比较其他融合方法（如基于插值、Fisher加权、SVD融合等）。

（完）
