# IELTS 目录说明

本目录集中管理雅思（IELTS）备考的**计划**与**练习产出**。所有英文写作、口语练习都放这里，
不再单独开 Writing 顶层菜单。

## 文件命名规范

**统一用「`类型-编号-主题.md`」格式（连字符分隔，编号补零到两位）。**

| 类型 | 前缀 | 示例 |
| --- | --- | --- |
| 写作练习 | `writing-` | `writing-01-agent.md`、`writing-02-what-is-an-agent.md` |
| 口语练习 | `speaking-` | `speaking-01-hobbies.md`、`speaking-02-work.md` |
| 听力笔记 | `listening-` | `listening-01-friends.md` |
| 阅读笔记 | `reading-` | `reading-01-news.md` |
| 复盘 / 其它 | `review-` | `review-week1.md` |

**规则要点**：

- **用连字符 `-`，不用下划线 `_`**（URL 更友好）。
- **编号递增、补零两位**（`01`、`02`…），保证按主题排序时顺序稳定。
- 编号是**该类型下的序号**，写作和口语各自从 `01` 开始。
- 文件名全英文小写；标题写在正文的 `# 一级标题` 里（显示标题与文件名解耦）。

## 目录结构与职责

| 文件 | 作用 |
| --- | --- |
| `index.md` | **备考总计划**（Simon × SMART × MECE × Feynman），含 Weekly log |
| `ielts-writing-ai-review.md` | **写作批改**：AI 批改提示词，每篇写完丢给 AI 评分+逐句改 |
| `writing-*.md` | 写作练习成品（英语文章） |
| `speaking-*.md` | 口语练习材料（如 Keith 视频逐字稿 / 自己的回答） |

## 怎么新增一篇练习

1. 按命名规范建文件，例如写作第 3 篇：`docs/ielts/writing-03-<topic>.md`。
2. 正文第一行写 `# 显示标题`。
3. 在 `mkdocs.yml` 的 `IELTS:` 下按**同样缩进**登记一行：`- 显示标题: ielts/文件名.md`。
4. **写作**：按 [`ielts-writing-ai-review.md`](ielts-writing-ai-review.md) 用 AI 批改，再把结果记进 `index.md` 的 Weekly log。

## 与其它菜单的关系

- **Growth Mindset** —— 提供方法论（Simon / SMART / Feynman），本目录**使用**它们。
- **ACP** —— 另一个独立目标，与本目录平级。
- ~~Writing~~ —— **已取消**，英文写作练习全部并入本目录（见上文命名规范）。
