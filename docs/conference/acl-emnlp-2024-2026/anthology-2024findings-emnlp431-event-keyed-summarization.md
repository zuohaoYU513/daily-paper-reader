---
title: Event-Keyed Summarization
title_zh: 事件键式摘要：结合文档级事件抽取的摘要生成任务
authors: "William Walden, Alexander Martin, Pavlo Kuchmiichuk, Aaron Steven White"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.431.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 将文档级事件抽取与事件摘要结合，并构造MUCSUM评测基准
tldr: 事件键式摘要将传统摘要与文档级事件抽取结合，目标是给定文档和已抽取事件结构为事件生成上下文摘要。作者基于MUC-4构建了包含全部事件摘要的MUCSUM基准，并对预训练模型和前沿模型进行基线评测。实验表明，将任务退化为普通摘要或结构到文本都会降低目标事件摘要质量，说明该基准能够有效评测事件结构在生成中的价值。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp431/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp431/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 533, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp431/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp431/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 572, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp431/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 708, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp431/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1250, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp431/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 248, \"label\": \"Table\"}]"
motivation: 现有摘要难以按指定事件生成上下文相关总结，事件结构未被充分利用。
method: 提出事件键式摘要任务，输入文档与事件结构、输出事件上下文摘要，并构建MUCSUM基准。
result: 对比实验显示普通摘要或结构到文本均弱于事件键式建模，MUCSUM评测稳定。
conclusion: 该基准可推动事件结构和摘要生成相结合的研究方向。
---

## Abstract
We introduce *event-keyed summarization* (EKS), a novel task that marries traditional summarization and document-level event extraction, with the goal of generating a contextualized summary for a specific event, given a document and an extracted event structure. We introduce a dataset for this task, MUCSUM, consisting of summaries of all events in the classic MUC-4 dataset, along with a set of baselines that comprises both pretrained LM standards in the summarization literature, as well as larger frontier models. We show that ablations that reduce EKS to traditional summarization or structure-to-text yield inferior summaries of target events and that MUCSUM is a robust benchmark for this task. Lastly, we conduct a human evaluation of both reference and model summaries, and provide some detailed analysis of the results.

---

## 论文详细总结（自动生成）

## 《事件键式摘要》论文详细总结

### 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：传统事件抽取（Event Extraction, EE）虽然以"响应特定用户信息需求"为初衷，但在正式建模中通常只关注事件结构指标，缺乏面向实际用户信息获取的考虑；传统摘要通常面向"读者平均关注点"生成，难以针对某个特定事件进行定制化描述。
- **核心问题**：如何将事件抽取（事件中心结构信息）与文本摘要（自然、可读、上下文化描述）相结合，使用户能基于一篇文档以及一个已有的事件结构，获得该特定事件的、情景化且信息完整的摘要？
- **整体含义**：作者提出 **事件键式摘要（Event-Keyed Summarization, EKS）** 这一新任务，将传统摘要生成与文档级事件抽取"联姻"，以事件类型和角色映射为条件，生成目标事件的短摘要，以此在事件结构与概括性文本表达之间建立桥梁，推动面向事件结构的人类中心式文本生成研究。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **任务定义**：
  - 定义事件本体为三元组 $\langle E, R, S\rangle$， $E$ 为事件类型集合， $R$ 为角色类型集合， $S$ 将每个事件类型映射到相关角色类型集合。
  - 查询事件被定义为 $\langle E, R \rangle$，其中 $E$ 为事件类型（配合若干事件触发器）， $R$ 为将角色类型映射到角色填充词组的函数。
  - **EKS 任务**：输入一篇文档 $D$ 和一个查询事件 $\langle E, R \rangle$，期望生成远短于原文的摘要 $S$，传达且仅传达文档中与该事件相关的信息；相关性由该事件类型对应的角色集合 $S(E)$ 决定。
- **MUCSUM 数据集的构建（以 MUC-4 为基础）**：
  - 基于经典 MUC-4 模板抽取语料；文档涉及拉丁美洲多国政治冲突，事件类型有 6 种：arson, attack, bombing, kidnapping, robbery, forced work stoppage；
  - 除学术界常用的 5 个角色（PerpInd, PerpOrg, Weapon, Victim, Target）外，额外加入 StageOfExecution（事件是实际发生、企图还是威胁）、以及可从文本中提取的 Date 与 Location；
  - （要点）作者采用"先生成后编辑"的半自动标注方法：首先用 ChatGPT（gpt-3.5-turbo）针对文档+事件信息生成不超过 3 句的候选摘要，然后人工逐条编辑修正；与标准 MUC-4 模板不同，MUCSUM 的训练/开发集仅包含有非空事件文档，共 1,300+200 篇文档、1,114+191 个事件摘要；测试集保留隐藏。
- **基线评测方法**：
  - 三个主模型为 BART-large、PEGASUS-large、T5-large；
  - 输入为文档文本与线性化事件模板的拼接，模板各角色用特殊分隔符标记；
  - 为对照结构到文本与传统摘要两种简化情形，分别做仅事件模板输入和仅文档输入两个消融；
  - 另使用 ChatGPT（gpt-3.5）与 GPT-4 做零样本提示评测，多提示平均并报告结果。
- **评价指标**：ROUGE-1/2/L、BERTScore、CEAF-REE F1（利用能抽取摘要中角色论元的跨距抽取器），以及基于自然语言推断的 $S_p\to S_r$、$S_r\to S_p$、$S_p\leftrightarrow S_r$ 与 $D\to S_p$ 等多种指标。

### 3. 实验设计：数据集、基准与对比方法

- **数据集**：
  - MUCSUM：根据经典 MUC-4（1,700 篇涉及拉美政治冲突和恐怖事件的文档，6 种事件类型、24 个角色）构建，对每个文档-事件模板对生成一条摘要；
  - 训练/开发/测试划分：1,300 / 200 / 200 篇文档（在论文测试表中刻意省略详细测试集统计，防止作弊）；
  - 摘要平均长度约 44~51 词（1.7-1.8 句 / 摘要），文档平均约 328-354 词、12-15 句。
- **对比方法与设置**：
  - **精调模型**：BART-large、PEGASUS-large、T5-large，分别在三种输入设置下评测（temp+doc、temp only、doc only）；
  - **零样本大模型**：ChatGPT、GPT-4，使用三组不同提示词取平均；
  - **附加评估**：CEAF-REE 需要先训练一个抽取摘要中论元的模型，使用 Xia et al. (2021) LOME 的跨距抽取器并基于 RoBERTa-large。
- **人工评估**：
  - 三个英语流畅者针对测试集中随机 30 个文档-事件对，对参考摘要及 5 种模型摘要按 5 点李克特量表（factuality, adequacy, coherence, relevancy, fluency）打分；属于多观察者独立评价、匿名来源、随机排序。
- **数据集/代码公开**：论文公开代码、数据与标注指导（MIT 许可）。

### 4. 资源与算力

- 论文在正文与附录中说明：精调实验使用 3 个模型，每个模型分别用 3 个随机种子（1337 / 1338 / 1339）训练 3 次；
- 每次训练在 **单块 NVIDIA RTX 6000 GPU** 上进行；
- 训练轮数固定为 30 个 epoch，按开发集 ROUGE-1 F1 选择最好 checkpoint。
- 但**未明确说明**具体训练时长、总 GPU 小时数、内存占用以及模型推理成本；正文也只在附录中粗略说明，没有提供更精确的资源用量信息。

### 5. 实验数量与充分性

- **实验数量**：
  - 3 个精调模型 × 3 种输入设置（完整输入、仅模板、仅文档），每种 3 seeds，即大量训练运行；
  - 两个大型零样本模型（ChatGPT 和 GPT-4），3 组不同提示词取平均；
  - 评测了 8 类自动指标：ROUGE-1/2/L、BERTScore、CEAF-REE、NLI 四向指标、以及与人工评分的 Kendall rank 相关性；
  - 30 个样本随机测试子集的人工评价 + 额外 30 个样本的双重标注一致性研究。
- **充分性与公平性**：
  - 有清晰的消融设计，证明该任务不只是纯粹文本摘要或结构到文本；
  - 多个指标、多人类评估视角、独立测试集；零样本大模型避免了针对测试集的调参问题，并强调提示词未使用 MUCSUM 标注的同一提示语，防止分数虚假膨胀；
  - 不足：人工评估规模较小（30 个样本 × 6 种来源 × 3 个评审），且模型摘要只取单次解码结果，无法充分覆盖生成多样性与极端失败模式；不同种子或提示下的差异未做显著性区间论证；
  - 参考摘要由论文作者内部写出，并非独立外部的人群众包注释，可能与后续评测有一定指标偏向。

### 6. 主要结论与发现

- **精调模型表现**：在完整（temp+doc）输入下 T5 在大多数指标上明显领先，BART 在 CR 与 $S_p\to S_r$ 等方面也很强，PEGASUS 偏抽取式提取，在该抽象式摘要基准上排后；
- **消融结论关键**：去掉文档时模型生成的摘要往往质量大幅下降（在 ROUGE、BERTScore、双方位蕴含等都有明显下降），去掉模板也会导致多项指标显著下降；说明 MUCSUM 确实必须把文档与事件模板共同作为输入，不能简单退化为"普通摘要"或"结构到文本"；
- **零样本模型**：ChatGPT/GPT-4 在传统词法重合类指标（ROUGE、BERTScore）落后于精调模型，但在若干 NLI 指标上却经常超过精调模型，说明它们能生成相对合理的摘要但词面重合度较低；
- **人类评价**：所有模型生成的摘要在统计上都显著劣于参考摘要；各模型之间的差异并不显著；GPT-4 与 PEGASUS 的平均得分偏低，BART/T5 综合稍好；评价呈现较大个体差异，同一摘要可以收到 2~5 分之间的差异分数；
- **判断-指标相关性弱**：人类评价分数与多数自动指标间的相关程度不高，NLI 指标在本数据上并未表现出以往工作中的明显领先优势，这提示应从人类中心角度重新审视自动评测。

### 7. 优点

- **任务创新性强**：将文档级事件抽取与摘要功能自然结合，贴合事件抽取最终服务人类用户目标，定义了清晰的任务数学框架（事件本体、事件类型/角色映射和输入输出形式）；
- **数据与标注质量较好**：基于领域权威 MUC-4 的模板标注，采用半自动生成+人工编辑效率较高，并加入事件状态、时间、地点等关键信息，增强摘要内容覆盖；
- **评测体系多样性好**：引入大量自动指标（词面匹配、语义相似、论元重构、NLI 蕴含）并配有人类主观质量评估、跨标注者一致性比较，以及选择性地做提示词平均与多种子运行，可多维度揭示模型差异；
- **剥离式消融控制合理**：明确对比完整输入、仅结构、仅文档三种条件，强力验证任务并非两种简单任务的简单线性组合；
- **人工评估设计较严格**：来源匿名、顺序随机、提示强调事实性/充分性/连贯性/相关性/流利度等并列规则，并且公布全部评分数据；
- **开源共享**：代码、数据、提示文本与评估材料公开，有利于后续科研复现与新增模型比较。

### 8. 不足与局限

- **领域与本体覆盖有限**：只用 MUC-4，事件类型仅含 6 类并且角色固定约 24 种，不能代表更复杂、开放的本体（如 FAMuS 或 MAVEN）；更丰富数据集中事件嵌套、跨句、跨事件模板的生成难度会更高；
- **基准只用了参考模板**：实验只基于 gold template，并不能体现真实信息抽取到事件键式摘要全链路中因预测模板错误带来的质量损失；
- **对超长文档的处理相对粗糙**：当输入超过模型窗口时，只从右侧截断文档，未做长文本摘要的专门优化；
- **人工标注相对"内行"**：摘要由论文三位作者亲自编写，存在作者内在一致性及对标注任务知识背景依赖的可能（也说明其 NLI 与自动指标高分判断存在潜在偏差）；
- **人工评估本身局限**：仅 3 个评审者，评定粒度单一，未引入事实性错误检测任务，评审者间相关性低意味着样本量太小可能不足以支撑强结论；
- **论文指出了对应伦理风险**：MUC-4/MUCSUM 数据涉及历史上真实恐怖袭击与真实涉案者，模型在此数据上产生的不可靠信息可能对这些历史事件和人物造成不实表述，因此声明仅供学术用途。

（完）
