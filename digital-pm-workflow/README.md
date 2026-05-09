# digital-pm-workflow

数字产品经理工作流 — 用于对 AI 智能体平台类项目进行系统化需求分析与工作量评估。

## 适用场景

1. 从模糊需求文档中提取结构化 PRD、用户故事、BPMN、Skill 契约
2. 对智能体/工具平台进行 L1→L2 功能点级的人天评估
3. 输出 Markdown + Excel 格式的工作量评估文档
4. 生成面向客户展示的 PDF 文档

## 三步工作流

### 步骤 1: 需求采集
- 输入：用户提供的需求文档（HTML/MD/对话/Excel）
- 角色：PM
- 输出：对需求文档的完整理解

### 步骤 2: 建模与结构化
- 全栈架构图（三层解耦）
- 敏态层：BPMN 调度序列图 + 用户故事 + 引擎定义
- Skill 开放体系：注册/发现/权限/版本/监控模块
- 稳态工具：Skill 契约（YAML）+ 内部 BPMN + 用户故事
- 领域对象模型
- V1/V2 功能边界清单

### 步骤 3: 技术复杂度拆解
- L1→L2 逐项拆解（复杂度 + 人天）
- 共用组件识别与交叉引用
- 按敏态 Owner 汇总 + 全栈总计
- 同时输出 `.md` 和 `.xlsx`

## 触发词

`需求分析` `建模与结构化` `复杂度拆解` `工作量评估` `Skill契约` `BPMN建模` `PRD` `用户故事地图`

## 文件结构

```
digital-pm-workflow/
├── SKILL.md                        # 核心 skill 指令
├── digital-pm-workflow.skill       # 打包格式
├── references/
│   ├── evaluation-guide.md         # 评估标尺与格式规范
│   └── output-templates.md         # 输出文档模板
└── README.md
```

## 安装

```bash
npx skills add DaliStudio2333/digital-pm-workflow
```
