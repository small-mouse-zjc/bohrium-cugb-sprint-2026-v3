# 04 相关工作：从矩阵到空白

单点：**先建"工作×维度"矩阵 → 由共同局限推空白 → 逐句绑定引用与贡献证据**。

## 快速开始
```
python scripts/matrix.py build --works work/works.json --dims work/dimensions.json --out out
python scripts/claim_bind.py --draft out/intro_draft.md --works work/works.json --manuscript work/manuscript.json --out out
python eval/metrics.py --out_dir out [--base_dir 基线目录]
```

## 已验证
`python examples/selftest.py`：6 篇文献、5 个分组、1 条可推导空白、1 处冲突；正例四项比率 1.00；四类注入缺陷全部命中。

## 输入格式
- `works.json`：每篇需 `wid/route/problem/data/metric/limit/limits/addresses/evidence{locator,quote}`，可选 `stance`、`key`、`label`。
- `dimensions.json`：五维键名与显示名。
- `manuscript.json`：本文已有 sections / figures / tables，用于校验贡献证据。

## 依赖
Python 3.9+，仅标准库。

## 限制
语义层面的"转述是否准确"需人工抽检；关键词法判定论断偏严；不生成真实文献。

## 示例声明
`examples/demo` 为构造演示：文献编号与元数据均为虚构，仅用于验证矩阵与核对器，**不得作为真实引用**；非平台案例结果。
