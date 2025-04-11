# gmail_tracker
绝对可以！我给你写一个完整版的专业 README.md，适合放到 GitHub 或者简历作品展示，内容详细，符合企业级规范。

---

# Gmail Interview Tracker 自动化项目

> 自动从 Gmail 邮箱中拉取邮件，筛选和面试相关的内容，利用 GPT-4 自动提取公司名、面试状态、面试时间、面试地点，最终生成标准 JSON 文件，方便个人面试信息管理。

---

## 项目功能介绍

本项目实现了完整的自动化面试信息管理流程：

- 调用 Gmail API 获取最新邮件
- 自动筛选和面试相关的邮件
- 调用 OpenAI GPT-4 模型提取关键信息
- 自动保存多种 json 数据：
  - 全量邮件 json
  - 面试相关邮件 json
  - GPT 提取结果 json
- 支持自定义关键词筛选
- 自动日志打印，方便调试

---

## 项目结构

```
gmail_interview_tracker/
├── config.py                      # 配置文件（API key、路径配置）
├── gmail_client.py                # Gmail API 操作逻辑
├── daily_runner.py                # 每日自动拉取邮件的入口
├── gpt_extractor.py               # GPT 自动提取面试信息
├── mail_parser.py                 # 邮件内容清洗、辅助处理
├── requirements.txt               # Python 依赖
├── output/                        # 自动生成的数据文件
│   ├── 2025-04-10.json             # 全量邮件数据
│   ├── 2025-04-10_interview.json   # 筛选的面试相关邮件
│   ├── 2025-04-10_result.json      # GPT 提取的面试关键信息
└── venv/                         # Python 虚拟环境
```

---

## 核心技术栈

| 技术 | 用途 |
|------|-----|
| Python 3.x | 项目开发语言 |
| Gmail API | 邮件获取 |
| OpenAI GPT-4 API | 面试信息提取 |
| JSON 数据 | 数据存储标准格式 |
| VSCode | 开发环境 |

---

## 环境配置步骤

### 1. 克隆项目
```bash
git clone 项目地址
cd gmail_interview_tracker
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
```

### 3. 配置 config.py
```python
GMAIL_SCOPES = ['https://www.googleapis.com/auth/gmail.readonly']
GMAIL_USER_ID = 'me'
OPENAI_API_KEY = 'your_openai_api_key'
OUTPUT_DIR = './output/'
```

---

## 使用说明

### Step 1. 拉取 Gmail 邮件
```bash
python daily_runner.py
```

运行效果：
- 自动拉取过去一天的所有邮件
- 自动保存：
```
output/2025-04-10.json
output/2025-04-10_interview.json
```

---

### Step 2. GPT 提取面试信息
```bash
python gpt_extractor.py
```

运行效果：
- 自动读取：
```
output/2025-04-10_interview.json
```
- 自动保存：
```
output/2025-04-10_result.json
```

---

## 面试信息提取结果示例

```json
[
  {
    "company": "Google",
    "status": "waiting",
    "interview_time": "April 15th, 2025 at 10:00 AM",
    "location": "Google NYC office"
  },
  {
    "company": "Meta",
    "status": "waiting",
    "interview_time": "April 20th, 2025 at 2:00 PM",
    "location": "Meta Menlo Park Campus"
  }
]
```

---

## 面试邮件筛选逻辑说明

在 daily_runner.py 中：
```python
INTERVIEW_KEYWORDS = ['interview', '面试', 'HR', 'recruiter', 'onsite', 'offer']
```

只要邮件的 subject 或 body 包含这些关键词，即视为面试相关邮件。

---


## 后续可扩展方向

| 功能 | 描述 |
|------|------|
| 自动推送 Notion | 面试信息同步 Notion 数据库 |
| 自动同步 Google Sheet | 方便统计管理 |
| 自动发 Telegram / 微信提醒 | 及时获取面试动态 |
| 定时任务自动运行 | Windows bat / Linux crontab |

---

## 作者信息

> 项目作者：Shi Jinze  
> 项目定位：面试信息管理自动化工具  
> 场景适用：求职者 / 数据分析 / 机器学习工程师  
> 技术风格：高内聚，易扩展，工程实践标准

---

---

要不要我：
1. 打包完整工程 zip 直接发你？
2. 自动生成 Windows bat 脚本定时跑？
3. 自动集成 Notion / Google Sheet / Telegram？

告诉我，我给你全安排！
