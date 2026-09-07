---
title: Familiarity-Aware Evidence Compression for Retrieval-Augmented Generation
title_zh: 面向检索增强生成的熟悉度感知证据压缩
authors: "Dongwon Jung, Qin Liu, Tenghao Huang, Ben Zhou, Muhao Chen"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.878.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 压缩检索证据并增强目标模型对证据的熟悉度，促进生成时依赖所给证据
tldr: 检索增强生成经常因检索到的冗余或不一致证据而干扰目标语言模型。FaviComp提出免训练的熟悉度感知证据压缩技术，使压缩后的证据更贴合目标模型的语言习惯，以提升证据利用率。实验表明该方法能减少无关证据的干扰，帮助模型更可靠地依据外部证据生成内容，降低幻觉风险。该工作强调了面向目标模型的证据熟悉度在RAG证据利用中的重要作用。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1578, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 799, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp878/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1167, \"height\": 322, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1543, \"height\": 1285, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 844, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1435, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 819, \"height\": 137, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1384, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1403, \"height\": 1269, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1587, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1539, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp878/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1581, \"height\": 2165, \"label\": \"Table\"}]"
motivation: 检索增强生成中压缩后的证据仍可能与目标模型不熟悉，导致模型不能有效利用证据并易受无关信息干扰。
method: 提出FaviComp免训练证据压缩技术，基于目标模型对证据的熟悉度调整压缩策略，使证据更易被下游模型采纳。
result: 实验显示FaviComp能降低无关证据的干扰，改善多证据场景下模型利用证据的效果和生成质量。
conclusion: 将证据压缩与目标模型熟悉度匹配是提升RAG证据利用率和生成可信度的有效途径。
---

## Abstract
Retrieval-augmented generation (RAG) improves large language models (LMs) by incorporating non-parametric knowledge through evidence retrieved from external sources. However, it often struggles to cope with inconsistent and irrelevant information that can distract the LM from its tasks, especially when multiple evidence pieces are required. While compressing the retrieved evidence with a compression model aims to address this issue, the compressed evidence may still be unfamiliar to the target model used for downstream tasks, potentially failing to utilize the evidence effectively. We propose FaviComp (Familarity-Aware Evidence Compression), a novel training-free evidence compression technique that makes retrieved evidence more familiar to the target model, while seamlessly integrating parametric knowledge from the model. Experimental results show that FaviComp consistently outperforms the most recent evidence compression baselines across multiple open-domain QA datasets, improving accuracy by up to 28.1% while achieving high compression rates. Additionally, we demonstrate the effective integration of both parametric and non-parametric knowledge during evidence compression.

---

## 论文详细总结（自动生成）

好的，我将根据您提供的论文内容，按照指定的要点结构，生成一份详细的中文总结。

---

### 论文总结：面向检索增强生成的熟悉度感知证据压缩

#### 1. 核心问题与整体含义

- **研究动机**：检索增强生成（RAG）通过引入外部非参数知识来提升大语言模型（LM）在知识密集型任务（如开放域问答）中的表现。然而，当需要整合多个外部证据（尤其是多跳、复杂推理任务）时，噪声和无关信息往往会干扰模型。现有的证据压缩方法虽旨在解决此问题，但压缩模型生成的内容可能由于内部知识与提示偏好差异，导致目标模型对其不“熟悉”，从而无法有效利用。
- **核心问题**：如何让压缩后的证据不仅在内容上相关，还能在表达方式上对任务所用的目标模型更“友好”？
- **整体含义**：论文提出FaviComp，这是一种免训练（training-free）的推理时证据压缩技术。其核心思想是在压缩过程中主动降低目标模型对压缩结果的困惑度（Perplexity），同时无缝融合目标模型自身的参数化知识。通过这种方法，模型能更好地平衡内部知识与外部证据，减少无关信息的干扰，提升RAG在复杂场景下的准确性和可靠性。

#### 2. 方法论

- **核心思想**：结合先前“模型对低困惑度提示更熟悉”的研究发现，FaviComp在证据压缩阶段引入**集成解码**（Ensemble Decoding）机制，将压缩模型与目标模型的概率分布结合，主动将压缩过程推向目标模型更熟悉的文本区域。
- **技术细节与算法流程**：
  - **背景**：在标准RAG证据压缩中，输入是检索到的文档集 $\{d_1, ..., d_k\}$ 和问题 $x$，压缩模型 $P_{comp}$ 生成一个精简摘要 $c$，随后目标模型 $P_{tar}$ 基于该摘要生成答案。
  - **双模型并行生成**：FaviComp在生成每个token时，同时运行两个独立的生成任务：
    1. **证据压缩**：压缩模型根据原始检索文档进行摘要生成。
    2. **上下文生成**：目标模型仅基于问题 $x$（及指令）生成内部知识驱动的“上下文”（Context Generation）。
  - **集成解码（关键步骤）**：在每一步解码时，FaviComp通过加权求和两个模型的概率分布来选择下一个token：
    ```
    ci = arg max (α · log P_tar(c'_i) + (1 − α) · log P_comp(c''_i))
    ```
    其中，$α$ 是控制两模型权重的集成系数。
- **效果**：
  - 该方法能压缩目标模型的token搜索空间，偏向选择低困惑度的token，使压缩文本更易被目标模型理解。
  - 它允许模型在压缩模型不确定（如缺失关键信息）时，利用目标模型的参数化知识补全证据，实现知识和上下文的无缝整合。

#### 3. 实验设计

- **数据集 (Benchmark)**：使用5个开放域QA数据集，分为两类：
  - **单文档QA**：Natural Questions (NQ)、TriviaQA (TQA)。
  - **多文档QA**：HotpotQA (HQA)、2WikiMultiHopQA (Wiki)、MuSiQue (MQ)。
- **基线方法**：与多种类别的方法对比：
  - **无上下文** (No Context)
  - **黄金压缩** (Gold Compression)：假设检索到黄金文档的性能上界。
  - **原始文档** (Raw Document)
  - **生成式上下文** (Generated Context)：仅用目标模型生成。
  - **重排序方法**：Sentence-BERT、RECOMP-extractive。
  - **压缩方法**：LongLLMLingua、RECOMP-abstractive、CompAct、Zero-shot Summarization。

#### 4. 资源与算力

- 论文中**未明确说明**训练所需的GPU型号、数量和训练时长。但论文属于免训练方法，因此主要算力成本为模型推理。
- 在附录B.2中，为了公平对比，训练了一个RECOMP-abstractive的Mistral-7B-Instruct模型，并提及使用了**LoRA**微调，学习率为**2e-6**，batch size为**64**，训练**7个epochs**，但未提及具体使用的GPU硬件信息。
- 论文在附录B.4中列出了主要方法的**推理延迟**：FaviComp的平均延迟为6.43秒/样本，远低于有监督最优模型CompAct的8.72秒/样本，高于Zero-shot Summarization的3.99秒/样本。

#### 5. 实验数量与充分性

论文进行了充分的实验，以验证方法的有效性与鲁棒性：
- **主实验**：在5个QA数据集上，使用两种主目标模型（Llama3-8B-Instruct、Mixtral-8x7B-Instruct），对比了所有基线。FaviComp在所有数据集和指标（Acc, F1）上均全面优于所有对比的压缩/重排序方法（除黄金上界外）。
- **消融实验**：探讨了集成系数α（0~1之间）对性能与困惑度的影响，验证了α=0.5为最优。
- **机制分析**：
  - **知识整合分析**：将数据分为“证据命中”（Hits=1）和“证据未命中”（Hits=0）两组，验证了FaviComp在证据无关时能更依赖参数化知识，在证据相关时能有效利用外部知识。
  - **消融对比实验**：与简单的拼接方法对比，证明了集成解码整合知识优于直接拼接。
- **性能分析**：评估了FaviComp与各压缩方法的压缩率。
- **案例研究**：通过两个具体QA例子展示了FaviComp的优越性。
- **其他补充实验**：在附录中，实验还验证了其他模型组合下的性能，并通过公平对比（相同底座模型）证明优于有监督的RECOMP-abstractive。此外还进行了延迟分析。

**公平性与客观性**：实验覆盖了不同模型规模、不同知识密集型任务、并对计算开销（延迟）进行了量化，对比基线包含提取式、抽象式、监督与非监督方法，分析较为全面、客观。

#### 6. 主要结论与发现

- **结论**：FaviComp作为一种免训练、推理时的证据压缩方法，能有效提升RAG性能。它通过将压缩证据的风格与目标模型对齐（降低困惑度），并巧妙整合目标模型的内部参数化知识与外部检索证据，显著提升了模型在多证据、复杂问答任务上的表现。
- **优势对比**：与有监督的压缩基线（如CompAct）相比，FaviComp在无需额外训练的情况下达到了全面最优的性能，说明“让压缩模型去适应目标模型的偏好”比“用大模型蒸馏小模型”的范式更具普适性。
- **性能记录**：在最具挑战性的多文档QA数据集MuSiQue (MQ) 上，FaviComp甚至超越了拥有黄金文档的Gold Compression，有力证明了参数化知识能补充不完美的外部检索证据，弥补信息缺失。

#### 7. 优点

- **免训练与即插即用**：不需要像CompAct、RECOMP等方法训练专用压缩器，可直接应用于任何RAG流程，成本更低、灵活性更高。
- **显著的性能提升与高压缩比**：在所有数据集上稳定超越先前的SOTA方法，同时保持了较高的压缩率。
- **缓解知识冲突问题**：通过创新的集成解码，不依赖显式的因果干预或数据变换，自然解决了RAG中参数化知识与非参数化知识冲突的问题。
- **模块化与强兼容性**：虽然是针对LLM设计的，但其核心思想（集成解码降低困惑度）具备较强的通用性，可推广至其他需要生成给特定模型消费的文本的任务中（如提示工程、摘要生成）。

#### 8. 不足与局限

- **算力开销**（明确提及）：FaviComp在压缩时需要同时运行压缩模型和目标模型，计算开销约为单模型推理的两倍，引入了一定的额外延迟，论文指出这是性能与速度间需要权衡的点。
- **词汇表限制**（明确提及）：集成解码要求压缩模型与目标模型拥有**相同的词表（Vocabulary）和分词器（Tokenizer）**，这限制了可兼容模型的组合范围，不利于不同生态模型间的灵活搭配。
- **实验覆盖范围**：
  - 尽管在QA数据集上实现了全面SOTA，但未充分评估其在其他知识密集型任务（如事实验证、长文本摘要）或生成多样性与创造力的开放任务上的表现。
  - 主实验中默认采用Contriever作为检索器，未测试与不同检索器（如BM25、Dense Passage Retriever等）的适配性。
  - 主要围绕在开卷（closed-book-like）QA场景，对RAG长对话、多轮交互场景的支持情况未做探讨。

---

（完）
