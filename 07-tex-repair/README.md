# 07 模板适配 + 编译收敛

单点：**模板要求逐项对齐 → 编译根因定位 → 构建清单可复现**。

## 快速开始
```
python scripts/texfit.py --project work/paper --template work/template.yaml --out out
python scripts/build.py  --project work/paper --out out --rounds 3
python scripts/logdiag.py --log out/main.log --out out      # 单独分析已有日志
```

## 已验证
`python examples/selftest.py`：
- 损坏工程命中 T01–T08 全部 8 类、10 处违规
- 修复版 0 违规
- 真实 TeX Live 2022 日志：E10×2、E01×2、E02×1，警告 E05/E06，行号定位到 13/19/30
- 本机无 TeX 时 `build.py` 返回 `static_only` 并注明未编译

## 真实编译
见 `examples/demo/compile_evidence.md`：修复版在 TeX Live 2022 下 `errors=0 / undefined=0 / pages=2`；损坏版两轮仍失败，错误分类如上。

## 依赖
Python 3.9+；`texfit.py` 仅标准库（读 YAML 需 PyYAML，缺省时可用 JSON 模板）；`build.py` 需 TeX 发行版，缺省时降级为静态模式。

## 限制
- 静态检查覆盖常见规则，不替代真实编译；宏包内部语义错误只能靠日志。
- 中文排版依赖 ctex/xeCJK，需镜像预装字体。
- Overfull 只报告不自动重排，避免"缩字号掩盖"。

## 示例声明
`examples/demo` 的工程、模板、日志为自建样例；日志片段来自真实 pdflatex 输出，非平台案例结果。
