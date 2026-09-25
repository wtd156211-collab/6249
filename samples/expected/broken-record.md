# 样例 broken-record（损坏记录与自相矛盾的键）

- 图：`samples/graphs/broken-record.json`
- 历史：`samples/history/broken-record.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/broken-record.json --history samples/history/broken-record.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
build/badkey.out	rerun	corrupt-record(key)
build/downstream.out	rerun	dep-rerun(build/badkey.out)
build/liar.out	rerun	key-mismatch
build/nooutfp.out	rerun	corrupt-record(outputs)
build/ok.out	up-to-date	-
# rerun=4 up-to-date=1 dropped=0
```

重跑集合：`build/badkey.out`、`build/downstream.out`、`build/liar.out`、`build/nooutfp.out`

核对要点：

- `build/badkey.out` 的键不是合法指纹，`build/nooutfp.out` 缺输出指纹，都按无记录退回。
- `build/liar.out` 的键格式合法，但与它自己的分量对不上，属于记录自相矛盾。
- `build/downstream.out` 三个依赖都不可复用，原因取字典序最小的那个。
