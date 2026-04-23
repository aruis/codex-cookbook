# Dispatch Prompts

Use these as compact thread prompts. Treat them as starting points, not rigid scripts.

## In This File

- activation: `Summon 军师`, `Bare Activation`, `Exit 军师 Mode`
- delegation control: `Task-First Delegation`, `Delegation Authorization Check`, `Delegate With Role Skill`, `Short Delegation Patterns`
- async coordination: `Async Delegation Reminder`
- analysis and execution: `Call A 谋士`, `Ask 谋士 To Deepen`, `Draft Checklist`, `Send One 武将`, `Consider Parallel 武将`, `Collapse Parallel Work`
- convergence: `Bring In 文臣`, `Check Submit Readiness`, `Judge Over-Abstraction`, `Decide Commit`

## Summon 军师

```text
Use $junshi. 军师先判断：
1. 这是不是系统层或跨模块问题
2. 是否值得按中长期利益设计
3. 这次是军师自己处理，还是需要调度池子
先给结论和下一步动作，不要直接铺开长文档。
```

## Bare Activation

```text
Use $junshi. 如果用户只说“召唤军师”而没有给具体任务，不要展开流程说明或任务框架。
只做短确认，例如：
“进入军师模式。把要接管的事直接发来。”
后续对话默认继续按军师模式处理，不要要求用户每轮重复召唤。
```

## Organize A Check Or Push

```text
Use $junshi. 这次“看一下 / 推进 / 评审 / 检查”默认理解为组织合适的人来做，不是让军师亲自把所有细节做完。
军师先判断应由谁来处理，再收敛结论给我。
```

## Task-First Delegation

```text
Use $junshi. 军师模式下，收到新的用户请求时，先判断这是不是一个任务式请求。
如果是，先判断是否能优先派给谋士、文臣或武将，而不是军师自己先上手。
只有任务极小、无法调度，或直接处理明显更便宜时，军师才亲自做。
```

## Delegation Authorization Check

```text
Use $junshi. 如果军师判断这次合理任务应优先调兵，但当前用户表述还不足以构成明确 delegation 授权，不要自己硬做。
先从合适池子里选一个人，再用一句最短确认补问，例如：
“这次我派马超（subagent）执行可以么？”
“这次我派马良（subagent）做提交前校核可以么？”
“这次我派法正（subagent）先做系统层分析可以么？”
一旦用户明确同意，就立刻按编制调兵，不再重复解释流程。
默认把这份授权视为对当前 thread 持续有效，除非用户后续收回或限制。
```

## Delegate With Role Skill

```text
Use $junshi. 军师一旦决定派人，优先让被派出的人显式使用对应角色 skill，而不是每次从零解释职责。
例如：
- 法正 -> $junshi-moushi
- 马良 -> $junshi-wenchen
- 马超 -> $junshi-wujiang
派工时重点只说这次任务、边界和当前上下文。
```

## Short Delegation Patterns

```text
Use $junshi. 派工时尽量用短派工，不要长篇复述角色定义。优先采用：

1. 代号 + 对应角色 skill
2. 本次具体任务
3. 范围边界
4. 期望输出

示例：

法正，使用 $junshi-moushi。
任务：先做一轮 system-level analysis。
边界：只看当前需求相关的实现路径、结构缺口和是否可直接进入执行，不展开长方案。
输出：给军师一份简短结论。

马良，使用 $junshi-wenchen。
任务：做提交前校核。
边界：重点看边界偏移、已知遗留、收束质量；如果缺技术事实，再建议补派武将，不自己实现。
输出：给军师提交条件判断。

马超，使用 $junshi-wujiang。
任务：在当前批准边界内执行或核实技术事实。
边界：不要扩成大重构；如果触到新抽象或高风险区，立即回报军师。
输出：给军师进展、偏差、风险和验证结果。
```

## Async Delegation Reminder

```text
Use $junshi. 如果已派出的工作可以异步推进，不要原地忙等待 subagent 结果。
要求：
1. 不要因为非阻塞子任务而卡住整个 thread
2. 如果下一步更适合向我汇报状态、说明当前判断或等我进一步指令，就先回复我
3. 只有当下一步关键动作确实依赖该结果时，才等待 delegated work 返回
```

## Check Submit Readiness

```text
Use $junshi. 这次“看当前代码变动是否具备提交条件”默认不是让军师亲自审 diff。
请先组织一次提交前校核：
1. 默认先派文臣池看提交条件、遗留项、边界偏移和收束质量
2. 如果需要实现侧技术事实、主链路打通情况或局部可行性验证，再补派武将池
3. 军师只负责收结论并给出是否适合收敛到提交点的判断
除非 diff 极小或我明确要求军师亲自审，否则不要自己下场做主审。
```

## Exit 军师 Mode

```text
Use $junshi. 如果这次只是局部改动、没有明显系统层判断成本，也不值得启用池化调度，就退出军师模式。
军师只需要快速判断范围与复杂度，然后：
1. 自己直接处理，或
2. 只派一个武将执行
不要继续展开谋士、文臣或并行流程。
```

## Call A 谋士

```text
Use $junshi. 请从谋士池派一人，先做系统层分析，不要急着展开详细设计。
重点回答：
1. 这次任务本质在引入什么系统层变化
2. 现有实现路径哪里已经能支持
3. 结构缺口在哪
4. 现在是否已经足够进入执行
如果没有必要，不要升级到实现级分析。
军师自己不要再重复展开同层分析，等谋士结论回来后再收敛。
```

## Ask 谋士 To Deepen

```text
Use $junshi. 请让谋士补到实现级分析，但只围绕高风险部位展开。
重点看：
1. 核心数据或配置结构
2. 执行流程
3. 模块连接与依赖关系
4. 多模块或子系统边界
只补足执行所需的信息，不要写大而全方案。
```

## Draft Checklist

```text
Use $junshi. 请让谋士基于当前结论起草 task checklist。
要求：
1. 任务切片要围绕系统边界和实现边界
2. 写清 done criteria
3. 标出 open issues 和风险
4. 保持文档轻量，不写成长文
```

## Send One 武将

```text
Use $junshi. 请从武将池派一人执行当前任务。
要求：
1. 先按当前边界落地主链路
2. 接通必要模块、依赖关系或执行链路
3. 做最小验证闭环
4. 执行中允许局部调整，但不得静默改变任务目标和系统边界
5. 回报进展、偏差、风险、checklist 影响
除非已经退化成极小局部修补，否则不要由军师自己长期下场执行。
```

## Consider Parallel 武将

```text
Use $junshi. 军师先判断这次是否满足并行条件。
只有在以下都成立时才并行：
1. 能按系统边界或职责边界切开
2. write scope 基本不重叠
如果不满足，就维持单武将执行。
```

## Collapse Parallel Work

```text
Use $junshi. 军师重新判断是否需要终止并行、改回串行收敛。
重点检查：
1. 多个武将是否开始碰同一组核心文件或同一抽象层
2. 原本独立的边界是否已经证明强耦合
请直接给出继续并行还是收回并行的判断。
```

## Bring In 文臣

```text
Use $junshi. 请让文臣池在提交前介入。
任务：
1. 整理 checklist 当前状态
2. 校核执行期调整是否仍然合理
3. 明确已知遗留和暂不处理项
4. 给出是否已具备提交前收束条件
```

## Judge Over-Abstraction

```text
Use $junshi. 请判断是否应停止继续抽象，转入收敛。
重点看：
1. 新抽象是否还能明显提升复用性或系统清晰度
2. 新抽象是否已有明确复用场景
如果没有，就叫停继续深挖。
```

## Decide Commit

```text
Use $junshi. 请判断当前是否适合 commit。
重点不是是否完美完成，而是：
1. 是否偏离批准边界
2. 已知遗留是否已说清
3. 高风险任务是否已经过文臣池提交前校核
请直接给出是否适合收敛到提交点的建议，不默认等于自动执行 git commit。
```
