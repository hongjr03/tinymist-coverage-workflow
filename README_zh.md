# Tinymist 覆盖率工作流

一个可重用的 GitHub Actions 工作流，用于使用 Tinymist 为 Typst 文档生成和追踪覆盖率报告。

## 特性

- ✅ 自动为 Typst 文档生成覆盖率报告
- ✅ 随时间追踪覆盖率变化
- ✅ 在 README 文件中添加覆盖率徽章
- ✅ 高度可配置，适应不同项目需求
- ✅ 适用于任何使用 Tinymist 的 Typst 项目

## 使用方法

### 基本设置

要在您的仓库中使用此工作流，请创建一个工作流文件（例如 `.github/workflows/coverage.yml`），内容如下：

```yaml
name: 覆盖率分析

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  coverage:
    uses: your-username/tinymist-cov/.github/workflows/tinymist-coverage.yml@main
    with:
      target_files: 'README.typ'  # 您的主要 Typst 文件
```

### 高级配置

您可以使用以下输入参数自定义工作流：

| 输入参数 | 描述 | 默认值 |
|---------|------|--------|
| `tinymist_version` | 使用的 Tinymist 版本 | `v0.13.10` |
| `setup_typship` | 是否设置 typship 开发环境 | `true` |
| `target_files` | 要分析的文件（逗号分隔） | `README.typ` |
| `report_path` | 存储覆盖率报告的路径 | `coverage/output` |
| `auto_commit` | 是否自动提交报告更新 | `true` |
| `readme_paths` | 要更新徽章的 README 文件（逗号分隔） | `README.md,README_zh.md` |

使用所有选项的示例：

```yaml
jobs:
  coverage:
    uses: your-username/tinymist-cov/.github/workflows/tinymist-coverage.yml@main
    with:
      tinymist_version: 'v0.14.0'
      setup_typship: false
      target_files: 'main.typ,docs/guide.typ'
      report_path: 'docs/coverage'
      auto_commit: false
      readme_paths: 'README.md'
```

## 覆盖率徽章

工作流成功运行后，它将在您指定的 README 文件中添加或更新覆盖率徽章：

[![Coverage](https://img.shields.io/badge/coverage-85.5%25-green)](coverage/output/coverage_report.md)

## 要求

- 包含 Typst 文件的 GitHub 仓库
- Tinymist 兼容的项目

## 工作原理

1. 工作流安装 Tinymist 和其他必要的依赖项
2. 它对您指定的文件运行覆盖率分析
3. 生成详细的覆盖率报告
4. README 文件使用覆盖率徽章进行更新
5. 更改被提交回仓库（如果启用了 auto_commit）
6. 报告作为工作流构件上传

## 许可证

MIT

## 贡献

欢迎贡献！请随时提交 Pull Request。
