---
title: "FactVerse: A Benchmark for Factual Consistency in Interleaved Image–Text Generation"
title_zh: FactVerse：交错图文生成中的事实一致性基准
authors: "Yubo Shan, Kun Zhang, Qiming Xu, Liping Cao, Yingying Cao, Jian Zhang, Yu Wang, Jingyuan Li, Yuanzhuo Wang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1323.pdf"
tags: ["query:faithfulness"]
score: 4.0
evidence: 针对交错图文生成的事实一致性评测基准，不含文本摘要或数值幻觉专门任务
tldr: 该论文针对交错图文生成中的事实一致性问题，提出 FactVerse 基准，包含3000个人工标注样本，用于评测生成内容与源信息的一致程度。该基准聚焦多模态叙事中的事实错误风险，为多模态事实一致性评估提供了标准化测试平台。由于不面向文本摘要或数值事实，对纯文本证据约束生成任务的相关性有限。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 1094, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 756, \"height\": 920, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1323/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 770, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1664, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1653, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1661, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1662, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1663, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1323/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 747, \"height\": 268, \"label\": \"Table\"}]"
motivation: 交错图文生成已成为重要方向，但其多模态叙事易传播错误信息，现有基准缺乏事实一致性评测机制。
method: 构建包含3000个人工标注样本的FactVerse基准，用于评测交错图文生成中的事实一致性。
result: 该基准能为交错图文生成提供标准化的事实一致性评测结果。
conclusion: 作为多模态事实一致性基准，FactVerse为跨模态生成评测提供参考，但与文本忠实度任务关联较弱。
---

## Abstract
Interleaved multimodal understanding and generation—where models can interactively comprehend and produce images and text in arbitrary orders—has emerged as a key research direction in generative Multimodal Large Language Models(MLLMs). Such interleaved image–text content plays an increasingly important role in information dissemination. However, the compounded persuasive power of multimodal narratives also raises the risk of factual misinformation. Despite this, existing benchmarks lack effective mechanisms to evaluate factual consistency in interleaved image–text content. To bridge this gap, we introduce FactVerse, a benchmark dedicated to evaluating factual consistency in interleaved image-text generation. FactVerse comprises 3,000 human-verified instances across four categories and 50 domains, supporting both English and Chinese. We also establish a multi-dimensional evaluation framework designed to rigorously assess factual consistency. Experiments demonstrate that our framework achieves high alignment with human judgments, significantly outperforming existing evaluation methods. Furthermore, our analysis reveals systematic deficiencies in current models, offering critical insights for future design.

---

## 论文详细总结（自动生成）

## 论文总结：FactVerse——交错图文生成中的事实一致性基准

### 一、核心问题与研究动机

- **背景与问题**：随着多模态理解与生成技术的快速发展，交错图文生成（即模型可任意顺序交互式地理解并生成图像与文本）已成为生成式多模态大语言模型（MLLMs）的重要研究方向。该类内容在知识传播中扮演关键角色，然而多模态叙事融合了文本与图像的“复合说服力”，使得错误信息的传播风险显著放大——正如“眼见为实”的认知偏差所揭示的那样，特别是在科学教育、医疗指南、新闻报道等高风险场景中，视觉丰富的错误内容往往比纯文本错误更具误导性。

- **现有评测基准的三方面不足**：
  1. **主要关注感知而非事实性**：如OpenLeaf、InterleavedBench等现有基准侧重语义相关性、视觉流畅度等感知质量，缺少对客观事实的显式验证机制；
  2. **缺乏可验证的黄金标准（Ground Truth）**：许多基准面向开放式创意任务（如故事生成），容忍歧义，无法为严格的真实性核查提供标准；
  3. **评测导向严重错位**：当指标奖励表面合理的内容时，模型会被激励追求连贯性与美观而牺牲事实准确性，既掩盖模型缺陷也催生误导性内容。

- **核心研究问题**：当模型生成貌似专业的科学图表或操作指南时，如何保证其事实真实性和逻辑严谨性？

### 二、方法论

#### 2.1 FactVerse 基准数据集的构建

- **任务定义**：将交错生成过程形式化为映射函数 F : (I, C) → S，其中 I 为指令，C 为多模态上下文（交错文本段与图像），S 为生成的输出序列。基于布卢姆认知分类学设计了四个核心任务：

  - **任务1：实体锚定事实生成（Entity-grounded Generation）**——对应“记忆”与“理解”层级，要求生成内容 (T, v) 与权威知识库中实体 e 的事实 F_e 和视觉属性 A(e) 严格对齐；
  - **任务2：机制锚定系统解释（Mechanism-grounded Explanation）**——对应“理解”与“关联”层级，将目标机制定义为有向因果图 G = (V, E_causal)，要求生成文本和图表与功能组件和方向性因果流一致；
  - **任务3：时间过程生成（Temporal Procedural Generation）**——对应“应用”与“规划”层级，过程定义为不可逆状态序列 P = {s₁,…,s_T}，强制时间单调性约束：若 i < j 则 T(sᵢ) < T(sⱼ)，且图像须准确反映累积状态变化 Δs_t；
  - **任务4：数据锚定分析（Data-grounded Analysis）**——对应“分析”与“综合”层级，要求生成结论 c 不与源数据 D 导出趋势 f_trend(D) 相矛盾（c ⊥̸ f_trend(D)），覆盖完整的“感知—分析—生成”链路。

- **数据收集与质控**：
  - 由12位STEM方向硕博研究人员组成专家团队，按规范化手册从多源收集数据：实体类取自Wikipedia等权威百科，机制类摘自开放学术文献与教学媒体，过程类来自WikiHow等经核验的分步指南，数据类源自Our World in Data、OECD等可靠国际数据库；
  - **混合增强策略**：对<5%的稀缺科学图解场景使用Gemini-2.5-flash-image-preview进行合成，并附加人工审查保证科学有效性；
  - **质量控制**：“双盲标注+专家仲裁”机制（Fleiss' Kappa < 0.6时触发高级专家介入），不可调和歧义的样本直接丢弃；对高风险医疗/工程操作引入“安全审查否决机制”——模型输出禁忌操作时强制将事实分数压至最低；过滤含暴力、冒犯、个人身份信息及低质量视觉证据的数据。

- **数据规模**：共3,000条人工验证实例，四类任务各750条，含英文2,000条和中文1,000条，覆盖24个子任务和50个领域，采用“长尾分布”策略以避免模型对特定来源的过拟合。

#### 2.2 三维事实评测框架

- **FactJudge 判别器（对抗式事实感知判别器）**：
  - 基于 Qwen3-VL-8B 微调，使用8,000条人工标注的评分数据（覆盖实体错配、因果链反转、步骤倒置等关键错误模式），每条包含详细错误解释；
  - 采用“思维链+先推理再打分”（Reasoning-then-Scoring）范式，促使模型先分析逻辑差异再给出分数；
  - 采取真实模型错误挖掘 + 针对性补充构造负样本的方法，并结合外部数据集构建对抗探针集验证泛化性。

- **语义锚定 VQA 验证策略（Semantically Anchored VQA）**：
  - 不再依赖开放式的视觉解读，而是将黄金标准中的关键事实约束（对象属性、空间关系、定量数据）转换为精确的问答对；
  - VQA模型仅充当客观验证器，检验生成图像是否会产生由专家黄金标准导出的标准答案，使主观视觉评判转化为可量化的事实指标。

- **规则约束检查（Rule-based Metrics）**：负责检查不依赖模型推理的量化组件：
  - *上下文命名实体召回（Context Entity Recall）*：从标准答案提取关键实体与生成文本比较，检查核心实体覆盖完整性；
  - *CLIPScore 创新性改造*：正因CLIP文本长度限制（77 token），创新地将需匹配内容截断为关键实体关键词而非冗长全文，有效消除背景叙述噪音，聚焦核心概念的图文语义对齐；
  - *结构核查（Structure Check）*：验证模型生成了指令所要求的图像数量。

- **五项定量指标的详细计算协议**（统一归一化至0-100）：
  - IFC（图像事实一致性）= s_FactJudge(I,C) × 10
  - TFQ（文本事实质量）= 0.5×语义评分 + 0.5×实体召回率
  - SAS（语义锚定分数）= 锚定VQA问题答对率百分比
  - ITS（图文协同）= 0.5×CLIP余弦相似度 + 0.5×FactJudge一致性评分（换算至100）
  - CC（指令合规）= 满足的结构约束比例百分比

### 三、实验设计

- **基准数据集**：FactVerse（3,000条实例，中英双语、四类任务、50个领域）。作为对比，与其他代表性基准的比较见表1：FactVerse在可验证事实（Verifiable Factuality）、多语言支持（EN+ZH）、准确率等方面为同类基准中对多语言支持最全面的，且拥有完整的离线评测体系。

- **评估的基线模型（10个，分三组）**：
  - **统一模型（Unified Models）**：Anole、Show-o、Emu3、Vila-U、VARGPT——将图像和文本统一于单一Transformer自回归框架。
  - **组合系统（Composite Systems）**：GPT-4o+DALL·E 3、Gemini 2.5+FLUX、Qwen3-VL-30B+SD3——LLM作为控制器调调用独立文本转图像模型。
  - **工具增强代理（Tool-Augmented Agents）**：GPT-5（启用Web搜索+Python沙箱）与Gemini 2.5（启用Google搜索Grounding+代码执行环境）。

- **评测指标**：IFC、TFQ、SAS、ITS、CC五项定量指标及总分AVG，全部归一化至0-100。

### 四、资源与算力

- **训练资源**：FactJudge的微调基于Qwen3-VL-8B，在4张NVIDIA A100（80GB）GPU节点上完成，整个微调耗时约4小时。
- **训练配置**：使用AdamW优化器+余弦学习率调度（最大学习率2e-5），训练3轮，全局批次大小128，最大序列长度2048 tokens；LoRA配置为r=64，alpha=16，BF16精度混合训练。
- **注意**：论文正文对FactVerse数据集构建中其他环节所需的算力或人工成本未给出量化说明，附录仅提及数据标注团队的构成与质量控制流程（含补偿超过当地最低工资），未提具体总支出。

### 五、实验数量与充分性

- **实验数量概览**：
  1. **主结果实验**：10个基线模型在FactVerse全量基准上的性能对比（见表2），并细分到四个核心任务的详细面板对比（见图5与附录表5-8）；
  2. **人类对齐消融实验**：将完整FactVerse框架与GPT-4o（整体感知）、以GPT-4o/Qwen3-VL-8B为判官的替代方案、以及移除VQA/移除规则的变体进行Kendall's τ与Spearman ρ对比（表3）；
  3. **组件级别消融实验**：使用留一法（Leave-One-Out）对FactJudge、VQA验证、命名实体召回、CLIP相似度、结构规则检查五个组件逐一进行排名稳定性分析（表4）；
  4. **对抗探针测试**：基于外部ScienceQA数据集构造50个扰动样本，比较FactJudge与基础模型和GPT-4o的识别准确率（表9）；
  5. **四类缺陷的定性案例分析**（图6中展示四个代表性失败模式）。

- **充分性与客观性评估**：
  - 实验设计**较全面**：覆盖三类主流架构（统一模型、管线组合、工具增强代理）、多个粒度（总体/任务细分/组件/定性案例），人类对齐实验包含完整框架、替代范式与组件消融的多层次比较，证据链完整；消融实验中的Δτ可归因至每一个模块。
  - **潜在局限**：① 评测核心依赖FactJudge微调模型，其评估能力上限受限于Qwen3-VL-8B基础能力及微调数据分布，可能存在自我偏好偏差（尽管对抗探测结果在一定程度上缓解了此疑虑）；② 数据集3,000样本覆盖面仍有限；③ 与纯闭源API模型对比时，硬件配置细节未知，即很难完全排除评估时对模型推理资源的差异影响。

### 六、主要结论与发现

- **总体性能分层**：工具增强代理（GPT-5：AVG 67.6、Gemini-2.5：AVG 66.8）> 组合系统（GPT-4o+DALL·E 3：57.8；Gemini+FLUX：56.6；Qwen3-VL+SD3：54.1）> 统一模型（Emu3最高44.6，其余均在39.6~43.0）。工具代理的IFC接近统一模型的两倍。

- **架构性能差异的归因分析**：统一模型在高维跨模态长序列处理上面临可扩展性和计算瓶颈，制约了细粒度事实对齐；组合系统通过LLM控制器获得较强的文本质量和指令合规性，但模态传递过程中的信息损失导致视觉事实保持不佳；工具增强代理通过检索增强的提示精炼、代码解释器确定性执行以及类“系统2”的分层规划，从根本上缓解了上述问题。

- **框架有效性验证**：
  - 完整FactVerse框架与人类判断的Kendall's τ=0.78、Spearman ρ=0.85，远超GPT-4o整体打分方法（0.61/0.67），证明仅依靠通用LLM推理不足以评估交错生成中的事实一致性；
  - 专门微调的FactJudge在管线内性能超过其基座模型Qwen3-VL-8B和GPT-4o，确认了领域特定微调的关键作用；
  - 消融实验表明去除FactJudge造成最严重排名退化（Kendall's τ骤降0.36、平均排名位移4.2），证实三维协同框架的不可替代性。

- **四类系统性缺陷**：
  1. **跨模态属性对齐不足**：文本知识正确（正确叙述招潮蟹不对称螯钳）但视觉生成失败（绘制对称螃蟹），说明模型依赖文本共现统计而非真正物理锚定，语义认知无法可靠转化为细粒度视觉生成保真度；
  2. **空间结构理解不足**：在要求生成内部截面示意图时模型输出通用等轴测视图，源于偏好输出安全且普通的视觉表达而非进行复杂空间推理；
  3. **时间对象漂移**：在多步CPR过程中人物外观在步骤间随机变化，违反对象恒常性，表明当前架构缺少有效的状态追踪机制，将各步骤视为孤立生成事件而非连贯逻辑序列；
  4. **感知与生成的耦合失败**：数据密集型图像识别中，即使强大模型也会出现感知错误；同时预测式模型存在严重数值幻觉——图像视觉元素与文本或基础数据直接矛盾。

### 七、优点与特色

- **填补空白**：首个专门面向交错图文生成事实一致性评测的基准，定位清晰，有效回应现有基准在真实性验证上的系统性缺失；
- **评测框架设计的严谨性和创新性**：突破纯“LLM-as-a-Judge”范式，构建“判别器+锚定VQA+规则约束”的三维协同框架，将评估锚定于可分解的黄金标准，有效缓解了整体性打分的幻觉盲区；细粒度指标各司其职、互补协同；
- **任务设计具有教育学理论支撑**：基于Bloom分类学将人类认知维度映射到四个核心评测任务中，将抽象的事实一致性需求转化为有精细形式化定义的任务约束（如因果图、时间单调性、趋势逻辑）；
- **标注质量控制严格**：采用“双盲标注+专家仲裁”、Fleiss' Kappa一致性量化、安全否决机制及零容忍歧义过滤，最大程度确保基准自身的科学严谨性；
- **方法验证多层次丰富**：既有与人类判断的相关性分析（Kendall τ/Spearman ρ），又有组件级消融（含排名位移量）和对抗泛化探针测试，而非单一主结果，增强了框架可信度；
- **双语支持**：覆盖中英双语，弥补了同类基准对跨语言泛化评测的忽视。

### 八、不足与局限性

- **数据规模受限**：由于人工验证成本高昂，当前3,000条实例可能无法覆盖全部专业领域和复杂边缘情况；虽有50个领域但长尾分布可能造成关键单元样本量不足，统计显著性受限；
- **评测模型泛化风险**：框架部分依赖微调模型，FactJudge 面对分布外错误或新型视觉幻觉的泛化能力仍有限——尽管附加入对抗探针集验证（准确率72%），但其训练素材源自特定模型组合的真实错误+定向构造，可能仍留有评估盲区；
- **未探索闭环训练集成**：该工作主要集中在评测本身，未直接探索将评测反馈整合到模型训练中的闭环应用（如基于FactVerse反馈的强化学习或自修正机制），论文将此列为未来工作；
- **环境不透明性风险**：GPT-4o、GPT-5、Gemini-2.5等闭源模型和DALL·E 3的评估细节、推理策略、工具可用性在不同版本间可能有较大波动，对实验可复现性和公平对比带来一定影响；GPT-5和Gemini-2.5代际较新，基础能力的代差与工具利用增益难以完全剥离归因；
- **任务设计偏科学领域**，架构以“可验证的客观事实”为核心取向，可能限制了对开放创意场景或主观解释性内容事实性的泛化评测；同时部分任务中“事实”认定依赖于人工整理的黄金标准，而这类标准本身在跨文化、跨语言情境中可能存在差异性认知。
- **局限性声明**：论文正文的Limitations部分明确指出：人工成本限制了数据集规模；对细粒度专家标注与自纠错/强化学习闭环整合留待未来工作。

（完）
