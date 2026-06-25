---
name: github-sync-setup
description: Claude Code GitHub sync configuration for memory persistence
metadata: 
  node_type: memory
  type: project
  originSessionId: 50e525f7-ba3e-4a3a-a2dd-cef5e3d2bccc
---

# GitHub 记忆同步配置

## 设置信息
- GitHub 用户名: 123-qw-er
- 仓库: ahh
- 同步方式: PowerShell 脚本 + Claude Code PostToolUse Hook
- 存储格式: 按时间戳文件夹 (yyyy-MM-dd_HH-mm) 每次同步一份完整快照
- 自动清理: 超过 7 天的文件夹自动删除

## 文件位置
- 同步脚本: `~/.claude/scripts/sync-memory.ps1`
- 本地缓存: `~/.claude/github-memory-sync/`
- Hook 配置: `~/.claude/settings.json` → PostToolUse

## 工作原理
1. Claude 写入/编辑 memory/*.md → 触发 PostToolUse Hook
2. 脚本检查变更（60秒防抖）
3. git pull → 创建时间戳文件夹 → 复制记忆 → git push
4. 扫描并删除 >7 天的旧文件夹
