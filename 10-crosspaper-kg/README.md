# 10 跨篇别名图谱

单点：**两篇独立材料 → 跨篇同名归一（含"不得合并"的显式判定）→ 每条边绑逐字引文 → 可执行查询**。

## 快速开始
```
python scripts/kg.py build --corpus work/corpus.json --relations work/relations.json --queries work/queries.json --out out
python eval/metrics.py --out_dir out
```

## 已验证
`python examples/selftest.py`：19 条提及 → 11 节点（6 个跨篇节点）、6 条边全部逐字、1 条非合并判定（`sediment sample` 现场样 vs 实验室样）、4 条查询全部有证据；五类缺陷（变体未归一、冲突合并、改写引文、空查询、缩写无全称）全部命中。

## 输入格式
- `corpus.json`：`{papers:[{paper_id,doi,title,year,paragraphs:[{paragraph_id,text}],mentions:[{surface,type,paragraph_id,quote,attrs?}]}]}`
- `relations.json`：`{relations:[{id,paper_id,subject,predicate,object,paragraph_id,quote}]}`
- `queries.json`：`{queries:[{id,kind:node|edges|path|nonmerge,...}]}`
- 身份限定字段：`site / sample_id / model_id / dataset_id / conditions`

## 四条查询示例
1. `node "gas hydrate"` → 两篇的 GH 是否同一节点、证据分别在哪段
2. `edges "increases"` → 哪些论文报告了同一关系
3. `path "salinity" → "dissociation pressure"` → 证据链
4. `nonmerge` → 哪些同名术语不得合并、依据是什么

## 依赖
Python 3.9+，仅标准库。

## 限制
规则式归一（不做 ML 消歧），保守不合并；不解析图表数值；`paragraph_id` 为 JATS 段落号，不写页码。

## 示例声明
`examples/demo` 为构造的两篇独立材料与示例输出，**非真实文献、非平台案例**。
