---
title: "SeaKR: Self-aware Knowledge Retrieval for Adaptive Retrieval Augmented Generation"
title_zh: SeaKR：面向自适应检索增强生成的自我感知知识检索
authors: "Zijun Yao, Weijian Qi, Liangming Pan, Shulin Cao, Linmei Hu, Liu Weichuan, Lei Hou, Juanzi Li"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1312.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用自我感知不确定性的自适应RAG以减少幻觉
tldr: 自适应检索增强生成（RAG）通过动态判断是否需要外部知识来缓解大语言模型幻觉。本文提出 SeaKR，从模型内部状态提取“自我感知不确定性”，并在不确定性高时自动触发检索；同时基于不确定性降低程度对检索片段重新排序，以最大化知识使用效率。对于需要多轮检索的复杂任务，SeaKR 也能自适应地进行多次检索。实验表明，该方法能更精准地调用外部知识，显著减少幻觉并提升生成质量，为自适应 RAG 提供了一种基于模型自身不确定性信号的新范式。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1312/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1312/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1613, \"height\": 745, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1312/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 789, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 785, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1640, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1261, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 622, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1566, \"height\": 1873, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1638, \"height\": 2425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1312/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1634, \"height\": 2211, \"label\": \"Table\"}]"
motivation: 现有自适应RAG难以准确判断何时需要外部知识，且片段整合效果有限。
method: SeaKR 从LLM内部状态提取自我感知不确定性，据此动态检索并按不确定性降低程度重排片段。
result: 在多个知识密集型任务上减少了幻觉，提升了生成准确性。
conclusion: 为自适应RAG提供了基于内部不确定性信号的检索决策与排序机制。
---

## Abstract
Adaptive Retrieval-Augmented Generation (RAG) is an effective strategy to alleviate hallucination of large language models (LLMs). It dynamically determines whether LLMs need external knowledge for generation and invokes retrieval accordingly. This paper introduces Self-aware Knowledge Retrieval (SeaKR), a novel adaptive RAG model that extracts self-aware uncertainty of LLMs from their internal states. SeaKR activates retrieval when the LLMs present high self-aware uncertainty for generation. To effectively integrate retrieved knowledge snippets, SeaKR re-ranks them based on LLM’s self-aware uncertainty to preserve the snippet that reduces their uncertainty to the utmost. To facilitate solving complex tasks that require multiple retrievals, SeaKR utilizes their self-aware uncertainty to choose among different reasoning strategies. Our experiments on both complex and simple Question Answering datasets show that SeaKR outperforms existing adaptive RAG methods.

---

## 论文详细总结（自动生成）

# 《SeaKR: Self-aware Knowledge Retrieval for Adaptive Retrieval Augmented Generation》论文总结

## 1. 核心问题与整体含义（研究动机）

- **背景问题**：大语言模型（LLM）常产生幻觉，主要原因之一在于查询超出了模型参数化知识的边界。检索增强生成（RAG）通过引入外部知识缓解该问题，但传统 RAG 对所有输入一律检索，导致效率低下，且噪声/冲突知识反而可能干扰模型本可正确作答的情形。
- **自适应 RAG 的挑战**：已有自适应方法（如 FLARE、DRAGIN、Self-RAG）主要基于模型输出层信号（token 概率、模型自我声明等）判断是否检索，但 LLM 存在自我偏差，可能“自信地输出错误内容”，因此输出级信号不能可靠反映真实知识充足性。
- **核心研究问题**：如何更准确地判断 LLM“何时需要外部知识”，以及“如何有效整合检索到的知识”，从而减少幻觉、提升生成质量。
- **论文含义**：提出 SeaKR，首次从 LLM **内部状态**（而非输出）中提取“自我感知不确定性”，并基于该信号驱动自适应的检索决策、知识重排与推理策略选择，为自适应 RAG 提供了新范式。

## 2. 方法论（SeaKR）

### 2.1 总体框架
- 三个核心组件：搜索引擎 `S(·)`、大语言模型 `LLM(·)`、自我感知不确定性估计器 `U(·)`。
- 采用 Chain-of-Thought（CoT）迭代推理：维护知识缓冲区 `K` 和推理缓冲区 `R`，每轮生成一个 rationale，动态决定是否检索。

### 2.2 自我感知不确定性估计器
- 对输入上下文 `c`，采样 `k` 个生成结果，提取每个结果中 `<EOS>` token 的隐藏表示 `H^{(l)}_{<EOS>}`。
- 计算这些表示的 Gram 矩阵的行列式（正则化），作为自我感知不确定性分数 `U(c)`。
- **原理**：Gram 行列式刻画一组表示的内部一致性；LLM 在生成错误内容时内部状态一致性更低，因此不确定性更高；相比输出层，内部状态规避了同义异形等自然语言噪声。

### 2.3 自我感知检索（何时检索）
- 构造输入上下文 `c_r`（包含问题、历史 rationales 和 ICL 示例），先进行一次“伪生成”（pseudo-generation）。
- 若 `U(c_r) > δ`（阈值），则触发检索；否则直接生成 rationale，不引入外部知识。
- 查询生成：从伪生成结果中剔除低概率 token 形成搜索引擎查询，使检索结果能填补不确定的信息缺口。

### 2.4 自我感知重排（如何整合）
- 搜索引擎返回 top-N 知识片段，对每个片段构造上下文并计算 `U(·)`。
- 选择使模型**不确定性降低最多**的知识片段（即 `U` 最小的片段）作为增强上下文，而非依赖搜索引擎的相关性排序，从而过滤与模型内部知识冲突或无关的噪声片段。

### 2.5 自我感知推理（复杂任务多轮整合）
- 迭代终止条件：出现“So the final answer is”或达到最大检索次数。
- 两种候选推理策略：
  1. **基于 rationale**：直接在最后生成的 rationale 后生成最终答案；
  2. **基于知识**：将全部已选知识片段拼接，作为上下文进行完整 CoT 推理。
- 最终选择不确定性分数更低的那条答案路径，相当于在策略层面进行自适应集成。

## 3. 实验设计

### 3.1 数据集
- **复杂 QA（多跳推理）**：2WikiMultiHopQA、HotpotQA、IIRC（answerable 子集）。
- **简单 QA（开放域问答）**：NaturalQuestions、TriviaQA、SQuAD。
- 评估指标：Exact Match（EM）和 F1。

### 3.2 基线方法
- **非自适应**：CoT、IRCoT。
- **自适应**：Self-RAG（微调）、FLARE（低概率触发）、DRAGIN（注意力权重触发）。
- 变量控制：所有方法共用 BM25 + Elasticsearch 检索器、同一版 Wikipedia（2018-12-20）外部知识源；简单 QA 限制检索次数为 1。

### 3.3 实现细节
- 主骨干：LLaMA-2-chat（7B）；另测试 LLaMA-3（8B）等。
- 超参数：知识返回数 N=3，伪生成采样 k=20，不确定性阈值 δ 在 NQ 训练集上搜索；使用 10 个 ICL 示例；内部状态取中间层（l = L/2）。

### 3.4 主要结果
- **复杂 QA**：SeaKR 在 2Wiki、HotpotQA、IIRC 上 F1 分别为 36.0%、39.7%、23.5%，超过最佳基线 6.0%、5.5%、0.6%；显著优于 FLARE、DRAGIN 和微调的 Self-RAG。
- **简单 QA**：SeaKR 在 TriviaQA（F1 63.1%）和 SQuAD（F1 36.5%）上最优；在 NQ 上与 FLARE 相当，但低于在 NQ 风格数据上微调过的 Self-RAG。

## 4. 资源与算力

- 论文明确说明：全部实验可在一张 **NVIDIA 3090 GPU（24GiB 显存）** 上完成。
- 通过修改 **vLLM** 实现 20 次伪生成的并行批处理，使 20 次伪生成的延迟与单次接近。
- 效率实验（4×Geforce 3090）：SeaKR 平均处理单题耗时（2Wiki 4.94s、HotpotQA 7.30s）显著低于 FLARE（8.44s/13.25s）和 DRAGIN（29.75s/19.25s）。
- 由于 SeaKR 是 **tuning-free** 方法，无需模型训练，论文未涉及训练时长；仅少量超参数搜索（NQ 训练集约 3000 样本）。

## 5. 实验数量与充分性

- **主要对比**：复杂 QA（3 数据集）+ 简单 QA（3 数据集），共 6 个基准。
- **消融实验**（表 3）覆盖：
  - 不确定性估计器替代方案：Prompting、Perplexity、Multi-Perplexity、LN-Entropy、Energy score；
  - 移除自我感知检索（每步强制检索）；
  - 移除自我感知重排（直接用搜索引擎第一结果）；
  - 移除自我感知推理（仅 rationale / 仅知识两种固定策略）。
- **骨干模型扩展**：LLaMA-2 base/chat 7B、LLaMA-3 base/instruct 8B、LLaMA-3.1-Instruct 8B，验证可扩展性。
- **超参数搜索**：对 N、k、δ 进行了网格搜索分析（图 3）。
- **案例分析**：检索触发、重排效果、推理策略选择三类案例（正文 + 附录）。
- **充分性评价**：整体实验设计较充分，消融覆盖了各核心模块；变量控制较好（统一检索器、知识源、ICL 示例）。但所有任务均为短格式 QA，未覆盖长文本生成、创造性写作等场景，因此结论的泛化范围有限。

## 6. 主要结论与发现

- SeaKR 在复杂和简单 QA 上均优于现有自适应 RAG 方法，尤其在多跳复杂问答中提升显著。
- 内部状态层面的自我感知不确定性比输出层面信号（token 概率、模型自述）更可靠地反映知识充足性。
- 消融显示：**知识整合策略（重排+推理）带来的性能提升甚至超过自我感知检索本身**，说明“如何整合”与“何时检索”同等重要，甚至更关键。
- 自适应检索避免噪声知识误导模型，验证了动态判断检索时机的必要性。
- SeaKR 无需微调、泛化性好，优于在简单 QA 上微调过的 Self-RAG 在复杂 QA 上的表现。
- 更强的骨干模型（LLaMA-3 系列）带来一致性能提升，说明方法可随模型能力正向扩展。

## 7. 优点与亮点

- **方法创新**：首次将内部状态不确定性（Gram 行列式）系统性地用于自适应 RAG 的检索决策与知识整合，而非仅停留在输出概率或提示模型自评。
- **同时解决两个关键问题**：不仅回答“何时检索”，还设计了“如何整合”的自适应机制（重排 + 推理策略选择），且证明后者贡献更大。
- **免训练、通用性强**：无需微调，容易迁移到不同 LLM 和任务。
- **检索去噪能力强**：自我感知重排能选择“对模型不确定性降低最大”的知识，缓解检索片段与模型内部知识冲突的问题。
- **推理策略自适应集成**：在 rationale 路径和知识路径之间按不确定性做集成，类似模型级 ensemble，提升鲁棒性。
- **工程效率意识**：vLLM 并行化使 20 次伪生成开销可接受，实际推理速度甚至快于 FLARE/DRAGIN。
- **消融和分析详尽**：对不确定性估计器、检索、重排、推理四个模块均做了替代/移除验证，并附有案例和效率数据。

## 8. 不足与局限

- **依赖内部状态**：方法要求可访问模型隐藏层，因此不适用于 GPT 系列等闭源商业模型，适用范围受限。
- **任务覆盖窄**：仅在短格式 QA 上评估，未涉及长格式问答、代码生成、创造性写作等多类 NLP 任务。
- **计算开销**：虽经 vLLM 加速，但每步需 20 次伪生成，整体 LLM 调用次数较多（复杂 QA 约 10 次/题），资源消耗仍高于简单触发式方法。
- **模型规模有限**：最大仅验证到 8B 参数模型，未在更大规模（如 70B+）上实验，扩展性结论尚不完整。
- **特定数据集上的劣势**：在 NQ 上低于经过同分布数据微调的 Self-RAG，说明免训练方法在面对领域内微调方法时仍有差距；对 IIRC 等强数值推理任务提升有限。
- **潜在滥用风险**：自我感知不确定性可作为对抗训练信号，用于生成更具欺骗性的内容；LLM+IR 结合也可能被用于自动化网络人肉搜索等，论文对此有伦理讨论但无具体防护方案。
- **对检索技术的依赖**：自我感知重排的效果可能被未来更先进的 IR 排序模型部分超越，方法的长期优势存在不确定性。

（完）
