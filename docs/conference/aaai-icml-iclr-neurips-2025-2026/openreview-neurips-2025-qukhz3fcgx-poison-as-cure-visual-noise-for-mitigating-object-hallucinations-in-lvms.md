---
title: "Poison as Cure: Visual Noise for Mitigating Object Hallucinations in LVMs"
title_zh: 以毒攻毒：用视觉噪声缓解大视觉语言模型的目标幻觉
authors: "Kejia Zhang, Keda TAO, Jiasheng Tang, Huan Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=quKHZ3fcgx"
tags: ["query:faithfulness"]
score: 5.0
evidence: 以优化视觉噪声在输入侧抑制目标幻觉，无需改动模型权重；对无依据事实内容的输入侧缓解有方法启发
tldr: 大视觉语言模型常输出看似合理但与图像事实不符的目标幻觉。论文将幻觉抑制形式化为优化问题，生成策略性视觉对抗扰动，在不改动模型权重的情况下增强模型对视觉证据的依赖并减少参数性幻觉输出。实验表明该扰动方法在多种LVM上降低目标幻觉率，为输入侧干预模型幻觉提供了新的低成本且免训练的解决途径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LVM可能生成看似合理但不准确的物体，存在目标幻觉问题，传统缓解常需改动模型或借助外部资源。
method: 提出视觉对抗扰动方法，将幻觉抑制视为优化问题，对视觉输入施加策略性优化噪声以增强对视觉事实的锚定。
result: 无需修改基座模型即可降低目标幻觉，提升模型输出的事实基础。
conclusion: 输入端的视觉对抗扰动是缓解LVM幻觉灵活且高效的新方向。
---

## Abstract
Large vision-language models (LVMs) extend large language models (LLMs) with visual perception capabilities, enabling them to process and interpret visual information. A major challenge compromising their reliability is object hallucination that LVMs may generate plausible but factually inaccurate information. We propose a novel \textit{visual adversarial perturbation (VAP)} method to mitigate this hallucination issue. VAP alleviates LVM hallucination by applying strategically optimized visual noise without altering the base model. Our approach formulates hallucination suppression as an optimization problem, leveraging adversarial strategies to generate beneficial visual perturbations that enhance the model's factual grounding and reduce parametric knowledge bias. Extensive experimental results demonstrate that our method consistently reduces object hallucinations across 8 state-of-the-art LVMs, validating its efficacy across diverse evaluations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

目标：以毒攻毒——用视觉噪声缓解大视觉语言模型的目标幻觉。

- **大视觉语言模型（LVMs）** 结合了大型语言模型（LLMs）与视觉感知能力，使其能够处理和解释图像等视觉信息。
- **目标幻觉（Object Hallucination）** 是影响 LVM 可靠性的核心障碍，即模型生成看似合理（plausible）但事实上不准确（factually inaccurate）的内容，尤其是图像中不存在的对象。
- 传统幻觉缓解方法通常需要修改模型架构、进行模型权重微调或依赖外部知识资源，这带来了高昂的计算成本及部署不便。
- 论文的核心动机在于探索一种**免训练的、输入侧干预**的幻觉缓解路径：能否只在输入图像上做文章，用策略优化的视觉噪声来引导模型更忠于视觉证据，而非依赖参数化先验知识。
- 论文为这一目标提出了**视觉对抗扰动（Visual Adversarial Perturbation, VAP）** 方法，将“幻觉抑制”重新形式化为一个优化问题，借助对抗攻击的思想生成“良性”噪声扰动。

**整体含义**：本文提供了一种与模型无关（model-agnostic）的幻觉抑制思路——不触碰模型权重，而通过修改视觉输入来“重新锚定”模型对图像内容的感知，降低了应用门槛，开辟了输入端干预缓解 LVM 幻觉的新方向。

---

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将“幻觉抑制”视为一个优化问题——求解一个最优的视觉扰动信号，叠加到输入图像上，用于压缩模型输出对于内部参数性先验（parametric knowledge bias）的依赖，同时增强对视觉证据（visual grounding）的依赖。
- **方法名称**：视觉对抗扰动（VAP）。
- **与传统对抗攻击的区别**：传统对抗扰动追求使模型输出错误结果，VAP 是“以毒攻毒”，以对抗优化手段制造的扰动反而是正面/利于真实感知的。
- **算法流程概述**：
  1. 输入一张原始图像（会触发幻觉）作为初始状态。
  2. 将幻觉缓解目标量化为一个损失/目标函数，该函数联合考虑视觉事实与模型输出中的对象一致性。
  3. 迭代优化扰动信号（类似于梯度上升/下降），使新增视觉噪声能有效地将模型对图像中对象类别的注意力调向真实视觉内容。
  4. 将学习到的扰动叠加到原图像上，再输入到任意的、未被修改的 LVM 模型中。
  5. 模型在该图像增强输入下生成新描述，目标幻觉率显著降低。
- **提及机制**：VAP 不减损模型原有能力，也不需要额外训练基础 LVM 的权重；该方法被描述为增强模型的视觉事实锚定（factual grounding）和降低参数知识偏移（reduce parametric knowledge bias）。
- 注：论文标题是“以毒攻毒”，隐喻对抗噪声（通常视为“毒”）在这里成为“解药”。

> 由于论文正文未能完整读取，具体的损失函数形式、迭代公式与超参数细节在本次总结中无法完整重述，以上是根据摘要得到的方法层面概述。

---

## 3. 实验设计：数据集 / 场景 / benchmark / 对比方法

- 论文在摘要中指出，方法在 **8 个最先进（state-of-the-art）LVMs** 上进行了评估。
- 覆盖了多样的评估场景/configurations，验证了方法在多个权威 LVM 上均稳定降低目标幻觉率。
- 未在现有可见信息中明确具体的数据集名称或 benchmark 列表（如 MSCOCO、POPE、CHAIR 等），但在 LVM 幻觉评估领域，主流 benchmark 通常包含——指向性对象存在性评估（POPE）、Caption 幻觉率（CHAIR）、对象属性与关系幻觉评估等。
- 作为无模型修改的缓解手段，方法对比于基线时具有两个天然优势：
  - （a）无需改变任何模型内部参数
  - （b）无需外部知识库参与推理
- 给出的评估覆盖 8 个 LVMs，跨模型通用性是其重要的实验证据点。

---

## 4. 资源与算力

- **本论文提取到的元数据与摘要中没有明确说明使用的 GPU 型号、GPU 数量、训练时间或推理开销。**
- VAP 需要对图像进行一次性扰动优化；若该方法在推理时为每个测试样本单独优化噪声（per-image optimization），则需消耗额外的推理侧计算资源；若扰动模式可泛化（训练一个轻量扰动生成器），则每次推理仅多一次前向。</u>
- 由于正文缺失，当前无法给出精确的资源与算力信息；也未能评估该方法相较基线微调的额外开销。

---

## 5. 实验数量与充分性

**现有信息范围内的实验概况：**

- 实验在不同 LVMs 上进行了跨模型的广泛验证（8 个 SOTA LVMs），这是实验设计中的核心充分性体现。
- 评估覆盖了不同的评估方式/场景，但具体实验组的数量（如不同数据集的数量、消融研究数量、扰动幅度分析、与其它方法精确对比指标）在当前可见文本中缺乏细节。
- 公平性方面，摘要声明了“多种评估下均持续减少目标幻觉”，但缺少与既有最佳幻觉缓解方法（如 VCD、OPERA、LURE、Woodpecker 等）的细致数值对比说明，无法在本次总结中展开。
- 从已有信息判断：实验规模在模型数量维度很完整（8条模型线），但在“多少数据集”、“多少消融维度”上尚无法判断全面性。用户如需要更精确的实验充分性结论，需回到论文原文实验章节阅读。

---

## 6. 论文的主要结论与发现

1. **输入侧视觉对抗扰动可用于对抗 LVM 目标幻觉**：策略优化的视觉噪声能够降低模型生成不存在对象的概率。
2. **无需修改基座模型权重**：VAP 完全在输入侧工作，对历史模型权重保持零改动，成为一种即插即用的幻觉缓解工具。
3. **跨模型泛化有效**：在 8 个 SOTA LVMs 上的一致效果表明该方法不依赖于特定模型架构或参数规模。
4. **机制倾向**：效果来源于增强视觉事实锚定和减少参数化先验偏差的良性对抗学习过程——“以毒攻毒”的可实现性被实验证实。
5. 这一方法摆脱了传统对抗方法只会导致模型犯错的认知局限，将对抗扰动在可靠性方向上拓展为一个正向、通用的解释工具。

---

## 7. 优点

- **方法切入点新颖**：将对抗噪声从有害工具转化为“良药”，在输入侧寻找幻觉缓解空间，拓宽了攻击思想在可信 AI 中的应用。
- **免训练，黑盒可用**：不需要访问和更新 LVM 权重，对以 API 为核心部署形态的大型模型有现实部署价值。
- **跨架构通用**：多个 SOTA LVM 上的稳定表现表明通用性强。
- **机制意义明确**：通过修改视觉输入信号来度量模型对图像事实的依赖与对参数先验的依赖，某种程度上提供了幻觉成因的一个新的探测视角。
- **低成本与可迁移性**：对于场景迁移或模型迭代不需要重复做模型训练。
- 论文被 NeurIPS-2025 接收，标志着这一方向的学术认可度较高。

---

## 8. 不足与局限

- **计算开销与部署效率不明朗**：输入侧逐样本优化扰动是否会造成推理时明显延迟，在摘要中不可见；如果不能训练泛化式的扰动生成器，实时应用场景受限。
- **评估细节覆盖不足**：由于仅有高层次实验展示，无法评断评测集中对“对象存在性”之外的方面（如位置幻觉、属性混淆、多对象关系幻觉）的覆盖。
- **偏差风险**：视觉对抗扰动可能对图像质量/语义引入新的噪声偏差，或会改变低层图像统计性质，使其在部分安全敏感场景（如医学影像、自动驾驶）中应用受限。
- **工程适用性存疑**：图像如有缩放、裁剪、压缩变换，优化出的扰动是否保持鲁棒是一个现实问题。论文未能展示对抗扰动的物理世界鲁棒性情形。
- **对比强度未能评估**：论文当前可见信息缺乏与最近基于解码策略、注意力修正等方法（如 VCD、OPERA）的比较结果，难以认定其效果在整体 SOTA 上处于绝对领先。
- **正文细节不可获取**：本次分析源于摘要提取文本，缺乏论文中公式、算法伪码、完整消融图的深度参考，以上一些局限性判断基于常规推理并按实际情况进行了标注。

---

（完）
