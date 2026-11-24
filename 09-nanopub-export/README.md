# 09 断言拆解 + 标准序列化

单点：**一句一断言 → 逐字证据 → JSON-LD/TriG 四层导出 → 回解析校验**。

## 快速开始
```
python scripts/nanopub.py build --assertions work/assertions.json --sources work/sources.json --out out
python eval/metrics.py --out_dir out
```

## 已验证
`python examples/selftest.py`：5 条断言全部原子、逐字、来源完整，TriG 回解析一致；四类缺陷（并列句、改写证据、缺段落号、重复）全部命中。

## 输入格式
- `sources.json`：`{sources:[{source_id, paragraph_id, text}]}`
- `assertions.json`：`{case_id, paper:{title,year,doi|doi_reason}, assertions:[{id,text,subject,relation,object,qualifier,evidence,confidence,derivation}]}`
- 关系词表：increases / decreases / supports / contradicts / uses / measured_by / located_in / composed_of / exceeds / has_value

## 依赖
Python 3.9+，仅标准库（导出为文本 TriG/JSON-LD，不依赖 rdflib）。

## 限制
不做签名与网络发布；关系词表封闭；不伪造页码；不解析图表内部数值。

## 示例声明
`examples/demo` 为构造文本与示例输出，**非真实论文、非平台案例**。
