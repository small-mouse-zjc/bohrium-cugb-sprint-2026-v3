# 05 可复现方法章节

单点：**每个声明参数都能溯源到正文/配置/日志/代码**，并把方法章节补成"复现九项 + 步骤四要素 + 具体限制"的可执行说明。

## 快速开始
```
python scripts/param_align.py --draft methods.md --params params.json --sources config.yaml train.log model.py --out out
python scripts/repro_check.py --manifest manifest.json --steps steps.json --params out/params.csv --out out
python eval/metrics.py --out_dir out
```

## 已验证
自建演示：3 个声明参数（learning_rate / batch_size / seed）全部有源，无源数值 0、冲突 0；复现九项覆盖 1.00、步骤四要素完整率 1.00、限制具体率 1.00。四类缺陷（参数冲突、凭空数值、缺项、步骤不完整）全部命中。真实运行产物在 `examples/expected/`。

## 输入格式
- `params.json`：`{params:[{key, aliases, unit}]}`
- `manifest.json`：`code_version / env / deps / hardware / data{access,name,version,split,seed} / command / runtime / limitations`
- `steps.json`：`{steps:[{id,name,input,operation,output,decision}]}`

## 输出
`params.csv`（逐参数四状态 sourced/unsourced/conflict/omitted）、`audit.json`（无源数值泛扫）、`repro.json` + `repro.md`（九项与步骤检查）。

## 依赖
Python 3.9+，仅标准库。

## 限制
别名表需人工维护；单位换算不做；扫不到的隐含参数不会自动发现（只报 `unsourced_number`）。

## 示例声明
`examples/demo` 为构造配置与日志，**非真实实验、非平台案例**。
