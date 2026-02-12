# 安全规范 - 敏感信息保护

## 核心原则

**永远不要**在对话中发送以下信息：

| 类型 | 示例 |
|------|------|
| 🔑 API Keys | `ghp_xxx`、`sk-xxx` |
| 🔐 Tokens | `eyJhIjoi...`、Cloudflare tunnel token |
| 🌐 服务器 IP | `45.207.211.19`、`localhost:8080` |
| 🔑 私钥/密码 | `.pem`、`.key` 文件内容 |
| 🔒 认证凭证 | cookies、session token |

---

## 正确做法

### 使用占位符
```bash
# ❌ 错误
curl -H "Authorization: Bearer ghp_xxx"

# ✅ 正确
curl -H "Authorization: Bearer $GITHUB_TOKEN"
# 或
curl -H "Authorization: Bearer <YOUR_API_KEY>"
```

### 使用环境变量
```bash
# 在 /root/.bashrc 或系统变量中设置
export G4F_API_KEY="你的key"
export GITHUB_TOKEN="你的token"
```

### 参考文档
- 配置参考：`TOOLS.md`
- 敏感信息存储：系统环境变量

---

## 发送前检查

### 快速检查清单

- [ ] 没有 `ghp_`、`sk-`、`eyJh` 开头的字符串
- [ ] 没有 IP 地址格式（`x.x.x.x`）
- [ ] 没有完整 URL 包含真实凭证
- [ ] 没有 `.pem`、`.key` 文件内容
- [ ] 使用 `$VAR_NAME` 或 `<PLACEHOLDER>` 代替真实值

---

## 遇到敏感信息请求时

当用户要求发送敏感信息：

1. **提醒**：这是敏感信息，不建议发送
2. **建议**：使用环境变量或占位符
3. **拒绝**：明确表示不会发送任何密钥、密码、Token

---

## 敏感信息存储位置

| 信息 | 存储位置 |
|------|----------|
| API Keys | 系统环境变量 |
| SSH 配置 | `/root/.ssh/` (权限 600) |
| 配置文件 | `.env` 文件（不提交到 Git） |
| 证书文件 | `/root/.cloudflared/` |

---

## 定期检查

- [ ] 定期检查 memory 文件是否有敏感信息
- [ ] 检查 Git 历史是否包含敏感信息
- [ ] 确认环境变量已正确设置

## Agent 协作安全

### 启用的 Agent
| Agent | 工作区 | 用途 |
|-------|--------|------|
| main | /root/.openclaw/workspace | 顶级秘书，协调所有任务 |
| dev-engineer | /root/.openclaw/workspace-dev | 开发工程师，遵循 Anthropic 框架 |

### agentToAgent 配置
- **状态**: 已启用
- **允许**: ["main", "dev-engineer"]
- **用途**: 派发开发任务

### 工作方式
```
老板 → main Agent → dev-engineer Agent → Claude Code 执行
           ↓
      汇报结果给老板
```

---

**记住：安全无小事，敏感信息一旦泄露无法撤回。**
