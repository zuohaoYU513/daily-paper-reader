---
title: "KAHAN: Knowledge-Augmented Hierarchical Analysis and Narration for Financial Data Narration"
title_zh: KAHAN：面向金融数据叙事的知识增强分层分析与生成
authors: "Yajing Yang, Tony Deng, Min-Yen Kan"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1405.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 知识增强的分层金融数据叙事生成，兼顾事实性
tldr: "从原始表格生成金融报告时，不仅要提取多层面的洞察，还要保证生成内容的事实正确。本文提出 KAHAN 框架，将 LLM 作为领域专家，按实体、成对、分组和系统四个层级系统化地分析数据，并借助知识增强叙事过程。在 DataTales 金融报告基准上，KAHAN 的叙事质量比现有方法提升超过 20%，同时保持 98.2% 的事实性，人工评估也验证了其实用价值；该框架还能迁移到医疗等其他领域，显示了知识增强与层次化分析对金融文本生成与事实性的共同促进。"
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1565, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 686, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 789, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 773, \"height\": 649, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1405/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 383, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 738, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1333, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 1168, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1640, \"height\": 1841, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1651, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1405/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 435, \"label\": \"Table\"}]"
motivation: 金融数据叙事需要系统提取多层级洞察并保持高事实性，现有方法仍有明显不足。
method: 提出知识增强分层框架，在各层级用 LLM 分析并生成受控文本，兼顾知识质量。
result: "在 DataTales 基准上叙事质量提升超过 20%，事实性达 98.2%，并迁移到医疗领域。"
conclusion: 为金融报告生成提供了可复用、高事实性的知识增强方法论。
---

## Abstract
We propose KAHAN, a knowledge-augmented hierarchical framework that systematically extracts insights from raw tabular data at entity, pairwise, group, and system levels. KAHAN uniquely leverages LLMs as domain experts to drive the analysis. On DataTales financial reporting benchmark, KAHAN outperforms existing approaches by over 20% on narrative quality (GPT-4o), maintains 98.2% factuality, and demonstrates practical utility in human evaluation. Our results reveal that knowledge quality drives model performance through distillation, hierarchical analysis benefits vary with market complexity, and the framework transfers effectively to healthcare domains. The data and code are available at https://github.com/yajingyang/kahan.

---

## 论文详细总结（自动生成）

好的，我已经仔细阅读了您提供的论文文本和元数据。根据您的要求，我将对这篇论文进行结构化、深入且客观的中文总结。

---

## 论文核心问题与整体含义

### 研究动机与背景
- **核心问题**：如何将结构化表格数据（如金融行情）自动、准确地转化为有洞见的自然语言叙事报告（如市场日报）。这面临两大关键挑战：
    1.  **多层级分析**：有效叙事需要从不同粒度（单个资产、行业板块、市场整体）提取信息并建立联系。
    2.  **领域知识增强**：生成有意义的叙事需要专业的领域知识（如理解“利率上升导致科技股下跌”背后的资本成本逻辑），这超越了单纯的模式识别。
- **现有方法的不足**：
    - **端到端方法**：将数据扁平化处理，缺乏层级分析，也无法进行领域知识解释。
    - **LLMs**：虽有推理能力和参数化知识，但在系统化提取多层级洞察和一致性地应用领域知识方面表现不佳。
- **核心目标**：提出一个能够引导LLM进行结构化、知识增强的层级分析，从而生成高质量、高事实性的金融叙事框架。

## 论文提出的方法论：KAHAN框架

### 核心思想
**知识增强的分层分析**：将LLM从单纯的“文本生成器”转变为“领域专家”，通过一个三阶段流程系统地引导其进行分析和叙事，在每个阶段将领域知识与洞察提取过程相结合。

### 关键技术细节（算法流程）
框架共分三个阶段，如图2所示：

1.  **Stage 1: Entity-level Analysis（实体级分析）**
    - **步骤1.1（问题生成）**：LLM作为领域专家，为给定实体（如“纳斯达克”）生成特有的分析问题列表（如“趋势如何？”“收益率如何变化？”）。
    - **步骤1.2（代码生成）**：基于分析问题，LLM生成执行特定指标计算（如SMA、MACD、波动率）的Python代码。
    - **步骤1.3（代码执行）**：执行动态生成的代码，计算数据指标（如“纳斯达克100：+5.8%”）。
    - **步骤1.4（洞察提取）**：LLM解读数值结果，生成带重要性分数的实体级洞察（如“纳斯达克显示强劲反弹（0.9）”）。

2.  **Stage 2: Multi-level Insight Synthesis（多层级洞察综合）**
    - 此阶段以实体级洞察为基础，进行更高层次的综合分析：
        - **成对分析（Pairwise）**：利用LLM生成的成对关系知识（如“板块轮动动态”、“动量韧性模式”），识别实体间的对比和关联（如“科技强势 vs. 医疗保健疲软”）。
        - **分组分析（Group）**：利用LLM生成的实体聚类知识（如“指数组成”、“成长型 vs. 防御型板块行为”），将实体分组并分析组内模式（如“指数组：表现不一”）。
        - **系统级分析（System）**：利用系统级知识（如“资本流动显示风险偏好变化”），综合所有洞察，识别整体市场动态（如“市场呈现板块轮动”、“利率波动影响投资者情绪”）。

3.  **Stage 3: Narrative Generation（叙事生成）**
    - 利用叙事知识（如“以广泛市场表现开头”、“用基点表示利率变化”）和学习到的层级洞察，生成连贯、专业、符合领域惯例的最终叙事报告。

## 实验设计

### 数据集与基准
- **主要基准**：**DataTales** 基准测试集，包含 **460个样本**，覆盖 **11个金融子市场**（如能源、股权等）。
- **跨领域验证**：**PhysioNet** 的**帕金森病（PD）步态分析**数据集（93名患者，73名健康对照组，306个会话），用于验证框架的可迁移性。

### 对比方法
- **Direct Prompting (DP)**：零样本生成，无领域知识或中间分析步骤。
- **Chain-of-Thought (CoT)**：在DP基础上增加了逐步推理指令。

### 评估模型
- **开源模型**：Llama3.1-8B-Instruct, Qwen2.5-7B-Instruct。
- **专有模型**：GPT-4o。
- **（注）**：金融专用模型（FinanceLLM和TouchStoneGPT）因在阶段1和阶段2无法生成所需输出而被排除。

### 评估指标
- **质量 (Quality)**：采用DnA-Eval方法，由GPT-4o从**描述性 (Description, 40%)**、**洞察力 (Insights, 40%)** 和**可读性 (Readability, 20%)** 三个维度评分。
- **事实性 (Factuality)**：采用修改版FActScore，将生成文本分解为原子事实，并对照脚本计算的数值指标和维基百科金融知识进行验证。
- **实用性 (Practical Utility)**：由**两位金融领域专家**（一位8年经验的交易员和一位3年经验的分析师）对30篇报告进行盲评。

## 资源与算力
- **论文未明确说明**：论文文本中并未提及具体使用的GPU型号、数量、训练/推理时长或任何训练资源的详细配置。因此，无法提供具体的算力信息。

## 实验数量与充分性

### 实验组数
论文报告了非常全面且多角度的实验，主要包括：
1.  **主要对比实验**：3种模型 (Llama3.1, Qwen2.5, GPT-4o) × 3种设置 (DP, CoT, KAHAN)，评估质量和事实性。
2.  **定量指标分析**：对30个样本进行细致的定量元素分析（如市场指标数、因果数量、风险覆盖率等）。
3.  **消融实验（知识组件）**：逐项移除实体洞察提取、洞察综合、叙事处理知识，评估其对质量的影响。
4.  **消融实验（层级结构）**：逐步增加分析层级（实体→+成对→+分组→完整KAHAN），评估结构贡献。
5.  **知识来源影响实验**：使用不同模型（Qwen2.5, GPT-4o）或方法（无引导）生成知识，评估其对Llama3.1性能的影响。
6.  **市场复杂度实验**：比较KAHAN在简单市场（3个实体的能源市场）和复杂市场（28+实体的股权市场）中的性能差异。
7.  **跨领域实验**：在帕金森病步态数据集上评估框架的通用性。
8.  **人工评估**：2位专家对30篇叙事报告的实用性进行排名。

### 充分性与客观性评价
- **充分性**：实验设计非常充分，不仅验证了主方法的有效性，还通过多种消融实验深入剖析了各个组件（知识、层结构）的贡献和适用场景，增强了结论的可信度和可解释性。
- **客观性**：评估维度较全面，结合了自动指标（质量、事实性）和人工评估（实用性）。使用了多次实验取平均值和置信区间，并进行了统计显著性检验（配对t检验），这在很大程度上保证了客观性。
- **公平性**：在相同设置下对比了不同模型和不同方法。但需要指出，人工评估仅基于*实用性*一个维度且只包含两位专家，可能存在个体偏好偏差。此外，FActScore的修改版本依赖于GPT-4o mini，评估器本身的偏差可能被引入。

## 主要结论与发现

1.  **质量显著提升**：KAHAN在叙事质量上全面优于基线。使用GPT-4o时，质量得分（8.26）比DP（6.89）和CoT（6.61）分别提升约**20%**和**25%**。这一优势在描述性和洞察力两个维度上最为突出。
2.  **事实性得以保持**：在质量大幅提升的同时，KAHAN保持了与基线相当甚至更高的事实性（GPT-4o下为**98.2%**），证明高质量叙事不必然以牺牲事实性为代价。
3.  **知识质量是核心驱动因素**：**知识蒸馏有效**，更强大的模型（如GPT-4o）生成的知识可以提升较弱的模型（如Llama3.1）的性能；**有引导的知识生成**比无引导的更好。
4.  **层级分析的收益与市场复杂度相关**：在简单市场中，层级分析带来的收益更大（如描述性 +1.41），而在复杂市场中，收益主要体现在洞察力上，但可能会牺牲部分可读性。
5.  **框架可有效迁移**：在医疗（帕金森病步态分析）领域，KAHAN同样大幅超越基线，验证了其通用性。
6.  **专家偏好**：人工评估显示，交易员（目标用户）更偏好KAHAN提供的深入全面的分析（80%案例），而分析师则更偏好CoT的简洁性。

## 优点

1.  **创新的框架设计**：KAHAN巧妙地将“层级分析”和“知识增强”结合，并创造性地将LLM定位为“领域专家”而非“文本生成器”，解决了现有方法的根本痛点。
2.  **高质量的结果**：在质量、事实性和实用性三个关键维度上均取得了显著的领先，且统计验证扎实。
3.  **全面的实验验证**：实验设计严谨，分析深入。不仅证明了有效性，还细致地剖析了“为何有效”、“何时最有效”（如市场复杂度）以及“如何可以更有效”（如知识来源）。
4.  **强大的实用性与可迁移性**：通过专家评估证明了其在真实投资决策中的价值，并通过跨域实验证明了其框架的通用性，这提升了其实际应用潜力。
5.  **知识可复用性**：框架中生成的领域知识库可以被缓存并在后续报告中复用，降低了计算成本。

## 不足与局限

1.  **领域覆盖有限**：论文明确指出，尽管框架设计是通用的，但评估主要集中在金融领域，仅通过一个医疗数据集进行了初步验证，领域覆盖的广度仍有待加强。
2.  **评估偏差风险**：
    - **事实性评估**：修改版FActScore依赖于脚本和维基百科，对于需要复杂推理的诠释性声明（interpretive claims）的验证可能不够准确，而恰恰这类错误在GPT-4o的事实性错误中占比最高（63%）。
    - **质量评估**：DnA-Eval评估使用GPT-4o作为评判者，可能存在自我偏差（self-bias）。
    - **人工评估**：仅两人参与，且评估维度单一，不足以全面代表所有用户群体或捕捉所有效用维度。
3.  **应用限制与风险**：
    - 错误分析表明，随着分析复杂度的增加，事实性会下降，这意味着模型可能因追求分析深度而产生更具迷惑性的错误。
    - 存在被滥用生成看似权威的误导性市场叙事的风险。
    - LLM的参数知识可能过时或不完整，影响领域知识的质量。
4.  **未报告算力消耗**：论文未提及计算成本，这对于评估框架的实际应用门槛是一个重要缺失。

（完）
