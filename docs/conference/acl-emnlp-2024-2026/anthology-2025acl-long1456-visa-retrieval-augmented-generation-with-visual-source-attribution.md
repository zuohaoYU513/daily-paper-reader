---
title: "VISA: Retrieval Augmented Generation with Visual Source Attribution"
title_zh: VISA：带视觉来源归因的检索增强生成
authors: "Xueguang Ma, Shengyao Zhuang, Bevan Koopman, Guido Zuccon, Wenhu Chen, Jimmy Lin"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1456.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 把RAG生成与视觉证据归因结合，在检索文档中精确框出支撑证据区域
tldr: 现有RAG系统只能给出文档级引用，用户难以在多篇内容丰富的文档中快速找到支撑回答的证据位置。本文提出VISA，用大视觉语言模型在生成答案的同时，对检索文档截屏中的证据区域以边界框进行高亮，实现视觉化的细粒度来源归因。系统评估在两个精选问答任务上进行，体现证据定位相比文档级引用更能方便用户核验。该工作使RAG归因从文档级别细化到可视证据区域，提升了生成内容的可验证性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1456/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 701, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1456/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1456/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 503, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1456/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1604, \"height\": 2127, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1456/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1629, \"height\": 2120, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 529, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1661, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 683, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 757, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 824, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 830, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1580, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1456/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 743, \"height\": 371, \"label\": \"Table\"}]"
motivation: RAG生成内容通常只关联到文档级引用，在内容丰富的多文档场景中难以快速核验具体证据位置。
method: 利用大视觉语言模型把答案生成和来源定位统一，直接在检索文档截图里用边界框标出支持答案的证据区域。
result: 在自建的多文档问答评测中，视觉来源标注可让用户更准确地定位答案所依据的文本或图像证据。
conclusion: 把来源归因细化到视觉区域级，提高RAG系统可核查性和用户溯源效率。
---

## Abstract
Generation with source attribution is important for enhancing the verifiability of retrieval-augmented generation (RAG) systems. However, existing approaches in RAG primarily link generated content to document-level references, making it challenging for users to locate evidence among multiple content-rich retrieved documents. To address this challenge, we propose Retrieval-Augmented Generation with Visual Source Attribution (VISA), a novel approach that combines answer generation with visual source attribution. Leveraging large vision-language models (VLMs), VISA identifies the evidence and highlights the exact regions that support the generated answers with bounding boxes in the retrieved document screenshots. To evaluate its effectiveness, we curated two datasets: Wiki-VISA, based on crawled Wikipedia webpage screenshots, and Paper-VISA, derived from PubLayNet and tailored to the medical domain. Experimental results demonstrate the effectiveness of VISA for visual source attribution on documents’ original look, as well as highlighting the challenges for improvement.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（动机与背景）

- **研究痛点**：现有 RAG（检索增强生成）系统虽然能生成带引用的答案，但大多停留在**文档级（document-level）引用**。在信息密集、多页面的检索文档中，用户很难在长文档里快速定位真正支撑答案的段落、表格或图片，认知负担较重。
- **已有方案的不足**：基于"文本块引用（passage-level citation）"的方案需要额外的工程将文本块映射回原始文档；且基于文本的管线依赖于 HTML 解析、OCR 等预处理模块，可能丢失表格、图片等视觉信息。
- **核心研究问题**：能否借鉴"文档截图嵌入检索（DSE）"的视觉化范式，构建一个**端到端、全视觉、可验证**的 RAG 流程——模型不仅生成答案，还能在原始文档截图中用边界框（bounding box）直接框出证据区域。
- **论文标题含义**：VISA = Retrieval-Augmented Generation with **Vi**sual **S**ource **A**ttribution，即"带视觉来源归因的检索增强生成"，首次在端到端 RAG 框架中实现视觉层面的证据定位。

## 2. 方法论：核心思想与技术细节

- **核心思想**：用大视觉语言模型（VLM）替代传统"文本抽取 + LLM 生成"管线，将"答案生成"与"证据定位"统一为**一个多模态 next-token prediction 任务**。
- **任务形式化定义**：
  - 输入：文本查询 q + 一组检索候选文档截图 D = {d₁, ..., dₙ}；
  - 输出三要素：答案 a、最相关文档标识 i、证据边界框坐标 B = [(x₁,y₁), (x₂,y₂)]。
- **模型输入输出设计**（以 prompt 模板形式）：
  - 单候选模式：输入文档截图 + 问题，输出 `Answer: ...` 与 `Bounding Box: ...`；
  - 多候选模式：输入 3 张候选文档截图 + 问题，输出 `Answer: ...`、`Evidence Document: {index}`、`Bounding Box: ...`；若无证据文档则输出 `No answer`。
- **训练策略**：
  - 基于 Qwen2-VL-2B-Instruct 与 Qwen2-VL-7B-Instruct 进行 LoRA 微调；
  - **随机裁剪增强**：在边界框外部区域随机裁剪，让模型适应不同输入尺寸，提升对未见过文档版式的零样本泛化；
  - 边界框采用**绝对坐标**表示（归一化到 [0,1] 的效果反而较差）；
  - 先训练单候选任务，再初始化到多候选任务继续训练一轮，多候选训练时冻结图像编码器以节省显存。

## 3. 实验设计：数据集、基准与对比方法

- **自建数据集**（三套）：
  | 数据集 | 来源 | 训练/测试规模 | 特点 |
  |---|---|---|---|
  | Wiki-VISA | Natural Questions + 真实维基百科网页截图重现 | 87k / 3,000 | 多页（最多 4 页）、多模态，答案可来自段落/表格/列表/图片 |
  | Paper-VISA | PubLayNet 医学论文版面 + VLM 合成问答 | 100k / 2,160 | 单页医学论文 PDF，3:2 宽高比 |
  | FineWeb-VISA | FineWeb-edu 网页采样 + VLM 合成 | 60k（仅训练） | 网页布局多样，用于数据增强与零样本分析 |
- **三种评测设置**：
  1. **Single oracle candidate**：只输入唯一相关文档，聚焦于"生成+定位"能力；
  2. **Multi-candidate, Oracle in Candidates**：3 个候选文档（1 正 + 2 难负例），需判别相关文档；
  3. **Multi-candidate, Oracle Not in Candidates**：约 20% 样本不含证据文档，考察模型的"No answer"拒答能力。
- **评价指标**：
  - 答案用宽松精确匹配（relaxed EM：与标准答案子串匹配且长度差 ≤ 20 字符）；
  - 边界框用 IoU（阈值 0.5 判定正确）；
  - 按证据内容类型（首页段落、跨页段落、非段落如表格/图片）分桶统计，总体准确率为类别宏平均。
- **对比方法**：
  - 零样本基线：Qwen2-VL-72B-Instruct、GPT-4o；
  - 微调模型：VISA-2B/7B（单候选与多候选变体）；
  - 对照管线：基于文本的归因系统（假设完美的 PubLayNet 版面检测器 + pytesseract OCR + Qwen2-VL 的 LLM 后端）；
  - 额外消融：不同训练数据组合（Wiki / Paper / FineWeb 及其混合）、坐标表示方式对比、有无随机裁剪、是否输出边界框（纯视觉 RAG）、prompt 中 Answer/bounding box 顺序互换。

## 4. 资源与算力

- 文中明确说明：使用 **4×H100 GPU** 进行微调；
- 单候选设置：LoRA、学习率 1e-4、batch size 64、**2 epoch**；多候选设置：以单候选权重初始化、学习率不变、**1 epoch**，且冻结图像编码器以降低显存消耗；
- 多候选数量仅设为 3，原因正是**计算资源受限**——更大候选集会引发 OOM（out-of-memory）。

## 5. 实验数量与充分性

- **实验组数相当丰富**，主要包括：
  1. 主结果表（表 2）：Wiki-VISA 与 Paper-VISA 在两个数据集 × 四种模型设置下的 bbx/ans 双指标评测；
  2. 与文本型归因管线的对比（表 3）；
  3. 五种训练数据组合的跨域迁移实验（表 4/表 7）；
  4. 边界框表示与裁剪策略的消融（表 5）；
  5. 不同模型骨干对比（Qwen2-VL vs. GPT-4o vs. Phi3-Vision，表 6）；
  6. 不同规模零样本模型的对比（表 8）与 prompt 顺序敏感性测试（表 9）；
  7. 人工抽取 50 例错误分析（三类错误）。
- **充分性评价**：实验维度较全面，覆盖了"零样本 vs. 微调""单候选 vs. 多候选""域内 vs. 跨域""视觉管线 vs. 文本管线"等多个维度，消融设计合理。**但存在一些局限**：多候选最多只测 3 个文档，与真实 RAG（常检索 20+ 文档）有差距；没有专门针对检索阶段质量的端到端联合评测（检索器固定为 DSE）；错误分析只抽样 50 例，统计显著性有限。

## 6. 主要结论与发现

- **现有 VLM 零样本无法完成视觉归因**：Qwen2-VL-72B 在回答上可到 60.4% 准确率，但边界框准确率仅 1.5%，GPT-4o 甚至为 0%——说明"能答对"远不等于"能定位"。
- **微调效果显著**：VISA-7B-single 在 Wiki-VISA 上 bbx 达 54.2%、答案 65.2%；在 Paper-VISA 上 bbx 达 68.2%。
- **多候选难度明显上升**：7B 多候选模型在 Wiki-VISA 上 bbx 降至 32.3%，说明"区分难负例 + 定位证据"的组合任务更具挑战。
- **无答案场景处理良好**：Oracle 不在候选时，VISA-7B-multi 有 82%~96% 的情况能正确拒答。
- **跨域泛化仍是瓶颈**：Paper 训练的模型在 Wiki 上 bbx 几乎为 0；但 Wiki 训练对 Paper 泛化相对较好（27.8%），FineWeb 作为增广数据可显著提升跨域表现（Paper+FineWeb 在 Wiki 上从 0.2% 提升到 36.1%）。
- **视觉管线优于文本管线**：即便文本管线白嫖一个"完美版面检测器"，OCR 引入的拼写错误仍拖累答案准确率，且文本管线无法有效利用图表等视觉元素。
- **错误主要来自源归因错误**：50 例抽样中有 43 例为"答对了但框错了区域"，框位偏移与粒度不匹配（如框整表而非特定单元格）相对较少。

## 7. 优点与亮点

- **任务新颖且实用**：首次将 RAG 来源归因下沉到"边界框级别的视觉证据定位"，直接缓解文档级引用带来的用户核验负担，属于有实际价值的重新定义。
- **统一视觉范式**：无需求助于 HTML 解析 / OCR / 版面分析等易错且脆弱的中间模块，对 PDF、网页、扫描件等多种格式天然鲁棒。
- **高质量数据构建**：Wiki-VISA 利用 NQ 人工判定的问答对与真实维基页面渲染，标注可靠；Paper-VISA 和 FineWeb-VISA 的合成流程（VLM 生成问答）可扩展性强。
- **实验分析细致**：按证据模态（段落/表格/图表/跨页）分别报告，揭示长文档定位、多文档判别等关键难点；数据组合实验清晰刻画了跨域迁移与数据增强的价值。
- **坐标系统设计有洞察**：发现随机裁剪 + 绝对坐标对零样本泛化更好，归一化坐标反而失败，是有价值的工程经验。

## 8. 不足与局限

- **答案形态单一**：只支持短答案生成，无法覆盖需要长文本解释的复杂问答场景。
- **证据假设过于简化**：假设支撑证据集中在文档内一个局部区域；真实场景中证据可能横跨多个段落、图、甚至多篇文档。
- **答案与证据的语义关系偏向抽取式**：Wiki-VISA 中答案多为证据区域的原文子串，模型可能依赖字符串匹配而非深层语义理解。
- **文档类型覆盖有限**：未涉及扫描件、手写体、复杂版式与多种长宽比文档；跨域泛化实验显示表现仍远低于域内。
- **候选规模受限**：多候选实验仅 3 个文档，且训练成本已致 OOM，无法反映大规模真实 RAG 检索环境（如 top-20 场景）的压力；也未端到端考察检索错误的传播。
- **粒度匹配缺乏用户研究**：模型选择的框粒度（整表、整段 vs. 句子、单元格）是否符合真实用户预期，缺少用户实验验证。
- **部分数据集质量不均**：FineWeb-VISA 为合成数据，质量不如 Wiki-VISA 的人工标注；对实验结论的可能偏差没有做充分的下限分析。

（完）
