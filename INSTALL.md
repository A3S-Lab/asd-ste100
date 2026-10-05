# 安装 asd-ste100

这份说明写给执行安装的 Agent。人也可以按同样的步骤做。

目标：当前 Agent 能读到技能 `asd-ste100`，并且 `node <技能目录>/scripts/am.mjs --version` 打印版本号。

## 规则

- 只装一份。已经存在时，更新这一份，不要再装到另一个目录。
- 不要改写用户已有的其他技能。
- Node.js 低于 20 或缺失时停下来，告诉用户。不要自行安装 Node.js。
- 不需要 `npm install`。渲染器在 `scripts/am.mjs`。

## 步骤

1. 运行 `node --version`。版本必须是 v20 或更高。
2. 查找已有安装：

```bash
ls -d ~/.grok/skills/asd-ste100 ~/.claude/skills/asd-ste100 ~/.codex/skills/asd-ste100 ~/.cursor/skills/asd-ste100 ~/.agents/skills/asd-ste100 ~/.copilot/skills/asd-ste100 ~/.gemini/skills/asd-ste100 ~/.config/opencode/skills/asd-ste100 2>/dev/null
```

3. 没有安装时，装到当前 Agent：

```bash
npx skills add A3S-Lab/asd-ste100 -g -y -a <当前 agent 名>
```

当前 Agent 的名字以 `npx skills add --help` 为准。常见名字：`grok`、`claude-code`、`codex`、`cursor`、`github-copilot`、`gemini-cli`、`opencode`、`cline`。

安装器不认识这个名字时，把仓库里的 `skills/asd-ste100` 目录复制到该 Agent 的 skills 目录。Grok 用 `~/.grok/skills/asd-ste100`。Claude Code 用 `~/.claude/skills/asd-ste100`。Codex 用 `~/.codex/skills/asd-ste100`。Cursor 用 `~/.cursor/skills/asd-ste100`。

4. 已经安装时，更新：

```bash
npx skills update asd-ste100 -y
```

5. 检查：

```bash
dir=$(ls -d ~/.grok/skills/asd-ste100 ~/.claude/skills/asd-ste100 ~/.codex/skills/asd-ste100 ~/.cursor/skills/asd-ste100 ~/.agents/skills/asd-ste100 ~/.copilot/skills/asd-ste100 ~/.gemini/skills/asd-ste100 ~/.config/opencode/skills/asd-ste100 2>/dev/null | head -1)
node "$dir/scripts/am.mjs" --version
python3 "$dir/scripts/ste-lint.py" --selftest
```

6. 用一则消息报告：装到了哪个目录，版本号，`ste-lint.py --selftest` 是否通过，用户还要做什么。没有后续动作时写「无」。
