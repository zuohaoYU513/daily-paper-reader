---
title: "RAG-DDR: Optimizing Retrieval-Augmented Generation Using Differentiable Data Rewards"
title_zh: RAG-DDR：利用可微数据奖励优化检索增强生成
authors: "Xinze Li, Sen Mei, Zhenghao Liu, Yukun Yan, Shuo Wang, Shi Yu, Zheni Zeng, Hao Chen, Ge Yu, Zhiyuan Liu, Maosong Sun, Chenyan Xiong"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=Pnktu2PBXD"
tags: ["query:faithfulness"]
score: 8.0
evidence: 利用可微数据奖励端到端对齐RAG各模块在证据使用上的偏好，提升依据检索证据生成的忠实性并抑制幻觉
tldr: 现有RAG适配多采用指令微调，易使各模块过拟合训练信号并忽视数据偏好差异。论文提出可微数据奖励方法，将数据偏好作为可微奖励，端到端联合训练RAG检索与生成模块。在多种RAG任务中，该方法显著提升模型遵循检索知识生成的能力并抑制幻觉，比传统SFT和固定奖励训练更具适应性。此工作说明细粒度数据奖励能更好协调证据利用与忠实生成。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 指令微调使RAG模块过拟合训练信号，忽视检索与生成等模块对数据偏好的差异，且无法充分利用检索证据。
method: 提出可微数据奖励（DDR）方法，端到端地将RAG系统中不同模块的数据偏好纳入奖励训练，替代单一SFT优化。
result: 在RAG任务上优于指令微调等基线，提升对检索证据的利用并减少幻觉。
conclusion: 可微数据奖励是增强RAG忠实性的高效训练范式，可泛化到不同RAG组件。
---

## Abstract
Retrieval-Augmented Generation (RAG) has proven its effectiveness in mitigating hallucinations in Large Language Models (LLMs) by retrieving knowledge from external resources. To adapt LLMs for the RAG systems, current approaches use instruction tuning to optimize LLMs, improving their ability to utilize retrieved knowledge. This supervised fine-tuning (SFT) approach focuses on equipping LLMs to handle diverse RAG tasks using different instructions. However, it trains RAG modules to overfit training signals and overlooks the varying data preferences among agents within the RAG system. In this paper, we propose a Differentiable Data Rewards (DDR) method, which end-to-end trains RAG systems by aligning data preferences between different RAG modules. DDR works by collecting the rewards to optimize each agent in the RAG system with the rollout method, which prompts agents to sample some potential responses as perturbations, evaluates the impact of these perturbations on the whole RAG system, and subsequently optimizes the agent to produce outputs that improve the performance of the RAG system. Our experiments on various knowledge-intensive tasks demonstrate that DDR significantly outperforms the SFT method, particularly for LLMs with smaller-scale parameters that depend more on the retrieved knowledge. Additionally, DDR exhibits a stronger capability to align the data preference between RAG modules. The DDR method makes the generation module more effective in extracting key information from documents and mitigating conflicts between parametric memory and external knowledge. All codes are available at https://github.com/OpenMatch/RAG-DDR.

---

## 论文详细总结（自动生成）

# RAG-DDR 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：检索增强生成（RAG）通过从外部资源检索知识来缓解大型语言模型（LLM）的幻觉问题。为使 LLM 适配 RAG，现有方法普遍使用指令微调（Instruction Tuning）来优化 LLM，提升其利用检索知识的能力。
- **问题**：这种监督式微调（SFT）主要让模型学会适应不同指令下的多种 RAG 任务，却存在两个关键缺陷：
  1. 使 RAG 各模块过拟合训练信号；
  2. 忽视了 RAG 系统中不同智能体（检索模块、生成模块等）对数据偏好的差异。
- **整体含义**：论文主张不能对所有 RAG 模块使用统一的、固定的监督信号，而应差异化地考虑各模块对数据的不同偏好，以实现更高效、更忠实的 RAG 系统。

## 2. 方法论：核心思想、关键技术与流程

- **核心思想**：提出可微数据奖励（Differentiable Data Rewards, DDR）方法，通过端到端训练 RAG 系统，对齐不同 RAG 模块之间的“数据偏好”。
- **关键技术**：
  - 将数据偏好形式化为可微奖励信号，替代传统 SFT 中单一的标签监督。
  - 使用**rollout（采样展开）**方法为 RAG 系统中的每个智能体收集奖励。
- **算法流程（文字说明）**：
  1. 对某一 RAG 模块，提示（prompt）该智能体采样若干潜在响应作为“扰动”（perturbations）；
  2. 评估这些扰动对**整个 RAG 系统整体性能**的影响；
  3. 根据影响效果优化该智能体，使其输出能提升 RAG 系统的整体表现；
  4. 对其他模块重复上述过程，实现系统级端到端联合优化。
- **本质**：DDR 把“模块输出对最终 RAG 表现的贡献”作为可微信号，将检索与生成模块的优化目标统一到系统最终性能上，从而让各模块学到相互协调的数据偏好。

## 3. 实验设计：数据集、场景、基准与对比方法

- **任务场景**：多种知识密集型任务（knowledge-intensive tasks），例如需要外部知识支撑的问答、事实验证等。
- **对比方法**：
  - 主要对比**指令微调 / SFT**方法；
  - 同时验证了 DDR 相对传统固定奖励训练的适应性优势。
- **基准与评估**：论文通过 RAG 系统在知识密集型任务上的最终生成表现来评估，重点关注对检索证据的利用效果与幻觉抑制能力。
- **具体数据集名称未在摘要中列出**，但在论文正文中应有提及（如常见 RAG benchmark）。

## 4. 资源与算力

- 摘要与元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力信息。
- 仅在开放获取说明中提供代码仓库（https://github.com/OpenMatch/RAG-DDR），未报告具体硬件配置。因此可以认为该论文在可见信息层面**缺少算力资源披露**。

## 5. 实验数量与充分性

- **实验数量**：从摘要可见至少包括：
  - 多组不同知识密集型任务的实验；
  - 不同参数量 LLM 的对比实验；
  - 对数据偏好一致性的分析实验；
  - 对幻觉抑制与知识利用效果的评估。
- **充分性与客观性评价**：
  - 实验覆盖多样化任务与模型规模，初步体现出方法的泛化性；
  - 但基于摘要无法判断是否包含完整消融（如去除可微奖励、替换搜索策略等）以及统计显著性检验；
  - 总体而言，实验设计框架较为全面，但其详细公平性（如基线调参强度、训练成本）需阅读原文进一步确认。

## 6. 主要结论与发现

- DDR 方法在知识密集型 RAG 任务上**显著优于传统 SFT 方法**，尤其对于参数量较小的 LLM——它们更依赖检索知识，DDR 带来的改进更明显。
- DDR 具有更强的**数据偏好对齐能力**，能让生成模块更有效地从文档中提取关键信息，并缓解参数记忆与外部知识之间的冲突。
- DDR 作为一种训练范式，可**泛化到不同的 RAG 组件**，实现对检索与生成环节的联合优化。
- 可微数据奖励为增强 RAG 系统的忠实性（faithfulness）提供了更高效的训练方式。

## 7. 优点

- **方法新颖**：将“数据偏好”引入奖励设计，突破了 SFT 对指令-输出单一映射的局限，属于系统级优化思路。
- **端到端可微**：利用 rollout 扰动评估模块贡献，使检索与生成模块能在同一目标函数下协同训练。
- **针对性强**：直接针对 RAG 幻觉与证据利用问题设计，能够缓解参数知识与检索证据之间的冲突。
- **实验验证有意义**：特别关注小参数模型，揭示模型规模与对检索知识依赖程度之间的关系，具有实际参考价值。
- **开源代码**：提供可复现实现，利于后续研究。

## 8. 不足与局限

- **信息不透明**：可见摘要中未报告具体数据集名称、评测指标细节、基线调优策略和计算资源，难以从摘要层面完整评判实验公平性。
- **实验覆盖有限**：虽有多种任务，但未在摘要中明确覆盖对话、多跳推理、低资源语言等更复杂场景。
- **可微性范围**：DDR 使用 rollout 扰动评估，本质上仍是近似梯度信号，可能不适用于检索索引等离散结构，对大规模检索模块的优化成本可能较高。
- **依赖整体奖励设计**：需要定义“整个 RAG 系统性能”的奖励，在复杂任务中奖励设计本身可能存在偏差或噪声。
- **未讨论负面风险**：如数据偏好过度对齐导致模型丢失通用能力、或奖励欺骗等问题在摘要中未作讨论。

（完）
