---
title: Assessing “Implicit” Retrieval Robustness of Large Language Models
title_zh: 评估大语言模型的隐式检索鲁棒性
authors: "Xiaoyu Shen, Rexhina Blloshmi, Dawei Zhu, Jiahuan Pei, Wei Zhang"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.507.pdf"
tags: ["query:hallu-rag"]
score: 6.0
evidence: 评估并增强LLM对RAG无关检索上下文的鲁棒性
tldr: 检索增强生成的效果高度依赖检索器精度，无关上下文会显著损害答案质量。论文评估了多种大语言模型在不显式判断检索相关性的情况下直接输出的隐式检索鲁棒性，并发现用金标与干扰上下文混合微调可显著提高模型对检索误差的鲁棒性，同时保持生成能力。该策略有助于缓解RAG场景下由检索噪声引发的幻觉和事实错误，但并非面向金融文本的专项研究。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main507/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main507/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 1619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main507/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 1155, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main507/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 754, \"height\": 1427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main507/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 1166, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 1043, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1697, \"height\": 720, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1691, \"height\": 1467, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1691, \"height\": 1468, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main507/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1691, \"height\": 1468, \"label\": \"Table\"}]"
motivation: RAG效果依赖检索器精度，检索到无关上下文时模型输出性能会显著受损。
method: 评估LLM在不显式判断检索相关性条件下直接输出的隐式检索鲁棒性，并采用金标与干扰上下文混合微调增强鲁棒性。
result: 混合微调显著提高模型对检索噪声的鲁棒性，同时保持原有生成能力。
conclusion: 为提高检索增强生成系统在不可靠检索条件下的可靠性提供了有效训练策略。
---

## Abstract
Retrieval-augmented generation has gained popularity as a framework to enhance large language models with external knowledge. However, its effectiveness hinges on the retrieval robustness of the model. If the model lacks retrieval robustness, its performance is constrained by the accuracy of the retriever, resulting in significant compromises when the retrieved context is irrelevant. In this paper, we evaluate the “implicit” retrieval robustness of various large language models, instructing them to directly output the final answer without explicitly judging the relevance of the retrieved context. Our findings reveal that fine-tuning on a mix of gold and distracting context significantly enhances the model’s robustness to retrieval inaccuracies, while still maintaining its ability to extract correct answers when retrieval is accurate. This suggests that large language models can implicitly handle relevant or irrelevant retrieved context by learning solely from the supervision of the final answer in an end-to-end manner. Introducing an additional process for explicit relevance judgment can be unnecessary and disrupts the end-to-end approach.

---

## 论文详细总结（自动生成）

好的，我已经仔细阅读并分析了您提供的论文内容。以下是按照您的要求生成的详细中文总结。

### 论文核心信息概览
- **论文标题**: Assessing “Implicit” Retrieval Robustness of Large Language Models（评估大语言模型的“隐式”检索鲁棒性）
- **会议**: EMNLP 2024 (Main Conference)
- **作者**: Xiaoyu Shen, Rexhina Blloshmi, Dawei Zhu, Jiahuan Pei, Wei Zhang

### 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：检索增强生成（RAG）通过引入外部知识库，有效弥补了大语言模型静态知识的局限性。然而，RAG系统的整体性能高度依赖于检索器（Retriever）的精度。当前端检索器不够精准、返回无关或误导性的上下文时，LLM的生成质量会受到显著损害，其表现甚至可能劣于完全依赖内部参数知识的模型。
- **核心问题**：本文关注LLM在RAG流程中的**检索鲁棒性**问题。一个理想的检索鲁棒模型必须具备两个关键能力：
    - **能力I**：能够从**相关**（Gold）的检索上下文中提取信息并给出正确答案。
    - **能力II**：当检索到的上下文是**干扰性**（Distracting/不相关）时，能够忽略它并回退到自身内部参数知识来回答问题。
- **核心矛盾**：以往提升鲁棒性的主流方法（显式方法）会引入一个额外的中间步骤，让模型先显式判断检索内容与问题的相关性，再根据判断结果走不同路径（如生成或放弃）。虽然这种做法粒度更细，但会增加延迟、有错误传播风险，且需要昂贵的相关性标注。本文旨在探索一条更简洁的“隐式”路径：**能否在不引入显式相关性判断模块的情况下，仅通过端到端的训练信号，让LLM自主学习如何区分并应对相关与不相关的检索上下文？**

### 2. 论文提出的方法论：核心思想与技术细节
- **核心思想**：与“显式”建模（先判断相关性再决定走哪条路径）不同，“隐式”鲁棒性要求LLM直接基于 `(问题, 上下文)` 生成答案，模型需要内部自主权衡上下文和自身知识的权重，而整个过程只依赖最终的答案监督信号。
- **理想目标建模**：论文用数学公式形式化定义了理想鲁棒模型 `p_robust(a|q, c)`（公式1）：
  ```
  p_robust(a|q, c) = {
      δ(a - a*), 如果正确答案a*在上下文c中
      p(a|q)     否则（即忽略c，依赖内部知识）
  }
  ```
  该定义清晰地明确了鲁棒模型的两条分支，即对应前述的Capability I和Capability II。
- **技术路线 (Fine-tuning on Mixed Context)**：
    - **核心策略**：为了达到上述理想状态，论文提出并验证了**混合微调**的有效性。在构建训练数据时，随机将一部分样本的金标（Gold）上下文替换为**干扰性（Distracting）上下文**，作为难负样本。
    - **实验变量**：通过控制训练集中干扰样本的混合比例（0%、20%、50%）来观察其对模型最终鲁棒性的影响。
    - **对照训练模式**：对比了仅用Gold上下文微调和用混合上下文微调；同时对比了全参数微调（Full Fine-tuning）和参数高效微调（LoRA）。
    - **关键思路**：该做法的目的是让模型在训练阶段就“看见”无关内容，并通过最终答案的监督信号学会在这种情况下“关掉”检索通道，转而依赖自身的参数化知识（即Capability II），同时不损害从相关上下文中提取答案（Capability I）的能力。

### 3. 实验设计：数据集、基准与对比方法
- **数据集基准（5个）**：论文选取了多样化的问答（QA）任务，全面覆盖不同领域和场景，避免单一知识源的偏差。
    - **AmbigQA**: 通用知识问答，知识源为维基百科。
    - **ePQA**: 产品特定问答，知识源为亚马逊商品页面（含JSON格式非结构化信息），测试尾部知识。
    - **Musique**: 需要多跳推理的问答，知识源为维基百科。
    - **SciQ**: 科学类单选题，知识源为教科书。
    - **TopioCQA**: 多轮对话问答，知识源为维基百科。
- **测试场景**：针对每个数据集，模型都在三种检索输入条件下被评估：
    1.  **无上下文 (None)**：作为性能下限（即`p(a|q)`）。
    2.  **金标上下文 (Gold)**：来自原数据集，含答案，测试Capability I。
    3.  **干扰性上下文 (Distract)**：模型最终测试的难点，检验Capability II。干扰上下文通过DPR检索器取Top-10文档，再选用其中与真实答案相似度最低的文档，以保证是“困难”且符合现实的干扰样本。
- **模型与方法**：
    - **开源模型**：Vicuna-1.3-7B/13B/33B 和 Llama-2-chat-7B/13B。测试了三种策略：**零样本提示**、**LoRA微调**、**全参数微调**。
    - **闭源模型**：GPT-3.5 (gpt-3.5-turbo-0613) 和 GPT-4 (gpt-4-0613)，作为强基线仅通过提示词进行测试。
    - **评估指标**：采用**Recall**指标（答案中命中金标字符的比例）来评估性能，因为生成答案可能更长但包含正确信息，论文通过实验验证发现该指标与人类判断的相关性最高。

### 4. 资源与算力
- **计算设备**：所有实验在 8 张 NVIDIA A100 GPU 上完成。
- **训练时长**：每个模型（7B）在单个数据集上训练约耗时 10 GPU 小时；13B 模型约 15 小时；33B 模型约 30 小时。
- **超参数设置**：固定batch size为64，模型只训一个epoch，文本截断长度为1024子词。学习率通过网格搜索在较广范围内（如1e-6至5e-3）为每个模型找到最优值。

### 5. 实验数量与充分性
- **实验数量**：论文进行的实验非常之多，涵盖了大规模的组合矩阵。
    - **5个数据集** × **7个模型（含闭源）** × **3种输入条件（无/金/干扰）**。
    - **5个开源模型** × **2种微调方法（全/洛拉）** × **3种混合噪声比例（0%/20%/50%）**。这部分是一个核心消融实验，定量分析了数据噪声对能力I和能力II的影响。
- **充分性与公平性**：
    - 设计上考虑了公平性，突出体现为对“干扰性”样本的构造，未采用“荒谬”级别的噪声，而是通过相似性检索挑选困难负样本，使得评估更具现实意义。
    - 文章对学习率进行了广泛的网格搜索，力求模型性能在各自的最优点附近，且在零样本和微调测试中使用了一致的提示词，以控制变量。
    - 论文的分析层次清晰，不仅呈现最终分数，还基于数据将问题解耦为能力I与能力II进行分别评估，很好地支撑了各个核心论点。可视为评估完备性很高，在资源允许的范围内做到了充分。

### 6. 论文的主要结论与发现
- **直接提示测试（未微调）**：
    - 在能力I（利用正确检索上）上，开源LLM显著弱于GPT-3.5/4，尤其在ePQA、Musique和TopioCQA这类复杂任务上。
    - 在能力II（忽略干扰）上，开源LLM可以比肩甚至超过GPT-3.5/4。模型越大，抗干扰能力通常也越强，反而是强大的闭源模型在涉及常识知识时有明显表现下降。
- **仅使用金标上下文微调**：
    - 能力I在挑战性数据集上得到显著增强，甚至能超越GPT-4（如在ePQA上）；但在简单数据上呈现瓶颈，此方法不足以缩小开源与闭源模型的差距。
    - 能力II会受损，因为在微调中模型学会了过度依赖提供的上下文。
    - **LoRA**在增强能力I上和全量微调接近，但能**更好地保住能力II**（维持干扰场景下的表现）。
- **使用混合上下文微调（核心发现）**：
    1.  **不影响能力I**：在微调中加入噪声上下文，甚至能挽回由于数据篇幅减少造成的性能瓶颈，在困难任务（Musique）上稳定性反而更好。
    2.  **显著提升能力II**：提高训练数据中的噪声比例，能使模型应对干扰性检索的结果稳步提升。
    3.  **接近无检索上限**：在输入较短、任务较直接的场景下，将50%的训练样本设为干扰，模型在受干扰时的性能几乎能达到不提供检索时的水平（即完全免疫干扰）。
- **总体结论**：LLM具备很强的隐式检索鲁棒性学习潜力，直接混合一点噪声数据进行端到端训练，就能基本解决检索噪声的问题。文中建议在多数非复杂推理任务的QA中，无须再加显式判断模块。

### 7. 优点
- **问题定义严谨**：从公式化的角度清晰地抽离并定义了检索鲁棒性的两个核心能力，为后续分析提供了干净的框架，有助于设计针对性的实验。
- **实验体系全面**：同时结合了多类型模型（开源/闭源）、多微调方法、多检索信息和多噪声比例，这一系统性组合观察在类似文献中实为少见，定量维度很扎实。
- **结果分析深入**：不是简单给分数，而是依据能力I/II的差距对数据进行了解读，巧妙利用了模型的性能天花板和行为差异来解释大道理。
- **实践指导价值高**：论文发现的简单“混合”做法，对于应用中想要快速提升RAG可靠性而不希望对模型结构动刀的情形提供了直接可落地的实用建议，成本极低。
- **方法颠覆性**：证明了传统认为需要显式相关性过滤的做法在某些情境下是不必要的，为轻量化RAG组件提供了新证据。

### 8. 不足与局限
- **模型规模与时限**：研究局限于Llama/Vicuna模型家族且最大仅33B。截至论文发表时已涌现很多更新的开源模型（如Mistral、更高参数Llama等），因此按当时版本的模型来比较开源与闭源系统的优势可能时效性已过。论文作者在Limitations中也明确指出了这一点。
- **回答格式限制**：评估仅使用了短答案数据集，这主要是为了便于召回率计算。对于日渐重要的篇幅长、结构复杂的生成型回答，检索噪声是否仍能被如此优雅地过滤器掉有待进一步检验。
- **数据构建模拟性强**：虽然干扰场景是通过DPR的Top-10挑选，但相对于真实的生产环境中检索器（可能返回高度相关的谎话或复杂矛盾信息），所用的模拟仍是受控环境，尚不能完全代表实际可能遇到的各种复杂挑战。
- **超参数搜索局限**：虽然搜索了广泛的学习率，但所有模型只训练了一个epoch，没有对Batch Size、Epoch数等进行细致的探索，数据集大小也被截为约3000训练/200测试条子集，这些因素在不同场景下可能有更复杂的影响。
- **理想模型缺口**：公式中理想的“忽略干扰”策略是能回退到内部知识，但这对模型本身内部知识的广度有隐性要求；实验也显示多跳或多轮任务中不能完美实现完全鲁棒性，说明对于这种深度推理的情况隐式办法可能还不能替代显示机制或专门结构。
- **泛化领域**：论文关注的是通用QA基准。面向金融等特定垂直领域（如财务报表、研报分析），领域术语、长文档、数字精确性与格式呈现的要求，以及信息错误的模式不一定被这些知识和任务代表，因此实验结果的可迁移性需要在该领域内重新评估。

---

（完）
