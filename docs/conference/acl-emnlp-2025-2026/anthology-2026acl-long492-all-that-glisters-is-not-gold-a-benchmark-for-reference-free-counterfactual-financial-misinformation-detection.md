---
title: "All That Glisters Is Not Gold: A Benchmark for Reference-Free Counterfactual Financial Misinformation Detection"
title_zh: 闪光的未必都是金子：无参考反事实金融错误信息检测基准
authors: "Yuechen Jiang, Zhiwei Liu, Yupeng Cao, Yueru He, Ziyang Xu, Chen Xu, Zhiyang Deng, Prayag Tiwari, Xi Chen, Alejandro Lopez-Lira, Jimin Huang, Jun’ichi Tsujii, Sophia Ananiadou"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.492.pdf"
tags: ["query:hallu-rag"]
score: 6.0
evidence: 用于检测金融错误信息的基准，关注金融文本的事实可靠性
tldr: 大型语言模型在金融新闻中可能传播错误信息。本文提出RFC-Bench基准，在段落层面评估无参考和对比诊断两种任务下的金融错误信息检测。实验显示模型在提供对比上下文时表现较强，而无参考设置下出现预测不稳定、无效输出增多等问题，表明当前模型在缺乏对比时难以维持事实可靠性。该基准为金融文本幻觉与错误信息研究提供了评测基础。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 915, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 750, \"height\": 312, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 803, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 809, \"height\": 587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 807, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 606, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 606, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 796, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 796, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 794, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 791, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 790, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long492/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1645, \"height\": 888, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1669, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 812, \"height\": 619, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 1080, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1664, \"height\": 1253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 451, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 811, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long492/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 752, \"height\": 949, \"label\": \"Table\"}]"
motivation: 金融新闻中的错误信息难以检测，现有模型在无参考场景下表现脆弱。
method: 构建RFC-Bench基准，包含段落级无参考检测与配对原始-扰动输入的对比诊断任务。
result: 实验表明模型在对比上下文下性能强劲，无参考设置下暴露显著弱点。
conclusion: 揭示了LLM在金融错误信息检测中的关键局限并提供了评测基准。
---

## Abstract
We introduce RFC-Bench, a benchmark for evaluating large language models on financial misinformation under realistic news. RFC-Bench operates at the paragraph level and captures the contextual complexity of financial news where meaning emerges from dispersed cues. The benchmark defines two complementary tasks: reference-free misinformation detection and comparison-based diagnosis using paired original–perturbed inputs. Experiments reveal a consistent pattern: performance is substantially stronger when comparative context is available, while reference-free settings expose significant weaknesses, including unstable predictions and elevated invalid outputs. These results indicate that current models struggle to maintain coherent belief states without external grounding. By highlighting this gap, RFC-Bench provides a structured testbed for studying reference-free reasoning and advancing more reliable financial misinformation detection in real-world settings.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）在评估金融新闻时，往往只关注文本是否流畅可读，而很少质疑文本本身作为解释对象是否“可接受”。现实中，**极小且保持表面流畅度的编辑**（如将“可能”变为“必然”，或将时间序列改写为因果关系），可以大幅改变一段文本所“担保”的信念承诺（belief commitments），产生看似合理但无新增可验证事实的**反事实金融错误信息**。
- **现有基准的局限**：已有错误信息检测数据集（如 GROVER、FEVER、SCIFACT、FIN-FACT、FINDVER、FISCAL）大多依赖外部证据或检索机制，将任务定义为“有依据的声明验证”，而忽略了**段落内部语义偏移**的检测。这种对证据访问的耦合已被质疑为威胁评测有效性。
- **现实风险**：随着 LLM 在金融应用中迅速普及，在缺乏外部验证时，模型是否会注意到“内容有问题”，还是选择顺应（accommodate）并给出自信结论，这是一个关系到金融信息安全的实践问题。
- **论文含义**：作者提出 RFC-BENCH，将段落级金融错误信息操作化为**保留表面合理性、但改变文本担保内容的反事实扰动**，从而在无需外部证据的条件下评估 LLM 的检测能力，揭示了当前模型在“无参考推理”上的结构性缺陷。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：以**“段落担保（warrants）”**而非“声明真伪”为检测对象，通过最小化扰动保留文本流畅度的同时改变其语义承诺。文章借鉴 Stalnaker 的“共同基础（common ground）”理论，把错误信息视为对信念更新的不当偏移。
- **两类评估任务**：
  - **Task 1: Reference-free Detection（无参考检测）**：仅给定单个段落，模型需输出二分类标签 Y = {True, False}，判断该段落是否被操纵。公式：`y* = arg max P_LLM(y | N)`。
  - **Task 2: Comparative Diagnosis（对比诊断）**：给定原始段落与扰动段落的配对 (N_fact, N_mis)，模型需四分类判断操纵类型 m ∈ M（Flipping, Numerical, Sentiment, Causal）。公式：`m* = arg max P_LLM(m | N_fact, N_mis)`。
- **四种操纵类型**（源于 Rangapur 等人的调查分类，映射见附录 C）：
  - **方向翻转（Directional Flipping）**：反转市场预期方向（涨→跌，乐观→悲观），保留实体、事件、数值。
  - **数值扰动（Numerical Perturbation）**：对数量表达做受控改变，保留方向、叙事结构，禁止新增事实。
  - **情感放大（Sentiment Amplification）**：强化评价性语气，保留事实与方向；用 FinBERT 做极性一致性检查。
  - **因果扭曲（Causal Distortion）**：替换或新增因果解释，保留结果、实体和可观测结果。
- **数据构建流程**（三层管线）：
  1. **数据采集**：从 Yahoo Finance 收集 1,404 篇真实金融新闻（标题+摘要），覆盖 223 只股票，时间 2025-04-25 至 2025-12-15。
  2. **类别特定 LLM 重写**：先用规则关键词分类器（附录 O）+ GPT-4.1 结构化分类标注类别；再用 GPT-4.1 按类别特定提示（附录 Q）重写；经专家迭代优化提示词；用 token 长度比、tiktoken 计算和质量控制（解码设置如 temperature、top_p）保证最小改动。
  3. **人类质量保证**：专家 A 全量审查；专家 B 分层抽查（10%/15%）；双标注者独立评估“类别正确性”和“重写有效性”；**冲突集**经独立复审和专家仲裁，无法解决则移除或划为 hard-case 子集。
- **最终数据集**：1,826 个原始-扰动段落对（保留率 89.4%），另附 123 个 hard-case 子集（最终为 122 个）。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **Benchmark**：RFC-BENCH，段落级、无参考金融错误信息检测基准，两个任务（检测 + 诊断）。
- **评估模型**：共 15 个模型。
  - **开源通用模型**：LLaMA 3.1-8B、LLaMA 3.1-70B、Qwen3-8B（thinking/non-thinking）、Qwen3-14B（两种变体）、Qwen3-32B（两种变体）、Qwen2.5-72B。
  - **领域专用模型**：FMDLlama（面向金融错误信息检测的微调模型）。
  - **闭源模型**：GPT-4.1、GPT-5 Mini、GPT-5.2、DeepSeek-chat、DeepSeek-reasoner。
- **对比方法/基线**：
  - **统一提示协议下的零样本评估**（主要设置），附 2-shot / 8-shot 消融。
  - **人类基线**：一位两年经验的金融专业人士与一位金融工程学生，各在 80 个样本子集（每类 20 个）上完成 Task 1；学生另完成 Task 2。
  - **表层特征基线**：仅使用长度比、标点差异、数字 token 差异、词汇重叠的 logistic 回归，用于排除表面伪影。
- **评测指标**：Accuracy、Precision、Recall、Macro-F1、MCC、AUROC（类别不平衡时），并单独报告 **Invalid Rate**（无效输出率）作为可靠性指标。

### 4. 资源与算力

- 论文 **明确提及算力资源**：研究得到 NVIDIA Academic Grant Program 资助，使用 **Brev 平台上的 32K A100 GPU-hours**。具体 GPU 数量、型号细节未展开。

### 5. 实验数量与充分性

- **实验规模概览**：
  - **主实验**：15 个模型 × 2 个任务（Task 1 二分类 + Task 2 四分类），含完整指标表和混淆矩阵（附录 K）。
  - **Few-shot 消融**：在 Task 1 上对 9 个模型进行 0-shot → 2-shot → 8-shot 对比（附录 J、表 9）。
  - **类别粒度分析**：Task 2 按四类操纵类型单独报告精度/F1；混淆矩阵揭示类别混淆模式。
  - **人类基线**：2 名标注者 × 2 个任务。
  - **表层特征基线**：logistic 回归对比。
  - **可靠性分析**：双标注者一致性（Percent Agreement、Macro-F1、Cohen's κ、Gwet's AC1），每个类别独立报告。
  - **误差分析**：典型样例研究（假阴性、假阳性、正确但错误理由、类别混淆等，见附录 M）。
  - **数据消融**：裁决前后样本对比、hard-case 子集分析。
- **充分性评估**：实验数量**总体充分**，覆盖了模型规模、推理模式（thinking/non-thinking）、领域适配、few-shot 影响、人类对比和表面伪影排除。但**没有**做多语言/多市场、多模态（表格/图表）的覆盖实验，也没有对 Task 2 做 few-shot 消融。此外，闭源模型使用默认解码设置可能引入随机性，但文章未报告多次运行方差。

### 6. 论文的主要结论与发现

- **Task 1（无参考检测）接近随机水平**：零样本最佳准确率仅 53.6%（DeepSeek-reasoner），GPT-4.1 为 52.7%；Macro-F1 均低于 0.53，MCC 接近 0。领域专用模型 FMDLlama（51.8%）也未改善，且出现 9.05% 的无效输出率。
- **Task 2（对比诊断）显著提升**：强模型达到 0.85–0.97 准确率，GPT-4.1 / GPT-5 Mini 达 0.97 左右；FMDLlama 也升至 62.9%。
- **Few-shot 收益有限**：8-shot 最佳仅 56.7%（LLaMA-3.3-70B）或 58.4%（GPT-4.1 2-shot），远不及 Task 2 的表现，说明问题不只是指令遵循能力。
- **人类基线**：金融专业人士在 Task 1 达 71.5% 准确率，显著优于所有 LLM；金融工程学生为 57.5%（略优于多数 LLM 但远低于专家）。Task 2 人类接近完美。这说明任务并非固有模糊，而是模型特定的“顺应以先（accommodation-first）”失败模式。
- **表层特征基线**：仅靠表面特征的逻辑回归明显低于 LLM 中位数，说明 Task 2 的优势不是来自格式或词汇伪影。
- **核心发现**：LLM 在提供显式对比时能定位差异并归因操纵类型，但在仅有单段落时无法可靠触发怀疑；这种缺陷在领域专用模型中同样存在，指向**无参考推理的根本性挑战**，而非金融知识缺失。
- **误差模式**：Task 1 中模型对前瞻性陈述过度怀疑、对新闻风格高度信任；Task 2 中倾向依赖表面词汇/数字线索而非操纵机制（如将极性反转误判为数值扰动）。

### 7. 优点

- **问题定义清晰且有理论支撑**：从“段落担保内容”和“共同基础”出发，将错误信息操作化为可量化的反事实扰动，超越了单纯声明级验证。
- **四类操纵机制覆盖全面**：基于已有金融错误信息调查分类，系统映射（附录 C）并逐一实现，可解释性强。
- **严格的质量保证流程**：多阶段审查（专家全量 + 专家抽查 + 双标注者 + 冲突仲裁），报告了多种一致性指标（Gwet's AC1 在类别不平衡下表现稳健），确保标签可靠性。
- **配对设计兼具评测与诊断价值**：Task 1 模拟现实无参考场景；Task 2 作为受控探针分离“检测”和“归因”能力，形成清晰的性能差距信号。
- **多方面消融与对照**：few-shot 消融、人类基线、表层特征基线、混淆矩阵、误差案例——多角度验证结论的稳健性。
- **负责任的数据发布**：不重新分发原始文章文本，仅提供元数据和合成重写文本；明确标注 synthetic 性质；MIT 许可证仅覆盖新增组件，保护版权。

### 8. 不足与局限

- **语言与地域局限**：仅覆盖英语、美国市场的金融新闻，难以推广至其他语言、地区、金融体系的报告惯例和监管环境。
- **模态局限**：只考虑文本，未纳入表格、图表、财报幻灯片、音频、视频等真实分析中的多模态信息。
- **扰动覆盖面有限**：反事实扰动由受控改写管线生成，可能无法捕捉真实世界错误信息的多样性（如长期不一致、协调式叙事操纵）。
- **孤立段落评估**：未涉及有检索/外部知识/更广泛上下文的场景，作为互补测试集而非替代证据型设置。
- **缺乏下游影响评估**：只测检测和诊断准确率，未评估对决策、交易行为或人类信任的实际影响。
- **类别不平衡**：最终数据集中 Numerical（703）远多于 Sentiment（253），可能影响模型在某些类别上的学习与评估稳定性。
- **指标细节未充分讨论**：有效输出上的指标计算可能掩盖无效输出率带来的实用性影响；零样本结果未报告多次运行的方差。
- **人类基线样本量小**：仅 80 个实例、2 名标注者，统计功效有限，且金融专业人士与学生的差异可能反映个体差异而非单纯的“专业”效应。

（完）
