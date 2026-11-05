# 入参

| 变量 | 类型 | 来源/说明 |
|---|---|---|
| layout_row / style_row | string | 步骤1输出 01.json 的 layout_row / style_row 字段 |
| draw.py | script | 本目录可执行实现（自包含，读 ../assets；CLI 见 logic.md） |
| routing_tables.json | object | 21+21 行定义（行键/主选/备选/票权/兜底），随包附 assets/ |
| zh_names.json | object | 行键与版式/风格名的中英映射，随包附 assets/ |
| seed | int\|null | 抽签种子（null=真随机） |