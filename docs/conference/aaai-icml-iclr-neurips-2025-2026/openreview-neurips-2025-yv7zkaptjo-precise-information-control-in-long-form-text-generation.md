---
title: Precise Information Control in Long-Form Text Generation
title_zh: 长文本生成中的精确信息控制
authors: "Jacqueline He, Howard Yen, Margaret Li, Shuyue Stella Li, Zhiyuan Zeng, Weijia Shi, Yulia Tsvetkov, Danqi Chen, Pang Wei Koh, Luke Zettlemoyer"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yv7zKaptjo"
tags: ["query:faithfulness"]
score: 9.0
evidence: 提出精确信息控制任务，要求长文本生成严格基于给定论断且不添加无依据内容，并含摘要类基准，直接针对忠实性幻觉
tldr: 长文本模型中常见的不忠实幻觉指生成未经输入上下文支持的信息。本文提出精确信息控制任务，让模型依据一组简短论断生成长文本，既要完整覆盖应包含的论断，也不得附加无依据内容，并构建含摘要、传记等八类任务的PIC-Bench基准。完整设置与部分设置分别测试模型不漏内容以及按需选择的能力，为摘要和数据到文本等场景的事实忠实度评估提供了可验证的新范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 长文本模型常产生无输入支持的幻觉信息，已有生成任务缺乏对输出信息是否受给定断言支持的可控约束。
method: 提出精确信息控制任务与PIC-Bench基准，包含完整和选择性两类设置，要求从给定可验证论断生成受支持的连贯长文。
result: 基准揭示LM在只包含输入论断且不添加无依据内容方面存在明显不足，为忠实性研究提供评测基础。
conclusion: PIC为监督和评测长文本生成的证据忠实性提供了可验证的统一框架。
---

## Abstract
A central challenge in language models (LMs) is faithfulness hallucination: the generation of information unsubstantiated by input context. To study this problem, we propose Precise Information Control (PIC), a new task formulation that requires models to generate long-form outputs grounded in a provided set of short self-contained statements, without adding any unsupported ones. PIC includes a full setting that tests a model’s ability to include exactly all input claims, and a partial setting that requires the model to selectively incorporate only relevant claims. We present PIC-Bench, a benchmark of eight long-form generation tasks (e.g., summarization, biography generation) adapted to the PIC setting, where LMs are supplied with well-formed, verifiable input claims. Our evaluation of a range of open and proprietary LMs on PIC-Bench reveals that, surprisingly, state-of-the-art LMs still hallucinate against user-provided input in over 70% of generations. To alleviate this lack of faithfulness, we introduce a post-training framework that uses a weakly supervised preference data construction method to train an 8B PIC-LM with stronger PIC ability—improving from 69.1% to 91.0% F1 in the full PIC setting. When integrated into end-to-end factual generation pipelines, PIC-LM improves exact match recall by 17.1% on ambiguous QA with retrieval, and factual precision by 30.5% on a birthplace fact-checking task, underscoring the potential of precisely grounded generation.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- 论文聚焦语言模型（LM）在长文本生成中的“忠实性幻觉”问题，即模型会生成输入上下文并未提供的、无法被证据支持的内容。
- 为此提出 **Precise Information Control（PIC，精确信息控制）** 这一新任务：模型必须基于一组给定的、简短且自包含的陈述（claims）生成连贯的长文本，并且**只能**包含这些陈述，不能额外添加无依据的信息。
- PIC 包含两种设置：
  - **完整设置（full setting）**：要求模型恰好包含所有给定陈述，测试会不会遗漏输入信息；
  - **部分设置（partial setting）**：要求模型只选择性地纳入与生成目标相关的陈述，测试信息筛选能力。
- 该任务形式将长文本生成与可验证输入直接绑定，为摘要、传记等场景下的事实忠实性提供了更可控、可评判的研究范式。

## 2. 方法论：核心思想与关键技术

- 核心思想是：把“忠实性”问题转化为输入与输出之间可验证的覆盖/控制问题，要求模型生成文本中的信息严格来源于给定的论断集合。
- 文章构建了 **PIC-Bench**：将八类长文本生成任务（如摘要、传记生成）改造成 PIC 形式，为模型提供结构良好、可验证的输入论断。
- 针对现有模型在该任务上的不足，论文提出一个**后训练框架**：
  - 使用**弱监督偏好数据构造方法**自动构建偏好数据；
  - 通过偏好优化/对齐式训练得到 **PIC-LM**（8B 参数规模）；
  - 目标是在满足 PIC 约束（不漏输入、不加无依据信息）的同时保持文本连贯性和质量。
- 需要说明：当前可获取的文本中未提供伪代码级的算法流程、偏好数据的具体构造公式或损失函数细节，完整技术方案应查看论文正文。

## 3. 实验设计：数据集、基准与对比

- 论文提出并使用了统一评测基准 **PIC-Bench**，覆盖八类任务：包括摘要生成、传记生成等常见长文本生成场景。
- 在 PIC-Bench 上评估了**多种开源与专有 LM**，覆盖面较广（可用文本中未列出具体模型名称）。
- 实验包括两大层面：
  1. **PIC-Bench 基准评测**：在完整设置与部分设置两种模式下测量模型的“忠实覆盖/不添加”能力；
  2. **下游流水线验证**：将训练后的 PIC-LM 集成到端到端事实生成系统中，在两类下游任务上检验实际收益：
     - 带检索的模糊问答（ambiguous QA with retrieval）；
     - 出生地事实核查（birthplace fact-checking）。
- 主要评估指标包括 F1、精确匹配召回率、事实精确率等。

## 4. 资源与算力

- 在提供的文本（摘要与元数据）中，**没有明确说明** GPU 型号、数量、训练时长等算力信息。
- 能确定的是训练出的目标模型 **PIC-LM 规模为 8B 参数**；训练过程采用弱监督偏好数据构造方法，但具体计算开销未给出。
- 如需完整的算力报告，需要查阅论文实验部分或附录。

## 5. 实验数量与充分性

- 从可获取信息看，至少进行了以下层面的实验：
  - 在含八类任务的 PIC-Bench 上对多种开放/专有 LM 进行基线评测；
  - 在完整设置下比较 PIC-LM 与基线模型（报告从 69.1% 到 91.0% 的 F1 提升）；
  - 两个下游任务中的集成与增益验证。
- 整体实验设计具备**跨任务广度**与**下游应用验证**，说明该框架有一定通用性。
- 但由于没有完整实验细节，**无法判断消融研究是否充分、统计显著性是否报告、多次运行方差是否控制**；就可用内容而言，实验覆盖是合理的，但充分性和公平性的深入评估有待阅读全文后才能完成。

## 6. 主要结论与发现

- 在 PIC-Bench 上，即便是前沿的开放或专有 LM，仍然在**超过 70% 的生成结果中**会出现针对用户输入论断的幻觉，即加入或遗漏了不应出现的信息。
- 通过弱监督偏好数据训练出的 8B 规模 PIC-LM：
  - 在完整 PIC 设置下从 **69.1% 提升到 91.0% F1**；
  - 集成到下游流水线后：
    - 在带检索的模糊问答中，精确匹配召回率提升 **17.1%**；
    - 在出生地事实核查任务中，事实精确率提升 **30.5%**。
- 结论是：精确受控生成不仅能提升本身任务的忠实性，也能改善下游事实生成流水线的可靠性，具有实际应用价值。

## 7. 优点

- **任务定义清晰**：将“不幻觉”操作化为“精确包含指定论断且不添加额外内容”，便于自动评估。
- **形式化区分重要**：完整设置与部分设置分别对应信息覆盖与信息筛选问题，更贴近实际场景。
- **基准设计有规模**：覆盖八类长文本任务，且输入采用结构化、可验证的陈述，比普通“摘要”评测更能定位模型忠实性缺陷。
- **训练成本合理**：使用弱监督方法来构造偏好数据，避免大规模人工标注，并以 8B 模型实现较大效果提升。
- **验证了下游收益**：不只是在合成基准上提升，还接入问答与事实核查流水线，证明 PIC 方法具有可迁移的真实价值。

## 8. 不足与局限

- **可获取信息有限**：此处仅有摘要与元数据，缺少完整方法细节、评估细节与消融实验，限制了对理论证明和工程设计的深入评估。
- **基线与覆盖范围未完全展示**：摘要未指出具体测试了哪些开源/专有模型，也没有说明 PIC-Bench 任务内各领域的难度分布；可能受限于英文或特定文本领域。
- **信息控制 vs. 文本质量**：以“只包含给定 claims”作核心标准时，可能对文本的连贯性、可读性与表达多样性约束不够，需要更多人工评估来排除“机械拼凑”式输出。
- **模型规模有限**：验证的是 8B 模型；更强的指令遵循与推理能力往往依赖更大模型，PIC 方法对更大模型的迁移效果尚不明确。
- **依赖输入论断质量**：框架有效性取决于给定的 claims 是否“结构良好、可验证”；如果上游抽取或提供的 claims 有噪声、冗余或冲突，则下游生成能力可能会被连带削弱。
- **算力与数据成本不透明**：未能论证弱监督偏好构造开销与可扩展性，可能限制社区复现或更大规模应用。

（完）
