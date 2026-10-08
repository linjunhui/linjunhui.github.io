# 林俊晖的笔记

用 Markdown 写，自动发布到 GitHub Pages。

## 这是什么

一个纯 Markdown 的笔记站。你只负责在 `docs/` 目录下写 `.md` 文件，
推送到 GitHub 后由 Actions 自动构建、自动发布，不需要手动做任何打包。

## 快速开始

```bash
# 本地预览（改一个字，浏览器立刻刷新）
mkdocs serve

# 本地构建到 site/ 目录
mkdocs build
```

## 目录结构

```
LinJunhui-Pages/
├─ docs/                  ← 你的笔记都写在这里
│  ├─ index.md            ← 首页
│  ├─ guide/index.md      ← 使用说明
│  └─ notes/              ← 笔记正文
├─ mkdocs.yml             ← 站点配置（导航在这里改）
├─ requirements.txt       ← 依赖
└─ .github/workflows/     ← 自动发布的流水线
```

## 写一篇新笔记

1. 在 `docs/notes/` 下新建 `我的笔记.md`
2. 打开 `mkdocs.yml`，在 `nav:` 里的「笔记」下面加一行：

   ```yaml
   - 我的笔记: notes/我的笔记.md
   ```

3. `git add . && git commit -m "add 我的笔记" && git push`

推上去之后大概一分钟，线上就更新好了。
