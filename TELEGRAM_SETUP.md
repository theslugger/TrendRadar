# 📱 Telegram Bot 推送设置指南

## 🤖 创建 Telegram Bot

### 第一步：创建 Bot
1. 在 Telegram 中搜索 `@BotFather`
2. 发送 `/newbot` 命令
3. 为你的 Bot 设置名称（例如：`TrendRadar News Bot`）
4. 设置用户名（例如：`trendradar_news_bot`，必须以 `bot` 结尾）
5. 获取 Bot Token（格式：`1234567890:ABCDEF1234567890abcdef1234567890ABC`）

### 第二步：获取 Chat ID
有以下几种方法获取 Chat ID：

#### 方法一：通过 API 获取（推荐）
1. 向你的 Bot 发送任意消息
2. 在浏览器中访问：`https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
3. 在返回的 JSON 中找到 `"chat":{"id":123456789}` 部分
4. 记录这个 Chat ID

#### 方法二：通过第三方 Bot
1. 搜索并启动 `@userinfobot`
2. 向它发送任意消息
3. Bot 会返回你的 Chat ID

#### 方法三：群组推送（可选）
如果想推送到群组：
1. 将你的 Bot 添加到群组
2. 给 Bot 管理员权限
3. 使用上述方法一获取群组的 Chat ID（通常是负数）

## ⚙️ 配置 GitHub Secrets

### 在 GitHub 仓库中设置 Secrets：

1. 进入你 Fork 的仓库
2. 点击 `Settings` → `Secrets and variables` → `Actions`
3. 点击 `New repository secret` 添加以下两个密钥：

**TELEGRAM_BOT_TOKEN**
- Name: `TELEGRAM_BOT_TOKEN`
- Value: 你的 Bot Token（例如：`1234567890:ABCDEF1234567890abcdef1234567890ABC`）

**TELEGRAM_CHAT_ID**
- Name: `TELEGRAM_CHAT_ID`
- Value: 你的 Chat ID（例如：`123456789`）

## 🔧 自定义配置

### 推送类型设置
在 `main.py` 的 CONFIG 中可以修改 `TELEGRAM_REPORT_TYPE`：

- `"current"` - 仅推送当次爬取结果
- `"daily"` - 仅推送每日汇总
- `"both"` - 同时推送当次爬取和每日汇总

### 安全设置
- `CONTINUE_WITHOUT_TELEGRAM` - 设置为 `True` 时，即使没有配置 Telegram 也会继续执行爬虫
- 设置为 `False` 时，如果没有 Telegram 配置会停止程序

## 📋 消息格式说明

### Telegram 推送消息包含：
- 📊 热点词汇统计标题
- 🔥/📈/📌 不同热度级别的关键词
- 每个关键词最多显示 5 条相关新闻
- 新闻标题支持点击跳转
- 排名信息（高排名加粗显示）
- 时间范围和出现次数
- 数据获取失败的平台提醒
- 更新时间戳

### 消息特点：
- 支持 Markdown 格式
- 自动处理超长消息（4000字符限制）
- 禁用网页预览避免消息过长
- 支持移动端新闻链接跳转

## 🔍 测试验证

### 手动测试：
1. 在 GitHub Actions 页面手动触发 workflow
2. 查看 Actions 日志确认是否成功发送
3. 检查 Telegram 是否收到推送消息

### 常见问题排查：
- **收不到消息**：检查 Bot Token 和 Chat ID 是否正确
- **权限错误**：确保 Bot 有发送消息权限
- **格式异常**：检查 Markdown 语法是否正确
- **消息过长**：系统会自动截断超长消息

## 📱 使用示例

成功配置后，你将收到类似这样的推送：

```
📊 热点词汇统计 - 当日汇总

🔥 马斯克 特斯拉 : 27 条

  1. 今日头条 [马斯克为何这么快就认怂了](link) [15-26] 00时24分 ~ 07时55分 (15次)
  
  2. 百度热搜 [特朗普回应马斯克道歉：非常好](link) [6-24] 00时24分 ~ 15时54分 (20次)
  
  ... 还有 23 条相关新闻

━━━━━━━━━━━━━━━━━━━

📈 华为 任正非 鸿蒙 HarmonyOS : 16 条

  1. 澎湃新闻 [华为发布Pura 80系列](link) [1-9] 00时24分 ~ 16时58分 (28次)

更新时间：2025-06-12 16:58:54
```

## 🎯 高级功能

### 自定义机器人设置：
- 设置机器人头像和描述
- 添加命令菜单（通过 BotFather）
- 设置欢迎消息

### 群组推送：
- 支持推送到 Telegram 群组
- 可以创建专门的新闻订阅群
- 支持多个 Chat ID（需要修改代码）

现在你已经成功配置了 Telegram Bot 推送功能！🎉 