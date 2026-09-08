---
title: "Beyond the Surface: Measuring Self-Preference in LLM Judgments"
title_zh: 超越表面：度量LLM评判中的自我偏好
authors: "Zhi-Yuan Chen, Hao Wang, Xinyu Zhang, Enrui Hu, Yankai Lin (林衍凯)"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.86.pdf"
tags: ["query:metacognitio"]
score: 10.0
evidence: 引入标准答案判断区分自我偏好与回答质量，提出DBG分数度量自我偏好
tldr: 大语言模型作为评判者时通常偏向自己的输出，但以往用自己与他人得分差度量自我偏好会混入回答质量因素。论文引入gold judgments作为答案质量的代理，提出DBG分数，通过相对分数差剥离质量影响，更纯净地衡量自我偏好偏差。该度量有助于准确评估基于LLM的评测与自我评价，揭示了自我偏好的真实程度。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 1143, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1650, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 768, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1634, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1490, \"height\": 868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1133, \"height\": 232, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1638, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1634, \"height\": 221, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1128, \"height\": 161, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1644, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1645, \"height\": 1459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main86/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1473, \"height\": 580, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 732, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1528, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1605, \"height\": 1097, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1599, \"height\": 1147, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1598, \"height\": 1147, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main86/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1606, \"height\": 1151, \"label\": \"Table\"}]"
motivation: 现有多项自我偏好度量法混淆了偏好与回答质量，导致偏差评估失真，需要更精细的度量设计。
method: 把gold judgments作为答案质量的代理，计算模型给自己打分与给他人打分的差异相对于gold判断的偏差，从而得到DBG自我偏好分数。
result: DBG分数能更准确地分离身份偏见与质量因素，实证发现了模型自我偏好程度的新现象。
conclusion: 将质量代理纳入测量可有效重构自我偏好评估，为LLM评测偏差分析提供了新工具。
---

## Abstract
Recent studies show that large language models (LLMs) exhibit self-preference bias when serving as judges, meaning they tend to favor their own responses over those generated by other models. Existing methods typically measure this bias by calculating the difference between the scores a judge model assigns to its own responses and those it assigns to responses from other models. However, this approach conflates self-preference bias with response quality, as higher-quality responses from the judge model may also lead to positive score differences, even in the absence of bias. To address this issue, we introduce gold judgments as proxies for the actual quality of responses and propose the DBG score, which measures self-preference bias as the difference between the scores assigned by the judge model to its own responses and the corresponding gold judgments. Since gold judgments reflect true response quality, the DBG score mitigates the confounding effect of response quality on bias measurement. Using the DBG score, we conduct comprehensive experiments to assess self-preference bias across LLMs of varying versions, sizes, and reasoning abilities. Additionally, we investigate two factors that influence and help alleviate self-preference bias: response text style and the post-training data of judge models. Finally, we explore potential underlying mechanisms of self-preference bias from an attention-based perspective. Our code and data are available at https://github.com/zhiyuanc2001/self-preference.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文核心问题与整体含义（研究动机和背景）

- 当前大语言模型（LLM）被广泛用作“评判者”（LLM-as-a-judge），但研究发现其存在**自我偏好/自我增强偏差（self-preference bias）**：模型在评判自己生成的回答时，倾向于给出比其他模型更高的评分。
- 既有度量方法通常直接计算“评判模型给自己回答的得分”与“给其他模型回答的得分”之差，然而这种方式**混淆了自我偏好与回答质量**：如果被评判者自己的回答确实质量更高，得分差也会为正，即使没有任何偏差。
- 因此，本文提出一种新的度量指标——**DBG score（Difference Between model scores and Gold judgments）**，引入**标准评判（gold judgments）**作为回答真实质量的代理，从而剥离质量因素，更干净地估计自我偏好偏差。
- 这一工作对基于LLM的评测体系具有重要价值：只有准确测量偏差，才能改进LLM作为评测工具的可信度，并为后续缓解偏差提供理论依据。

## 2. 论文提出的方法论

### 核心思想
- 假设每个回答`r`存在真实内在质量`Q(r)`，评判模型A的评分`S_A(r)`可分解为：
  `S_A(r) ≈ Q(r) + b_A(r)`，其中`b_A(r)`是模型对该回答的偏差。
- 只考虑自我偏好时，模型只对自己的回答存在正向偏差，因此`b_A(r_B)=0`且`b_A(r_A)>0`。
- 用Bradley-Terry模型描述偏好概率：`P(r_A ≻ r_B) = σ(δ + b_A)`，其中`δ = Q(r_A)-Q(r_B)`是质量差。
- 传统方法使用`w_A = E_x[σ(δ + b_A)]`，即模型A选自己回答的期望概率；但`δ`会污染该值。

### DBG score 定义
- 引入无偏“标准评判”的偏好概率：`w* = E_x[σ(δ)]`。
- DBG score定义为：`ŵ_A = E_x[σ(δ + b_A) - σ(δ)]`。
- 当`ŵ_A > 0`时说明模型存在自我偏好，数值越大偏差越严重。
- 当`b_A`较小时，一阶泰勒展开表明`ŵ_A ≈ E_x[σ′(δ)]·E_x[b_A]`，即它是真实偏差`b_A`的线性缩放估计，从而**将质量效应δ显式移除**。

### 具体实现
- **标准评判（gold judgments）的构造**：聚合三个强模型——GPT-4o-mini、Gemini-1.5-Flash、DeepSeek-V3的评判结果（多数投票或概率平均）作为回答质量的代理。
- **成对比较协议**：将同一指令的两个回答组成pair，评判模型只输出A或B，并利用输出token概率计算偏好；交换回答顺序后取均值以消除位置偏差。
- **预训练模型**使用少样本上下文学习（两个示例）；**后训练模型**使用零样本提示。
- 所有模型temperature设为0，保证确定性；通过限制回答最大长度缓解长度偏差。
- 整体流程为：生成回答 → 模型做一对多成对比较 → 位置交换 → 计算胜率 → 与gold judgments计算的胜率相减得DBG score。

## 3. 实验设计

### 数据集与任务
- **AlpacaEval**（有用性，主实验）
- **WMT19（de-en）**（翻译质量，见附录）
- **TruthfulQA**（真实性，见附录）
- 每个数据集随机采样**500个示例**。

### 评测模型与被测模型
- 作为**gold judge**：GPT-4o-mini、Gemini-1.5-Flash、DeepSeek-V3（三个模型来自不同家族，避免偏好泄漏）。
- 作为**被测judge模型**：
  - Llama-3.1-8B（-Instruct）、Llama-3.1-70B（-Instruct）
  - Qwen2.5-7B（-Instruct）、Qwen2.5-72B（-Instruct）
  - gemma-2-9B（-it）
  - Qwen2.5-Instruct系列：0.5B、1.5B、3B、7B、14B、32B、72B
  - 推理模型：DeepSeek-R1-Distill-Qwen-32B、QwQ-32B，与Qwen2.5-32B-Instruct对照
- 附录中还测试了闭源模型 Claude-3.5-Haiku、Qwen-Plus、GLM-4-Plus。

### 对比基准
- 传统方法（即`w_A`，仅看模型自评与他评的胜率差）与新提出的DBG score进行了对比。
- 人类注解：从AlpacaEval抽取100条样本，由人类比较模型对回答的胜率，验证gold judgments可靠性。
- 三个gold judge之间的两两一致性也被评估。

### 消融与机制分析
- **响应风格影响**：用DeepSeek-V3将模型对回答重写为“attractive”和“humorous”两种统一风格，比较风格改写前后DBG的变化。
- **后训练数据影响**：将Llama-3.1-8B和Qwen2.5-7B在相同的UltraChat-200k数据上微调，得到-UltraChat版本，观察自我偏好是否减弱。
- **注意力机制分析**：分析judge模型在层间对各回答token的平均注意力，比较模型是否更关注自己的回答。

## 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量、训练时长或推理算力总量。
- 只在Limitations中提到：由于成本限制，未选择GPT-4o或Gemini-1.5-Pro等更强模型作为gold judge。
- 因此关于计算资源的细节无法从论文中获取。

## 5. 实验数量与充分性

### 实验数量
- 核心结果在AlpacaEval上展示，另外两个数据集（TruthfulQA和WMT19）的结果放在附录，主要结论具有跨数据集一致性。
- 覆盖三类主要对比：
  - 相同规模下：预训练vs 预训练、后训练vs 后训练、预训练vs 后训练；
  - 不同规模下：8B/70B、7B/72B等；
  - 推理模型：32B LRM与普通32B模型。
- 附加实验包括：人类一致性与gold judge间一致性分析、专有模型分析、few-shot与zero-shot对照、文本重写后语义保持验证、注意力分析。

### 充分性评价
- **优点**：试验矩阵较全面，从版本、尺度、推理能力、数据与风格维度交叉验证；同时考虑了位置偏差、温度、长度偏差等干扰因素，并使用人类判断与标准裁判一致性来支撑可靠性。
- **局限**：
  - 主实验集中在3个数据集，且正文主要呈现AlpacaEval；任务类型仍属开放域指令跟随/翻译/真实性，未覆盖数学、代码、Agent等场景；
  - 人类验证样本仅100条，规模较小；
  - 部分观察（如模型对回答内容的混淆）缺乏定量统计显著性检验；
  - 对每个实验条件未报告多次运行的标准差/置信区间。

## 6. 论文的主要结论与发现

1. **引入gold judgments使自我偏好的测量更准确**。例如Qwen2.5-72B-Instruct作为裁判给自身回答的胜率为52.3%，高于Llama-3.1-70B-Instruct给出的50.0%，但仍低于gold judgments给出的54.5%，说明其得分优势主要来自回答质量而非自我偏好。
2. **预训练模型和后训练模型都存在自我偏好偏差**；这表明自我偏好不是后训练阶段单独引入的。
3. **后训练模型并不一定比预训练模型偏差更严重**。例如Llama-3.1-8B-Instruct的DBG为0.2%，而Llama-3.1-8B的DBG高达25.6%。
4. **更大规模的模型自我偏好更弱**。Llama-3.1-70B的DBG为0.4%，而Llama-3.1-8B为21.6%；Qwen2.5-0.5B-Instruct为41.7%，14B版本仅2.1%。因此评测时应尽量选用更大模型。
5. **推理模型（LRM）也存在自我偏好，且并不一定比普通LLM更低**。如DS-R1-Distill-Qwen-32B的DBG为4.8%，高于Qwen2.5-72B-Instruct的2.6%。
6. **统一响应风格可以缓解自我偏好偏差**。把不同模型的回答改写成一致的有吸引力或幽默风格后，DBG显著下降；但不能完全消除，说明内容本身也贡献了偏差。
7. **在相同数据上后训练不同模型可降低自我偏好**。但经过相同数据微调后仍存在残余的自我偏好，说明预训练遗留的“生成—评判”差异难以完全消失。
8. **注意力分析显示**，judge模型相比其他模型更关注自己的响应，这可能是自我偏好产生的机制之一。

## 7.

## 7. 总结与展望

### 7.1 研究贡献

本文的核心贡献在于从方法论层面解决了 LLM-as-a-judge 自我偏好测量中的“质量混淆”问题。传统方法将自评得分与他评得分的差值直接视为自我偏好，却忽略了被评判回答本身可能存在真实质量差异；DBG score 通过引入外部标准评判（gold judgments）作为质量基准，将质量因素显式剥离，使测得的偏差更接近模型内在的自我偏好。这一思路具有较强普适性，不仅可用于自偏好检测，也可推广到其他类型的评判偏差（如风格偏好、格式偏好等）度量。

此外，论文构建了跨模型家族、跨规模、跨训练范式的系统测评框架。从预训练基座模型到后训练模型，再到具有推理能力的大推理模型，都有较完整的覆盖；还通过风格改写、共享数据微调、注意力机制分析等辅助实验，从行为与机制两个层面验证了自我偏好的来源与可干预性。

### 7.2 实践意义

- 为自动评估流程提供了一个**无需人类标注的偏差校准工具**，可在使用 LLM-as-a-judge 时快速诊断评判者是否存在对自身输出的偏袒。
- 实验发现“更大模型通常自偏好更低但有例外”，提示实际部署时应**结合 DBG score 筛选评判模型**，而非仅依据模型规模或通用榜单表现。
- 响应风格统一与共享后训练数据均能有效降低偏差，说明在需要多模型对比的评测任务中，**标准化生成格式与共享训练背景**有助于提升评测公平性。

### 7.3 未来研究方向

- 进一步提高标准评判构造的可靠性，例如引入多维质量标注或经过校准的人类偏好池，避免标准评判本身带有残留偏差。
- 将 DBG score 扩展至**逐样本的偏差建模**，不仅给出整体偏差量，还能定位偏好发生在哪类指令或输出特征上。
- 探索**无偏评测协议**，如在评判时隐去回答来源、在训练阶段加入偏差正则化，或利用少样本校准自动消除自我偏好的影响。
- 将研究范围扩大至开放问答之外的任务，包括数学推理、代码生成、多轮对话、多模态生成等领域，检验自我偏好的普遍性。

（完）
