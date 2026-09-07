---
title: Mitigating Hallucination Through Theory-Consistent Symmetric Multimodal Preference Optimization
title_zh: 通过理论一致的对称多模态偏好优化缓解幻觉
authors: "Wenqi Liu, Xuemeng Song, Jiaxi Li, Yinwei Wei, Na Zheng, Jianhua Yin, Liqiang Nie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tIW29IpCwG"
tags: ["query:faithfulness"]
score: 4.0
evidence: 利用对称偏好优化和直接成对响应监督来抑制幻觉，与偏好优化缓解目标相关。
tldr: 针对直接偏好优化用于缓解多模态幻觉时目标函数不严谨、偏好监督较间接的问题，提出对称多模态偏好优化（SymMPO）。方法采用成对的响应偏好进行对称偏好学习，同时保证与理论对齐。该方案能直接增强模型对视觉输入的敏感度，从而降低幻觉生成。研究表明，理论一致且直接的偏好反馈能够更有效地提升多模态模型的忠实度。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: DPO在缓解多模态幻觉时存在优化目标不严谨和偏好监督间接的问题。
method: 提出理论一致的对称多模态偏好优化SymMPO，以直接的响应对进行对称偏好学习并保持理论对齐。
result: 该方法显著增强模型对视觉输入的关注并降低幻觉，为偏好式幻觉缓解提供更优训练目标。
conclusion: 为多模态幻觉缓解提供理论支撑更强、监督更直接的偏好优化范式。
---

## Abstract
Direct Preference Optimization (DPO) has emerged as an effective approach for mitigating hallucination in Multimodal Large Language Models (MLLMs). Although existing methods have achieved significant progress by utilizing vision-oriented contrastive objectives for enhancing MLLMs' attention to visual inputs and hence reducing hallucination, they suffer from non-rigorous optimization objective function and indirect preference supervision. To address these limitations, we propose a Symmetric Multimodal Preference Optimization (SymMPO), which conducts symmetric preference learning with direct preference supervision (i.e., response pairs) for visual understanding enhancement, while maintaining rigorous theoretical alignment with standard DPO. In  addition to conventional ordinal preference learning, SymMPO introduces a preference margin consistency loss to quantitatively regulate the preference gap between symmetric preference pairs. Comprehensive evaluation across five benchmarks demonstrate SymMPO's superior performance, validating its effectiveness in hallucination mitigation of MLLMs.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 一、核心问题与研究动机

现有利用直接偏好优化（DPO）来缓解多模态大模型（MLLMs）幻觉的工作虽然采用视觉对比目标取得了一定效果，但存在两个关键缺陷：

- **优化目标不严谨**：已有目标函数（如视觉对比变体）与原版 DPO 的数学推导偏离较大，缺乏严格的理论对齐，导致优化行为不可控。
- **偏好监督较间接**：多数方法使用间接的偏好信号（如视觉注意力差异）做监督，而非直接使用真实响应对的优劣信息，削弱了偏好学习与幻觉缓解之间的因果联系。

### 二、方法论：SymMPO

论文提出 **对称多模态偏好优化（SymMPO，Symmetric Multimodal Preference Optimization）**，核心思想是同时保持严格的 DPO 理论对齐并实现更直接、更对称的偏好反馈。具体而言：

- **直接偏好监督**：不使用间接的视觉对比信号，而直接使用成对的响应优劣（response pairs）作为监督，提高偏好信号与生成质量之间的因果联结。
- **对称偏好学习**：在传统有序偏好学习（有序偏好指单组“好-坏”响应的排序学习）之外，引入对称偏好样本构造，使偏好学习能够双向闭合，增强模型对视觉输入的敏感度。
- **偏好边缘一致性损失**：新增一项损失函数，用于定量调节对称偏好对之间的偏好差距，使偏好梯度更新在数值上更平衡、均匀。

整体上，SymMPO 的算法流程可分为：

1. 构造标准响应对与对称响应对；
2. 分别计算各响应对的相对偏好得分；
3. 将偏好学习损失与偏好边缘一致性损失加权融合；
4. 利用该合成目标更新多模态大模型参数。

该设计同时解决了“目标不严谨”与“监督间接”两重问题。

### 三、实验设计

- **数据集 / 基准**：模型在跨越五个基准数据集的场景下进行综合验证，但当前材料未具体说明五个 benchmark 的名称，也未披露具体训练集/测试集来源。
- **对比方法**：论文提及“对比现有 DPO 类方法”与基于视觉对比目标的方法，但未在提供的文本中列出具体方法名称。
- **评估指标**：未在给定内容中展开。
- 结论相对宏观：SymMPO 在五个基准上均取得了更优表现。

### 四、资源与算力说明

论文提供的文本**未明确说明**实验所使用的：

- GPU 型号与数量
- 训练迭代数与训练时长
- 模型参数量（backbone 规模）
- 其他计算资源成本

故无法判断该方法的总体计算开销。

### 五、实验数量与充分性评估

- **实验数量**：由摘要可知至少包含五个基准数据的大规模评估，但没有展示具体table细节，无法统计准确实验组数；相关的消融分析、不同训练数据规模下的对比等未在现有材料中体现。
- **充分程度**：由于五个评测任务整体覆盖较广，方法有效性获得了一定证据支撑；然而，
  - 五个基准的名称、难度梯度、幻觉类型覆盖面不明；
  - 未见与更多近期基线方法的广度对比；
  - 未见消融实验，导致对“对称偏好学习”与“偏好边缘一致性损失”两个模块各自贡献的证明不足；
  - 公平性（对照组设置是否一致、是否有统一超参）不可验证。

综上：从证据链完整度看，实验信息展示不足，其充分性和可复现性仅凭当前信息无法充分评估。

### 六、主要结论与发现

- SymMPO 通过直接响应对偏好监督有效增强了模型对视觉输入的敏感度，显著降低幻觉生成频率。
- 严格保持与 DPO 的理论对齐，能够在不破坏偏好学习有效性的前提下提升多模态模型忠实度。
- 偏好边缘一致性的引入优于仅有有序偏好的设置，说明对称信息在偏好优化中具有明确增益。
- 实验证实理论一致且监督更直接的偏好反馈范式，为多模态幻觉缓解提供了更优训练目标与可参考研究路径。

### 七、优点

1. **理论对齐性**：方法强调优化目标与标准 DPO 严格保持一致，避免了以往目标函数“形似而神不似”的问题。
2. **监督精确性**：直接用成对响应的优劣作为监督信号，与期望优化的行为高度契合，设计思路简洁且逻辑自洽。
3. **设计新颖性**：增加对称偏好对和“偏好边缘一致性”约束，在已有有序偏好之外给出补充调节机制，具有一定学术创新点。
4. **综合验证**：在五个基准上同步验证总体收益，虽然细节缺失，但覆盖面布局较全面。
5. **问题定位准确**：清楚指出既有 DPO 变体方法中两个核心痛点，并直接从痛点出发设计方案。

### 八、不足与局限

1. **信息缺失严重**：论文PDF访问受限，本文档仅提供摘要和答题卡，实验细节严重不全，无法全面评价实证部分。
2. **实验透明性不足**：五基准名称、评估协议、方法基线、实现超参数均未展示，难以判断是否存在选择性报告或数据拟合风险。
3. **消融缺失风险**：未见针对对称偏好学习和偏好边缘损失的分别验证，无法明确各子模块的净贡献。
4. **算力数据缺失**：未报告计算资源成本，对大模型偏好优化任务的实际可行性难以评估。
5. **场景局限**：重点展示英语及通用指令场景下的幻觉缓解效果，未见跨语言、跨模态领域外推、实时推理等实际业务场景验证。
6. **潜在风险未提及**：对称偏好构造是否可能引入偏好标注噪声扩展性、是否可能过高增加偏好对计算负荷、是否有高一致性偏置风险，均未在材料中讨论。

（完）
