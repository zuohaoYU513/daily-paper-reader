---
title: Learning Auxiliary Tasks Improves Reference-Free Hallucination Detection in Open-Domain Long-Form Generation
title_zh: 学习辅助任务提升开放域长文生成中的无参考幻觉检测
authors: "Chengwei Qin, Wenxuan Zhou, Karthik Abinav Sankararaman, Nanshu Wang, Tengyu Xu, Alexander Radovic, Eryk Helenowski, Arya Talebzadeh, Aditya Tayade, Sinong Wang, Shafiq Joty, Han Fang, Hao Ma"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-short.93.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 面向开放域长文生成的无参考幻觉检测，发现仅靠内部状态不足，借辅助任务提升检测可靠性
tldr: 论文针对开放域长文生成中的幻觉检测展开系统研究，指出现有方法或局限于少数领域，或依赖外部事实核查工具。实验表明模型输出概率与熵等内部状态单独不足以可靠区分事实与幻觉内容。为此提出利用辅助任务学习来增强无参考幻觉检测能力，在不依赖外部工具情况下提高判断可靠性。实验结果验证辅助任务能显著改善检测效果，为长文本幻觉监测提供了轻量化方案。
source: ACL-2025-Short
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 505}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 781, \"height\": 488}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 479}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 477}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 477}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 770, \"height\": 129}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 773, \"height\": 646}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 777, \"height\": 527}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 176}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 765, \"height\": 176}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 600, \"height\": 207}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 760, \"height\": 177}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 124}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 365, \"height\": 126}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 366, \"height\": 126}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 130}]"
motivation: 开放域长文生成中大模型幻觉严重，而现有检测依赖外部事实工具或局限于少数领域，需要更自包含的检测方法。
method: 系统研究无参考幻觉检测，引入辅助任务学习信号，以模型内部状态结合辅助任务来区分事实与幻觉内容。
result: 结果显示仅靠内部状态无法可靠区分，而学习辅助任务显著提升了检测性能。
conclusion: 无参考场景下可通过辅助任务提高幻觉检测能力，减少对外部事实核查工具的依赖。
---

## Abstract
Hallucination, the generation of factually incorrect information, remains a significant challenge for large language models (LLMs), especially in open-domain long-form generation. Existing approaches for detecting hallucination in long-form tasks either focus on limited domains or rely heavily on external fact-checking tools, which may not always be available.In this work, we systematically investigate reference-free hallucination detection in open-domain long-form responses. Our findings reveal that internal states (e.g., model’s output probability and entropy) alone are insufficient for reliably (i.e., better than random guessing) distinguishing between factual and hallucinated content. To enhance detection, we explore various existing approaches, including prompting-based methods, probing, and fine-tuning, with fine-tuning proving the most effective. To further improve the accuracy, we introduce a new paradigm, named RATE-FT, that augments fine-tuning with an auxiliary task for the model to jointly learn with the main task of hallucination detection. With extensive experiments and analysis using a variety of model families & datasets, we demonstrate the effectiveness and generalizability of our method, e.g., +3% over general fine-tuning methods on LongFact.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：大语言模型（LLMs）在开放域长文本生成（如回答百科类开放问题）中容易产生“幻觉”——生成看似流畅但不符合事实的内容。相比短文本任务，长文本生成需要模型综合跨领域知识，幻觉检测的复杂度显著更高。
- **现有方法的不足**：
  - 许多已有幻觉检测方法聚焦于短表单轮输出；
  - 针对长文本的检测工作往往局限于少数领域（如传记生成）或过度依赖外部事实核查工具（如 Google Search），这些工具并非总是可用或可扩展。
- **核心问题**：**能否提出一种“无参考”（reference-free）的幻觉检测方法，仅依靠模型自身能力（如内部状态、微调等），不依赖外部知识库或检索工具，就能在开放域长文本中可靠区分“事实性”与“幻觉性”内容？**
- **整体含义**：论文系统性地探索了多种无参考检测方案，发现仅靠模型内部状态（概率、熵）的检测效果几乎等同于随机猜测，而在引入“辅助问答任务 + 推理理由”进行微调后，可显著提升幻觉检测准确性。这项工作为长文本环境下构建自包含、可扩展的幻觉检测器提供了新范式。

## 2. 论文提出的方法论

论文分为“分析阶段”与“方法创新阶段”两部分：

### 2.1 内部状态检测分析（前期探索）
- 将长文本响应拆分为原子化声明（atomized claims），并用 Google Search 标注正误，构建检测基准。
- 尝试利用模型对声明中各 token 的**输出概率**或**熵（不确定性）**作为幻觉信号，具体变体包括：
  - 所有 token 的算数平均或几何平均（即困惑度）；
  - 取概率最低/熵最高的前 K 个 token 的平均值（K=1、3、5）；
  - 取概率最低/熵最高的前 P% token 的平均值（P=5、10、15）。
- 还额外探索了仅针对“实体相关词”的上述变体。
- **发现**：所有内部状态都无法有效区分事实声明与幻觉声明（性能不优于随机猜测）。原因是长文本声明中混杂大量无关紧要的停用词，且概率/熵反映的是“模型对该 token 序列的生成置信度”，而非“声明内容本身的事实正确性”。

### 2.2 三种已有方法对比
- **Prompting 方法**：
  - `Prompt TF`：直接要求模型输出 True/False；
  - `Prompt Prob`：要求模型输出认为声明正确的概率（0~1）；
  - `SelfCheckGPT`：采样 20 条新响应，通过对比一致性判断；
  - `Prompt CoT-TF`：要求模型先给出推理路径再给出 True/False。
- **Probing 方法**：冻结原 LLM，在其上下文嵌入之上训练一个 MLP 分类器；
- **Fine-Tuning 方法**：用 LoRA 微调 LLM，输入声明并训练其输出 True/False。

实验显示 **Fine-Tuning 效果最佳**（LongFact 上 BAcc 76.1%），Probing 次之，Prompt TF 与 SelfCheckGPT 一般，Prompt Prob 最差。

### 2.3 新方法 RATE-FT（Rationale and Auxiliary Task Enhanced Fine-Tuning）
- **核心思想**：以 Fine-Tuning 为基础，进一步引入两类提升信号：
  1. **Rationale（推理理由）增强**：在训练数据中补充对每个声明“为何正确/错误”的解释性文本。训练时采用 `label-rationale` 格式，输出第一个 token 仍是 True/False，不增加推理时的生成成本。
  2. **辅助问答（QA）任务增强**：针对每个声明生成一个与其关键信息相关的问题及正确答案。
     - 若声明为事实，答案直接提取自该声明；
     - 若声明为幻觉，则基于纠错理由构造正确回答。
     - 最终将 QA 训练样本与原声明检测样本混合，让模型同时学习“判断声明是否正确”和“回答声明中的关键信息”两个相关联的任务。
  - 作者借用了认知科学中“通过多样化背景重复巩固知识”的概念，认为辅助 QA 任务提供互补视角，增强泛化性。
- 整体流程图：对比 Fine-Tuning（仅用 claim+label）与 RATE-FT（claim+label+rationale 作为主任务，question+answer+rationale 作为辅助任务）。
- 训练完成后，检测时的指标仍用模型输出首个 token 为 True 的概率 `P_factual`，并通过对验证集进行阈值搜索来完成最终分类。

## 3. 实验设计

### 3.1 数据集 / 场景
- **LongFact**：开放域长文本生成数据集，覆盖 38 个领域。论文从中抽样 200 个 prompt，由模型生成响应，再拆分为原子声明；通过 Google Search 标注得到 2394 条事实声明和 223 条幻觉声明，随机均衡后取各 223 条用于实验（训练/验证/测试 = 70%/20%/10%）。
- **Biography（传记生成）**：来自 FActScore 的传记生成任务，用于验证跨数据集泛化性。
- **不同骨干模型**：除 Llama-3-8B-Instruct 外，还使用 Llama-3.1-70B-Instruct、Mistral-7B-Instruct、Qwen2.5-7B-Instruct，验证跨架构一致性。

### 3.2 对比方法
- 内部状态基线（概率与熵的多种聚合变体）；
- Prompt TF / Prompt Prob / SelfCheckGPT / Prompt CoT-TF；
- Probing（4 种不同嵌入类型选最优）；
- Fine-Tuning（LoRA，与 RATE-FT 同规模）；
- RATE-FT（完整版）；
- 消融变体：RATE-FT 去掉辅助任务、Fine-Tuning + paraphrase 数据增强、半量训练的 RATE-FT 等。

### 3.3 评价指标
- **Balanced Accuracy（BAcc）**，平衡考虑正负类别的准确率；
- 对于结合外部工具处理“不确定”样本的混合管线，还引入了 **BAcc-unknown** 指标。

## 4. 资源与算力

- 论文正文与附录中**未明确报告**训练所需的 GPU 型号、数量、训练时长或总体算力消耗。
- 仅可推测实验涉及：4 种不同规模的模型（7B、8B、70B），LoRA 微调（使用 LLaMA-Factory 库）、SelfCheckGPT（每组需采样 20 条响应）。具体资源开销未量化，属于论文的一种信息缺失。

## 5. 实验数量与充分性

- 实验覆盖较广，主要包括：
  - 内部状态检测实验（概率与熵的多种聚合方式，图 2-5）；
  - 两大数据集（LongFact 与 Biography）上的 4 类已有方法对比；
  - RATE-FT 与基线的整体对比（表 2）；
  - 消融实验（去除辅助任务、使用 paraphrase 的数据增强等价对照、半量训练对照）；
  - 跨模型泛化实验（Llama-3.1-70B、Mistral-7B、Qwen2.5-7B，表 4）；
  - 分布外（OOD）场景测试：在 LongFact 训练、在 Biography 上评测；
  - 引入不确定性的混合检测实验（BAcc-unknown）；
  - 提供全部评估 prompt 与实现细节。
- **充分性评价**：整体实验设计较系统，对比组设置全面，消融分析能较好隔离辅助任务的贡献与额外数据量的作用；跨数据集、跨模型、OOD 等多重验证提升了结论的可靠性。
- **客观与公平性**：
  - 使用 BAcc 而非普通准确率，考虑正负类不平衡，更公平；
  - 所有超参数和阈值都在验证集上搜索选择，避免测试集调参；
  - 构造基准时用 Google Search 生成标签，具有一定客观性；
  - 但标签由模型与搜索引擎自动生成，可能存在标注误差；
  - 在“隐藏子集”中仅采样 200 个 prompt，最终仅使用 446 条声明进行主实验（223 正/223 负），**数据规模偏小**。

## 6. 主要结论与发现

1. **内部状态不足以检测开放域长文幻觉**：模型输出概率和熵在区分长文本中的事实/幻觉声明时，效果不优于随机猜测。
2. **Fine-Tuning 是目前最有效的现有方法**：优于 Prompting 与 Probing；但即使 Fine-Tuning，绝对准确率仍有较大的提升空间。
3. **引入 CoT 理由能够提高检测效果**：从 Prompt TF 的 69.9% 提升到 Prompt CoT-TF 的 74.9%。
4. **RATE-FT 显著优于通用 Fine-Tuning**：在 LongFact 上达到 79.6%（较 Fine-Tuning 提升 +3.5 个百分点），在 Biography 上达到 80.9%。
5. **各组件均有效**：去掉辅助任务后性能下降（LongFact：79.6→77.5），说明辅助 QA 任务与理由增强各有贡献。
6. **提升来自任务设计而非简单数据扩充**：使用 paraphrase 扩充数据（Fine-Tuning para）效果只有 76.8%，低于 RATE-FT；半量 RATE-FT 仍有 78.5%，优于全量 Fine-Tuning。
7. **方法可跨模型、跨数据集泛化**：在 70B、7B 等多模型上均能取得一致增益。
8. **结合不确定性判断可以在“不确定”子集上进一步提升性能**：未见明确绝对的提示，但附录中的混合管线在五分类融合时可使 BAcc-unknown 达到 85.0%（RATE-FT 最佳）。

## 7. 优点

- **首个系统性研究**开放域长文本中“无参考”幻觉检测的工作，切入角度新颖。
- **方法简单而有效**：RATE-FT 不需要额外的外部工具，仅通过构造辅助任务和理由增强来改进 Fine-Tuning，具备轻量化、可复用的特点。
- **训练与推理解耦**：RATE-FT 在训练时加入 CoT 式理由，但推理时仍只依赖第一个输出 token 的 True/False 概率，检测成本与普通 Fine-Tuning 一致。
- **消融设计科学**：设计了多种对照（去辅助任务、数据扩充等价化、半量训练等），清楚证明收益来自“任务多样性”而非“数据量增大”。
- **实验验证全面**：覆盖两个数据集、四种模型（7B/8B/70B），包含 OOD 与混合管线分析，且公开所有 prompt，便于复现。
- **指标选择合理**：使用 BAcc，有效避免类别不平衡带来的评估偏差。

## 8. 不足与局限

- **基准数据规模有限**：仅基于 200 个 prompt 且过滤后每组类别各 223 条声明，训练与测试规模都较小；虽然 LongFact 本身覆盖 38 个领域，但对长文本理解的多样性仍有不足。
- **标签依赖大型生成工具与搜索引擎**：数据标注过程中使用模型自身拆分声明和生成搜索查询，再依赖 Google Search 结果进行“客观”验证。这种由模型参与的自举流程可能引入系统性偏差。
- **未报告推理/训练成本**：没有给出 GPU 数量、运行时间等具体资源数据，削弱了实用性评估。
- **仅关注“检测”而非“缓解”**：作者承认未将检测结果用于指导生成，限制了实际应用闭环。
- **外部依赖假设**：尽管称为无参考检测，RATE-FT 的训练优化严格依赖于训练时用外部工具生成的标签；真正的“完全无外部依赖”仅在推理阶段成立。
- **辅助任务构造依赖主模型自身**：对幻觉声明生成“正确回答”仍需模型与搜索引擎辅助，构造过程可能存在噪声。
- **未深入探讨错误模式**：未分析 RATE-FT 在哪些主题/语言/声明形态上仍容易误判，泛化边界不够清晰。

（完）
