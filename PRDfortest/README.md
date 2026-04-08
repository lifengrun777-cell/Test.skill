# 软件测试 Agent 工具库

一个基于 Trae IDE 的智能软件测试工具库，通过 AI Agent 技术实现测试流程自动化。

## 项目简介

本项目旨在打造一个软件测试用的 Agent 工具库，通过模块化的 Skill 设计，实现从需求分析到测试用例生成的全流程自动化支持。

## 项目结构

```
PRDfortest/
├── .trae/
│   └── skills/                          # Skill 仓库
│       ├── requirement-integrator/      # Skill 1: 需求整合器
│       │   └── SKILL.md                 # Skill 定义文件
│       │
│       ├── test-case-generator/         # Skill 2: 功能测试用例生成器
│       │   └── SKILL.md                 # Skill 定义文件
│       │
│       ├── performance-test-generator/  # Skill 3: 性能测试用例生成器
│       │   └── SKILL.md                 # Skill 定义文件
│       │
│       └── jmeter-test-generator/       # Skill 4: JMeter 测试脚本生成器
│           └── SKILL.md                 # Skill 定义文件
│
├── input/                               # 输入文件目录
│   ├── requirements/                    # 原始需求文档（Word/TXT/PDF/XMind）
│   └── api-docs/                        # 接口文档（JSON/YAML/Markdown）
│
├── output/                              # 输出文件目录
│   ├── requirements/                    # 需求整合器输出的 MD 文档
│   ├── test-cases/                      # 功能测试用例输出
│   └── performance-tests/               # 性能测试输出
│       ├── 性能测试方案.md              # 性能测试方案文档
│       └── jmeter/                      # JMeter 测试脚本
│           ├── performance_test.jmx     # JMeter 测试脚本
│           ├── csv/                     # 测试数据目录
│           └── performance_test_guide.md # 使用文档
│
├── src/                                 # 源代码目录
│
└── README.md                            # 项目说明文档
```

## 工作流程

```
┌─────────────────────────────────────────────────────────────┐
│                        输入文件                              │
│  input/requirements/ (XMind, Word, PDF, TXT)                │
│  input/api-docs/ (JSON, YAML, Markdown)                     │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│              Skill 1: requirement-integrator                │
│                    需求整合器                                │
│  - 整合 XMind 与文档                                         │
│  - 语义分析与匹配                                            │
│  - 生成标准化需求规格说明                                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                   中间产物                                   │
│  output/requirements/ (需求规格说明 MD 文档)                 │
└────────────┬───────────────────────────────────┬────────────┘
             │                                   │
             ▼                                   ▼
┌──────────────────────────┐      ┌──────────────────────────┐
│ Skill 2:                 │      │ Skill 3:                 │
│ test-case-generator      │      │ performance-test-        │
│ 功能测试用例生成器        │      │ generator               │
│                          │      │ 性能测试用例生成器        │
│ - 等价类划分              │      │ - 需求分析                │
│ - 边界值分析              │      │ - 接口映射                │
│ - 场景法                  │      │ - 场景设计                │
│ - 错误推测法              │      │ - 思考时间设置            │
└────────────┬─────────────┘      └────────────┬─────────────┘
             │                                   │
             ▼                                   ▼
┌──────────────────────────┐      ┌──────────────────────────┐
│ 输出:                     │      │ 输出:                     │
│ output/test-cases/       │      │ output/performance-tests/│
│ (功能测试用例 MD 文档)    │      │ (性能测试方案 MD 文档)    │
└──────────────────────────┘      └────────────┬─────────────┘
                                               │
                                               ▼
                                  ┌──────────────────────────┐
                                  │ Skill 4:                 │
                                  │ jmeter-test-generator    │
                                  │ JMeter 测试脚本生成器     │
                                  │                          │
                                  │ - 脚本结构生成            │
                                  │ - CSV 数据配置            │
                                  │ - 认证流程支持            │
                                  │ - 高级功能                │
                                  └────────────┬─────────────┘
                                               │
                                               ▼
                                  ┌──────────────────────────┐
                                  │ 输出:                     │
                                  │ output/performance-tests/│
                                  │ jmeter/                  │
                                  │ (.jmx 脚本 + CSV 数据)   │
                                  └──────────────────────────┘
```

## 功能模块

### Skill 1: 需求整合器 (requirement-integrator)

**功能描述**：将非结构化的需求文档（Word/TXT/PDF）与结构化的思维导图进行深度整合。

**输入**：`input/requirements/` 目录中的 XMind 文件和需求文档

**输出**：`output/requirements/` 目录中的标准化需求规格说明（MD 格式）

**核心能力**：
- 文档整合：整合 Word/TXT/PDF 与 XMind 文件
- 语义分析：识别不同来源中的同一需求点
- 关联匹配：通过语义匹配关联文件
- 规格生成：生成标准化需求规格说明
- 冲突检测：识别并标注矛盾描述

**使用方式**：
1. 将 XMind 文件和需求文档放入 `input/requirements/` 目录
2. 告诉 Agent："请整合这些需求文档"
3. Agent 将自动生成需求规格说明到 `output/requirements/` 目录

---

### Skill 2: 功能测试用例生成器 (test-case-generator)

**功能描述**：根据需求规格说明文档（MD 格式）生成全面的功能测试用例。

**输入**：`output/requirements/` 目录中的需求规格说明文档

**输出**：`output/test-cases/` 目录中的功能测试用例文档

**核心能力**：
- 需求分析：深入理解需求文档，提取功能点和业务逻辑
- 测试设计：运用等价类划分、边界值分析、场景法和错误推测法
- 用例生成：生成结构化、可执行的测试用例
- 覆盖率分析：确保测试用例覆盖所有功能点和异常场景

**输出格式**：
- 严格使用 Markdown 表格格式
- 包含：用例编号、测试模块、测试标题、前置条件、测试步骤、测试数据、预期结果、优先级

**使用方式**：
1. 确保需求规格说明已存在于 `output/requirements/` 目录
2. 告诉 Agent："请根据需求文档生成测试用例"
3. Agent 将自动生成功能测试用例到 `output/test-cases/` 目录

---

### Skill 3: 性能测试用例生成器 (performance-test-generator)

**功能描述**：根据需求文档和接口文档设计性能测试方案和用例。

**输入**：
- `output/requirements/` 目录中的需求规格说明文档
- `input/api-docs/` 目录中的接口文档（JSON/YAML/Markdown 格式）

**输出**：`output/performance-tests/` 目录中的性能测试方案文档

**核心能力**：
- 需求分析：识别核心业务流程、关键用户路径和业务目标
- 接口映射：将业务场景与接口文档中的具体接口进行关联
- 场景设计：设计负载、压力、并发等性能测试场景
- 思考时间设置：设置合理的思考时间，模拟真实用户行为

**测试类型**：
- 负载测试 (Load Testing)
- 压力测试 (Stress Testing)
- 并发测试 (Concurrency Testing)
- 容量测试 (Volume Testing)
- 稳定性测试 (Stability Testing)

**接口文档格式**：
- JSON 格式（.json）
- YAML 格式（.yaml, .yml）
- Markdown 格式（.md）

**使用方式**：
1. 确保需求规格说明已存在于 `output/requirements/` 目录
2. 将接口文档放入 `input/api-docs/` 目录
3. 告诉 Agent："请生成性能测试方案"
4. Agent 将自动生成性能测试方案到 `output/performance-tests/` 目录

---

### Skill 4: JMeter 测试脚本生成器 (jmeter-test-generator)

**功能描述**：根据 API 文档生成 JMeter 性能测试脚本（.jmx）和测试数据文件。

**输入**：`input/api-docs/` 目录中的接口文档（JSON/YAML/Markdown 格式）

**输出**：`output/performance-tests/jmeter/` 目录中的 JMeter 测试脚本

**输出结构**：
```
output/performance-tests/jmeter/
├── performance_test.jmx          # JMeter 测试脚本
├── csv/                          # 测试数据目录
│   ├── scenario1_data.csv
│   ├── scenario2_data.csv
│   └── ...
└── performance_test_guide.md     # 使用文档
```

**核心能力**：
- 脚本结构生成：创建符合 JMeter 5.6.3+ 规范的测试计划
- CSV 数据配置：生成参数化测试数据文件
- 认证流程支持：实现登录、Token 提取和管理
- 高级功能：文件上传、JSON Body、路径参数等

**脚本特性**：
- TestPlan：根元素与用户定义变量
- ThreadGroup：可配置并发、启动时间、循环次数
- HTTP Request Defaults：服务器、端口、协议配置
- HTTP Header Manager：Content-Type、Authorization 头
- Response Assertion：状态码验证
- Listeners：结果查看器

**使用方式**：
1. 将接口文档放入 `input/api-docs/` 目录
2. 告诉 Agent："请生成 JMeter 测试脚本"
3. Agent 将自动生成 .jmx 脚本和 CSV 数据文件到 `output/performance-tests/jmeter/` 目录

**执行测试**：
```bash
# GUI 模式
jmeter -t output/performance-tests/jmeter/performance_test.jmx

# 命令行模式
jmeter -n -t output/performance-tests/jmeter/performance_test.jmx -l results.jtl -e -o report/
```

---

## 快速开始

### 环境要求

- Trae IDE
- PowerShell 5.0+
- Python 3.14+ (用于 PDF 解析)
- JMeter 5.6.3+ (用于执行性能测试)

### 使用流程

#### 完整流程（推荐）

```bash
# 1. 将原始需求文档放入输入目录
将 XMind 文件和需求文档放入 input/requirements/

# 2. 将接口文档放入接口文档目录
将接口文档（JSON/YAML/Markdown）放入 input/api-docs/

# 3. 执行需求整合
告诉 Agent："请整合这些需求文档"
→ 生成 output/requirements/需求规格说明.md

# 4. 生成功能测试用例
告诉 Agent："请根据需求文档生成测试用例"
→ 生成 output/test-cases/功能测试用例.md

# 5. 生成性能测试方案
告诉 Agent："请生成性能测试方案"
→ 生成 output/performance-tests/性能测试方案.md

# 6. 生成 JMeter 测试脚本
告诉 Agent："请生成 JMeter 测试脚本"
→ 生成 output/performance-tests/jmeter/performance_test.jmx
```

#### 单独使用某个 Skill

```bash
# 直接使用功能测试用例生成器
将需求规格说明放入 output/requirements/
告诉 Agent："请生成测试用例"

# 直接使用性能测试用例生成器
将需求规格说明放入 output/requirements/
将接口文档放入 input/api-docs/
告诉 Agent："请生成性能测试方案"

# 直接使用 JMeter 测试脚本生成器
将接口文档放入 input/api-docs/
告诉 Agent："请生成 JMeter 测试脚本"
```

## 扩展计划

- [x] Skill 1: 需求整合器
- [x] Skill 2: 功能测试用例生成器
- [x] Skill 3: 性能测试用例生成器
- [x] Skill 4: JMeter 测试脚本生成器
- [ ] Skill 5: 测试报告生成器
- [ ] Skill 6: 缺陷分析助手
- [ ] Skill 7: 测试数据生成器
- [ ] Skill 8: 接口测试用例生成器

## 技术栈

- AI Agent: Trae IDE 内置
- 文档处理: PowerShell + Word COM
- PDF 解析: Python + PyPDF2
- 思维导图: XMind 格式解析
- 接口文档: JSON/YAML/Markdown 解析
- 性能测试: JMeter 5.6.3+
- 测试方法论: 等价类划分、边界值分析、场景法、错误推测法

## 贡献指南

欢迎贡献新的 Skill 或改进现有 Skill：

1. Fork 本仓库
2. 在 `.trae/skills/` 下创建新的 Skill 目录
3. 编写 `SKILL.md` 定义文件
4. 更新 README.md 中的工作流程图
5. 提交 Pull Request

## 许可证

MIT License

## 更新日志

### v1.3.0 (2026-04-08)
- 新增 Skill 4: JMeter 测试脚本生成器
- 新增 JMeter 脚本输出目录 `output/performance-tests/jmeter/`
- 支持 .jmx 脚本和 CSV 数据文件生成
- 支持认证流程、文件上传等高级功能
- 更新工作流程图，反映 JMeter 脚本生成流程

### v1.2.0 (2026-04-08)
- 新增接口文档输入目录 `input/api-docs/`
- 优化 performance-test-generator skill，支持 JSON/YAML/Markdown 格式接口文档
- 新增接口映射功能，将业务场景与接口进行关联
- 新增思考时间设置，模拟真实用户行为
- 更新工作流程图，反映接口文档输入

### v1.1.0 (2026-04-08)
- 优化项目结构，分离输入输出目录
- 更新 test-case-generator skill，优化工作流程
- 统一所有 skill 的输入输出路径
- 添加工作流程图

### v1.0.0 (2026-04-08)
- 初始化项目结构
- 实现 Skill 1: 需求整合器
- 实现 Skill 2: 功能测试用例生成器
- 实现 Skill 3: 性能测试用例生成器
