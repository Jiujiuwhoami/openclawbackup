# 工作区结构 - OpenClaw 多 Agent 标准实践

## OpenClaw 架构

```
~/.openclaw/
├── openclaw.json              ← 主配置（bindings, agents.list）
│
├── agents/                     ← Agent 状态目录
│   ├── main/
│   │   ├── agent/            ← main Agent 状态
│   │   │   └── auth-profiles.json
│   │   └── sessions/         ← main Agent 会话
│   │
│   ├── dev-engineer/
│   │   ├── agent/
│   │   └── sessions/
│   │
│   ├── designer/
│   │   ├── agent/
│   │   └── sessions/
│   │
│   └── operator/
│       ├── agent/
│       └── sessions/
│
├── workspace-main/            ← main Agent 工作区
│   ├── SOUL.md              ← 角色定义
│   ├── AGENTS.md            ← 工作规范
│   ├── USER.md              ← 用户信息
│   ├── SECURITY.md          ← 安全规范
│   └── memory/              ← 每日笔记
│
├── workspace-dev/            ← dev-engineer Agent 工作区
│   ├── SOUL.md              ← 角色定义（开发工程师）
│   ├── AGENTS.md            ← 开发规范
│   ├── init.sh              ← 启动脚本
│   ├── feature_list.json    ← 功能清单
│   ├── progress.md          ← 进度追踪
│   └── memory/              ← 开发笔记
│
├── workspace-design/         ← designer Agent 工作区
│   └── SOUL.md
│
└── workspace-ops/           ← operator Agent 工作区
    └── SOUL.md
```

## Agent 职责

| Agent | 工作区 | agentDir | 职责 |
|-------|--------|----------|------|
| main | workspace-main | agents/main/agent | 顶级秘书，协调所有任务 |
| dev-engineer | workspace-dev | agents/dev-engineer/agent | 开发工程师 |
| designer | workspace-design | agents/designer/agent | 设计师 |
| operator | workspace-ops | agents/operator/agent | 运营经理 |

## 路由规则 (bindings)

```json
{
  "bindings": [
    { "agentId": "main", "match": { "channel": "telegram" } }
  ]
}
```

- Telegram 消息 → main Agent
- main Agent → 派发到其他 Agent

## 协作方式

```
老板 → main Agent（我）
           │
           ├── 开发 → dev-engineer Agent
           ├── 设计 → designer Agent
           └── 运营 → operator Agent
```

## 每个 Agent 独立

- **Workspace**: 配置文件（SOUL.md, AGENTS.md）
- **agentDir**: 认证配置（auth-profiles.json）
- **sessions**: 会话历史（独立存储）
