# 入参

| 变量 | 类型 | 来源/说明 |
|---|---|---|
| ${input.query} | string | 链路输入 query 原文（user 消息「## 用户原始 query」节） |
| ${3} | string(JSON) | 步骤3输出 03.json 全文 JSON（user 消息「## 内容分析结果（analysis）」节；system「## 用户输入」表的 ${3.*} 行为其内键） |