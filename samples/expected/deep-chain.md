# 样例 deep-chain（深链，链首输入被改写）

- 图：`samples/graphs/deep-chain.json`
- 历史：`samples/history/deep-chain.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/deep-chain.json --history samples/history/deep-chain.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
build/stage-01.out	rerun	input-changed(src/seed.txt)
build/stage-02.out	rerun	dep-rerun(build/stage-01.out)
build/stage-03.out	rerun	dep-rerun(build/stage-02.out)
build/stage-04.out	rerun	dep-rerun(build/stage-03.out)
build/stage-05.out	rerun	dep-rerun(build/stage-04.out)
build/stage-06.out	rerun	dep-rerun(build/stage-05.out)
build/stage-07.out	rerun	dep-rerun(build/stage-06.out)
build/stage-08.out	rerun	dep-rerun(build/stage-07.out)
build/stage-09.out	rerun	dep-rerun(build/stage-08.out)
build/stage-10.out	rerun	dep-rerun(build/stage-09.out)
build/stage-11.out	rerun	dep-rerun(build/stage-10.out)
build/stage-12.out	rerun	dep-rerun(build/stage-11.out)
# rerun=12 up-to-date=0 dropped=0
```

重跑集合：`build/stage-01.out`、`build/stage-02.out`、`build/stage-03.out`、`build/stage-04.out`、`build/stage-05.out`、`build/stage-06.out`、`build/stage-07.out`、`build/stage-08.out`、`build/stage-09.out`、`build/stage-10.out`、`build/stage-11.out`、`build/stage-12.out`

核对要点：

- 链首只看自己的输入，链上其余目标没有声明输入，只能靠依赖传播判定。
- 12 层逐层传播：第 2 层起的原因都是 `dep-rerun(上一层)`，同一轮里每个目标只判定一次。
