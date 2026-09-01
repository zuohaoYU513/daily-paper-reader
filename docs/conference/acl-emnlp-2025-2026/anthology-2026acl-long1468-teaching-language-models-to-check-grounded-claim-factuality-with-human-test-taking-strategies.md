---
title: Teaching Language Models to Check Grounded Claim Factuality with Human Test-Taking Strategies
title_zh: 教语言模型用人类应试策略核查基于证据的声明事实性
authors: "Yuxuan Ye, Raul Santos-Rodriguez, Edwin Simpson"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1468.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向RAG的grounded声明事实性核查，提升LM输出的事实校验效率
tldr: "Grounded声明事实性核查对检索增强生成等应用至关重要，现有蕴含分类器需要阈值调参，直接提示又未充分利用推理能力。论文将该任务建模为判断题阅读理解，并提示大模型采用显式应试策略进行高效推理。方法相比无引导开放式推理减少80%以上token消耗，同时达到与更昂贵方法相当的表现，为事实性核查提供高效实用方案。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1468/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1577, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1468/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 737, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1468/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 728, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1468/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1640, \"height\": 1015, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1468/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 1081, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1514, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1514, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 728, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 725, \"height\": 181, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 726, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 723, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 724, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 683, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 762, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 765, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 759, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 762, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 486, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 490, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 789, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 787, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 797, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 795, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 776, \"height\": 728, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 789, \"height\": 404, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 793, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1468/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1596, \"height\": 1494, \"label\": \"Table\"}]"
motivation: 基于证据的事实性核查对RAG应用关键，现有方法需阈值调参或提示推理效率低。
method: 将grounded声明事实性核查建模为是非题阅读问答，用人类应试策略引导LLM推理。
result: "该方法减少超过80%的token消耗，同时性能与更昂贵方法相当。"
conclusion: 将事实性核查重构为结构化阅读理解任务，可显著提升大模型核查效率与可用性。
---

## Abstract
Grounded claim factuality checking is important for large language model (LLM) applications such as retrieval-augmented generation, as it helps users assess the correctness of generated outputs. Existing metrics using entailment classifiers require dataset-specific threshold tuning, while LLM-based approaches often use direct prompting, which underutilises the reasoning capabilities of LLMs. We address this by formulating grounded claim factuality checking as a true/false reading comprehension task and prompting LLMs with explicit test-taking strategies for efficient reasoning. Our method reduces token usage by over 80% compared to unguided open-ended reasoning, and achieves competitive performance to more expensive alternatives across two factuality benchmarks, setting a new state of the art on one. To further reduce inference cost, we train small language models (SLMs) to replace LLMs in the checking pipeline. Using supervised fine-tuning (SFT) and a self-revision mechanism, the SLMs learn to improve their factuality judgements. Experimental results show that the resulting SLMs perform on par with strong baselines, combining low inference costs with generating supporting rationales to support interpretability. Code and datasets will be released upon acceptance.

---

## 论文详细总结（自动生成）

## 论文核心信息

- **标题**：Teaching Language Models to Check Grounded Claim Factuality with Human Test-Taking Strategies
- **作者**：Yuxuan Ye, Raul Santos-Rodriguez, Edwin Simpson（布里斯托大学智能系统实验室）
- **会议**：ACL 2026 Long Papers
- **代码**：https://github.com/Haruhi07/Test-Taking

---

## 1. 核心问题与研究动机

- **研究背景**：大型语言模型（LLM）在摘要生成、问答等任务中，常出现生成内容与源文档（grounding document）不一致的"幻觉"问题。基于证据的声明事实性核查（grounded claim factuality checking）对检索增强生成（RAG）等应用至关重要，可帮助用户评估生成输出的正确性。
- **现有方法的不足**：
  - **基于蕴含分类器的指标**（如 SummaC、AlignScore）需要针对数据集调整阈值，泛化能力差，且分块处理源文档会造成信息损失。
  - **直接提示 LLM** 的做法（LLM-as-judge）往往让模型自由推理，未显式引导推理过程，未充分利用 LLM 的推理能力，且推理输出冗长、成本高。
- **核心问题**：如何设计一种*无需阈值调参、泛化能力强、推理高效、可解释*的事实性核查方法？

---

## 2. 方法论

### 2.1 核心思想

将 grounded claim factuality checking 重构为**是非题阅读理解任务**（True/False reading comprehension），并借鉴人类应试策略，以显式准则引导 LLM 分步推理。

### 2.2 LLM 核查流程（两阶段管道）

1. **声明分解（Claim Decomposition）**：将复杂声明分解为多个可独立验证的**原子事实（atomic facts）**，解决证据在文档中稀疏分布的问题。采用少样本提示引导 LLM 完成分解。
2. **原子事实核查（Atomic Fact Checking）**：针对每个原子事实 F 与文档 D，按以下四个准则**依序**核查：
   - **C1**：声明的主语和宾语是否在 D 中出现？
   - **C2**：主语和宾语的描述是否被 D 显式支持？（未被验证的信息留到下一步；若可验证但错误则直接输出 False）
   - **C3**：主语与宾语之间的关系是否被 D 显式支持？
   - **C4**：未验证的信息能否由 D 推断得出？
   
   该策略的核心在于：**先验证显式信息，再处理推断信息**。例如"水可变为水蒸气，反之亦然"，声明"水蒸气可变为冰"需经两跳推理才能验证为 True——这体现了 C3→C4 的递进逻辑。模型需输出"Final Answer: yes/no"及推理过程。

### 2.3 SLM 训练方法（两阶段知识蒸馏）

- **训练数据**：由 LLM（教师模型，Qwen3-30B）生成参考输出，训练 SLM（学生模型，Qwen3-0.6B）。
- **阶段一：SFT（监督微调）**
  - **声明分解学习**：目标函数为 `L(θ) = E[log Pθ({fref} | c)]`，使 SLM 生成的原子事实对齐教师的分解结果。
  - **推理格式对齐**：构造满足/违反各准则的合成数据，SFT 使 SLM 学会按测试策略生成推理过程。
- **阶段二：DPO（直接偏好优化）**
  - 筛选出"SLM 判断错误、LLM 判断正确"的样本，构成偏好对 `(yc = LLM 输出, yr = SLM 输出)`。
  - 目标函数：`L(θ) = -E[log σ(β(sθ(x, yc) − sθ(x, yr)))]`，通过拉开正负样本概率差，抑制 SLM 的错误推理模式，模拟"学生通过纠错提升成绩"的过程。

---

## 3. 实验设计

### 3.1 基准数据集

| Benchmark | 内容 | 规模（测试集） |
|---|---|---|
| **FacTax-Benchmark** | 新闻摘要（PolyTope、SummEval、FRANK、CLIFF、Wang20、Goyal21、Cao22）+ 对话摘要（DiaSummFact） | 1592 条 |
| **LLM-AggreFact** | 摘要（AggreFact-CNN/XSUM、TofuEval、RAGTruth）+ RAG（ClaimVerify、LFQA、ExpertQA）+ 事后验证（REVEAL、FactCheck-GPT）+ 人工撰写声明（WiCE） | 30420 条 |

### 3.2 对比基线

- 蕴含类指标：TrueTeacher（11B）、MiniCheck 系列（0.4B–7B）、FactCG（0.4B）
- LLM 直接提示：ChatGPT-ZS/CoT、FACTAX、Llama-3.3-70B-Instruct、GPT-4o
- 本方法：Qwen3-4B-Instruct / Qwen3-30B-A3B-Instruct（含 Thinking 变体）

### 3.3 评估指标

- **主指标**：平衡准确率（BAcc）
- **分解质量**：ROUGE-L（完整性）+ 句子嵌入余弦相似度（SECS，语义相似度）

---

## 4. 资源与算力

- **文中未明确报告 GPU 型号、数量或训练时长**。仅提及使用了英国 Isambard-AI 国家 AI 研究资源（AIRR）提供的计算资源。
- 教师模型为 Qwen3-30B-A3B-Instruct（MoE 架构，激活参数 3B），学生模型为 Qwen3-0.6B，训练集约 7 万条（分解）和 3.2 万条（核查），训练 3 个 epoch 并早停。据此可推断训练成本较低，但具体算力细节无法从文中获知。

---

## 5. 实验数量与充分性

论文共包含 **10 组主要实验**，覆盖面较全面：

| 实验类型 | 内容 | 结论 |
|---|---|---|
| 主实验 | 两基准 × 多基线 × 多模型 | 30B-Instruct 在 FacTax 达到 SOTA；SLM+DPO 达到 72.6/73.6 |
| 输出长度分析 | Instruct vs Thinking 模式 | Instruct 模式 token 减少 80%–90% |
| 消融：管道组件 | 去除分解/策略/两者 | 每个组件都显著贡献（p<0.05） |
| 消融：准则设计 | 仅 C1–C3 vs 仅 C4 vs 全部 | 显式验证与推断互补 |
| 消融：SLM 训练数据 | 去除某一基准的训练数据 | SLM 泛化受限，训练数据多样性重要 |
| 单遍 vs 两遍 | 合并提示 vs 分步提示 | 两遍准确率更高 |
| 提示改写鲁棒性 | ChatGPT/Gemini 改写提示 | 性能波动很小 |
| 长上下文分析 | 按文档长度分组 | 性能不随长度单调下降 |
| 阈值敏感性 | 固定阈值 0.5 vs 动态调优 | 不影响总体结论 |
| 定性分析 | 案例展示 | 可解释性强，错误案例多为过度严格 |

**充分性评价**：实验数量充足，消融设计逻辑清晰，统计显著性检验（paired bootstrap test）和多种子标准差报告增强了可信度。但 SLM 训练数据仅来自两个基准的 dev 集，对 SLM 泛化能力的评估仍有限。

---

## 6. 主要结论与发现

1. **提示设计显著优于直接提示**：Qwen3-30B-A3B-Instruct 在 FacTax 上平均 BAcc 78.0，超过 GPT-4o（75.3）和 Llama-3.3-70B（74.5），且无需任何训练数据。
2. **效率提升巨大**：Instruct 模式比 Thinking 模式减少 **80%–90%** token 消耗，说明结构化策略比开放式探索更高效。
3. **SLM 训练有效**：0.6B 模型经 SFT+DPO 后达到 72.6（FacTax）/73.6（LLM-AggreFact），超过 ChatGPT-3.5 基线的若干方法，与 11B 的 TrueTeacher 相当。
4. **DPO 的纠错机制显著优于纯 SFT**：SFT→SFT+DPO 在 FacTax 上提升 7.8 个 BAcc 点，证明"从错误中学习"的有效性。
5. **可解释性**：模型生成的推理过程可定位错误声明中的具体部分，并指出支持证据。

---

## 7. 优点

- **创新性强**：首次将人类应试策略引入事实性核查提示设计，将隐式推理转为结构化推理（C1→C4 递进）；首次将 SLM 应用于生成推理式的事实性判断。
- **效率与性能兼得**：token 用量降低 80% 以上，同时达到 SOTA 或接近 SOTA 的性能。
- **零样本泛化**：LLM 管道是零样本方法，无需阈值调参、无需训练数据，直接跨数据集迁移。
- **可解释性**：输出含推理过程的判断，帮助用户识别错误来源并定位证据。
- **鲁棒性验证充分**：提示改写实验表明策略对措辞变化不敏感；长上下文实验表明方法不受文档长度干扰。
- **小模型部署可行**：0.6B 模型性能接近 30B 教师，低成本、可解释，具有实际部署潜力。

---

## 8. 不足与局限

- **SLM 泛化能力有限**：表 8 显示去除某一基准的训练数据后，该基准性能显著下降，说明 SLM 依赖训练数据覆盖度，跨域迁移能力弱于 LLM。
- **复杂文档场景仍有差距**：在 LFQA、TofuEval-MediaS 等需要深度推理的数据集上，SLM 与强基线差距明显，教师模型本身在这些子集上表现也一般。
- **教师模型规模受限**：仅使用 30B 模型作为教师，未尝试 Qwen3 系列的更强模型或多教师集成，蒸馏数据质量仍有提升空间。
- **提示工程敏感性**：虽经改写验证鲁棒，但作者承认进一步提示优化可能带来性能提升，存在对特定模型/数据集过拟合的风险。
- **实验资源细节缺失**：未报告训练时长、GPU 型号与数量，影响可复现性评估。
- **文档长度覆盖有限**：基准文档平均长度仅约 400–560 token，未验证在更长文档（如数万 token）上是否仍有效。
- **过度严格判断倾向**：定性分析显示模型有时因措辞细微差异而过于保守，将可验证事实误判为 False，虽推理过程合理但影响准确性。

---

（完）
