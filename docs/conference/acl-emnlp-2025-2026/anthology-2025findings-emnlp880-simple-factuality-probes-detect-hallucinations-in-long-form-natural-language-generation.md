---
title: Simple Factuality Probes Detect Hallucinations in Long-Form Natural Language Generation
title_zh: 简单事实性探针检测长文本自然语言生成中的幻觉
authors: "Jiatong Han, Neil Band, Muhammed Razzak, Jannik Kossen, Tim G. J. Rudner, Yarin Gal"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.880.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 使用轻量探针基于隐藏状态单样本检测长文本生成中的幻觉
tldr: 长文本生成中的幻觉检测通常需要多次采样，计算成本高。该工作发现大模型隐藏状态对长文本事实性具有很强的预测能力，提出用轻量探针从单次采样中高效检测幻觉。在多种长文本任务上，该简单基线能达到与昂贵多采样方法相近的性能，为推理时幻觉检测提供了低成本方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1317, \"height\": 631, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1564, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1576, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1328, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1515, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp880/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1653, \"height\": 434, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 1002, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 968, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1655, \"height\": 768, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 558, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 883, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1661, \"height\": 1213, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp880/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 478, \"label\": \"Table\"}]"
motivation: 现有幻觉检测依赖大量采样，代价高，难以用于前沿大模型长文本。
method: 利用隐藏状态训练轻量探针，仅需单次生成即可预测事实性。
result: 该探针达到与多采样方法相当的检测性能。
conclusion: 隐藏状态可高效支持幻觉检测，简化了长文本生成的事实性监控。
---

## Abstract
Large language models (LLMs) often mislead users with confident hallucinations. Current approaches to detect hallucination require many samples from the LLM generator, which is computationally infeasible as frontier model sizes and generation lengths continue to grow. We present a remarkably simple baseline for detecting hallucinations in long-form LLM generations, with performance comparable to expensive multi-sample approaches while drawing only a single sample from the LLM generator. Our key finding is that LLM hidden states are highly predictive of factuality in long-form natural language generation and that this information can be efficiently extracted at inference time using a lightweight probe. We benchmark a variety of long-form hallucination detection methods across open-weight models up to 405B parameters and demonstrate that our approach achieves competitive performance with up to 100x fewer FLOPs. Furthermore, our probes generalize to out-of-distribution model outputs, evaluated using hidden states of smaller open-source models. Our results demonstrate the promise of hidden state probes in detecting long-form LLM hallucinations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、论文的核心问题与整体含义

### 研究动机
- 大语言模型（LLM）在生成长文本时经常伴随**带有高度自信的幻觉**（confident hallucination），例如代码库级编辑、多页技术报告、推理辅助等前沿应用场景，单次生成可达数万 token，幻觉风险显著放大。
- 现有幻觉检测方法（如语义熵、自一致性、图不确定性）**依赖从生成模型中多次采样**，而前沿模型参数量已达数百亿甚至数千亿，多次采样在计算上**不可行、不经济**。
- 因此，需要一种**仅需单次生成即可提供细粒度事实性评分**的高效检测方法，使模型能在生成的同时标注输出中哪些部分可信、哪些需要人工核实。

### 核心发现
- 论文的核心经验发现是：**LLM 的隐藏状态（hidden states）对长文本生成中声明级别（claim-level）的事实性具有高度预测能力**。
- 通过轻量探针（probe）从隐藏状态中提取事实性信号，可以在推理时以极低开销实现长文本幻觉检测，性能可与昂贵的多采样方法媲美。

## 二、论文提出的方法论

### 核心思想
- 在一个长文本生成中，将输出分解为**原子声明（atomic claims）**，对每个声明提取 LLM 的隐藏状态表示，然后训练一个轻量分类器（探针）来预测该声明为真的概率。

### 训练流程（Algorithm 1，两阶段）
1. **阶段一：生成监督事实性数据集**
   - 给定提示池 D_prompt，用生成模型 π_gen 生成一个长文本输出 z；
   - 用辅助模型 π_aux 将 z 分解为原子声明集合 C；
   - 对每个声明 c，用编码器 LM（可以是生成模型本身 π_gen，或更小的模型 π_small）提取隐藏状态 h_c；
   - 用检索增强验证器 f_ret（如 Wikipedia 检索或 Web Search API）作为"oracle"为声明打上二元标签 y_c ∈ {0,1}；
   - 汇总所有 (h_c, y_c) 对构成训练集 D_probe。
2. **阶段二：拟合探针**
   - 训练一个简单分类器 f，将隐藏向量映射为事实性概率 p(y=true|c) = f(h_c; θ)。
   - 候选分类器：
     - **稀疏逻辑回归（Sparse Logistic Regression）**：带 L1 惩罚，目标是 min_θ (1/|C|) Σ L(y_c, f(h_c;θ)) + λ‖θ‖₁；
     - **XGBoost**：梯度提升决策树，可捕捉隐藏状态坐标间的非线性交互。

### 推理流程（Algorithm 2，五步）
1. **答案生成**：生成模型 π_gen 对提示 x 产生长文本完成 z；
2. **声明分解与跨度归属**：辅助模型 π_aux 将 z 分解为 (c, S(c)) 对，其中 S(c) = [s(c), e(c)] 是声明对应的连续 token 跨度；跨度不重叠，冲突时归给最先检测到的声明；
3. **隐藏状态提取**：用 π_gen 或 π_small 对每个声明 c 编码获得隐藏状态 h_c；
4. **探针评估**：探针 f 将 h_c 映射为事实性概率 p̂_c = f(h_c) ∈ [0,1]；
5. **细粒度事实性可视化**：将声明级事实性分数传播回对应的 token 跨度，以红绿热图形式覆盖在原始文本上（绿色=可信，红色=需核验），实现直观的可视化。

### 关键设计细节
- **隐藏状态选择**：实验表明，**最后一个 token（Last Token）的隐藏状态**效果最佳，优于首 token 和倒数第二个 token（见图 6 左侧）。
- **层选择**：单层与 5 层分组拼接效果相当（图 6 右侧），未带来显著提升。
- **主观性过滤**：对测试声明进行主观性过滤（剔除主观、不可验证的声明，遵循 Jiang et al. 2024）通常能提升探针性能（图 5）。

## 三、实验设计

### 数据集与 Benchmark
- **训练集**：LongFact 数据集（Wei et al., 2024），涵盖多种话题（25–75 个主题，不同模型因 token 长度差异而主题数不同），使用 Web Search API 做检索验证；
- **测试集**：FActScore 数据集（Min et al., 2023），30 个 Wikipedia 人物实体，使用 Wikipedia 文档检索验证。

### 生成模型（π_gen）与辅助模型（π_aux）
- **π_gen**：Llama 3.2-3B、Llama 3.1-8B、Llama 3.1-70B、Llama 3.1-405B、Gemma2-9B；
- **π_aux**：GPT-4o-mini（用于声明分解、问题生成、等价性判断等）；
- 生成长度上限 512 token，温度 0.7，top-k=50。

### 对比基线
- **Semantic Entropy（SE）**：随机生成问题后多次高温度采样，计算回答分布的语义熵；
- **P(True)**：让模型对自身声明进行多备选回答评估；
- **SelfCheckGPT**：模型在已有上下文基础上自检声明的正确性；
- **Graph Uncertainty（图不确定性）**：包括 Self-Consistency + Verbalized Confidence（SC+VC）和 Closeness Centrality（Cc），对多次采样结果构造二分图，用中心性指标量化不确定性；
- **Verbalized Confidence（PH-VC）**：直接询问模型自身声明为真的可能性。

### 主要实验维度
1. **域内与跨域测试**：在 LongFact 上训练，在 FActScore 人物传记声明上测试（跨域泛化）；
2. **跨模型泛化**：同一模型系列内小模型探针 → 大模型输出（如 3B 探针检测 405B 输出）；
3. **跨架构泛化**：开源模型探针 → 闭源模型输出（GPT-4o-mini、InstructGPT、ChatGPT、PerplexityAI）；
4. **校准分析**：按探针分数阈值保留数据，观察保留数据的准确率变化（rejection ratio vs accuracy）；
5. **反转域测试**（附录 C.2）：在 FActScore 上训练，在 LongFact 上测试，验证域迁移方向的影响；
6. **稀疏探针与神经元引导**（附录 E）：仅使用少量选中神经元的激活值训练探针，并尝试通过"钳制"（clamping）神经元激活值来因果性地减少幻觉。

## 四、资源与算力

- 论文明确说明：**总实验消耗约 440 GPU 小时（A100 节点）**，来自 OATML 实验室自有机器和第三方云供应商，总计约 **2×10²⁰ FLOPs**（与图 2 的横坐标对应，乘以测试实体数量）。
- 方法本身的推理开销：**仅需对每个声明做一次前向传播**，对比采样方法（如 Cc@10）在 Llama3.1-405B 上节省约 **两个数量级（约 100 倍）的 FLOPs**。
- 论文还提到：LongFact 验证成本约为 **每 1,000 个声明 6.6 美元**（约 1/3 用于 token 生成、2/3 用于搜索查询），而探针方法可显著规避这类检索验证开销。
- 注意：论文未给出单个实验的详细时间分解，也没有明确 A100 的具体数量与卡时拆分。

## 五、实验数量与充分性

### 实验覆盖情况
- 覆盖 **4 个模型家族规模梯度**（3B、8B、70B、405B）外加 Gemma2-9B，共 5 个开源模型；
- 对比了 **6 类主流基线**（SE、P(True)、SelfCheckGPT、SC+VC、Cc、PH-VC），每个基线最多测试了 k=2、3、5、10 四种采样规模；
- 进行了**跨域**（LongFact→FActScore）、**跨模型规模**（小→大）、**跨架构**（开源→闭源）三类泛化测试；
- 提供了**消融实验**：token 位置（FT/SLT/LT）、层分组大小（1 vs 5）、分类器类型（LR vs XGBoost）、主观性过滤（有/无）、反转域测试；
- 提供了**校准分析**（rejection ratio vs accuracy）和**统计显著性**报告（bootstrap 标准误，95% 置信区间）；
- 附录中还包含**神经元级因果干预实验**（clamping 神经元激活值提升事实性）。

### 充分性与公平性评价
- **优点**：实验体量较大，模型规模跨度广，对比基线全面，且所有指标均带 bootstrap 置信区间，方法间对比在同一测试声明集上进行；
- **细节**：SE 因成本过高只随机抽取了 20% 的测试声明进行评估，这是一个**实际妥协**，可能在对比中引入一定偏差；训练与测试声明数量存在较大差异（表 5），但作者对此做了说明（较大模型需要更多训练声明才能有效）；
- **局限性**：所有实验集中于英文生成场景，未覆盖多语言、多模态或更长上下文（>512 token）场景；对闭源模型的测试依赖较小规模的开源模型训练探针，OOD 性能虽有意义但绝对增幅有限。

## 六、论文的主要结论与发现

1. **探针性能与多采样方法相当，开销低 100 倍**：Factuality Probes 在长文本事实性检测（AUROC）上与 SE、P(True)、SelfCheckGPT 等昂贵方法相当或更优，与 Graph Uncertainty 类方法（SC+VC、Cc）性能持平，但计算成本仅为其几乎百分之一；
2. **检测性能随模型规模对数线性提升**：从 3B 到 405B，AUROC 从约 0.726 提升至约 0.758（域内），呈一致的 log-linear 趋势；
3. **跨域泛化性强**：在 LongFact 上训练的探针可以很好地迁移到 FActScore 人物传记声明上，且优于 5 次采样的采样基线；
4. **跨模型泛化有效**：
   - 同一模型系列内：3B 探针可以检测 405B 的输出（AUROC≈0.70），性能与域内相当；
   - 跨架构：开源模型探针可以检测 GPT-4o-mini、InstructGPT、ChatGPT 等闭源模型的输出（最佳 AUROC≈0.73），说明 LLM 内部的事实性表征具有一定**普遍性**；
5. **探针分数校准良好**：多数模型（8B 以上）的探针置信度与实际事实性存在清晰正相关；拒绝低置信度声明可稳定提升保留数据准确率；
6. **线性探针的高效性可归因于三点**：标准化声明格式、最终 token 的信息瓶颈、以及绕过"问题生成"这一中间环节直接访问语义表征；
7. **神经元级可解释性**：少量事实性神经元即可支撑探针性能，且通过 clamping 这些神经元的激活值可**因果性地**提升模型的事实性（如 Llama3.1-8B 的 FActScore 从 0.599 提升至 0.664，+10.9%）。

## 七、优点

- **极简高效**：方法本身只是"隐藏状态 + 线性探针"，但系统性地验证了其在长文本场景下的有效性和跨模型泛化能力；
- **工程上可行**：只需一次 generate() 调用，探针轻量、

# 续：第七节（补全）至全文结束

## 七、优点（续）

- **工程上可行**：只需一次 `generate()` 调用，探针轻量、训练快速，且隐藏状态在生成过程中即可同步提取，无需额外的模型调用或外部检索验证（仅在训练阶段需要验证器标注）；
- **可视化友好**：将声明级分数映射到 token 跨度生成红绿热图，用户可直接看到文本中哪些句子可信、哪些需要人工核对，这在事实性标注工具链中具有很高的落地价值；
- **因果干预见成效**：不仅做"检测"，还尝试通过 clamping 事实性神经元来直接降低幻觉输出，将检测结果转化为可操作的生成干预，方向新颖且有实际意义；
- **开源与诚实**：代码、数据生成脚本和探针权重均开源，实验细节（如 GPU 小时数、FLOPs 估算、验证成本）披露充分，可复现性强。

## 八、缺点与局限性

### 1. 对"声明分解"环节的强依赖
- 方法整体效果高度依赖辅助模型（GPT-4o-mini）的声明分解质量。若分解产生过长或过短的声明、遗漏关键限定语（如时间、地点、条件），探针的输入表示会失真，从而影响事实性判断。论文并未深入分析声明分解错误对最终结果的传导误差。

### 2. 标签噪声与验证器偏差
- 训练标签依赖 Web Search API 或 Wikipedia 检索。对于模糊、时效性强或来源稀疏的声明，检索验证器的标签本身可能不准确，导致探针学习到的是"验证器的判断"而非"客观事实性"。论文对验证器的准确率评估不充分。

### 3. 评估长度受限
- 所有实验的生成长度上限为 **512 token**，这与论文宣称的"代码库级编辑、多页报告"等超长文本场景有明显差距。512 token 只能算"中等长度"，真正的超长文本（数千至数万 token）中的幻觉模式（如跨段落矛盾、章节间一致性）未得到验证。

### 4. 场景与语言覆盖窄
- 实验仅覆盖英文维基百科式知识型声明，未涉及代码、数学推理、多轮对话、多语言或多模态输入。不同领域的隐藏状态表征可能存在系统性差异，探针的通用性结论尚不稳固。

### 5. 探针性能上限有限
- 最佳域内 AUROC 约 0.75–0.76，虽然与多采样方法持平，但绝对准确率并不高。这意味着探针更适合作为"风险预警器"而非"权威事实性判断器"，在高风险场景中仍需人工复核。

### 6. 对模型内部表征的机制解释不足
- 论文观察到多个模型家族存在"事实性方向"（factual direction），但对这一方向的形成原因、与模型训练过程的因果关系解释停留在推测层面。clamping 实验虽证明了因果性，但仅是对线性方向的粗粒度干预，与实际的幻觉产生机制之间仍有解释鸿沟。

### 7. 训练与推理不对称
- 训练阶段需要大量检索验证（约 6.6 美元/千声明），虽然是一次性成本，但对于持续更新新领域、新版本的生成模型，重复构建训练集的成本会积累；探针的域迁移能力也并非始终无损（附录中的反转域实验显示方向性依赖）。

## 九、主要创新点

1. **首次系统论证"单次生成 + 隐藏状态探针"在长文本事实性检测上的可行性与高效性**，将事实性检测的成本从多采样（×10）压缩到几乎为 0 的边际开销；
2. **声明级隐藏状态对齐框架**：将原文中的声明文本对齐到生成期间实际产生困惑与斟酌的 token 位置，利用最终 token 的隐藏状态作为声明级语义的压缩表示，既有理论直觉又有实证支撑；
3. **跨模型、跨架构泛化的发现**：证明隐藏状态中的事实性信号具有一定的"普适方向性"，为未来训练"通用事实性探针"提供了可能；
4. **将探针与神经元归因连接**：通过稀疏逻辑回归识别的正权重神经元与 clamping 实验结合，实现了从"检测"到"干预"的闭环，开启了对幻觉进行在线纠偏的新路径。

## 十、不足与改进方向

### 方法层面
- 探索**自适应层选择**（而非固定最后一层/固定分组），针对不同模型动态挑选事实性表征最强的层；
- 将探针从二分类扩展为**多维度事实性属性预测**（如来源性、时间性、可验证性分开打分）；
- 引入连续生成过程中的**在线累积信号**，而不仅是生成结束后的静态隐藏状态。

### 实验层面
- 在**更长文本（2k–10k token）**、**多语言**、**代码/数学**等更多场景下验证；
- 将标签来源从检索验证扩展到多模型共识验证或人类标注，对比不同标注质量对探针上限的影响；
- 对声明分解进行扰动分析，量化辅助模型误差的传导。

### 理论层面
- 用可解释性工具（如 SAE、logit lens、激活补丁）深入分析"事实性方向"的语义内涵，理解它在模型前向传播中的具体作用路径；
- 探索**跨时间漂移**：当生成模型更新版本后，旧探针的失效速度与再训练成本如何权衡。

### 落地层面
- 将探针输出接入 RAG 系统的置信度控制模块，实现"低事实性声明自动触发检索验证"的混合管线；
- 利用 clamping 或推理时干预（inference-time intervention）直接修改生成分布，实现幻觉的自动抑制。

## 十一、个人评价与启示

- 这是一篇**"极简方法 + 系统性验证"**的典范论文。作者没有提出复杂的理论框架，而是抓住一个关键经验观察——隐藏状态中编码了事实性信念——用最经济的手段（线性分类器）将其转化为可用的工具，并用大量实验把"简单是否有效"这一问题回答得淋漓尽致。
- 论文最有价值的贡献或许并不在于"检测性能刷新 SOTA"（AUROC 0.76 并不惊艳），而在于证明了在多采样不可行的超大规模模型时代，**单次内部信号仍然能提供足够的事实性监督**。这为后采样时代（post-decoding era）的幻觉治理提供了一个低成本、可扩展的基线。
- 对读者而言，最大的启示是：**不要低估 LLM 内部隐藏状态的信息量**。当外部验证成本高企时，模型自身的置信状态——尤其是经过对齐与博弈训练后的模型——往往隐含着事实性的强先验。学会读取这些内部信号，是塑造可信 AI 的重要一步。
- 当然，探针的工程实现中隐藏了很多"魔鬼细节"：声明分解的 prompt 设计、隐藏状态提取的位置选择、训练集构建中的主观性过滤等。复现者若跳过这些细节，性能很可能大打折扣。因此，该工作也更像一份"事实性探针实践指南"。

## 十二、总结（一句话）

本论文提出了一种**基于隐藏状态线性探针的长文本声明级事实性检测方法**，以单次生成、近乎零边际开销实现了与昂贵多采样方法相当的性能，并通过跨模型、跨架构实验及神经元干预实验，揭示了 LLM 内部存在可迁移的"事实性方向"，为高效幻觉检测提供了新的实用范式。

（完）
