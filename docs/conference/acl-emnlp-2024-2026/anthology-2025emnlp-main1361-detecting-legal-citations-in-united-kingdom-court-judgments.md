---
title: Detecting Legal Citations in United Kingdom Court Judgments
title_zh: 检测英国法院判决中的法律引用
authors: "Holli Sargeant, Andreas Östling, Måns Magnusson"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1361.pdf"
tags: ["query:evidence-qa"]
score: 4.0
evidence: 在英国法院判决语料上标注立法和判例引用并系统评测
tldr: 法律引用检测是判例映射、引用分析和检索的基础，但英国判决引用格式跨越数百年且常涉外国或历史权威。作者利用剑桥法律语料库首次系统比较正则表达式、BERT等编码器与GPT-4.1三类模型，并产出190份判决共45179条涉及英国及非英国立法和判例的细粒度标注金标准。该语料和评测协议为司法文档中的引用抽取与法律知识库构建提供了公开基准。
source: EMNLP-2025-Main
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 517, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1455, \"height\": 1059, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 815, \"height\": 862, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1552, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 816, \"height\": 1460, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 813, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 716, \"height\": 1966, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1441, \"height\": 1498, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1361/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 820, \"height\": 513, \"label\": \"Table\"}]"
motivation: 英国法院判决引用风格复杂且随历史演变，自动检测存在挑战。
method: 使用剑桥法律语料库，系统比较正则、Transformer编码器、大语言模型三类范式，并构建金标准标注语料。
result: 建立了190份判决、45179条法律引用的高质量金标准语料，完成首次系统评测。
conclusion: 为法律引用检测提供了高质量基准和多范式基线，支撑后续判例网络构建。
---

## Abstract
Legal citation detection in court judgments underpins reliable precedent mapping, citation analytics, and document retrieval. Extracting references to legislation and case law in the United Kingdom is especially challenging: citation styles have evolved over centuries, and judgments routinely cite foreign or historical authorities. We conduct the first systematic comparison of three modelling paradigms on this task using the Cambridge Law Corpus: (i) rule‐based regular expressions; (ii) transformer-based encoders (BERT, RoBERTa, LEGAL‐BERT, ModernBERT); and (iii) large language models (GPT‐4.1). We produced a gold‐standard high-quality corpus of 190 court judgments containing 45,179 fine-grained annotations for UK and non-UK legislation and case references. ModernBERT achieves a macro-averaged F1 of 93.3%, only marginally ahead of the other encoder-only models, yet significantly outperforming the strongest regular-expression baseline (35.42% F1) and GPT-4.1 (76.57% F1).

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、论文的核心问题与整体含义（研究动机和背景）

- **核心任务**：本文聚焦于"法律引用检测"（Legal Citation Detection），即从英国法院判决文本中自动抽取指向**立法（legislation）**和**判例法（case law）**的引用。
- **研究动机**：准确识别法律引用是诸多下游法律NLP应用的基础，包括判例映射（precedent mapping）、引用网络分析、法律信息检索、自动问答系统等。法律引用是否被准确抽取，直接影响经验性法律研究的可信度。
- **问题挑战**：英国法律引用检测尤其困难，原因有三：
  1. **引用格式多样且不统一**：英国判例法缺乏统一的引用格式，法官以自然语言写作而非模板化引用，格式历经数百年演变。
  2. **频繁涉及外国或历史权威**：英国法院常引用欧盟法、英联邦国家法律及历史性判例（甚至16–17世纪的文献），这些引用遵循各自辖区的格式惯例。
  3. **此前缺乏针对英国法的系统性研究**：虽然已有针对美国、德国、巴西、土耳其等辖区的法律实体识别（LER）工作，但尚无以英国法为对象的专门研究。作者指出许多已有工作依赖正则表达式却缺乏严格的性能评测。
- **整体含义**：本文填补了英国法领域缺乏系统性的法律引用抽取评测的空白，给出了基准数据集和多种基线的性能比较，为后续工作提供了可复现的参照。

## 二、论文提出的方法论

本文的核心方法是**对三类建模范式进行系统对比评测**，而非提出单一新模型。

1. **语料库构建与标注（CLC-Citation）**
   - 基于Cambridge Law Corpus（CLC），原样本按法院分层随机抽样，因标注工具（INCEpTION）技术问题，最终保留**190份判决**。
   - 初始由三位法律学者标注，发现标注不一致后，由第一作者（具有法律学位及事务律师资格）进行了**系统性再标注**，流程包含三步：
     - ① Schema细化：区分"英国实体"与"非英国实体"子标签，制定详细指南；
     - ② 系统重标注：依据细化指南重新标注全部190份案件；
     - ③ 交叉验证修正：用RoBERTa初版模型识别训练集和验证集中的潜在不一致，人工复核修正。
   - **质量控制**：测试集由第一作者相隔六个月以上进行两次标注，一致性极高（Cohen's κ = 0.99；10,249句中仅46句存在差异）。
   - 采用**BIO2格式**进行token级标注；评估时将B-REFERENCE和I-REFERENCE合并为正类。
   - 细粒度标签包括：UK Case Reference (UKCR)、UK Statute Reference (UKSR)、Case Reference (CR)、Statute Reference (SR)、Case Name Parties (CNP)、Case Neutral Citation (CNC)、Case Law Report Reference (CLRR)，涵盖了英国/非英国、立法/判例/案件头部引用等区分，并将英国和非英国的两标签统一为REFERENCE进行主要评测。

2. **方法一：正则表达式（RegEx）基线**
   - 基于法学专业知识设计模式，分别针对立法引用和判例引用。
   - 对判例引用设计了两种变体：**过包含**（overinclusive，以追求覆盖率为导向）和**欠包含**（underinclusive，以追求精确性为导向）。
   - 在训练集和验证集上进行了迭代优化，但最终模式仍主要覆盖英国常见引用形态。

3. **方法二：预训练Transformer编码器**
   - 微调并评估了五种模型：BERT（cased/uncased两种版本）、RoBERTa、LEGAL-BERT、ModernBERT。
   - 统一训练协议：50训练轮次、100步warm-up、权重衰减0.01、学习率从5e-5线性衰减至1e-7，选择验证集F1最高的checkpoint。
   - 分别在"仅英国标签"和"全标签"两种设置下训练。
   - 值得注意的设计：LEGAL-BERT是uncased模型，为隔离大小写影响，同时训练了cased和uncased的BERT进行对照。

4. **方法三：Decoder类大语言模型（GPT-4.1）**
   - 使用**few-shot + TANL格式**提示词（Paolini et al., 2021），引导模型以 `{引用文本 | REFERENCE}` 的形式输出标注。
   - 对比了**静态few-shot**（固定示例）与**动态few-shot**（轻量RAG：用OpenAI text-embedding-3-small计算相似度，动态选择最相近的8条训练示例，其中至少4条含正例）。
   - 温度为0，使用chat completion模式，每句独立预测。

## 三、实验设计：数据集、基准与对比方法

- **数据集**：自行构建的 **CLC-Citation 语料库**（来自CLC），共190份判决、982,156 tokens；划分为训练（110份）、验证（30份）、测试（50份）。标注规模为45,179条法律引用。涵盖英国各类法院（上诉法院、高等法院各分庭、最高法院、枢密院、各类裁判所等，总计约60种法院类型）。由于该研究无现成的UK法引用检测基准，作者自建语料库，并给出详细标注指南作为未来工作可复用的基准；在此之上对比不同模型。
- **评测设置**：
  - **两个评测变体**：①仅英国引用（UK-only）；②全部法律引用（All labels，含外国引用）。
  - **两个细分维度**：立法（Statute）与判例（Case）分别评测。
- **评价指标**：Token级F1、精确率、召回率、Jaccard Index（IoU）、Seqeval F1（完整实体跨度级别匹配）。
- **对比方法**（三大类共10+种配置）：
  - RegEx：Legislation-only / Overinclusive / Underinclusive
  - Encoders：BERT-Cased、BERT-Uncased、LEGAL-BERT、RoBERTa、ModernBERT
  - LLM：GPT-4.1-Static、GPT-4.1-Dynamic

## 四、资源与算力

- **GPU算力**：论文**未明确说明**训练所用的GPU型号、数量或训练时长。这属于信息缺失，读者无法从文中了解编码器微调的计算成本。
- **LLM API成本**：文中提供了部分成本信息：
  - GPT-4.1的最终版实验（50个测试案件）花费约 **45美元**（其中输入约$28、输出约$17、嵌入约$0.02）。
  - 每份案件推理成本约为1美元。
  - 曾尝试GPT-o1但因其估算成本为GPT-4.1的**6–20倍**而放弃。
  - 作者指出，按此成本，对CLC全库（>320,000案件）做推理在成本上不可行。

## 五、实验数量与充分性

### 实验数量概览
- **系统性主实验**：8种模型配置 × 2个标签设置（UK/All）的完整评估表，外加按立法/判例两种引用类型的分类结果表，以及GPT-4.1和RegEx的对应结果。每组都报告了F1、P、R、Jaccard、Seqeval F1五项指标。
- **消融或变体设计**：RegEx有3种变体；BERT有cased/uncased两种序列化消融；GPT-4.1有静态/动态两种提示策略。
- **误差分析**：对三类方法分别做了错误类型归纳与实例举证（例如正则的欠包含/过包含问题、RoBERTa的假阴性等）。
- **人工一致性**：测试集双标注Cohen's κ=0.99。

### 充分性与公平性评价
- **充分性**：作为一项数据集发布+方法评测工作，实验覆盖了从规则到专用编码器再到通用LLM的完整谱系，多指标和多标签切换的评测使结论较扎实。但缺少消融实验（如BERT-based模型在不同训练集大小下的表现），也未探究同一编码器不同随机种子的方差。因此在敏感性/稳定性证明上有所欠缺。
- **公平性**：
  - 文中提到已尽量避免引入偏误（测试集两轮标注间隔六个月以上）。
  - 但需要注意，RoBERTa参与了训练/验证集合的交叉验证修正（模型预测提示错误并修正人类标注），这种"模型辅助修正训练集"的做法对RoBERTa本身是一种隐性优势或劣势并未讨论。
  - GPT-4.1的提示词刻意不区分英国/非英国引用，使得UK标签上的低精度可部分归因于指令设计而非模型真实能力；对比在提示词设计上不完全对称。
  - 对RegEx，模式仅以英国引用为主，覆盖率天然受限；虽多次迭代但边界效应明显。

## 六、主要结论与发现

1. **编码器模型显著优于其他方法**：所有预训练编码器的F1均超过90%。最佳结果为 **ModernBERT在"全标签"设置下达93.3% F1（Seqeval F1 81.65%）**。
2. **正则表达式基线表现极差**：最佳变体（Overinclusive）F1仅为**35.42%**（全标签）、35.53%（UK标签）。尽管精确率在某些变体中可超过93%，但召回率极低（约7%–24%不等），说明面对UK引用的复杂性和多样性，规则方法覆盖力严重不足。
3. **GPT-4.1虽具有高召回但精确率偏低**：动态提示的GPT-4.1在全标签上为76.57% F1（召回96.74%、精确63.36%）。其高召回（不易漏掉引用）特性使其在作为"辅助预筛"上有一定价值，但由于过度预测问题，在实际高精度应用场景下性价比不高。
4. **LEGAL-BERT的领域预训练增益有限**：LEGAL-BERT（92.72%）与BERT-Cased（92.50%）差距微弱，原因之一是其预训练语料覆盖了美国判例、欧盟判例和英国立法，却不含英国判例，存在辖区不匹配；此外，其uncased属性削弱了法律引用对大小写依赖特征的利用。
5. **各模型对案件引用的识别优于对立法引用的识别**（差距约2–4个百分点），主要因为案例引用通常有更规范的战后引用结构（如[2022] UKSC 25），而立法引用缩写形式繁多。
6. **对低频类型（历史引用与学术引用）识别普遍困难**：历史文献引用（如"Ersk. 2, 6, 15; Duke of Queensberry, Mor. 14, 251"）句法差异较大；学术引用往往与法律引用形态相似，导致模型将其错误标记为引用。
7. **纠错结果**：标注修正发现RoBERTa、LEGAL-BERT和ModernBERT在任务上有微小差异，但其性能差距都在2%以内。

## 七、优点

- **填补英国法领域空白**：首次对UK法律引用检测进行了系统性评测，提供了公开的金标准语料（CLC-Citation）及详细标注指南。
- **数据质量严谨**：标注反复迭代、模型交叉验证、测试集双次独立标注等设计表明了高标准的语料可信度；标注者既具备学术资格（法学学位），又有实务经验（非执业律师）。
- **评测覆盖全面**：包含三大类方法（规则、编码器、生成式LLM），7种以上模型，多个标签体系（UK vs. All、立法 vs. 判例），多项指标（F1、P、R、Jaccard、Seqeval F1），评测维度较立体。
- **误差分析细致**：对三种范式都提供了错误类型的样例展示，帮助读者理解各类方法失效的本质原因，而非只给一组数值。
- **对实际工程应用有明确指导价值**：指出正则方式不适用该任务且成本不可忽视；LLM方案虽然当前精度不足，但在召回率上具有优势，且动态RAG提示能带来增益。

## 八、不足与局限

- **数据集规模与覆盖面有限**：仅190份判决构成标注语料，虽然覆盖多个法院，但在不同历史时期、复杂非英国引用（不同辖区的变异范围极广）和特定案件类型上覆盖度有限。对稀有引用形态的模型识别能力明显受损。
- **测试集修正幅度不确定**：虽然模型交叉验证在一定程度上改善了标注质量，但训练/验证集的修正无法完全避免纠正过程中的反向偏差（因RoBERTa的错误引导而错误“修正”的风险没有被讨论）。
- **缺少可复现细节**：关于算力（GPU型号/数量/训练时间）和批处理大小等细节都没有给出，复现门槛较高。RoBERTa虽参与了训练、验证集的交叉验证修正工作，但未对这一过程的影响进行消融或量化描述。
- **LLM评测的局限**：GPT-4.1模型在测试处理时受输出token长度限制，15,000 token以上的6条句子在分析时被剔除，可能略微影响统计代表性；所用提示词对英国标签设计要求不精细，影响公平比较。解释对于低精度结果的讨论显得不够，未能区分是能力问题还是提示词工程造成的偏差。
- **标注粒度折衷**：作为发表物，实体类型被整合为单一的REFERENCE类进行评测，未按细粒度类型（UKSR、UKCR等）报告模型的具体表现。对用户而言，无法清晰看出模型在"区分UK与非UK实体"上的标签级能力。
- **模式风险提示**：论文注意到法律文本中可能存在偏见与风险（如错误引用传播到下游分析），但并未实际从数据和模型层面对其进行系统性检测，因此这是一个警示而非解决的问题。
- **无法覆盖全部UK引用的具体情况**：尤其对于历史判例中手写/古老形式的引用和学术性引用，三类方法都难以应对，提醒未来工作应进一步对此类引用开展专项处理。

（完）
