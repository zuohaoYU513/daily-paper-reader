---
title: "Investigating Factuality in Long-Form Text Generation: The Roles of Self-Known and Self-Unknown"
title_zh: 探究长文本生成中的事实性：自知与未知的作用
authors: "Lifu Tu, Rui Meng, Shafiq Joty, Yingbo Zhou, Semih Yavuz"
date: 2024-09-27
pdf: "https://openreview.net/pdf?id=qLxkXgmWwx"
tags: ["query:faithfulness"]
score: 8.0
evidence: 检测长文本生成中无支撑论断并评估自我判断设置
tldr: 该研究分析GPT-4、Llama-3等模型长文本生成中的事实性，发现生成后半部分事实分数下降、无支撑论断增多；并进一步探究不同评估设置下模型能否准确判断自身输出的正确性。研究为长文本生成的可信度评估与自我修正提供了实证基础。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 长文本生成中模型常混合真假信息，需要通过系统分析揭示事实性下降规律并评估模型的自我判断能力。
method: 对多个大模型的长文档输出做分句事实性评分和无支撑论断计数，并比较多种评估设置下模型自我判断的准确率。
result: 发现事实分数随文本推进明显下降，无支撑论断增加，且模型的自我判断受评估环境影响。
conclusion: 长文本事实性退化可量化，改进自我评估协议有助于自动识别和纠正无依据内容。
---

## Abstract
Large language models (LLMs) have demonstrated strong capabilities in text understanding and generation. However, they often lack factuality, producing a mixture of true and false information, especially in long-form generation. In this work, we investigates the factuality of long-form text generation across various large language models (LLMs), including GPT-4, Gemini-1.5-Pro, Claude-3-Opus, Llama-3-70B, and Mistral. Our analysis reveals that factuality scores tend to decline in later sentences of the generated text, accompanied by a rise in the number of unsupported claims.
Furthermore, we explore the effectiveness of different evaluation settings to assess whether LLMs can accurately judge the correctness of their own outputs: Self-Known (the percentage of supported atomic claims, decomposed from LLM outputs, that the corresponding LLMs judge as correct) and Self-Unknown (the percentage of unsupported atomic claims that the corresponding LLMs judge as incorrect). The results indicate that even advanced models like GPT-4 and Gemini-1.5-Pro fail to achieve perfect Self-Known scores, while their Self-Unknown scores remain notably above zero, reflecting ongoing uncertainty in their self-assessments.
Moreover, we find a correlation between higher Self-Known scores and improved factuality, while higher Self-Unknown scores are associated with lower factuality. Interestingly, even without significant changes in the models' self-judgment (Self-Known and Self-Unknown), the number of unsupported claims can increases, likely as an artifact of long-form generation. These findings show the limitations of current LLMs in long-form generation, and provide valuable insights for improving factuality in long-form text generation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：尽管大型语言模型（LLMs）在文本理解与生成上展现出强大能力，但在长文本生成中常常难以保持事实性，会输出真假信息混杂的内容，这一问题在长文场景中尤为突出。
- **研究动机**：需要对长文本生成中的事实性退化现象进行系统性的量化分析，并进一步探究模型能否准确判断自身输出中哪些内容是可信的、哪些是不可信的——即模型对“自知”（self-known）与“未知”（self-unknown）的感知能力。
- **核心问题**：长文本生成中事实性如何随生成进程变化？不同规模的模型能否可靠地识别自身输出中的无支撑论断？自我判断能力与事实性之间存在怎样的关联？
- **整体含义**：本研究为长文本生成的可信度评估提供了实证依据，揭示了现有模型的自我判断局限，并为未来设计更好的自我修正与事实性增强机制提供了方向。

### 2. 方法论

- **核心思想**：将长文本生成输出拆分为原子论断（atomic claims），逐条评估其是否可被外部知识支撑（grounding），从而量化事实性；再比较不同评估设置下模型对自身输出的判断能力，区分“自知”（能识别正确的断言）与“自未知”（能识别错误/无支撑的断言）。
  
- **关键技术细节**：
  - 对多个LLM的长文档输出进行**分句（逐句子）事实性评分**，观察事实分数在生成文本中的分布与变化趋势。
  - 对生成内容进行**无支撑论断（unsupported claims）计数**，并统计其随生成进程的演变。
  - 定义两个核心指标：
    - **Self-Known**：从LLM输出中分解出的、被事实核查支撑的原子论断中，该LLM自身判断为“正确”的比例。
    - **Self-Unknown**：不被支撑的原子论断中，该LLM自身判断为“错误”的比例（即模型能识别出自己错误的能力）。
  - 分析这些自我评估指标与整体事实性之间的相关性，并考察在生成文本不同位置（如前半部分 vs. 后半部分）的变化情况。

- **评估方式说明**（基于摘要推断）：评估设置涉及对模型输出做原子论断分解，可能结合外部知识或检索证据进行支撑性判断，并让模型自身在多种提示或评估协议下做出“正确/错误”的判断。

### 3. 实验设计

- **评估模型**：覆盖多种主流先进LLM，包括：
  - GPT-4
  - Gemini-1.5-Pro
  - Claude-3-Opus
  - Llama-3-70B
  - Mistral
- **数据集/场景**：论文提取内容中未明确给出具体的下游任务数据集名称或benchmark，但从摘要推断是泛指长文本生成（long-form generation）任务，可能涵盖开放性生成、摘要类或知识密集型任务，需要长篇幅输出。提取内容未交代具体评测数据规模与领域构成。
- **对比方法**：该研究**并非以某一特定基线方法为主要对比对象**，而是以多个模型间的横向比较为核心；主要对比各模型的：
  - 事实性得分（有支撑论断的比例）
  - 无支撑论断数量
  - Self-Known 与 Self-Unknown 值
  - 不同自我判断评估设置下模型的表现差异。
- **实验性质**：属于实证分析型研究（evaluation study），并非提出新型生成方法并与之对比，而是通过可复现的评测协议揭示现象与规律。

### 4. 资源与算力

- **提取内容中未详细说明**使用的GPU型号、数量、训练时间或推理成本等算力资源。
- 仅能推断该项研究涉及多次调用商用API（GPT-4、Gemini-1.5-Pro、Claude-3-Opus等）以及本地部署模型（如Llama-3-70B），每一步都要完成长文本生成与细粒度的事实性评估，推理开销可观。
- 由于论文文本未提供算力清单，无法给出更精确的资源描述。

### 5. 实验数量与充分性

- **模型覆盖面较广**：5种主流LLM，涵盖商用闭源与开源模型，具有较好的代表性。
- **实验设置较为多元**：涉及不同自我评估协议/环境的比较，并同时使用事实性评分、无支撑论断计数、Self-Known与Self-Unknown等多个相关性维度。
- **未说明的内容**：
  - 测试样本量（生成了多少条长文本、每个模型各多少条）；
  - 是否做了多轮采样、随机性控制；
  - 是否有跨领域（如新闻、学术、对话等）的覆盖；
  - 消融实验（如去掉不同评估组件）等信息未被提取文本提及。
- **总体评价**：从摘要可以看出实验设计有较强的问题针对性，多模型+多维指标能在一定程度上支撑主要结论；然而由于未披露样本规模与任务类别，实验充分性客观上难以完全评估，尤其是缺少对“不同任务类型/提示设置对事实性退化影响”讨论的可能性，其客观性与公平性有待正文里更多细节支撑。

### 6. 主要结论与发现

- **事实性随生成进程退化**：在生成的长文本中，越靠后的句子其事实性得分往往越低，呈现出明显的下降趋势。
- **无支撑论断递增**：随着文本长度增加，无支撑论断（unsupported claims）数量也随之上升。
- **自我判断并不完美**：即使如GPT-4、Gemini-1.5-Pro等先进模型，也无法达到完美的Self-Known水平（不能完全辨识自身输出中所有正确内容），同时它们的Self-Unknown值显著不为零（始终存在一些模型本应能意识到但有未纠正的错误）。
- **自我判断与事实性的相关性**：
  - Self-Known 越高 → 生成事实性整体越好；
  - Self-Unknown 越高 → 生成事实性越差。
- **长文本生成中的特殊现象**：即便在模型的自我判断能力（Self-Known 和 Self-Unknown）没有显著改变的情况下，无支撑claim数仍可能上升，说明这可能是长文本生成自身带来的伪影/退化现象，而非模型判断力下降所致。
- **总体启示**：当前LLM在长文本生成中事实性有限，单纯依赖其自我判断来识别错误是不够的，需要设计更好的评估和自我纠正协议以降低无依据内容的产生。

### 7. 优点

- **问题选取具有现实重要性**：针对长文本生成事实性系统退化这一关键短板，直接回应LLM可信落地的核心挑战。
- **提出具有区分度的新指标**：将模型自我认知拆分为Self-Known与Self-Unknown两个维度，能更清晰揭示模型“知道什么”和“不知道什么”，优于笼统的置信度评估。
- **多模型覆盖、结论更具普适性**：同时考察闭源（GPT-4、Gemini、Claude）和开源（Llama-3-70B、Mistral）模型，揭示了该问题是系统性的而并非某一家模型特有。
- **发现区分“判断能力下降”与“生成退化”两个因素**：通过区分模型自我判断变化与无支撑claim数量变化，指出长文本生成退化可能独立于判断能力，这一观察对后续研究很有方法论参考价值。
- **相关性分析为后续建模提供线索**：将Self-Known/Self-Unknown与事实性建立量化关联，可以直接启发自我修正系统的设计。

### 8. 不足与局限

- **缺乏对任务多样性的覆盖**：提取文本未标明具体数据集，难以判断结论是否在摘要、问答、报告写作等不同长文本任务上均成立。
- **评估规模未披露**：未交代样本数、提示词设置、生成长度范围、多次采样等执行细节，可复现性受限。
- **事实性评估本身存在挑战**：对“原子论断”的分解与外部证据支撑的判断都依赖额外模型或数据源，其自身可能存在偏差，摘要中没有对这些评估方法的可靠性展开误差分析。
- **自我判断设置的定义与边界**：Self-Known/Self-Unknown中的“对应LLM判断”依赖特定提示和评估协议，评估环境对结果的影响较大，论文的抽象中并未说明哪种设置最优，也未给出协议的标准化建议。
- **计算资源说明缺失**：未报告API调用规模或本地模型的推理资源成本，限制了对方法的成本可适性的判断。
- **缺乏干预实验**：该研究偏重观测与分析，并未验证所提方案（如利用Self-Unknown进行自我纠正）是否真的能改善事实性，应用价值有待进一步检验。

（完）
