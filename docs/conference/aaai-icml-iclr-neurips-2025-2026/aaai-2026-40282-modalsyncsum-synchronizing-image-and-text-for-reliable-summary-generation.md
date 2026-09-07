---
title: "ModalSyncSum: Synchronizing Image and Text for Reliable Summary Generation"
title_zh: 模态同步摘要：同步图像与文本以实现可靠的摘要生成
authors: "Xuanqi Chen, Ziying Rong, Xinfeng Liao, Yiqian Wu, Bowei Zhang, Pengfei Fu, Shengyi Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40282/44243"
tags: ["query:faithfulness"]
score: 7.0
evidence: 面向多模态摘要生成，通过校验与精炼修正幻觉描述并提升事实准确性
tldr: 面向图文多模态输出摘要任务中大模型常出现幻觉与图文不对齐的问题，论文提出模态同步摘要框架，通过图像感知信息抽取缓解图文错配，借助问题解答式描述校验检测并修正幻觉化的图像描述，再用命名实体引导的细化保证事实准确与实体一致。该方法能够同时增强文本摘要与图像选择的可靠性，为多模态摘要的视觉忠实与事实一致性提供了可复用的处理流程。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态模型在图文摘要任务中常出现幻觉和视觉-文本对齐不足，影响摘要的语义一致性与视觉忠实性。
method: 提出多模态摘要框架，结合图像感知信息抽取、问题解答式描述校验和命名实体引导的精炼模块，消除图文错配与幻觉描述。
result: 该方法能够缓解视觉-文本错位，降低图像描述幻觉，提高实体级事实准确性。
conclusion: 抽取-校验-精炼的统一框架可增强多模态摘要的可靠性，对视觉与文本证据的同步建模有益于忠实摘要生成。
---

## Abstract
Multimodal summarization with multimodal output (MSMO) aims to generate coherent textual summaries while selecting the most semantically relevant images to enhance expressiveness. Despite the advancements of large multimodal models like GPT-4o, LLaMA-3, and Grok-3, these models often exhibit hallucination and weak visual-text alignment when applied to MSMO tasks. To address these challenges, we propose ModalSyncSum, a unified framework that enhances semantic consistency and visual faithfulness.    It incorporates image-aware information extraction to mitigate visual-text misalignment, QA-based description verification to detect and correct hallucinated image descriptions, and named entity-guided refinement to ensure factual accuracy and entity alignment across modalities.   Furthermore, we introduce a new evaluation metric M3AS, which jointly considers image content coverage, text-image alignment, and summary consistency, filling the gap in evaluating multimodal summary quality. Experimental results show that our model outperforms prompt-based baselines across multiple datasets, achieving significant gains on ROUGE, BLEU, and BERTScore, with BLEU improving by 21.95%.  In human evaluation, M3AS exhibits stronger correlation with human judgments in consistency, image-summary relevance, and focus, surpassing existing automatic metrics.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：多模态输出摘要（MSMO）任务旨在同时生成连贯的文本摘要并挑选最相关的图像，以增强信息表达力。尽管GPT-4o、Grok-3、GLM-4v等大规模多模态模型在纯文本摘要上已接近人类水平，但在MSMO任务中仍然面临两个关键问题：
  - **幻觉**：模型常误读视觉内容（如将图像中的"hot pink"识别为"red"），或因文本标题误解而错误推断语义（如从"highness"推断出柬埔寨王室），导致总结内容与真实图像语义矛盾。
  - **弱图文对齐**：生成的文本无法忠实反映视觉信息，暴露出现有模态融合和对齐策略的局限。
- **评估缺陷**：现有自动评估指标（ROUGE、BLEU）主要衡量词元重叠，无法捕捉多模态摘要中的视觉语义；文本一致性指标（如UniEval）在多模态场景下缺乏跨模态一致性评估能力，造成全面的评估盲区。
- **整体含义**：论文通过构建一个不依赖大型模型微调的框架——ModalSyncSum，以及一个新的评估指标M³AS，系统地缓解了上述问题，提升了摘要生成的可靠性和视觉忠实度，并补足了多模态摘要评估角度的缺失。

## 2. 方法论：ModalSyncSum框架与M³AS评估指标

### 2.1 核心思想

ModalSyncSum采用**"抽取-校验-精炼"**的流水线思路，不使用微调，而是通过多阶段验证与迭代修正，将"图像-文本"之间的对齐问题转化为可控的校验步骤。核心在于将图像转化为经过验证的文本描述，将其注入原文增强语义，并利用两轮QA校验确保最终摘要的事实准确性与跨模态一致性。

### 2.2 技术细节与流程

#### 阶段一：生成图像描述（Image-Aware Information Extraction）

- 使用CLIP将文章句子与图像映射到共享语义空间。
- 通过余弦相似度 `sim(si, Ij) = (vsi·vIj)/(‖vsi‖·‖vIj‖)` 筛选与图像相关的句子。
- 设定阈值τ1（=0.3），只保留 `sim(si, Ij) ≥ τ1` 的句子作为图像Ij的参考句集Sj。
- 将Sj输入大型视觉-语言模型（LVLM），生成图像的初始候选描述。

#### 阶段二：图文一致性双重校验（QA-Based Description Verification）

- **CLIP筛选**：为每张图像生成多个候选描述dji，用CLIP计算描述与图像的相似度，过滤低于阈值τ2（=0.4）的描述，保留D^CLIP_j。
- **BLIP问答验证**：从保留下来的每个候选描述中构造有关细粒度视觉属性（衣着、表情、动作、背景物等）的问题Qi，使用BLIP模型基于图像回答：`Bi = BLIP(Ij, Qi)`。
- **一致性判定**：仅保留与BLIP答案在语义上一致的描述，得到DFinal_j。
- **LLM聚合**：通过提示语言模型将高质量描述合并为一个完整且连贯的最终描述d*_j。

#### 阶段三：摘要生成与实体级一致性验证（Named Entity-Guided Refinement）

- 计算每个图像描述d*_j与原文每个句子si的相似度，将描述插入至相似度最高的句子si*之后，形成融合图像上下文的结构化文章Amod。
- 基于Amod使用LLM生成初始摘要y。
- **NER抽取实体**：从摘要中提取命名实体集合E。
- **QA生成与双源回答**：为每个实体自动生成问题qEi，分别从摘要中得到答案a_yi和从原文中得到答案a_Ai，判断两者是否一致：`Consis(qEi) = True(若ayi≈aAi) 否则 False`。
- **迭代修正**：若存在不一致，则提示LLM依据({qEi, aAi})修正摘要，迭代直到所有实体问题均一致。

#### M³AS评估指标

M³AS（Multimodal Triple-factor Assessment Score）从三个维度评估多模态摘要质量：

1. **图像信息分数（Score_img_info）**：融合图像信息覆盖率（Img coverage）与图像信息密度（Img density），公式为几何均值 `sqrt(Img_coverage · Img_density)`，同时衡量图像内容的覆盖程度与摘要中图像信息的浓缩程度。
2. **图文对齐分数（Score_img&sum）**：`sqrt(sim(d*,y) · sim(I,y))`，综合图像描述与摘要、图像与摘要之间的语义相似性，衡量文本与视觉之间的匹配度。
3. **一致性分数（Score_consist）**：基于QA对的关键点正确性（ri）、内容在原文中出现的频率权重（ci）、以及跨模态出现的模态数占比（mi/M），以温度系数δ调节跨模态偏好，衡量摘要与原始图文内容的整体一致性。

最终M³AS为三者加权和：`M3AS = α·Score_img_info + β·Score_img&sum + γ·Score_consist`，默认α=0.25，β=0.25，γ=0.5。

## 3. 实验设计

### 3.1 数据集

| 数据集 | 特点 |
|--------|------|
| MSMO | 源自Daily Mail网站，人工撰写的要点式摘要，由研究生挑选相关图像 |
| M3LS | 多语言多模态摘要数据集，按语言组织，含文章、图像及元数据 |
| E-Liputan | 印度尼西亚语多模态数据集，面向摘要引导的生成式摘要 |

每个数据集随机采样5,000个实例；多语言M3LS采用分层抽样确保语言覆盖均衡。

### 3.2 对比方法

- **传统多模态摘要模型**：Vision-GPLM、VG-GPLMs、Va-SOGM
- **大规模通用模型直接提示（LVLM+Prompt）**：GPT-4o、GLM-4v、Grok-3、Gmini、Doubao-Vision-Pro
- **自有框架**：使用不同LVLM作为基座，将ModalSyncSum应用于GPT-4o、GLM-4v、Grok-3、Gmini、Doubao之上

### 3.3 评估设置

- **自动评估**：ROUGE（R-1/R-2/R-L）、BLEU（B-1/B-2）、BERTScore以及新提出的M³AS
- **人工评估**：15名来自计算机科学、新闻和法律背景的研究生，针对500个随机样本，在Likert 0–4量表上评估4个维度：一致性（Consistency）、流畅性（Fluency）、焦点与覆盖率（Focus&Coverage）、图文相关性（Image-Summary Relevance）

### 3.4 实现细节

- 使用预训练的CLIP计算图文语义相似度
- CLIP-ViT与BERT-SQuAD用于QA验证的一致性检查
- BERT-NER用于命名实体识别
- 阈值设置：τ1=0.3（图像-句子筛选），τ2=0.4（描述-图像过滤）
- M³AS权重：α=0.25，β=0.25，γ=0.5

## 4. 资源与算力

- **论文未明确说明**所使用的GPU型号、数量、训练时长或推理成本。
- 仅提及使用了数据挖掘实验室提供的计算资源，以及使用了预训练模型（CLIP、BLIP、BERT变体、各类LVLM）进行推理级别的验证与生成。
- 由于框架无需微调大型多模态模型，计算负担主要来自多轮LVLM推理（生成描述、摘要、QA验证和修订）以及CLIP/BLIP前向传播，但文中缺少具体的量化算力分析。

## 5. 实验数量与充分性

论文共进行了**六类主要实验**：

| 实验类型 | 具体内容 |
|----------|----------|
| 主要性能实验 | MSMO数据集上对比5种传统方法+5种LVLM直接提示+5种ModalSyncSum增强的LVLM |
| 跨数据集实验 | 在MSMO、M3LS、E-Liputan三个数据集上对比4个代表性模型 |
| 消融实验 | 移除图像一致性校验（w/o ImgC）、移除摘要一致性校验（w/o SumC）、GPT-4o直接图像输入各变体对比 |
| 指标扰动敏感性分析 | 设计4组扰动（修改图像描述细节、替换无关图像、修改摘要细节、原始数据）检验M³AS各子分数的判别力 |
| 超参数搜索 | 对τ1和τ2在0.1-0.5范围内进行组合实验 |
| 人工评估与指标相关性 | 15名评估者、500个样本，验证M³AS与4个人类评价维度的相关系数 |

### 充分性与客观性评价

- **优点**：数据集覆盖英语、多语言（M3LS）、印尼语（E-Liputan），具有一定泛化性验证；消融实验完整地验证了各模块的贡献；M³AS的扰动实验证明了其能识别不同类型错误；人工评估从多学科角度进行。
- **不足**：
  - 主要性能表（表1）仅展示了MSMO上的详细对比，跨语言数据集上的对比仅包含有限模型（未列出全部LVLM基线）。
  - 表3消融实验存在格式错误标识（文中引用为"Table ??")，说明论文在最终排版校对上有疏漏。
  - 表1中**GPT-4o直接提示的R-1等指标明显低于传统方法**，与传统常识（当前LVLM在摘要ROUGE上已接近SOTA）有出入，但对这一倒挂现象的解释不够充分。
  - 论文表1中传统模型表现出比LVLM更高的ROUGE，作者的解释（"表面层面分歧大、但语义准确度更高"）不够有力，可能存在数据集分布或提示方式的偏差。
  - M3AS与Fluency相关性较低（0.46），说明该指标在评估语言流畅度方面不足。

## 6. 主要结论与发现

- **框架有效性**：ModalSyncSum显著提升了LVLM在多模态摘要任务中的表现。平均而言，相比直接提示方法，R-1提升21.3%、R-2提升14.7%、R-L提升15.4%、B-1提升18.1%、B-2提升25.8%、BERTScore提升7.8%、M³AS提升23.5%，其中BLEU最大提升达21.95%。
- **直接图像输入可能有害**：消融实验表明，GPT-4o直接输入图像（GPT-4o(Img)）的表现甚至劣于纯文本GPT-4o，说明缺乏任务对齐的LVLM直接处理多模态输入会导致质量下降；而ModalSyncSum相比GPT-4o(Img)在R-1上+12.7、在M³AS上+6.5。
- **一致性校验模块具有重要作用**：单独去掉图像一致性（w/o ImgC）或摘要一致性（w/o SumC）校验都会导致明显的性能退化，验证了QA反馈机制对减少幻觉和增强对齐的价值。
- **M³AS指标的有效性**：M³AS与人工评估具有极强的相关性——Consistency（0.9588）、Image-summary relevance（0.9221）、Focus&Coverage（0.8672）——显著超越ROUGE、BLEU和BERTScore等传统指标，说明M³AS能更好地反映人类对多模态摘要质量的判断。
- **跨语言泛化性**：在M3LS（多语言）与E-Liputan（印尼语）上，ModalSyncSum虽然词汇指标略低于英语MSMO，但BERTScore和M³AS表现依然突出，证明其具有语言无关的多模态理解能力。
- **阈值选择是关键**：τ1=0.3与τ2=0.4为最优设置，过高或过低都会损害摘要质量与图文一致性。

## 7. 优点

- **无需微调大型模型**：框架构建于推理和提示之上，成本可控、可适配任意LVLM，工程实用性强。
- **多阶段冗余验证机制**：CLIP相似度过滤 + BLIP问答验证 + NER引导的QA修订形成三重保障，有效降低图像描述中的幻觉，在方法上具有较强的系统性和鲁棒性。
- **创新性地将图像"文本化"**：通过将图像内容转化为经过验证的文本描述再插入原文的方法，巧妙地规避了LVLM在处理"图像-长文本"融合时面临的对齐困难。
- **补足了多模态摘要评估的空白**：M³AS创新地融合了图像信息覆盖率、图文语义对齐和内容一致性三个视角，摆脱了传统文本指标无法评估视觉内容的局限，且实验证明与人类判断高度一致。
- **扰动敏感性分析严谨**：通过设计4类扰动场景验证了M³AS各子分数的判别能力，表明该评估指标具有可靠的诊断功能。
- **实验范围较广**：覆盖英语、多语言、低资源语言三种数据集类型，验证了框架在跨语言场景下的一般适用性。

## 8. 不足与局限

- **表面词汇指标提升有限**：在MSMO数据集上，ModalSyncSum相比传统方法（如Va-SOGM）在R-1、R-2上的绝对分数并不占优，作者解释为表面差异大但语义对齐好，然而ROUGE与M³AS之间的张力未得到更深入的分析。
- **跨语言性能偏低**：在M3LS和E-Liputan上，R-1和R-2等指标相比传统方法有时仍有差距，因为多模态预训练模型在低资源语言上的支持有限，论文未能提出针对性的语言适配方案。
- **指标Fluency相关性偏弱**：M³AS与人类评价的Fluency仅有0.46的相关性，说明该指标对语言流畅性和可读性的评判能力不足，一个完整的评估体系仍需补充语言质量维度。
- **论文存在格式错误**：表3引用出现占位符未替换（"Table ??")，在表1与表3间也存在数字不一致（如GPT-4o B-1在表1中为18.15%，在表3中为20.15%），在一定程度上影响论文的严谨性。
- **缺少误差分析**：未对失败案例进行系统性分析，例如在什么类型的图像或文本上ModalSyncSum仍然会出错、QA验证在什么场景下会失效等。
- **算力成本披露不足**：虽然免微调，但多轮LVLM推理（生成描述→聚合→生成摘要→修订）在真实场景中需要多次大模型调用，论文未讨论实时性、API成本或推理效率问题。
- **人工评估覆盖面有限**：15名评估者和500个样本来自英语MSMO单一数据集，评估结果可能无法完全泛化到其他语言场景。
- **信息泄漏风险**：M³AS的计算需要用到图像描述DFinal_j以及答案匹配逻辑，如果图像描述本身包含一定噪声或者评估过程中使用的模型与生成过程中一致，可能导致评估偏差。此外，评估者均为单一机构的研究生，可能存在评分偏差。

（完）
