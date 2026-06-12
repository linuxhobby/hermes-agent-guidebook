# Hermes Agent 常用指令速查

> 参考 [tailscale-command.html](https://github.com/community-scripts/ProxmoxVE) 风格制作的单文件查询卡片。**推荐直接使用 HTML 版**（支持实时搜索 + 点击复制）：
>
> - HTML 版：同级或 [ProxmoxVE/hermes-command.html](../ProxmoxVE/hermes-command.html)
> - 直接打开即可在浏览器使用，无需安装。

---

## 推荐 Shell Alias（强烈建议添加到 ~/.zshrc 或 ~/.bashrc）

```bash
alias h='hermes'
alias ht='hermes --tui'
alias hd='hermes doctor --fix'
alias hl='hermes logs -f'
alias hs='hermes sessions browse'
alias hm='hermes model'
alias hsk='hermes skills list'
alias hbk='hermes backup --quick'
```

---

## CLI 命令

### 🚀 启动与对话
| 命令 | 说明 |
|------|------|
| `hermes` | 启动交互式对话（默认恢复最近会话） |
| `hermes -c "任务描述"` | 一次性执行后退出（适合脚本调用） |
| `hermes -z "prompt"` | One-shot 纯净输出（仅最终结果，无 UI） |
| `hermes --tui` | 启动现代 TUI（推荐） |
| `hermes --model xxx` | 临时指定模型 |
| `hermes --yolo` | 跳过所有危险审批（**慎用**） |
| `hermes --fresh` / `--private` | 全新会话 / 隐私模式（不存历史） |
| `hermes --workspace ~/proj` | 指定工作目录作为上下文 |

### 💬 会话管理
- `hermes sessions list` / `browse` —— 列出 / 交互式挑选会话（日常最常用）
- `hermes sessions rename <id> "标题"`
- `hermes sessions export <id> --format md`
- `hermes sessions prune --older-than 30d`

### 🧠 模型管理
- `hermes model` —— 交互式挑选器（最推荐）
- `hermes model list` / `current` / `benchmark` / `pricing`
- `hermes fallback list` / `add`

### 🛠️ 工具与技能
- `hermes skills list` / `search` / `browse` / `install <name>` / `update`
- `hermes tools list` / `enable xxx` / `disable xxx --permanent`
- `hermes bundles list` / `plugins list`

### ⚙️ 配置与设置
- `hermes setup`（改 Key/模型时首选） / `--models-only` / `--keys-only`
- `hermes config show` / `edit` / `set key value`
- `hermes postinstall`

### 🔍 诊断与状态
- `hermes doctor` / `doctor --fix`
- `hermes status` / `--deep`
- `hermes logs -f` / `logs errors --since 2h`
- `hermes debug share` （上传日志给支持）
- `hermes prompt-size`

### 📡 网关 / Cron / 集成
- `hermes gateway status` / `setup` / `start` / `run`
- `hermes cron list` / `create` / `run <name>`
- `hermes portal info`
- `hermes dashboard` （Web UI，默认 9119）
- `hermes kanban ...`

### 🗄️ 备份与维护
- `hermes backup` / `--quick`
- `hermes import ~/xxx.zip`
- `hermes update` / `update --check`
- `hermes claw migrate` （从 OpenClaw 迁移）

### 🧩 高级
- `hermes memory setup` / `status`
- `hermes mcp list` / `add`
- `hermes --worktree` （并行隔离 agent）
- `hermes profile create xxx`
- `hermes insights 7`

---

## 对话内斜杠命令（聊天窗口内直接输入）

**核心必记**：`/help`、`/model`、`/memory`、`/clear`

### Session / 对话控制
- `/help`、` /new` / `/reset`、` /clear`、` /compact [here N]`、` /export`
- `/retry`、` /undo [N]`、` /rollback`
- `/private`、` /yolo`
- `/goal ...`、` /subgoal ...`、` /status`

### 配置与切换
- `/model [name]`（支持 `--global`）
- `/personality xxx`、` /verbose`、` /fast`、` /reasoning`
- `/voice on|off|tts`

### 工具与技能
- `/skills`、` /tools`、` /bundles`、` /cron`、` /curator`、` /kanban`
- `/reload-skills`、` /reload-mcp`

### 信息与维护
- `/version`、` /update`、` /debug`、` /usage`、` /insights`
- `/copy`（复制最后回复）、`/image <path>`
- `/quit [--delete]`

**小技巧**：
- `/system 从现在开始所有回复必须带单元测试`
- `/temp claude-sonnet-4` （仅下一条临时切模型）
- `/compact` + `/memory add 刚才结论是...` 管理长上下文神器

---

## 更多资源

- 完整指南（强烈推荐阅读）：`06-基础使用入门.md` 中的「常用命令速查大全」和「斜杠命令系统」
- 官方文档：https://hermes-agent.nousresearch.com/docs/
- GitHub: https://github.com/NousResearch/hermes-agent
- 本文件配套 HTML 版支持**实时搜索 + 一键复制**，比 Markdown 方便得多。

---

*本参考基于 2026 年 6 月本地安装 (`hermes --help`) + 指南书 + 源码 `hermes_cli/commands.py` 整理，部分子命令随版本演进可能略有差异，建议以 `hermes <cmd> --help` 为准。*