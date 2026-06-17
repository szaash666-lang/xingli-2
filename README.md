# Mental Health Self Intake Skill

一个面向中文场景的skill，用于帮助来访者在咨询前做心理困扰自我梳理，并给出非诊断性的风险分层、诊断方向假设和求助建议。

## 适用场景

- 来访者想先整理自己的心理状态、困扰来源和功能受损情况。
- 心理咨询师需要一个基础情况调查和初步分流的访谈框架。
- 需要识别自伤、自杀、伤人风险，并优先给出安全行动建议。
- 需要把用户描述整理成结构化的咨询前摘要。

## 重要边界

这个 skill 不用于确诊，也不替代心理咨询师、精神科医生、急诊或危机干预服务。

它只输出：

- 初步风险等级：低 / 中 / 高 / 紧急
- 主要问题假设
- 可能需要专业评估的诊断方向
- 当前紧急程度
- 下一步求助建议
- 需要立即求助的信号

如果出现明确自杀计划、近期自伤/自杀行为、伤人风险、严重精神病性症状、严重物质使用或无法保证短期安全，skill 会要求暂停普通问卷，优先联系当地急救、危机热线或可信任的身边支持者。

## 文件结构

```text
mental-health-self-intake/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── assessment-framework.md
```

- `SKILL.md`：触发说明、核心边界、访谈流程和输出格式。
- `agents/openai.yaml`：Codex UI 元数据。
- `references/assessment-framework.md`：风险等级、判断框架、转介规则和参考来源。

## 使用方式

在 Codex 中调用：

```text
Use $mental-health-self-intake to help me梳理当前心理困扰并给出初步风险分层。
```

也可以用中文直接描述：

```text
我最近状态很差，想做一个心理咨询前的自测和风险判断。
```

## 输出格式

skill 会尽量使用如下结构：

```markdown
## 初步整理
- 当前主要困扰：
- 持续时间与诱因：
- 功能受损：
- 保护因素：

## 风险等级
- 等级：低 / 中 / 高 / 紧急
- 理由：
- 现在最需要做的安全动作：

## 主要问题假设
- 1.
- 2.
- 3.

## 诊断方向假设
- 可能需要专业评估的方向：
- 不足以判断或需要继续了解的信息：

## 建议下一步
- 立即：
- 未来 24-72 小时：
- 之后 1-2 周：

## 需要立即求助的信号
-

## 可继续追问的问题
-
```

## 验证

本地已使用官方 skill 校验脚本验证：

```bash
/opt/anaconda3/bin/python3 /Users/araraki/.codex/skills/.system/skill-creator/scripts/quick_validate.py "/Users/araraki/Documents/xingli 2/mental-health-self-intake"
```

结果：

```text
Skill is valid!
```

## 参考来源

- SAMHSA suicide warning signs: https://www.samhsa.gov/mental-health/suicidal-behavior/warning-signs
- SAMHSA 988 Lifeline: https://www.samhsa.gov/mental-health/988
- WHO mhGAP self-harm and suicide recommendations: https://www.who.int/teams/mental-health-and-substance-use/treatment-care/mental-health-gap-action-programme/evidence-centre/self-harm-and-suicide
- 国家卫健委《心理援助热线技术指南（试行）》: https://www.nhc.gov.cn/wjw/c100175/202101/ce4756ac40e742a48b00ff32d3807825.shtml
- 国家心理健康和精神卫生防治中心 12356 通知: https://ncmhc.org.cn/channel/newsinfo/7902
