# 行校验 + 行内抽签（纯程序，无 LLM；可执行实现见本目录 draw.py）

1. 输入：步骤1输出 01.json 的 layout_row / style_row 字段（中文行键）；
2. 四级容错归行（规范化比较，忽略大小写与空格）：英文行键 → 中文行键 →
   英文票池名（主选/备选 id）→ 中文票池名，任一命中即归该行；
3. 全不命中 → 兜底行（版式「总览/汇总」、风格「专业商务」），留痕 fallback=true；
4. 行内加权抽签：票池 = 主选×10 + 每个备选×9（无行外票）；
   rng=random.Random(seed)，版式先抽、风格后抽（共用一 rng，顺序固定）；
   seed 缺省=真随机（交互多样性），评测侧按 cid 派生（复现）；
5. 抽中名在 assets/sn_infographic/layouts_zh|styles_zh/<id>.md 无定义文件时
   → sn 原兜底：版式 hub-spoke、风格 corporate-memphis；
6. 输出 02.json。

## 输出格式
输出 02.json（单 JSON）：{"layout": "<英文id>", "style": "<英文id>", "layout_zh": "<中文名>", "style_zh": "<中文名>", "layout_trace": {row, row_zh, picked, caliber, fallback, drawn, is_primary, pool_size}, "style_trace": {同左}}。

用法：python 2_draw/draw.py --layout-row "数据/指标" --style-row "数据分析" --seed 42
