---
title: Adaptive LLM Routing under Budget Constraints
title_zh: 预算约束下的大语言模型自适应路由
authors: "Pranoy Panda, Raghav Magazine, Chaitanya Devaguptapu, Sho Takemori, Vishal Sharma"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1301.pdf"
tags: ["query:metacognitio"]
score: 6.0
evidence: 预算约束下自适应路由选择合适LLM以控制成本
tldr: 实际场景缺乏查询与LLM最优配对的完整标注，且用户查询动态变化，监督式路由假设过强。本文将LLM路由建模为上下文赌博机问题，并构建查询与大模型的共享嵌入空间，在预算约束下无需穷举推理即可自适应决策。该方法为在成本和性能之间寻求平衡的LLM部署提供了可扩展的自适应路由方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 583, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 625, \"height\": 317, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 615, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 752, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 715, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1301/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 731, \"height\": 513, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 718, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 799, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 898, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 817, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1301/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 403, \"height\": 263, \"label\": \"Table\"}]"
motivation: 真实场景缺乏最优查询-LLM配对的完整标注，用户查询动态变化，监督式路由难以适用。
method: 将LLM路由建模为上下文赌博机问题，构建查询与LLM共享嵌入空间，在线学习预算约束下的路由策略。
result: 无需对所有查询配对穷举推理即可自适应选择合适大模型，控制部署成本并保持任务表现。
conclusion: 为大模型服务在预算约束下的自适应路由提供了可扩展的在线学习机制。
---

## Abstract
Large Language Models (LLMs) have revolutionized natural language processing, but their varying capabilities and costs pose challenges in practical applications. LLM routing addresses this by dynamically selecting the most suitable LLM for each query/task. Previous approaches treat this as a supervised learning problem, assuming complete knowledge of optimal query-LLM pairings. However, real-world scenarios lack such comprehensive mappings and face evolving user queries. We thus propose to study LLM routing as a contextual bandit problem, enabling adaptive decision-making using bandit feedback without requiring exhaustive inference across all LLMs for all queries (in contrast to supervised routing). To address this problem, we develop a shared embedding space for queries and LLMs, where query and LLM embeddings are aligned to reflect their affinity. This space is initially learned from offline human preference data and refined through online bandit feedback. We instantiate this idea through Preference-prior Informed Linucb fOr adaptive rouTing (PILOT), a novel extension of LinUCB. To handle diverse user budgets for model routing, we introduce an online cost policy modeled as a multi-choice knapsack problem, ensuring resource-efficient routing.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 论文基本信息
- **标题**：Adaptive LLM Routing Under Budget Constraints（预算约束下的大语言模型自适应路由）
- **作者**：Pranoy Panda, Raghav Magazine, Chaitanya Devaguptapu, Sho Takemori, Vishal Sharma（Fujitsu Research）
- **发表会议**：EMNLP 2025 Findings
- **核心贡献**：提出 PILOT——一种基于偏好先验的上下文赌博机路由算法，在仅依赖二元反馈（如点赞/点踩）的条件下，对查询进行预算受限的 LLM 分配。

---

## 1. 核心问题与研究动机

- **背景**：实际部署 LLM 时需要权衡性能与成本。不同模型性能与费用差异悬殊；大型模型质量高但部署/调用昂贵，小型模型廉价但能力有限。例如客服场景中简单问题（营业时间查询）用小型模型即可，复杂推理问题则需要更强（更贵）的模型。
- **现有路由方法的缺陷**：
  - 现有 LLM 路由方法（如 HybridLLM、Routerbench 相关工作）将该问题视为**监督学习**，依赖"每个查询对所有候选 LLM 的最优配对"标注数据集，需要让所有 LLM 回答所有查询以确定最优配对，**标注成本极度高昂**；
  - 缺乏对**查询分布漂移（query distribution shift）**的适应性，一旦用户查询模式变化，静态路由性能下降。
- **本文的核心问题**：能否在**无完整配对标注**、仅依靠"所选模型响应对用户是否满意"的二元反馈（即 bandit feedback）条件下，在预算约束内做自适应 LLM 路由？
- **核心洞察**：该问题与新闻/广告推荐（contextual bandit）的经典场景高度相似——系统只展示少部分新闻/广告，仅能获得被展示物品的点击反馈。

---

## 2. 方法论

### 2.1 总体思路
- 将 LLM 路由重新定义为**预算受限的上下文赌博机（budget-constrained contextual bandit）问题**：
  - 上下文：查询的嵌入向量；
  - 臂（arms）：候选 LLM 集合；
  - 反馈：用户对所选 LLM 响应的评价（如赞/踩），即二元奖励；
  - 约束：连续 Q 个查询的总 token 成本 ≤ 预算 B。
- 构建一个**共享嵌入空间**：查询与 LLM 都被映射到同一向量空间，**余弦相似度即表示查询-模型亲和度（affinity）**。
- 嵌入空间有两个阶段的演化：
  1. 用离线人类偏好数据（ChatArena）**预训练**；
  2. 在线运行时用 bandit feedback **持续精调**。

### 2.2 预训练阶段：基于人类偏好的两阶段学习
- **阶段一（学习查询投影）**：对预训练嵌入模型 ϕ 学习线性变换 ψ(q) = Wϕ(q) + b，参数 W、b 通过**基于余弦距离的三元组损失**在人类偏好数据 D_pref 上训练。利用正/负查询池构造困难负样本（如"Anthropic 偏好的模型在同一查询上输给更小的模型"这一类样本）来增强判别力。
- **阶段二（学习 LLM 嵌入）**：固定阶段一学到的查询投影参数，通过 **softmax 形式的胜率分布 + 二元交叉熵损失**学习每个 LLM 在共享空间中的嵌入 θ_pref。
- **动机**：先固定查询投影再学习 LLM 嵌入，分两阶段训练可避免"移动目标问题"（joint optimization 下余弦目标不稳定）。

### 2.3 在线学习阶段：PILOT 算法
- 基于 **LinUCB** 框架进行扩展：
  - 奖励建模为归一化查询嵌入与归一化 LLM 嵌入的余弦相似度：
    E[r_t | a, q_t] = cos(ψ̂(q_t), θ̂_a) = ψ̂(q_t)·θ̂_a；
  - 维护每个臂的岭回归参数 A_a、b_a；
  - **关键创新**：初始化时注入偏好先验：A⁰_a = λ_a I，b⁰_a = λ_a θ_pref_a（即相当于把预训练 LLM 嵌入作为正则化先验，N(θ_pref_a, (λ_a I)⁻¹)）。λ_a 取模型在预训练阶段精度的倒数，控制先验强度与探索程度；
  - 每轮选择使 UCB 最大的臂：
    argmax_a [cos(ψ̂(q_t), θ̃_a) + α√(ψ̂(q_t)ᵀ(A_aᵗ)⁻¹ψ̂(q_t))]。
- **理论结果**（Proposition 2.1 / C.1）：证明偏好先验初始化的 PI-OFUL 在 ∥θ_pref − θ*∥ ≤ ∥θ*∥ 的条件下，累积遗憾上界**严格 ≤** 标准 OFUL，为"带先验的 bandit 更好"提供了理论依据。

### 2.4 在线成本约束：Online Cost Policy
- 将预算分配问题建模为**在线多选背包问题（Online Multi-choice Knapsack Problem, ON-MCKP）**；
- 采用 ZCL 算法：为每个 LLM（物品）设置值 = 估计奖励（余弦相似度）、重量 = 估计 token 成本，维护预算利用率 z_t，通过**成本-效益资格阈值**筛选可用模型（E_t ⊂ L），再选出最高奖励的 LLM；
- 引入 **binning 策略**：总查询分成 N = ⌈Q/S⌉ 个 bin，每 bin 分配预算 B/N，剩余预算可滚动至下一个 bin，解决 ZCL 无限时域假设在有限 Q 下预算利用不充分的问题；
- 理论保证：Zhou et al. (2008) 定理表明该在线策略性能与"预知全部查询"的最优离线策略差距有界。

### 2.5 算法流程概要
- **Algorithm 1（PILOT）**：先以人类偏好数据做两阶段预训练，再进入在线循环：选 UCB 最大的 LLM → 观察 bt 反馈 → 更新 A、b 参数。
- **Algorithm 2/3（Online Cost Policy）**：按 bin 分配预算，逐查询计算 LLM 成本 Ct，按当前预算利用率设置资格阈值 th_l，选择满足阈值且预测奖励最高的 LLM，并更新剩余预算与利用率 z。

---

## 3. 实验设计

### 3.1 数据与场景
| 组件 | 内容 |
|---|---|
| 路由评估数据 | **Routerbench**（Hu et al., 2024）：36,497 个样本，覆盖 64 任务（MMLU、Hellaswag、GSM8k、Winogrande、ARC Challenge、MTBench、MBPP），包含 11 个 LLM（开源：Llama-70B-Chat、Mixtral-8x7B、Yi-34B-chat、Code Llama-34B、Mistral-7B-chat、WizardLM13B；商用：GPT-4、GPT-3.5-turbo、Claude-instant-v1、Claude-v1、Claude-v2），含每模型的成本与评分。 |
| 预训练偏好数据 | **ChatArena**（Chiang et al., 2024），采样其中两个模型均属于 Routerbench 的 11 模型的子集。 |
| 数据划分 | 1000 样本做超参调优；剩余按**学习桶:部署桶 = 10:1** 划分（模拟流量 A/B 桶学习-部署框架）。 |

### 3.2 测试场景
- **单任务**：MMLU 多选问答（Routerbench 子集）；
- **多任务**：完整 Routerbench（代码生成、数学、多轮对话等）；
- **路由设置**：多 LLM（全集 11 个模型）与二元 LLM 路由（如 GPT-4 vs Mistral-7B；GPT-4 vs Mixtral-8x7B；GPT-4 vs Llama2-70B；Claude-v1 vs Mixtral-8x7B）。

### 3.3 对比方法
- **全一对一路由**：所有查询发给单个 LLM（GPT-4、Claude、Mixtral 等）；
- **上下文赌博机基线**：LinUCB（无偏好先验）、Epoch-Greedy、Explore Only、Random Policy；
- **监督式路由参考**：HybridLLM（Ding et al., 2024）作为监督学习上限类比（附录 D.1）；
- 所有基线的预算分配都统一使用本文的 cost policy，保证对比公平。

### 3.4 评估指标
- 部署桶上的性能-成本曲线；
- 不同学习桶容量下的性能；
- **累积遗憾（cumulative regret）**。

---

## 4. 资源与算力

- **论文中未明确披露**具体 GPU 型号、数量或训练时间。
- 仅提到：查询嵌入主要用 OpenAI text-embedding-3-small（同时用 Instructor-XL 做敏感性测试）、路由时延分析（PILOT 选模型平均耗时 0.065s–0.239s，GPT-4 平均推理时间 2.5s）。
- 需要说明：该论文的实验整体是"基于已有 Routerbench 评测结果"的仿真在线学习（而非重新训练或大规模采样 LLM），实际算力开销较低。

---

## 5. 实验数量与充分性评估

论文实验丰富，说明作者做了大量验证，实验清单包括：

- **主实验**（Figure 3）：单任务/多任务 × 多 LLM/二元 LLM 路由，涵盖性能-成本、学习桶大小、遗憾曲线；
- **在线成本策略对比**（Figure 4、Table 1）：与两种朴素固定预算分配方式（B/Q 或无溢出/有溢出）、与离线最优 P−λC 策略对比；
- **定性路由分析**（Section 5.1）：统计 MMLU/ARC（90% 给 GPT-4）、MBPP（28% 给 Claude）、GSM8K（94% 给 Claude-v1，因性价比高）的分配逻辑，验证路由行为合理；
- **查询复杂度分析**（Table 4）：用 Evol Complexity + Mann-Whitney U 检验表明 PILOT 将更复杂查询送到大模型且差异显著；
- **嵌入模型敏感性**（Figure 5）：换 Instructor-XL 仍保持优势；
- **监督式对比与分布漂移**（Figure 6、7）：与 HybridLLM 对比性能几乎持平或更优；仿真 MMLU→GSM8k 分布漂移证明 PILOT 能自适应而静态监督路由不能；
- **偏好评测**（App. D.3）：其偏好预测精度（65.0）超过 RouteLLM（63.6）；
- **噪声鲁棒性**（Table 5）：5% 噪声下奖励仅掉 <4%；
- **消融**（Table 6）：预训练 router 只有 $1 预算时性能 0.34，加入 10% 在线数据达到 0.61，验证在线学习的重要价值；
- **超参敏感性**（Table 7）：探索参数 α 的倒 U 型影响。

总体评估：**实验覆盖面较广、多角度验证充分**。预算成本对比做了一致策略控制，基线对比公平；但"与监督式路由对比"仅在二元设定下进行、对监督式模型描述的公平性细节稍少，且未做不同模型池规模的系统化泛化测试，可视为一定不足。

---

## 6. 主要结论

- PILOT 在 **多任务（Routerbench 全量）** 场景下，用 **25% 成本**实现了 **GPT-4 93% 的性能**；在单任务（MMLU）下用 **27% 成本**达到 **GPT-4 86% 的性能**，并优于其它 all-to-one 与 bandit 基线。
- 偏好先验初始化能在在线学习初期提供有效冷启动，与纯 LinUCB 相比有望获得更低的遗憾界。
- 在线成本策略有效：在多个预算档位下可略优于或媲美具备全局后见的离线 P−λC 策略。
- 对查询分布漂移有很强的适应能力，这是静态监督路由不具备的。

---

## 7. 优点

1. **问题形式化新颖**：把 LLM 路由从"昂贵的监督标注"转换为 practical 的上下文赌博机设置，只需点赞/点踩极弱反馈即可工作；
2. **先验-在线结合架构**：离线人类偏好预训练（不需要目标数据集）+ 在线 bandit 微调，兼顾冷启动与适应性；
3. **理论贡献**：给出带偏好先验的 OFUL 类算法遗憾界不高于标准 OFUL 的理论证明（Proposition C.1），科学性强；
4. **预算控制机制**：以 ON-MCKP + ZCL + binning 解决在线预算分配问题，对用户友好，可直接调节预算-性能弧线；
5. **实验设计周到**：使用"学习桶-部署桶"划分模拟在线环境，且 cost policy 对全部基线统一施加，在多维度结果上互相印证。

---

## 8. 不足与局限

- **离线学习与在线成本策略解耦**（作者自认）：Algorithm 1 的 bandit 学习阶段完全不考虑预算约束，只在部署阶段用 cost policy 重新挑选模型。这造成"学习到的路由偏好"与"有预算约束的实际服务策略"之间存在次优性；作者把"带预算的在线学习"留作未来工作；
- **场景局限**：只考虑单轮（single-turn）查询路由，未处理真实系统中常见的多轮对话、上下文交互式路由；
- **先验依赖**：需从 ChatArena 获取人类偏好作为预训练信号；若偏好数据与目标任务的模型交集不覆盖目标模型池，预训练效果会受限；
- **成本估计假设**：输出 token 数用调参数据中该 LLM 的平均输出 token 长度近似——对长尾查询可能带来成本估算偏差；
- **未披露算力资源**，无法评估大规模可复现成本；
- **公平性细节**：与监督式 HybridLLM 的对比主要集中在二元模型池且未充分讨论其多种变体下的超参调优差异，存在一定的比较粒度不足。

---

（完）
