# Contributing

欢迎补充新的开放 Agent 模型、修正数据或提交可复现实验结果。

## 新增模型

请同时更新 `README.md` 和 `data/agents.json`，并至少提供：

- 模型名称、发布组织和主要 URL；
- 权重或代码的开放形式及许可证；
- 总参数量、激活参数量、上下文长度；不能确认的字段可以留空；
- 主要应用方向和技术特点；
- benchmark 名称、成绩、评测配置、结果来源和核对日期。

优先引用模型卡、官方代码仓库、论文和榜单原始页面。新闻报道和社交媒体可以作为线索，不作为成绩的唯一证据。

## 成绩标注

- 项目方模型卡或仓库中的数字标为 `model author`。
- 独立榜单结果标为 `third-party leaderboard`，并给出榜单 URL。
- 本仓库复现结果标为 `repository reproduction`，同时提交配置、日志和环境信息。
- 不要省略影响结果的 agent scaffold、harness、上下文长度、采样参数和运行次数。
- 同名 benchmark 使用不同版本时，名称中保留版本号。

提交前请确认 JSON 可以正常解析，并检查 README 中的链接。
