---
title: Do Language Models Mirror Human Confidence? Exploring Psychological Insights to Address Overconfidence in LLMs
title_zh: 大语言模型是否反映人类置信度？基于心理学洞见缓解LLM过度自信
authors: "Chenjun Xu, Bingbing Wen, Bin Han, Robert Wolfe, Lucy Lu Wang, Bill Howe"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1316.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 考察模型在各种任务上的过度自信模式并利用人格提示发现置信偏差，提出相应矫正方案
tldr: 心理学认为人的自信判断常出现对难易任务的高估或低估，大模型是否也有类似表现鲜有研究。论文在Llama-3-70B、Claude-3-Sonnet和GPT-4o等一系列问答任务上考察发现，模型对任务难度变化不敏感，并会随着专家/外行、种族/性别等不同角色提示给出带有偏见的置信度，而实际准确率不变。基于这些观察作者提出Answer-F方法缓解过度自信，为模型可信度与校准研究提供心理学视角。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 756, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1641, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1656, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1415, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1662, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1599, \"height\": 1849, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1316/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1654, \"height\": 570, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1387, \"height\": 836, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 527, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 846, \"height\": 711, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1692, \"height\": 902, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 779, \"height\": 1611, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 782, \"height\": 1698, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 778, \"height\": 1695, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1316/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1549, \"height\": 1818, \"label\": \"Table\"}]"
motivation: 人类存在典型过度自信模式，大模型是否遵循类似规律及其受难度与角色影响需要系统探索，以改善校准。
method: 在多种难度问答任务与不同persona提示下测量模型置信度与实际准确率差距，基于心理规律提出缓解过度自信的回答-校正方法。
result: 实验显示模型对任务难度不够敏感且置信度受身份词刻板影响，矫正方法能降低过度自信偏差。
conclusion: 借助心理学框架可解释大模型的过度自信并改进其置信度校准，使自我评估更可靠。
---

## Abstract
Psychology research has shown that humans are poor at estimating their performance on tasks, tending towards underconfidence on easy tasks and overconfidence on difficult tasks. We examine three LLMs, Llama-3-70B-instruct, Claude-3-Sonnet, and GPT-4o, on a range of QA tasks of varying difficulty, and show that models exhibit subtle differences from human patterns of overconfidence: less sensitive to task difficulty, and when prompted to answer based on different personas—e.g., expert vs layman, or different race, gender, and ages—the models will respond with stereotypically biased confidence estimations even though their underlying answer accuracy remains the same. Based on these observations, we propose Answer-Free Confidence Estimation (AFCE) to improve confidence calibration and LLM interpretability in these settings. AFCE is a self-assessment method that employs two stages of prompting, first eliciting only confidence scores on questions, then asking separately for the answer. Experiments on the MMLU and GPQA datasets spanning subjects and difficulty show that this separation of tasks significantly reduces overconfidence and delivers more human-like sensitivity to task difficulty.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：可靠的置信度（confidence）估计是人机协作有效运行的基础，而大语言模型（LLMs）在许多真实任务中表现出系统性过度自信。已有心理学研究表明，人类对自己任务表现的估计能力同样有限——表现为在简单任务上低估自己（underconfidence）、在困难任务上高估自己（overconfidence）。本文试图引入心理学视角，系统考察 LLM 是否遵循类似的过度自信模式，以及其置信度估计对任务难度和角色提示（persona）的敏感性与偏见。
- **核心问题**：论文围绕三个子问题展开：
  1. LLM 的表达置信度是否对任务难度具有合理的校准能力，是否呈现类似人类的"过估/低估"模式？
  2. 模型在不同专家水平的角色（如专家 vs. 外行）下是否呈现过高定位（overplacement）或过低定位（underplacement）偏差？
  3. 人口统计属性（种族、性别、年龄）提示是否会导致模型置信度表达出现系统性偏见？
- **整体含义**：该研究借助心理学中 Moore and Healy (2008) 的信息理论模型来解释模型的过度自信偏差，并提出改进 LLM 置信度校准的新方法（AFCE），对提升模型可信度、可解释性和安全性具有直接价值。

## 2. 论文提出的方法论

- **核心思想**：论文提出 **Answer-Free Confidence Estimation（AFCE，免作答置信度估计）**——将"作答"与"置信度估计"两个过程解耦为两阶段独立提示：
  - **第一阶段（置信度估计）**：仅让模型阅读一组问题，估计自身（或某角色）能答对多少题（0-10），不需给出选项答案。
  - **第二阶段（实际作答）**：单独让模型回答同样的问题，仅给出选项字母。
- **设计逻辑**：作者假设置信度估计与任务执行由不同机制介导；若两者在同一上下文中混用，答案生成过程中的"认知负荷"或"过度思考"会污染置信度判断，导致默认高置信度输出。AFCE 通过隔离两者，使模型能专注地评估自身能力，从而降低过度自信，提升校准性。
- **使用的指标**：采用 **Expected Calibration Error（ECE，期望校准误差）**（M=10 bins）评价校准质量，数学定义为：
  - \( ECE = \sum_{m=1}^{M} \frac{|B_m|}{n} |\text{acc}(B_m) - \text{conf}(B_m)| \)，即各置信度区间内平均置信度与实际准确率的加权偏差。
- **提示模板示例（AFCE 置信度阶段）**："阅读下列问题，估计你能正确回答多少个（0-10），不要提供任何解释。"

## 3. 实验设计

- **数据集/基准**：
  - **MMLU**：选取高中和大学难度的物理、化学、生物子集，代表"高中/大学"难度层级。
  - **GPQA**：博士生/专家创建的高难度物理、化学、生物题，代表"专家级"难度。
  - **补充数据集（开放域泛化测试）**：NaturalQuestions-open（NQ-open）和 SimpleQA，各 100 道开放式问答题。
- **受测模型**：
  - 主实验模型：Llama-3-70B-Instruct、Claude-3-Sonnet、GPT-4o。
  - 附加模型（附录）：Gemma2-9B、LLaMA-3-8B、LLaMA-3.2-90B、Mixtral-8x7B。
- **对比方法（基线）**：
  1. **Vanilla Verbalized Confidence**：要求模型作答并直接报告置信度；
  2. **Top-K Prompting**：要求模型给出 K 个最佳猜测及其概率；
  3. **Quiz-Like Prompting**：仿照 Moore and Healy (2008)，一次回答 10 题并估计答对数；
  4. **Sampling-based**：自随机采样 3 次 + Avg-Conf 聚合；
  5. **Probability-based**：以模型首个生成 token 的概率作为置信度。
- **角色与偏见场景**：
  - **Expertise persona**：随机普通人（randomly chosen person）、专家（expert）、外行（layman）；
  - **人口统计 persona**：种族（White / Black / Asian / Hispanic）、性别（Male / Female / Non-binary）、年龄组（18–24 / 25–39 / 40–54 / 55+）。
- **实验分组形式**：每个 prompt 包含 10 道题为一组（消融中另测试了 5 题一组）。

## 4. 资源与算力

- **论文中未明确报告**所消耗的 GPU 型号、数量或训练/推理总时长。
- 所有模型均以推理方式评估（temperature=0，top-p=1），未涉及模型微调。
- 具体计算资源投入只能从模型规模推理估计（70B 级推理需较高显存如 A100 级集群），但论文中未提供可供复现的算力明细，这是其在可复现性报告上的一个缺憾。

## 5. 实验数量与充分性

- **整体实验量较大且维度丰富**，主要实验组包括：
  - 主校准实验：3 个主模型 × 3 个领域 × 3 个难度 × 6 种置信度方法（表 1）；
  - 扩展模型验证：4 个额外模型 × 全科目/难度矩阵（表 5）；
  - Overplacement 分析：3 个模型 × 3/5 种角色；
  - Demographic 偏见分析：多模型 × 3 大人口维度（性别/种族/年龄）；
  - 消融实验（GPT-4o）：
    - 开放域生成问答（NQ-open、SimpleQA）；
    - 分组数量变化（5 题 vs. 10 题）；
    - 题目顺序随机化。
- **充分性与客观性评价**：
  - 覆盖模型多样（开源 + 闭源、不同规模、不同系列），显著提升结论的可推广性；
  - ECE 为标准校准指标，对比方法覆盖了 verbalized、sampling 和 probability-based 三类主流方法；
  - 消融实验验证了方法的鲁棒性；
  - 然而，主数据集限于科学类多选题（物理/化学/生物），且仅集中于英文问答，缺少跨语言、跨任务类型以及真实部署场景下的验证。论文也依赖 ECE 这一单一校准指标，未使用 Brier Score 等替代指标交叉验证。

## 6. 论文的主要结论与发现

- **（1）模型置信度对任务难度不敏感**：
  - 与人类置信度随难度显著变化不同，LLM（尤其 LLaMA-3-70B 和 Claude-3）的置信度曲线相对平坦，缺乏对难度的适当回归性响应；
  - GPT-4o 相对更敏感，置信度随性能变化存在一定斜坡。
- **（2）AFCE 有效缓解过度自信**：
  - AFCE 在专家级高难任务上显著降低 ECE，如 GPT-4o 平均 ECE 较 Vanilla 降低约 58.4%，较 Quiz-like 降低 63.8%，较 Sampling 降低 65.8%，较 Top-K 降低 15.3%；
  - AFCE 在开放域（SimpleQA/NQ-open）任务上也超越基线，表明其超越多选题格式的可扩展性。
- **（3）Expertise persona 导致置信度远离真实能力**：
  - 所有模型均呈现对"专家"角色的过度置信（overplacement），以及对"外行/普通人"角色的置信度低估（underplacement），而实际答题准确率几乎不受角色影响；
  - 这说明模型置信度受 persona 语义关联的刻板偏见主导，与其真实模拟表现脱节。
- **（4）人口统计属性诱发系统性置信度偏差**：
  - LLaMA-3-70B 与 Claude-3 在承担任何人口属性角色时普遍低估置信度；
  - 但低估程度呈现刻板模式：女性角色置信度低于男性、老年人（55+）和年轻人（18–24)置信度低于中年人（40–54）、不同种族间也存在显著差异；
  - GPT-4o 在这些维度上的置信度偏差相对最小，校准更为均衡。
- **总体**：答案生成与置信度估计由不同机制驱动；心理学启发的方法（AFCE）可以显著改善模型校准，揭示 LLM 置信表达中的系统性偏差并给出应对框架。

## 7. 优点

- **跨学科理论创新**：将 Moore and Healy (2008) 的人类过度自信模型系统迁移到 LLM 评估中，兼具理论深度和工程可操作性，是"心理学 × NLP"交叉研究的良好示范。
- **方法简单且有效**：AFCE 无需访问模型内部状态，仅通过变更提示流程即显著降低 ECE，对 API 白盒/黑盒模型都适用，易于在实际系统中部署。
- **角色扮演实验设计巧妙**：系统地将 persona 干扰从实际准确率中分离出来，清晰展示了模型"置信度表达"与"任务能力"之间的系统性断裂。
- **评估面广、结果扎实**：覆盖多种模型架构（开源、闭源、不同规模）、多难度基准和消融对照（开放域、组大小、顺序），显著增强了结论的外部效度。
- **刻画了伦理风险**：对人口属性角色提示引发的置信偏差进行分析，揭示了角色扮演 AI 在计算社会科学等应用中可能导致误导性结论的风险，具有重要社会价值。

## 8. 不足与局限

- **任务范围局限**：主实验仅覆盖物理/化学/生物多个难度级别的多项选择 QA，缺乏对通用开放域任务、生成式长文本任务（除少量消融外）、代码、数学推理等更深层认知任务的全面覆盖。
- **依赖 ECE 单一指标**：ECE 的 bin 数量与分箱方式会影响数值结果；论文未使用其他校准指标（如 Brier score、可靠性图统计检验）进行交叉验证，结论说服力有限。
- **提示敏感性**：置信度估计本身高度依赖提示措辞；角色扮演提示本身具有诱导性，可能存在"伪偏差"（模型只是遵从测试者预期而调节输出，而非真实反映其先验偏见），但作者对此未做充分的因果剥离。
- **模型类别仍有限**：虽然使用了 7 个模型，但未覆盖 Gemini Pro、PerplexityAI、中文或领域专用模型等，结论向更广泛模型族推广需谨慎。未报告多次运行方差（temperature=0 只能消解采样随机性，无法消解 prompt/顺序扰动）。
- **人类对照数据是借用而非复现**：人类数据取自 Moore and Healy (2008) 的既有论文，题目与本文的 LLM 测试题目不完全一致，人-机对比属于跨实验/跨题目的间接比较，严格性有限。
- **伦理与安全边界**：论文坦承人口统计提示可能加剧有害刻板印象，但未量化或讨论角色扮演系统在实际产品中的伤害缓解机制（如去偏 prompt、输出过滤等）。

（完）
