# 林俊晖的笔记

Markdown 笔记站 —— 线上地址 <https://linjunhui.github.io/>

## 这是什么

一个纯 Markdown 的笔记站，用 MkDocs + Material 构建。
你只负责在 `docs/` 下写 `.md`，推送到 GitHub 后由 Actions 自动构建发布，
不需要手动打包，也不需要提交构建产物。

- **仓库**：`linjunhui/linjunhui.github.io`（用户站点，所以线上是根域名）
- **部署**：push 到 `master` → GitHub Actions 构建 → 发布

## 本地预览

```bash
"C:/Users/Administrator/.workbuddy/binaries/python/envs/default/Scripts/python.exe" -m mkdocs serve
```

打开 <http://127.0.0.1:8000/>，改一个字浏览器会自动刷新。

> 换台机器首次运行，先装依赖。注意**必须走 https 镜像**，
> 本机全局配的 `http://mirrors.aliyun.com`（80 端口）会被沙箱拦截：
>
> ```bash
> pip install -r requirements.txt \
>   --index-url https://mirrors.aliyun.com/pypi/simple/ \
>   --trusted-host mirrors.aliyun.com
> ```

## 目录结构

```
LinJunhui-Pages/
├─ docs/                        ← 你的笔记都写在这里
│  ├─ index.md                  ← 首页
│  ├─ guide/index.md            ← 使用说明
│  └─ notes/                    ← 笔记正文
├─ mkdocs.yml                   ← 站点配置（导航在这里改）
├─ requirements.txt             ← 依赖
└─ .github/workflows/deploy.yml ← 自动发布流水线
```

## 写一篇新笔记

1. 在 `docs/notes/` 下新建 `我的笔记.md`
2. 打开 `mkdocs.yml`，在 `nav:` 的「笔记」下面加一行：

   ```yaml
   - 我的笔记: notes/我的笔记.md
   ```

3. 提交并推送：

   ```bash
   git add . && git commit -m "add 我的笔记" && git push
   ```

推上去大概一分钟，<https://linjunhui.github.io/> 就更新好了。

## 三个别碰的坑

1. **`mkdocs.yml` 里 `toc` 的 `slugify` 配置千万别删。** MkDocs 默认会把中文标题
   打成空串，生成 `id="_1"`、`id="_2"`，导致目录跳转和 `#锚点` 链接全废。
2. **不要提交 `site/` 目录。** 它已在 `.gitignore` 里，构建交给 GitHub 那台机器。
3. **别把 `master` 退回 `main`。** 远端默认分支是 `master`，
   workflow 的触发分支也是 `master`，改名会导致推送后不构建。

## 历史备份

仓库里有个 `legacy-academicpages` 分支，保存着替换前的旧内容
（academicpages 学术主页模板，commit `8fe4efb`）。想找回来看：

```bash
git checkout legacy-academicpages
```
