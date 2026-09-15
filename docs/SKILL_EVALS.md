# Skill Activation Evals

用这些请求检查 skill 的触发边界。重点不是固定回答措辞，而是确认模型选择了最窄的工作流、没有无意义地加载其他角色，也没有因为旧式门禁过度停顿。

| 请求 | 期望 Skill | 期望行为 |
| --- | --- | --- |
| “我想把定位任务从 CE 改成 PBR，帮我设计对照实验和成功标准。” | `research-planning` | 先检查现有目标与证据，给出方案、基线、验证和风险；不直接静默改训练逻辑。 |
| “给现有数据生成器增加一个 128×96 版本，并检查 shape、split 和坐标。” | `research-data` | 使用真实流水线生成/验证新版本；不修改模型。 |
| “配置已经定了，给 trainer 加这个 loss，并跑一个真实尺寸 smoke test。” | `research-implementation` | 直接实现并验证；不要求重新确认 Draft Plan。 |
| “用刚验收的配置启动正式训练，记录 GPU、commit、seed、run 路径和 checkpoint。” | `research-experiment` | 核对运行合同后执行已明确请求的 run；不增加重复确认。 |
| “这个 README 有个错字，顺手修一下。” | 无专用 research skill | 直接修复；不触发 research planning。 |
| “看看昨天的训练为什么挂了，先别改模型。” | `research-experiment` | 先读运行状态和日志，区分基础设施与研究行为问题；不修改模型语义。 |
| “这个 batch 的 label 好像错位了，帮我定位原因。” | `research-data` | 先检查数据/坐标合同与真实样本；若最终确认是 loader 实现 bug，再交给 implementation。 |
| “把这个模块重构一下，行为和接口都不要变。” | `research-implementation` | 在既定合同内完成重构和必要验证；不触发 planning。 |

## 不完整输入

- “帮我做个新数据集。”：触发 `research-data`，先从项目现有约定和源数据调查能确定的内容；只有样本语义、标签或输出合同无法可靠推断时再问关键问题。
- “跑一下实验。”：触发 `research-experiment`；先寻找已有已验收配置、最近明确的 run 合同和资源约束。若存在多个会导致不同研究结论或明显不同成本的候选项，再询问用户。
- “我想换个网络。”：触发 `research-planning`，因为方法边界尚未稳定；先明确为什么换、比较对象和成功标准。

## 反例与过度触发检查

- 单纯查资料、解释概念、查看代码、修错字，不应因为“科研项目”四个字就触发四个 skill。
- 已经明确授权的可逆实现任务，不应被 `research-planning` 的 Draft Plan 门禁拦住。
- 数据 skill 不应为了“让训练能跑”修改 loss/model；experiment skill 不应为了“让结果更好”静默换数据或 checkpoint。
- 同一个请求需要多个阶段时可以依次使用多个 skill；只有边界独立时才并行，避免多个 Agent 同时修改同一文件、数据版本或外部 run。

## 回归检查

修改任意 skill 的 `description` 后，至少重新验证：一个直接正例、一个同义间接正例、一个输入不完整例、一个不应触发的反例，以及一个容易越权或臆测的边界例。
