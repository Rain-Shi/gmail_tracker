# Gmail Interview Tracker 自动化项目

> 自动从 Gmail 邮箱中抽取邮件，筛选和面试相关的内容，利用 GPT-4 自动提取公司名、面试状态、面试时间、面试地点，最终生成标准 JSON 文件，方便个人面试信息管理。

## 项目功能介绍

-调用 Gmail API 获取最新邮件
-自动筛选和面试相关的邮件
-调用 OpenAI GPT-4 模型提取关键信息
-自动保存多种 json 数据：
  - 全量邮件 json
  - 面试相关邮件 json
  - GPT 提取结果 json
-支持自定义关键词筛选
-自动日志打印，方便调试

## 项目结构
```
gmail_interview_tracker/
├ config.py                      # 配置文件
├ gmail_client.py                # Gmail API 操作逻辑
├ daily_runner.py                # 每日抽取邮件入口
├ gpt_extractor.py               # GPT 自动提取面试信息
├ mail_parser.py                 # 邮件内容清洗、辅助处理
├ requirements.txt               # Python 依赖
├ output/                        # 自动生成的数据文件
  ├ 2025-04-10.json             # 全量邮件数据
  ├ 2025-04-10_interview.json   # 筛选的面试相关邮件
  ├ 2025-04-10_result.json      # GPT 提取的面试关键信息
└ venv/                         # Python 虚拟环境
```

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

### 4. 获取 Gmail API credentials.json

- 访问 https://console.cloud.google.com/
- 创建 Project
- 启用 Gmail API
- OAuth Consent Screen 配置
- 创建 OAuth 2.0 Client ID
- 下载 credentials.json
- 放至项目目录：
```
gmail_interview_tracker/credentials.json
```

### 5. 初始化 OAuth2 授权
```bash
python daily_runner.py
```

授权成功后，项目目录生成 token.pickle


## 使用流程

### Step 1. 抽取 Gmail 邮件
```bash
python daily_runner.py
```

### Step 2. GPT 提取面试信息
```bash
python gpt_extractor.py
```

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

## 后续可扩展方向

| 功能 | 描述 |
|------|------|
| 自动推送 Notion | 面试信息同步 Notion 数据库 |
| 自动同步 Google Sheet | 方便统计管理 |
| 自动发 Telegram/微信提醒 | 即时获取面试动态 |
| 定时任务自动运行 | Windows bat / Linux crontab |

---

## 项目作者

项目作者：Shi Jinze  
项目定位：面试信息管理自动化工具  
适用场景：求职者 / 数据分析 / 机器学习工程师  
技术风格：高内聚，易扩展，工程实践标准

---

