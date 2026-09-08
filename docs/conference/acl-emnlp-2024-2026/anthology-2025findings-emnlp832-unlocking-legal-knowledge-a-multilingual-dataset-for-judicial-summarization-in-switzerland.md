---
title: "Unlocking Legal Knowledge: A Multilingual Dataset for Judicial Summarization in Switzerland"
title_zh: 解锁法律知识：瑞士多语言司法摘要数据集
authors: "Luca Rolshoven, Vishvaksenan Rasiah, Srinanda Brügger Bose, Sarah Hostettler, Lara Burkhalter, Matthias Stürmer, Joel Niklaus"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.832.pdf"
tags: ["query:evidence-qa"]
score: 4.0
evidence: 面向法院判决的多语言法律摘要数据集与评测
tldr: 针对法院判决缺少法律要点摘要、人工标注昂贵的问题，构建瑞士里程碑判决摘要数据集SLDS，涵盖2万份联邦最高法院判决及其德语、法语和意大利语官方要点。作者微调了Qwen2.5、Llama3.2等开源模型，并与GPT-4o、Claude3.5等大模型和推理模型比较，用LLM-as-a-Judge评测摘要质量。该资源可显著改善法律信息获取，为法院文件上的自动摘要评测提供多语言法律基准。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1499, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1567, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 749, \"height\": 1300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1393, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1497, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1496, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1493, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 797, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 799, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp832/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1631, \"height\": 404, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 181, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 976, \"height\": 1234, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 2562, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1665, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp832/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 815, \"height\": 1633, \"label\": \"Table\"}]"
motivation: 法院判决常缺法律要点摘要且人工标注成本高昂，限制法律检索和可访问性。
method: 构建包含2万份瑞士联邦最高法院判决及三语要点的数据集，并微调开源模型与商业模型对比。
result: 覆盖2万份判决，验证了开源模型在司法摘要上的相对效果与评测可行性。
conclusion: SLDS有助于降低司法摘要成本并促进多语言法律文本自动摘要研究。
---

## Abstract
Legal research depends on headnotes: concise summaries that help lawyers quickly identify relevant cases. Yet, many court decisions lack them due to the high cost of manual annotation. To address this gap, we introduce the Swiss Landmark Decisions Summarization (SLDS) dataset containing 20K rulings from the Swiss Federal Supreme Court, each with headnotes in German, French, and Italian. SLDS has the potential to significantly improve access to legal information and transform legal research in Switzerland. We fine-tune open models (Qwen2.5, Llama 3.2, Phi-3.5) and compare them to larger general-purpose and reasoning-tuned LLMs, including GPT-4o, Claude 3.5 Sonnet, and the open-source DeepSeek R1. Using an LLM-as-a-Judge framework, we find that fine-tuned models perform well in terms of lexical similarity, while larger models generate more legally accurate and coherent summaries. Interestingly, reasoning-focused models show no consistent benefit, suggesting that factual precision is more important than deep reasoning in this task. We release SLDS under a CC BY 4.0 license to support future research in cross-lingual legal summarization.

---

## 论文详细总结（自动生成）

## 一、核心问题与研究动机

- 法律检索高度依赖**裁判要旨（headnotes）**——由法官或书记员撰写的判决要点摘要，律师借助它快速判断判决的相关性。
- 由于人工撰写要旨成本极高，大量法院判决没有配套摘要，制约了法律信息的可获取性与检索效率。
- 摘要生成（Summarization）是 NLP 中辅助司法工作的关键方向，但现有法律摘要数据集主要集中于**单语**或**单一法域**，难以覆盖瑞士这类**多官方语言（德、法、意）**司法体系下的跨语言摘要需求。
- 为此，论文构建了 **SLDS（Swiss Landmark Decisions Summarization）**——瑞士联邦最高法院 20K 份里程碑判决的三语言摘要数据集，并系统性评测了当下多种开源与商业大模型在该任务上的表现。

## 二、方法论

### 1. 数据集构建
- 从瑞士联邦最高法院官方仓库（bger.ch）抓取 1954–2024 年间五个官方卷册（I–V）发布的里程碑判决，获得判决全文（按原始语言：德/法/意，单语）及对应**三种语言**的官方要旨。
- 数据集以“一对一对”长格式存储：每份判决对应德/法/意三条要旨，共形成 **60K+ 数据行**。
- 采用两阶段流水线：
  - **抓取**：异步爬虫，带超时重试与断点续抓；
  - **后处理**：自动识别判决语言、按官方规则映射到法律领域、将多语言要旨“融化（melt）”为长格式，并分配 sample_id。
- **数据划分**：按判决年份切分训练集（1954–2021）、验证集（2022）、测试集（2023–2024），避免时间泄露并反映不同时期撰写风格差异。
- 数据集的摘要特性分析显示：压缩比（CR）远高于 EUR-Lex-Sum 与 MILDSum；高度抽取性之外仍有约 30% 的四元组全新组合，说明摘要在“摘要 vs 抽象”间呈独特平衡。

### 2. 评测方法
- **传统指标**：BERTScore、BLEU、ROUGE-1/2/L（经 lighteval 框架计算）。
- **LLM-as-a-Judge**：
  - 采用 **DeepSeek V3** 作为裁判模型（多语种能力强、成本低，且不在被测模型列表内以避免自我偏好）；
  - 从五个维度打分：①准确性 & 忠实性；②完备性 & 相关性；③清晰度和连贯性；④法律条文引用；⑤判决理由引用；
  - 评分标准化：1–3 分归一化到 0–2 分，加总为 0–10 分并等比例到百分比。
- **人工评估**：
  - **Human-as-a-Judge**：两位专业律师（评估者未获知判决全文）对 63 个样本（覆盖全部 9 个语言子集）、3 个代表性模型共 189 条输出按相同协议评分；
  - **Contextualized Human Analysis**：第三位法律专家结合判决全文对 6 个样本进行逐案深度定性分析。

### 3. 模型与设置
- **微调模型**：Qwen2.5（0.5B、1.5B、3B、7B、14B）、Llama 3.2 3B、Phi-3.5-mini；采用 LoRA（rank=16, alpha=16）参数高效微调，最大序列长度 8192，训练 3 epochs。
- **直接推理模型**：GPT-4o、Claude 3.5 Sonnet、DeepSeek R1、o3-mini，采用 one-shot prompting（示例选自验证集、按语言子集选取最短序列）。

## 三、实验设计

- **Benchmark**：SLDS 测试集，约 978 个样本，覆盖 9 种“判决语言→要旨语言”组合（de→de, de→fr, de→it, fr→de, fr→fr, fr→it, it→de, it→fr, it→it）。
- 对比对象包括微调小模型 vs. 尚未微调的大型专有/推理模型，并额外比较了微调前后表现以量化微调增益。
- 结果以宏平均给出，所有指标在各语言子集上均衡加权，缓解语言样本不均衡带来的偏差；不确定性通过 bootstrap 估计置信区间。

## 四、资源与算力

- 文中在附录明确说明：微调与学习率扫描主要使用 **1 块 NVIDIA H100 96GB**，部分训练在 **2 块 NVIDIA A100 80GB**节点完成。
- 全部实验累计运行时间约 **15.363 天**。

## 五、实验数量与充分性

### 实验数量
- 对 7 个开源小模型进行了微调，并对每个模型执行了 3 个学习率的扫描（1e-5、5e-5、1e-4）；
- 推理/评测阶段覆盖 4 个大模型、9 个语言子集，生成大量逐一对比结果；
- 额外做了微调前后对比（表 5）、消融式语言子集热力图（图 7/8）、两类人工评估及相关性分析（图 9）；
- 数据集的摘要属性（压缩率、EFC/EFD、N-Gram Novelty、Formulaicness、Coverage Increment）也进行了系统测度并与 BillSum、EUR-Lex-Sum、MILDSum 对比。

### 充分性评价
- **较充分且客观**：评测结合了词法指标、裁判大模型、和两级专业人工评估，形成了较完整的评测链；在不同语言子集上做细化报告，能揭示跨语言能力差异。
- **存在局限**：
  - 人工标注规模有限（63 个抽样样本；深度分析仅 6 个），且缺少 IAA（Inter-Annotator Agreement）报告，削弱了主观评分的稳健性；
  - 意大利语子集仅有少数样本且只一位律师流利掌握，可能带来评估偏差；
  - LLM-as-a-Judge 与人类专家总体相关性仅中等（0.26 左右），说明裁判模型尚不能完全代替人评；
  - 未尝试微调更大规模（>14B）的开源模型，未能充分检验规模扩展的收益边界。

## 六、主要结论与发现

1. **微调模型词法对齐强，法律质量弱**：微调后的 Qwen2.5 14B 在 BERTScore、BLEU、ROUGE-2/L 上甚至超过 GPT-4o、Claude 3.5 Sonnet 等大得多的模型，但 JUDGE 分数显著偏低——说明传统指标高不能保证法律内容的准确性、完整性与结构规范。
2. **大规模模型在法的精确性上仍具优势**：GPT-4o、Claude 3.5 Sonnet 尽管词法分数不高（部分因输出格式缺少后处理），但生成要旨的法律准确度与完整性更好。
3. **推理模型未显示出稳定优势**：DeepSeek R1 的 JUDGE 总分最高，但与 Claude 3.5 Sonnet 差幅很小；o3-mini 甚至只比 14B 微调模型高 3.4 分左右——法律要旨生成更多依赖事实提取、领域知识与格式规范，而非复杂推理。
4. **跨语言鲁棒性是关键短板**：Qwen2.5 14B 在法→法同语种下表现优秀，当输入与输出语言不一致时下降明显（尤其德/意输入）。
5. **法语要旨得分总体偏高**：这可能与模型对法语生成能力更强或法语文档结构更规律有关。
6. **传统相似度指标与法律质量偏差大**：如 Claude 3.5 Sonnet 出现低 BERTScore 但高 JUDGE 分（原因在于模型输出 JSON/Unicode 转义），明确揭示了既有指标在领域评测中的误导性。
7. **数据集质量与安全性良好**：对预训练语料重叠测试显示 SLDS 被污染的可能性很低，可安全用于模型评测。

## 七、主要优点

- **填补空白**：提供了首个覆盖单一多语言法域的大规模判决摘要数据集（60K 行、三种语言、CC BY 4.0 开放许可），在德语-法语、意大利语-德语样本量上远超此前的 EUR-Lex-Sum。
- **评测体系完整**：传统指标 + LLM-as-a-Judge + 两类人工专家评估的结合，在有限预算内捕捉了不同维度质量差异；
- **语言拆解细致**：按 9 个子集分别报告，能揭示跨语言泛化及评测指标偏置问题；
- **丰富的附录支撑**：提供了提示词细节、一示例（one-shot）选择策略、输出伪影修正（Claude 的 JSON）、数据集字段使用等完整记录，训练/评测脚本开源，利于复现；
- **严谨的数据质量保证**：对司法保密（匿名化）与版权合规做了说明，并进行了语料污染排查。

## 八、不足与局限

- **人类评估规模偏小**：63 份抽样及 6 份深度分析只能提供初步结论，且缺少 IAA，评分主观性难以量化。
- **LLM-as-a-Judge 相关性有限**：裁判模型与律师间相关度不高，法律维度上的可靠性仍需提升。
- **跨语言不平衡**：意语判决占比过低（约 4%），针对意语的性能估计置信区间较大，结论可能不稳健。
- **评测条件不对称**：专有大模型采用 one-shot 推理而微调模型采用 zero-shot，难以完全剥离提示收益；部分模型输出格式异常需要人工修正（如 Claude 的空输出/JSON包裹），增加了评测复杂度。
- **未做规模上限探索**：没有微调 ≥15B 的更大开源模型，无法完全说明放大参数是否能弥合与商业模型的差距。
- **应用范围限制**：模型生成的 headnote 可能存在对法条的错误引入或对判决的过度推断——在缺乏人工复核的前提下不宜直接作为法律工作辅助；论文对此有明确的风险警示。

（完）
