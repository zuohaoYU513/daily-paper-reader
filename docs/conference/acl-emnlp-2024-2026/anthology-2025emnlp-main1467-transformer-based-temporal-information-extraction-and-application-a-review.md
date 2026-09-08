---
title: "Transformer-Based Temporal Information Extraction and Application: A Review"
title_zh: 基于Transformer的时间信息抽取与应用综述
authors: "Xin Su, Phillip Howard, Steven Bethard"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1467.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 对基于Transformer的时间信息抽取进行综述，直接服务跨句时间信息与时间线抽取
tldr: 时间信息抽取旨在从非结构化文本中提取结构化时间信息，还原文档隐含的时间线。该综述系统梳理基于Transformer的预训练语言模型在这一任务上的研究进展，包括任务形式、模型方法与医疗、新闻、情报等应用。文章还指出现有综述缺乏的问题并展望未来方向，为跨句时间信息抽取与时间演化追踪研究提供了系统地图。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1467/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1467/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 799, \"height\": 590, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1467/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1666, \"height\": 1638, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1467/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1632, \"height\": 1754, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1467/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 1083, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1467/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1483, \"height\": 357, \"label\": \"Table\"}]"
motivation: 尽管Transformer在时间信息抽取上取得很大进展，但该方向仍缺乏系统性综述。
method: 采用综述方法梳理基于Transformer的时间抽取模型架构、任务设定及在医疗等领域的应用。
result: 系统呈现了时间信息抽取的技术版图，并指出当前研究空白与潜在发展方向。
conclusion: 基于Transformer的时间信息抽取已显著推进时间线发现，仍需在复杂时间结构上继续探索。
---

## Abstract
Temporal information extraction (IE) aims to extract structured temporal information from unstructured text, thereby uncovering the implicit timelines within. This technique is applied across domains such as healthcare, newswire, and intelligence analysis, aiding models in these areas to perform temporal reasoning and enabling human users to grasp the temporal structure of text. Transformer-based pre-trained language models have produced revolutionary advancements in natural language processing, demonstrating exceptional performance across a multitude of tasks. Despite the achievements garnered by Transformer-based approaches in temporal IE, there is a lack of comprehensive reviews on these endeavors. In this paper, we aim to bridge this gap by systematically summarizing and analyzing the body of work on temporal IE using Transformers while highlighting potential future research directions.

---

## 论文详细总结（自动生成）

# 基于Transformer的时间信息抽取与应用综述：详细中文总结

## 一、论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：时间信息抽取（Temporal Information Extraction, Temporal IE）旨在从非结构化文本中提取结构化时间信息，揭示文档中隐含的时间线，帮助下游任务（如时间推理、时间线摘要、时序问答）以及人类用户更好地理解文本内容随时间的演变。
- **背景缺位**：Transformer架构（尤其是BERT、RoBERTa、T5以及近年的生成式大语言模型如GPT-4、LLaMA3）在NLP多个任务上取得了突破性进展，在时间信息抽取领域也已有大量工作。然而，既有综述（如 Lim et al., 2019; Leeuwenberg and Moens, 2019; Alfattni et al., 2020; Olex and McInnes, 2021）主要聚焦于规则系统或传统机器学习模型，或仅局限于临床领域；缺乏一篇系统、综合地梳理Transformer在时间信息抽取中应用的综述。
- **论文目标**：本文填补这一空白，系统梳理、总结并分类基于Transformer的时间信息抽取方法、数据集与应用，同时指出研究缺口和未来研究方向。综述聚焦于TimeML框架中定义的三个核心任务：时间表达式识别、时间表达式规范化、时间关系抽取。

## 二、论文提出的方法论（综述框架与核心结构）

> 说明：本文是一篇综述论文，不提出新的技术方法，而是对现有文献进行系统化梳理与分类。其“方法论”体现在综述的组织框架与分析维度上。

- **综述三个核心子任务**：
  1. **时间表达式识别**：识别文本中的时间点、时间段和周期（如"February 25, 2024"、"three days ago"）。
  2. **时间表达式规范化**：将识别出的时间表达式转换为标准化格式（如ISO-TimeML的TIMEX3格式）。
  3. **时间关系抽取**：识别事件与事件、事件与时间表达式之间的时序关系（如before、after、simultaneous）。
- **数据集综述体系**：将32个数据集分为两大类：
  - **TimeML框架及其变体数据集**：如TimeBank、TempEval系列、各语言TimeBank（法语、西班牙语、葡萄牙语、日语、意大利语、韩语）、THYME临床数据集、i2b2-2012、MATRES、TimeBank-Dense、TDDiscourse等。
  - **其他标注框架数据集**：如WikiWars（TIMEX2）、SCATE、CaTeRS、TORDER、Temporal Dependency Tree/Graph等。
  - 分析维度包括：领域（新swire、临床、Wikipedia、叙事、论坛等）、语言覆盖（15种语言）、标注任务类型。
- **时间表达式方法综述**：以BERT等Transformer编码器作为骨干模型，将识别任务建模为Token分类；少数工作采用生成式（encoder-decoder）；规范化任务则常采用MLM微调或多分类方式（如按小时分类）。
- **时间关系抽取方法综述**：将现有方法分为判别式与生成式两类：
  - **判别式方法**：细分为外部知识集成（常识知识、句法语义知识、时间规则、标签分布）和鲁棒性增强（多任务学习、数据增强、继续预训练、对抗训练、自训练）两大阵营。
  - **生成式方法**：一类是微调encoder-decoder模型（BART/T5）；另有一类是面向LLM的提示方法（如ChatGPT），以及借助ILP进行全局约束优化、零样本一步生成整篇文档时序图的尝试。
- **应用综述体系**：梳理时间IE系统在时间线抽取、时间线摘要、时间问答等下游任务中的应用方式（直接拼接图、注意力融合、图神经网络编码等）。
- **方法论对比框架**（Appendix H）：系统对比了各类时间关系抽取方法（常识集成、句法/语义集成、时间规则约束、鲁棒性增强、生成式）的优缺点，并对比了判别式与生成式方法的性能、效率、数据需求、灵活性和可解释性。

## 三、实验设计（数据与基准）

> 作为综述，本文未报告具体的实验设计和自身实验结果，但系统归纳了时间信息抽取领域各类模型被评测的高频基准。

- **常用时间关系抽取基准**：
  - MATRES（274篇文档）
  - TimeBank-Dense（36篇文档）
  - TDDiscourse（34篇文档）
- **其他重要数据集**：
  - THYME系列（临床领域）：SemEval-2015/2016/2017 Clinical TempEval
  - i2b2-2012（临床文本）
  - TimeBank/TempEval共享任务系列
  - 各语言TimeBank数据集（法语、西班牙语、葡萄牙语、日语、意大利语、韩语等）
  - Richer Event Description、CaTeRS、Event StoryLine等
- **时间表达式识别/规范化基准**：TimeBank、TempEval、WikiWars、SCATE、German Temporal Expression、PATE等。
- **评估指标**：以TempEval-3标准为主，计算精确率、召回率和F1值；针对时间关系抽取，需进行图闭包操作后计算时间感知得分。
- **评测中的公平性/同质化问题**：绝大多数时间关系抽取工作仅用MATRES、TimeBank-Dense和TDDiscourse三个数据集评测，它们规模小且存在重叠、集中于新闻领域，模型可泛化性证据不足。

## 四、资源与算力

- 该论文是综述文章，**未报告自身实验所需的算力资源**（如GPU型号、数量、训练时长等）。
- 论文提及：大多数现有时间关系抽取模型**未公开可用**（如表2的"Avl"列所示），即使代码公开，也往往需要在新数据集上重新训练，涉及大量复制工作，这是复现成本高的原因之一。
- 部分被综述的工作提及了模型规模（如基于BERT/RoBERTa、多语言XLM-R、BART/T5等），但对具体训练硬件配置未在综述中汇总。

## 五、实验数量与充分性分析

- 作为综述，本文涵盖了对现有工作的宏观整合与分析：系统整理了**32个数据集**（覆盖15种语言、多个领域），梳理了大量时间关系抽取方法（超过40个代表工作），从方法层面做了系统分类。
- **领域偏差分析**：在32个数据集中，有20个（63%）以新闻为主，领域高度同质化；跨域的Clinical TempEval 2017显示，任务跨域后性能普遍下降约20个百分点。
- **规模偏小的风险**：最常用的三个时间关系基准（MATRES、TimeBank-Dense、TDDiscourse）合计仅344篇文档，比同类NLP语料小1~2个数量级；TimeBank-Dense单篇文档占全数据集近3%，指标易于受个别标注影响；超参调整容易过拟合。
- **评测不统一**：不同工作在计算F1时存在差异（如有的只评估"before/after"两类，有的排除"vague"类），导致横向对比不够公平。
- **综述覆盖面评价**：本文覆盖面较广，大量内容以表格形式（涵盖模型基础、知识引入、鲁棒性、可用性）系统地综合了工作。但深层分析有限，尤其在生成式LLM方向，相关成果多为初步尝试。
- **整体实验充分性结论**：综述揭示了现有研究方法的严重同质化，模型之间的SOTA小幅提升可能更多来自超参调整而非实质方法进步；现有评测无法充分验证模型泛化能力。

## 六、论文的主要结论与发现

1. **领域偏倚严重**：现有数据集以新闻领域占绝对主导（63%），跨域迁移性能显著下降，制约系统泛化能力；丰富领域多样性是当务之急。
2. **语言多样性充足但还有不平衡**：现有数据集已覆盖15种语言（如英、中、德、荷、西、法、意、阿、越、日等），不同语言对时间概念的切分（如"夜晚"与"傍晚"）存在文化差异，多语言时间IE值得继续关注。
3. **多种标注框架停滞不前**：除TimeML及其小幅扩展之外，缺乏新的端到端标注框架探索；已有时间图难以独立解释，实际应用局限于将时间图作为辅助信息。
4. **时间表达式识别与规范化方法同质化**：大量工作采用BERT的Token分类或MLM范式；生成式LLM在该任务上的潜力基本未展开。
5. **生成式LLM尚无法超越判别式方法**：多项工作中生成式（特别是提示式）的绝对性能仍不如微调的判别式模型；但其灵活性、零样本能力在小规模数据和可解释应用场景中具备潜在价值。
6. **时间关系抽取整合知识仍是主流策略**：引入外部常识、句法/语义、时间规则与标签分布知识的做法比较普遍，但由于数据特点不突出，各方案差异不大。
7. **模型公开度低限制应用**：多数模型不公开，导致下游任务很难复现和应用这些系统；从短期看，缺乏公开框架与隐蔽测试集也阻碍研究公平比较与产业落地。
8. **应用长期停留在辅助层面**：时间图或时间信息管线多作为文本加工后的附加特征用于下游时序推理任务；服务人类、特别是可视化和交互设计方面仍很薄弱。
9. **数据与评测口径不统一**：构建公开的、测试集隐蔽的基准与统一的评估处理方法对公平比较非常重要。

## 七、优点

- **综述视角全面**：覆盖了从任务定义、时间标注框架、到两大主流建模范式（判别式 vs. 生成式）、再到下游应用的系统性全链路，并附有方法对比表与数据集摘要表（含30+数据集与40+模型）。
- **客观性较好**：对SOTA提升的实质贡献提出质疑，明确指出方法同质化问题与评测基准集中化风险；也公正指出生成式方法目前性能低但潜力广阔。
- **深入揭示数据隐患**：打破了不少研究中对新闻语料的依赖意识，用数据指出跨域性能下降的实际问题，使模型可泛化性得到重视。
- **实践导向强**：关注模型的公开可用性、复现成本、公平评测与HCI角度下的人本需求，这些在学术综述中较少被系统讨论。
- **从多维度建议未来方向**：明确给出框架扩展、数据多样性、生成式LLM、公共工具与评测基准、人机交互可视化的未来研究路线（对比此前文献更具体且具有可操作性）。
- **领域历史连接较好**：与早前综述相比，将新旧时代、多语言及多领域的信息进行了合理整合（如把规则系统HeidelTime等置于Transformer背景下说明）。

## 八、不足与局限

- **综述范围局限**：仅关注Transformer类方法，没有覆盖规则系统或传统机器学习方法，相关方法的价值总结相对缺失；事件触发词抽取也未作为独立任务纳入分析（作者将此归因于该方向缺少独立的研究）。
- **深层对比不足**：虽然建立了分类框架，但对不同方法（如多任务与数据增强或外部知识图网络等）之间的实际性能对比与参数影响没有开展量化分析，对性能的批评缺乏实验证据支撑。
- **数据集偏差风险**：自身综述中的多数时间关系抽取方法集中在三个偏小的新闻数据集与临床数据集间的比较，评价标准也未必统一——部分工作只对二分类计算得分，导致横向比较存在公平性问题。
- **LLM前沿方向资料有限**：生成式语言模型的各类新型应用（尤其是强化学习、上下文学习消融方式、大模型评估细节）尚处早期，综述只能给出方法论上的悬念；相关推论具有高度时效性，未来容易过时。
- **标注属性讨论不够完全**：对不同框架中的规范化粒度与语义组成差异（如SCATE与TimeML的实际兼容性）讨论较浅，对时间关系标签体系的闭包规则和评估共识也未充分详细比较。
- **缺乏更细致的应用生态分析**：对已应用系统的质量、延迟等生产成本描述有限；对于未公开的模型，未能论述其训练中所用额外预处理语料的差异性对齐。

（完）
