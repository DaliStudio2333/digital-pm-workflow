---
name: digital-pm-workflow
description: >
  数字产品经理工作流。用于对AI智能体平台类项目进行系统化需求分析与工作量评估。
  三步走：需求采集 → 建模与结构化 → 技术复杂度拆解。
  适用场景：(1) 用户需要从模糊需求文档中提取结构化PRD、用户故事、BPMN、Skill契约；
  (2) 用户需要对智能体/工具平台进行L1→L2功能点级的人天评估；
  (3) 用户需要输出Markdown+Excel格式的工作量评估文档。
  (4) 用户需要生成面向客户展示的PDF文档。
  触发词：需求分析、建模与结构化、复杂度拆解、工作量评估、Skill契约、BPMN建模、PRD、用户故事地图。
---

# 数字产品经理工作流

对AI智能体平台类项目进行系统化的需求分析和工作量评估，三步走流程。

## 核心方法论

### 角色切换

本工作流需要在三类角色间灵活切换：

- **PM（结构框架）**: 定义模块边界、识别共用模式、输出结构化文档
- **业务专家（领域逻辑）**: 补充具体业务规则的数量级、复杂度和不确定性（如财务口径规则、质检标准、法务条款库）
- **架构师（技术判断）**: 双态架构（敏态ReAct/稳态LangChain）、数据源策略、Skill注册体系

### 架构约定（智能体平台项目通用）

当项目涉及智能体平台时，默认遵循以下架构约定（从实际项目中提炼，新项目可调整）：

1. **双态分层**: 敏态数字员工(ReAct+Harness, 智能化为目标) / 稳态工具智能体(LangChain CLI, 自动化为目标)
2. **Skill开放体系**: 稳态工具封装为CLI → Skill注册中心 → 敏态Agent通过Tool Calling调度
3. **工具间零预置依赖**: 所有编排决策由敏态Agent在ReAct循环中实时完成
4. **双入口模式**: 人类→IM对话→数字员工(敏态) / 人类→Web工作台→工具直连(稳态)
5. **三层架构**: L1 应用交互层 → L2 智能体层(数字员工+Skill体系+工具智能体) → L3 平台底座层

## 三步工作流

### 步骤1: 需求采集

- 输入: 用户提供的需求文档(HTML/MD/对话/Excel)
- 角色: PM
- 动作: 从已有文档中提取半结构化需求，识别模糊地带，在对话中向用户确认补充信息
- 输出: 对需求文档的完整理解（记在脑中，不单独写文档）

### 步骤2: 建模与结构化

详见 `references/output-templates.md` 中的完整模板。

**必需产出:**
1. 全栈架构图 (ASCII art, 三层解耦)
2. 敏态层: BPMN调度序列图(Mermaid) + 数字员工用户故事 + 内部引擎定义
3. Skill开放体系: 注册/发现/权限/版本/监控 模块定义
4. 稳态工具: Skill契约(YAML: id/params/returns)、内部BPMN(Mermaid)、用户故事
5. 领域对象模型 (敏态层+稳态层+L1/L3)
6. L1/L3层: 定义范围，标注V1/V2
7. V1/V2功能边界清单 + Skill注册清单汇总

**角色切换提示:** 建模时遇到领域逻辑（如财务规则条数、质检标准、法务条款分类），主动切换到业务专家角色并询问用户确认。

### 步骤3: 技术复杂度拆解

详见 `references/evaluation-guide.md` 中的完整评估标尺和格式。

**评估标尺:**
- 低: 0.5-1人天 (CRUD/正则/标准库)
- 中: 1.5-3人天 (规则>5条/LLM Prompt/状态管理)
- 高: 3-8人天 (复杂计算/LLM多轮调优/CV训练/重交互)

**必需产出:**
1. 每个稳态工具 L1模块→L2功能点 逐项拆解 (复杂度+人天+业务备注)
2. 敏态数字员工引擎 (共享引擎 + Per-agent Harness)
3. Skill开放体系管理面 (发现/权限/版本/监控/网关)
4. L1应用交互层 (WEB工作台 + IM集成)
5. L3平台底座层 (RAG + 日志 + 推理 + 存储)
6. 共用组件清单 (独立评估，避免重复计入)
7. 交叉引用矩阵 (工具→共用组件 ✓标注)
8. 前置依赖阻塞项清单
9. 按敏态Owner汇总 + 全栈总计

**格式要求:** 同时输出 `.md` 文件（详细分析）和 `.xlsx` 文件（表格化，含复杂度颜色标注）。

## 步骤4: 生成客户展示PDF

### 双视图文档体系

产出需要同时满足两个用途：
1. **研发交付视图**: 技术架构、接口契约、AI Coding Prompts
2. **客户展示视图**: Executive Summary、ROI分析、交付路线图、用户采纳指南

### 客户展示文档清单

| 文档 | 用途 | 必需 |
|------|------|------|
| `v8_00_项目提案_Executive_Summary.md` | 高管汇报、立项评审 | ✅ |
| `v8_01_业务价值分析.md` | ROI分析、投资决策 | ✅ |
| `v8_04_交付路线图.md` | 项目管理、期望管理 | ✅ |
| `v8_05_用户采纳指南.md` | 推广、培训、变更管理 | ✅ |
| `v8_06_API端点清单.md` | 接口开发、前后端联调 | ✅ |
| `v8_07_AI_Coding_Prompts/` | AI辅助开发 | 可选 |

### 图表处理流程

文档中的图表需要转换为高清PNG嵌入PDF：

#### 图表类型识别

| 类型 | 识别方法 | 处理方式 |
|------|---------|---------|
| ASCII art框图 | 检测`┌┐└┘│`字符 | 多模态AI理解→HTML复刻→截图 |
| ASCII art树形 | 检测`├└│─`字符 | 多模态AI理解→HTML复刻→截图 |
| ASCII art甘特图 | 检测时间线+团队分工 | 多模态AI理解→HTML复刻→截图 |
| Mermaid图表 | 检测` ```mermaid ` | Playwright渲染→高清截图 |

#### 多模态AI处理ASCII图表

**关键流程**：先截图→AI理解→HTML复刻

**关键配置参数**：

```python
# 2K高清配置
SCREENSHOT_CONFIG = {
    "ascii": {
        "viewport_width": 2560,
        "viewport_height": 1440,
        "device_scale_factor": 2,  # 2x缩放，保证清晰度
    },
    "mermaid": {
        "viewport_width": 2560,
        "viewport_height": 1440,
        "device_scale_factor": 2,
    },
}

# 创建页面时设置device_scale_factor
page = await browser.new_page(
    viewport={"width": 2560, "height": 900},
    device_scale_factor=2  # 关键：2x缩放
)
```

**CSS注入使背景透明**（关键步骤）：

```python
await page.evaluate("""() => {
    const style = document.createElement('style');
    style.textContent = `
        body { 
            background: transparent !important; 
            padding: 0 !important; 
            margin: 0 !important;
        }
        * { background-color: transparent !important; }
    `;
    document.head.appendChild(style);
}""")
```

**完整处理流程**：

```python
# 1. 渲染ASCII文本为临时截图
await page.goto(f"file:///{temp_html}")
await page.screenshot(path=temp_screenshot)

# 2. 多模态AI查看截图，理解结构
# (AI读取截图，理解视觉布局)

# 3. 基于理解生成HTML
# (AI生成高质量HTML，复刻原始结构)

# 4. 注入CSS使背景透明
await page.evaluate("""() => {
    const style = document.createElement('style');
    style.textContent = 'body { background: transparent !important; padding: 0 !important; margin: 0 !important; } * { background-color: transparent !important; }';
    document.head.appendChild(style);
}""")

# 5. 使用page.screenshot截取 + 裁剪去除空白
screenshot_bytes = await page.screenshot(full_page=True, omit_background=True)
img = Image.open(io.BytesIO(screenshot_bytes))
if img.mode != 'RGBA':
    img = img.convert('RGBA')
bbox = img.getbbox()
if bbox:
    img = img.crop(bbox)  # 裁剪去除空白
img.save(output_path)
```

#### Mermaid高清渲染

**关键配置**：

```python
# Mermaid渲染配置
# 1. 初始viewport宽度设置为2000px
# 2. 等待Mermaid渲染完成（4秒）
# 3. 设置#container最小宽度为1800px
# 4. 使用container.screenshot截取
```

**完整代码**：

```python
# 1. 加载Mermaid HTML
await page.set_viewport_size({"width": 2000, "height": 1200})
await page.goto(f"file:///{temp_html}")
await page.wait_for_timeout(4000)  # 等待mermaid渲染完成

# 2. 注入CSS使背景透明，设置#container最小宽度
await page.evaluate("""() => {
    const style = document.createElement('style');
    style.textContent = `
        body { 
            background: transparent !important; 
            padding: 0 !important; 
            margin: 0 !important;
        }
        * { background-color: transparent !important; }
        #container {
            min-width: 1800px !important;
            padding: 20px !important;
        }
    `;
    document.head.appendChild(style);
}""")
await page.wait_for_timeout(300)

# 3. 使用container.screenshot截取
container = page.locator('#container')
if await container.count() > 0:
    screenshot_bytes = await container.screenshot(omit_background=True)
else:
    screenshot_bytes = await page.screenshot(full_page=True, omit_background=True)

# 4. 保存为PNG
img = Image.open(io.BytesIO(screenshot_bytes))
if img.mode != 'RGBA':
    img = img.convert('RGBA')
img.save(output_path)
```

**效果对比**：

| 配置 | 修改前 | 修改后 |
|------|--------|--------|
| viewport | 固定2560x1440 | 动态获取内容尺寸 |
| #container宽度 | 无限制 | min-width: 1800px |
| 图片尺寸 | 600x544 | 3680x2820 |
| 清晰度 | 模糊 | 高清 |

### PDF生成流程

```bash
# 使用V3脚本处理所有文档
python scripts/md_to_pdf_pipeline_v3.py \
    --ascii-html-dir ascii_html \
    file1.md file2.md file3.md
```

**脚本功能**：
- 自动识别文档中的ASCII图表和Mermaid图表
- ASCII图表：输出临时截图供AI处理
- Mermaid图表：直接渲染为高清PNG
- 生成`*_with_images.md`（图片版）
- 生成`*.pdf`（带样式的PDF）

### 文件结构

```
数字产品经理产出/
├── scripts/
│   ├── md_to_pdf_pipeline_v3.py     # 图表处理+PDF生成脚本
│   ├── render_ascii_preview.py      # ASCII文本渲染为临时截图
│   └── test_render.py               # 测试脚本
├── ascii_html/                      # AI生成的图表HTML
├── ascii_preview/                   # ASCII文本临时截图
├── images/                          # 最终高清PNG
├── pdf/                             # PDF输出
└── *_with_images.md                 # 带图片引用的MD版本
```

## 参考示例

本次项目中产出的成品文档可作为格式参考：

**技术视图**:
- `v8_02_建模与结构化_数字产品经理输出.md`
- `v8_03_技术复杂度拆解_数字产品经理输出.md`
- `v8_03_技术复杂度拆解.xlsx`

**客户展示视图**:
- `v8_00_项目提案_Executive_Summary.md`
- `v8_01_业务价值分析.md`
- `v8_04_交付路线图.md`
- `v8_05_用户采纳指南.md`

如需查看完整示例，引导用户提供上述文件的路径。
