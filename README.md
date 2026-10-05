# stc-answer

stc-answer 是一份 agent 技能。它约束中文的用词和句长。关系复杂时，读者得到一页 HTML。

```bash
npx skills add A3S-Lab/stc-answer -g -y --all
```

需要 Node.js 20 或更高版本。渲染器在技能目录里。不必 `npm install`。

## 回答路径

| 从 | 到 | 动作 |
| --- | --- | --- |
| 用户 | agent | 提问 |
| agent | 检查脚本 | 提交中文稿 |
| 检查脚本 | 渲染器 | 必须项为 0 |
| 渲染器 | 读者 | 一页 HTML |

短事实不走这条路径。agent 直接在对话里写中文短句。

## 三份来源

| 部分 | 管什么 | 来源 |
| --- | --- | --- |
| 中文规则 | 用词和句长 | 简明技术中文 0.2 |
| 英文句子 | 句长和语态 | `ste-lint.py` |
| 页面 | 把稿排成 HTML | `am.mjs` 0.4.9 |

中文规则在 [`stc/规范.md`](skills/stc-answer/stc/规范.md)。词表在 [`stc/词表.md`](skills/stc-answer/stc/词表.md)。检查脚本是 [`stc/tools/check.py`](skills/stc-answer/stc/tools/check.py)。

| 来源 | 许可 |
| --- | --- |
| [mzopedia/simplified-technical-chinese](https://github.com/mzopedia/simplified-technical-chinese) 0.2 | 文本 CC BY 4.0，脚本 MIT |
| [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill) | MIT |
| [QingYunA/answer-me-with-html](https://github.com/QingYunA/answer-me-with-html) 0.4.9 | MIT |

许可细节在 [NOTICE](NOTICE)。

## 两路输出

| 条件 | 输出 |
| --- | --- |
| 一两句能说清 | 对话中的中文短句 |
| 必须看见关系 | 一页 HTML |
| 只改写已有文字 | 对话中的改写结果 |
| 句子本身是英文 | 通过结构检查的英文 |

技能怎么判断，写在 [`SKILL.md`](skills/stc-answer/SKILL.md)。

## 边界

它不是 ASD-STE100 的译本。仓库不含 ASD 词典。它与 ASD 没有关系。

官方英文文本向 [asd-ste100.org](https://www.asd-ste100.org/STE_downloads.html) 申请。

技能名是 `stc-answer`。仓库地址也是 `stc-answer`。

## 安装

1. 运行下面的安装命令。
2. 新开一个 agent 会话。

只装 Grok 时，把 `--all` 换成 `-a grok`。装好后，Grok 的目录是 `~/.grok/skills/stc-answer`。

其他 agent 的步骤在 [INSTALL.md](INSTALL.md)。

## 本地检查

```bash
node skills/stc-answer/scripts/am.mjs --version
python3 skills/stc-answer/scripts/ste-lint.py --selftest
python3 skills/stc-answer/stc/tools/check.py --strict skills/stc-answer/stc/规范.md skills/stc-answer/stc/examples/after.md
```

## English

<!-- stc:off -->

stc-answer is an agent skill. It limits Chinese wording and sentence length. A complex answer becomes one HTML page.

```bash
npx skills add A3S-Lab/stc-answer -g -y --all
```

HTML pages need Node.js 20 or newer. This repository omits the ASD-STE100 dictionary.

<!-- stc:on -->
