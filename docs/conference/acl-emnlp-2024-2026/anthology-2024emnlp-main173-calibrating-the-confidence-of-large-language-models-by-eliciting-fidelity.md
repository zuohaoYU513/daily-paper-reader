---
title: Calibrating the Confidence of Large Language Models by Eliciting Fidelity
title_zh: 通过引导忠实度校准大语言模型的置信度
authors: "Mozhi Zhang, Mianqiu Huang, Rundong Shi, Linsen Guo, Chong Peng, Peng Yan, Yaqian Zhou, Xipeng Qiu (邱锡鹏)"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.173.pdf"
tags: ["query:metacognitio"]
score: 10.0
evidence: 将置信度分解为对问题的不确定性与对生成答案的忠实度，以校准置信度与正确率
tldr: 对齐后的大语言模型常表现出过度自信，口头置信度与实际正确率不一致。该文将模型置信度分解为对问题的不确定性和对自身生成答案的忠实度两部分，提出即插即用的UF校准方法。在多个RLHF模型和多项选择问答数据集上，该方法持续提升置信度校准效果，并引入IPR和CE两个新评估指标，为置信度校准提供了可解释的新框架。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 586, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 582, \"height\": 951, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1399, \"height\": 789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1467, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1463, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1472, \"height\": 317, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1550, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1099, \"height\": 1124, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1366, \"height\": 1123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1366, \"height\": 1123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1366, \"height\": 1125, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1367, \"height\": 1123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main173/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1101, \"height\": 1124, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 645, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 789, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1658, \"height\": 724, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1623, \"height\": 2453, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1630, \"height\": 1373, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1630, \"height\": 1348, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1644, \"height\": 1445, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1430, \"height\": 1298, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main173/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 763, \"height\": 906, \"label\": \"Table\"}]"
motivation: RLHF对齐使模型往往过度自信，置信度与实际正确率失配，需要分解置信度来源并加以校准。
method: 提出UF校准：将置信度分解为问题不确定性和答案忠实性两个因素，并用即插即用方式对置信度进行调整估计。
result: 在6个RLHF模型及多个MCQA数据集上验证了该校准方法的有效性，并引入了新的校准度量指标IPR和CE。
conclusion: 把置信度分解为不确定性与忠实度能显著改善过度自信，并给出更细粒度校准评估方法。
---

## Abstract
Large language models optimized with techniques like RLHF have achieved good alignment in being helpful and harmless. However, post-alignment, these language models often exhibit overconfidence, where the expressed confidence does not accurately calibrate with their correctness rate. In this paper, we decompose the language model confidence into the Uncertainty about the question and the Fidelity to the answer generated by language models. Then, we propose a plug-and-play method, UF Calibration , to estimate the confidence of language models. Our method has shown good calibration performance by conducting experiments with 6 RLHF-LMs on four MCQA datasets. Moreover, we propose two novel metrics, IPR and CE, to evaluate the calibration of the model, and we have conducted a detailed discussion on Truly Well-Calibrated Confidence for large language models. Our method could serve as a strong baseline, and we hope that this work will provide some insights into the model confidence calibration.

---

## 论文详细总结（自动生成）

## 摘要
本文针对对齐后大语言模型普遍存在的过度自信问题，提出将模型置信度分解为“对问题的不确定性（Uncertainty）”与“对生成答案的忠实度（Fidelity）”两个维度，并据此设计了一种即插即用的 **UF Calibration** 方法。该方法不需要访问模型内部 token logits，适用于 GPT-3.5/GPT-4 等黑盒 RLHF 模型，在 6 个 RLHF-LM 和 4 个多项选择问答（MCQA）数据集上取得了稳定的校准效果。此外，论文提出了 **IPR**（Inverse Pair Ratio）和 **CE**（Confidence Evenness）两个新的校准评估指标，并讨论了什么才是“真正良好校准的置信度”。

## 1. 研究动机与核心问题
- **核心问题**：RLHF 等对齐技术使语言模型更具帮助性和无害性，但也带来了“过度自信”问题——模型输出的置信度与其实际正确率不匹配（如模型给出 95% 置信度的答案，其真实正确率远低于 95%）。
- **已有证据**：预训练模型的 per-token logit 近似良好校准，但 RLHF-LM 的 token 概率分布因优化目标（对齐人类偏好而非拟合语料频率）而失真。
- **现有方法的不足**：
  - **Logit-based**（如 Temperature-Tuning）通常需要极高的温度（>2.0），会使模型输出过于随机；
  - **Verbalization-based**（让模型口头表达置信度）依赖模型的自我认知与指令遵循能力，且不同模型倾向于输出固定、集中的置信度表达（如“0.8”“0.9”），并非真正的个性化校准。
- **核心直觉**：当把模型之前选中的选项替换为“所有其他选项均不正确”后重新提问——若模型改选其他选项，则说明其对原答案的“忠实度”不高。这一行为可以用于估计模型对答案的置信度。

## 2. 方法论：UF Calibration
论文将模型对问题 Q 的答案 ai 的置信度分解为：
- **Uncertainty(Q)**——模型对问题本身的不确定程度（通过多次采样的答案分布熵来衡量）；
- **Fidelity(ai)**——模型对其生成答案 ai 的忠实程度（通过分层“忠实度链”的替换测试来衡量）。

整体置信度公式为：

```
Conf(Q, ai) = (1 − Uncertainty(Q)) × Fidelity(ai)
```

算法分为四步（伪代码可见原文 Algorithm 1）：

1. **回答采样**
   对问题 Q 采样 K 次（黑盒设 K=10），得到答案分布 P_sampled 与答案集合 A，取频率最高的选项为最终答案。

2. **引出忠实度（核心创新）**
   - 对答案集中每个答案 ai，用“All other options are wrong.”替换原有选项 oi，再以贪心解码方式重新提问；
   - 若模型仍选择 ai 则停止；若选择其他选项，则继续剔除该新选选项并重复提问，直到模型选择被替换后的选项，从而得到一个分层“忠实度链” C（如 A→C→D）；
   - 链越短，说明初始答案的忠实度越高；链中每个元素按其从右到左的位置获得权重 τ^i（默认 τ=2）；
   - 标准化后的单链忠实度计算公式：Fidelity_C(ai) = τ^i / Σ τ^i；
   - 综合所有链：以 P_sampled(首个元素) 作为各链出现概率的代理，加权平均得到每个答案的忠实度 F(ai)。

3. **不确定性估计**
   对采样答案分布 P_sampled 计算归一化信息熵：

   ```
   Uncertainty(Q) = − Σ p_i·log p_i / log M
   ```

   （M 为选项数，确保了不确定性范围在 [0, 1]）

4. **置信度融合**
   将（1 − Uncertainty）作为整体置信度缩放因子，乘以每个答案的忠实度，得到最终校准置信度。

## 3. 实验设计
- **数据集**：4 个多项选择问答（MCQA）基准
  - ARC-Challenge（1172 题，测试集）
  - MMLU（57 个学科，每学科采样 18 题以控制调用成本）
  - CommonSenseQA（1221 题，验证集）
  - TruthfulQA（817 题）
- **模型**：6 个 RLHF-LM
  - 闭源：GPT-3.5-Turbo、GPT-4-Turbo
  - 开源：LLaMA2-7B/13B/70B-Chat、Baichuan2-13B-Chat
- **对照组**：
  - **Verb**：提示模型输出 0~1 的浮点数作为置信度
  - **Ling**：提示模型用固定表（如 “Almost Certain”“Probably” 等）表达置信度
  - **Sampled**：采样 10 次，以频率估计答案概率
  - **Token**（仅开源模型）：直接使用 token 生成概率
  - **Conformal Prediction**（附录 D.1）
  - **CAPE-ENUM**（附录 D.2，选项排列法）
- **评估指标**：
  - 原有：ECE_10（期望校准误差）、Brier Score、Accuracy
  - 新提出的两个指标：
    - **IPR_10**（Inverse Pair Ratio）：衡量可靠性图中“逆向对”（置信度高但准确率低的相邻柱）的比例，用于度量可靠性图的单调性；
    - **CE_10**（Confidence Evenness）：可靠性图各柱密度的均匀度——检验模型的置信度是否总是集中在某些固定区间（如恒输出 0.8/0.9）而非分布于不同置信度水平上。

## 4. 资源与算力说明
论文并未明确说明所使用的 GPU 型号、数量或训练/推理成本等硬件信息。仅在致谢中提及计算平台为复旦大学 CFFF 平台。附录提供各模型平均调用次数（即单问题额外 token 开销）以供对推理成本作侧面评估：不同模型/数据集上的平均调用次数约为 1.8–4.3 次，但并未报告具体硬件配置或总时钟/能耗。

## 5. 实验数量与充分性评估
- **主实验**：6 个模型 × 4 个数据集 × 7 种方法（表 1–3），覆盖闭源与开源、7B~70B 的模型规模梯度，规模较充分。
- **参数消融**（表 4）：分别去除 “Uncertainty” 或 “Fidelity” 分量，并对 τ 取 1.5、2.0、2.5、3.0、4.0、5.0 进行调节，结果表明 τ=2.0 最优，验证两个分量均有必要性。
- **温度鲁棒性**（图 4/7）：比较 LLaMA2-13B-Chat 和 Baichuan2-13B-Chat 在温度 0.1~1.0 下的校准表现，显示 UF 方法在各温度下均有优势。
- **参数规模效应**（图 5）：考查 LLaMA2-7B/13B/70B 系列上的各方法校准与模型规模的关系。
- **附录补充实验**：与 Conformal Prediction 及 CAPE 的比较（含 Brier Score）、Candidate-Aware UF Calibration 变体实验、置信度表达集中性分析等，覆盖面较广。
- **总体评价**：实验设计整体客观公平，但评估任务均限制在“答案集合已知”的 MCQA 范畴，不涉及开放式生成，因此结论的外部推广性仍有待进一步验证。另外，Calibration 集划分等设置下的对比方法（如 Conformal）需要训练集而 UF 不需要，这一设置上的差异需要注意。

## 6. 主要结论与发现
- UF Calibration 在 ECE_10、IPR_10 和 CE_10 三个指标上普遍优于 Verb、Ling、Sampled、Token 等方法，GPT-3.5-Turbo 的校准曲线在 4 个数据集上均接近 y=x。
- 去除 Uncertainty 分量后性能有所下降但依然优于多数基线；只有 Fidelity 时模型回答的置信度仍然有较好的校准效果。这说明 Fidelity 是估计置信度的关键信号，而 Uncertainty 单独无法作为答案置信度的有效估计。
- Verbalization-based 方法的 CE 值很低（约 0.1–0.53），表明模型倾向于反复表达少数固定置信度（0.8 和 0.9），这不是理想的校准——即使 ECE 指标偶然接近 0，也可能只是“平均准确率恰好落在模型偏好的置信区间”。
- 随着模型参数增大（7B→70B），模型准确率提升且 ECE 下降，但其置信度表达的“集中化偏好”并未改善甚至更严重。语言模型的自知能力仍需提升。
- 校准过程不影响模型最终答案选择，UF 方法在提升校准的同时不会损害准确率。

## 7. 优点
- **黑盒友好**：不依赖任何 per-token logits 或内部表示，适用 ChatGPT、GPT-4 等商业模型，适用范围广。
- **即插即用**：不需要训练/微调等额外操作，不需要额外的校准集与数据拟合步骤，没有下游数据的要求，可以离线或在线直接应用。
- **分解框架简洁可解释**：将传统的单点置信度拆分为“不确定性”（广泛意义上的模型内部状态）与“忠实度”（输出层面的承诺程度）两部分；忠实度链的图式化表示高度直观且无需启发式 Prompt 设计。
- **新指标补充了盲区**：IPR 直接度量可靠性图/置信度-准确率关系的“单调性”，CE 捕捉了已有 ECE 无法观测到的“置信度过度集中在少数固定区间”问题，指出了“ECE 偶然良好”的陷阱。
- **消融较完备**：对两组成分（不确定性、忠实度）和 τ 均做了敏感度分析。
- **对比充分**：纳入 logit-based、verbalization-based、采样估计、conformal prediction 和 CAPE 法等多类主流方法，并附带 4 个数据集的可靠性图与 Brier Score 等扩展结果。
- **讨论有洞察力**：对“真正良好校准的置信度”这一问题进行了深入讨论，这三方面（ECE/IPR/CE）兼顾准确度、单调性和分布均匀性的分析框架对社区有一定启发性。

## 8. 不足与局限
- **适用范围窄**：方法仅适用于答案集合已知的场景（多项选择、文本分类、情感分类、RLHF 偏好标注等），无法直接用于开放式生成/自由文本问答场景。论文本身将此列为 Limitation。
- **多次额外调用模型：推理开销增加**：每道题除了采样以外还需要额外的少则 2 次多则 3–4 次以上的模型调用（表 5），且每次调用都要求使用贪心解码；在长文本/高并发/成本受限的线上推理场景中，该方法的额外成本可能难以承担。
- **对 option 结构有一定依赖**：用“All other options are wrong”（全他选项错误）替换原选项的方式，在部分情境（如 MMLU 或 TruthfulQA）中如果替换后的该选项实质上是正确答案（例如选项“以上皆非”“无正确答案选项”等蕴含关系）就可能导致度量失真。论文附录 D.3 提出的 Candidate-Aware 变体被用来缓解这一风险，但增加了额外 prompt 复杂度。
- **采样和不一致的假设**：Fidelity 链的权重分配（τ^i 按位置指数衰减）是启发式的，只在实验数据集上有经验支撑，缺乏理论推导。
- **性能与基线的差异并不在所有情况下都占优**：例如 GPT-4-Turbo 在 ARC-Challenge 上 ECE_10 为 0.127，比部分基线（Verb 等）指标更差——强模型上的优势集中体现在 TRUTHFULQA/MMLU 等较大且更均衡的数据上，小规模数据集上的增益可能有限。
- **评估数据集全部为英文 MCQA**：未覆盖中文、多语言或更接近真实应用的开放域问答情境。
- **未报告 GPU 训练时长/推理算力**：虽然该方法不需要真正训练，但没有报告总调用 token 量的换算和成本对比。

## 总结
UF Calibration 通过对“不确定性”与“忠实度”两个维度的分解，提出了一个新的即插即用置信度校准范式。在多个黑盒与开源 RLHF-LM 上较系统化地验证了它对校准质量（ECE/IPR/CE）的提升，且实现成本相对可控。该工作对“真正良好校准的置信度”的讨论和所给出的两个度量指标（IPR、CE）也丰富了评测体系。但当前的验证主要局限于 MCQA/封闭答案集等受限场景，且其开环启发式假设和额外调用开销仍有较大优化空间，适用范围有待扩展。

（完）
