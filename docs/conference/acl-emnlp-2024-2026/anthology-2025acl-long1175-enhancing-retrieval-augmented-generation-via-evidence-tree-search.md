---
title: Enhancing Retrieval-Augmented Generation via Evidence Tree Search
title_zh: 通过证据树搜索增强检索增强生成
authors: "Hao Sun, Hengyi Cai, Yuchen Li, Xuanbo Fan, Xiaochi Wei, Shuaiqiang Wang, Yan Zhang, Dawei Yin"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1175.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 将证据选取建模为证据树搜索，建模多句证据间的协同依赖以支撑可靠生成
tldr: 检索增强生成中检索文档常含大量冗余或无关内容，而现有证据提取难以建模多句证据间的协同依赖且搜索空间巨大。ETS将证据选择重新表述为证据树搜索，在候选证据集合中寻找最优多句证据组合。该方法同时处理多句证据监督缺乏与计算低效的问题，为下游生成提供更紧凑的证据集。实验显示ETS提高了证据质量和下游生成效果，为证据约束生成提供了可扩展的搜索范式。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1175/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 774, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1175/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1175/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1175/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1175/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 359, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1175/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1643, \"height\": 1266, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1175/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1175/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1668, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1175/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1642, \"height\": 335, \"label\": \"Table\"}]"
motivation: 现有证据抽取难以建模证据句间的协同依赖，且面对指数级候选集合计算低效，影响RAG生成质量。
method: 提出证据树搜索框架ETS，将多句证据选择转化为树搜索问题，以显式建模证据句之间的相互依赖。
result: ETS在证据质量和下游生成任务上均优于基线，并显著降低搜索开销。
conclusion: 用树搜索显式建模证据句间关系可有效提升RAG的证据选择质量和生成可靠性。
---

## Abstract
Retrieval-Augmented Generation (RAG) is widely used to enhance Large Language Models (LLMs) by grounding responses in external knowledge. However, in real-world applications, retrievers often return lengthy documents with redundant or irrelevant content, confusing downstream readers. While evidence retrieval aims to address this by extracting key information, it faces critical challenges: (1) inability to model synergistic inter-dependencies among evidence sentences, (2) lack of supervision for evaluating multi-sentence evidence quality, and (3) computational inefficiency in navigating exponentially growing search spaces of candidate evidence sets. To tackle these challenges, we propose ETS (Evidence Tree Search), a novel framework that reformulates evidence retrieval as a dynamic tree expansion process. Our approach first constructs an evidence tree where each path represents a candidate evidence set, explicitly modeling inter-sentence dependencies through context-aware node selection. We then leverage Monte Carlo Tree Search (MCTS) to efficiently assess evidence quality and introduce an Early-Terminating Beam Search strategy to efficiently accelerate the model inference. Extensive experiments on five datasets demonstrate that ETS significantly outperforms existing methods across different readers. Our code and datasets will be released to facilitate future research.

---

## 论文详细总结（自动生成）

# 中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：检索增强生成（RAG）通过引入外部知识提升大语言模型回答的准确性，但在真实应用中，检索器常常返回包含大量冗余或无关内容的冗长文档，直接输入给读者模型（Reader LLM）会增加处理负担并干扰生成。
- **关键问题**：证据检索（Evidence Retrieval）旨在从长文档中找出支持回答的关键句子，但存在三个核心挑战：
  1. **协同依赖缺失**：相关证据往往由多句信息组成，传统逐句相关性建模无法捕获证据句之间的复杂交互。
  2. **监督信号不足**：多数 RAG 语料只提供文档级相关标注，缺少用于评估“多句证据集合质量”的直接监督。
  3. **搜索空间爆炸**：从长文档中选择多句候选组合，会形成指数级增长的组合搜索空间，使精确求解在计算上不可行。
- **论文含义**：作者提出 ETS（Evidence Tree Search），将证据检索建模为动态“证据树”扩展过程，并用蒙特卡洛树搜索（MCTS）产生质量评估信号，用“早期终止束搜索”加速推理，从而从长文档中定位更紧凑、协同性更强的多句证据集合，最终提升下游 RAG 生成的准确性和效率。

## 2. 方法论

- **整体流程**：
  1. 给定查询和搜索引擎返回的长文章；
  2. 将长文章切分为句子，并利用 BGE 模型过滤出与查询语义相似的候选句，以缩小搜索空间；
  3. 在训练阶段，用 MCTS 构造“证据树”，树中每条从根到叶的路径即为一个候选证据集合；
  4. 从树中提取“正确路径”和“错误路径”，分别训练策略模型（Policy Model）和值模型（Value Model）；
  5. 推理阶段使用“早期终止束搜索”生成高质量证据，并将其作为上下文送入 Reader LLM 回答。

- **MCTS 标注过程**：
  - **选择（Selection）**：从查询节点出发，根据 UCT 公式选择待扩展节点，平衡探索与利用。
  - **扩展（Expansion）**：并行计算把每个候选句加入当前证据集后 Reader 输出正确答案的似然，保留似然最高的 M 个句子作为扩展节点。
  - **模拟（Simulation）**：沿当前路径构造证据集，让 Reader 作答；若答案正确则奖励为 1，否则使用输出正确答案的似然作为奖励。
  - **回溯（Backpropagation）**：从叶节点到根更新访问次数和节点价值。
  - 重复以上模拟直到最大迭代次数或无节点可扩展。

- **模型训练**：
  - 策略模型由预训练 LLM（Qwen2.5-7B-Instruct-1M）初始化；
  - 值模型在此策略模型基础上增加一个带 Sigmoid 的线性层，与 token 预测的 softmax 层共享大多数参数，实现参数高效联合优化；
  - 损失函数包含两项：正确路径上策略模型的负对数似然损失 + 所有路径上值预测的均方误差损失，系数为 β；
  - 该多任务损失让策略模型学会生成正确证据，同时让值模型学会评估每个中间节点最终获得正确答案的期望回报。

- **推理加速**：Early Terminating Beam Search
  - 因为生成目标句子直接来自原文，解码出的前缀可以唯一确定其在原文中的位置时，不再继续逐 token 生成，而是直接对齐原文，大幅减少解码步数；
  - 用已训练的值模型评估扩展候选证据的质量，保留高价值节点；
  - 重复扩展、评估、回溯，直到达到最大深度或无法继续；
  - 最终选取累积价值最高的证据路径作为输出。

## 3. 实验设计

- **数据集（Benchmark）**：来自 LongBench 的 5 个问答数据集：
  - 2WikiMultihopQA、HotpotQA、MuSiQue（多文档问答）
  - MultiFieldQA、Qasper（单文档问答）
  - 评估指标为 EM（Exact Match）和 F1。
- **对比基线**，按三类划分：
  - **检索法**：BM25、BGE-base-en-v1.5、LLM-Embedder（以句子为检索单元，返回 top 句）；
  - **抽取法**：ChatGLM3-6B-128K、Qwen2.5-7B/14B/32B/72B-Instruct-1M（或相应长上下文版本）、GLM-4-9B-Chat-1M 等，通过长上下文模型抽取相关证据；
  - **学习法**：CFIC-7B（“Chunking-Free In-Context Retrieval” 的当前 SOTA），按官方代码和数据实现。
- **下游 Reader**：Qwen2.5-14B-Instruct-1M 与 Qwen2.5-72B-Instruct，控制为给 Reader 提供可比量的文本证据。
- **其他实验**：
  - 消融研究（去掉 Beam Search；去掉 Early Termination）在 2Wiki、HotpotQA、MuSiQue 上开展；
  - 超参数研究（扩展数量 B1、束宽 B2，取值 1–5）在上述三个数据集上开展；
  - 输入长度效应实验（长度从 5000 到 70000），比较 ETS 与直接输入全文；
  - 在 MuSiQue 上做了案例对比，与 BGE-base-en、Qwen2.5-72B、CFIC-7B、GPT-4 的证据定位效果进行定性比较。

## 4. 资源与算力

- 文中明确给出训练/MCTS 的算力配置：
  - MCTS 标注阶段使用 Qwen2.5-7B-Instruct-1M 作为 Reader；
  - MCTS 最大迭代次数设为 20，超参数 w=1.4、β=0.1；
  - 训练集采样 6000 条正确路径与 6000 条错误路径；
  - 策略模型以 Qwen2.5-7B-Instruct-1M 初始化，微调 2 个 epoch、batch size=1、学习率 1×10⁻⁶；
  - 使用 8 张 NVIDIA A100 80GB GPU。
- **未明确信息**：论文未报告具体训练时长、单次 MCTS 标注耗时、推理阶段 GPU 使用与端到端延迟数字（仅在消融/延迟讨论中给出相对基准单位），也未给出对于 14B/72B Reader 部署成本的详细量化。
- 作者还在 Limitations 中承认 MCTS 标注需要多轮模拟，带来额外标注成本。

## 5. 实验数量与充分性

- **实验数量**：比较充分：
  - 5 个数据集 × 2 个 Reader 的主实验；
  - 3 个数据集上的消融实验（去束搜索、去早停）；
  - 3 个数据集上的超参数搜索（B1、B2 各 5 档）；
  - 2 个 Reader × 5 种输入长度的性能/鲁棒性实验；
  - 1 个典型 case study。
- **制度设计**：基线覆盖检索、抽取、学习三大类，且对 Reader 输出证据量做了可比性控制，整体较为公平、客观。消融设计能够验证所提两个关键组件（Beam Search、Early Termination）的价值；不同输入长度实验进一步验证长文档鲁棒性。
- **不足/客观性局限**：
  - 只在 LongBench 的英文 QA 子集上测试，未覆盖更广泛的任务类型和语言；
  - 未报告多次运行的方差或显著性检验，难以判断结果差异的统计稳健性；
  - 训练目标完全来自 Reader 的可答性，可能引入任务偏向；对非 QA 类生成任务缺少检验。
- 总体而言，实验设计系统、基线覆盖面广，足以支撑“有效提升证据质量”的主要结论，但在多样性和统计推断上仍可增强。

## 6. 主要结论与发现

- **全面领先**：ETS 在所有 5 个数据集的两种 Reader 下均优于所有基线。以 Qwen2.5-14B-Instruct-1M 为 Reader 时，相对于最佳基线平均相对提升达 22%。
- **树式证据搜索有效**：将证据检索建模为树扩展过程，能够探索句子组合空间并显式考虑句间依赖关系，比单纯“句子-查询”相似度排序或 LLM 直接抽取效果更好。
- **小 Reader 可以强于大模型**：在相同的证据下，ETS 使 14B 模型能够达到接近甚至超越 72B 长上下文模型的答案质量，说明高质量证据可以大幅减轻 Reader 的推理负担，有降低部署成本的可能。
- **推理效率提升**：Early Terminating Beam Search 能显著降低推理延迟，且输入越长优势越明显；beam search 本身则保证证据空间搜索更充分、避免陷入局部最优。
- **长输入鲁棒性**：随着输入长度增加，ETS 的性能下降幅度远小于“直接使用全文”的方式。
- **超参经验**：扩展数量和束宽设置在约 4 时性能最好；过小会遗漏候选，过大会引入噪声并增加计算成本。
- **案例分析**：ETS 能提供比检索、抽取和对比学习基线更完整、更能帮助读者推导正确答案的证据文本，甚至可与 GPT-4（在定性质性上）相当。

## 7. 优点

- **方法新颖**：用树路径表示证据集合，通过上下文相关的节点扩展来建模证据句之间的协同依赖，直接回应了现有方法“逐句孤立”的缺陷。
- **自监督信号构建合理**：利用 MCTS 的模拟奖励（读者生成正确答案的似然）对节点估值回溯，为多句证据质量提供了密集监督，避免了完全依赖人工标注。
- **训练高效**：策略与值模型共享大部分参数，在一个 LLM 结构上加一个线性层即可；损失函数联合优化生成与价值估计。
- **推理加速巧思**：Early Terminating Beam Search 利用“生成文本是原文子串”这一性质，在解码前缀可以定位原文句子时提前终止，具有实用价值，同时保持搜索广度。
- **实验扎实**：跨多种任务、多种大小模型和三类基线，并做了消融、超参、输入长度和案例研究，结论可信度高。研究者计划开源代码和数据，便于复现与后续研究。

## 8. 不足与局限

- **标注与训练成本高**：MCTS 多次模拟需要反复调用 Reader LLM，带来较高的离线标注开销；作者在 Limitations 也明确承认这一点。
- **模型规模有限**：策略/值模型仅使用 Qwen2.5-7B-Instruct-1M 作为 backbone，没有检验 13B+ 的生成模型是否同样适用或是否需要更多搜索预算。
- **数据集覆盖面窄**：全部来自 LongBench 的问答型任务（尤其是英文多跳 QA），缺少对摘要、多语言、对话、长文档生成等 RAG 常见场景的验证。
- **潜在偏差风险**：
  - MCTS 标注依赖单个 Reader 的判断，可能把该模型的“偏好”写入训练信号；
  - 输入候选句先用 BGE 相似度过滤，若过滤阈值或排序不恰当会提前丢失关键证据；
  - 正确路径与错误路径的自动划分可能受随机一致命中影响，带来噪声标签。
- **对比公平性的细节缺失**：论文没有给出各方法实际“喂给 Reader 的证据量”的可比性量化指标，也没有报告误差线、显著性检验或

…显著性检验或置信区间，因此各方法之间的性能差异是否具有统计显著性，目前难以直接判断，读者无法据此确认某些提升幅度（如 22% 相对提升）是否在随机波动之外仍然稳定成立。

- **可复现性细节不足**：虽然论文声明将开源代码和数据，但未给出完整的超参数搜索配置、候选句过滤阈值（如 BGE 相似度的具体截断值）、MCTS 扩展节点数 `B1` 与束宽 `B2` 在不同数据集上的具体最优取值、以及 Reader 推理时的最大输出长度等关键工程细节，这为后续研究者复现和公平对比增加了一定障碍。

## 9. 综合总结与展望

ETS 论文针对 RAG 中“从长篇文档中寻找多句协同证据”这一关键问题，提出了一个新颖且完整的解决方案：通过将证据检索转化为动态证据树的构建，引入 MCTS 来自动生成多句证据组合的质量监督信号，并用轻量级的策略/值模型联合学习来驱动推理阶段的高效束搜索。该方法在长文档问答基准上取得了全面而显著的性能提升，同时展现出良好的推理效率与长输入鲁棒性，为“检索-生成”流程中的证据筛选环节提供了一条具有实用价值和理论启发的新路径。

从更广的研究视角看，该工作的主要贡献在于：其一，将组合搜索的思想引入证据检索，突破了以往“逐句打分 + 贪心筛选”的局限；其二，通过“模拟生成正确答案的似然”来构造奖励，使训练信号与下游任务目标直接对齐；其三，针对生成式证据抽取设计的早期终止机制，展示了在受限生成任务上利用解码前缀与原文字符串匹配关系进行加速的可行性。这些思路不仅适用于 RAG 的证据检索，也可能启发后续在开放域问答、长文档摘要、事实验证等需要多片段组合推理的任务中借鉴。

当然，该方法的现实落地仍面临训练成本高、依赖单模型标注、评测场景有限等挑战。未来工作值得探索的方向包括：使用更强或更大规模的模型作为策略/值模型骨架以提升证据判断上限；引入多 Reader 集成或人为可读性约束来减少标注偏差；将方法扩展到更多任务类型与语言；以及设计更高效的 MCTS 近似或蒸馏策略以降低离线标注开销。总体而言，ETS 在方法创新、实验严谨性和应用价值方面均表现突出，是证据检索与 RAG 领域一项值得关注的研究成果。

（完）
