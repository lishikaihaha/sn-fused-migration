# 融合链迁移包（sn-fused v3.0，sn 上游结构，2026-11-05）

中文用户 query → 生图 prompt 扩写链：**4 次 LLM + 1 程序段**。
真源 = `pipeline_app/prompts.py`（build_*）+ `pipeline_app/assets/`——本包由
`export/export_sn_fused.py` 程序化导出，与执行侧逐字一致。

## 段序与数据流

```
query ──1意图扩充⊕选行(LLM)──▶ 01.json{7意图字段+layout_row+style_row}
      └─2行校验+抽签(程序)──▶ 02.json{layout/style英文id+中文名+trace}
            └─3内容分析(LLM)──▶ 03.json{analysis 23字段}
                  └─4结构化(LLM)──▶ 04.json{layout}（sn 结构策划：分节+视觉元素+文字标签）
                        └─5扩写(LLM,终稿)──▶ 05.json{prompt}（空间组织按版式定义现场生成）
                              └─6终稿(程序)──▶ 06.json{final}
```

## 段落目录 ↔ 运行产物映射

| 包内目录 | 段 | 类型 | 运行产物（out/<案号>/） |
|---|---|---|---|
| 1_intent_route/ | 1 意图扩充⊕选行 | LLM | 01.json |
| 2_draw/ | 2 行校验+抽签 | 程序（draw.py 可执行） | 02.json |
| 3_analysis/ | 3 内容分析 | LLM | 03.json |
| 4_structured/ | 4 结构化内容 | LLM | 04.json |
| 5_expand/ | 5 扩写（终稿） | LLM | 05.json（05_system.md=system 留痕） |
| 6_final/ | 6 终稿提取 | 程序 | 06.json（+06_final.txt 兼容副本） |

## 调用规范

1. **${} 变量注入**：整串替换（值原样替换占位符，不二次转义）；变量在模板中
   只出现一次；缺传变量会原样残留（配置错误信号）。
0. **三条规范（v3.1）**：①步骤纯数字编号 1~6，每步一个目录、一个输出 JSON
   （出参即产物，01.json~06.json）；②所有 prompt 输入用点路径变量标注来源——
   `${input.query}`=链路输入、`${N.field}`=步骤N输出 JSON 的字段、`${N}`=步骤N
   输出 JSON 全文、`${N.layout_def}` 类=按步骤N字段从 assets 派生的文件内容。
2. **LLM 调用形态**：system + user 两消息；①③④按 system 内 JSON 契约解析
   输出，⑤a/⑤b 为自由 markdown/散文输出。
3. **定义文件读取**：`assets/sn_infographic/{layouts_zh,styles_zh}/<id>.md`
   中文优先，缺失回落英文 `{layouts,styles}/` 同名文件。
4. **评测口径**：seed 按 cid 派生（md5 前 8 位十六进制）保抽签复现；
   交互跑 seed 缺省真随机（同类 query 行内多样性）。

## 与上游 sn-infographic 的本地裁定

1. 抽签去掉 3 张行外随机票（原 ~6% 无关选型）；
2. 行选择由 ① LLM 清单语义选行（替代上游 data_type 开放串模糊匹配）；
3. 门禁 20 问已删（默认全走扩写）；结构策划遵循 sn 本位（住④结构化内容，无独立版式规划段）；
4. 白名单守卫（记录制）：key_data_points_verbatim 数字词元级存活检查；
5. 输出语言钉子（⑤ 输出语言节）。

上游来源：github.com/OpenSenseNova/SenseNova-Skills（MIT），中文对照文档见
项目 `_sn_research/sn-infographic-迁移包/`。
