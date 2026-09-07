---
title: "From Extraction to Deduction: Resolving Functional Misalignment in RAG via a Collaborative Critic-Reasoner Framework"
title_zh: 从抽取到演绎：通过协作式评论-推理框架解决RAG中的功能错配
authors: "Yufei Chen, Yao Wang, Haibin Zhang, Hualin zhou, Tao Gu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5d8b4bf449fb1dec8f2da1f85a3bd49ef389dc13.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 在RAG中由Critic净化检索证据、Reasoner生成，防止生成器采纳错误证据而编造内容
tldr: 检索增强生成中检索器偏重语义相关，常常召回包含错误答案片段的文档，使生成器将其当作捷径产生虚假内容。该工作提出Critic-Reasoner协作框架，将生成过程解耦为Critic的细粒度证据净化与Reasoner的推理性生成，先遮蔽误导实体并保留支持性背景再到解码。该方法把RAG的鲁棒性控制从粗粒度过滤转向细粒度认知解耦，从而减少对错误证据的盲从，提升生成内容的正确性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: RAG中检索结果虽语义相关却可能含有错误事实片段，生成器倾向直接采纳这些认知捷径。
method: Critic识别并遮蔽检索文档中的误导性实体，保留支持性上下文，随后由Reasoner基于净化后的证据进行生成。
result: 框架能有效缓解生成器对错误检索内容的盲从，提高最终回答的事实正确性。
conclusion: 细粒度证据净化配合串行化角色分工可改善RAG生成的事实可靠性。
---

## Abstract
Retrieval-augmented generation (RAG) systems suffer from a fundamental functional misalignment where retrievers optimize for semantic relevance, often recalling documents with high background utility but factually erroneous answer spans that generators blindly adopt as cognitive shortcuts. To resolve this, we propose the collaborative Critic-Reasoner framework that shifts robustness control from coarse-grained filtering to fine-grained cognitive decoupling. We disentangle the generation process into two serialized roles by deploying a Critic to perform surgical evidence purification through identifying and masking misleading entities while preserving supportive background context, followed by a Reasoner that switches from rote extraction to deductive reasoning based on the residual evidence. We operationalize this framework via a two-stage alignment strategy combining supervised fine-tuning (SFT) with path-aware direct preference optimization (DPO) to enforce strict behavioral synergy. Experimental results on adversarial benchmarks such as ConFiQA demonstrate that our method significantly outperforms baselines, achieving a 25.99\% accuracy gain in conflicting scenarios and effectively resolving the trust bias dilemma in real-world RAG.

---

## 论文详细总结（自动生成）

# 论文总结：从抽取到演绎：通过协作式评论-推理框架解决RAG中的功能错配

## 1. 论文的核心问题与整体含义

- **核心问题**：检索增强生成（RAG）系统存在“功能错配”——检索器以语义相关性为优化目标，经常召回与问题高度相关但包含事实性错误答案片段（answer span）的文档；生成器则倾向于将这些错误片段当作“认知捷径”直接采用，从而产生不忠实甚至虚假的生成内容。
- **研究动机**：传统 RAG 的鲁棒性控制主要依赖粗粒度的文档过滤或后处理，难以应对“相关但错误”的细粒度证据。论文希望从认知层面解耦“检索到的背景”与“需要推理的答案”，避免生成器对错误证据的盲从。
- **整体含义**：提出由 Critic（评论者）与 Reasoner（推理者）协作的框架，将 RAG 的鲁棒性控制从粗粒度过滤转向细粒度认知解耦，提升生成内容的事实正确性与可信性，解决现实 RAG 系统中的“信任偏差”（trust bias）问题。

## 2. 论文提出的方法论

- **核心思想**：把生成过程解耦为两个串行化的角色，各自承担不同认知功能：
  - **Critic**：负责“外科手术式”的证据净化（evidence purification），具体做法是识别并遮蔽（mask）检索文档中的误导性实体，同时保留对回答有用的支持性背景上下文。
  - **Reasoner**：基于 Critic 净化后的残余证据进行演绎推理（deductive reasoning），从“机械抽取”转变为“逻辑推导”，避免直接复制错误片段。
- **关键技术细节**：
  - 将上述角色分工作为一种细粒度的认知解耦策略，强调“净化”发生在解码前，而非在最终输出后做过滤。
  - 采用**两阶段对齐策略**实现训练，以保证 Critic 与 Reasoner 的行为协同：
    1. 监督微调（SFT）：让各角色学会各自的任务（识别/遮蔽与推理生成）。
    2. 路径感知的直接偏好优化（path-aware DPO）：在偏好优化中引入“路径”信息，强制模型在给定净化轨迹上产生更优行为。
- **公式 / 算法流程**：论文提供的摘要中未给出具体数学公式或伪代码；从描述推断流程为：先检索，Critic 逐实体判断并遮蔽误导信息，保留上下文，再交给 Reasoner 生成答案。训练阶段先 SFT 后 path-aware DPO。

## 3. 实验设计

- **数据集 / 场景**：摘要中明确提到使用了**对抗性基准 ConFiQA**（conflicting-question-answering，冲突问答），对应“真实世界中检索证据与生成答案存在冲突”的场景。
- **Benchmark**：ConFiQA 属于对抗性评测集，专门构造检索结果包含高相关背景但错误答案片段的情况。
- **对比方法**：摘要仅提到“significantly outperforms baselines”，但未列出基线方法名称（如普通 RAG、重排序、事后纠正等均未在摘要中出现）。
- **评价指标**：报告中提到“accuracy”，冲突场景中方法获得了 **25.99% 的准确率提升**，说明最终生成的正确率是主要衡量标准。

## 4. 资源与算力

- 论文摘要和所提供元数据中**完全没有提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量等。
- 因此，无法从现有材料判断该方法的训练代价或可扩展性；若需要可复现的算力信息，必须查阅完整论文的“实验设置”或“实现细节”部分。

## 5. 实验数量与充分性

- **已呈现的实验数量**：根据摘要，至少有一组核心量化结果——在 ConFiQA 冲突场景下相对基线提升 25.99% 准确率。可能还包含其他数据集，但摘要未给出。
- **未呈现的实验**：没有列出多个数据集上的完整结果，没有明确的基线对比表格，没有展示消融实验（如去掉 Critic、去掉 DPO 等），也没有说明统计显著性与重复实验次数。
- **充分性与客观性评估**：由于提供的材料仅为摘要层次，实验信息不足以判断充分性与公平性。需要完整论文中的实验设计、基线选择、超参数设置等来佐证。当前只能认为“初步证明了方法有效”，但尚不足以作全面可靠的评估。

## 6. 论文的主要结论与发现

- 协作式 Critic-Reasoner 框架能有效缓解生成器对错误检索内容的“盲从”，降低错误证据被当作捷径使用的概率。
- 将粗粒度过滤替换为细粒度“证据净化 + 演绎生成”之后，RAG 在对抗冲突场景中的准确率显著提高（提升 25.99%）。
- 两阶段对齐（SFT + path-aware DPO）能够强化“净化”与“推理”之间的行为协同，进而解决现实世界 RAG 系统中的信任偏差问题。
- 该工作认为 RAG 的事实可靠性问题根源不在检索精度，而在生成器对“语义相关但事实错误”证据的错误利用，因此需要从认知分工上重构生成框架。

## 7. 优点

- **问题刻画有新意**：明确区分“背景相关性”与“答案正确性”，点出了 RAG 中一种容易被忽略但实际很常见失败模式。
- **方法设计新颖**：提出“细粒度认知解耦”，不是简单对整篇文档做相关性过滤，而是对具体实体级别做“保留 vs 遮蔽”，保留了可用背景，这种“外科手术式”净化有较高可解释性。
- **训练策略配合较好**：用 SFT 初始化子任务，再用 path-aware DPO 优化整体路径——相比单任务微调更能保证 Critic 与 Reasoner 的协作一致性。
- **实验场景具有对抗性**：选用 ConFiQA 这类冲突问题基准，较好贴合“检索相关但答案错误”的困境，能在严苛环境下验证方法。
- **表述清晰**：摘要用“抽取 → 演绎”和“过滤 → 解耦”等对比强烈地突出了贡献点。

## 8. 不足与局限

- **信息完整性受限**：当前只基于论文摘要和元数据，无法确认方法内部细节（例如如何训练 Critic 识别误导实体、是否需要对上游检索器做任何改动、额外推理开销有多大等）。
- **实验覆盖面有限**：仅从摘要看到 ConFiQA 一个基准；现实中的 RAG 还涉及多跳问答、开放域知识问答、反事实场景等，缺少验证。
- **缺乏消融与分析**：对于“Critic 遮蔽是错误的实体，会不会误伤正确信息”“Reasoner 的演绎能力在不同大模型上的适应性”等问题，摘要未提供答案。
- **适用性限制**：该框架引入了串行的 Critic 和 Reasoner，可能增加系统复杂度与推理延迟；且依赖质量较高的“检索文档中错误往往是局部实体、可屏蔽”的假设，若整篇文档都对答案形成误导，可能效果受限。
- **客观公平性**：无法确认基线是否包含多种代表性强基线，也可能存在选择性报告最优数字的风险；需要补充不同种子、不同模型、不同数据分布下的实验。
- **算力未报告**：缺少训练和推理的算力信息，会限制他人复现及横向比较效率。

（完）
