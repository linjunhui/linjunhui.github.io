# 怎么记笔记、怎么发布

## 写在哪儿

所有内容都放在 `docs/` 目录下：

| 位置 | 用途 |
| --- | --- |
| `docs/index.md` | 站点首页 |
| `docs/notes/` | 笔记正文，一篇一个 `.md` |
| `docs/guide/` | 使用说明类文档（就是这个页面） |
| `docs/assets/` | 图片等静态资源 |

## 写一篇新笔记

```bash
# 1. 新建文件
docs/notes/我的新笔记.md
```

2. 打开根目录的 `mkdocs.yml`，在 `nav:` 的「笔记」分组下面加一行：

```yaml
nav:
  - 笔记:
      - 笔记目录: notes/index.md
      - 我的新笔记: notes/我的新笔记.md   # ← 加这行
```

3. 本地看效果：

```bash
python -m mkdocs serve
```

浏览器打开 http://127.0.0.1:8000/ ，改一个字页面会自动刷新。

## 发布

```bash
git add .
git commit -m "add 我的新笔记"
git push
```

推上去之后，GitHub Actions 会自动构建并部署。大约 1～2 分钟后刷新线上地址就能看到。
进度可以在仓库的 **Actions** 标签页看。

!!! tip "不用手动 build"
    线上构建是在 GitHub 的服务器上跑的，你本地不需要执行 `mkdocs build`，
    也不需要把 `site/` 目录提交上去（它已经在 `.gitignore` 里了）。

## Markdown 语法速查

### 文字

**加粗**、*斜体*、`行内代码`、~~删除线~~、==高亮==

### 提示块

```markdown
!!! note "标题"
    这是提示内容，注意缩进四个空格。

!!! warning "小心"
    这是警告内容。
```

!!! warning "缩进很重要"
    提示块里的内容必须相对 `!!!` 缩进 4 个空格，否则不会被识别。

### 代码块

````markdown
```python
def hello():
    print("hello")
```
````

### 表格与任务列表

| 列 A | 列 B |
| --- | --- |
| 内容 | 内容 |

- [x] 已完成的事
- [ ] 还没做的事

### 折叠块

```markdown
??? note "点我展开"
    藏起来的内容。
```

??? note "点我展开"
    藏起来的内容，默认是收起的。
