# asd-ste100

给主流 coding agent 用的一份技能。中文用简明技术中文（STC）。这是 ASD-STE100 的中文替代规范：40 条编号规则，约 170 条受控词，以及一个检查脚本。它不是 ASD-STE100 的译本，与 ASD 没有关系。

问题需要看见关系才能懂时，Agent 只写一份短 Markdown 稿，自带命令把它排成一页 HTML。

| 来源 | 用了什么 | 许可 |
| --- | --- | --- |
| [mzopedia/simplified-technical-chinese](https://github.com/mzopedia/simplified-technical-chinese) 0.2 | 中文规范、词表、`stc/tools/check.py` | 文本 CC BY 4.0，脚本 MIT |
| [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill) | 英文结构规则，以及 `scripts/ste-lint.py` | MIT |
| [QingYunA/answer-me-with-html](https://github.com/QingYunA/answer-me-with-html) 0.4.9 | 单页 HTML 渲染器 `scripts/am.mjs` | MIT |

ASD-STE100 的正文和约 900 词词典不在本仓库。官方文本向 [asd-ste100.org](https://www.asd-ste100.org/STE_downloads.html) 申请。详情见 [NOTICE](NOTICE)。

## 安装

需要 Node.js 20 或更高版本。渲染器已经打进 `scripts/am.mjs`，不需要 `npm install`。

一条命令装到本机已识别的全部 agent：

```bash
npx skills add A3S-Lab/asd-ste100 -g -y --all
```

只装当前这个 agent 时，把 `--all` 换成它的名字，例如 `-a grok`、`-a claude-code`、`-a codex`、`-a cursor`。安装器是 [vercel-labs/skills](https://github.com/vercel-labs/skills)。

手动安装时，把 `skills/asd-ste100` 整个目录复制到该 agent 的 skills 目录。常见位置：

| Agent | 全局目录 |
| --- | --- |
| Claude Code | `~/.claude/skills/asd-ste100` |
| Codex | `~/.codex/skills/asd-ste100` |
| Cursor | `~/.cursor/skills/asd-ste100` |
| GitHub Copilot | `~/.copilot/skills/asd-ste100` |
| Gemini CLI | `~/.gemini/skills/asd-ste100` |
| Grok | `~/.grok/skills/asd-ste100` |
| OpenCode | `~/.config/opencode/skills/asd-ste100` |
| Cline 等读取 `.agents/skills` 的 agent | `~/.agents/skills/asd-ste100` |

项目内安装去掉 `-g`。各 agent 的项目目录以 `npx skills add --help` 为准。

不要把同名 skill 装两遍。两份指令会一起加载。

给 Agent 的安装步骤在 [INSTALL.md](INSTALL.md)。

## 你会得到什么

| 你说 | Agent 做的事 |
| --- | --- |
| 讲讲 TCP 三次握手 | 写中文短稿，生成一页 HTML |
| 把这段说明改清楚 | 按简明技术中文改写，不出页面 |
| 用英文改写这条工具说明 | 按英文结构规则改写，并用 `ste-lint.py` 检查 |
| `ls` 怎么看隐藏文件 | 一两句中文，不出页面 |

技能正文在 [skills/asd-ste100/SKILL.md](skills/asd-ste100/SKILL.md)。

## 本地检查

```bash
node skills/asd-ste100/scripts/am.mjs --version
python3 skills/asd-ste100/scripts/ste-lint.py --selftest
python3 skills/asd-ste100/stc/tools/check.py --strict skills/asd-ste100/stc/规范.md skills/asd-ste100/stc/examples/after.md
```

## English

<!-- stc:off -->
One Agent Skills package. Chinese text uses Simplified Technical Chinese (STC). STC has its own rules and word list. It is not a translation of ASD-STE100. A complex answer becomes one HTML page through the bundled `am` renderer. `scripts/ste-lint.py` checks English structure. Install with `npx skills add A3S-Lab/asd-ste100 -g -y --all`. This repository does not include the ASD-STE100 dictionary.
<!-- stc:on -->
