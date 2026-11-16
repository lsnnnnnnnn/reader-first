# 中英文编辑示例

以下是为说明编辑决策而编写的例子，不是论文引文，也不是实际测试结果。只在原文或上下文已经提供关系时，按这些方式展开。

目录：名词关系；结论范围；依存关系；从句标记；拟人与操作；条件和量词；术语与被动句；歧义；工作状态；文学表达。

## 1. 展开名词之间的关系

原文：
> 我新增了三个并发写入场景下的缓存失效回归测试，本地全部通过；线上高负载情况下的可靠性尚未验证。

改写：
> 我新增了三个回归测试，检查并发写入时缓存能否按预期失效。三个测试在本地都通过了；线上高负载下是否可靠，还没有验证。

保留测试数量、测试条件、本地结果和未验证范围。这里的“失效”是缓存机制的术语，不应误改成缓存发生故障。

## 2. 把限制放在所限制的结论旁边

原文：
> 这项仅覆盖 Linux 环境、尚未在 Windows 上运行的修复验证结果表明路径中的空格问题已解决。

改写：
> 在 Linux 上，验证结果表明这项修复解决了路径包含空格时的问题。Windows 上的结果还没有验证。

保留 Linux 范围。不要删掉后半句后泛称“问题已解决”。

## 3. 缩短依存关系

原文：
> The patch the reviewer who joined the team last week approved changes the retry limit.

改写：
> The reviewer who joined the team last week approved this patch. The patch changes the retry limit.

让 patch 与 changes 直接相接。重复 patch 比换成可能指向 reviewer 的代词更清楚。

## 4. 只在有帮助时补从句标记

原文：
> I reviewed the tests the maintainer added, but I have not run them.

可选改写：
> I reviewed the tests that the maintainer added, but I have not run them.

两句都可以使用。补 that 能提示结构，但原句并不因为省略它而错误。保留 reviewed 与 have not run 的区别。

## 5. 用实际行为替换不必要的拟人

原文：
> The handler eats the exception by returning `None` without logging it, which may hide the failed write from callers.

改写：
> The handler returns `None` without logging the exception. Callers may therefore miss the failed write.

保留 `None` 和 may。不要新增成功状态、数据丢失或调用者一定无法发现错误等原文没有说明的事实。

## 6. 保留条件、量词和因果强度

原文：
> 只有在重试次数超过三次且备用服务可用时，客户端才会切换服务；这可能降低部分请求的失败率，但实验尚不能证明因果关系。

这段已经清楚，可以保留。只要求返回修改后文本时，直接返回原文，不加评语。不要把“超过三次”改成“三次或以上”，不要把“且”改成“或”，不要把“可能”改成“会”。

## 7. 保留熟悉的技术术语与合适的被动句

原文，面向熟悉系统开发的读者：
> The garbage collector scans the heap. Three samples were excluded because their timestamps were missing.

保留这两句。如果任务没有提供排除样本的执行者，就不要为了改成主动句而编造 we。garbage collector 是稳定术语，不需要拆成解释性的长短语。面向新读者时，只在需要理解机制的地方补一个简短定义。

## 8. 不为消除歧义而补写事实

原文：
> 已补充请求超时重试回退覆盖。

没有上下文时，不要擅自展开为“重试失败后切换到备用服务”，也不要声称已经运行测试。可保守改为：
> 已补充与请求超时、重试和回退有关的覆盖。

如果读者必须知道确切内容才能使用这段话，提出一个具体问题，例如：“这里是补充了测试，还是新增了程序处理逻辑？”先完成其他不受歧义影响的部分。

## 9. 把工作状态写清楚

原文：
> 输入边界修复已完成；两个用于检查旧版兼容性的新增测试本地通过，完整测试集尚未运行。

改写：
> 输入边界问题已修复。检查旧版兼容性的两个新增测试在本地都通过了；完整测试集还没有运行。

保留修复内容、两个测试的目的、本地结果和未运行的完整测试集。原文没有说明执行者或具体改动方式，因此不补写“我”或“修改了代码”。不要将这个结果概括成“旧版兼容性已全面验证”。

## 10. 保留文体所需要的语言

原文：
> 夜色吞下了最后一班车的灯光，她这才转身。

用户在写小说时，保留“夜色吞下”。它服务于意象，并没有妨碍跟上事件。只有用户需要字面说明或明确要求去掉拟人时才改写。不要从“无生命主语”指标推出文学写作禁令。
