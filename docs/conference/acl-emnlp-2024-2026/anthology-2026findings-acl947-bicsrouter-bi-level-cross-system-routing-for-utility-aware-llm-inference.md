---
title: "BiCSRouter: Bi-Level Cross-System Routing for Utility-Aware LLM Inference"
title_zh: BiCSRouter：效用感知的大语言模型推理双层跨系统路由
authors: "Mao Keyu, Eiki Murata, Ukyo Honda"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.947.pdf"
tags: ["query:metacognitio"]
score: 6.0
evidence: 考虑效用与成本的自适应跨系统路由框架，可迁移至基于置信度的接受/精炼/检索/弃答路由
tldr: 该文提出跨系统路由问题，并设计双层路由框架BiCSRouter。它先在系统内部选择最优配置，再通过轻量级路由在两个系统范式（单代理深度推理与多代理协同）间按预测性能与成本选择最优范式。该框架将路由决策拓展到跨计算范式层面，为效用感知的LLM推理提供通用方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1594, \"height\": 827, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 775, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 841, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl947/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 653, \"height\": 430, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1511, \"height\": 953, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 727, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl947/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1503, \"height\": 1111, \"label\": \"Table\"}]"
motivation: 现有路由框架限于单一计算范式，无法在单代理深度推理与多代理协作系统之间进行效用感知选择。
method: 将跨系统路由形式化为双层决策，系统内部学习策略，系统间用轻量路由器按性能与成本选择最佳范式。
result: 实验表明BiCSRouter能在保证效果的同时优化推理成本，优于单一范式内的路由方案。
conclusion: 跨系统路由可拓展LLM推理的服务选择空间，为大规模模型推理降本增效带来新思路。
---

## Abstract
Selecting an appropriate LLM configuration for a given query is critical, yet existing routing frameworks operate within a single computational paradigm. To address this gap, we formalize the Cross-System Routing Problem, a hierarchical decision-making task that decomposes routing into intra-regime configuration selection and inter-regime system selection. Building on this, we propose BiCSRouter, a bi-level cross-system routing framework that integrates two orthogonal regimes: intensive reasoning via single-agent systems and extensive collaboration via multi-agent systems. BiCSRouter performs policy learning within each system and employs a lightweight inter-regime router that selects the optimal regime based on predicted performance and cost. Experiments on the MBPP and MATH benchmarks demonstrate that BiCSRouter outperforms 15 representative baselines across three types. On MBPP, compared to the performance ceiling of GPT-5, BiCSRouter achieves a 46% reduction in cost with only a 2% drop in accuracy. Finally, we show that BiCSRouter can extend to additional regimes, highlighting its generality as a cross-system routing framework.

---

## 论文详细总结（自动生成）

# BiCSRouter：效用感知的大语言模型推理双层跨系统路由

## 1. 论文核心问题与整体含义

**研究动机与背景：**

- 现有 LLM 路由框架（LLM Routing）**局限于单一计算范式（computational paradigm）**：要么只能在单代理系统（single-agent）内部的模型池选模型，要么只能在一个多代理系统（multi-agent）内部选拓扑与角色。
- 单代理系统擅长**深度密集推理（Intensive Reasoning）**——逻辑链条稳定、推理深度强；多代理系统擅长**广泛协作（Extensive Collaboration）**——通过多角色分工提供多样探索。两者具有正交的互补优势，但现有路由方法无法同时利用。
- Gao et al. (2025) 虽初步尝试在两个系统间路由，但采用固定配置、忽略系统内的配置优化，未抓住“系统选择”与“模型选择”的本质差异。
- 作者认为路由系统应跳出模型选择的范畴，进行**跨系统路由（Cross-System Routing）**，在异构计算范式的层面做决策。

**核心意义：**
将路由从范式内的模型选择提升到系统级范式的决策层，形式化定义了**跨系统路由问题（Cross-System Routing Problem, CSRP）**，并提出一个可扩展、效用感知、同时优化性能与推理成本的通用框架 BiCSRouter。

## 2. 方法论

**核心思想：** BiCSRouter 采用层级化双层结构，将路由拆分为**系统内路由（Intra-Regime Routing）** 和**系统间路由（Inter-Regime Routing）** 两个正交子问题，并解耦性能预测与成本预测。

**两种范式定义：**
- **Intensive Reasoning（IR，密集推理）范式**：Ω_ir = M_ir × T_ir，推理图限制为单节点结构，仅允许顺序推理，采用旗舰模型（GPT-5）强化推理深度。
- **Extensive Collaboration（EC，广泛协作）范式**：Ω_ec = M_ec^N × T_ec，允许多代理拓扑（链式、全连接、辩论等），由多个高效模型（GPT-4o mini、Gemini 2.5 Flash、DeepSeek-V3.1）协作完成推理。

**算法流程（按推理阶段）：**
- **阶段一：语义编码**——用 MiniLM 文本编码器从查询 q 提取语义特征 f_q。
- **阶段二：系统内配置采样**——对每个范式 t，通过策略 π_t 在拓扑/策略空间、角色空间和模型池中依次采样配置 c_t（利用 VAE 做潜在空间的语义匹配，角色的分配采用自回归过程），由 REINFORCE 算法优化，奖励为“准确率 − λ·成本”。
- **阶段三：效用估计——** 对每个范式的配置分别预测其预期效用 U_t = P_t − λ·C_t，选用效用更高的系统执行：
  - **性能预测（Polarized Performance Prediction）**：双头 MLP 结构，共享查询难度编码器后分两个独立头预测不同范式的正确概率。训练目标整合二元交叉熵（概率校准）、Uplift Ranking Loss（决策边界优化，带课程学习）和熵正则（防止模式崩塌）。
  - **成本预测（Topology-Aware Cost Predictor）**：模拟推理图拓扑流向，将总成本按拓扑序分解为每个代理的输入/输出 token 成本；输出 token 数通过 MLP 预测，输入 token 数按拓扑规则确定性计算，最终以实际价格（CPT）加权求和。

**关键目标：** 训练时联合优化策略生成损失、性能预测损失与成本预测损失（L_total = λ_re·L_re + λ_perf·L_perf + λ_cost·L_cost）。

## 3. 实验设计

**数据集：**
- **训练/测试**：MBPP（代码生成，500 测试）与 MATH（数学推理，519 测试子集）；训练按 9:1 切分。
- **OOD 评估**：GSM8K（356 条抽样）与 HumanEval（129 条）。
- **扩展评估（NLU 任务）**：MMLU（约 1500 条）与 OpenBookQA（500 条完整测试集）。

**Benchmark 方法（15 个基线，分三组）：**
1. **单代理参考基准**：GPT-4o mini CoT、GPT-5 CoT（性能上限参考线）。
2. **静态多代理架构**：LLM Debate、MacNet、AFlow。
3. **自适应路由方法**：RaterLLM、HybridLLM、GraphRouter、Eagle、RouterDC、AutoMix、BAMAS（low/high）、RouteLLM、MasRouter、MixLLM、Router-R1。

**对比公平性说明：** 对需要两个 LLM 的路由器统一采用 GPT-4o mini（小模型）+ GPT-5（大模型）实现；静态多代理基线引用 MasRouter 原文的 6-agent 数据（不比较成本）；多条结果标注引用自 MasRouter 原文。

## 4. 资源与算力

论文在正文与附录中**均未提供具体的算力信息**——未报告使用的 GPU 型号、数量、训练总时长或参数量等细节。仅报告了学习率（0.001）、批大小（32）、最多 5 个 epoch 加早停、使用 Adam 优化器与 StepLR 学习率调度。因此无法从论文中获知完整的训练资源消耗情况。

## 5. 实验数量与充分性

**主要实验组：**
- **主基准（MBPP/数学推理）**：3 类共 15 个基线的系统性对比。
- **消融实验（4 组）**：去除层间路由、去除层内路由、去除成本预测器、固定单一范式。
- **敏感性分析**：对成本惩罚系数 λ ∈ {10, 20, 30, 40, 50} 的 5 组对比，含随机路由对照。
- **多系统扩展实验**：额外引入 2 个新范式（LR、AC），验证 2/3/4 个系统配置。
- **OOD 泛化实验**：2 个 OOD 数据集上的行为评估。
- **扩展自然语言理解任务**：MMLU + OpenBookQA 上的方法对比。
- **案例研究**：3 种路由决策场景（推理需求、成本效率、边缘案例）的定性分析。

**充分性评价：** 实验覆盖范围较广，考虑了主基准、消融、敏感性、泛化性、系统性扩展、跨任务领域与定性案例，整体充分。但存在一定的偏差风险，例如部分基线（AFlow、LLM Debate、MacNet）使用 MasRouter 报出的结果作为参考而非自行实现，且每条基线只在不太多的模型池配置下测试；多代理静态基线的成本未计入对比；对参差不齐的基线开销（有的成本为 0.06 与 3.78 美元）可能使平均性能对比不完全等价。

## 6. 主要结论与发现

- **跨系统路由可行且高效**：BiCSRouter 在两个基准上始终优于所有单一系统内的自适应路由基线。在 MBPP 上超过自适应路由基线的平均 Pass@1 约 8.99%。
- **性能-成本均衡显著**：在 MBPP 上，相对 GPT-5 单代理性能上限，仅损失约 2% 的准确率，却节省约 46% 的推理成本；在 MATH 上损失 1.34% 准确率但节省 25% 成本。
- **两个层级缺一不可**：去掉层间路由或去掉层内路由均导致明显性能下降；去掉成本预测器则准确率微升但推理成本大幅上升。
- **路由比率自适应分布偏移**：当从训练集转移到更简单的 OOD 基准时，模型会自动减少推理强度范式的选择比例，实现更高效的资源分配。
- **盲目增加系统数无益**：引入额外范式（LR、AC）并不会带来持续的性能增益，反而加剧异构性、扩大搜索空间、增加策略学习难度。
- **框架可扩展**：可自然推广到自然语言理解等其他任务分布，并保持良好成本控制。

## 7. 优点

- **问题建模有创新性**：首次将跨系统路由形式化为层次化双级决策问题，将“配置选择”与“系统范式选择”明确区分，为系统级路由奠定了原则性基础。
- **架构设计解耦清晰**：将性能预测与结构化成本预测解耦，成本预测建模拓扑执行流而非简单回归，在路由时提供可解释的效用链路。
- **级联路由机制合理**：先在两个系统内各自学习最优配置，系统间采用轻量路由，无需训练重型统一的策略。
- **控制粒度上较灵活**：通过成本惩罚系数 λ 可平滑地调节性能-成本偏好（A/B 决策点），且对不同 λ 值表现稳健。
- **泛化验证较全面**：覆盖 OOD 分布（GSM8K、HumanEval）和自然语言理解任务（MMLU、OpenBookQA），实验中还包含多系统扩展分析与决策案例的可视化，论证的广度较好。

## 8. 不足与局限

- **范式内模型池受限**：作者在 Limitations 中承认 IR 范式只使用了一个单一、昂贵的旗舰模型（GPT-5）。更小但通过更强推理策略/深层一致拓扑也可能达到相近性能，存在进一步降本空间。
- **系统扩展性存疑**：实验表明无意义地增加系统数并不能提升表现，反而会放大异质性、扩大搜索空间，使策略学习困难，框架的通用扩展性并未完全证实。
- **资源信息的缺失**：未报告算力、GPU 需求以及训练时间，这对判断路由器的实际部署与训练成本构成障碍。
- **成本指标差异较明显**：IR 固定范式成本为 2.87（MATH）、1.78（MBPP）美元，远高于其他方法，与 EC 固定范式（成本 0.49）等差异悬殊，可能导致成本维度与某些基线的对比不完全一致，但常规成本比较仍能体现优势。
- **实验域范围与偏差风险**：主实验集中于代码与数学推理，虽然扩展了 NLU 任务，但仍限于较窄的任务类型，且未覆盖更开放域的问答或对话任务。部分基线使用第三方报告数据，存在不一致比较的风险。
- **伦理风险**：路由决策可能继承底层 LLM 的偏见，并可能系统性地偏袒某些模型/系统，甚至放大偏见行为；效率的提升也可能降低滥用门槛。作者在 Ethics 部分明确予以了提醒。
- **多代理范式的外部失效模式**：如答辩中的从众（conformity）与谄媚（sycophancy）等问题可能未被显式建模，当前消融只在内部一致性上做了验证，未讨论这些社会性失效模式对路由决策边界的影响。

（完）
