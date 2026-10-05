# 受控写法：规则来源

中文和英文用两套规范。操作步骤以 `SKILL.md` 为准。本文件只说明来源。

## 中文：简明技术中文

中文替代品是简明技术中文（Simplified Technical Chinese，STC）0.2。作者是 mzopedia。它不是 ASD-STE100 的译本，与 ASD 没有关系。

本技能收录的副本：

- `stc/规范.md`：6 节，40 条。操作句不超过 30 字。描述句不超过 40 字。
- `stc/词表.md`：禁用词、选词、一词一义。约 170 条。
- `stc/tools/check.py`：零依赖检查脚本。
- `stc/docs/校准报告.md`：句长阈值的校准说明。

文本许可是 CC BY 4.0。脚本许可是 MIT。上游是 <https://github.com/mzopedia/simplified-technical-chinese>，提交 `90ad0f004b26d7a66e286980b5efaf4769ad8584`。

`scripts/am.mjs` 里还有一份更短的中文提示。那些提示不代替 STC。中文以 `stc/tools/check.py` 为准。

## 英文：ASD-STE100 的结构规则

本仓库不收录 ASD-STE100 正文，也不收录它约 900 个核准词的词典。需要核准英文用词时，向官方申请 Issue 9（2025 年 1 月）：<https://www.asd-ste100.org/STE_downloads.html>。

`scripts/ste-lint.py` 只检查英文的结构。它不检查中文，也不对照 ASD 词典。

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
