# Role Routing

主 Agent根据任务的主要风险选择一个稳定角色；只有交接关系明确时才使用多个角色。

| 请求内容 | 负责人 | 必需交接 |
| --- | --- | --- |
| 需求澄清、系统边界、架构取舍、Draft Plan | 主 Agent | 已确认的接口、假设与风险 |
| 数据、标注、坐标、生成、预览、质量 | data_manager | 不可变数据路径、版本、数量、split、合同和验证 |
| 模型、代码、配置、Pipeline、loss、metric、测试 | implementation_manager | 兼容配置、接口合同、测试证据 |
| 训练、GPU、监控、ClearML/MLflow、checkpoint、结果 | experiment_manager | 任务 ID、命令、运行目录、状态和结果 |

标准交接顺序：

```text
用户想法
  → 主 Agent 讨论与调查
  → Draft Plan
  → 用户确认
  → data_manager（需要数据时）
  → implementation_manager（需要实现时）
  → experiment_manager（需要正式实验时）
  → 主 Agent 汇报与下一轮决策
```

主 Agent本身承担架构负责人职责。Pipeline 归实现角色。算力调度默认由 experiment_manager 负责；只有多机、多用户资源竞争成为独立问题时，才增加专门资源角色。
