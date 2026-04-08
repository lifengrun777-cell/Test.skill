# 性能测试输出目录

此目录用于存放性能测试相关的所有输出文件。

## 目录结构

```
performance-tests/
├── 性能测试方案.md              # performance-test-generator 生成的性能测试方案
└── jmeter/                      # jmeter-test-generator 生成的 JMeter 测试脚本
    ├── performance_test.jmx     # JMeter 测试脚本
    ├── csv/                     # 测试数据目录
    │   ├── scenario1_data.csv
    │   ├── scenario2_data.csv
    │   └── ...
    └── performance_test_guide.md # 使用文档
```

## 子目录说明

### 性能测试方案.md
- 由 `performance-test-generator` skill 生成
- 包含性能需求分析、测试场景设计、接口映射等内容
- 基于 `output/requirements/` 中的需求规格说明和 `input/api-docs/` 中的接口文档

### jmeter/
- 由 `jmeter-test-generator` skill 生成
- 包含可直接执行的 JMeter 测试脚本（.jmx）
- 包含参数化测试数据文件（CSV）
- 包含使用说明文档

## 使用说明

1. 此目录中的文件由相关 skill 自动生成
2. 请勿手动修改此目录中的文件，以免被覆盖
3. JMeter 脚本可直接用于性能测试执行

## 执行 JMeter 测试

```bash
# GUI 模式
jmeter -t output/performance-tests/jmeter/performance_test.jmx

# 命令行模式
jmeter -n -t output/performance-tests/jmeter/performance_test.jmx -l results.jtl -e -o report/
```
