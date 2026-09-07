---
title: "ReFEree: Reference-Free and Fine-Grained Method for Evaluating Factual Consistency in Real-World Code Summarization"
title_zh: ReFEree：面向真实代码摘要的无参考细粒度事实一致性评测方法
authors: "Suyoung Bae, CheolWon Na, Jaehoon Lee, Yumin Lee, YunSeok Choi, Jee-Hyong Lee"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.653.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 提出无需参考、细粒度的代码摘要事实一致性评测方法，评估生成摘要与源代码间的忠实度
tldr: 真实世界的代码摘要往往多语句且依赖上下文，而现有事实一致性评测主要针对孤立代码片段，难以细粒度定位错误。本文定义了面向代码摘要的事实不一致准则，提出ReFEree，一种无需参考的细粒度评测方法，能够评估多句功能及依赖上下文。实验显示ReFEree可以更准确地发现代码摘要中的事实不一致问题，为摘要一致性评测提供了可迁移的细粒度方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long653/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 881, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long653/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1637, \"height\": 920, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long653/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long653/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long653/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1649, \"height\": 784, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 505, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1663, \"height\": 929, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 522, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 814, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 813, \"height\": 894, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 814, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 811, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1659, \"height\": 1208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 812, \"height\": 709, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 808, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 574, \"height\": 822, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 808, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 807, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 813, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 811, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 807, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 811, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1670, \"height\": 2280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1641, \"height\": 2160, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long653/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1650, \"height\": 1581, \"label\": \"Table\"}]"
motivation: 现有摘要一致性评测主要面向孤立短摘要，难以评估真实世界代码摘要的多句功能和依赖上下文。
method: 提出ReFEree，一种无参考细粒度方法，定义面向代码摘要的事实不一致准则并进行评估。
result: 实验证实ReFEree能够更准确地识别真实代码摘要中的事实不一致内容。
conclusion: 该方法可支持对代码摘要及类似长摘要进行细粒度的事实一致性自动评测。
---

## Abstract
As Large Language Models (LLMs) have become capable of generating long and descriptive code summaries, accurate and reliable evaluation of factual consistency has become a critical challenge. However, previous evaluation methods are primarily designed for short summaries of isolated code snippets. Consequently, they struggle to provide fine-grained evaluation of multi-sentence functionalities and fail to accurately assess dependency context commonly found in real-world code summaries.To address this, we propose ReFEree, a reference-free and fine-grained method for evaluating factual consistency in real-world code summaries. We define factual inconsistency criteria specific to code summaries and evaluate them at the segment level using these criteria along with dependency information. These segment-level results are then aggregated into a fine-grained score. We construct a code summarization benchmark with human-annotated factual consistency labels. The evaluation results demonstrate that ReFEree achieves the highest correlation with human judgment among 13 baselines, improving 15-18% over the previous state-of-the-art. Our code and data are available at https://github.com/bsy99615/ReFEree.git.

---

## 论文详细总结（自动生成）

# ReFEree：面向真实代码摘要的无参考细粒度事实一致性评测方法

## 一、核心问题与整体含义

**(1) 研究动机与背景**

- 随着 GPT-4 等大语言模型（LLMs）被越来越多地用于代码理解与解释，代码助手（如 GitHub Copilot、Claude Code）能够生成长篇、描述性的代码摘要。这类摘要若与代码实际实现不符，会直接误导开发者，造成调试滞后、维护成本提升，因此**对摘要事实一致性的准确评估变得至关重要**。
- 现有评测方法存在两大局限：
  - **参考（reference）依赖型方法**（如 ROUGE、BLEU、BERTScore）：依赖人工参考摘要，而代码摘要是一对多任务，词汇重叠无法体现语义正确性，且常因参考质量不佳而产生误判。
  - **无参考 LLM 评测方法**（如 LLM-judge、G-Eval、FActScore、CODERPE）：把摘要看作整体，仅凭 LLM 内部知识给出单一粗粒度分数，缺乏可解释性，无法定位不一致的具体句子或原因。
- 更关键的问题是：**真实世界代码中的函数/类常依赖外部定义**，摘要经常会描述这些外部依赖元素。现有方法只将输入代码作为上下文，无法验证这类外部依赖描述的准确性。

整体含义：该论文试图填补“真实代码环境下的长摘要在细粒度层面的事实一致性自动评测”这一空白。

## 二、方法论（ReFEree）

**(1) 核心思想**

- 提出一种**参考无关（reference-free）且细粒度（fine-grained）**的评测框架。
- 核心思路：**先定义专门的代码摘要事实不一致准则 → 用静态代码分析构建依赖关系 → 摘要按句切分后用 LLM 针对每个准则逐一评估 → 将各片段分数聚合为总体一致性分数**。

**(2) 关键技术细节**

**① 四种事实不一致准则（Factual Inconsistency Criteria）**

| 准则 | 定义 | 在人工标注中的出现比例 |
|---|---|---|
| C1 名称不一致 | 摘要中的函数/类/变量名称与实际代码标识符不符，或误指项目中同名实体 | 14% |
| C2 类型不一致 | 摘要所描述的返回类型/变量类型与实际代码或直接依赖函数中的类型不一致 | 15% |
| C3 功能不一致 | 摘要所描述的功能与代码实际实现不符，常源于忽略/曲解依赖关系 | 35% |
| C4 上下文无关 | 摘要含与输入代码不相关/无法从代码验证的冗余、幻觉式内容 | 33% |

（另有 3% 为重复等次要问题。准则的确立基于 300 个人工分析的 LLM 生成摘要，涉及 Qwen2.5-Coder、CodeLlama、GPT-4 三种模型。）

**② 代码相关信息搜索（Searching Code-Related Information）**

论文利用**基于 AST 的静态程序分析**思路，分两步获取外部依赖证据：

- **Step 1 — 构建项目上下文图**：遍历项目仓库中的每个文件，解析 AST，构建异质有向无环图，将函数、类、变量等实体作为节点，数据依赖关系（Assign、Refers、Typeof、Inherits 等）作为有向边。
- **Step 2 — 选择核心相关信息**：
  - 从输入代码中的每个实体做深度有限搜索（DFS），在项目上下文中找到直接依赖实体；
  - 只保留输入代码中被调用的**核心实体**（函数、类、变量）对应的 1 跳（1-hop）依赖关系，避免深层检索带来的噪声；
  - 跨文件依赖 → 在项目对应模块里精确匹配实体代码；
  - 第三方库/内置模块等外部依赖 → 从外部 API 文档中检索对应解释；
  - 结果以 `# 名称 # 内容` 的注释形式附加到输入代码前面，作为评测上下文。

**③ 句子级准则评测器（Segment-Level Evaluator）**

- 用 NLTK 句子分词器将摘要 D 切分为句子集合 `D = {S₁, ..., S_n}`；
- 构造准则评测 prompt，将“相关依赖信息 + 输入代码 + 单句摘要片段”输入 LLM，判定该句针对某一准则是否存在不一致（存在=0，不存在=1）。

**④ 总体一致性分数公式**

$$\text{SCORE} = \frac{1}{|D| \times |\text{Criteria}|} \sum_{S \in D} \sum_{C \in \text{Criteria}} f(S, C)$$

- 分数范围 0~1，每个句子对四个准则逐项判断后等权加总。
- 该分解-聚合（decompose-and-aggregate）方式，同时实现了细粒度与可解释的评判。

## 三、实验设计

**(1) Benchmark 构建——核心特色**

- 实验团队自行构建了包含**人工标注**的代码摘要事实一致性基准（此前无类似基准）：
  - **代码来源**：从 DevEval（115 个 Python 真实仓库）提取 1,825 个 Python 函数；从 ClassEval（10 个 Java 仓库）提取 230 个 Java 函数；
  - 约 86% 为非独立函数，含跨文件依赖；
  - **摘要生成**：使用 ChatGPT（chatgpt-4o-latest）生成长篇描述性摘要，并**刻意引导生成包含至少一句事实不一致内容的摘要**；
  - 标注分**摘要级（1~5 分）**与**片段级（每句对 C1~C4 每个准则标注 CORRESPOND / NOT CORRESPOND）**；
  - 采用三种 LLM 多数投票提出候选标签 + 三名 CS 背景人类标注者事后修正的人工–AI 协作模式；标注者间一致性达到摘要级 Krippendorff's alpha = 0.74、片段级平均 0.84，信度较高。

**(2) 对比方法（13 种基线）**

- **参考型方法（8 种）**：ROUGE-1/2/L、BLEU、METEOR、BERTScore、SBCS、SBED；
- **无参考型方法（5 种）**：SIDE、LLM-Judge、G-Eval、FActScore、CODERPE；
- 评测指标：Pearson、Spearman、Kendall Tau 三种相关性系数。

## 四、资源与算力

- 论文仅提供了评测阶段的模型调用和成本数据，**没有明确报告任何 GPU 硬件型号、数量或训练时长**。
- 评测器：主要使用 OpenAI 的 **GPT-4.1-mini**；在泛化实验中额外调用了 Llama3-8B、Mistral-7B、Qwen2-7B、Qwen2.5-Coder-7B、GPT4o-mini。
- 每次评测的 API 成本约为 **0.004 美元/样本**，远低于 DecompFactScore（0.0058/样本）。
- 每样本推理时长约 10.24 秒；生成 2,055 条“幻觉摘要”的成本约 250 美元，摘要级和片段级预标注的成本分别约 300 与 800 美元。
- 结论：该工作属于非训练、推理/评测类研究，对大规模 GPU 算力的需求很低。

## 五、实验数量与充分性

论文共进行了**两大类共 7 组以上实验**，覆盖面较广：

| 实验类别 | 内容 |
|---|---|
| 主要对比实验 | 在 Python 与 Java 基准上，与 13 种方法比较三种相关性系数，重复三次取平均，p < 0.005，统计显著 |
| 消融实验 | ① 比较 ReFEree (w/ info) 与 ReFEree (w/o info)，验证依赖信息搜索模块的作用；② 比较全准则（C1~C4）与使用单个准则的权重消融 |
| 片段级评测 | 报告对四种准则的片段级识别准确性（两种语言的平均准确率 0.93 以上） |
| 泛化实验 | 将 ReFEree 的评测器替换为 6 种不同的 LLM（从开源小模型到闭源大模型），验证其对不同评测器的泛化性 |
| 稳定性实验 | 在改变 prompt 模板与改变随机种子两种条件下，比较 IAA 稳定性 |
| 其他验证 | 1-hop/0-hop/2-hop 检索效果对比；加权 vs 等权准则聚合对比；人类写摘要上的适用性；摘要长度鲁棒性；failcase 分析 |

**充分性评估**：

- 优点：Python+Java 双语言、真实仓库场景、从参考型到 LLM-judge 的丰富基线、多语言泛化测试、统计显著性校验齐全，客观性与对照公平性较好；
- 不足：仅覆盖 Python/Java 两种语言，未覆盖 JavaScript/TypeScript/Go 等；全部实验以相关性和 IAA 为指标，没有执行成本/可用性方面的更深入分析；片段级准确率仅在自建基准上测得（生成摘要时已故意包含不一致，与自然分布存在偏差）；此外人类标注过程用了 Human-AI collaboration，虽然在附录中提供了 89.5% 的对照一致性，但这可能无法完全消除模型对人工标注的系统性影响。

## 六、主要结论与发现

1. **与人类判断的相关性全面领先**：ReFEree 在 Python、Java 上分别比此前最强的无参考基线 G-Eval 提升约 15% 和 18% 的平均相关性。
2. **引入依赖信息至关重要**：去除相关信息搜索模块后，相关性降低约 0.05，证明外部信息是真实代码摘要一致性评估的关键环节。
3. **细粒度高准确度**：片段级评估器对 C1~C4 的判定准确率达 93% 上下，能够精确告诉用户哪一句错、属于哪一类错误。
4. **四项准则缺一不可**：单准则消融中，仅用功能/类型一致性损失的性能较小，仅用名称一致性性能下降最多，说明类型一致性和功能一致性在人类判断中权重更高。
5. **泛化性与稳定性良好**：更换底层评测 LLM 均保持对 G-Eval 的一致优势；在不同随机种子下 IAA 高达 0.89~0.90，远优于 G-Eval 在 Java 上的 0.712。
6. **错误模式**：依赖数量超过 11 个时 C3/C4 的错误率上升较快；跨文件和外部依赖比文件内依赖更难评估。C1 和 C4 更容易误报（false positive）。

## 七、优点与亮点

1. **问题定义清晰、针对性强**：鲜明指出真实代码摘要“跨句功能、外部依赖”两大特点，并围绕它们设计完整方案，切中现有方法痛点。
2. **从人工样本中归纳准则**：四种不一致准则通过 3 种 LLM 的 300 个摘要 + 3 名人工标注者分析总结而来，不是拍脑袋制定的 rubric；有明确的准则分布和大量真实样例支撑。
3. **模型无关、可解释的细粒度评测**：LLM 仅承担“输入的每个句子是否违反每项准则”的二元判断，最终得分由分解公式算得，不靠模型内部知识直接打分；输出可以定位到“第几句、哪类错误”，比“整篇 1~5 分”更有实用价值。
4. **工程贡献扎实**：用 AST + DFG + 依赖检索，实现低成本（无需训练、每次 0.004 美元），并给出 1-hop/2-hop 的有效性对比。
5. **基准构建规范度高**：自建 benchmark 采用人机协同标注，报告了两种信度指标，并证明了人机标注与纯人工标注的相关性（Pearson 0.94），该基准对社区后续研究有较大价值。
6. **实验设计相对全面**：涵盖双语言、13 基线、多种 LLM 的泛化、prompt/seed 敏感性、长度鲁棒性和失败模式分析。

## 八、不足与局限

1. **语言覆盖有限**：只验证 Python 和 Java；未能证明对 JavaScript、Go、Rust 等主流语言的适用性，而这些语言的依赖解析方式差异较大（如 JS 的动态导入与 npm 生态）。
2. **无法处理动态语言特性**：依赖 AST 静态分析，对 Python 的动态分派（dynamic dispatch）、运行时动态生成代码等场景识别能力有限；论文虽称此类实体只占 0.07%，但这一统计仅基于当前 benchmark 数据，不能完全排除真实开发环境中的盲点。
3. **评测模型的分数分布依赖分段方式**：总分 = 不一致句子的比例；若总结句子长度不均匀或过长，可能影响粒度与可比性。
4. **没有对评测本身与下游影响的联合研究**：仅验证了相关性，未证明以 ReFEree 为奖励信号/反馈能否真正帮助 LLM 生成更一致的摘要（缺少将评测器用于迭代修正的应用性检验）。
5. **故意引入幻觉的 benchmark**：为覆盖四种准则而刻意引导生成包含不一致内容的摘要，虽然是基于真实错误

5. **故意引入幻觉的 benchmark**：为覆盖四种准则而刻意引导生成包含不一致内容的摘要，虽然是基于真实错误模式（300 条人工分析样本）设计的，但这种构造方式使不一致句子的比例显著高于自然分布，可能高估评测器在实际场景中的判别能力；同时“人为诱导 + 人机协同标注”可能引入系统性偏差，无法完全代表真实用户随手生成的摘要分布。

6. **对摘要本身的结构假设较强**：评测流程依赖于句子级切分（NLTK 分词器），当摘要包含代码块、公式、项目符号列表或碎片化短语时，切分质量会下降，从而影响“逐句 × 逐准则”的聚合得分精度；论文虽进行了长度鲁棒性分析，但未对完全非叙述性摘要（如纯列表式）做专门验证。

7. **静态分析对第三库依赖的解释存在边界**：对第三方库/内置模块采用“外部 API 文档检索”方式补充证据，但若文档不完整或版本不匹配，检索到的信息可能与实际代码语义不一致，从而干扰评测器判断。

8. **未展示评测器对恶意或对抗性摘要的鲁棒性**：实际中模型可能生成“表面流畅但逻辑混淆”的摘要，这种摘要不易在二元“不一致/一致”判定中被稳定识别；论文未报告这类边缘样本的失败率。

## 九、改进方向与未来工作

1. **语言扩展与跨语言验证**：将 AST/DFG 依赖提取模块推广到 JavaScript、TypeScript、Go、Rust 等主流语言，并针对各语言特有的依赖解析机制（如动态 `import`、接口实现）做适配，验证 ReFEree 的通用性。

2. **静态 + 动态分析相结合**：对 Python 等动态语言的运行时行为，可引入执行追踪（execution tracing）、类型推断或轻量动态分析工具，在不显著增加成本的前提下补足静态分析无法覆盖的动态分派路径。

3. **建立自然分布的无偏基准**：在真实开发者/模型生成的摘要中按自然频率采样（而非刻意诱导不一致），配合纯人工标注，构建更贴近实际部署场景的评测集，以更可靠地评估方法在实际中的查准率与查全率。

4. **将评测器用于“以评促改”闭环**：将 ReFEree 的细粒度反馈（第几句、属于哪类不一致、可能的证据）作为强化学习奖励信号或 LLM 自修正的输入，验证其能否有效提升模型生成的摘要事实一致性，这是从“评测指标”走向“实际应用价值”的关键一步。

5. **优化片段切分与证据追溯**：引入文本分割模型或多模态解析（把代码块/列表也作为段落单元），并在输出中对每个不一致判断给出可读的代码证据片段，进一步增强可解释性与工程师的实用体验。

## 十、总体评价与结论

ReFEree 的核心价值在于：**把真实代码摘要评测从“依赖参考的整体打分”推进到“无参考的细粒度事实核查”**。它充分利用了代码结构（AST + 依赖图）与 LLM 推理能力，通过“四类不一致准则 + 外部依赖感知 + 句子级分解聚合”实现了高相关性、高可解释性和低成本，并在 Python/Java 双语言基准上以全面优势超越 13 种基线方法。

其方法论上最值得借鉴的设计是：不是让 LLM 直接输出分数，而是将评测任务分解为“有明确语义边界、可验证、可追溯”的细粒度判断，并配以与代码事实强相关的证据上下文；这种“分解-验证-聚合”范式对代码摘要乃至更广泛的自然语言生成事实一致性评测都具有示范意义。

当然，作为一篇以评测框架为核心的论文，它在语言覆盖面、真实分布基准、动态代码处理及“评测-生成”闭环方面仍留有开放问题。但从现阶段实验结果看，它已为代码辅助工具的输出质量控制提供了一个可靠、实用且廉价的自动化评测基础。

（完）
