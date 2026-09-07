---
title: "Align Documents to Questions: Question-Oriented Document Rewriting for Retrieval-Augmented Generation"
title_zh: 对齐文档与问题：面向检索增强生成的导向问题式文档改写
authors: "Jiaang Li, Zhendong Mao, Quan Wang, Yuning Wan, Yongdong Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.884.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 通过面向问题的文档改写消除检索文档与生成文本间的风格偏差，使模型更依赖检索证据、减少幻觉
tldr: 检索增强生成中，LLM面对混合内容时偏好流畅但可能幻觉的生成内容，而忽略真实但凌乱的检索证据，导致证据价值受限于呈现形式。为弥合这一差距，作者提出QREAM：用两阶段风格受控改写器，将检索文档改写成问题导向风格并保留事实，让LLM能更好利用证据。实验显示QREAM显著减少了模型对检索证据的忽视，提升了回答事实正确性和证据利用率。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 624}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1664, \"height\": 1174}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1567, \"height\": 489}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 658}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 231}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1607, \"height\": 1591}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 295}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 278}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 224}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1716, \"height\": 366}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 754, \"height\": 272}]"
motivation: RAG中模型常偏好流畅但虚构的内容，而忽略真实但杂乱的检索证据，证据价值受呈现形式限制。
method: 提出QREAM两阶段风格受控改写器，将检索文档对齐到问题风格并保留事实，以方便LLM读取。
result: 实验显示QREAM缓解了模型混合上下文中的风格偏置，提升了回答的事实正确性和证据利用度。
conclusion: 事实保留的问题导向文档改写可作为增强RAG模型对证据依赖的通用前端方法。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances the factuality of Large Language Models (LLMs) by incorporating retrieved documents and/or generated context. However, LLMs often exhibit a stylistic bias when presented with mixed contexts, favoring fluent but hallucinated generated content over factually grounded yet disorganized retrieved evidence. This phenomenon reveals that the utility of retrieved information is bottlenecked by its presentation. To bridge this gap, we propose QREAM , a style-controlled rewriter that aligns retrieved documents with a question-oriented style while preserving facts, better for LLM readers to utilize. Our framework consists of two stages: (1) QREAM-ICL , which uses stylistic seeds to guide iterative rewriting exploration; and (2) QREAM-FT , a lightweight student model distilled from denoised ICL outputs. QREAM-FT employs dual-criteria rejection sampling, filtering based on answer correctness and factual consistency to ensure high-quality supervision. QREAM seamlessly integrates into existing RAG pipelines as a plug-and-play module. Experiments demonstrate that QREAM consistently enhances advanced RAG pipelines, yielding up to 8% relative improvement with negligible latency overhead, effectively balancing question relevance with factual grounding.

---

## 论文详细总结（自动生成）

# QREAM 论文详细中文总结

## 1. 核心问题与研究动机

检索增强生成（RAG）通过引入外部知识来提升大语言模型（LLM）的答案事实性，是缓解知识更新滞后、知识缺失和幻觉问题的重要技术路径。然而，作者指出当前 RAG 系统存在一个被忽视的关键瓶颈——**LLM 读者的“风格偏置”（Stylistic Bias）**：当模型同时面对两种类型的内容时——

- **检索文档**：事实准确性高，但结构松散、内容冗余、与问题相关性不足；
- **生成文档**：由 LLM 对提问直接生成，风格流畅且紧扣问题，但易于产生幻觉。

LLM 读者会显著偏好后者，即使前者的内容在事实上是正确的。这意味着**检索信息的可用性被其呈现形式所“瓶颈化”**——即便证据正确，若表达凌乱，模型也不愿意采用。

该论文的核心问题即：**如何弥合检索文档与生成文档之间的呈现差异，将真实、杂乱、非问题导向的检索证据转化为既保留事实、又具备生成文本“问题导向风格”的形式，从而提高 RAG 中证据的利用率？**

## 2. 方法论：QREAM 框架

### 2.1 核心思想

QREAM（**Q**uestion-oriented document **RE**writing for Effective **A**nswering **M**odels）将 RAG 中生成式 LLM 的角色重新定义为 **“风格可控、内容受事实约束的改写器”（style-controlled, content-grounded rewriter）**，而非自由文本生成器。其目标是将检索文档 R 重写为 `R̃`，使之同时满足：

- 风格上与问题对齐（仿真生成文本的流畅性、结构清晰度）；
- 事实内容与原检索证据严格一致（保留检索证据的可靠性）。

QREAM 整体是一个即插即用的检索后处理模块，可无缝嵌入现有 RAG 管线。

### 2.2 总体范式：Explore-then-Distill（先探索，再蒸馏）

受限于“不存在已标注的问题导向文档”，QREAM 采用两阶段训练框架：

- **Stage I — QREAM-ICL（上下文学习探索）**：生成大量风格各异的问题导向改写候选，从中进行探索性采样；
- **Stage II — QREAM-FT（蒸馏训练）**：通过双向去噪策略过滤候选，构建高质量监督数据训练轻量级学生模型。

### 2.3 Stage I：QREAM-ICL 迭代式风格探索

**（1）风格种子生成（Stylistic Seeds Generation）**

- 从训练集中采样 M 个与目标任务无关的问题 `{q̂ᵢ}`；
- 用一个 LLM 生成器 `M_Gen` 为每个问题生成一段“背景材料”风格的文档 `gᵢ`；
- 这些 `(q̂ᵢ, gᵢ)` 对作为 few-shot 演示 `E`。

关键设计：**种子问题与目标问题无关，从而将“风格”与“内容”解耦**——改写器模仿的是形式结构，而非照抄种子中的事实内容，避免内容干扰和幻觉注入。

**（2）迭代改写（Iterative Rewriting）**

- 第一轮：将检索文档拼接为 `r_raw`，利用模板、种子演示 `E`、问题 `q` 生成第一版改写 `r̃₁`；
- 后续每一轮：截取上一轮输出的前 l 个 token（保留高密度信息并控制上下文长度），继续改写，迭代 N 轮；
- 得到候选集 `C_q = {r̃₁, ..., r̃ₙ}`。

### 2.4 Stage II：双向去噪蒸馏（Bidirectional Denoising Distillation）

QREAM-ICL 的迭代输出必定包含噪声（幻觉、冗余、错误内容），若直接蒸馏会污染学生模型，因此设计**双标准拒绝采样**来筛选高质量候选：

**（1）下游效用检查（Downstream Utility Check）**

- 将候选改写喂入固定 QA 读者 `M_Read`，得到预测答案 â；
- **硬性过滤**：若预测文本中不包含标准答案字符串（a* ∈ â），则直接剔除；
- 对幸存候选计算 token 级 F1 得分作为性能分数 `S_perf`；

**（2）上游保真检查（Upstream Fidelity Check）**

- 采用类似 FactScore 的原子事实分解验证方法：将改写文本分解为多个原子事实 F；
- 逐个判断每个事实是否能由原始检索文档 `r_raw` 推导（文本蕴含）；
- 一致性分数 `S_fact` = 被支持事实占比；

**（3）综合质量评分与教师数据构建**

- 综合分数取两者均值：
  `S_total = ½(S_perf + S_fact)`
- 每个问题选取 S_total 最高的候选作"黄金改写" r̃*，过滤掉完全没有候选通过硬性检查的问题。

**（4）学生模型训练**

- 将数据和指令模板 `T_FT` 封装后，微调轻量级学生模型 `M_Student`，目标函数为最大化黄金改写的生成对数似然。

## 3. 实验设计

### 3.1 数据集与 Benchmark

选取 4 个开放域问答（ODQA）基准数据集，涵盖单跳和多跳推理：

- **Natural Questions（NQ）**——单跳
- **TriviaQA（TQA）**——单跳
- **HotpotQA**——多跳
- **2WikiMultiHopQA（2WikiMQA）**——多跳

使用标准官方划分和评估协议，报告 **Accuracy（Acc）** 与 **token-level F1**。

### 3.2 基线对比

对照方法分为三类：

| 类别 | 方法 |
|------|------|
| 标准 RAG 管线 | 仅检索文档、仅生成文档（Generated Doc.）、两者拼接（Retrieved + Generated） |
| 后检索处理/压缩 | LongLLMLingua、CompAct（主动压缩）、RECOMP（抽取式压缩）、FaviComp（熟悉度感知融合） |
| 高级 RAG 框架 | Self-RAG、HippoRAG（集成 QREAM 后验证即插即用能力） |
| 专有强模型验证 | GPT-5 mini（更强读者上的效果验证，附录 D） |

### 3.3 读者与组件配置

- 检索器：Contriever-MSMARCO（top-5）
- 读者骨干：Llama-3-8B-Instruct、Mistral-7B-Instruct-v0.3
- QREAM-ICL：M=4 个风格种子，N=3 轮迭代，截断长度 l=100
- 学生模型：Llama-3.2-1B-Instruct，微调数据量 4,000 条（每数据集 1,000）

## 4. 资源与算力

论文正文及附录**未明确披露具体的训练硬件配置、GPU 型号/数量、微调时长或浮点运算量**。

文中仅可从间接信息推断出：

- QREAM-FT 使用 **1B 参数量**的 Llama-3.2-1B-Instruct 微调；
- 蒸馏数据规模较小（4,000条样本），推测训练算力需求不大；
- 推理阶段增强了速度：在 NQ 上的端到端延迟为 **0.18s**（标准 RAG 为 0.16s，QREAM-ICL 为 2.41s），说明 1B 蒸馏模型带来约 **13 倍速度提升**。

如果读者关心可复现性所需的精确算力配置，论文并未提供。

## 5. 实验数量与充分性

整体实验设计较为全面，共包含以下实验模块：

### 5.1 主要实验

- **主实验（两种读者 × 四个数据集 × 十余种对比方法）**：完整表格覆盖 QREAM-ICL、QREAM-FT 与所有基线在 Acc 和 F1 上的对比，且在每个 Read 骨架下都给出了完整数据；
- **先进框架集成**：Self-RAG、HippoRAG 上的叠加增益验证；
- **更强大专有模型验证**（GPT-5 mini，附录 D）。

### 5.2 分析实验（消融与机制验证）

| 实验 | 验证目标 | 结论 |
|------|---------|------|
| 蒸馏标准消融（无过滤/仅效用/仅保真/双标准） | Stage II 双向去噪必要性 | 双标准过滤最优，F1 最高、幻觉率最低 |
| 风格种子消融（零样本重写/自重构/无关种子 + 不同数量示例） | Stage I 设计和种子来源 | 无关的种子优于目标问题自身生成的种子；M=4 时性能饱和 |
| 上下文冲突（CC）实验 | 是否缓解读者的风格偏置 | 使用 QREAM 改写后，NQ-CC 上准确率从 19.4% 大幅提升到 77.4% |
| 风格对齐与幻觉定量评估（s_orient、r_inc） | 是否达成“风格接近生成文本、幻觉率接近检索文档”的目标 | 是，风格得分接近生成文档，幻觉率接近原始检索 |
| 定性案例比较 | 与最优基线 FaviComp 对比 | 基线留下干扰实体和歧义逻辑，QREAM 做改写后正确 |
| 提示指令鲁棒性（附录 C） | 是否过度依赖特定 prompt 措辞 | 5 种指令变体上性能波动不超过 0.8 F1 |
| 迭代轮数灵敏度（附录 B） | N 的取值影响 | 饱和于 N=3，首轮即已有较大提升 |
| 效率分析 | 计算开销 | QREAM-FT 相对 ICL 教师模型延迟降低约 13 倍，几乎与标准 RAG 持平 |

### 5.3 充分性评价

**优点**：实验矩阵较为完整——横跨多类基线、多种流水线、两种开源读者 + 一种专有读者，辅以针对方法核心设计要素的消融、有效性分析和效率分析，能支撑论文的核心论断。

**可改进之处**：

- 蒸馏只用 4 个数据集各 1,000 条（合计 4,000）样本，样本规模较小，虽可解释轻量级模型的良好性能，但其跨数据集泛化和更大数据的扩展性未验证；
- 仅验证了单一检索器（Contriever-MSMARCO）和单一学生模型架构（Llama-3.2-1B），没有验证检索器变化、学生规模变化对下游性能的影响；
- CC 实验中只测试了两个数据集（NQ-CC 与 TQA-CC），若能扩展到多跳 CC 场景会更有说服力。

## 6. 主要结论与发现

1. **检索文档的呈现形式显著制约其效用**。LLM 读者对“流畅、问题导向风格”的内容有天然偏好，即便生成的文本存在幻觉；这一发现验证了论文的出发点——实际瓶颈不仅在于证据信息是否存在，还在其如何呈现。
2. **QREAM 的“探索—蒸馏”机制有效**。QREAM-ICL 通过风格种子和迭代改写即可超过所有现有后检索处理方法；而蒸馏后的 QREAM-FT（1B 参数）在准确率上基本匹配甚至超越 8B 教师的 ICL 版本，并在部分数据集上反超。
3. **双向去噪蒸馏是性能的关键**。只有在“下游效用 + 上游保真”双重过滤下训练学生模型，才能获得高回答正确率且低幻觉率的改写结果（幻觉率从 14.8% 降至 9.2%）。
4. **QREAM 是通用即插即用增强模块**。无论嵌入标准 RAG 管线，还是高层次框架 Self-RAG 与 HippoRAG，乃至与专有 GPT-5 mini 搭配，均获得一致的增益——相对提升最高达 8%。
5. **风格偏置可被消解**：上下文冲突（CC）中，原始检索的可用率从 19.4% 提升到 77.4%，证明在风格对齐后模型会真正采纳检索证据。
6. **实际部署效率可行**：QREAM-FT 的端到端延迟（0.18s）接近未改写的标准 RAG 管线（0.16s），满足实时部署需求。

## 7. 亮点与创新之处

1. **问题视角新**：此前 RAG 后处理研究（如 RECOMP、FaviComp）侧重于压缩/去噪/融合，而 QREAM 首次关注“文档的呈现风格”这个维度，敏锐地定量刻画并利用 LLM 读者的风格偏置，提出了用“问向格式”对齐检索文本这种低成本且有效的数据增强思路。
2. **风格与内容的解耦式种子构造**：用不相关的问题作为风格种子是一个巧妙的设计。它使模型只能学习目标风格的结构模式（如何组织一个问答式回答），无法照抄种子中语义内容，从源头隔离了事实干扰。
3. **迭代改写“探索” + 蒸馏“利用”的两阶段流程**：将 LLM 当作候选采样器来产生多样化的候选改写，再通过严格筛选提炼出高质量监督信号，既保留了 LLM 改写器的风格表达能力，也通过蒸馏实现了速度与噪声控制的最优平衡。
4. **双向去噪蒸馏信息**：同时考虑下游（读者是否能得到正确答案）与上游（内容是否忠实于原始证据），实际上把 QA 最终效果和证据保真两个目标统一到了数据筛选标准中，思路清晰且通用。
5. **全方位、定量的分析实验**：论文定义了“风格对齐分数”和“事实不一致率”两个定量指标，用数据而非仅凭端到端指标证明方法确实达到了风格/事实两个目标的最优折衷。CC 实验更是直接对照了偏置消除效果。
6. **即插即用且具泛化性**：能兼容各类 RAG 系统（自研、已有框架、专有模型），无需修改检索器和读者，适配性好。

## 8. 不足与局限

### 8.1 作者自述的局限

- **依赖检索质量**：QREAM 假定“检索已完成”，未结合检索器训练或重排序进行联合优化。若初始检索本身有缺失或引入了无关内容，QREAM 无法凭空恢复真实现象，会继承检索环节的缺陷。

### 8.2 其他值得指出的局限

1. **实验覆盖的广度局限**：
   - 仅在“单跳 + 多跳”开放域问答数据上验证；知识密集型任务还包括事实验证、长文本问答、代码/科学领域等，结论推广性存疑；
   - 只对单一检索器、单一学生规模（1B）进行评估，未评估不同检索质量水平或不同学生规模假设下的行为变化。
2. **蒸馏数据规模偏小**（4,000 条），大规模数据蒸馏的效果是否仍能维持，未经探索。
3. **幻觉率仍然不为零**——QREAM-FT 重写的文档包含约 9.2% 的原子事实未被原始检索文档支持的事实。幻觉被最大程度抑制但并未消除。
4. **风格对齐的语义定义依赖语言模型评价**——风格对齐分数（s_orient）本身是另一种 M_Gen 生成式的概率度量，可能带有与目标任务相似的偏置或噪声；不同读者/生成器选择会对评估结果产生潜在影响。
5. **不同 reader 上的鲁棒

5. **不同 reader 上的鲁棒性验证不足**。QREAM-FT 的训练与调参主要建立在 Llama-3 家族读者上，专有模型验证（GPT-5 mini）被放在附录作为补充。对于与 Llama 指令风格差异较大的读者——例如编解码器架构、前缀式 LM 或经由不同 SFT 范式对齐的模型——QREAM 改写是否依然能保持稳定增益，是一个悬而未决的问题。此外，蒸馏阶段选择的黄金改写依赖于特定读者的反馈信号，这意味着教师数据在某种程度上已与某一读者耦合，读者迁移时可能需要重新蒸馏。

6. **缺乏细粒度失败模式分析**。对于未通过硬性过滤的问题、或经过重写后读者依然答错的样本，论文没有给出系统的错误归因——究竟是检索内容本身不含答案、改写过程丢失关键实体、还是读者仍受残留风格干扰？这种“端到端增益 + 部件级指标”的分析策略，使得方法头上仍留有几层黑箱。

7. **评测以字符串匹配为主，缺乏生成质量人工评测**。论文的主指标 Acc 和 token-level F1 依赖于标准答案字符串匹配，无法细致刻画生成答案的完整语义质量与可读性。对于经过改写的证据最终如何影响读者生成答案的连贯性、逻辑性和用户感知可信度，未提供人工评测或 LLM 多维评估结果。

8. **语言覆盖与跨领域泛化有限**。所有实验均基于英文开放域问答。对中文、低资源语言，以及知识密集型文本生成（如报告撰写、事实验证）等场景中风格偏置的强度与 QREAM 的迁移效果，论文不提供证据。

9. **“风格偏置”的机理刻画仍偏表层**。文章通过 CC 实验和风格分数证明读者“偏好问题导向文本”，但未深入剖析偏置的来源——例如是否源于指令微调阶段训练数据的格式分布、解码先验（decoding preference）位置，还是注意力机制对结构化文本的天然亲和。若该机制没有被真正解释清楚，后续面对新读者时“风格对齐到什么程度才够”只能继续依赖经验调参。

### 8.3 潜在风险与负面影响考量

- **可用于掩盖来源的改写**：QREAM 将检索证据改写为一种“类生成”表达，客观上降低了文本在风格上与原始来源的区隔度。在需要明确区分模型内在知识与外部证据的场景中，这类改写可能增加溯源（attribution）与引用核查的难度——尽管它保留内容上的忠实性，却抹平了“人读起来像引用”的语体痕迹。
- **双过滤的隐式偏向**：蒸馏筛选把“读者是否命中标准答案”作为首要效用信号，可能偏向只重写那些答案吻合度较高的样本，导致学生模型在困难问题上缺乏泛化，也就是存在一定 **selection bias**——它学到的模式可能仅适用于中等难度问题分布。

## 9. 综合评价与总结

**QREAM 是一篇完成度较高、叙事清晰且方法可复现性较强的 RAG 后处理研究。** 其价值来自于三个层面：

- **现象层面**：它通过 CC 等实验有力地展示了一个此前未被充分量化的 RAG 瓶颈——即“证据有用性不仅取决于事实正确性，还取决于文体呈现是否迎合 LLM 读者的解码先验”。这个现象本身对 RAG 社区便有启发意义。
- **方法层面**：“Explore-then-Distill，而 Distill 环节又双指标把关”的设计，在“高性能教师 ICL 改写”与“低延迟轻量学生模型”之间做了一次实用且优雅的折衷。用户无需重训检索器或读者就能获得增益，工程上的性价比很高。
- **实证层面**：多数据集 × 多读者 × 多基线的实验矩阵，再叠加风格对齐/事实率的定量分析，支撑了论文“风格重写为何有效”的因果链解释，而非简单的屠榜式汇报。

同时需要看到，QREAM 的目标是**工程性缓解而非机理性解决风格偏置**——它通过格式转换来提高证据被采纳的概率，但读者的内在偏好依旧存在。未来沿着“可控改写 + 读者解偏 + 证据链显式监督”方向继续深入，将可能产生更彻底、更可溯源的方案。

总体而言：**推荐关注 RAG 后处理、上下文压缩、证据表达学习与检索噪声鲁棒性的研究人员阅读；作为即插即用模块，也值得在真实的 RAG 产品管线中试点验证其实际收益。**

（完）
