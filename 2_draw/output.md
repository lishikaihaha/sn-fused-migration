# 出参

| 字段 | 类型 | 说明 |
|---|---|---|
| 产物=02.json | object | 出参即产物，字段如下 |
| layout / style | string | 抽中的版式/风格英文 id（执行标识符，定位定义文件） |
| layout_zh / style_zh | string | 中文名（展示层） |
| layout_trace / style_trace | object | {row(英文行键), row_zh, picked(步骤1原值), caliber(归行口径), fallback, drawn, is_primary, pool_size} |