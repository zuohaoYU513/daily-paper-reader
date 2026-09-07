---
title: "M3D: MultiModal MultiDocument Fine-Grained Inconsistency Detection"
title_zh: M3D：多模态多文档细粒度不一致检测
authors: "Chia-Wei Tang, Ting-Chih Chen, Kiet A. Nguyen, Kazi Sajeed Mehrab, Alvi Md Ishmam, Chris Thomas"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.1243.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 细粒度判断声明中每个方面与多模态证据文档的逻辑关系，溯源具体证据
tldr: 针对现有事实验证只能在样本粒度给出判定，无法定位问题方面与具体证据的问题，提出M3D方法和M3DC基准。该方法预测声明中每个方面与多模态文档集合的细粒度逻辑关系，定位不支持的声明方面与对应证据。通过新合成的多模态多文档基准验证了方法的有效性，为细粒度事实核查和来源追踪提供了方法论支持。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 794, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 898, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1631, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 1021, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 476, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 477, \"height\": 364, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 474, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 475, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 479, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 479, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1004, \"height\": 969, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 615, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1648, \"height\": 1087, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 553, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1554, \"height\": 2414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1663, \"height\": 1637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1647, \"height\": 735, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1657, \"height\": 1100, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1653, \"height\": 1417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main1243/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 475, \"height\": 362, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1243/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1243/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1243/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1243/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1645, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main1243/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 220, \"label\": \"Table\"}]"
motivation: 事实验证现有方法只做样本级预测，无法指出声明中哪个方面有误以及依赖哪份证据，核查效率低。
method: 构建声明合成基准M3DC，使用模型对声明的每个方面预测其与文本、图片、视频、音频等多模态证据的逻辑关系。
result: 在新基准上，该方法能对声明各方面做细粒度不一致判断并定位到具体证据。
conclusion: 提供了一套能在多模态多文档环境中进行细粒度核查与证据溯源的方法体系。
---

## Abstract
Fact-checking claims is a highly laborious task that involves understanding how each factual assertion within the claim relates to a set of trusted source materials. Existing approaches make sample-level predictions but fail to identify the specific aspects of the claim that are troublesome and the specific evidence relied upon. In this paper, we introduce a method and new benchmark for this challenging task. Our method predicts the fine-grained logical relationship of each aspect of the claim from a set of multimodal documents, which include text, image(s), video(s), and audio(s). We also introduce a new benchmark (M3DC) of claims requiring multimodal multidocument reasoning, which we construct using a novel claim synthesis technique. Experiments show that our approach outperforms other models on this challenging task on two benchmarks while providing finer-grained predictions, explanations, and evidence.

---

## 论文详细总结（自动生成）

好的，基于您提供的论文元数据与摘要信息，以下是对该论文的详细结构化总结：

## 1. 核心问题与整体含义

- **研究背景**：事实核查（Fact-checking）是一项人力密集型任务，核查者需要将声明（claim）中每一项事实性断言与一组可信来源材料进行比对。现有自动化方法大多停留在**样本级（sample-level）预测**，即只给出整条声明“支持/反对/证据不足”的粗粒度判定。
- **不足之处**：
  - 无法定位声明中**具体哪个方面（aspect）** 存在问题；
  - 无法指出该问题方面**具体依赖或违背了哪一份证据**；
  - 现有基准往往只涉及单一模态或单一文档，难以满足多模态多文档谣言与虚假信息场景下的细粒度核查需求。
- **整体意义**：论文提出一种**细粒度多模态多文档不一致检测**的新任务设定，让模型不仅能判定整条声明的真实性，还能对声明中每个独立方面给出逻辑关系，并溯源到具体证据片段，从而提升事实核查的自动化粒度与可解释性。

## 2. 提出的方法论

- **核心思想**：将样本级的“声明-证据”关系判定，细化为“**声明中的每个方面 vs. 多模态文档集合**”的细粒度逻辑关系预测，实现“精准定位不可靠声明片段 + 证据溯源”。
- **任务定义**：给定一条声明和一组异构文档（包含文本、图像、视频、音频四种模态），模型需对声明中拆分出的每个方面（aspect）预测其与各证据之间的逻辑关系（如支持、矛盾、证据不足、无关等），输出细粒度的不一致判断。
- **关键技术细节**：
  - **方面粒度切分**：将声明按语义单元拆分为多个独立可验证的方面，作为细粒度预测的基本单位；
  - **多模态文档编码**：对不同模态证据分别编码，并在统一表示空间完成方面-证据的交叉匹配；
  - **细粒度关系分类**：为每个“方面-证据”对预测逻辑关系，覆盖多文档间的联合推理与冲突识别。
- **注**：摘要中未给出具体的模型结构公式或网络架构细节，提供的文字描述仅概述了整体方法范式。
- **M3DC 基准构建**：提出一种新颖的**声明合成技术（claim synthesis）**，自动构造需要多模态、多文档联合推理才能判断真假的高难度声明，形成匹配任务的测评基准 M3DC。

## 3. 实验设计

- **基准数据集**：
  - 论文新构建的 **M3DC基准**：由合成声明组成，每条声明需要综合多模态、多文档证据进行推理；
  - 同时使用了另一个（或多于一个）已有基准进行对比测评，但摘要未指明具体数据集名称。
- **任务场景**：多模态多文档细粒度不一致检测，覆盖文本、图像、视频、音频四种证据模态。
- **对比方法**：论文显示其提出的方法在两个基准上**胜过其他对比模型**，但摘要未列举具体基线名称（如 LLaVA、GPT-4V 等均未出现）。

## 4. 资源与算力

- **摘要中未明确说明**：
  - 未提供使用的 GPU 型号与数量；
  - 未报告训练时长、模型参数规模或硬件环境；
  - 也未提及调参开销或推理资源需求。
- **提示**：如需完整算力信息，需查阅论文正文的实验设置部分。

## 5. 实验数量与充分性

- **已知实验**：
  - 两个基准上的**主实验对比**（证明优秀于其他模型）。
  - 结果表明方法同时提供**更细粒度的预测、解释与证据**。
- **充分性评估**：
  - 摘要层面能确认的实验组数有限，未见明确的消融实验、模态组合分析或跨模型泛化结果描述；
  - 因原始文本仅含摘要，**无法判断是否有消融实验**（如去除某模态的影响）或鲁棒性测试；
  - 有待在全文实验中确认是否对不同声明长度、方面数量、证据数量做难度分层分析；
  - 若仅从摘要看，实验对**可解释性输出质量**的测评方式也未被具体说明。

## 6. 主要结论与发现

- 在细粒度多模态多文档不一致检测任务上，所提出的方法**有效优于现有其他模型**，在两个基准上均表现出更强性能。
- 除了较高的整体判定准确率外，该方法还能：
  - 在**方面级别**做细粒度不一致判断；
  - 输出预测的**解释**；
  - 定位并展示具体支持的**证据**；
- 证明了以“方面-证据”为单位的细粒度核查替代样本级判定是可行且有效的。

## 7. 优点

- **粒度创新**：从样本级预测推进到方面级（aspect-level）预测，能够明确指出声明中哪一部分不可信，这在信息核查应用（如新闻验证、医疗谣言检测）中更有操作价值。
- **证据溯源能力**：输出不仅包含判断，还包括具体引用的证据，提升模型结果的可信度和可追溯性，利于人工复核。
- **多模态、多文档覆盖**：模型同时处理文本、图像、视频和音频四种模态，并可跨多份文件进行证据理解和矛盾发现，更接近实际复杂场景。
- **可用评测基准**：通过自动合成技术构建 M3DC 基准，弥补了该方向缺乏多模态多文档细粒度事实验证评测数据的缺口。
- **解释性输出**：方法被设计为可产出细粒度预测、解释与证据三类输出，较纯分类模型更为透明。

## 8. 不足与局限

- **摘要信息有限**：最明显的是缺少实验设置细节（数据集规模、构建方式、具体评估指标等），不便于独立验证其方法的可复现性。
- **算力信息缺失**：摘要中完全没有提及推理或训练的硬件资源要求，也无法确认在实际部署中的效率。
- **基准的合成性质**：M3DC 基于自动声明合成技术构造，可能与真实网络谣言、自然传播中的声明存在分布偏差，模型在合成数据上的表现未必能完全迁移到真实世界事实核查任务。
- **多模态覆盖的深度未知**：是否对四类模态同等有效、以及存在模态缺失情况下的鲁棒性，在摘要中无法确认。
- **与真实下游应用的结合不足**：未在摘要中展示与现有事实核查流程（human-in-the-loop）的衔接情况，也未讨论在开放域证据检索中的适用性。
- **模型细节未给出**：架构主体及其不同类型证据的融合机制未在摘要中解释清楚，需要阅读正文才能评估方法论的新颖性与可复现性。

（完）
