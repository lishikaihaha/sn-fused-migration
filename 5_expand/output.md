# 出参

| 字段 | 类型 | 说明 |
|---|---|---|
| 产物=05.json | object | {"prompt": string}——中文散文终稿（约 400~800 字）；出参即产物（步骤6 取 prompt 字段 → 06.json {"final"}） |
| （程序侧守卫）verdict_guard | object | 步骤3 03.json.key_data_points_verbatim 数字词元级存活检查（记录制，missed 入 meta） |