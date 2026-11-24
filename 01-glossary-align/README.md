# 01 术语锁定的段落级双语对照

单点：**术语表强制约束 + 段落级双语对照 + 机器质检**。不追求全文润色。

## 快速开始
```
python scripts/pdf_to_paras.py --in paper.pdf --out work/paras.jsonl
python scripts/glossary.py extract --paras work/paras.jsonl --out work/cand.csv
# 填好译名后
python scripts/glossary.py lock --in work/cand.csv --out out/glossary.csv
# Agent 按 SKILL.md §3 逐段翻译，产出 out/bilingual.json
python scripts/qc.py --paras work/paras.jsonl --bi out/bilingual.json --glossary out/glossary.csv --out out
python eval/metrics.py --skill out --base <基线结果目录>   # 可选
```

## 已验证
`python examples/selftest.py`：取段 7 段、术语 16 条、正例五项比率 1.00，三类注入缺陷全部命中。

## 依赖
Python 3.9+；PDF 解析需 PyMuPDF 或 pypdf（缺失时脚本会明确降级并告警），其余脚本仅标准库。

## 限制
不做 OCR、不转写图片公式、不评价译文文采；术语表需人工/Agent 填译名后锁定。

## 示例声明
`examples/demo` 为自建演示文本与示例输出，**非平台正式案例，不含真实论文断言**。
