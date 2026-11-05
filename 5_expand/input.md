# 入参

| 变量 | 类型 | 来源/说明 |
|---|---|---|
| ${prompt} | string | 本步完整 user prompt 文本，四段构成（段间 --- 分隔）：「④结构化内容：\n${4.layout}」「## 选中版式：${2.layout_zh}（${2.layout}）\n${2.layout_def}」「## 选中风格：${2.style_zh}（${2.style}）\n${2.style_def}」「用户语言：${3.user_language}——终稿必须以该语言书写，与用户原始 query 同语种」 |
${prompt} 内嵌变量来源 | — | ${4.layout}=步骤4输出 04.json 的 layout 字段（④结构化内容，原文或序列化 JSON 文本）；${2.layout_zh}/${2.layout}/${2.style_zh}/${2.style}=步骤2输出 02.json 字段（抽中版式/风格的中文名/英文 id）；${2.layout_def}/${2.style_def}=assets 派生（非步骤2输出），按英文 id 读取 assets/sn_infographic/{layouts,styles}_zh/<id>.md 定义全文（缺失回落英文目录）；${3.user_language}=步骤3输出 03.json 的 user_language 字段（zh→「简体中文（Simplified Chinese）」；缺失默认简体中文） |