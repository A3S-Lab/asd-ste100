# 安装 stc-answer

这份说明写给执行安装的 Agent。人也可以按同样的步骤做。

目标：当前 Agent 能读到技能 `stc-answer`，并且 `node <技能目录>/scripts/am.mjs --version` 打印版本号。

## 规则

- 只装一份。已经存在时，更新这一份，不要再装到另一个目录。
- 不要改写用户已有的其他技能。
- Node.js 低于 20 或缺失时停下来，告诉用户。不要自行安装 Node.js。
- 不需要 `npm install`。渲染器在 `scripts/am.mjs`。

## 步骤

1. 运行 `node --version`。版本必须是 v20 或更高。
2. 查找已有安装：

```bash
ls -d ~/.grok/skills/stc-answer ~/.claude/skills/stc-answer ~/.codex/skills/stc-answer ~/.cursor/skills/stc-answer ~/.agents/skills/stc-answer ~/.copilot/skills/stc-answer ~/.gemini/skills/stc-answer ~/.config/opencode/skills/stc-answer 2>/dev/null
```

3. 没有安装时，装到当前 Agent：

```bash
npx skills add A3S-Lab/stc-answer -g -y -a <当前 agent 名>
```

当前 Agent 的名字以 `npx skills add --help` 为准。常见名字：`grok`、`claude-code`、`codex`、`cursor`、`github-copilot`、`gemini-cli`、`opencode`、`cline`。

安装器不认识这个名字时，把仓库里的 `skills/stc-answer` 目录复制到该 Agent 的 skills 目录。Grok 用 `~/.grok/skills/stc-answer`。Claude Code 用 `~/.claude/skills/stc-answer`。Codex 用 `~/.codex/skills/stc-answer`。Cursor 用 `~/.cursor/skills/stc-answer`。

4. 已经安装时，更新：

```bash
npx skills update stc-answer -y
```

5. 检查：

```bash
dir=$(ls -d ~/.grok/skills/stc-answer ~/.claude/skills/stc-answer ~/.codex/skills/stc-answer ~/.cursor/skills/stc-answer ~/.agents/skills/stc-answer ~/.copilot/skills/stc-answer ~/.gemini/skills/stc-answer ~/.config/opencode/skills/stc-answer 2>/dev/null | head -1)
node "$dir/scripts/am.mjs" --version
python3 "$dir/scripts/ste-lint.py" --selftest
python3 "$dir/stc/tools/check.py" --strict "$dir/stc/规范.md" "$dir/stc/examples/after.md"
```

6. 用一则消息报告：装到了哪个目录，版本号，`ste-lint.py --selftest` 是否通过，用户还要做什么。没有后续动作时写「无」。
