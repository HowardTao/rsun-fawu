# 事项跟踪：本地 Markdown

本工程的规格和任务保存在 `.scratch/` 下。

## 文件约定

- 每个功能一个目录：`.scratch/<feature-slug>/`。
- 规格文件：`.scratch/<feature-slug>/spec.md`。
- 实施任务：`.scratch/<feature-slug>/issues/<NN>-<slug>.md`；从 `01` 起编号，每个任务一个文件。
- 实施任务顶部用 `Status:` 行记录分诊状态，角色字符串见 `triage-labels.md`。
- 评论与讨论历史追加到文件底部的 `## Comments` 下。

## 技能要求“发布到事项跟踪系统”时

按上述约定创建对应文件；目录不存在时创建目录。

## 技能要求“读取相关任务”时

读取引用路径的文件。仅给出编号时，在对应功能目录中定位；编号有歧义时先确认。

## Wayfinding operations

用于 `/wayfinder` 的决策规划；决策任务状态独立于实施任务的分诊状态。

- 地图：`.scratch/<effort>/map.md`，保存目标、说明、已决事项索引、尚未明确的问题与范围边界。
- 子任务：`.scratch/<effort>/issues/<NN>-<slug>.md`，从 `01` 起编号，正文记录要解决的问题。
- 类型：顶部 `Type:` 行，取值为 `research`、`prototype`、`grilling` 或 `task`。
- 状态：顶部 `Status:` 行，使用 `open`、`claimed`、`resolved`。
- 阻塞关系：顶部 `Blocked by: NN, NN` 行；列出的任务全部为 `resolved` 时解除阻塞，无依赖时写 `None`。
- 待处理任务：扫描子任务目录，选择处于 `open` 且没有未解决阻塞的任务，按编号升序处理。
- 认领：开始工作前设置 `Status: claimed` 并保存。
- 解决：在任务的 `## Answer` 下追加答案，设置 `Status: resolved`；在地图的已决事项索引中追加一句摘要及任务链接。
