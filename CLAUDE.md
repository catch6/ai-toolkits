# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

面向 AI Agent 的技能（Skills）集合，遵循 [Agent Skills](https://agentskills.io/) 格式，通过 `npx skills` CLI 安装到 AI 开发环境中。

## 架构

所有技能位于 `skills/<name>/SKILL.md`，可通过以下命令安装：

```sh
npx skills add https://github.com/catch6/ai-toolkits --skill <name>
```

## Skill 文件格式

```markdown
---
name: skill-name
description: 'Use when ...'
---

skill content
```

- `description` 用于 AI 匹配触发条件，应简洁描述使用时机
- 技能正文使用**英文**
- 动态上下文通过 `!` 前缀注入（如 !`git status`）
- 用户输入通过 `$ARGUMENTS` 占位符接收
