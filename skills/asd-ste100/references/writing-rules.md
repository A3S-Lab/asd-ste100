# 受控写法：规则来源

本文件说明规则从哪来。操作时以 `SKILL.md` 里的句长和步骤为准。

本仓库不收录 ASD-STE100 正文，也不收录它约 900 个核准词的词典。需要核准英文用词时，向官方申请 Issue 9（2025 年 1 月）：<https://www.asd-ste100.org/STE_downloads.html>。

## 中文优先

默认用简体中文。用户明确要求其他语言时，改用该语言。

中文句子的机器检查在 `scripts/am.mjs` 里。它按字符数限制句长，并提示轻动词、套话和连续的「的」。这些中文词表来自 Answer me with HTML，并指向 [Simplified Technical Chinese](https://github.com/mzopedia/simplified-technical-chinese)。它们不是 ASD 词典。

`scripts/ste-lint.py` 只检查英文的结构。它不认识中文词表。

## 英文结构规则

ASD-STE100 是欧洲航空航天与防务工业协会（ASD）维护的受控英语。现行版本是 Issue 9。公开资料把它概括为 9 个部分、53 条写作规则，外加一份一词一义的词典。下面只转述规则类别，不引用标准原文。

- 一个词只承担一个意思，也只做一种词类。
- 动作用动词。不写 `perform an inspection`。写 `inspect`。
- 不用短语动词。短语动词的意思不能从两个词相加得到。
- 步骤用主动语态，一句只写一个动作。
- 步骤句最多 20 个英文词。说明句最多 25 个英文词。
- 不省略主语、动词或冠词。
- 名词连用不超过 3 个词。
- 不用分号。
- 一段一个主题，最多 6 句。三步及以上改用列表。
- 允许的动词形式：不定式、祈使、一般现在、一般过去、一般将来，以及只作形容词的过去分词。
- 一般不用现在完成时。若「已经发生且现在仍有效」这个差别会丢，就保留，并说明原因。
- 「may」「可以」「可能」表示把握程度。不要改成确定事实。

## 为什么给 Agent 用

STE 原先给不能回头提问的维修人员。另一个 Agent、翻译流程或非母语读者也没有机会追问。短句和固定名称减少误读。

## 来源

- <https://www.asd-ste100.org/>
- <https://www.asd-ste100.org/about_STE.html>
- <https://en.wikipedia.org/wiki/Simplified_Technical_English>
- <https://github.com/danyuchn/asd-ste100-skill>
- <https://github.com/QingYunA/answer-me-with-html>
- <https://github.com/mzopedia/simplified-technical-chinese>
