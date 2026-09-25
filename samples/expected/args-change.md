# 样例 args-change（只改参数与工具标识、没有文件变化）

- 图：`samples/graphs/args-change.json`
- 历史：`samples/history/args-change.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/args-change.json --history samples/history/args-change.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
build/app.elf	rerun	args-changed
build/main.o	rerun	tool-changed
# rerun=2 up-to-date=0 dropped=0
```

重跑集合：`build/app.elf`、`build/main.o`

核对要点：

- `build/main.o` 只换了工具标识，参数与输入都没变。
- `build/app.elf` 同时受参数变化与依赖重跑影响，按优先级只报参数变化。
