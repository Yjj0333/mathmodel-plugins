# BZD 数学建模技能市场（ChatGPT 插件）

数学建模竞赛全流程 + BZD 系列 ChatGPT 可安装插件市场，覆盖 赛题分析 → 建模思路 → 编程求解 → 论文撰写 → 全文自查评审 各阶段。

## 在 ChatGPT 中安装

1. 打开 ChatGPT 的 **插件市场 → 添加插件市场** 对话框；
2. **来源** 填：`https://github.com/Yjj0333/mathmodel-plugins`（或 `git@github.com:Yjj0333/mathmodel-plugins.git`）；
3. **Git 引用** 选 **主分支**；
4. **稀疏路径** 留空即可安装整个市场（仓库根目录自带 `.agents/plugins/marketplace.json`）；也可以填 `plugins/<插件名>` 只加载单个插件；
5. 在市场中按需安装插件。**注意：技能只在安装后「新开的会话」里生效**，旧会话不会注入；
   调用方式是输入 `@` 选择插件或其中的技能（如 @BZD题意逐句翻译），也可以直接描述任务让 ChatGPT 自动匹配技能。

## 推荐安装：BZD 数模全家桶

不想逐个挑插件？直接安装 **`bzd-mathmodel-suite`（BZD 数模全家桶）**：它把全部 19 个技能打包在一个插件里（含全流程三阶段、图表选型与模板库、全部 BZD 自查评审技能），所有 `$技能` 交叉引用在同一插件内闭环，无跨插件依赖，安装一次即可用 `$bzd-review-paper`、`$2analysis-modeling` 等任意技能名调用。

## 插件列表

| 显示名 | 插件名 | 功能 | 依赖建议 |
|---|---|---|---|
| 数模全流程工作流 | `mathmodel-workflow` | 赛题分析、编程求解冻结、论文撰写三阶段工作流，含图表选型子技能 | 安装后建议同时安装 BZD数模字典 插件（$bzd-model-dictionary）以支持 2analysis-modeling 的模型核验。 |
| BZD 题意逐句翻译 | `bzd-problem-translator` | 逐句拆解赛题，生成Mermaid跨问流程图与Markdown报告 | — |
| BZD 建模思路 | `bzd-modeling-ideas` | 生成贯穿全文的整体建模思路、多模型比较与选型依据 | — |
| BZD 问题重述 | `bzd-problem-restatement` | 根据赛题生成问题重述，或对照原题检查已有重述 | — |
| BZD 问题分析自查 | `bzd-problem-analysis-checker` | 对照赛题检查问题分析的建模逻辑、联动和章节边界 | — |
| BZD 模型假设自查 | `bzd-model-assumption-checker` | 对照赛题诊断模型假设的合理性、依据、边界与后文用途 | — |
| BZD 模型建立求解自查 | `bzd-model-solution-checker` | 检查模型建立、算法求解、结果检验与灵敏度分析闭环 | — |
| BZD 符号说明自查 | `bzd-symbol-notation-checker` | 核对论文符号表、正文公式、单位、下标与排版的一致性 | — |
| BZD 摘要自查 | `bzd-abstract-checker` | 仅输入摘要，诊断数学建模摘要的独立性与具体问题 | — |
| BZD 论文格式自查 | `bzd-paper-format-checker` | 逐项检查摘要、标题密度、图表重复、模型可读性与全文排版 | bzd-review-paper 插件会自动引用本插件的格式审查报告，建议一起安装。 |
| BZD 论文评审 | `bzd-review-paper` | 区分国赛与小型竞赛，生成专属细则并评审得分位次 | 依赖 BZD 论文格式自查 插件（$bzd-paper-format-checker），建议一起安装。 |
| BZD AI工具使用披露 | `bzd-ai-usage-disclosure` | 生成并检查数学建模竞赛AI工具使用声明与匿名详情材料 | — |
| BZD 国赛高校国奖查询 | `bzd-cumcm-school-awards` | 查询高校近五年国奖、2026预测与高频指导教师 | 可选搭配 BZD 论文评审 插件复盘往年论文。 |
| BZD 参考文献与附录自查 | `bzd-reference-appendix-checker` | 检查参考文献数量质量、附录长度、复现与匿名风险 | — |
| 科研绘图模板库 | `mathmodel-figure-templates` | 内置10+科研绘图模板（SHAP、云雨图、ROC、泰勒图、和弦图等）的即用Python脚本 | — |

## 仓库结构

```
.agents/plugins/marketplace.json   # 插件市场清单
plugins/<name>/
  .codex-plugin/plugin.json        # 插件 manifest
  skills/<skill-name>/SKILL.md     # 技能定义
  skills/<skill-name>/references|scripts|assets|agents/...  # 子技能与资源
```

## 跨插件依赖

- `mathmodel-workflow` 的 `$2analysis-modeling` 会调用 `$bzd-model-dictionary`（BZD数模字典）核验候选模型；
- `$bzd-review-paper` 会导入 `$bzd-paper-format-checker` 的格式审查结果；
- `$bzd-cumcm-school-awards` 可选调用 `$bzd-review-paper` 复盘往年论文。

建议一次性安装全部插件，保证 `$技能` 交叉引用可用。

## 安装后用不了？排查步骤

1. **添加市场 ≠ 安装插件**：添加插件市场只是登记了市场来源，还需要在「插件」页面进入 **BZD 数学建模技能市场**，对需要的插件逐个点击 **安装/添加**；已安装的插件才会出现在右侧已安装列表里。
2. **manifest 有改动后需要重新添加市场**：如果之前添加过旧版本，先在市场中删除该市场 → 重新按上面步骤添加（客户端有缓存，右上角 ↻ 刷新也可尝试）。
3. **新会话测试**：安装后新开一个会话，输入 `$mathmodel-workflow` 或 `$bzd-review-paper` 调用；`$技能名` 引用只对已安装插件生效。
4. **跨插件依赖**：`$bzd-review-paper` 依赖 `$bzd-paper-format-checker`、`$2analysis-modeling` 依赖 `$bzd-model-dictionary`，相关插件需一起安装。
