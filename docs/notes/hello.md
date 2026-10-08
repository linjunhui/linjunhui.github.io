# 第一篇笔记

> 2026-10-08 · 示例

这篇是拿来当模板用的，可以直接复制改名成你自己的笔记。

## 为什么用 Markdown

因为它就是纯文本 —— 十年后还能打开，不挑软件，git diff 也看得懂。
写完推上去，GitHub Pages 负责渲染成网页。

## 一段代码

```python
from pathlib import Path

notes = sorted(Path("docs/notes").glob("*.md"))
for i, note in enumerate(notes, 1):
    print(f"{i:02d}. {note.stem}")
```

## 一个表格

| 方案 | 构建 | 适合 |
| --- | --- | --- |
| MkDocs Material | Actions | 笔记、文档 |
| docsify | 无 | 想极简 |

## 待办

- [x] 搭好站点骨架
- [ ] 把仓库推到 GitHub
- [ ] 打开 Pages 开关
- [ ] 写更多笔记

---

想写自己的第一篇了？新建 `docs/notes/你的标题.md`，
再到 `mkdocs.yml` 的 `nav` 里加一行就完事。
