# JMeter 测试脚本输出目录

此目录用于存放 jmeter-test-generator skill 生成的 JMeter 测试脚本和相关文件。

## 目录结构

```
jmeter/
├── performance_test.jmx          # JMeter 测试脚本
├── csv/                          # 测试数据目录
│   ├── scenario1_data.csv
│   ├── scenario2_data.csv
│   └── ...
└── performance_test_guide.md     # 使用文档
```

## 文件说明

### performance_test.jmx
- JMeter 测试脚本文件
- 可直接在 JMeter GUI 中打开
- 支持命令行执行

### csv/ 目录
- 存放测试数据文件
- 支持 UTF-8 编码
- 用于参数化测试

### performance_test_guide.md
- 测试脚本使用说明
- 包含执行步骤和注意事项

## 使用说明

1. 此目录中的文件由 jmeter-test-generator skill 自动生成
2. 基于 `input/api-docs/` 目录中的接口文档
3. 请勿手动修改此目录中的文件，以免被覆盖

## 执行测试

### GUI 模式
```bash
jmeter -t output/performance-tests/jmeter/performance_test.jmx
```

### 命令行模式
```bash
jmeter -n -t output/performance-tests/jmeter/performance_test.jmx -l results.jtl -e -o report/
```

### 分布式测试
```bash
jmeter -n -t output/performance-tests/jmeter/performance_test.jmx -R server1,server2
```
