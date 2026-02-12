# Telegram 多 Bot 协作配置

## 待配置（需要 Bot Token）

```json5
{
  "channels": {
    "telegram": {
      "enabled": true,
      "accounts": {
        "main": {
          "name": "秘书 Bot",
          "botToken": "YOUR-MAIN-BOT-TOKEN"  // 替换为你的 token
        },
        "dev": {
          "name": "开发 Bot",
          "botToken": "YOUR-DEV-BOT-TOKEN"  // 替换为你的 token
        },
        "design": {
          "name": "设计 Bot",
          "botToken": "YOUR-DESIGN-BOT-TOKEN"  // 替换为你的 token
        },
        "ops": {
          "name": "运营 Bot",
          "botToken": "YOUR-OPS-BOT-TOKEN"  // 替换为你的 token
        },
        "research": {
          "name": "研究 Bot",
          "botToken": "YOUR-RESEARCH-BOT-TOKEN"  // 替换为你的 token
        }
      }
    }
  },
  "bindings": [
    { "agentId": "main", "match": { "channel": "telegram", "accountId": "main" } },
    { "agentId": "dev-engineer", "match": { "channel": "telegram", "accountId": "dev" } },
    { "agentId": "designer", "match": { "channel": "telegram", "accountId": "design" } },
    { "agentId": "operator", "match": { "channel": "telegram", "accountId": "ops" } },
    { "agentId": "researcher", "match": { "channel": "telegram", "accountId": "research" } }
  ]
}
```

## 创建 Bot 步骤

1. 打开 @BotFather
2. `/newbot` 创建 5 个 Bot
3. 复制 token 填入上方配置

## 群聊中使用

```
@秘书Bot - 协调任务
@开发Bot - 执行开发
@设计Bot - 执行设计
@运营Bot - 执行运营
@研究Bot - 执行研究
```
