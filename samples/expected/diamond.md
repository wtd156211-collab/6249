# 样例 diamond（菱形依赖，一侧重跑、一侧复用、汇合点传播）

- 图：`samples/graphs/diamond.json`
- 历史：`samples/history/diamond.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/diamond.json --history samples/history/diamond.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
app/final.bin	rerun	dep-rerun(build/left.b)
build/core.a	up-to-date	-
build/left.b	rerun	input-changed(src/left.c)
build/right.c	up-to-date	-
# rerun=2 up-to-date=2 dropped=0
```

重跑集合：`app/final.bin`、`build/left.b`

核对要点：

- `build/core.a` 与 `build/right.c` 的记录与当前状态逐项一致，判定可复用。
- `app/final.bin` 只报告一次，原因取字典序最小的重跑依赖。
