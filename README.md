# Outlook邮件API服务

基于FastAPI + aioimaplib的高性能异步邮件管理服务，支持OAuth2认证和高并发访问。

## 快速部署

### 1. 安装依赖
```bash
pip install -r requirements.txt
```

### 2. 启动服务
```bash
python main.py
```

服务将在 `http://localhost:8000` 启动，访问 `http://localhost:8000/docs` 查看交互式API文档。

## API使用指南

### 1. 注册邮箱账户
```bash
curl -X POST "http://localhost:8000/accounts" \
     -H "Content-Type: application/json" \
     -d '{
       "email": "your_email@outlook.com",
       "refresh_token": "your_refresh_token",
       "client_id": "your_client_id"
     }'
```

### 2. 获取邮件列表
```bash
# 获取所有邮件（收件箱+垃圾箱）
curl "http://localhost:8000/emails/your_email@outlook.com?folder=all&page=1&page_size=100"

# 只获取收件箱邮件
curl "http://localhost:8000/emails/your_email@outlook.com?folder=inbox"

# 只获取垃圾箱邮件
curl "http://localhost:8000/emails/your_email@outlook.com?folder=junk"
```

### 3. 获取邮件详情
```bash
curl "http://localhost:8000/emails/your_email@outlook.com/INBOX-12345"
```

## 特性

- ✅ **极简部署**: 单文件架构，无额外配置
- ✅ **高性能**: 基于FastAPI + aioimaplib异步处理
- ✅ **OAuth2认证**: 支持微软现代认证
- ✅ **智能分页**: 默认100封邮件/页，支持自定义
- ✅ **多文件夹支持**: 收件箱、垃圾箱、整合视图
- ✅ **健壮性**: 完善的错误处理和日志记录

## 数据存储

用户凭证自动保存在 `accounts.json` 文件中，首次注册后后续调用无需重复提供凭证。 