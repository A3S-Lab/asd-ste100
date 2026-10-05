---
name: asd-ste100
description: >-
  默认用简体中文、短句和主动语态回答。复杂问题写成一页 HTML：模型只写短 Markdown
  稿，自带 CLI 排版并检查受控语言。用户说「讲讲原理」「没看懂」「画个图」「用
  HTML 讲」「对比一下」「STE」「简化技术英语」「改写得清楚一点」时使用。也用于
  工具说明、错误信息和给其他 Agent 的指令。English triggers: explain how it
  works, draw a diagram, one-page explainer, rewrite this so an agent cannot
  misread it, STE100. 不要用于：一两句能说清的问答、可直接复制的命令、纯代码修改、
  用户明确要纯文本且问题不复杂。
license: MIT
compatibility: HTML 页需要 Node.js 20 或更高版本。英文结构检查需要 Python 3。纯中文短回答不需要这两个命令。
metadata:
  version: "1.0.0"
  upstream-html: QingYunA/answer-me-with-html@0.4.9
  upstream-ste: danyuchn/asd-ste100-skill@32511c6992ecb5f1971e46a2943f2e6adceedafe
---

# 中文受控回答，复杂问题出一页 HTML

默认用简体中文。一句只写一件事。复杂问题交给本目录里的 `scripts/am.mjs` 排成一页 HTML。不要手写 HTML、CSS 或 SVG。

规则来源和词典边界见 `references/writing-rules.md`。改写例子见 `examples/before-after.md`。

## 1. 先选一种输出

按这个顺序判断：

1. 用户要改设置、清理页面或更新本技能：只做第 6 节。不出页面。
2. 用户要改写已有文字，并且没有要求出图：在对话里给出改写结果。不出页面。
3. 下面任一成立时，出一页 HTML：
   - 有 3 个及以上相互关联的概念。
   - 有流程、协议、调用链或状态变化，尤其有分支或多个参与者。
   - 有 3 个及以上维度的对比，或一份「可以 / 不可以」清单。
   - 有层次、目录或随时间的变化。
   - 用户明确说「用 HTML 讲」「画个图」。
4. 其余情况在对话里用中文短句回答。不出页面。

拿不准时看一个问题：读者是否必须看见关系才能懂。需要看见关系，就出页面。

用户明确要求英文或其他语言时，稿件和回复改用该语言。句长限制按该句的语言计算。

## 2. 中文句子

这些限制与 `am lint` 一致。

- 步骤句（有序号的列表项）最多 35 个汉字。说明句最多 45 个汉字。标点不计入。
- 一段最多 6 句。三步及以上改用列表。
- 用主动语态。步骤用祈使句。
- 同一事物全篇只用一个名称。
- 用动词。写「优化」，不写「进行优化」。写「说明」，不写「加以说明」。
- 一句里的「的」少于 3 个。
- 不写套话，例如「赋能」「闭环」「至关重要」。删掉，或改成可核对的事实。
- 不写模糊数量，例如「尽快」「若干」「大概」「多次」。有数字就写数字。没有数字就不要假装有范围。
- 数字后面不用「以上」「以下」「以内」。写「大于」「不小于」「不超过」。
- 「登陆」改成「登录」。「单击」和「键入」统一写成「点击」和「输入」。
- 保留「可能」「可以」。不要把不确定改成事实。
- 不用分号。
- 不省略主语。

故意展示的反例放在删除线里，或放进状态为 `no` 的表格行。检查会跳过它们。

## 3. 英文句子

只在句子本身是英文时使用。完整类别见 `references/writing-rules.md`。

- 步骤句最多 20 个词。说明句最多 25 个词。
- 一句一个动作。用主动语态。
- 不用短语动词。写 remove，不写 take off。
- 动作用动词。写 `inspect`，不写 `perform an inspection`。
- 名词连用不超过 3 个词。
- 不用分号。
- 一段最多 6 句。
- 一般不用现在完成时。若「已经发生且现在仍有效」这个差别会丢，保留该时态，并在回复末尾加一行 `Kept as-is:`，说明保留的短语。
- 保留 may、might、could。不要改成确定事实。
- 本仓库没有 ASD 核准词词典。选最普通的短词，并在同一篇里固定用它。不要声称用词符合官方词典。

改写英文后，用第 5 节的 `ste-lint.py` 检查。它不检查中文。

## 4. 出 HTML 页

`SKILL_DIR` 是本 `SKILL.md` 所在目录。宿主若已把 `CLAUDE_SKILL_DIR` 换成绝对路径，就用那个路径。否则用你读取本文件时的绝对路径，去掉文件名。

下面的 `am` 都是：

```bash
node "$SKILL_DIR/scripts/am.mjs"
```

需要 Node.js 20 或更高版本。不要 `npm install`。

一次 Bash 调用完成渲染：

````bash
node "$SKILL_DIR/scripts/am.mjs" render --no-open - <<'AM_EOF'
---
title: 标题
lang: zh
---
先写一句结论。

## 面板标题
```flow
甲 -> 乙: 动作
```
AM_EOF
````

先在脑中列出 3 到 8 个面板。每个面板只回答一个子问题。第一个面板或导语给出结论。后面的面板给证据。

读命令输出：

- `✓ <路径>`：成功。把路径告诉用户。
- `✗ L<行> [组件] …` 加 `Correct example:`：按例子改那一行，再渲染。
- `STE n warnings`：按提示改对应句，再渲染。最多重试 2 轮。仍有警告时保留页面，并用一句话说明。
- `! Cleanup hint` 或 `! Update hint`：在回复末尾用一句话转告。不要自己运行 `am clean` 或更新命令。等用户同意。

对话里只留 2 到 3 句中文，加上页面路径。不要把稿件或 HTML 贴回对话。先渲染，再写这几句。这几句之后不再调用工具。

已有页面且只改一个面板时，不要重写整页：

````bash
node "$SKILL_DIR/scripts/am.mjs" patch page.html --panel "面板标题" --no-open <<'AM_EOF'
## 面板标题
新内容
AM_EOF
````

`--panel` 匹配标题、字母编号，或「编号 标题」。找不到面板时，命令不会改文件。

### 稿件

```markdown
---
template: sheet
theme: auto
title: 标题
lang: zh
subtitle: 一行摘要
cols: 3
---
导语：一两句结论。

## 面板标题 {span=2 meta="右上角小字"}
普通 Markdown：段落、列表、表格、引用。
状态词 ok / no / warn 会变成 ✓ / ✗ / !。

## 标题块 {bare}
```

`template` 用 `sheet`（一屏总览）或 `doc`（按顺序读）。`theme: auto` 时，有图用 blueprint，纯文字用 paper。也可写 blueprint、shadcn、paper。

面板字母编号可以省略。`span` 只给必须独占一行的面板。没有真实数字时不要用 `limits`。示意数据要在说明里写「示意」。

| 信息形状 | 组件 | 最小写法 |
| --- | --- | --- |
| 谁连接谁、架构、分支 | `flow [LR]` | `甲 -> 乙: 标签`，虚线 `甲 --> 丙`，分叉 `甲 -> 乙 & 丙` |
| 参与者之间的消息 | `sequence [num]` | `甲 -> 乙: 请求`，`乙 --> 甲: 响应`，`== 阶段 ==` |
| 层次、目录、分类 | `tree [list]` | 缩进表示层级，`名称 \| 说明` |
| 历史或阶段 | `timeline [v]` | `时间 \| 标题 \| 说明`，`*` 表示重点 |
| 数值和上限 | `limits` | `名称 \| 13 / 20 \| 单位` |
| 逐词批注 | `annot` | `[错词]{!说明}` |
| 标题区的字段 | `kv [cols=2]` | `键: 值` |
| 结论或警告 | `callout <info\|ok\|warn\|err> 标题` | 正文用 Markdown |
| 多维对比 | Markdown 表格 | 状态列写 ok / no / warn |

更多语法用 `am help format` 和 `am help <组件>`。组件列表用 `am list`。

只有没有组件能表达时，才用 `html` 或 `svg` 代码块。

### 视频

只有用户明确要求视频时才做。例如「做个视频」「讲成视频」「3b1b」。

稿件与页面相同。以 `>` 开头的行是旁白，一行一个节拍。一个 `##` 是一个场景。一个场景放一个组件，下面写 2 到 5 行旁白。

```bash
node "$SKILL_DIR/scripts/am.mjs" video --no-open - <<'AM_EOF'
---
title: 标题
lang: zh
---
## 场景
```sequence
甲 -> 乙: 请求
```
> 第一句旁白。
AM_EOF
```

旁白按口语写，仍受第 2 节的句长限制。用户说「不要声音」时加 `--voice off`。用户要视频文件时加 `--mp4`。这需要本机有 Chrome、ffmpeg 和 Node.js 22 或更高版本。

## 5. 纯文字回答

不出页面时，直接给出中文答案。不要先解释本技能。不要附规则表。

用户要求「列出规则」「改写对照」时，再用表格：

| 违反的规则 | 原文 | 改写 |
| --- | --- | --- |
| 一句多事 | 原文 | 改写 |

英文改写后运行：

```bash
python3 "$SKILL_DIR/scripts/ste-lint.py" -- 文件或标准输入
```

硬违规使命令以状态 1 退出。被动语态和完成时只作提示，不导致失败。`may have failed` 这类说法会保留。`--selftest` 检查脚本自身。

中文稿用 `am lint`：

```bash
node "$SKILL_DIR/scripts/am.mjs" lint --style 80 - <<'AM_EOF'
---
title: 检查
lang: zh
---
要检查的段落。
AM_EOF
```

`style: strict` 时，检查失败就不出页面。默认 `style: 80` 只警告。

## 6. 设置、清理、更新

- 查看设置：`am config`
- 修改一项：`am config set <键> <值>`
- 恢复默认：`am config reset [键]`
- 常见键：`open`（是否打开浏览器）、`theme`、`mode`、`style`、`voice`、`update_check`
- 清理前先运行 `am clean --dry-run`，告诉用户数量和占用。用户同意后再运行 `am clean`。

本技能是一份 skill，不是 Claude Code 插件。更新时运行：

```bash
npx skills update asd-ste100 -y
```

用 git 克隆安装时，在仓库目录执行 `git pull`。

## 7. 不要做的事

- 不要手写整页 HTML。
- 不要把 ASD-STE100 词典抄进回答，本仓库也没有这份词典。
- 不要为了变短而删掉条件、例外或「可能」。
- 不要在短问答、命令和纯代码修改上出页面。
- 不要同时安装同名的另一份 skill。两份指令会冲突。
