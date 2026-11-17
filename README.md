# 工业声学AI在线检测 · 客户合作可行性评估 Skill

> 输入客户名称 → 输出合作可行性判断 + 场景匹配 + 行动方案。
> 面向工业声学AI在线检测方案供应商的售前决策自动化工具：从"这家公司值不值得打"到"怎么打"。

一个 [Claude Code](https://claude.com/claude-code) Skill（同样适用于其他支持 SKILL.md 规范的 Agent 工具）。

---

## 这个 skill 做什么

输入一个客户名称，自动完成：**公开信息调研 → 生产工序 × AI 声学关联分析 → 场景匹配 → 六维可行性评分 → 决策链推测 → 行动方案**，输出双版本报告：

| 版本 | 定位 |
|------|------|
| **内部评估版** | 决策工具：评分、决策链、接触路径、情报缺口 |
| **客户汇报版** | 说服材料：业务相关性分析，对接人可一字不改转发给其决策链 |

核心机制：

- **场景匹配矩阵**：技术匹配度 × 急迫度 × 证据等级（A/B/C）× 规模，行动节奏与证据等级强制对齐
- **实体谱系三分类**：集团/合资/更名客户先做目标/并行/排除分类，不假设"拿下 A 自动覆盖 B"
- **相关性 = 客户痛点 × 我方资产**：每个场景标注"已有资产 / 需新建"
- **双版本转化规则**：内置硬红线 7 条 + 诚实底线 3 条，客户版是换姿态重写而非删节
- **ROI 快算框架**：集中式拓扑偏人工替代、分散式拓扑偏客诉/审核/体系一致性

## 适用人群

- 工业声学AI检测 / 工业质检AI方案商的销售、售前、渠道团队
- 需要快速判断"这个客户值不值得打"的商务人员
- 任何做工业 AI 质检生意、想要一套结构化客户评估方法论的团队（框架可直接换皮）

---

## 安装方法

### Step 1：克隆到 Claude Code 的 skills 目录

```bash
# macOS / Linux
git clone https://github.com/tongzhouAM/acoustic-ai-customer-assessment.git \
  ~/.claude/skills/acoustic-ai-customer-assessment

# Windows (Git Bash)
git clone https://github.com/tongzhouAM/acoustic-ai-customer-assessment.git \
  "/c/Users/$USERNAME/.claude/skills/acoustic-ai-customer-assessment"
```

安装后目录结构：

```
.claude/skills/acoustic-ai-customer-assessment/
├── SKILL.md                       ← 核心方法论（五步评估流程）
├── README.md                      ← 本文件
├── VERSION                        ← 版本信息
├── references/
│   ├── solution-components.md     ← 方案组件速查（架构/交付流程/商业模型框架）
│   ├── scenario-library.md        ← AI 声学应用场景库（S1-S16，按行业）
│   ├── competitor-brief.md        ← 竞品速查（14+ 家厂商拆解与应对）
│   ├── industry-benchmarks.md     ← 分行业 ROI 基准与关键参数
│   ├── decision-patterns.md       ← 企业类型 → 决策链模式
│   └── dual-version-rules.md      ← 双版本产出规则（硬红线+诚实底线）
└── templates/
    ├── assessment-report-template.md   ← Markdown 报告模板
    └── assessment-report-template.html ← HTML 网页报告模板
```

### Step 2：重启 Claude Code，skill 自动加载

### Step 3：验证

对话中输入"帮我分析一下这家公司"即可触发；也可在 `/` 命令中查看 skill 是否加载。

---

## 使用方法

### 基础调用

```
帮我评估一下 {客户名称}，看和我们的声学AI检测方案相关性如何
```

### 带背景信息的调用

```
分析一下 {某汽车内饰Tier1}，他们主营座椅头枕和扶手，有30个听音工，我们已在接触他们的质量总监
```

### 触发关键词

客户评估 · 合作可行性 · 客户分析 · 打单评估 · 能不能打 · 值不值得跟 · 客户筛选

---

## 输出产物

每次评估产出 **两份文件**（保存到用户指定目录，未指定时 Claude 会先询问）：

| 文件 | 用途 |
|------|------|
| **Markdown 报告** `{客户简称}-AI声学合作评估-{日期}.md` | 完整文字报告，可提交评审 |
| **HTML 网页报告** `{客户简称}-AI声学合作评估-{日期}.html` | 商务蓝灰风格网页，浏览器打开、分享、投屏 |

报告结构（9 章）：Executive Summary → 公司画像（含实体谱系+窗口事件扫描）→ 生产工艺×AI关联 → 场景匹配 → 合作可行性（六维评分+杠杆价值双评级）→ 行动方案 → 风险 → 假设验证与反面观点 → 参考资料（T1/T2/T3 分级）

---

## 与配套 skill 的关系

| 场景 | 使用 skill |
|------|-----------|
| 任意行业的通用客户评估（不限于声学方案） | [customer-relevance-assessment](https://github.com/tongzhouAM/customer-relevance-assessment)（通用母版） |
| 判断某公司值不值得打（声学行业版） | **本 skill** |
| 锁定客户后做深度技术调研（异音特征、传感器布点） | [nvh-pre-sales-research](https://github.com/tongzhouAM/nvh-pre-sales-research) |
| 先筛选再深入 | 母版/本 skill → nvh-pre-sales-research（串联） |

本 skill 是通用母版（customer-relevance-assessment）的声学行业垂直实例：流程一致，领域知识（场景库/竞品库/方案组件）预置在 references。

---

## 注意事项

1. **评估结果基于公开信息**：所有分析来自互联网公开数据，部分结论需实地验证
2. **报告中的财务数据**：注意标注数据年份与时效性
3. **场景匹配需要技术确认**：P0 场景深度展开是方法论推演，实际部署前需现场勘察
4. **竞品信息定期更新**：`references/competitor-brief.md` 建议每季度刷新
5. **本仓库为通用化版本**：公司名、产品型号、客户名均已匿名化，使用前替换为贵方自己的方案组件与口径

---

## 版本

**v1.0.0** · 2026-11-17（公开通用版，源自内部 v1.7.1 通用化）

作者：tongzhouAM · MIT License
