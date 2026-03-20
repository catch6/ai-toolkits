# AI Toolkits

面向 AI Agent 的技能集合，遵循 [Agent Skills](https://agentskills.io/) 格式。

## 技能（Skills）

技能是可跨项目安装的可复用指令集，通过 `npx skills` 安装到目标项目。

### git-commit

按照 Conventional Commits 规范创建 Git 提交。

```sh
npx skills add https://github.com/catch6/ai-toolkits --skill git-commit
```

触发时机："提交改动"、"暂存文件"、"拆分成多个提交"

- 提交前检查工作区状态
- 按逻辑边界自动拆分提交（功能/重构、前端/后端、测试/生产代码）
- 强制使用 `type(scope): 中文描述` 格式
- 防止提交密钥、强制推送和跳过 hook

### translate

自动检测语言并翻译（中文↔英文，其他语言→中文），保留格式、代码和语气风格。

```sh
npx skills add https://github.com/catch6/ai-toolkits --skill translate
```

触发时机："翻译这段文字"、"把这个改成英文"、"translate this"

## 开源协议

MIT
