---
title: Evidence-Focused Fact Summarization for Knowledge-Augmented Zero-Shot Question Answering
title_zh: 证据聚焦事实摘要：用于知识增强零样本问答
authors: "Sungho Ko, Hyunjin Cho, Hyungjoo Chae, Jinyoung Yeo, Dongha Lee"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.594.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 面向证据的知识图谱事实摘要框架，用蒸馏和偏好对齐使摘要忠实可靠并突出关键证据
tldr: 知识增强问答中，把知识图谱三元组机械地转成文本会造成证据密度低、重复内容多等问题。本文提出EFSum框架，将其中的LLM优化为证据聚焦的事实摘要器，主要通过蒸馏和偏好对齐完成，使摘要保留关键证据且更忠实。实验表明，EFSum在零样本问答上既提升了LLM的性能，又提供了精简可信的知识摘要，支持更可靠的知识利用。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main594/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main594/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 777, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main594/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1576, \"height\": 812, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main594/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main594/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 312, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1489, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1634, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1489, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 758, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 788, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1485, \"height\": 1300, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main594/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1473, \"height\": 412, \"label\": \"Table\"}]"
motivation: 知识图谱三元组直接转成文本往往重复低效，证据密度不足，难以服务知识增强问答。
method: 通过蒸馏和偏好对齐把LLM优化为证据聚焦的事实摘要器，为问答提供精简且关键的证据文本。
result: 实验显示EFSum提高了零样本QA性能，并使生成的证据摘要更忠实有用。
conclusion: 面向证据的事实摘要能够改善结构化知识到自然语言的转换质量，提升下游QA可靠性。
---

## Abstract
Recent studies have investigated utilizing Knowledge Graphs (KGs) to enhance Quesetion Answering (QA) performance of Large Language Models (LLMs), yet structured KG verbalization remains challenging. Existing methods, like concatenation or free-form textual conversion of triples, have limitations, including duplicated entities or relations, reduced evidence density, and failure to highlight crucial evidence. To address these issues, we propose EFSum, an Evidence-focused Fact Summarization framework for enhanced QA with knowledge-augmented LLMs. We optimize an LLM as a fact summarizer through distillation and preference alignment. Our extensive expeirments show that EFSum improves LLM’s zero-shot QA performance with its helpful and faithful summaries, especially when noisy facts are retrieved.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 一、核心问题与研究动机

- **研究背景**：大语言模型（LLMs）在零样本问答（Zero-Shot QA）中表现出色，但常因参数知识不完整或过时产生“幻觉”（hallucination）。知识图谱（KGs）作为外部结构化知识源，可用于增强LLM的问答能力。
- **核心挑战**：将KG中的符号化事实（三元组，(head, relation, tail)）转化为LLM可理解的自然语言文本（即事实文本化/verbalization），存在严重的“模态鸿沟”（graph-text modality gap）。
- **已有方法的两个关键缺陷**：
  1. **证据密度低（Low Evidence Density）**：无论是直接拼接三元组（KAPING）还是线性化生成自由文本（Rewrite），都会因实体/关系重复而产生大量冗余，导致相同token长度下有效证据稀疏。
  2. **证据清晰度低（Low Evidence Clarity）**：生成的知识文本缺乏对问题关键证据（如答案跨度）的强调，无法在开头位置突出关键事实，还掺杂大量与问题无关的噪声。
- **本文目标**：设计一种**面向证据的总结（evidence-focused summarization）**方案，使KG事实经处理后生成的文本既能压缩冗余、提升证据密度，又能优先突出与问题相关的关键证据，从而增强LLM的零样本QA准确率。

### 二、方法论

论文提出了**EFSum（Evidence-focused Fact Summarization）框架**，核心思想是通过优化一个小型开源LLM，使其作为“事实总结器”，能够针对给定问题从检索到的一组事实三元组中生成“高密度、高清晰度”的摘要。EFSum框架的完整做法包含三个层次：

1. **零样本提示方案（EFSum prompt）**
   - 直接通过详细提示词引导LLM（GPT-3.5-turbo）将问题相关事实三元组转换为一段连贯摘要。
   - 提示中要求摘要须作为问答上下文，不得直接透露答案，且只包含给定三元组的内容。

2. **蒸馏阶段（EFSum distill: LLM Distillation）**
   - 使用GPT-3.5-turbo（教师模型）用EFSum prompt对问答训练数据（q, a, F）生成高质量“参考摘要”。
   - 使用**监督微调（SFT）**训练Llama2-7B（学生模型），使其模仿生成面向证据的事实摘要。
   - 训练目标采用标准因果语言建模目标约化损失函数：  
     \( L_{SFT} = - \mathbb{E}_{(q,a,F,s) \sim \mathcal{D}} \log p_\theta(s \mid q, F) \)
   - 蒸馏阶段使模型获得生成灵活自然总结的基本能力。

3. **偏好对齐阶段（Preference Alignment with DPO）**
   - **摘要候选采样**：用微调后的模型针对每个训练样本采样M个摘要候选。
   - **两个质量过滤器**：
     - *Helpfulness过滤器*：将摘要交给QA模型生成答案，并与标准答案比对，检查是否能帮助QA模型答对问题。
     - *Faithfulness过滤器*：基于G-Eval方法用GPT-4评估摘要相对给定三元组是否包含无法推断出的不忠实信息（幻觉检测）。
   - **从宽泛到具体的改写（Broad-to-Specific Paraphrasing）**：对通过过滤器的候选，利用LLM在答案引导下改写为更聚焦问题具体答案的“特定摘要”。
   - 将同时通过过滤器的“精细摘要”作为偏好对中的首选（preferred），将未通过帮助性或忠实性过滤的候选作为非首选（dispreferred），从而构建偏好数据集。
   - **直接偏好优化（DPO）**：  
     \( L_{DPO}(\theta^*;\theta) = -\mathbb{E}_{(q,a,F,s^+,s^-)\sim\mathcal{P}} \log \sigma\left[ r(q,F,s^+) - r(q,F,s^-) \right] \)，  
     其中 \( r(q,F,s) = \frac{p_{\theta^*}(s|q,F)}{p_\theta(s|q,F)} \)，训练得到与问答任务偏好对齐的最终总结器。

### 三、实验设计

- **数据集**：
  - **WebQSP**（子集WebQSP-WD）：基于Freebase/Wikidata的KGQA数据集，测试集含1,033条样本，大多数为单跳问题。
  - **Mintaka**：复杂、多语言问答数据集，涵盖8种复杂度类型（多跳、比较、计数等），在本文使用英文4,000条测试样本。
- **评估的QA模型**：GPT-3.5-turbo、Flan-T5-XL、Llama2-7B-Chat三个模型作知识增强问答底座。
- **基线方法**：
  - No knowledge（无外部知识提示）、KAPING（三元组拼接）、KG2Text（T5-large微调的graph-to-text模型，基于WebNLG训练）、Rewrite（LLM的三元组改写方法）。
- **事实检索配置**：
  - 默认使用MPNet编码器进行语义相似度检索，取top-K相关三元组。检索范围设为一跳或二跳邻域。
  - 另外测试了“随机事实检索Random”和“流行关系知识Popular”两种注入方式以检验鲁棒性。
- **实验场景与研究问题对应关系**：
  - RQ1：固定最大token长度L=200/400，检验证据密度对QA准确率的影响。
  - RQ2：固定三元组数K=10/30，检验证据清晰度对模型定位答案能力的影响（仅考察事实F完全包含正确答案且QA模型自身可答对的子集上）。
  - RQ3：分析各方法的帮助性（summarizer输出摘要中包含正确答案的比例）和忠实性（1−幻觉发生率），及消融验证。
- **评价指标**：生成式KGQA的准确率（答案中是否出现正确答案之一，按文本包含判断）。此外还提供了“摘要级准确率”与“答案级准确率”以细致评价各类方法。

### 四、资源与算力

- 论文**未明确披露**以下算力和资源使用信息：
  - 使用了多少块GPU（型号与数量）
  - 训练总时长与训练轮数（epochs）
  - 硬件成本
  - 总体训练/推理的能耗预算
- 从文中可间接推断使用的是：

  - 学生模型：Llama2-7B（微调阶段）。
  - 教师模型：GPT-3.5-turbo（参考摘要生成与改写）和GPT-4（G-Eval忠实性过滤）。
  - 这些信息不足以准确估计算力成本，客观地说，论文在资源透明度方面有所欠缺。

### 五、实验规模、数量与充分性评估

- **实验组数较多，结构较完整**：

  - 主实验：3个QA模型 × 2个数据集 × 2种知识数量场景（L=200/400），与4个基线比较。
  - 清晰度实验（RQ2）：固定K=10/30，在各QA模型与数据集上做了系统实验。
  - 不同检索器鲁棒性实验（表2）：随机、popular、MPNet三种检索模式下进行验证。
  - 随K变化稳健性分析（K从10到150）：给出答案级与摘要级两个粒度图。
  - 帮助性与忠实性分析：各基线方法定量对比。
  - 消融研究（表4）：在Flan-T5-XL上移除paraphrase、helpfulness过滤器、全部过滤器+paraphrase三个变体。
  - 跨数据集泛化面实验（表5）：在WebQSP/Mintaka上交叉验证训练总结器的泛化性。

- **充分性评价**：
  - 覆盖了密度与清晰度两个维度，实验逻辑较严密，与提出的RQ一一呼应。
  - 主实验结果中有一些不一致的现象（如Mintaka上EFSum蒸馏模型低于某些基线），论文没有完全掩饰这一问题，有一定客观性。
  
  - 不足方面：
    - 消融实验只在Flan-T5-XL一种QA模型上做，缺少GPT-3.5和Llama2-Chat下的多样性消融验证。
    - 跨数据集泛化只用两个数据集互相训练/测试，样本类型较有限。
    - 论文对Mintaka上GPT-3.5上的性能下降解释不够清晰。

### 六、主要结论与发现

1. **EFSum确实能有效改善证据密度**：在限制token长度（L=200与L=400）的条件下，EFSum在大多数实验组合上优于基线的三元组拼接或改写方法。尤其在知识文本极端压缩（更小L值）时，优势更为明显。
2. **EFSum能增强证据清晰度**：在固定数量三元组（K=10或30）的实验中，EFSum显著提升了LLM定位答案的能力。在逐渐增大三元组输入时，EFSum在答案级准确率和摘要级准确率上维持稳定的领先优势。
3. **偏好对齐（DPO）提高帮助性和忠实性**：帮助性过滤器和忠实性过滤器以及回答引导的转述步骤对最终性能贡献显著；消融实验表明删除组件会使性能严重下降。
4. **开放模型经过蒸馏+偏好对齐后能较稳定地代替闭源教师**：EFSum蒸馏模型仅用Llama2-7B做底座的条件下，在大多情形下优于直接用GPT-3.5-turbo做EFSum prompt的效果，且更忠实，更少幻觉。
5. **跨数据集泛化基本成立**：模型在源数据集上训练可迁移应用于未见数据集，效果仍能超过多数基线。

### 七、方法的优点与亮点

- **问题定位精准**：直击结构化知识文本化的两大痛点（证据密度低、清晰度低），用定量分析（token重复率、答案位置、语义相似度）支持论点，说服力强。
- **方法设计完整**：提出“LLM提示 → 蒸馏 → 偏好对齐”的三步走路线，将蒸馏（模仿大模型总结能力）与DPO偏好对齐（生成任务导向的高质量摘要）有机结合。
- **引入两级自动质量过滤**：通过Helpfulness过滤器与Faithfulness过滤器（基于G-Eval）将摘要候选自动划分为优劣，配合“宽泛转具体”的改写机制，使最终偏好对能严格聚焦QA场景，而无需人工标注。
- **可移植性强**：作为独立于任何特定QA模型的模块，其灵活性与模型无关性确保其可便利嵌入不同知识增强流水线。
- **实验设计视角新颖**：通过固定token长度和固定三元组数量的双设置分别检验证据的“密度”与“清晰度”，实验架构与研究问题高度一致。
- **开源代码**和详细的中间数据样例与提示模板均公开，可复现性强。

### 八、不足与局限

1. **评估指标粗糙**：
   - 仅用“答案是否出现在生成文本中”的简单字符串包含式准确率，容易高估模型效果，难以识别语义上不正确但包含实体的回答。作者在局限说明时也坦诚这一点。
2. **对具体模型偏见难以控制**：
   - 部分大模型（如Llama2-7B-Chat在WebQSP上）对特定格式有内在偏好，事实总结器的优势在这些场景下体现不明显，可能需要为个体模型做额外的适配，否则效果受干扰（论文在Limitation中也提到）。
3. **依赖检索器质量**：
   - 对Mintaka等需要多跳信息的复杂数据集，MPNet检索器傾向于返回一跳到答案无关的邻居，限制了摘要器能够改善的“证据上限”。检索结果不佳会造成无米之炊。
4. **计算资源与数据构建成本高**：
   - 依赖GPT-3.5-turbo与GPT-4生成参考数据与做G-Eval评估，且每次训练中需要多次进行QA推理采样与过滤器运行，构建数据成本较高。
5. **跨数据集泛化验证深度有限**：
   - 只在两个KGQA数据集之间作了双向迁移测试，尚不清楚是否适用于领域差距大的数据以及不同语言的QA效果。
6. **Mintaka性能不稳定**：
   - EFSum蒸馏在Mintaka数据集上、以GPT-3.5作为QA底座时反而明显弱于基线和EFSum prompt，反映不同大小的QA模型对使用摘要的偏好并不一致，本篇论文对细粒度原因缺乏分析。
7. **需要更多人工验证**：对于忠实性评价仍主要依赖另一个LLM的评估，并没有结合人类直接评估，自动评估结果可能不能完全代表使用真实场景的忠实性体验。

---

### （完）
