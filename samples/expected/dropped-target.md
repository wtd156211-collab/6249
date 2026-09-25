# 样例 dropped-target（目标被删掉，历史还有记录、当前图里没有）

- 图：`samples/graphs/dropped-target.json`
- 历史：`samples/history/dropped-target.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/dropped-target.json --history samples/history/dropped-target.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
build/a.out	up-to-date	-
build/b.out	up-to-date	-
legacy/old.out	dropped	not-in-graph
# rerun=0 up-to-date=2 dropped=1
```

重跑集合：（空）

核对要点：

- `legacy/old.out` 只存在于历史记录，判定为 `dropped`，不进重跑集合，原因列固定写 `not-in-graph`。
- 剩下两个目标各项一致，仍可复用。
