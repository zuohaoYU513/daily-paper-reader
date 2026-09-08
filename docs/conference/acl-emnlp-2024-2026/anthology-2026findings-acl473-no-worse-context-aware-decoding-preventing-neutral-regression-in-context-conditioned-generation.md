---
title: "No-Worse Context-Aware Decoding: Preventing Neutral Regression in Context-Conditioned Generation"
title_zh: 无更差上下文感知解码：防止上下文条件生成中的中性回归
authors: "Yufei Tao, Ameeta Agrawal"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.473.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 解码时适配器防止上下文条件生成出现回归，提升基于检索生成的可信度
tldr: 当LLM依赖检索到的外部上下文回答或摘要时，非信息性上下文也可能覆盖原本正确的答案，造成中性回归。该文将中性回归形式化为do-no-harm要求，用正确项准确率下降来量化，并提出NWCAD：在解码期采用双流设置与两级门控，判断上下文是否无信息；若无信息则回退到无上下文解码，不确定时使用对比式回退。实验显示NWCAD能显著减少正确答案被非信息上下文覆盖的情况，为检索增强与证据约束生成提供了解码层面的安全保障。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1533, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1415, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 726, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl473/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 345, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 816, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1669, \"height\": 667, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1176, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 754, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 771, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 768, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 816, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1669, \"height\": 656, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1336, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1618, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1669, \"height\": 657, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1063, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 962, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1183, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1383, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl473/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1278, \"height\": 249, \"label\": \"Table\"}]"
motivation: 非信息性外部上下文可能使LLM覆盖原本正确的输出，损害RAG场景中的事实可靠性。
method: 提出NWCAD解码适配器，基于双流两阶段门控判断上下文是否有信息量，并回退或采用对比解码。
result: 实验表明NWCAD在保留上下文收益的同时显著降低中性回归率。
conclusion: 解码期的do-no-harm机制能有效提升上下文条件生成的可信度，增强对RAG系统的依赖。
---

## Abstract
Large language models (LLMs) can answer questions and summarize documents when conditioned on external contexts (e.g., retrieved evidence), yet context use remains unreliable: models may overwrite an already-correct output (neutral regression) even when the context is non-informative. We formalize neutral regression as a do-no-harm requirement and quantify it by measuring accuracy drops on baseline-correct items under answer-consistent contexts. We propose No-Worse Context-Aware Decoding (NWCAD), a decode-time adapter built on a two-stream setup with a two-stage gate: it backs off to no-context decoding when the context is non-informative, and otherwise uses context-conditioned decoding with a contrastive fallback under uncertainty. We evaluate NWCAD on benchmarks that separate do-no-harm reliability from context utilization (accuracy gains on genuinely helpful contexts). NWCAD prevents neutral regression on baseline-correct items while preserving strong context-driven accuracy on helpful contexts.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：在检索增强生成（RAG）等上下文条件生成场景中，LLM 即使面对**非信息性上下文**（如含糊相关或干扰性的段落），也可能干扰模型原本正确的输出，导致生成答案从正确变为错误。作者将这一失败模式命名为**中性回归（Neutral Regression）**——即模型原本答对，但上下文本身并未提供有用信息，引入上下文反而使答案被覆盖为错误答案。
- **深层含义**：论文强调，传统的上下文感知解码方法（如 CAD、AdaCAD、CoCoA）只关注平均准确率提升，缺乏 **“do-no-harm”（不伤害）保证**——即便模型在无上下文时已经正确，且上下文提供了极弱甚至误导性的信号，这些持续改变分布的方法也可能翻转原本正确的 token 选择，造成级联错误。
- **总体意义**：这项研究首次将中立回归作为一个系统性失败模式进行形式化和量化，并提出了一个"不差于基线"的解码机制，以在**不降低上下文利用能力**的前提下保护原本正确的基线输出，从而为检索增强、证据约束等实际场景提供更可靠、更安全的解码策略。

## 2. 方法论：NWCAD

### 2.1 核心思想

NWCAD 是一个**解码期适配器**，而非全新的对比倾斜规则。它采用**双流（two-stream）设置**（有上下文与无上下文并行前向传播）和**两级门控**，产生三路路由决策：

1. 当检测到上下文无信息时，**精确回退**到无上下文的解码流（保证不伤害基线）；
2. 当上下文流足够确定时，使用**标准有上下文解码**；
3. 仅在不确定时，才调用**对比解码回退**（如 CAD/CoCoA）。

### 2.2 关键技术细节

- **核心信号**：
  - **上下文压力（Context Pressure）**：使用两个分布之间的 Jensen-Shannon 散度（JS），并采用 top-K 并集近似（K=50）降低计算开销。
  - **置信度分数（Confidence）**：使用 top-1 token 的 margin（即最高概率与次高概率之差）。
- **关键阈值**：三个超参数——中性阈值 τ、基线置信度门槛 κpri、上下文置信度门槛 κctx。

### 2.3 决策逻辑

$$
z'_t =
\begin{cases}
z^{ >0}_t, & \text{若 } D_t \le \tau \land (p^{ >0}_{t,1} - p^{ >0}_{t,2}) \ge \kappa_{\text{pri}} \\
z^{c}_t, & \text{若 } (p^{c}_{t,1} - p^{c}_{t,2}) \ge \kappa_{\text{ctx}} \\
z^{\text{fallback}}_t, & \text{否则（CAD 风格回退）}
\end{cases}
$$

- **Stage 1（BC 门）**：当低发散（上下文未实质改变 next-token 分布）且无上下文流高置信时，**精确复制无上下文 logits**——在贪心解码下保证该 token 与无上下文流相同，若每一步都如此，则解码输出与无上下文完全一致。
- **Stage 2（CC 门）**：当 Stage 1 不适用时，若上下文流置信度高（margin ≥ κctx），则用上下文流 logits；否则使用 CAD 风格的对比回退解码器（默认为 CoCoA），该回退解码器可按需替换为 CAD/AdaCAD 等。

## 3. 实验设计

### 3.1 数据集 / 场景

**Part I（受控评估）——Augmented NQ-open**：

- 以 NQ-open 为基础构建三个受控子集：
  - **Restated**：重述正确答案的上下文（基线正确的样本）；
  - **Distractor**：含类型匹配但错误的干扰上下文（如相近年份），且不含正确答案；
  - **Helpful**：模型基线答错但上下文可以纠正答案的样本。
- 每个子集 300 例（共 900 例），仅在基线答对的样本上测 do-no-harm，在基线答错的样本上测 context utilization。

**Part II（全切片评估）**：

- 12 个 QA 基准：NQ-SYNTH、NQ-SWAP、HotpotQA distractor/support、NQ-val-short、PopQA、TabMWP 等；
- Beyond-QA：ToFuEval（对话摘要，AlignScore）、ExpertQA（长形式回答，ROUGE-L/BERTScore-P）。

### 3.2 对比方法

- 基线：无上下文解码（No-context）、标准有上下文解码（With-context）；
- 上下文感知解码方法：CAD、AdaCAD、CoCoA；
- NWCAD 变体：NWCAD BC（仅 Stage 1）、完整两阶段 NWCAD（Stage 1 + Stage 2）。

### 3.3 评估模型

- 三个开源权重模型：Llama-3.1-8B-Instruct、Llama-3.1-70B-Instruct、Ministral-3-8B-Instruct；
- 两个 API 黑盒模型（gpt-5-mini 和 gpt-5.2，仅验证中性回归的存在性，无法运行 NWCAD 或 CAD 方法）。

### 3.4 评估指标

- 精确匹配准确率（EM，SQuAD 标准化）；
- 附加 GPT-4o-mini LLM 语义评价验证是否严格 EM 偏颇；
- ToFuEval 的 AlignScore、ExpertQA 的 ROUGE-L/BERTScore-P。

## 4. 资源与算力

* **论文明确说明的算力信息**：相对解码延迟通过单个 RTX 5090 GPU (FP16, microbatch=1) 测量。
- 论文**未明确报告**总训练时间、GPU 数量或具体算力预算。该方法不进行模型训练（仅推理时解码），因此所需算力主要体现在多次主流比较的推理成本上。

## 5. 实验数量与充分性

- **实验数量**：非常广泛——包括三组受量子集 × 三个模型的受控测试、12 个全切面 QA 数据集、两个超越 QA 的任务、GPT-4o-mini 语义评估、LLM 评估、消融研究、路由统计、延迟测量、敏感性分析（对每个超参数进行 sweep）以及 top-K JS 近似验证。附录包含大量完整表格，实验数量非常充足且严谨。
- **客观性与公平性**：阈值只在 Llama-3.1-8B 上调节，然后**冻结并直接迁移**到其他两种模型和所有基准数据，避免了对每个模型单独调优的偏差风险。此外采用了语义评估（而非仅依赖严格 EM）来确认结论的稳健性。
- **缺点**：所有实验均采用贪心解码，未覆盖温度随机性、束搜索等解码算法。受控子集是自动构建的，无法消除内部验证等构建偏差。

## 6. 主要结论与发现

1. **中性回归确实存在且跨模型普遍**：增加非信息性上下文会导致基线正确答案被覆盖。在五个模型家族中均可观察到类似现象。
2. **NWCAD 最有效**：在受控子集上，NWCAD 在保持中性样本上优秀保护能力的同时，显著提升了 Helpful 子集上的准确率，在受控子集上表现均优于 CAD/AdaCAD/CoCoA。
3. **显式回退比连续倾斜更好**：与持续修改 logits 的对比解码不同，当检测到上下文无信息时**精确复制**无上下文 logits，能在贪心解码下避免 token 层面的无意义翻转。
4. **关键洞察——对比混合很少被需要**：路由统计显示，CAD 风格的回退仅在每次生成中约 1%–2% 的 token 上被调用。大多数步骤本质上是在"无上下文"和"标准有上下文"两种解码之间进行**决策选择（regime selection）**，而不是将两种分布持续混合。
5. **跨领域泛化良好**：在 beyond-QA 任务（ToFuEval 摘要一致性、ExpertQA 长篇回答）上也获得了改善，说明该适配器在短答案 QA 之外的领域依然有效。

## 7. 优点

* **问题形式化清晰**：定义了一个具体可操作的"中性回归"概念，并建立了"do-no-harm" vs. "context utilization"的明确评估框架，区分了"防止回归"和"利用上下文"两个核心维度。
- **方法论简洁且富有理论意义**：轻量级、无训练的解码器适配器，只需修改推理规则即可。
- **具备"不差于"保证**：理论性质清晰——只要 BC 门被选择，贪心解码下能精确恢复无上下文输出，这是连续 logits 倾斜方法无法保证的性质。
- **阈值迁移有效**：在 8B 模型上调参后直接应用于 70B 和其他模型族，仍能保持优势，展现出较好的跨模型迁移性。
- **实验设计周到**：受控子集隔离了中性回归和上下文利用，能准确推断中性回归的方向和数值；全切片 QA + 越域任务综合检验泛化性；GPT-4o-mini 语义评估和消融实验增强了结论的可靠性。
- **模块化设计**：回退解码器可替换，NWCAD 可作为适配器加装在 CAD/AdaCAD/CoCoA 之上且都有改善。

## 8. 不足与局限

* **基于贪心解码的假设**：中性回归的理论保证仅在贪心解码下成立，不适用于采样式解码、束搜索等。实验上的中性回归实验结果也仅基于贪心解码。
- **阈值迁移可能不适用于各种模型域**：默认阈值在 Llama-3.1-8B 上调节后迁移到其他模型。虽然在本实验中效果良好，但对新模型、新领域或新的提示设置不一定最优，且敏感性尚未深入评估（如不同 LLM 系列之间的分布差异）。
- **需要 token 级 logits**：NWCAD 需要有上下文和无上下文两个流的逐 token logits，无法直接适用于不暴露 logits 的黑盒 API 模型或商业系统。
- **可控子集存在构建偏差**：基于 NQ-open 构建的受控子集经过自动筛选，可能无法完整反映真实检索噪声的分布。未来仍需更真实的噪声缓解测试。
- **效率**：双流前向传播增加了计算开销（虽然实际测量中每一轮生成耗时可能低于某些对比解码方法，但相对于 Only-no-context baseline 仍会更高）。且只使用一个 RTX 5090 GPU 进行延迟测量，代表性有限。
- **未考虑长形式输出可靠性**：虽然 beyond-QA 任务略有涉及，但主要针对短答案 QA（最多 32 个 new tokens），未专门讨论长文本生成、多步推理输出时的累积级联风险。

---
（完）
