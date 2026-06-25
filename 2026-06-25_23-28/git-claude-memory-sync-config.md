---
name: git-claude-memory-sync-config
description: Complete configuration details for Claude Code memory auto-sync to GitHub
metadata: 
  node_type: memory
  type: project
  originSessionId: 50e525f7-ba3e-4a3a-a2dd-cef5e3d2bccc
---

# Claude Code 记忆 → GitHub 自动同步配置

## 架构
```
Claude 写入 memory/*.md
  → PostToolUse Hook (Write 匹配)
    → sync-memory.ps1 (PowerShell)
      → git pull → 创建时间戳文件夹 → git push
      → 清理 >7 天旧文件夹
```

## 关键信息
- GitHub 用户名: 123-qw-er
- GitHub 仓库: ahh
- 仓库地址: https://github.com/123-qw-er/ahh
- 认证方式: GITHUB_PAT 用户环境变量 + HTTPS
- Git 全局用户名: 123-qw-er
- Git 全局邮箱: 123-qw-er@users.noreply.github.com

## 文件清单
| 文件 | 路径 | 作用 |
|------|------|------|
| 同步脚本 | ~/.claude/scripts/sync-memory.ps1 | 核心同步逻辑 |
| 本地仓库 | ~/.claude/github-memory-sync/ | GitHub 仓库本地克隆 |
| Hook 配置 | ~/.claude/settings.json | PostToolUse 钩子 |

## 维护
- 更换 PAT: 运行 `setx GITHUB_PAT "ghp_新token"`
- 更改仓库: 编辑脚本中的 `$GithubUser` 和 `$GithubRepo`
- 手动运行: `powershell -ExecutionPolicy Bypass -File ~/.claude/scripts/sync-memory.ps1`
