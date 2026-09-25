# 样例 multi-output（多输出目标与输出被外部改写的下游）

- 图：`samples/graphs/multi-output.json`
- 历史：`samples/history/multi-output.json`
- 命令：`python3 cache_judge.py --graph samples/graphs/multi-output.json --history samples/history/multi-output.json`

下面代码块就是该命令的标准输出（制表符分隔，逐行可核对）：

```text
docs/index.html	rerun	no-record
gen/page.html	rerun	dep-output-changed(gen/theme.css)
gen/theme.css	up-to-date	-
pkg/bundle	rerun	input-changed(src/pages/b.html)
pkg/site.json	rerun	dep-rerun(pkg/bundle)
# rerun=4 up-to-date=1 dropped=0
```

重跑集合：`docs/index.html`、`gen/page.html`、`pkg/bundle`、`pkg/site.json`

核对要点：

- `pkg/bundle` 是多输出目标：两个输出一起参与它自己的输出集合指纹。
- `gen/theme.css` 的改动手落在它自己的输出文件上，它自身可复用，下游 `gen/page.html` 必须重跑。
- `docs/index.html` 是本轮新增的目标，历史里没有记录。
