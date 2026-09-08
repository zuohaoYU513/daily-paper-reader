---
title: "All That Glitters is Not Gold: Improving Robust Retrieval-Augmented Language Models with Fact-Centric Preference Alignment"
title_zh: 闪光的未必是金：通过以事实为中心的偏好对齐提升鲁棒检索增强语言模型
authors: "Jia Hao, Chunhong Zhang, Jiarun Liu, Haiyu Zhao, Zhiqiang Zhan, Zheng Hu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.588.pdf"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 针对检索增强生成中噪声或干扰文档造成的幻觉问题，提出基于事实中心的偏好对齐以提升生成可靠性
tldr: 针对检索增强语言模型易受高相关噪声文档干扰、从而影响事实性生成的问题，提出以事实为中心的偏好对齐方法FPA。该方法构建偏好数据让模型从检索结果中提取真正有用的事实信息，而不是依赖整段文档或先过滤噪声。实验表明该方法相较于传统噪声过滤和自适应检索方案更具鲁棒性，能有效缓解检索噪声导致的幻觉。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 651}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 768}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 524}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 358}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 506}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 81, \"height\": 98}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 765, \"height\": 497}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl588/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 765, \"height\": 490}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 715, \"height\": 276}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1586, \"height\": 671}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1642, \"height\": 371}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 197}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 345}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1640, \"height\": 1340}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl588/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1631, \"height\": 1677}]"
motivation: 已有噪声过滤会丢失关键信息，且难以应对高语义相关的干扰文档，降低检索增强模型的生成质量。
method: 提出FPA，通过基于文档内容事实性的偏好数据与偏好优化训练，让LLM直接抽取有用信息并摆脱噪声。
result: 实验显示FPA在噪声检索场景下比传统过滤与微调方法更稳健，能有效减少干扰文档导致的错误。
conclusion: 以事实为中心的偏好对齐能提升检索增强模型的抗噪能力，为RAG幻觉缓解提供了有效训练策略。
---

## Abstract
Retrieval-augmented language model (RALM) relies on retrieved external knowledge to generate responses, resulting in vulnerability in the face of retrieval results with noisy documents. Previous works integrate additional filters or finetune Large Language Models (LLMs) to learn adaptive retrieval to reduce the performance damage of noisy documents. However, prior noise filtering may lead to the loss of crucial information, and these methods do not focus on distracting documents with high semantic relevance, which is the most challenging problem. In this study, we propose a training method for fact-centric preference alignment (FPA) to improve the ability of LLMs to directly extract useful information from noisy retrieval results without prior filtering. Our method performs positive document mining based on factual consistency and uses LLMs self-generated synthetic data as training data without manual annotation. We evaluate our FPA on four question answering benchmarks, and the experimental results demonstrate that our method achieves significant improvement with a small scale of training data.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与研究背景

检索增强语言模型（RALM）通过引入外部检索文档来弥补大语言模型（LLM）知识不足或幻觉的问题，但检索结果并非总是干净，其中常混有**不相关文档**乃至**高语义相关的干扰文档（distracting documents）**，它们会显著误导 LLM 生成错误答案。论文指出，这类干扰文档是“最棘手的问题”，因为它们与问题在语义上高度接近，却包含不同的事实。

已有应对思路主要有两条，但都存在不足：
- **在后处理阶段做过滤**（如重排、压缩）：可能导致关键信息被过度过滤而丢失，造成性能下降。
- **通过微调让 LLM 自适应决定是否检索**：没有专门提升模型辨识高语义相关干扰文档的能力，在被提供检索结果时仍易被误导。

为此，论文提出一种以**事实中心偏好对齐**为思路的训练方法 **FPA**（Fact-centric Preference Alignment），目标是让模型在面对检索噪声时，不依赖前置过滤，直接从中提取真正有用的事实信息，并在文档无用时回退到内部知识作答。

## 2. 方法论

### 2.1 核心思想

将“文档相关性”的评判从**语义相似性**转向**事实一致性**——即判断文档是否与“问题 + 标准答案”形成的事实陈述（ground truth statement）一致，而非仅仅看是否包含答案词或语义相近。因为干扰文档往往语义相近而事实矛盾。

### 2.2 正向文档挖掘

- 形式化：对问题 q 和标准答案 â，合成事实陈述 s = f(q, â)。
- 将文档 d 与 s 输入 **NLI 模型**进行蕴含关系识别（RTE 任务）：若 doc 与陈述 s 的关系为 **Entailment（蕴含）**，则该文档判为正向文档（factual consistent），否则为负向文档。

公式为：

```
con(d, s) = I(P(E) > max(P(C), P(N)))
```

其中 C/N/E 分别为矛盾、中立、蕴含。文中使用 **BART-Large-MNLI** 实现该标注。

论文还通过让 LLM 对文档做可回答性（Ans）和事实一致性（Con）打分，将检索文档划分为相关文档、潜在无关文档、无关文档、干扰文档四类，统计后发现：RAG 答错时“干扰文档”占比更高，提示模型常误把这些文档当成相关。该分析为方法提供了依据。

### 2.3 偏好数据构造

- 对每个（来自 NQ 训练子集的）问题，取 top-ks 文档作为种子集 Ds，从中选出 kt 个构造训练上下文 Dt（实验中 ks=8, kt=5），其中包含若干正向文档（最多 kt−1 个）和随机负向文档，并**随机打乱顺序**以提升难度和位置鲁棒性。
- 在 prompt 末尾加入引文触发指令（如 "According to documents 1 and 5"），用于控制模型引用范围：
  - **Chosen response**：引用全部正向文档，并要求回答正确。
  - **Rejected response**：逐个只引用某个负向文档，且只保留回答错误的样本。
- 为缓解 LLM 引用索引幻觉，设计了 **citation mismatch data augmentation**：将 chosen response 中某个被引用文档索引改换为一个未被引用的文档索引，构成 rejected 样本，强化模型对索引-内容一致性的敏感性。

### 2.4 偏好对齐与推理

- 使用 **DPO**（Direct Preference Optimization）微调生成器，损失函数：

```
L_DPO = −E[log σ(rθ(x, y_w) − rθ(x, y_l))]
rθ(x, y) = β log(πθ(y|x)/πref(y|x))
```

其中输入 x = I ⊕ Dt ⊕ q，y_w 为引用正向文档且回答正确的首选项，y_l 为参照负向文档而答错的次选项。

- 推理时引入**自适应检索提示**（adaptive retrieval prompting），告诉模型“若检索文档不含用信息，可根据自身知识补充作答”，以减少无相关信息时的强制套用上下文。

## 3. 实验设计

### 3.1 数据集与评测

| 任务 | 数据集 | Retriever |
|---|---|---|
| 短答案问答 | Natural Questions（NQ） | DPR |
| 短答案问答 | PopQA | Contriever-MS MARCO |
| 短答案问答 | TriviaQA | Contriever |
| 长答案问答 | ASQA | GTR |

指标：NQ、PopQA、TriviaQA 使用 EM（Exact Match）；ASQA 使用 ALCE 的 str-em（正确性）、citation precision（引文精确率）和 citation recall（引文召回率）。

### 3.2 对比方法

**不使用检索**
- w/o Retrieval：LLM 直接依靠参数知识回答。

**不微调 LLM 的 RAG**
- Vanilla RAG：直接使用 top-5 检索文档。
- RAG w/ rerank：RankT5-large 重排后取 top-5。
- RAG w/ compress：LongLLMLingua 压缩 top-5 文档。

**微调 LLM 的 RAG 方法**
- Self-RAG、RetRobust、InstructRAG-FT（并比较只使用 NQ 训练的 InstructRAG-FT † 做跨域评估）。

所有 FPA 数据（约 5k 偏好样本）均取自 NQ 训练集，并使用相同的 Llama-3-8B-Instruct 基座模型。报告性能分为 NQ 的域内结果与其它数据集的域外结果。

## 4. 资源与算力

- 文中明确说明：使用 **2 块 NVIDIA RTX 4090**，通过 **LoRA** 对 Llama-3-8B-Instruct 微调，训练 5 个 epoch，耗时约 **3.5 小时**，模型通过 HuggingFace 的 LLaMA-Factory 框架实现。
- 代码已公开：https://github.com/haojiahj/FPA。

## 5. 实验数量与充分性评估

论文实验较充足且基本客观：

1. **主实验**（表 2）：覆盖 4 个 QA benchmark 与 8 类基线，衡量 EM、str-em、citation precision/recall；且同时报告 NQ 域内以及其它数据上的域外表现。
2. **消融研究**（表 3）：对偏好对齐、自适应检索提示、citation mismatch 增广三组件逐项与叠加消融。
3. **鲁棒性分析**（图 4、图 5）：
   - 不同噪声比例下的准确率；
   - 相关文档出现在不同位置时的性能变化；
   - top-k 检索数量（k = 1/5/10）时的通用性。
4. **证据依赖分析**（表 4）：比较 finetune 后的 FPA 在“提供证据 vs. 不提供证据”下的表现，验证模型不是仅依赖内部记忆。
5. **效率分析**（表 5）：对比数据规模、对 GPT-4 的依赖、训练模块数量等。
6. **案例分析**（图 6 和附录 B）：展示无有用文档和有有用文档两种场景下的典型输出，直观比较 FPA 与 Vanilla RAG/InstructRAG-FT 的行为。
7. **附录的数据统计**（图 7-8）：正文档位置分布、正文档数量分布，说明训练数据的均衡性。

从数量和方式上看，实验较为充分：既覆盖了鲁棒性的多种因素（噪声比例、位置、文档数量），也做了域外泛化和无证据对照，令结论更有说服力。不过部分基线指标引自原论文而非完全复现，属于该领域常见的合理做法；论文也自述只做单次运行、未报告多次种子方差。

## 6. 主要结论与发现

- 相比 Vanilla RAG，FPA 在所有数据集上均显著提升，如 NQ 从 56.5→66.9，PopQA 从 62.7→67.1，TriviaQA 从 71.7→78.7，ASQA 的 str-em 由 42.5→48.8。
- 在 NQ 域内、以及跨到 PopQA/TriviaQA/ASQA 的域外表现，均优于 InstructRAG-FT（同为仅用 NQ 训练），尤其在 ASQA 上明显胜出。
- 消融显示：**偏好对齐**是最核心的训练组件，自适应检索提示能有效提升低检索质量时的表现，citation mismatch 增广更侧重提高引用质量而非问答准确率。
- 对各噪声分档（图 4），FPA 都优于 / 不低于基线；即使 top-5 文档全部不相关时准确率仍有 22.88%，说明自适应检索提示确实起到“回退内部知识”的作用。
- 由于训练时对文档位置做了随机化，FPA 对相关文档出现在上下文中间或末尾的场景也不再出现明显的“lost-in-the-middle”式衰减。

## 7. 优点

1. **切入点新颖**：从“事实是否一致”界定文档是否为正样本，而非由人工标注的 gold passage 或简单“包含答案词”定义——能温和处理“包含正确答案但实际无关”这类特殊负例。
2. **低成本全自动数据构建**：利用 NLI 模型和 LLM 自身采样生成训练数据，无需人工标注、无需调用 GPT-4。
3. **高效**：仅用 5k 规模的小数据量、两个 GPU、一块 8B 模型即可超越一些 70k 数据级别的方法，说明方法的数据效率高。
4. **较强的鲁棒性设计**：文档随机洗牌提升了位置稳健性；对抗噪声比和不同文档数量实验均说明其效果好不是偶然。
5. **较高的可迁移性**：同一份模型无需针对每个检索器或任务单独微调，即可适应不同检索源，并能从短答案 QA 迁移到长答案 QA。
6. **分析细致**：初步统计“相关/潜在无关/无关/干扰”文档在 RAG 答对与答错时的分布比例，从侧面验证了问题诊断的正确性。

## 8. 不足与局限

1. **任务覆盖仍有限**：实验始终围绕**单跳**开放域问答（NQ、PopQA、TriviaQA、ASQA），未考虑多跳推理或领域特定任务，其泛化性还有待验证。
2. **依赖标准答案和 NLI 模型**：正负文档挖掘需要“问题-答案”组成的标准事实陈述；对于没有标准答案或答案不可获得的场景，该挖掘方式可能失效，NLI 模型的标注噪声也会影响数据质量。
3. **模型规模单一**：主体实验仅采用 Llama-3-8B-Instruct，无法判断该方法对更大模型是否仍然有效或仍有类似增益。
4. **引文精确率并非最优**：作者也承认偏好数据鼓励“尽量多引用有用文档”而非“引用最少但足够的文档”，故 citation precision 不如一些针对性优化的方法（如 InstructRAG-FT）。
5. **对极端差检索质量仍有局限**：当检索文档整体质量极差时，模型即使具备回退知识能力，性能提升也有限（作者在 Limitations 中自述）。
6. **可复

6. **可复现性不足**：文中明确说明只进行单次运行，未报告多种随机种子下的均值与方差，因此无法严格评估训练和采样过程中的稳定性；同时部分基线指标引自原始论文而非在完全一致的设置下复现，可能引入潜在比较偏差。

总体而言，FPA 针对 RALM 中“高语义相关干扰文档”这一棘手问题，提出了一种数据高效、无需人工标注的偏好对齐训练方案。其核心贡献在于将文档相关性从“语义相似”转变为“事实一致”，并借助 NLI 模型自动构建偏好数据，使模型学会在噪声上下文中只采信与事实相符的文档；配合自适应检索提示，还可在检索文档完全无用时有意识地回退到内部参数知识。该方法在 NQ、PopQA、TriviaQA、ASQA 等多个开放域问答基准上取得一致的显著提升，并展现出较强的跨域迁移能力和位置鲁棒性，且训练成本极低，具有较强的实用价值。

不过，其局限也同样明显：依赖“问题-标准答案”构成的 NLI 事实判断使其不易推广到没有标准答案或多跳推理任务；实验仅基于 8B 规模模型且缺乏多次运行统计；引文精确率并非最优，且检索质量极差时收益仍有限。未来若能拓展任务范围、验证更大规模模型、补充更严谨的统计比较，将进一步提升结论的可信度。

（完）
