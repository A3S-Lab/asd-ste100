# 改写例子

这些例子说明规则。它们不是 ASD-STE100 的原文。

## 中文说明

改写前的反例放在代码块里。检查会跳过代码块。

```text
我们对插件系统进行了全面的梳理，并赋能了连接器与技能的闭环，这一点至关重要，能够帮助用户尽快理解整体架构。
```

问题：轻动词「进行了梳理」。套话「赋能」「闭环」「至关重要」。模糊数量「尽快」。一句里塞了三件事。

改写后：

> 插件有两种。商店页只改内存里的安装状态。连接器和技能会写到本机，并在下一次会话交给 Agent。

## 中文步骤

改写前：

```text
用户可以在安装之后通过壳层把目录同步下来并在失败时重试。
```

改写后：

1. 调用安装接口。
2. 读取操作系统里的安装记录。
3. 把记录写到本机。
4. 写入失败时，返回 HTTP 502。

## 英文工具说明

改写前：

```text
This tool will attempt to synchronize state across the various backends that have been configured, and if a conflict is detected it may resolve it automatically depending on the strategy that has been set.
```

改写后：

> The tool tries to synchronize state across the configured backends. If it finds a conflict, it reads the configured strategy. The tool may resolve the conflict without a user.

最后一句保留 may。原文没有承诺一定成功。
