---
title: "Adaptive Hallucination Alleviation in Multimodal Large Language Models: From Strategic Data Selection to Severity-Guided Training"
title_zh: 多模态大语言模型的自适应幻觉缓解：从策略性数据选择到严重度引导训练
authors: "Yuanyi Xu, Xiangru Zhu, Sihang Jiang, Zhixu Li, Bei Yang, Xiaoxiao Xu, Yanghua Xiao, Wei Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39955/43916"
tags: ["query:hallu-rag"]
score: 5.0
evidence: 通过面向幻觉的数据采样与严重度引导训练来缓解多模态大模型幻觉，其数据与训练思路可迁移至文本幻觉场景。
tldr: 多模态大模型仍存在各种幻觉，影响实际部署；已有方法难以高效构造高质量幻觉样本并细粒度处理。本文提出面向幻觉缓解的数据采样策略，并引入幻觉严重度的定量度量，依据严重度指导训练过程。结果显示该策略能更有效地提升幻觉缓解训练效果，为多模态幻觉抑制提供了数据与训练层面的自适应方案。由于研究对象为视觉语言幻觉，与文本证据生成场景存在差异但方法具有迁移可能性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型在多种任务上表现优异但仍饱受幻觉困扰，已有方法难以高效构造高质量幻觉样本并细粒度处理。
method: 提出策略性数据采样选择更适合幻觉缓解训练的样本，并设计幻觉严重度定量度量以指导分级训练。
result: 实验显示该数据选择与严重度引导训练能显著提升幻觉缓解效果，优于此前粗粒度处理方案。
conclusion: 数据选择与严重度感知训练可提升多模态幻觉抑制的针对性，其数据侧思路对文本幻觉缓解也有借鉴价值。
---

## Abstract
Multimodal Large Language Models (MLLMs) have recently achieved strong performance across a variety of multimodal tasks. However, they still suffer from various forms of hallucination, which hinder their practical deployment. Prior approaches often struggle to efficiently construct high-quality hallucination-related samples and to process them in a fine-grained manner, resulting in limited effectiveness in hallucination alleviation. To address this issue, we propose a data sampling strategy that selects samples better suited for hallucination-oriented training, thereby enhancing training effectiveness. In addition, we introduce a quantitative method for measuring hallucination severity and assign individualized weights to training samples accordingly. Building on this, we present Hallucination-Differentiated Direct Preference Optimization (HD-DPO), a novel preference optimization framework. During fine-tuning, HD-DPO incorporates these weights into both the formulation of customized loss functions and the modulation of localized visual attention, enabling fine-grained optimization. Experimental results demonstrate that our method outperforms existing fine-tuning strategies across multiple benchmarks and generalizes well to diverse MLLM architectures, effectively reducing hallucination rates and enhancing overall model performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

多模态大语言模型（MLLMs）尽管在跨模态理解与生成任务上表现卓越，但仍普遍存在“幻觉”问题——即模型生成的响应与图像内容或客观事实相矛盾。这些幻觉以多种形式呈现（错误的物体、属性、位置、动作、数量或杂项错误），严重阻碍模型的实际落地部署。

作者指出，幻觉产生的根源在于模型在推理时过度依赖预训练文本语料中的统计先验，从而压制了真实的视觉线索。现有幻觉缓解方法（尤其是基于偏好优化的方法，如DPO）存在两大核心缺陷：

1. **数据质量问题**：并非所有收集到的样本都适合作为幻觉训练数据。许多图像场景简单、内容稳定，模型在描述时仅产生稀疏且轻微的幻觉；用这些低质量样本进行微调效率低下，效果有限。
2. **严重度未区分问题**：已有方法在训练过程中将所有幻觉样本等同处理，当轻微与严重错误获得同等关注时，模型无法集中能力修复最关键的幻觉，导致训练后仍残留顽固错误。

针对上述问题，本文提出了一套从“数据选择”到“严重度引导训练”的自适应幻觉缓解方案。

## 2. 方法论：核心思想、关键技术细节

### 2.1 总体框架

本文方法包含三个步骤：**图像选择（Image Selection）→ 文本生成与打分（Text Generation & Scoring）→ 模型训练（Model Training）**，整体流程见原文图 2。

### 2.2 第一步：图像选择（数据筛选）

**核心思想**：筛选出“不稳定”的图像样本——即那些能够诱导模型产生严重幻觉的图像，丢弃“稳定”的低价值样本。

**具体做法**：
- 对每张图像施加**高斯噪声掩码**（Gaussian mask），引入视觉不确定性，从而放大模型的固有文本偏好；
- 比较模型在原始图像与加噪图像上的响应，从**两个维度**评估样本质量：
  - **PPL 指标**：使用 MLLM 中 LLM 组件计算响应文本的困惑度。噪声注入后 PPL 显著上升，说明文本生成不稳定、依赖易变的视觉线索，容易产生幻觉。
  - **CLIP-S 指标**：衡量响应与图像之间的语义一致性。噪声注入后 CLIP-S 显著下降，表明文本—图像对齐薄弱，是幻觉的关键信号。

**综合评分公式**：

```
Score_sample = [PPL(ẏ) − PPL(y)] / PPL(y) + [CLIP-S(y, x) − CLIP-S(ẏ, x)] / CLIP-S(y, x)
```

该分数越高，表示样本越容易产生严重的、与内容相悖的幻觉。作者据此把训练集从 23k 过滤至 5k。

### 2.3 第二步：文本生成与幻觉严重度打分

**幻觉检测与分类**：将图像与模型生成的含幻觉描述送入 GPT-4V，进行句子级别的幻觉检测、分析和修正：
- 幻觉分为六类：**Object**（物体）、**Attribute**（属性）、**Position**（位置）、**Action**（动作）、**Number**（数量）、**Miscellaneous**（杂项）；
- GPT-4V 对每个被判为幻觉的句子给出推理依据（分析），并将原句最小化修改以得到正样本回应；人工评估表明检测和修正准确率达 **93.5%**。

**双重自检机制**（量化句子级严重度，分值为 w_j）：
- 第一轮：将图像和可疑幻觉句提交给 MLLM 自身，询问句中是否存在幻觉。模型能够自主识别的记为 0.5 分（轻微）；
- 第二轮：对第一轮未识别的句子，附加 GPT-4V 的分析信息再询问。此轮被识别的记为 1.0 分（中度）；
- 仍无法被识别的记为 1.5 分（严重）。
- 作者说明 0.5/1.0/1.5 的间距经过试验验证，能在“过分强调严重幻觉”与“完全忽视轻微幻觉”之间取得较优平衡。

**幻觉数量与类型得分**：句中幻觉严重度与同一句中出现的**幻觉类型数**（而非幻觉总数）正相关。单类型计 1 分，每多一种类型加 0.5 分。若句中包含“Object”类幻觉，则该得分乘以 **1.2**（α 系数），因为物体幻觉被认为是最基本的幻觉类型。

**最终句子权重** = 自检分数 × 幻觉类型数得分。样本级严重度分数通过对所有幻觉句按**token 数量加权平均**得到：

```
s = Σ(t_j · w_j) / Σ(t_j)
```

由此构造带权偏好数据集 D = {(t_i, x_i, y_i^p, y_i^d, s_i)}。

### 2.4 第三步：HD-DPO 模型训练

作者在标准 DPO 基础上实现了**显式**和**隐式**两种加权改进：

#### （1）显式改进：严重度加权损失（Explicit）

标准 DPO 损失对所有样本一视同仁。HD-DPO 将样本级严重度分数 s 直接注入 DPO 目标函数的拒绝响应项中：

```
L_HD-DPO(explicit) = −E[ log σ( β·log(π_θ(y_p)/π_ref(y_p)) − s·β·log(π_θ(y_d)/π_ref(y_d)) ) ]
```

分数越高的样本（幻觉越严重）会在优化中被赋予更大的惩罚幅度，使模型集中精力修复最顽固的幻觉。

#### （2）隐式改进：视觉注意力调节（Implicit）

- 在训练图像 x_i 前，从正样本 y_p 中提取修正后的描述句作为文本指引；
- 利用预训练的**GLIP** 模型在该图像上执行目标检测，定位与这些描述句对应的局部区域——这些区域将是模型极易产生幻觉的地方；
- 对图像编码器输出的 patches，若 patch 索引落入已检测区域 R，则将其嵌入乘以权重 s_i（其他 patch 不变）：

```
Ẽ_k = s_i·E_k  (k∈R),  或 E_k (k∉R)
```

- 通过放大关键区域的视觉嵌入，模型在后续自注意力计算中更关注高风险区域，从而强化视觉锚定、降低幻觉。

下表可概括三个步骤的贡献：

| 步骤 | 方法 | 作用 |
|------|------|------|
| 数据选择 | 噪声注入 + PPL/CLIP-S 综合评分 | 筛出易产生严重幻觉的“不稳定”样本 |
| 严重度量化 | GPT-4V 分类检测 + 双重自检 + 类型计数 | 生成句子级/样本级严重度分数 |
| 训练 | HD-DPO（显式加权损失 + 隐式视觉注意力） | 按严重度差异化优化模型 |

## 3. 实验设计

### 3.1 评测基准（Benchmarks）

| Benchmark | 任务类型 | 评测内容 |
|------------|----------|-----------|
| **AMBER** | 生成 + 判别 | 存在性、属性、关系维度的细粒度幻觉度量（无需 LLM 标注） |
| **MMHal-Bench** | 开放生成 | 96 对图像—问题，跨 8 类场景，人类增强 RLHF 对齐 |
| **CHAIR** | 自由描述 | 物体幻觉检测（CHAIR_S 句子级、CHAIR_I 实例级） |
| **HallusionBench** | 判别 | 346 张图 + 1129 对受控是非问，区分语言幻觉与视觉错觉 |
| **MMBench** | 综合 | 将自由输出转为预设选项，评估感知与推理能力（作为通用能力参照） |

### 3.2 方法与骨干模型对比

**骨干模型**：主实验用 LLaVA-1.5-7B；另验证 Qwen-VL、InstructBLIP、InternLM-XComposer2。

**对比方法**（均以 LLaVA 为基础）：
- **RLHF**（Sun et al. 2024）
- **CSR**（Zhou et al. 2024b）
- **POVID**（Zhou et al. 2024a）
- **V-DPO**（Xie et al. 2024）

**训练数据**：LLaVA-Instruct-150K 的“detail 23k”子集，经图像选择筛至 5k。

**实现细节**：2 epochs，batch size 64，学习率 2e-6，零权重衰减，LoRA rank 64，dropout 0.05，β=0.1。“仅使用描述性数据，未使用任何 QA 样例”。

## 4. 资源与算力

**论文未明确说明所用 GPU 型号、数量、训练时长等详细信息**，仅给出超参数设置（epochs、batch size、学习率、LoRA rank 等）。如需复现该研究，算力成本无法从公开文本中直接推算。

## 5. 实验数量与充分性分析

### 实验组别概览

| 实验类型 | 内容 | 覆盖情况 |
|----------|------|----------|
| 主实验（表 1） | LLaVA-1.5-7B 上与 4 种 SOTA 方法对比，覆盖 5 个 benchmark | 充分 |
| 泛化实验（表 2） | 在 3 种不同架构（Qwen-VL, InstructBLIP, InternLM-XComposer2）上验证 | 良好，但模型数量有限 |
| 消融研究（表 3） | 4 组：原始 DPO(w/o IS) → +DPO → +HD-DPO(explicit) → +HD-DPO 完整 | 有效验证了各环节贡献 |
| 类别分析（表 4） | 对 6 类幻觉类型分别用 1k 样本单独微调 | 细致 |
| 案例研究（图 4） | Object/Attribute/Position 三类各举一例 | 形象但样本量少 |

### 充分性与公平性评价

- **优点**：覆盖了多个主流的生成式和判别式幻觉基准，同时引入通用综合基准（MMBench）来监测方法是否以牺牲整体能力为代价换取幻觉指标改善，这种思路较好。消融实验逐一验证了图像选择、显式加权和隐式注意力的贡献。跨架构泛化实验增强了结论的可信度。
- **不足**：
  - 对比方法数量偏少（仅 4 种偏好优化方法），未与更多近期幻觉缓解方法对齐比较；
  - 骨干模型主实验只用 LLaVA-1.5-7B，缺少更大规模模型（如 13B/34B）上的验证；
  - 表格数据中对于显著性差异或多次运行的方差没有披露，统计可信度存疑；
  - 案例研究只有 3 个示例，呈现可能的幸存者偏差。

## 6. 主要结论与发现

1. **HD-DPO 显著优于现有微调策略**：在 MMHal-Bench 上实现 20.9% 相对提升；CHAIR 上幻觉句率降至 4.1、幻觉物体率降至 2.8；AMBER 准确率达到 79.7%、F1 为 83.2%，创当时 SOTA。
2. **仅用描述数据就改善判别任务**：模型从未见过 QA 样本，却在 HallusionBench、AMBER 等判别基准上有较大提升，说明方法从根本上增强了视觉—语义对齐而非仅拟合特定题型。
3. **跨架构普适性**：HD-DPO 在 Qwen-VL、InstructBLIP、InternLM-XComposer2 上均稳定降低各类幻觉指标，且不同初始水平的模型其增益侧重点不同。
4. **渐进式消融证实各组件有效**：图像筛选提升判别力；显式加权损失显著改善生成任务中的物体幻觉；隐式视觉注意力调节进一步降低幻觉率、提升整体得分（MMBench 上损失极其轻微）。
5. **幻觉类别影响存在层级差异**：Object、Attribute、Position 是“主要类型”，对训练影响最大；Object 幻觉的修正效果最具全局带动性。Miscellaneous、Action、Number 为“次要类型”。

## 7. 方法优点

1. **系统性数据治理思路新颖**：通过噪声注入 + PPL 与 CLIP-S 双指标联立评分来筛选“易幻觉”样本，从源头上保证偏好数据质量，逻辑清晰且不需要人工标注。
2. **细粒度严重度量化设计巧妙**：融合了外部模型（GPT-4V）检测的客观分类信息与模型自身的自我认知情况（双重自检），并考虑了幻觉类型数量与物体幻觉的特殊权重，形成了多维度的句子级度量。
3. **显式与隐式双通道加权**：不仅把严重度注入损失函数，还将权重映射至图像局部区域注意力，实现了“文本—视觉”两个模态上的差异化处理，比单纯加权的 DPO 更深入。
4. **严格保障正样本质量**：通过 GPT-4V 对原句做**最小化编辑**获得正样本，避免引入额外冗长或改写噪声对训练造成干扰。
5. **实验证明了方法的通用性**：在多模型架构上验证，不依赖特定模型结构。

## 8. 不足与局限

1. **依赖大模型标注**：整个流程严重依赖 GPT-4V 完成幻觉检测、分析和修正。这一方面带来 API 成本，另一方面训练数据质量受限于 GPT-4V 本身的判断上限（尽管人工验证达到 93.5%，但仍非理想标准）。
2. **算力与复现细节缺失**：未披露 GPU 型号与数量、训练时长或总计算量，影响研究的可复现性和资源评估。
3. **存在的性能权衡**：在 HallusionBench 上未超越 V-DPO；消融实验也发现隐式注意力重分配可能偶尔忽略相关视觉线索，导致 MMBench 轻微下降。说明该方法并非在所有任务上都严格占优。
4. **面对“难以察觉”幻觉的能力有限**：双重自检机制对自身无法感知的错误本质上赋予更重的分数——这意味着模型越是“不知道自己不知道”，训练信号越强。这在逻辑上有合理性，但对于需要对抗模型系统性盲区的场景未必足够。
5. **适用范围有限**：主要验证集中于描述与常规 VQA 任务；对于复杂多轮对话、推理链条中的幻觉，以及需要外部知识排查的幻觉场景，论文没有给出证据。
6. **统计严谨性存疑**：未见多次重复实验的标准差或显著性检验等报告，无法断言 MMHal-Bench 或 CHAIR 等指标上的优势是否统计显著。
7. **数据规模的讨论不充分**：作者将训练集从 23k 压缩至 5k，但没有系统展示“最佳数据量”曲线，也未验证该筛选逻辑在不同数量的样本下是否依然稳健。

**总体评价**：这是一篇系统性地从数据选择、严重度定量到差异化训练端到端缓解 MLLM 幻觉的高质量工作，在数据治理与细粒度偏好优化方面贡献突出；但其过度依赖 GPT-4V、缺少算力透明度与统计严谨性报告等问题，使其复现性和泛化边界仍需进一步验证。

（完）
