# Stable Role References

`agents/` 只保存稳定角色的职责与交接参考，不再承担初始路由。Codex/ChatGPT 的 repo-scoped 工作流入口位于 `.agents/skills/`；模型先依据各 skill 的 `name + description` 做匹配，触发后再按需读取这里的角色细节。

| Skill | 稳定角色/职责 | 何时读取对应角色文档 |
| --- | --- | --- |
| `research-planning` | 主 Agent / 架构负责人 | 需要跨阶段交接、研究边界或 Draft Plan 时 |
| `research-data` | `data_manager` | 数据生成、标注、坐标、split、预览、质量和版本交付时 |
| `research-implementation` | `implementation_manager` | 模型、代码、配置、Pipeline、loss、metric 和验证交付时 |
| `research-experiment` | `experiment_manager` | 正式训练/评估、GPU、监控、checkpoint 和实验归档时 |

主 Agent仍是唯一的用户协调入口，但不要把所有角色文档预先塞入上下文。选择能够完成请求的最小 skill/角色集合；边界清楚、不会同时修改同一文件或外部状态的子任务可以并行。

典型的完整研究迭代可以是：

```text
用户想法
  → research-planning（仅在研究边界尚未稳定时）
  → research-data（需要新数据或数据变更时）
  → research-implementation（需要代码/模型变更时）
  → research-experiment（需要正式 run 时）
  → 主 Agent 汇总证据与下一轮决策
```

这不是强制流水线。只改配置、只验证数据或只查看一个已有实验时，应直接触发对应 skill，不必经过前置阶段。
