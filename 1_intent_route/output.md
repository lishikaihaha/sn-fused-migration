# 出参

| 字段 | 类型 | 说明 |
|---|---|---|
| 产物=01.json | object | 出参即产物，字段如下 |
| intent_summary | string | 意图摘要；query 明示文字引号逐字引用 |
| complex_text | bool | 复杂文字类任务开关 |
| word_tasks | string[] | complex_text=true 时的文字任务拆解（位置/角色：逐字内容） |
| extracted_entities | string[] | 去格式词实体清单 |
| need_search / search_dimensions | bool / string[] | 检索判定（本链知识循环关闭，仅留档） |
| text_in_image | string[] | query 明示画面文字逐字摘录（保真第一手） |
| layout_row | string | 选定的版式路由行键（中文，如「数据/指标」；取值只能来自 system 清单方括号内） |
| style_row | string | 选定的风格路由行键（中文，如「数据分析」） |