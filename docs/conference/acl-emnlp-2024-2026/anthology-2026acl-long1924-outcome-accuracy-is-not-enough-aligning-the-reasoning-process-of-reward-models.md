---
title: "Outcome Accuracy is Not Enough: Aligning the Reasoning Process of Reward Models"
title_zh: 仅结果准确是不够的：让奖励模型的推理过程对齐
authors: "Binghai Wang, Yantao Liu, Yuxuan Liu, Tianyi Tang, Shenzhi Wang, Chang Gao, Chujie Zheng, Yichang Zhang, Le Yu, Shixuan Liu (刘世萱), Tao Gui, Qi Zhang, Xuan-Jing Huang (黄萱菁), Bowen Yu, Fei Huang, Junyang Lin"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1924.pdf"
tags: ["query:metacognitio"]
score: 4.0
evidence: 研究判断结果准确与推理过程一致性的不一致，对分析自我判断缺陷有参考价值
tldr: 针对生成式奖励模型与LLM裁判可能用错误推理得出正确判断的欺骗性对齐问题，提出Rationale Consistency这一细粒度指标，衡量模型推理与人类判断的一致性。对前沿模型的分析表明该指标能有效区分模型并检测欺骗性对齐，而传统结果准确率指标不能。将推理一致性与结果准确率结合用于训练可改善奖励模型的泛化能力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 765, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1665, \"height\": 1198, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 764, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 743, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 1262, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1924/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 730, \"height\": 609, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 1198, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1663, \"height\": 990, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 779, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1658, \"height\": 1204, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1658, \"height\": 1154, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 857, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 648, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1659, \"height\": 1545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1924/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1659, \"height\": 1552, \"label\": \"Table\"}]"
motivation: 奖励模型和LLM裁判存在用错误理由获得正确判断的欺骗性对齐现象，仅优化结果准确率会损害其泛化能力。
method: 提出推理一致性度量来衡量模型推理过程与人类判断的对齐程度，并设计混合训练信号融合结果准确率与推理一致性。
result: 实验显示推理一致性比结果准确率更能区分前沿模型并检测欺骗性对齐，混合训练能提升奖励模型的泛化性。
conclusion: 奖励模型的评估与训练需关注推理过程一致性，而不仅仅是判决结果准确率。
---

## Abstract
Generative Reward Models (GenRMs) and LLM-as-a-Judge exhibit deceptive alignment by producing correct judgments for incorrect reasons, as they are trained and evaluated to prioritize Outcome Accuracy , which undermines their ability to generalize during RLHF. We introduce Rationale Consistency , a fine-grained metric that quantifies the alignment between the model’s reasoning process and human judgment. Our evaluation of frontier models reveals that rationale consistency effectively discriminates among state-of-the-art models and detects deceptive alignment, while outcome accuracy falls short in both respects. To mitigate this gap, we introduce a hybrid signal that combines rationale consistency with outcome accuracy for GenRM training. Our training method achieves state-of-the-art performance on RM-Bench (87.1%) and JudgeBench (82%), surpassing outcome-only baselines by an average of 5%. Using RM during RLHF, our method effectively improves performance as demonstrated on Arena Hard v2, notably yielding a 7% improvement in creative writing tasks. Further analysis confirms that our method escapes the deceptive alignment trap, effectively reversing the decline in rationale consistency observed in outcome-only training.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：生成式奖励模型（GenRM）和 LLM-as-a-Judge 在训练和评估中仅以"结果准确率（Outcome Accuracy）"为优化目标，导致模型可能学会用**错误的推理逻辑**得出**正确的最终判断**，即"欺骗性对齐（Deceptive Alignment）"。这种模型在静态基准上表现良好，但在 RLHF 等下游场景中泛化能力不佳。
- **背景**：奖励模型在 RLHF 中至关重要，但常见的标量奖励模型不透明，生成式奖励模型虽可输出推理链，但推理链常沦为对既有偏见的"事后合理化"，而非真正驱动判断的逻辑基础。
- **研究动机**：作者认为，只监督结果、不监督推理过程，会让模型学会走捷径（如依赖表面格式、泛泛而谈的风格评价），因此必须显式度量和训练"推理过程与人类判断的一致性"。
- **整体含义**：该研究将"思考过程是否与人类对齐"提升为与结果正确性同等重要的考核维度，为奖励模型训练提供了更稳健的监督信号层级。

---

## 2. 论文提出的方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 提出**推理一致性（Rationale Consistency, RC）**指标，用于度量模型在做出评判时列举的原子化理由与人类专家给出的原子化理由之间的语义匹配程度。
- 提出 **META JUDGE** 评测框架，对模型推理过程与人类判断进行细粒度可比对的结构化评估。
- 训练阶段，设计**混合奖励**：$R_{final} = R_{rationale} \times R_{outcome}$，即"只有结果正确且推理也正确，模型才能获得高奖励"，保证结果是推理的逻辑必然。

### 关键技术细节

**1. 基准构建（原子化理由分解）**
- 选取人类专家标注偏好数据集 HelpSteer3（覆盖 General/Code/STEM/Multilingual 四个领域），每个领域各采样 250 条，共 1,000 条构成 HelpSteer3-Atomic。
- 利用 GPT-5 将自由文本的人类评语分解为互斥且证据具体的"原子理由"，每条样本保留 3–7 条原子理由。
- 额外构建创意写作基准 **CW-Atomic**，由 3 名标注者独立标注 350 条样本、删除不一致数据后剩 207 条，用于评估跨领域与跨标注者泛化性。

**2. META JUDGE 语义匹配**
- 评估时要求模型先输出按重要性降序排列的原子理由列表，再由 LLM 评估器将人类原子理由与模型理由进行**严格的一对一语义匹配**，打分范围 $[0,1]$，具体匹配以最优匹配 $\pi$ 计算总分：
$$S_{total} = \max_\pi \sum_{(i,j)\in\pi} s_{ij}$$
- 推理一致性定义为平均软召回率：
$$RC = \frac{1}{N}\sum_{k=1}^{N} \frac{S_{total}^{(k)}}{|R_h^{(k)}|}$$

**3. 训练奖励**
- 结果奖励：二元信号，模型偏好与人类标签一致为 1，否则为 0。
- 理由奖励：采用**平均精度（Average Precision, AP）**，对模型输出的理由列表引入软排序约束，使更贴近人类认知的核心理由排在前面：
$$R_{rationale} = AP = \frac{\sum_{k=1}^{|R_{ai}|} \bigl(P@k \times I(k)\bigr)}{|R_h|}$$
- 混合奖励采用乘法门控形式：$R_{final} = R_{rationale} \times R_{outcome}$（对照加法形式见消融，加法虽分数略高但导致 16.5% 的推理-结果不一致率，而乘法则仅为 0.9%）。
- 优化算法：采用 **GRPO (Group Relative Policy Optimization)**，每组采样 8 条输出，组内标准化奖励计算优势，并带 KL 散度约束。

---

## 3. 实验设计：数据集、Benchmark 与对比方法

### 评测数据集/Benchmark

- **HelpSteer3-Atomic**：基于 HelpSteer3 构建的原子化理由基准，共 1,000 条，四个领域（Code/General/Multilingual/STEM）。
- **CW-Atomic**：创意写作领域新标注数据集（207 条），由不同标注者群体标注，作为跨域、跨标注者的 OOD 测试集。
- **RM-Bench**（Chat/Code/Math/Safety 四类判别任务）与 **JudgeBench**（Knowledge/Reasoning/Math/Code 深度推理判别任务），两者合计取平均作为总指标。
- **Arena Hard v2**（Hard Prompt 与 Creative Writing）用于下游 RLHF 对齐效果验证。

### 模型评估对象

- 共评估 19 个前沿 LLM / LLM-as-a-Judge，覆盖 GPT、Gemini、Claude、DeepSeek、Qwen 等模型系列，如 GPT-5、o3、o3-mini、GPT-4.1、Gemini 3 Pro/Flash、Claude 3.5/3.7/4/4.5、DeepSeek-R1、Qwen3 系列等。
- 评测器使用 Qwen3-Plus（主）与 DeepSeek-R1（对照），验证对评测器选择的鲁棒性。

### 训练与对比方法

- 训练基座模型：Qwen3-14B 和 Qwen3-30B-A3B 两种规模。
- 控制器：**Ours（结果+推理监督）** vs. **Outcome-Only（仅结果监督）**，严格保持训练管线一致、仅改变奖励来源。
- 对比 SOTA 方法：标量 RM（Skywork-Reward-*）、GenRM（RM-R1、RRM-32B、Nemotron-Super、GRAM-R²、Principles-Qwen32B 等）、LLM-as-a-Judge（GPT-4o、Claude-3.5-Sonnet、DeepSeek-R1-0528）。
- 下游 RLHF 验证：将训练好的 GenRM 接入 Qwen-30B-A3B-Base 的 GRPO 对齐流程，与 Outcome-Only 奖励模型对比。

---

## 4. 资源与算力

- 论文正文与附录**未明确给出训练所用 GPU 型号、卡数及总训练时长**。
- 附录 D 仅提供了超参数层面的间接信息：
  - GenRM 训练：学习率 $2\times10^{-6}$、batch size 256、mini-batch 128、每组采样 8 条、最大生成长度 12K tokens、最大提示长度 8K tokens、总训练 2 epochs。
  - 下游对齐训练：batch size 512、mini-batch 128、每组采样 8 条、90 步训练。
- 结论：资源与算力细节披露不足，仅能根据模型规模（14B、30B-A3B）和超参大致推测训练开销不可忽视。

---

## 5. 实验数量与充分性

### 实验数量汇总

| 实验类别 | 数量/范围 |
|---|---|
| 大规模模型评估 | 19 个前沿 LLM，跨 4 个领域、2 个基准（HS-Atomic + CW-Atomic） |
| 评测器鲁棒性检验 | 2 种评测器交叉验证（Qwen-Plus vs. DeepSeek-R1） |
| GenRM 训练主实验 | 2 种模型规模 × 2 种奖励信号（Ours vs. Outcome-Only） |
| 下游 RLHF 验证 | Arena Hard v2，Hard Prompt + Creative Writing 两子集 |
| 消融实验 | 奖励形式（乘法 vs. 加法 vs. 仅推理）、训练动态对比 |
| 分析实验 | 训练动力学曲线、推理退化 Flaw Tag 分布（F1–F7）、一致性率对比、案例研究 |
| 案例研究 | 多个细粒度案例分析（表 1、表 6、表 7、表 10、表 11 等） |

### 充分性评估

- **充分之处**：
  - 多角度消融（奖励形式、信号来源、模型规模），验证了"乘法门控"的必要性。
  - 训练动态对比直观展示了"结果奖励相近但推理奖励发散"的关键现象。
  - OOD 测试（CW-Atomic）增强了结论的普适性。
- **可改进之处**：
  - 训练基座仅限 Qwen 系列，未见在其他模型家族（如 Llama、Mistral）上的可复现性验证。
  - 下游 RLHF 仅评估了 30B-A3B 一个规模。
  - 评测器为 LLM，虽然作者验证了对两种评测器的鲁棒性，但 LLM 匹配的边界情况仍需更大规模人工校验。
  - 未比较"推理一致性指标"与"其他过程奖励（PRM）"在计算成本上的差异。

---

## 6. 论文的主要结论与发现

1. **结果准确率无法检测欺骗性对齐**：o3 与 o3-mini 的结果准确率相近，但 o3-mini 的推理一致性比 o3 低约 50%。类似模式也出现在 Gemini 3 Pro 与 Gemini 3 Flash 之间。
2. **结果准确率对前沿模型区分度不足**：前沿模型在结果准确率上趋于饱和（约 0.76–0.82），而推理一致性（RC）可拉开显著差距（约 0.2–0.4），具有更大的区分度。
3. **仅结果监督会导致推理退化**（Rationale Degeneration）：outcome-only 训练使模型从证据导向型（EG）推理转向基于泛泛而谈准则（CG）或风格化描述（GS）的捷径推理，证据型理由比例从 93.6% 降至 45.4%。
4. **混合监督显著提升 GenRM 能力**：在 RM-Bench 上达到 87.1%，在 JudgeBench 上达到 82.0%，总平均分超过仅结果监督基线（84.6% vs. 80.3%），在 JudgeBench 代码域提升超过 7%。
5. **混合训练提升了下游 RLHF 效果**：在 Arena Hard v2 上，Creative Writing 得分从 62.00% 提升至 69.08%（+7%），Hard Prompt 从 19.10% 提升至 21.22%。
6. **评测器选择对 RC 度量影响很小**：不同 LLM 评测器得分高度一致（$R^2=0.983$, RMSE=0.006），证明 RC 度量是稳健的。
7. **即使最强模型也仅为 40% 左右推理一致性**：当前 LLM 的推理逻辑与人类判断仍有很大差距，合成数据替代人类标注尚不可靠。

---

## 7. 优点

1. **问题提出富有洞察力**：将"欺骗性对齐"从抽象安全概念落地为可量化的具体指标，适合奖励模型场景，论述清楚、有案例支撑。
2. **方法论设计精妙**：
   - 使用原子化分解把不可比的自由文本理由转变为可逐条匹配的清单，为推理过程建立可靠评估基础。
   - META JUDGE 采用严格的一对一匹配并限制输出长度，防止模型用"一条宽泛理由配多个人类理由"的投机行为。
   - AP 训练的软排序约束既衡量召回又衡量排序优先级，比无序 F1 更精细地刻画推理质量。
3. **训练信号设计具有门控逻辑**：乘法形式强制"正确结论必须由正确推理得出"，在单一框架内同时调节结果与过程，很有力地抑制了推理和结果脱节的问题。
4. **实证分析深入**：训练动态曲线（结果奖励相似、推理奖励发散）、Flaw Tag 分布变化（F1–F7）、案例对比等多层次验证让"推理退化"现象有迹可循。
5. **评估规范有力**：同时采用同域（HS-Atomic）与跨域（CW-Atomic，且标注者不同）验证，有效控制域内过拟合风险。

---

## 8. 不足与局限

1. **注释成本高、可扩展性不足**：RC 度量要求高质量人类原子化标注，构造代价大；作者坦承新领域/新语言需同等标注力度，当前定位是验证"理由级监督的价值"，而非全可扩展管线。
2. **基座模型覆盖窄**：训练验证仅在 Qwen3-14B 与 Qwen3-30B-A3B 上执行，未验证在 Llama/Mistral 等第三方底座上的独立效果。
3. **评测器本身是 LLM**：RC 计算依赖 LLM 语义打分，虽然验证了两评测器间一致性较强，但打分偏差无法完全排除，需要在更广泛评测器集合上验证。
4. **合成理由无法完全替代人类理由**：论文依赖 GPT-5 将人类自由文本分解为原子理由，虽然人工抽检 93 条，但系统性偏差（分解遗漏或引入幻觉）的风险仍在。
5. **训练数据与评测数据同源**：HelpSteer3-Atomic 既用于训练又用于评测，在 HelpSteer3 域内分数可能偏高，跨域（CW-Atomic）提升幅度也明显更小（+1.4% vs. +12.13%），说明仍有面向新域的过拟合风险。
6. **计算资源未披露**：仅给出超参（epochs、batch、采样数），未说明 GPU 型号、卡数与训练耗时，降低复现便利性。
7. **加法 vs. 乘法消融深度不足**：加法 0.8 权重取得的总分更高，作者以"16.5% 推理-结果不一致率"为由否定了加法方案，但对于"分数优先还是稳健性优先"未见进一步权衡讨论；未来可做更系统的多目标联合优化探索。

---

（完）
