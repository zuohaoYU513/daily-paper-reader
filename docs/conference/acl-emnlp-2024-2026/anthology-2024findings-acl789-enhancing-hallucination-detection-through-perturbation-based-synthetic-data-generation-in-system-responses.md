---
title: Enhancing Hallucination Detection through Perturbation-Based Synthetic Data Generation in System Responses
title_zh: 通过系统回复中基于扰动的合成数据生成增强幻觉检测
authors: "Dongxu Zhang, Varun Gangal, Barrett Lattimer, Yi Yang"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.789.pdf"
tags: ["query:faithfulness"]
score: 6.0
evidence: 基于扰动的合成数据生成，用于训练幻觉检测器
tldr: 该文针对LLM幻觉检测人工标注昂贵且过时的问题，提出通过扰动改写系统响应自动生成忠实与幻觉样本。用这些数据微调T5-base检测器，在准确率和延迟上超过零样本检测器及已有合成方法。该工作为幻觉检测提供了低成本、可扩展的训练数据生成途径。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl789/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 720, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl789/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 669, \"height\": 400, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 835, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 726, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 595, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1564, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1558, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1210, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1793, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl789/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 471, \"height\": 213, \"label\": \"Table\"}]"
motivation: 幻觉检测的标注成本高、领域更新快，传统微调难以大规模适配垂直场景。
method: 通过重写系统回复，自动构造忠实与幻觉输出对，并微调轻量检测器。
result: 微调后的T5-base在准确率和延迟上超过SOTA零样本检测器。
conclusion: 提供了一种有效且快捷的幻觉检测器训练数据合成方法。
---

## Abstract
Detecting hallucinations in large language model (LLM) outputs is pivotal, yet traditional fine-tuning for this classification task is impeded by the expensive and quickly outdated annotation process, especially across numerous vertical domains and in the face of rapid LLM advancements. In this study, we introduce an approach that automatically generates both faithful and hallucinated outputs by rewriting system responses. Experimental findings demonstrate that a T5-base model, fine-tuned on our generated dataset, surpasses state-of-the-art zero-shot detectors and existing synthetic generation methods in both accuracy and latency, indicating efficacy of our approach.

---

## 论文详细总结（自动生成）

## 论文中文总结：Enhancing Hallucination Detection through Perturbation-Based Synthetic Data Generation

### 1. 论文的核心问题与整体含义
- **研究背景**：大型语言模型（LLM）在生成回复时经常出现“幻觉”（hallucination），即生成内容与给定知识源矛盾（内在幻觉）或无法被知识源验证（外在幻觉）。这对实际部署构成严重安全与信任风险，因此幻觉检测非常重要。
- **核心痛点**：构建幻觉检测器通常依赖人工标注，成本高、耗时长；且随着 LLM 快速迭代，旧标注数据很快失效。例如论文中的表 1 显示，同一 GPT-3.5 检测器在面对较新的 LLM（如 GPT-4、Longformer）时，F1 从较早的 0.78 迅速下降到 0.13，说明检测系统需要快速、低成本地适配新模型与新领域。
- **整体研究含义**：论文旨在提供一个**自动化、廉价、能快速适应目标 LLM 系统分布**的幻觉检测器训练数据合成方案，使幻觉检测更准确、快速且长期成本可控。

### 2. 论文提出的方法论
- **核心思想**：不是从零生成人工文本，而是直接**对目标 LLM 的系统回复进行重写（rewriting）**，自动产生成对的“忠实回复”和“幻觉回复”，并以此微调一个轻量级的端到端检测器。此方法利用了“Minor perturbation”（Lucas et al., 2023）的技术思路。
- **关键流程**（三步流水线，见论文图 1）：
  1. **采样（Sampling）**：从目标 LLM 系统中采样真实回复（包含部分潜在幻觉）。
  2. **重写（Rewriting）**：使用一个能力较强的 LLM（论文选用 GPT-4）：
     - 将该回复改写为**忠实回复**（完全被知识与对话历史支持）；该步骤用于清洗系统回复中本身存在的幻觉。
     - 将该回复改写为**幻觉回复**（引导产生与原回复有一定程度相似但不可验证或与事实矛盾的回复）；提示词设计上不预设任何幻觉类别，以获取更真实、多样的幻觉。
     - 对 BEGIN 数据集（三类标注）额外生成 “Generic（笼统/不提供信息）”类回复。
  3. **微调（Finetuning）**：使用上述合成数据微调 T5-base（223M 参数）检测器，用于二分类（忠实/幻觉）或三分类（忠实/幻觉/笼统）。
- **关键优势**：全自动、无需人工标注；由于扰动直接作用于目标 LLM 的回复，训练分布与实际应用分布更一致，易于适配新 LLM。

### 3. 实验设计
- **数据集/场景 1：OpenDialKG-Eval**（知识图谱支持对话场景）
  - 数据来源：基于 OpenDialKG 中的对话与 Freebase 知识库，用 GPT-4 模拟聊天系统生成回复。
  - 构建细节：通过 Amazon Mechanical Turk (AMT) 人工标注 402 条回复；按置信度划分 312 条为测试集、90 条为开发集。
- **数据集/场景 2：BEGIN benchmark**（文档级知识对话场景，三分类：Fully attributable / Not fully attributable / Generic）
  - 包含 4 个对话系统生成的 12k 回复，覆盖 3 个知识领域（Wizard of Wikipedia、TopicalChat、DoG）；仅在公开的 Dev/Test 划分上实验。
- **对比底座（Zero-shot detectors）**：SelfCheckGPT (QA/NLI)、G-Eval、SCALE XL、论文内部的 GPT-4 zero-shot（三分类/二分类）。
- **对比合成数据微调方案**：FADE、HaluEval、AugWOW、BEGIN-Adv。
- **辅助性实验**：
  - 消融实验（只保留一类合成数据）；
  - 幻觉模式定性分析（对比 System 分布 vs. HaluEval vs. FADE vs. Ours）；
  - 生成质量人工评估（对照系统输出、忠实生成、幻觉生成的忠实比例）；
  - 额外跨域评估（OOD，OpenDialKG 训出的模型在 BEGIN 测试集上评估）。

### 4. 资源与算力
- GPU 信息：**论文正文未明确提及 GPU 型号、数量或训练时长**，仅描述延迟评估在 AWS g5.xlarge 实例上执行（零样本 baseline），T5-base 微调模型延迟报为 0.20 sec/条。
- 微调配置：T5-base + LoRA（rank=16，α=32，target_modules = ["q","v"]），batchsize=4，AdamW 优化器，学习率从 {1e-3, 1e-4, 1e-5} 网格调节；OpenDialKG 训练 5 epoch，BEGIN 训练 1 epoch。
- 推断成本亮点：每条合成数据的生成成本为 OpenDialKG 上 0.008 USD、BEGIN 上 0.006 USD（使用 gpt-4-1106-preview），明显低于 AMT 平均 0.20 USD/条的人工标注成本。

### 5. 实验数量与充分性
- 实验数量较全面，涵盖：
  - 主实验两组（OpenDialKG-Eval、BEGIN 测试集，各对比 6~7 个基线）；
  - 消融实验 1 组（检验忠实与幻觉合成数据各自的必要性，表 4）；
  - 模式分析实验 1 组（144 条样本分布对比，表 5/图 2）；
  - 合成质量人工评估 1 组（表 6）；
  - 跨域 OOD 评估 1 组（附录表 13）。
- **充分性与公平性评价**：
  - 优点：对比中尽量做到“apple-to-apple”——微调数据量、开发集选择等做了取舍说明；两个基准数据集（对话、多系统与三分类）具有一定代表性。
  - 不足：OOD 实验仅有附录、规模较小；每个主设置只报告有限随机种子（部分仅两次运行取平均）；数据生成依赖单一 GPT-4 版本，其随机性对生成分布的影响没有单独分析。

### 6. 论文的主要结论与发现
- 在 OpenDialKG-Eval 上，用本文合成数据微调的 T5-base 达到 **F1 0.762**，显著优于既往合成基线 HaluEval（0.702）/FADE（0.625），并超越 SOTA 零样本检测器 SCALE XL（0.687）；
- 在 BEGIN 三分类任务上达到 **F1 0.473**，优于 AugWOW（0.378）与 BEGIN-Adv.（0.459），且高于 GPT-4 internal（0.323）；
- 微调型检测器比所有零样本 baseline 的**延迟低得多**（0.20s vs. 0.22s–60.59s），推断成本优势显著；
- 消融实验证明：忠实与幻觉两类合成数据对训练**缺一不可**（去掉其中一类后 F1 明显下降）；
- 幻觉模式分析发现：相比既有方法偏重“添加新实体/实体替换/交换”，该方法生成的幻觉更贴近真实系统回复分布，主要模式为“给实体添加不可验证属性（Adding attribute）”，KL 散度比 HaluEval/FADE 低（0.34 vs. 0.67/1.53）；
- 人工评估显示该系统能将大约 19% 系统输出中的隐含幻觉转化为忠实回复，而反向转化率极低。

### 7. 优点（亮点）
- **完全自动化**：不需要人为预先定义幻觉类别，提示词通用性好，可方便迁移到摘要、QA 等任务。
- **分布对齐好**：通过在目标系统回复上做局部扰动，训练集与目标分布高度一致，面对新 LLM 迭代时可低门槛快速适配。
- **成本/性能都友好**：训练出的 T5-base 预测速度快、单项合成批次成本低于 AMT 人工标注几个数量级；
- **模式发现新颖**：揭露了“给实体增加未验证属性”这一类此前未充分讨论的真实幻觉模式，和真实系统回复分布更贴近。
- **完整性较好**：主实验+消融+人工评估+跨域评估、开源代码/数据意图明确（承诺发布 GitHub 链接）。

### 8. 不足与局限
- 论文本身明确提及：
  - 合成数据质量受提示 LLM（GPT-4）能力限制；若改写模型表现不佳则数据噪声较大；
  - 生成的幻觉仍可能和真实系统中**非刻意/自发现象**存在差异，提示方法仍未能完全消除偏差；
  - 主动引导大模型生成幻觉内容有“引入虚假信息”的风险，需要配合数据溯源/过滤等合规控制。
- 实验层面：
  - 未披露 GPU 型号与训练时长细节；
  - 未系统性测试目标 LLM 种类变化（如仅用了 GPT-4 模拟的 OpenDialKG 对话系统与 BEGIN 的 4 个系统）、未对多个随机种子稳定做统计分析；
  - BEGIN 测试集只报一次结果（部分取两次运行平均），未有充分方差/显著性检验；
  - 附录中 OOD 结果仅在二分类化后的小范围比较，泛化结论相对有限。
- 设计层面：
  - 幻觉检测器只评估 T5-base 一种架构，未探讨更大/更小检测器的影响；
  - 该方法对多轮对话、知识图谱或长文档等不同格式知识的泛化仍主要以实验形式论证，机制上缺乏系统性表征。

（完）
