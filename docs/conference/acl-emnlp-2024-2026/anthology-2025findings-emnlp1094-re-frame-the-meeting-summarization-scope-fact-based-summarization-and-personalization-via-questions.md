---
title: "Re-FRAME the Meeting Summarization SCOPE: Fact-Based Summarization and Personalization via Questions"
title_zh: 重定会议摘要范围：基于事实的摘要与提问式个性化
authors: "Frederic Kirstein, Sonu Kumar, Terry Ruas, Bela Gipp"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1094.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: FRAME模块化摘要流程抽取显著事实以避免幻觉，并提供无参考评估框架P-MESA
tldr: 大模型会议摘要常出现幻觉、遗漏和无关内容。论文提出FRAME流水线，将摘要重构为语义增强任务：抽取并给显著事实打分、按主题组织、再充实成抽象摘要；同时用SCOPE提问推理实现个性化。配套的P-MESA多维无参考评估能可靠识别错误实例。该方案兼顾事实忠实与个性化，为会议摘要提供了模块化改进方向。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1094/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1579, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1094/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1094/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1587, \"height\": 954, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1597, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 823, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 697, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 785, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 783, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 792, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 822, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 653, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 794, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 750, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 634, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 552, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1135, \"height\": 681, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1238, \"height\": 660, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 712, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1580, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 784, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1654, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 796, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1652, \"height\": 771, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 776, \"height\": 560, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1595, \"height\": 742, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1660, \"height\": 484, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1655, \"height\": 742, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1638, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1605, \"height\": 736, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1094/table-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1655, \"height\": 960, \"label\": \"Table\"}]"
motivation: 会议摘要中大模型输出经常出现幻觉、遗漏和无关信息，且缺乏面向目标的评估。
method: 抽取并排序显著事实，按主题组织并增强大纲；另设计九问推理协议SCOPE实现个性化摘要。
result: P-MESA可可靠识别错误实例，FRAME输出以事实为驱动的摘要。
conclusion: 以事实抽取为基座并辅以多面评估可降低会议摘要幻觉并支持个性化。
---

## Abstract
Meeting summarization with large language models (LLMs) remains error-prone, often producing outputs with hallucinations, omissions, and irrelevancies. We present FRAME, a modular pipeline that reframes summarization as a semantic enrichment task. FRAME extracts and scores salient facts, organizes them thematically, and uses these to enrich an outline into an abstractive summary. To personalize summaries, we introduce SCOPE, a reason-out-loud protocol that has the model build a reasoning trace by answering nine questions before content selection. For evaluation, we propose P-MESA, a multi-dimensional, reference-free evaluation framework to assess if a summary fits a target reader. P-MESA reliably identifies error instances, achieving ≥ 89% balanced accuracy against human annotations and strongly aligned with human severity ratings ( 𝜌 ≥ 0.70 ). On QMSum and FAME, FRAME reduces hallucination and omission by 2 out of 5 points (measured with MESA), while SCOPE improves knowledge fit and goal alignment over prompt-only baselines. Our findings advocate for rethinking summarization to improve control, faithfulness, and personalization.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：会议摘要具有信息分布分散、上下文依赖强、显著内容因人而异三大核心挑战。现有 LLM 摘要系统将会议视为线性文本进行压缩，结果频繁出现幻觉（hallucination）、关键信息遗漏（omission）与无关内容（irrelevance）。
- **根本论点**：当前方法的失败源于结构性错配——先"压缩形式"而非"重建意义"。论文主张将会议摘要从"文本缩减问题"重新定义为"语义增强任务"，先显式地抽取、筛选和组织事实，再基于已有事实撰写摘要。
- **整体含义**：通过将摘要流程模块化、事实化，并引入面向读者的推理协议，可同时提升摘要的控制力、忠实度和个性化水平，为会议摘要乃至通用摘要提供了新的范式方向。

## 2. 论文提出的方法论

### 2.1 FRAME（Fact-based Reconstruction and Abstractive MEeting Summarization）
- **核心思想**：将摘要建模为四阶段"富集"流水线，模拟人类摘要者的认知过程（抽取事实→筛选→组织→撰写）。
- **事实表示——"陈述-上下文"二元组**：每个事实定义为 `⟨c, κ⟩`，其中 `c` 是自包含的陈述，`κ` 是理解该陈述所需的全局最小上下文。要求满足完备性（引用可解析）与最小性（只表达一个意思，上下文不冗余）。与原子事实和分子事实相比，该表示在解释性与上下文保留间取得平衡。
- **四阶段流程**：
  1. **事实识别（Fact Identification）**：利用 LLM 从会议文本中抽取事实元组，并用 LLM 裁判（受 FActScore 启发）对事实进行验证（事实性、完备性、清晰度、最小性），删改补写约 5% 的事实。
  2. **笔记筛选（Note-Taking）**：对每个事实打功能标签（决策、行动项、洞见、背景）并给出 1–10 的相关性分数；随后按语义重叠对事实分组合并，保留最高分。平均保留约 40% 的事实（约 103 个原始事实中保留 41 个）。
  3. **组织（Organization）**：将高分事实（ri≥8）与决策类事实作为大纲主点，中等分事实（6≤ri<8）与背景事实作为支撑，形成层次化大纲。
  4. **摘要撰写（Summarization）**：LLM 严格基于大纲和支撑事实"富集"生成抽象摘要，禁止引入事实之外的内容；随后由质量保证模块按大纲遵循度、事实准确性、信息覆盖、格式四大维度评分，超标则触发一轮修订循环。
- **工程细节**：针对超长会议设计了 Chunk Processor（块处理器）与 Memory Bank（存储库）以解决上下文窗口限制与跨块事实去重问题。

### 2.2 SCOPE（Summarizing Content Oriented to Personal Expectations）
- **核心思想**：借鉴认知科学中的出声思维（think-aloud）与元认知研究，在事实筛选前让 LLM 显式回答 9 个问题，构建关于读者特征、目标与信息需求的推理轨迹。
- **九个问题**分为四个认知阶段：规划（读者先验知识、当前项目、目标兴趣）、初始评估（信息如何与读者角色相关、紧迫性、是否需要简化/补充、举例验证）、控制（重新审视并排除无关信息）、评估（指出难以分类的不确定内容）。
- **作用机制**：SCOPE 插入 FRAME 的 Note-Taking 阶段，在相关性打分前对事实进行预筛；读者画像同时在大纲生成和摘要撰写阶段起作用。9 个问题的答案充当 LLM 的"工作记忆"，比静态角色注入更稳定地锚定内容选择。

### 2.3 P-MESA（Personalized-MEeting Summary Assessor）
- **核心思想**：面向读者的、无参考的多维评估框架，用于判断"单个摘要是否满足单个目标读者"。
- **七个维度**：事实性（factuality）、完整性（completeness）、相关性（relevance）、目标对齐（goal alignment）、优先级结构（priority structuring）、知识水平匹配（knowledge-level fit）、情境框架（contextual framing）。维度经 50 篇文献综述＋人工研究筛选精炼而来（最初 9 维合并/删除为 7 维）。
- **实现**：三阶段流水线——错误实例检测、严重程度评分、按类别聚合影响分数。LLM 裁判（GPT-4o）接收读者画像后对每个维度给出 1–5 分的李克特评分。

## 3. 实验设计

### 3.1 数据集
- **QMSum**：真实会议基准，含学术（ICSI）、产品设计（AMI）、议会（WCPC）三类会议，共 232 场，平均 7,303 词。
- **FAME**：合成多智能体会议数据集，500 场英文/300 场德文会议，覆盖 14 种会议形式、28 个主题，约 50% 含打断现象。
- 主实验各随机采样 50 个英文样本。
- **跨域推广**：arXiv、XSum、BigPatent、PubMed 四类文档摘要数据集；以及基于 MIMIC 方法将 PubMed 文献转化为模拟会议进行测试。

### 3.2 对比方法与评估指标
- **基线**：GPT-4o、Gemini 1.5 Pro 的零样本单次摘要；个性化场景对比"读者定制提示（reader-tailoring）"与"角色扮演（role-playing）"，以及基于反馈的自改进基线（FB-1/2/3）。
- **评估指标**：无参考 MESA（8 个通用质量维度）、新提出的 P-MESA（7 个个性化维度，1–5 分；分数越低越好）、ROUGE（R-1/R-2/R-L）、BERTScore（F1）。
- **人类评估**：P-MESA 开发与验证阶段各 48 条人工标注摘要（开发集用于维度精炼，验证集仅用于评估代理效度）；6 名标注员、经过一周培训、报告 Krippendorff's α（各维度 0.68–0.84）；个性化对比阶段 5 名标注员评估 20 组×3 种方法生成的摘要。

## 4. 资源与算力

- **计算成本**：论文报告的 FRAME 在 GPT-4o 下每次会议约需 72,059 输入 token＋11,674 输出 token，估算费用 $0.21/会议、耗时约 225 秒；单次 LLM 摘要约 $0.06、5 秒；SCOPE 额外增加约 0.03 美元/13 秒。事实抽取与验证占总计算量约 62%。FRAME + Llama-3.1-8B 可在约 $0.03/会议的预算下达到与反馈式三轮迭代接近的质量。
- **计算资源的明确说明**：论文未明确给出 GPU 型号、数量或训练时长。由于方法基于闭源/开源 LLM 的 API 或推理调用而非微调训练，论文以 token 数、API 费用和推理秒数作为核心资源度量，而非传统算力指标。使用 Azure 上的 GPT-4o 部署（4K 输出上限），以及 Gemini 1.5 Pro、Llama 3.1 8B、Gemma 3 4B 四个模型作为骨干。

## 5. 实验数量与充分性

- **主实验**：通用摘要（表 2）与个性化摘要（表 3）各在两个数据集上完成，覆盖 8 个 MESA 维度＋7 个 P-MESA 维度＋ROUGE/BERTScore。
- **消融与敏感性实验**：
  - 安全机制：事实验证（150 个事实仅 8 个需修订）；摘要精修的作用。
  - 跨模型泛化：4 种骨干模型（GPT-4o、Gemini 1.5 Pro、Llama 3.1 8B、Gemma 3 4B）。
  - 跨域推广：4 个非会议文档摘要数据集。
  - 架构最小性：3 种压缩流水线变体（combined-1/2/3）vs 完整 FRAME。
  - 阈值敏感性：默认/低/高三档事实保留阈值。
  - 事实表示对比：陈述-上下文元组 vs 分子事实。
  - 个性化方法对比：读者定制 vs 角色扮演 vs SCOPE（单模型条件下）。
- **P-MESA 效度验证**：两轮各 48 条独立标注，报告检测 B-ACC≥89%、Cohen's κ≥0.74、严重程度相关性 ρ≥0.70、人类排名对比等。
- **充分性与客观性评价**：整体实验量较充分，覆盖泛化性、消融、人机一致性多个层面；基线对比注重公平性（排除"复用同一模型的反馈式方法"进入主实验，但在附录 L 中单列对比）。局限在于样本规模（各 50 条）、合成数据的生态效度、骨干模型以 GPT-4o 为主导致部分结果与其自身强大能力耦合，以及阈值选择具有一定人工经验性。

## 6. 论文的主要结论与发现

- FRAME 将摘要重构为富集任务后：GPT-4o 骨干下在 QMSum 上将幻觉从 3→1、在 FAME 上从 4→1（5 级李克特，越低越好）；无关性从 2–3→1；重复从 3–4→1–2；结构从 4→3。
- FRAME 生成的摘要以主题而非时间顺序组织，能过滤低价值内容并保持说话者归因清晰。
- SCOPE 在个性化摘要中将相关性从 3→1、知识水平匹配从 2→1、目标对齐从 3→2，且不牺牲通用质量（MESA 分数与通用设置相近）。SCope 优于读者定制提示和角色扮演，原因是显式建模了"信息为何重要"而非仅"为谁生成"。
- P-MESA 是可靠的人类判断代理：错误检测 B-ACC≥89%，严重程度相关性 ρ≥0.70，且在目标对齐（ρ=0.81）与相关性（ρ=0.78）维度对齐最强。
- 跨模型实验表明 FRAME 的好处源于架构而非模型能力；FRAME 可缩小商用与开源模型间的质量差距。
- 跨域实验显示 FRAME 对文档摘要同样有效，尤其在降低重复（-3）与遗漏方面，说明其具备通用摘要框架潜力。

## 7. 优点

- **方法设计亮点**：
  - 提出"陈述-上下文"事实表示，兼顾可验证性与可解释性，避免原子事实（上下文破碎）与分子事实（上下文不足）的缺陷。
  - 将摘要建模为与人类认知步骤对应的四阶段流水线，每个阶段职责清晰、可插拔；模块化设计便于替换骨干模型和下游适配。
  - SCOPE 以 9 问推理协议将心理学中的出声思维转化为可复现的 LLM 提示流程，为个性化摘要提供了超越角色注入的机制性路径。
  - P-MESA 是无参考、面向目标读者的多维评估指标，填补了个性化摘要缺乏低成本自动评估的空白，且经严格人工标注验证（高 B-ACC 与高秩相关）。
- **实验设计亮点**：消融体系完整（架构最小性、阈值敏感性、跨模型/跨域泛化、安全机制逐一验证），并额外报告了成本-质量四象限分析，兼顾实用部署视角。

## 8. 不足与局限

- **骨干依赖**：FRAME/SCOPE 的效果高度依赖底层 LLM 的推理能力；小模型下事实抽取质量下降，验证与修订环节的重要性上升。
- **数据覆盖**：QMSum 与 FAME 虽覆盖多种会议类型，但缺少医疗咨询、法律会议等专门领域；合成数据（FAME）与现实会议动态仍有差距；论文只评估了英文数据上的主实验。
- **评估指标与相关性**：FRAME 在 ROUGE/BERTScore 上较基线无持续优势甚至偏低，说明它与参考摘要的结构差异可能被参考型指标惩罚；MESA 维度采用中位数而非均值汇报，掩盖了分布尾部的细节。
- **计算成本**：多阶段流水线的 token 开销显著高于单次 LLM 摘要（约 3.5 倍费用、45 倍耗时），不适用于实时或资源受限场景；论文没有报告端到端的 GPU 训练/推理硬件需求，且未与传统高效方法（如蒸馏小模型）进行量化对比。
- **冗余与偏差风险**：SCORE 的 9 个问题虽然经过认知框架设计，但其维度和措辞主要由作者定义，缺少与其他个性化推理协议的系统消融对比；标注员年龄区间集中（22–29 岁）、样本数量有限，P-MESA 的跨文化、跨年龄泛化性尚未验证。
- **阈值经验性**：重要性分数范围（9–10 决策 vs 1–3 低显著性）和保留阈值（ri≥6/8）为经验设定，虽有敏感性分析，仍缺乏理论或数据驱动的校准依据。

（完）
