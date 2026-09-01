---
title: Enhancing Hallucination Detection via Future Context
title_zh: 通过未来上下文增强幻觉检测
authors: "Joosung Lee, Cheonbok Park, Hwiyeol Jo, Jeonghoon Kim, Joonsuk Park, Kang Min Yoo"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.35.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过采样未来上下文增强黑盒模型的幻觉检测能力
tldr: 黑盒大语言模型在生成文本时可能产生幻觉，而用户无法观察生成过程，这给幻觉检测带来挑战。受“幻觉一旦出现往往会持续”的观察启发，本文提出采样未来上下文的方法，将后续生成的文本作为线索提供给现有基于采样的检测器。实验表明，该采样策略能够与多种基线方法无缝集成，并显著提升它们在多个检测任务上的性能，为在黑盒场景下更可靠地识别幻觉提供了简单有效的增强手段。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 559, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1615, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1608, \"height\": 936, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1613, \"height\": 924, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 521, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 521, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1631, \"height\": 1112, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1608, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1610, \"height\": 980, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1594, \"height\": 964, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl35/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1590, \"height\": 960, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1486, \"height\": 816, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1501, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1479, \"height\": 808, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1314, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1325, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1651, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1316, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1323, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 583, \"height\": 133, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 503, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1486, \"height\": 817, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl35/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1238, \"height\": 918, \"label\": \"Table\"}]"
motivation: 黑盒生成器产生的幻觉难以检测，且幻觉具有持续性，需要利用未来上下文线索。
method: 采样未来上下文并与多种基于采样的检测器集成，提供额外线索来提升检测性能。
result: 在多个方法和数据集上验证了该采样策略能一致地改善幻觉检测效果。
conclusion: 为黑盒LLM幻觉检测提供了一种通用、轻量的增强手段，可广泛应用于在线内容检测。
---

## Abstract
Large Language Models (LLMs) are widely used to generate plausible text on online platforms, without revealing the generation process.As users increasingly encounter such black-box outputs, detecting hallucinations has become a critical challenge.To address this challenge, we focus on developing a hallucination detection framework for black-box generators.Motivated by the observation that hallucinations, once introduced, tend to persist, we sample future contexts.The sampled future contexts provide valuable clues for hallucination detection and can be effectively integrated with various sampling-based methods.We extensively demonstrate performance improvements across multiple methods using our proposed sampling approach.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）被广泛用于在线平台生成流畅、看似合理的文本，但用户无法观察模型的生成过程（黑盒场景），这使得检测模型输出中的幻觉（hallucination）成为一项关键挑战。
- **现有方法的不足**：
  - 基于不确定性的方法依赖生成器内部的 token 级 logits，但在真实场景（如博客、API 已更新或下线）中通常不可用；
  - 基于检索的方法在需要内部文档或专有知识库时受限，且难以检测逻辑幻觉和内部矛盾（论文引用 Mündler et al. 报告，ChatGPT 产生的自相矛盾幻觉中有 35.2% 无法通过检索验证发现）。
- **核心观察（论文的核心动机）**：幻觉一旦引入往往会持续存在（"snowball effect"）。论文通过 SelfCheckGPT 数据集上的统计验证：当当前句子是幻觉时，后续句子为幻觉的概率显著更高，且错误会逐步向后传播。
- **研究目标**：在完全黑盒、无检索的条件下，利用**采样未来上下文（future context）**作为额外线索，增强采样类幻觉检测方法的性能。

## 2. 方法论

### 2.1 核心思想

论文提出一种通用的增强框架：给定待检测的目标句子，让一个指令微调的 LLM（检测器）采样该句可能接续的未来句子，将这些未来上下文与目标句子一起提供给检测器，帮助其判断目标句子是否为幻觉。

### 2.2 未来上下文采样（Future Context Sampling）

- 使用指令微调 LLM 作为未来上下文采样器，提示其生成目标句子的“下一个句子”。
- 当需要生成更远的未来（超过一句）时，采用**多句同时生成**的方式（而非逐句顺序生成），每个采样路径生成的一组句子定义为一个未来上下文（future context）。

### 2.3 与现有采样方法的集成

论文采用统一而简单的策略：**将未来上下文直接附加到原检测 prompt 末尾**，应用于三类方法：

1. **DIRECT（论文提出的新基线）**：显式向检测器提出二元问题（"该句子关于概念是否准确？答 Yes/No"），仅依赖检测器内部知识和推理能力判断幻觉；
2. **SelfCheckGPT +f**：在原有的多组采样替代上下文-响应对中追加未来上下文，扩大 LLM 可用于一致性判断的证据；
3. **SC（自相矛盾检测）+f**：在 SC 的两阶段流程（解释生成→矛盾判定）中，用未来上下文替代原有描述字段。

### 2.4 幻觉评分

- 目标句子与每个采样的线索（clue）配对进行逐一判断：判断为幻觉得 0 分，非幻觉得 1 分，无法判断（N/A）得 0.5 分；
- 将所有配对的得分取平均，得到该句子的幻觉分数。

### 2.5 未来上下文的扩展方式

- **每轮样本数（s）**：增加每个未来位置采样的句子数；
- **前瞻步数（t）**：增加向未来探索的轮数；
- **过滤机制**：探索了基于 prompt 的隐式过滤和基于 NLI 模型的显式过滤，只保留与当前句子语义相关的未来上下文。

## 3. 实验设计

### 3.1 数据集与 Benchmark

论文标准化了多个现有数据集以支持统一评测，共 6 个数据集：

| 数据集 | 幻觉类型 | 规模（幻觉/非幻觉） |
|---|---|---|
| SelfCheckGPT | 逻辑幻觉（模型生成上下文） | 1392 / 516 |
| SC-ChatGPT | 自相矛盾幻觉 | 491 / 2935 |
| SC-GPT4 | 自相矛盾幻觉 | 207 / 1527 |
| SC-LLaMA | 自相矛盾幻觉 | 236 / 1532 |
| SC-Vicuna | 自相矛盾幻觉 | 185 / 878 |
| True-False | 事实性幻觉 | 1972 / 2125 |

### 3.2 检测器 LLM

使用了三种指令微调模型作为检测器：
- LLaMA 3.1-8B
- Gemma 3-12B
- Qwen 2.5-7B

### 3.3 对比方法

- **DIRECT**（论文提出的直接判断基线）+f 变体
- **SelfCheckGPT** +f 变体
- **SC（Self-Contradiction Detection）** +f 变体

### 3.4 评估指标

- 主指标：AUROC（数据集没有显著不平衡）
- 辅助指标：AUCPR（附录表 11）

### 3.5 补充实验场景

- 采样成本与 token 效率分析（不同 w/s 组合）
- 未来句质量分析（幻觉/非幻觉未来句对检测的贡献）
- prompt 过滤与 NLI 过滤的未来上下文选择
- 检索增强方法（VeriScore +f）
- 段落级幻觉检测
- 未来上下文来源对比（生成器 vs. 检测器）

## 4. 资源与算力

- **论文未明确说明**所使用的 GPU 型号、数量、训练总时长或具体算力消耗。
- 仅在附录中报告了各检测器的**采样 token 数**（如表 6），用于说明不同方法的推理成本差异，但没有给出端到端的时间或硬件信息。

## 5. 实验数量与充分性

### 实验数量

论文进行了**非常大量且全面的实验**，主要包括：
- **主实验**（表 1）：3 个检测器 × 6 个数据集 × 6 个方法变体，共 108 个 AUROC 数值，并附 AUCPR 结果（表 11）；
- **多个消融/分析实验**：
  - 增加采样未来句数量对 SelfCheckGPT 和 SC 的影响（图 3、图 11、图 12）；
  - DIRECT +f 中采样数与 lookahead 轮数的独立影响（图 7）；
  - 采样数与 lookahead 的联合影响（图 8、图 13）；
  - 未来上下文的过滤实验（表 2）；
  - 未来句质量统计（图 5、图 6、表 7、表 8）；
  - 与单纯增加响应采样数的对比（图 10）；
  - 未来上下文来源（生成器 vs. 检测器）对比（图 9）；
  - 段落级检测（表 10）和检索增强场景（表 9）；
  - 未来上下文拼接聚合分析（图 14）。

### 充分性与公平性评价

- **优点**：实验覆盖了多数据集、多检测器、多方法，且从多个角度（样本数、lookahead、质量、成本、过滤）对方法进行了深入剖析，整体上非常充分。
- **公平性考虑**：论文统一了数据集格式，避免了以往因生成器、检测器、格式差异导致的不可比问题；在过滤实验中采用了固定阈值以避免调参偏差；未来句采样设置跨检测器保持一致。
- **潜在偏倚**：SelfCheckGPT 数据集中使用模型生成的文本作为上下文，且句子由同一生成器连续生成，存在标签噪声；SC 数据集中将自相矛盾情况下初始响应直接视为幻觉，定义上存在一定的近似。

## 6. 主要结论与发现

1. **未来上下文一致提升检测性能**：在大多数配置下，将采样未来上下文融入 DIRECT、SelfCheckGPT 和 SC，均带来 AUROC 的提升（表 1）。SelfCheckGPT+f 平均提升约 1.3 分，SC+f 平均提升约 5.1 分，提升幅度显著。
2. **增加采样数 s 有效**：随着每个未来位置采样句子数的增加，各方法性能持续上升（图 3、图 11、图 12）。
3. **增加 lookahead 轮数 t 有效**：更远的未来上下文提供更强的雪球效应信号，提升效果有时优于增加采样数（图 7、表 5）。
4. **未来上下文具有成本优势**：将 SelfCheckGPT 的对照采样数 w 减少、增加未来句采样 s，可以在更低 token 消耗下达到相当或更优性能（图 4）；将未来上下文与 SelfCheckGPT 结合可**有效降低采样成本**。
5. **未来句的状态与当前句统计相关**：幻觉当前句子后更容易出现幻觉未来句，非幻觉当前句子后更容易出现非幻觉未来句；与当前句状态匹配的未来句对检测最有帮助（图 5、图 6）。
6. **选择性过滤可进一步提升性能**：prompt 式过滤取得了优于无过滤的检测结果，NLI 过滤也有提升空间（表 2）。

## 7. 优点

- **完全黑盒、生成器无关**：不依赖生成器的 logits、注意力或内部状态，只使用检测器自身的生成能力，适用范围广。
- **方法即插即用、可扩展性强**：通过简单的 prompt 拼接即可与多种现有采样方法集成，无需改动原有框架。
- **统一的 benchmark**：标准化了 6 个数据集并公开重构版本，解决了以往评测标准不一致的问题，促进后续可比研究。
- **分析视角丰富深入**：不仅报告主结果，还从雪球效应、未来句质量、采样成本、过滤策略、聚合方式等角度进行了多维度分析，为理解未来上下文的作用机理提供了充分证据。
- **采样可控性强**：通过调节采样数 s 和前瞻轮数 t，可为不同应用场景（实时性 vs. 高精度）提供灵活配置。

## 8. 不足与局限

- **未来句质量不稳定的问题**：某些检测器（尤其是 Qwen 2.5）生成的未来句存在低质量问题，如生成不足或重复输出（例如反复输出 "Sure!"），限制了长前瞻轮数的效果（图 9、表 7、表 8）。
- **相关性不构成因果**：论文承认未来句与当前句幻觉状态之间的关联是统计相关而非因果，尽管可用作预测信号，但其可靠性依赖数据分布。
- **检索增强实验覆盖有限**：未来上下文对检索方法（VeriScore）的探索仅在 True-False 单数据集、GPT-4o 单检测器上进行，结论的泛化性需要更多验证。
- **提示工程的一致性约束**：为保持跨检测器的公平，论文没有针对各模型进行 prompt 调优，这可能在部分模型中低估了方法上限；高质量的 prompt 设计可能会带来更大收益。
- **过滤阈值固定**：NLI 过滤采用固定阈值，没有针对不同模型/数据集调优，性能仍有提升空间。
- **对未来上下文质量的依赖**：当采样到的未来句大多与当前句无关或质量低下时，方法增益会减弱甚至失效。
- **未报告资源消耗细节**：未明确指出 GPU 型号、训练/推理的算力总开销，不利于读者评估实际部署成本。

---

（完）
