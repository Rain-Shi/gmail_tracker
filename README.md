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
### 4. credentials.json 获取步骤
为了获取 Gmail 邮件，需要配置 Google Cloud 项目，并下载 OAuth2 授权文件 credentials.json。

第一步：打开 Google Cloud Console
网址：https://console.cloud.google.com/

第二步：创建一个 Project
左上角 → 选择项目 → 新建项目

名称可自定义：

nginx
复制
编辑
Gmail Interview Tracker
第三步：启用 Gmail API
左侧菜单：API & Services → Library

搜索 Gmail API

点击 → 启用

第四步：配置 OAuth 同意屏幕
左侧菜单：API & Services → OAuth consent screen

选择 External（外部）

填写 App Name（比如 Gmail Interview Tracker）

添加自己的 Gmail 作为 Test User（测试用户）

第五步：创建 OAuth 2.0 Client ID
左侧菜单：Credentials（凭据）

点击 Create Credentials → OAuth Client ID

Application Type 选择 Desktop App

点击创建

第六步：下载 credentials.json
Google 会自动下载这个文件，命名类似：

pgsql
复制
编辑
client_secret_xxx.json
第七步：放到你的项目根目录
放在：

bash
复制
编辑
gmail_interview_tracker/credentials.json
（可重命名为 credentials.json）

第八步：首次运行自动授权
运行：

bash
复制
编辑
python daily_runner.py
程序会自动打开浏览器进行 OAuth2 登录授权。登录你自己的 Gmail，授权后会在项目目录自动生成：

复制
编辑
token.pickle
这个文件用于保存授权信息，后续不会再弹授权窗口。
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
