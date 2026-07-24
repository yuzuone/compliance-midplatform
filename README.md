# Zero-Trust Compliance Mid-Platform

零信任合规审查中台 — 基于 FastAPI 的企业级数据隐私合规自动化工具。

在企业出海场景中，跨境数据合规审查面临两个核心矛盾：合同审查繁琐（需逐条对照多国法规），以及 PII 数据直接传入云端大模型存在泄露风险。本中台通过 PII 脱敏 + 法规知识图谱 + 规则引擎实现“脑手分离”架构，在前端 Dashboard 完成全流程闭环。

## 功能

| 功能            | 描述                              |
| ------------- | ------------------------------- |
| **PII 识别与脱敏** | 自动检测身份证号、手机号、邮箱、银行卡号，策略化脱敏后输出   |
| **合同合规审查**    | 上传 DOCX/TXT 合同文档，自动检测数据隐私违规条款   |
| **红线批注**      | 审查意见以 Word 批注形式直接标注在原文档上，下载带批注版 |
| **法规知识库**     | 导入中国法律法规全文（如 PIPL），自动拆分为结构化条款   |
| **多域审查规则**    | 覆盖数据隐私、跨境传输、AI 治理等合规领域          |
| **主题切换**      | Light/Dark 双主题，玻璃拟态 UI          |

## 快速启动

```bash
# 1. 安装依赖
pip install fastapi uvicorn python-docx python-multipart

# 2. 启动统一服务（端口 8100）
cd compliance-midplatform
python -m uvicorn app:app --host 0.0.0.0 --port 8100

# 3. 打开 Dashboard
# http://localhost:8100
```

## 使用流程

### 合同审查（4 步走）

1.  **上传文档** — 粘贴文本或拖拽 .txt/.docx 合同文件

2.  **PII 识别** — 自动检测并脱敏身份证号、手机号等敏感信息

3.  **合规审查** — 规则引擎扫描合同条款，输出审查发现问题

4.  **导出报告** — 下载带红线批注的 Word 文档

### 法规导入

1.  点顶栏「导入法规」

2.  拖拽法律文件（.txt/.docx）或粘贴全文

3.  系统自动解析条款结构，存入知识库供规则引擎检索

## 项目结构

    compliance-midplatform/
    ├── app.py                        # 统一服务入口 (FastAPI + Uvicorn)
    ├── static/
    │   └── dashboard.html            # 前端 Dashboard (原生 HTML/CSS/JS)
    ├── services/
    │   ├── pii_engine/               # PII 识别与脱敏引擎
    │   ├── knowledge_base/           # 法规知识库 (SQLite)
    │   ├── document_engine/          # Word 红线批注渲染
    │   └── api_gateway/              # API 网关
    ├── tests/                        # 端到端测试
    └── output/                       # 测试模板与输出样本

## 技术栈

| 层级     | 技术                     |
| ------ | ---------------------- |
| 后端框架   | FastAPI + Uvicorn      |
| 知识库    | SQLite (DELETE 日志模式)   |
| 文档处理   | python-docx            |
| PII 检测 | 正则引擎 + 规则策略            |
| 前端     | 原生 HTML/CSS/JS (零框架依赖) |
| 主题     | CSS 变量 + 玻璃拟态          |

## 许可证

MIT
