# 08 双栏阅读顺序重排

单点：**只修阅读顺序**——通栏块分带、带内左栏整栏→右栏、剔除跨页重复页眉页脚、合并断词与续段，并给出页码/坐标供回查。

## 快速开始
```
python scripts/reflow.py --pdf paper.pdf --out out --audit
python eval/measure.py --out out --truth truth.json     # 有已知真值时
python scripts/reflow.py --pdf paper.pdf --out base --baseline   # 朴素基线对照
```

## 已验证（自建已知真值样本）
`examples/tools/make_demo.py` 生成 2 页双栏 PDF（23 块，每块带 `[[Pn]]` 标记）+ `truth.json`：

| 指标 | 本 Skill | 朴素 y→x 基线 |
|---|---|---|
| 位置命中率 | 1.00 | 0.3043 |
| 逆序对 | 0 | 20 |
| 相邻错位 | 0 | 18 |
| order_match | true | false |

真实运行产物在 `examples/expected/{reflow,baseline}/`。

## 输出
- `paragraphs.jsonl`：`{id,page,col,bbox,text,order_index}`，顺序即阅读顺序
- `reflow.json`：页数、栏数判定、剔除的页眉页脚、串栏疑似位置
- `reflow.md`：人读版

## 依赖
PyMuPDF（fitz）。无 PyMuPDF 时脚本会明确报错，不静默降级。

## 限制
不做表格结构、公式识别、OCR；无可靠双栏证据时判 `layout=single` 而不硬分栏。

## 示例声明
`examples/expected` 来自 `make_demo.py` 构造的样本，**非真实论文、非平台案例**。
