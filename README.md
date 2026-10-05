# stc-answer

让 coding agent 用简明技术中文写说明。关系必须看见才能懂时，回答是一页 HTML。

```bash
npx skills add A3S-Lab/stc-answer -g -y --all
```

需要 Node.js 20 或更高版本。渲染器已经在技能目录里，不必 `npm install`。

仓库名是 `stc-answer`。装入 agent 后的目录名是 `asd-ste100`。

## 为什么用它

一句里有多件事时，读者会读错。同一个概念有多个词时，读者也会读错。简明技术中文限制句长和用词。本仓库把这套规则交给 coding agent。

## 改写前后

改写前：

```text
用户首先需要登陆到目标服务器，然后切换到 /opt 目录并且创建一个用于存放采集器配置文件以及运行时产生的临时数据的工作目录。
```

改写后：

1. 登录目标服务器。
2. 切换到 `/opt` 目录。
3. 创建工作目录 `/opt/collector`。工作目录存放配置文件和临时数据。

全文在 [`skills/asd-ste100/stc/examples/`](skills/asd-ste100/stc/examples/)。

## 你说什么，Agent 做什么

| 你说 | Agent 做的事 |
| --- | --- |
| 讲讲 TCP 三次握手 | 写中文短稿，生成一页 HTML |
| 把这段说明改清楚 | 按简明技术中文改写，不出页面 |
| 用英文改写这条工具说明 | 按英文结构规则改写，并用 `ste-lint.py` 检查 |
| `ls` 怎么看隐藏文件 | 一两句中文，不出页面 |

技能怎么判断，写在 [`skills/asd-ste100/SKILL.md`](skills/asd-ste100/SKILL.md)。

## 边界

- 中文遵循简明技术中文 0.2。操作句不超过 30 字。描述句不超过 40 字。规范在 [`stc/规范.md`](skills/asd-ste100/stc/规范.md)。
- 英文只检查句子结构。脚本是 [`scripts/ste-lint.py`](skills/asd-ste100/scripts/ste-lint.py)。本仓库没有 ASD-STE100 词典。
- 不用于营销文案、法律原文和代码本身。

简明技术中文按中文重写了规则。它不是 ASD-STE100 的译本，与 ASD 没有关系。官方英文文本向 [asd-ste100.org](https://www.asd-ste100.org/STE_downloads.html) 申请。

## 只装一个 agent

```bash
npx skills add A3S-Lab/stc-answer -g -y -a grok
```

把 `grok` 换成 `claude-code`、`codex` 或 `cursor`。安装器是 [vercel-labs/skills](https://github.com/vercel-labs/skills)。

装进当前项目时，去掉 `-g`。同一技能只装一份。两份指令会同时生效。

给执行安装的 Agent 的步骤在 [INSTALL.md](INSTALL.md)。

## 手动复制

把 `skills/asd-ste100` 复制到下表的目录。

| Agent | 全局目录 |
| --- | --- |
| Claude Code | `~/.claude/skills/asd-ste100` |
| Codex | `~/.codex/skills/asd-ste100` |
| Cursor | `~/.cursor/skills/asd-ste100` |
| GitHub Copilot | `~/.copilot/skills/asd-ste100` |
| Gemini CLI | `~/.gemini/skills/asd-ste100` |
| Grok | `~/.grok/skills/asd-ste100` |
| OpenCode | `~/.config/opencode/skills/asd-ste100` |
| 读取 `.agents/skills` 的 agent | `~/.agents/skills/asd-ste100` |

各 agent 的项目目录以 `npx skills add --help` 为准。

## 来源

| 来源 | 用了什么 | 许可 |
| --- | --- | --- |
| [mzopedia/simplified-technical-chinese](https://github.com/mzopedia/simplified-technical-chinese) 0.2 | 中文规范、词表、`stc/tools/check.py` | 文本 CC BY 4.0，脚本 MIT |
| [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill) | 英文结构规则，以及 `scripts/ste-lint.py` | MIT |
| [QingYunA/answer-me-with-html](https://github.com/QingYunA/answer-me-with-html) 0.4.9 | 单页 HTML 渲染器 `scripts/am.mjs` | MIT |

许可细节在 [NOTICE](NOTICE)。

## 本地检查

```bash
node skills/asd-ste100/scripts/am.mjs --version
python3 skills/asd-ste100/scripts/ste-lint.py --selftest
python3 skills/asd-ste100/stc/tools/check.py --strict skills/asd-ste100/stc/规范.md skills/asd-ste100/stc/examples/after.md
```

## English

<!-- stc:off -->

stc-answer is an agent skill. It writes Simplified Technical Chinese. A complex answer becomes one HTML page.

```bash
npx skills add A3S-Lab/stc-answer -g -y --all
```

HTML pages need Node.js 20 or newer. The skill directory is `skills/asd-ste100`. This repository omits the ASD-STE100 dictionary.

<!-- stc:on -->
