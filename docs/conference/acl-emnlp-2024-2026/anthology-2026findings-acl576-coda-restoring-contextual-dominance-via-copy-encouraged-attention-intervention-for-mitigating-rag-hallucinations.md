---
title: "CoDA: Restoring Contextual Dominance via Copy-Encouraged Attention Intervention for Mitigating RAG Hallucinations"
title_zh: CoDA：通过鼓励复制的注意力干预恢复上下文主导性以缓解RAG幻觉
authors: "JinWei Shi, Qizhuo Xie, Qianzi Hou, Zhipeng Wang, Wanting Su, Jianhua Zhao, Tao Zheng, Tieke He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.576.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 通过鼓励复制的注意力干预恢复对检索证据的关注，缓解RAG幻觉
tldr: 该文发现RAG即使检索证据正确充分仍可能产生幻觉，原因是生成时上下文选择性注意力减弱，模型内部参数知识压过外部证据。作者提出CoDA，通过鼓励复制上下文内容的注意力干预，恢复信息路由中的上下文主导地位。实验结果验证该方法能有效缓解RAG幻觉，为证据约束生成提供了轻量且可解释的干预策略。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1710, \"height\": 981, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1419, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1657, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 769, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl576/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 767, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl576/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl576/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 835, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl576/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl576/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 772, \"height\": 283, \"label\": \"Table\"}]"
motivation: RAG在有充分准确证据的情况下仍会产生幻觉，源于内部参数知识过度主导生成路径。
method: 基于对注意力路由的分析，通过鼓励复制检索上下文的注意力干预来恢复上下文主导性。
result: CoDA在多种RAG任务中显著降低了幻觉发生率。
conclusion: 证明了注意力路由干预能有效改善RAG对证据的依赖并减少幻觉。
---

## Abstract
Retrieval-augmented generation reduces hallucination by grounding model outputs in external evidence, yet hallucinations can still occur even when the retrieved context is accurate and sufficient. From the perspective of information routing in the residual stream, this reflects an imbalance where internal parametric knowledge overwhelms external context during generation. We present an attention-centric analysis of RAG hallucination under valid evidence, showing that hallucinated and factual tokens diverge in mid-to-late Transformer layers as context-selective attention routing weakens, allowing parametric influence to dominate the residual stream. Motivated by prior studies showing that some attention heads—often referred to as copying heads—exhibit stronger information transport capacity, we aim to extend similar evidence-carrying behavior to a broader set of attention heads. To this end, we introduce CoDA, a lightweight inference-time attention intervention that amplifies evidence-aligned value states, enabling more attention heads to transport reliable external evidence in a copy-encouraged manner. Experiments demonstrate that CoDA improves contextual faithfulness, reduces hallucination, and remains robust under long and noisy contexts with modest and stable inference overhead.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义

- **研究动机**：检索增强生成（RAG）通过引入外部证据来缓解大模型幻觉，然而即使检索到的上下文**准确且充分**，模型仍然可能产生与证据相矛盾的输出。这一现象说明幻觉并非单纯源于检索失败，而是与 Transformer 架构如何整合内部参数知识与外部上下文有关。
- **核心问题**：从残差流（residual stream）中信息路由的视角来看，RAG 幻觉的本质是**内部参数知识压倒了外部上下文信号**，导致模型在生成时未能充分“使用”已提供的正确证据。
- **整体含义**：论文提出将幻觉缓解从盲目的检索质量改善或全局参数压制中解放出来，转而从**机制可解释性的角度**定位幻觉形成的具体层，并在推理期进行干预，以恢复上下文在信息路由中的主导地位。这项工作对“证据充分但模型依然臆造”这一实际常见场景给出了可解释、可操作的优化路径。

## 方法论

### 1. 核心思想
- 论文基于机制可解释性研究，观察到部分注意力头（称为“复制头 / copying heads”）具备较强的信息搬运能力，能将外部上下文中的事实性片段直接路由到目标 token。其基本假设是：**复制行为不应是少数专门头独有的能力**，通过合适的干预，可以让更多普通注意力头在证据语义对齐时也表现出复制行为，从而将可靠的外部证据更有效地送入残差流。

### 2. 两阶段框架：定位（Localize）+ 干预（Intervene）

- **阶段一：幻觉易发层的定位**
  - 将每一层对生成 token 的知识贡献分解为两部分：
    - **外部上下文分数（ES）**：计算生成 token 最终层隐藏状态与所关注上下文 token 隐藏状态之间的余弦相似度，衡量注意力层是否有效路由了上下文一致的信息。
    - **参数知识分数（PS）**：通过 LogitLens 将 FFN 前后的残差流状态映射到词表分布，以二者的 Jensen–Shannon 散度衡量 FFN 注入的参数性影响大小。
    - **累计比率（CR）**：按层累计归一化后的 PS 与 ES，刻画参数性知识随深度增加对 token 表征形成的相对主导程度。
  - 基于 CR 计算数据集级别的指标：
    - **激活强度 A**（CR 绝对值的均值）；
    - **分歧强度 Δ**（幻觉 token 与事实 token 在 CR 上的期望差异绝对值）；
    - **幻觉敏感度 H = A × Δ**，取最高分的若干层作为干预目标层集合 R。

- **阶段二：鼓励复制的注意力调制（CoDA）**
  - 仅在已定位到的易发层 l∈R 上执行推理期干预，具体步骤：
    1. 对注意力矩阵按头取平均，得到 token 级的注意力强度，选出 Top-K 个上下文 token 作为“上下文锚点”；
    2. 对每个注意力头，计算每个 token 的 value 向量与锚点 value 向量之间的平均余弦相似度（语义一致性分数 S）；
    3. 对 S 做 min–max 归一化后，通过以 0.5 为中心的 sigmoid 变换得到自适应剂量因子 w（由 α 控制最小权重、τ 控制锐度）；
    4. 将原始注意力权重乘以 w，从而放大与证据一致的 value 状态、抑制不一致的干扰信号。
  - 无需修改模型参数，也无需对 FFN 做显式编辑或缩放，属于轻量、即插即用的推理期干预。

## 实验设计

### 1. 数据集与 Benchmark
- **幻觉基准**：RAGTruth（450 个忠实样本）、Dolly (AC)（100 个忠实样本），用于评估在有效证据下模型产生幻觉的倾向。
- **上下文忠实度基准**：基于 CoFaithfulQA 的六个子集——HotpotQA（1,546）、NewsQA（374）、NQ（3,010）、SearchQA（10,692）、SQuAD（2,799）、TriviaQA（5,887），用于衡量生成内容是否扎根于检索上下文。
- **噪声与长上下文评测（自构建）**：在 CoFaithfulQA 的 NQ / TriviaQA 上，通过向包含 gold evidence 的上下文中注入来自其他实例的不相关段落，控制上下文总长度与噪声比例，评估方法的鲁棒性与性能退化幅度（ΔConR）。

### 2. 对比方法
- 提示类：AttrPrompt、OIPrompt；
- 解码类：COIECD；
- 微调类：SFT、KAFT；
- 对齐类：C-DPO、DDR；
- 机制干预类：ReDeEP、ParamMute；
- 基线：Vanilla-RAG。

### 3. 评估协议
- 主指标为 **Context Recall（ConR，越高越好）** 与 **Memory Recall（MemR，越低越好）**；
- 幻觉缓解对比采用 GPT-4o 对 ReDeEP vs Base、CoDA vs ReDeEP 做两两配对判断（Win/Tie/Loss）；
- 效率方面记录了端到端单样本延迟与相对开销百分比。

## 资源与算力

- 论文正文中**未明确披露**使用的 GPU 型号、GPU 数量、训练时长及总计算量等关键算力信息。
- 从模型规模可推断实验使用了 Llama3-8B、Llama2-13B、Llama2-7B 三类开源模型，并同时运行多项基线和消融比较，所需算力量级应为多卡 A100/H100 级水平，但论文未给出具体数值，这是一个有待补充的信息缺口。

## 实验数量与充分性

论文呈现的实验分组大致包括：

1. **机制定位分析**：层级的激活强度 A 与分歧强度 Δ 指标可视化，以及 CR 轨迹对比，验证了幻觉形成集中在某些中后层。
2. **主实验（上下文忠实度）**：在 CoFaithfulQA 全部六个子集上对比 11 种方法，CoDA 均取得最高 ConR。
3. **幻觉缓解对比**：在三类 Llama 模型上分别针对 RAGTruth 与 Dolly (AC) 做 GPT-4o 配对评估。
4. **稳健性实验**：不同上下文长度与噪声水平下的 ΔConR 对比。
5. **效率分析**：两个数据集 × 三个模型的延迟测试，以及不同 prompt 长度下的延迟变化。
6. **案例评估**：附录 D 提供了 5 个典型人类评估案例并附逐条解读。

**充分性评价**：多数据集、多基线、多 backbone 的设置提高了结论的稳健性，整体实验较为充分。但存在一定不足：缺少对超参数（如 Top-K 锚点数、最小权重 α、调制锐度 τ、干预层数 k）的敏感性消融；所有实验集中于 Llama 家族，未覆盖更多架构；测评主要依赖自动指标与 GPT-4o 评判，实际展示的人工 case 数量有限（仅 5 例）。

## 主要结论与发现

1. **幻觉的机制定位**：事实 token 与幻觉 token 的残差流分歧并非均匀分布，而是在 Transformer 的中后层集中爆发。早期的激活强度高不代表幻觉形成，只有当中后层上下文选择性注意力路由减弱时，参数知识才开始占主导。
2. **干预的有效性**：CoDA 在 CoFaithfulQA 六个子集上均取得最佳 ConR（较 ParamMute 提升 1.5–3.0 个百分点），同时保持较低的 MemR，说明模型对证据的依赖增强并非以滥用参数记忆为代价。
3. **超越基线方法的优势**：在 RAGTruth 和 Dolly (AC) 上，CoDA 对 ReDeEP 的胜率在 RAGTruth 上达到 56%–61%，在 Dolly (AC) 上进一步提升至 60%–70%，优势跨数据集和模型规模保持一致。
4. **鲁棒性**：在长上下文和噪声注入条件下，CoDA 的 ConR 退化幅度（ΔConR）在所有六个子集上均小于 Vanilla-RAG 和 ReDeEP，表明其只关注部分锚点与关键层的设计能自然地抵抗无关信息的干扰。
5. **轻量高效**：推理延迟开销稳定在约 15%–17%（跨模型约 1.0–1.6 秒），且随 prompt 变长相对开销呈下降趋势，具有良好的实际部署前景。

## 优点

- **机制驱动、可解释性强**：从残差流与注意力路由出发建立量化指标，真正做到了先定位病因、再对症下药，而非黑箱式修修补补。
- **即插即用、训练无关**：不需要微调模型，也不需要修改 FFN 或参数知识本身，直接作为推理期插件运行，适用范围广且易于集成到已有 RAG 系统中。
- **与主流思路形成互补**：不同于简单抑制参数激活的做法（如 ParamMute），CoDA 选择了动态放大证据一致信号的路径，既增强了上下文的主导性，又保留了有用的参数知识，实验证明这种平衡确实带来更优的表现。
- **方法设计轻巧**：只算子平均注意力、少量锚点的语义一致性以及 sigmoid 剂量因子，计算量有上限且可控，物理意义明确。

## 不足与局限

- **模型覆盖有限**：实验只涉及 Llama 家族（7B/8B/13B），没有验证 Qwen、Mistral、Gemma 等更广泛的架构。注意力模式、中间层数量以及 FFN 结构的变化可能影响复制头分布和干预效果，跨架构泛化尚不明确。
- **超参数未做细致消融**：Top-K 锚点数、α、τ、干预层集合的大小等关键超参数对方法性能的影响未被系统探索，默认取值的普适性存疑。
- **定位方式存在简化风险**：幻觉的易发层筛选是在数据集级别进行的，个体样本之间可能差异显著，固定干预层集合不一定对每个样本最优。
- **评测的深度有限**：GPT-4o 自动评判存在偏差风险；所展示的人工案例仅 5 个，样本量小且部分案例实际上只是风格上的差异而非实质性的事实改进（论文附录 D 自己也承认了这一点）。
- **尚未覆盖互联网规模的多样场景**：论文只考察了单一事实型问答场景，未讨论多跳推理、多文档对比、对话式 RAG 或需要更新知识等更复杂情况。检索源不完整或误导性较强时，CoDA 仍不能保证正确性。
- **算力信息缺失**：未说明计算环境与资源，不利于研究者复现或评判效率实验的公平性。
- **额外延迟仍不可忽视**：约 15%–17% 的推理开销在高吞吐生产环境中需要权衡，论文也未演示结合并行化/系统优化的变体。

（完）
