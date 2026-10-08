# 林俊晖的笔记

Markdown 笔记站，线上地址：<https://linjunhui.github.io/>

技术栈：**MkDocs + Material for MkDocs**，托管在 GitHub Pages，
由 GitHub Actions 自动构建发布。

- **仓库**：`linjunhui/linjunhui.github.io`（用户站点仓库，所以线上是根域名）
- **部署分支**：`master`（默认分支就是它，别改成 main）
- **本地工作区**：`D:/LinJunhui-Pages`

---

## 一、部署是怎么工作的

整个链路只有一步，其余全自动：

```
你写 .md  →  git push 到 master  →  GitHub Actions 构建  →  自动发布
                                    (.github/workflows/deploy.yml)   ↓
                                                        约 1 分钟后线上更新
```

### 关键设置（已经配好，但必须知道）

仓库的 **Settings → Pages → Build and deployment → Source** 必须是
**`GitHub Actions`**，当前已是。

> ⚠️ **如果有人把它改回 `Deploy from a branch`**，GitHub 会用 Jekyll
> 重新构建仓库，把 MkDocs 站点整个覆盖掉（症状见下文「故障排查」）。
> 遇到这种情况，去那个下拉框切回 `GitHub Actions` 即可。

### 手动触发一次发布（不改内容）

```bash
git commit --allow-empty -m "chore: 触发重新构建"
git push
```

发布进度在仓库的 **Actions** 标签页可以看到。

---

## 二、新增一篇文章

### 方式 A：在本地（推荐）

**1. 新建文件**

在 `docs/notes/` 下新建 `.md`，文件名建议用英文或拼音（避免路径问题）：

```bash
docs/notes/my-first-note.md
```

**2. 在导航里登记**

打开 `mkdocs.yml`，找到 `nav:`，在「笔记」分类下加一行：

```yaml
nav:
  - 首页: index.md
  - 笔记:
      - 笔记目录: notes/index.md
      - 第一篇笔记: notes/hello.md
      - 我的第一篇: notes/my-first-note.md   # ← 新增这行
```

**格式规则**：`- 显示标题: 文件路径`，路径相对 `docs/`，**可以不带 `.md` 后缀**。

**3. 发布**

```bash
git add . && git commit -m "add 我的第一篇" && git push
```

### 方式 B：直接在 GitHub 网页上（适合随手改）

1. 打开仓库 → **Add file → Create new file**，路径填 `docs/notes/xxx.md`
2. 写完内容，填提交信息，点 **Commit changes**
3. **别忘了 nav**：再到 `mkdocs.yml` 里点铅笔图标编辑，加上导航那一行，
   否则文章不在侧边导航里（但直接访问 URL 仍能看到）

---

## 三、缩进规则（最容易踩的坑）

`nav` 是 YAML，**子项必须比父级多缩进 2 个空格**。层级结构长这样：

```yaml
nav:
  - 首页: index.md
  - 笔记:                        # ← 2 空格
      - 笔记目录: notes/index.md  # ← 6 空格
      - 第一篇笔记: notes/hello.md
  - 成长思维:                     # ← 2 空格
      - 笔记列表: growth-mindset/index.md
```

**错误示范**（这样写会被当成两个平级条目，导航不显示层级）：

```yaml
  - 成长思维:
    - 笔记列表: growth-mindset/index.md    # ❌ 只有 4 空格，和父级对齐了
```

**第二条铁律**：`nav` 里引用的文件必须真实存在。
写了导航但没建文件，`mkdocs build` 会直接报错，线上就不会更新。
错误信息长这样：

```
WARNING - A reference to 'xxx/index.md' is included in the 'nav'
          configuration, which is not found in the documentation files.
```

---

## 四、新增一个分类

以「读书笔记」为例，两步：

**1. 建目录和索引页**

```bash
mkdir docs/reading
```

创建 `docs/reading/index.md`：

```markdown
# 读书笔记

按主题分类，新的往上加。

## 全部笔记

| 日期 | 标题 | 标签 |
| --- | --- | --- |
| — | 暂无 | — |
```

**2. 在 `mkdocs.yml` 的 `nav` 里登记**

```yaml
  - 读书笔记:
      - 笔记目录: reading/index.md
```

之后这个分类下的文章都放 `docs/reading/`，往 nav 里这个分类下加行即可。

---

## 五、本地预览

改完想先看看效果再发布，就起本地服务：

```bash
"C:/Users/Administrator/.workbuddy/binaries/python/envs/default/Scripts/python.exe" -m mkdocs serve
```

打开 <http://127.0.0.1:8000/>，保存文件浏览器**自动刷新**。
确认没问题再 `git push`。

> 换台机器首次运行，先装依赖。**必须走 https 镜像**（本机全局配的
> `http://mirrors.aliyun.com` 走 80 端口，会被沙箱拦截）：
>
> ```bash
> pip install -r requirements.txt \
>   --index-url https://mirrors.aliyun.com/pypi/simple/ \
>   --trusted-host mirrors.aliyun.com
> ```

---

## 六、目录结构

```
LinJunhui-Pages/
├─ docs/                          ← 所有内容都写在这里
│  ├─ index.md                    ← 站点首页
│  ├─ guide/index.md              ← 使用说明
│  ├─ notes/                      ← 笔记分类一
│  │  ├─ index.md                 ← 该分类的目录页
│  │  └─ hello.md
│  └─ growth-mindset/             ← 笔记分类二
│     └─ index.md
├─ mkdocs.yml                     ← 站点配置，导航在这里登记
├─ requirements.txt               ← 依赖清单
└─ .github/workflows/deploy.yml   ← 自动发布流水线
```

**提交信息约定**：中文，格式 `add: xxx`（新文章）/ `fix: xxx` / `chore: xxx`。

---

## 七、故障排查

**Q：推上去了，但线上没更新 / 变得不对劲？**

按顺序检查：

1. **看构建有没有跑**：仓库 → Actions 标签页，看最新那条是不是绿的。
   - 没有 run → 检查推送的分支是不是 `master`（推到别的分支不会触发）
   - 红色失败 → 点进去看日志，最常见原因是 nav 引用了不存在的文件
2. **构建成功但页面不对**：打开站点 `右键 → 查看网页源代码`，搜 `generator`：
   - `mkdocs-1.6.1, ...` → 正常，是我们的站
   - `Jekyll v3.10.0` → **Pages 的 Source 被改回分支模式了**，
     去 `Settings → Pages` 切回 `GitHub Actions`，然后推个空提交触发重建
3. **本地验证**：跑 `mkdocs build`，看有没有 WARNING，修复后再推

**Q：想找替换前的旧内容？**

旧内容（academicpages 学术主页模板）完整保存在远端分支 `legacy-academicpages`：

```bash
git fetch && git checkout legacy-academicpages
```

---

## 八、千万别动的几处配置

| 位置 | 原因 |
| --- | --- |
| `mkdocs.yml` 里 `toc` 的 `slugify` 配置 | 默认行为会把中文标题的锚点打成 `id="_1"`，删了目录跳转和 `#锚点` 链接全废 |
| `.github/workflows/deploy.yml` 的 `branches: [master]` | 改了分支名，推送就不会触发构建 |
| 仓库 `Settings → Pages → Source` | 保持 **GitHub Actions**，改回分支模式会被 Jekyll 覆盖 |
| `site/` 目录 | 构建产物，已在 `.gitignore`，不要提交，也不要手动改 |

---

## 九、Markdown 语法速查

Material 主题支持的常用写法（更多见 `docs/guide/index.md`）：

```markdown
!!! note "提示块"
    内容相对 !!! 缩进 4 个空格。

??? note "默认折叠的块"
    点标题才展开。

==高亮文字==  ~~删除线~~  **加粗**  *斜体*  `行内代码`

- [x] 任务列表（已完成）
- [ ] 任务列表（未完成）
```
