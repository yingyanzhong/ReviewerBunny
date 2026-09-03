# ReviewerBunny🐰 — WorkBuddy 论文审稿专家（心理学 / 临床心理学 / 医学）

面向心理学、临床心理学与医学领域作者的 WorkBuddy 专家（Agent 型）。它按同行评审人标准审阅论文初稿或返修稿，核查期刊适配、研究设计、测量、伦理、统计、报告规范与结论，输出内容严格对应的中英文两份 Markdown 审稿意见报告。

## 类型

`expertType: "agent"`（单专家，非专家团）。

## 专家身份

- **名字**：审稿兔🐰（英文 ReviewerBunny🐰，自称「兔兔 / 小兔子」）
- **职业**：心理学·临床心理学·医学论文审稿专家
- **头像**：`avatars/expert.png`（512×512，≤500KB）
- **行业分类**：`12-IndustryConsultant`（学术审稿属于跨领域专业咨询服务，不对应产品/技术/营销等更具体的分类；与现有临床专家保持同一分类）

## 目录结构

```text
reviewerbunny/
├── .codebuddy-plugin/
│   └── plugin.json          # 专家包清单（名称、展示信息、分类、标签、quickPrompts）
├── agents/
│   └── reviewerbunny.md     # 专家定义：身份 + 语气隔离 + 称呼规则 + 能力 + 流程 + 输出规范 + 铁律
├── skills/
│   ├── SKILL.md             # 审稿总纲领（6 步流程、8 检查点、报告模板、处理建议标准、话术、自检）
│   └── references/          # 备选调用（按需加载，不默认全读）
│       ├── 心理统计审稿Skill.md            # 定量稿件统计专项核查
│       ├── reporting-guidelines.md         # 报告规范索引（CONSORT/STROBE/PRISMA/STARD/TRIPOD/COREQ/CARE/SPIRIT/JARS 等）
│       ├── statistics-checklist.md         # 统计方法学检查清单
│       ├── statistics-from-liu-hongyun.md  # 刘红云《高级心理统计》方法与易错点
│       ├── 心理学论文常用统计方法与易错点总结.md
│       ├── 高级心理统计_刘红云.docx / 【教材】高级心理统计 刘红云.pdf
│       ├── SOUL.md          # 小兔子人格与对话语气（迁移自「小兔子persona.md」）
│       └── USER.md          # 对使用者的称呼规则（迁移自根目录 USER.md）
├── avatars/
│   └── expert.png           # 专家头像
└── README.md
```

## 设计要点

1. **渐进式披露**：`agents/reviewerbunny.md` 承载身份、能力概览与输出规范；审稿纲领在 `skills/SKILL.md`；领域知识下沉到 `skills/references/` 按需加载。
2. **研究类型 → 报告规范映射**：审稿的本质是「对照标准」，映射表是审稿纲领的灵魂。
3. **不编造铁律**：所有意见以原文为依据，缺什么标什么；每条意见定位到章节/图表/行（有行号指明行号，无行号指明章节与段落）。
4. **意见分级**：Major（影响结论可信度）vs Minor（表述/格式），每条意见 = 问题 + 为何重要 + 建议 + 定位。
5. **推荐意见判定标准**：Accept / Minor Revision / Major Revision / Reject，给出可执行阈值。
6. **双语输出**：`<稿件名>-review-en.md` 与 `<稿件名>-review-zh.md` 内容严格一一对应。
7. **语气隔离**：与用户对话时用兔兔语气并遵守称呼规则（见 `skills/references/SOUL.md`、`USER.md`）；**任何审稿报告严禁出现兔兔语气、emoji、昵称或对用户的亲密称呼**，报告通篇使用客观、专业、克制的学术语言。

## 使用方式

- 用户提交论文（PDF/docx）或粘贴稿件内容，并告知目标期刊；要求「审稿 / 评审 / peer review / 给审稿意见 / 扮演审稿人 / 评估这篇论文能否发表 / 按审稿人标准提意见」时激活。
- 一修：完整评估并检索目标期刊及 Precision Medication、General Psychiatry 近 5 年相关论文推荐引用。
- 二修及以后：先建立上一轮意见的逐点核查表（已充分解决 / 部分解决 / 未解决 / 新增问题），再决定是否提出新意见；若上一轮未推荐过上述两刊论文，按一修要求补充推荐。

## 安装到 WorkBuddy

专家必须放在 WorkBuddy 的「我的专家」目录才能被检测到：

```text
%USERPROFILE%\.workbuddy\plugins\marketplaces\my-experts\plugins\reviewerbunny\
```

1. 将本目录（除 `.git/`、`.workbuddy/` 外）复制到上述路径；
2. 将插件条目注册到 `%USERPROFILE%\.workbuddy\plugins\marketplaces\my-experts\.codebuddy-plugin\marketplace.json` 的 `plugins` 数组：

```json
{
  "name": "reviewerbunny",
  "source": "./plugins/reviewerbunny",
  "description": "（与 plugin.json 的 description 一致）"
}
```

3. 重启 WorkBuddy，在「专家中心 - 我的专家」中找到「审稿兔🐰」。
4. 官方自动化方式：在 WorkBuddy 中召唤 `expert-manager` 技能，执行 `validate_expert.py` 与 `register_expert.py` 完成校验与注册。

## 后续可扩展方向

- `skills/references/domain-psychometrics.md`：心理测量专项（量表信效度、临界值、文化适应）。
- `skills/references/reviewer-ethics.md`：审稿伦理与 COPE 规范。
- `skills/templates/review-report.docx`：Word 版审稿报告模板。
- `skills/scripts/`：PDF 稿件解析辅助脚本（如需要）。
