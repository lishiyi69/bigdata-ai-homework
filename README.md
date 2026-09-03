# 大数据与人工智能课程作业

本仓库用于存放《大数据与人工智能》课程的作业、实验代码与学习笔记。

## 仓库结构

```
.
├── assignments/   # 课程作业（每次作业一个子目录）
├── labs/          # 实验 / 上机代码
├── notes/         # 学习笔记
└── README.md
```

## 环境说明

- 语言：Python 3.x
- 常用库：NumPy、Pandas、Matplotlib、scikit-learn、PyTorch 等

## 提交规范

- 每次作业放在 `assignments/` 下对应编号的子目录，例如 `assignments/01`、`assignments/02`
- 每个作业目录内建议包含：代码、说明文档（README）、必要的运行说明
- 提交信息（commit message）建议采用 `作业N：简短描述` 的格式
- 大文件（数据集、模型权重等）不要直接提交，放入本地 `data/` 目录（已在 `.gitignore` 中忽略）
