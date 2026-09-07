---
title: "Benford’s Curse: Tracing Digit Bias to Numerical Hallucination in LLMs"
title_zh: 本福特定律的诅咒：追踪数字偏差到大语言模型的数值幻觉
authors: "Jiandong Shao, Yao Lu, Jianfei Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AOe1aUhEQQ"
tags: ["query:faithfulness"]
score: 8.0
evidence: 大语言模型数值幻觉与预训练语料数字偏差相关
tldr: 针对大语言模型在数值问题上频繁产生幻觉的问题，论文依据本福特定律提出预训练语料中前导数字分布偏斜诱发数字生成偏差的假设。作者检验开源预训练语料的数字频率，并构造真实数字均匀分布的七类数值推理评测集，验证了数字偏差显著存在。研究首次把语料层面的数字先验与数值幻觉联系起来，为数值幻觉评测与缓解提供了新的方向。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 大语言模型在复杂推理任务上表现出色，却在基础数值问题上经常输出错误结果，本文推测这与预训练语料中前导数字分布不均匀有关。
method: 提出数字偏差导致数值幻觉的假设，并建立真实数字在七项数值推理任务中均匀分布的评测基准来检测模型生成偏差。
result: 评测结果表明大语言模型的数字输出系统性偏向预训练语料中常见数字，验证了语料数字先验对数值幻觉的成因作用。
conclusion: 预训练语料的统计偏差而非单纯推理能力不足是数值幻觉的重要来源，为数值事实的评测与校准提供了理论依据。
---

## Abstract
Large Language Models (LLMs) exhibit impressive performance on complex reasoning tasks, yet they frequently fail on basic numerical problems, producing incorrect outputs. Inspired by Benford’s Law, a statistical pattern in which lower digits occur more frequently as leading digits, we hypothesize that the skewed digit distributions in web-collected corpora may be learned by LLMs during pretraining, leading to biased numerical generation. To investigate the hypothesis, we first examine whether digits frequencies in pretraining corpus (OLMo2) follows Benford's law. We then construct an evaluation benchmark in which the ground-truth digits are uniformly distributed within each of the seven numerical reasoning tasks. Our evaluation results demonstrate that leading open-source LLMs show a consistent pattern of digit bias that resembles Benford's law. Through logit-lens tracing and neuron-level dissection, we identify that this bias arises predominantly from a small subset of highly digit-selective feed-forward network (FFN) neurons in the deeper layers. Finally, we demonstrate that pruning these neurons mitigates imbalanced overgeneration and partially corrects erroneous outputs, providing causal evidence that fine-grained pretraining digit bias can propagate into model behavior. Our findings reveal a fundamental connection between corpus-level statistics and symbolic failure modes in LLMs, offering a new lens for diagnosing and mitigating hallucinations in numerical tasks.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大语言模型（LLMs）在复杂推理任务中表现出色，却在基本的数值问题（如数值比较、简单运算等）上经常出错，产生与事实不符的输出。
- **现象观察**：论文从本福特定律（Benford's Law）获得灵感——该定律指出自然数据中前导数字的分布并不均匀，较小的数字（如1、2）出现频率更高。
- **核心猜测**：网络抓取的大规模预训练语料中存在数字分布偏斜，LLM 在预训练过程中学到了这种统计先验，导致其数值生成也呈现出类似的偏置倾向，从而产生数值幻觉。
- **整体含义**：该研究将语料层面的统计偏差与模型的符号失败模式联系起来，为理解数值幻觉提出了一个重要来源——未必只是推理能力不足，也可能是预训练数据的数字分布不均衡所致。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：验证语料先验→检测输出偏差→定位神经机制→因果验证，形成"统计假设—行为验证—机制归因—因果干预"的完整闭环。
- **第一步——语料检查**：检验开源预训练语料（OLMo2）中各前导数字的出现频率是否符合本福特定律。
- **第二步——评测基准构建**：构建七个数值推理任务的评测集，关键设计在于让每个任务中正确答案的数字分布严格均匀，从而排除真实答案本身分布不均衡的干扰——若模型仍表现出偏斜输出，即可归因于内在生成偏置而非任务本身要求。
- **第三步——机制归因**：利用 logit-lens 技术逐层追踪模型内部表示中的数字倾向，并通过神经元层面的解剖分析，定位产生数字偏好信号的具体结构。
- **第四步——因果验证**：通过剪除识别出的高数字选择性前馈网络（FFN）神经元，观察是否能缓解失衡的数字生成并纠正部分错误输出——若有效，则提供了偏置影响行为的直接因果证据。

### 3. 实验设计：使用了哪些数据集 / 场景 / Benchmark / 对比方法

- **预训练语料分析对象**：OLMo2 开源语料集——统计前导数字的实际频率分布，检验其与本福特定律的拟合程度。
- **评测基准（Benchmark）**：作者自行构建的包含七类数值推理任务的评测集。这七类任务的覆盖场景从摘要来看未完全列出，总体为要求模型输出确定性数值答案的符号推理问题。评测集的关键特点是所有任务的真实数字均统一分布。
- **评测的模型**：多个领先的开源 LLM（如 OLMo2 系列等在摘要范围内提及）。对比方式为：将模型输出数字的频率分布与（a）预训练语料分布、（b）本福特定律理论分布、（c）作为对照的答案均匀分布进行对比，以此判断偏置的存在与方向。
- **消融/干预实验**：针对识别出的高选择性神经元进行剪除，对比剪除前后的输出分布与准确率变化。

### 4. 资源与算力

- 论文摘要和提供的元数据中**未明确说明**具体的算力资源（如 GPU 型号、数量、训练时长、预处理耗时等）。
- 由于涉及的实验主要是四类：语料统计（消耗少量）、模型推理评测（若干开源模型、可复现）、logit-lens 追踪与神经元剪枝等，推测计算量没有超出学术实验室的可承受范围，但这一推测需要原始论文确认，不能作为事实。

### 5. 实验数量与充分性

- **实验组数概览**：
  - 七个数值推理任务的基准评测（模型输出分布分析）；
  - 语料层面前导数字统计（检验是否符合本福特定律）；
  - logit-lens 分层追踪实验（跨层内部表征分析）；
  - 神经元剪枝因果干预实验（消融性验证）。
- **充分性与客观性分析**：
  - 基准设计思路巧妙（保证真实分布均匀以隔离语料先验），实验能从关联到因果形成闭环，逻辑严密；
  - 覆盖面和公平性方面存在较大优化空间——目前论文只检验了语料与偏置的关联性，评测任务以数值推理为主，尚不清楚是否推广到更广泛的事实问答或需多位数字的场景；只用少数几个开源模型是否足以说明所有 LLM 尚有局限，若加入商业闭源模型或更多尺度模型（小/中/大/超大参数）进行对比，结论会更有说服力；
  - 在论文评审中获得 8.0 的评分与 NeurIPS-2025 录用，说明整体方法设计和实验逻辑具有较高可信度，细节补充需要结合全部附录来佐证。

### 6. 论文的主要结论与发现

- **现象层面**：评测结果证明领先的开源 LLM 在数值输出上表现出系统性的前导数字偏置，这种偏置的模式与本福特定律所刻画的方向一致（偏好小数字）。
- **归因层面**：这种偏置在机制上主要源于深度网络层中数量很小的一部分高数字选择性 FFN 神经元，即语料统计信息被编码在特定的神经元子集中。
- **因果层面**：通过剪除掉这些神经元，模型过度的数字失衡生成自然恢复，错误输出部分得到纠正——这证明预训练语料的细粒度数字偏差确实可以由"语料内的统计特征"逐步传导为客户可见的行为性幻觉。
- **总体判断**：数值幻觉的重要来源是预训练语料的统计偏差，而非单纯的推理能力不足——该结论为此类幻觉的评测与校准提供了理论依据与干预方向。

### 7. 优点总结

- 设计严谨且具有"归因—验证"的完备逻辑，将统计规律（本福特定律）转化为面向 LLM 的可检测偏置假设，实践路径清晰；
- 评测基准刻意将正确答案的数字构造为均匀分布，剔除了"回答分布本身反映地面真实分布"的混淆因素，对比实验方法非常干净；
- 跳出纯行为学分析的范畴，联合 logit-lens 与神经元级剪枝实现从行为到机制再到干预的闭环，提供了因果性验证——这在数值幻觉类论文中比较少有；
- 概念点题巧妙，将本福特定律的"诅咒"与幻觉问题结合，为语料学视角下的大模型可解释性和幻觉缓解赋予了新的方向。

### 8. 不足与局限

- **数据与场景覆盖有限**：语料检查主要建立在 OLMo2 上；训练语料有其独特的爬取、清洗规则，结论是否在 Common Crawl、The Pile 等其他语料下统一成立未可知。
- **模型覆盖有限**：实验只覆盖了几个开源模型，无法证明该偏置在所有（尤其是闭源、对齐技术更强的）LLM 上都具备同等强度和相似模式。
- **任务范围局限**：七类数值推理任务虽然代表性较强，但尚未覆盖多位数运算、科学计算、代码生成或事实性 QA 等更广泛的数值场景，单数字和多位数字的偏置结构可能并不完全一致。
- **干预实验的作用上限存在未知**：剪除神经元只能"部分纠正误差输出"，这暗示除语料统计先验外还有别的影响因素，需要补充对残留偏置的解释；
- **缺少更正式的可训练性等指标补充**，本福特定律分布与实际语料分布的偏差既可能是训练目标设计中的天然产物，也可能受后训练对齐影响，文中未系统区分这些不同环节各自的贡献。

---

（完）
