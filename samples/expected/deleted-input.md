# 样例 deleted-input（声明输入在变更集里被删掉）

- 图：`samples/graphs/deleted-input.json`
- 历史：`samples/history/deleted-input.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/deleted-input.json --history samples/history/deleted-input.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
build/frag.out	rerun	input-missing(src/frag.in)
build/page.out	rerun	dep-rerun(build/frag.out)
# rerun=2 up-to-date=0 dropped=0
```

重跑集合：`build/frag.out`、`build/page.out`

核对要点：

- `build/frag.out` 的声明输入被删除，比内容变化更硬，直接按 `input-missing` 退回。
- `build/page.out` 自己没有文件变化，只能靠依赖传播重跑。
