---
title: "Analyzing LLM Behavior in Dialogue Summarization: Unveiling Circumstantial Hallucination Trends"
title_zh: 分析大语言模型在对话摘要中的行为：揭示情境性幻觉趋势
authors: "Sanjana Ramprasad, Elisa Ferracane, Zachary C. Lipton"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.677.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 通过人工跨度标注评测大模型对话摘要忠实度，揭示看似合理但缺少对话支持的内容
tldr: 针对对话摘要任务中以往评估集中于BART等小模型、对大模型幻觉认识不足的问题，以人工标注对GPT-4与Alpaca-13B的摘要进行跨度级不一致检测与分类。结果显示LLM常生成流畅但未被对话支撑的幻觉内容，系统性揭示出情境性幻觉趋势。该工作填补了LLM对话摘要忠实度评测空白，有助于设计更可靠的摘要模型和评测方案。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 723, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1186, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 456, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1090, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1088, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 992, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long677/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 743, \"height\": 621, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long677/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 847, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long677/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long677/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 697, \"label\": \"Table\"}]"
motivation: 对话摘要领域的大模型行为研究不足，已有评测主要面向BART类模型，缺乏对LLM幻觉的系统认识。
method: 基于人工标注，对GPT-4和Alpaca-13B生成的对话摘要做跨度级不一致检测并分类幻觉类型。
result: 大模型常生成貌似合理但缺乏对话支撑的内容，表现出明显的情境性幻觉趋势。
conclusion: 为大模型对话摘要忠实度评估提供基准与分析，推进对话摘要幻觉领域研究。
---

## Abstract
Recent advancements in large language models (LLMs) have significantly advanced the capabilities of summarization systems.However, they continue to face a persistent challenge: hallucination. While prior work has extensively examined LLMs in news domains, evaluation of dialogue summarization has primarily focused on BART-based models, resulting in a notable gap in understanding LLM effectiveness.Our work seeks to address this gap by benchmarking LLMs for dialogue summarization faithfulness using human annotations,focusing on identifying and categorizing span-level inconsistencies.Specifically, we evaluate two prominent LLMs: GPT-4 and Alpaca-13B.Our evaluation reveals that LLMs often generate plausible, but not fully supported inferences based on conversation contextual cues, a trait absent in older models. As a result, we propose a refined taxonomy of errors, introducing a novel category termed “Contextual Inference” to address this aspect of LLM behavior. Using our taxonomy, we compare the behavioral differences between LLMs and older fine-tuned models. Additionally, we systematically assess the efficacy of automatic error detection methods on LLM summaries and find that they struggle to detect these nuanced errors effectively. To address this, we introduce two prompt-based approaches for fine-grained error detection. Our methods outperform existing metrics, particularly in identifying the novel “Contextual Inference” error type.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

对话摘要（Dialogue Summarization）是自然语言处理中的重要任务，然而大语言模型（LLMs）在该任务中的**忠实性（faithfulness）** 研究一直存在空白：

- 已有研究对 LLM 幻觉的评测主要集中在**新闻摘要**领域，发现 GPT-3 生成的新闻摘要不一致率低于 5%。
- 对话摘要领域的既有评测大多基于 **BART 等小型微调模型**，对 GPT-4 等先进 LLM 的系统性行为分析不足。
- 对话文本天然具有口语化、指代省略、依赖语境共享知识等特点，LLM 在摘要中容易产生**看似合理但缺乏直接证据**的推断性内容，这类幻觉尚未被系统定义与研究。

本文的核心意义在于：**首次系统性地、通过人工跨度级标注来评估 LLM 在对话摘要任务中的幻觉行为**，并据此提出新的错误分类法、揭示 LLM 不同于旧模型的错误分布，同时提出了更有效的自动错误检测方法，填补了该评测空白。

## 2. 方法论：核心思想、关键技术细节

### 2.1 人工标注流程
- **第一阶段（不一致标注）** ：雇佣两名语言学专业事实核查者，对摘要中与对话原文冲突、歪曲信息或缺乏证据的跨度进行标注。标注者间 pairwise F1 为 66.94%，达到较高一致性水平。
- **第二阶段（错误分类）** ：由一位语言学专家作者对已标注错误做更细粒度的类别划分。

### 2.2 错误分类体系（核心贡献）
论文提出了一套适用于 LLM 摘要特征的**新错误分类法**，包含六类：

| 错误类别 | 简要定义 |
|---|---|
| **Circumstantial Inference（情境性推断）** | **新增类别**：模型依据对话中的间接/情境证据做出推断，得出对话中未直接陈述的信息。这类错误源于 Grice 合作原则中的“量的准则”——对话者常省略双方共享知识，而 LLM 会将这些省略内容补全为看似合理的断言。 |
| **Logical Error（逻辑错误）** | 事件顺序错乱、缺乏常识推理、遗漏关键细节导致的逻辑不准确。 |
| **World Knowledge（外部世界知识）** | 摘要引入了对话中未提及的真实世界事实，如说出未提及的公众人物全名。 |
| **Referential Error（指代错误）** | 代词指代不清或信息归属错误（misattribution）。BART 以指代消解错误为主（95%），LLM 中错误归属占比更高（58%）。 |
| **Figurative Misrepresentation（比喻误读）** | 将对话中的隐喻、反讽或玩笑当作字面意思进行摘要，曲解原意。 |
| **Nonsensical（无意义输出）** | 包含语法错误或 LLM 重复 prompt/指令等异常输出。 |

### 2.3 自动错误检测方法
论文除采用并评估已有自动指标外，提出了两种基于 prompt 的细粒度错误检测方法，采用“**先识别、后验证**”的两阶段流程：

1. **ChatGPT-Span**：先用通用 prompt 让 GPT 识别摘要中缺乏证据的不一致跨度；再通过验证 prompt，对跨度按 1–5 分评估其受对话支持的程度，仅将评分低于 5 的跨度判定为不忠实。
2. **ChatGPT-SpanMoE（Mixture-of-Experts）** ：改进版——对分类法中每个错误类型分别设计专用 prompt 作为“专家”，由 GPT 分别针对各错误类型进行识别，再进行与上述相同的验证环节。

## 3. 实验设计

### 3.1 数据集
- **SAMSum**：人工编写的对话摘要数据集（合成书面对话）。
- **DialogSum**：真实场景口语对话摘要数据集。
- 为便于与既有工作比较，使用与 RefMatters 和 FacEval 相同的数据点进行标注。

### 3.2 评测模型
| 类别 | 模型 |
|---|---|
| **LLM（零样本）** | GPT-4（gpt-4-32k-0613）、Alpaca-13B |
| **FT-Summ（微调基线）** | BART、UniLM、MV-BART、Coref-BART、CondigSum-BART、CODS |

其中 GPT-4 和 Alpaca-13B 使用默认设置与零样本 prompt 生成摘要；对 FT-Summ 模型利用了 RefMatters 和 FacEval 既有人工标注。

### 3.3 自动评测基线
- **问答（QA）类**：QAFactEval、QuestEval
- **自然语言推断（NLI）类**：SummaC-ZS、SummaC-Conv
- **Prompt 类**：ChatGPT-Direct Assessment（ChatGPT-DA）

### 3.4 评测任务
- **二分类一致性检测**：判别摘要整体是否忠实（用 balanced accuracy）。
- **跨度级检测**：识别具体不一致文本跨度（用 F1）。

## 4. 资源与算力

论文中**未明确说明使用的 GPU 型号、数量或训练耗时**等算力资源信息。原因在于：

- 本文的 LLM（GPT-4、Alpaca-13B）评测采用**零样本推理**，不涉及模型训练。
- Alpaca-13B 的推理硬件配置未在文中列出。
- 主要资源消耗在于人工标注（聘请两位标注者，时薪分别为 18 美元和 22 美元）和基于 GPT-4 的查询调用。

## 5. 实验数量与充分性

### 实验覆盖情况
- **模型覆盖**：2 个 LLM + 6 个 FT-Summ 模型，跨两个对话摘要数据集。
- **人工标注规模**：对 GPT-4 和 Alpaca-13B 的摘要进行完整跨度级不一致标注；对 BART 的标注用于错误分类对比。
- **自动检测评估维度**：同时评估了二分类整体一致性和跨度级 F1，并按错误类别细粒度报告各指标的表现。

### 充分性与公平性评估
**优点：**
- 人类标注采用两名语言学专业标注者并报告 pairwise F1=66.94%，保证了一定可靠性。
- LLM 统一采用零样本设置，便于反映模型的天然能力并保证公平比较。
- 自动指标阈值基于独立子集确定（约 150 条样例），避免人为调优偏差。

**不足：**
- 只评估了两个 LLM，无法代表所有大模型。
- 每个模型的摘要标注量有限，统计效力受到限制。
- 错误分类的第二轮标注仅由一位作者完成，存在主观性风险。
- 内部对比默认 GPT-4 与 Alpaca-13B 均使用默认解码参数，没有测试温度等超参数对幻觉的影响。
- 两轮标注之间未报告第二轮的独立信度检验。

总体而言，实验设计**覆盖面合理但规模有限**，足以支持主要结论，但对于细粒度类别间差异的量化推断应审慎对待。

## 6. 主要结论与发现

1. **LLM 在对话摘要中的幻觉率显著高于新闻摘要领域**：GPT-4 约有 **23%** 的摘要含有不一致内容，远高于新闻摘要中的 <5%。Alpaca-13B 的错误率也更低但整体仍不如 BART 稳定。
2. **LLM 产生大量“情境性推断”幻觉**：约 **38%** 的 LLM 错误属于 Circumstantial Inference；同一类别在 BART 摘要中只占 1%。这说明 LLM 倾向于基于情境线索补全对话中未明说的信息，产生流畅但无直接证据支持的内容。
3. **LLM 的逻辑错误大幅减少**：Logical Error 在 FT-Summ 中占比超过 50%，在 LLM 中约占 17%，体现 LLM 更强的语义推理能力。
4. **LLM 不再有语法错误，但存在指代错误形态转变**：LLM 的 referential errors 以**信息误归属**为主（58%），而 BART 以**指代消解错误**为主（95%）。
5. **自动检测器的性能差异明显**：传统 QA/NLI 类指标在检测 LLM 摘要错误时效果不佳；prompt 类方法相对更好，但在 LLM 摘要上的表现普遍低于在 FT-Summ 上的表现。
6. **ChatGPT-SpanMoE 是表现最优的检测方法**：在二分类和跨度检测上均超过所有现有指标，尤其对 **Circumstantial Inference** 的检测提升显著（Few-shot 下 FT-Summ F1 达到 29.04，LLM 达到 33.22）。

## 7. 优点

- **填补研究空白**：首次对 LLM 对话摘要进行细粒度人工跨度标注评测，研究对象从 BART 等旧模型扩展至 GPT-4。
- **提出新错误类别**：Circumstantial Inference 具有重要理论意义，揭示了 LLM 在自然语言理解中“过度推断”这一行为模式，也为后续评测提供了参考。
- **以 Grice 语用学理论为基础**：为“情境性幻觉”提供了理论根据。
- **构建并公开了标注数据集**：为社区后续研究提供资源。
- **系统评估自动检测方法**：在二分类和跨度两个层面、按错误类型分别评估各指标，分析全面。
- **提出有效的自动检测新方法**：MoE 式分类型 prompt 思路优于统一 prompt，能针对性地提高检测能力。

## 8. 不足与局限

- **评测模型有限**：只有 GPT-4 和 Alpaca-13B 两个 LLM，难以推广到所有大模型。
- **标注数据规模较小**：受限于人工成本（时薪 18–22 美元），标注样本量不大，影响统计可靠性。
- **错误分类的第二轮标注存在主观偏差风险**：仅一名作者完成，且未报告第二轮标注的信度。
- **未报告训练/推理算力细节**：不利于复现和资源评估。
- **依赖 GPT-4 作为检测器**：GPT-4 为闭源收费模型，成本与可访问性限制了方法复现；且用 GPT-4 检测 GPT-4/其他模型输出可能存在系统性偏差。
- **“情境性推断”是否应视为错误存在语境依赖**：论文指出在开放领域对话中这种推断可能是合理的，但在医疗等高风险场景中则后果严重；这种情境依赖性未被充分量化研究。
- **没有深入分析不同的 prompt 设计、温度或解码策略对幻觉的影响**。

（完）
