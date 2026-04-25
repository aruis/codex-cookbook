# Dispatch Prompts

Use these as compact thread prompts. Treat them as starting points, not rigid scripts.

## In This File

- activation: `Summon 军师`
- delegation: `Send A 谋士`, `Send A 武将`, `Bring In 法正`
- orchestration: `Parallelism Check`, `Commit Judgment`

## Summon 军师

```text
Use $junshi. 军师先判断：
1. 这是不是系统层或跨模块问题
2. 是否值得按中长期利益设计
3. 这次是军师自己处理，还是需要调度别人
先给结论和下一步动作，不要直接铺开长文档。
```

## Send A 谋士

```text
Use $junshi. 请从谋士池派一人，先做系统层分析，不要急着展开详细设计。
重点回答：
1. 这次任务本质在引入什么系统层变化
2. 现有实现路径哪里已经能支持
3. 结构缺口在哪
4. 现在是否已经足够进入执行
```

## Send A 武将

```text
Use $junshi. 请从武将池派一人执行当前任务。
要求：
1. 先按当前边界落地主链路
2. 接通必要模块、依赖关系或执行链路
3. 做最小验证闭环
4. 回报进展、偏差、风险和验证结果
```

## Bring In 法正

```text
Use $junshi. 请让法正在收束阶段介入。
任务：
1. 做 review 或提交前校核
2. 补测试或验证闭环
3. 给出 submit-readiness 判断
4. 如被明确指派，再处理 commit-side handling
```

## Parallelism Check

```text
Use $junshi. 军师先判断这次是否适合并发。
只有在任务边界清晰、写入范围基本不重叠时才并发。
一旦出现强耦合或共享写入，就收回串行。
```

## Commit Judgment

```text
Use $junshi. 请判断当前是否适合 commit。
重点不是是否完美完成，而是：
1. 是否偏离批准边界
2. 已知遗留是否已说清
3. 高风险任务是否已经过法正提交前校核
请直接给出是否适合收敛到提交点的建议，不默认等于自动执行 git commit。
```
