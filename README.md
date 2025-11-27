# Academic Pages
**Academic Pages 是一个用于个人和专业作品集网站的 GitHub Pages 模板。**

![Academic Pages 模板示例](images/themes/homepage-light.png "Academic Pages 模板示例")

# 快速开始

1. 如果您还没有 GitHub 账户，请注册一个并确认您的电子邮件（必需！）
1. 点击右上角的"使用此模板"按钮。
1. 在"新建仓库"页面，输入您的公共仓库名称为"[您的 GitHub 用户名].github.io"，这也将是您网站的 URL。
1. 设置全站配置并添加您的内容。
1. 将任何文件（如 PDF、.zip 文件等）上传到 `files/` 目录。它们将出现在 https://[您的 GitHub 用户名].github.io/files/example.pdf。
1. 通过进入仓库设置，在"GitHub pages"部分检查状态
1. （可选）使用 `markdown_generator` 文件夹中的 Jupyter notebooks 或 python 脚本从 TSV 文件生成出版物和演讲的 markdown 文件。

更多信息请访问 https://academicpages.github.io/

## 本地运行

当您最初在网站上工作时，在将更改推送到 GitHub 之前能够在本地预览更改是非常有用的。要在本地工作，您需要：

1. 克隆仓库并按照上述说明进行更新。

### 使用不同的 IDE
1. 确保您已安装 ruby-dev、bundler 和 nodejs
    
    在大多数 Linux 发行版和 [Windows Subsystem Linux](https://learn.microsoft.com/en-us/windows/wsl/about) 上，命令是：
    ```bash
    sudo apt install ruby-dev ruby-bundler nodejs
    ```
    如果您看到错误 `Unable to locate package ruby-bundler`、`Unable to locate package nodejs`，请运行以下命令：
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
    然后再次尝试运行 `sudo apt install ruby-dev ruby-bundler nodejs`。

    在 MacOS 上，命令是：
    ```bash
    brew install ruby
    brew install node
    gem install bundler
    ```
1. 运行 `bundle install` 以安装 ruby 依赖项。如果遇到错误，请删除 Gemfile.lock 并重试。

    如果您看到文件权限错误，例如 `Fetching bundler-2.6.3.gem ERROR:  While executing gem (Gem::FilePermissionError) You don't have write permissions for the /var/lib/gems/3.2.0 directory.` 或 `Bundler::PermissionError: There was an error while trying to write to /usr/local/bin.`
    本地安装 Gems（推荐）：
    ```bash
    bundle config set --local path 'vendor/bundle'
    ```
    然后再次尝试运行 `bundle install`。如果成功，您应该看到一个名为 `vendor` 和 `.bundle` 的文件夹。

1. 运行 `jekyll serve -l -H localhost` 以生成 HTML 并从 `localhost:4000` 提供服务，本地服务器将在 Markdown (*.md) 和 HTML 文件更改时自动重建和刷新页面，而对核心模板和配置（即 `_config.yml`）的更改将需要停止并重新启动 Jekyll。
    您也可以尝试 `bundle exec jekyll serve -l -H localhost` 以确保 jekyll 在您自己的本地机器上使用特定的依赖项。

如果您在 Linux 上运行，可能需要在能够本地运行之前安装一些额外的依赖项：`sudo apt install build-essential gcc make`

## 使用 Docker

在不同的操作系统上工作，或者只是想避免安装依赖项？如果您已安装 [Docker](https://www.docker.com/)，可以使用提供的 `Dockerfile` 构建一个容器来为您运行站点。

您可以通过在仓库中运行以下命令来构建和执行容器：

```bash
chmod -R 777 .
docker compose up
```

现在您应该能够从 `localhost:4000` 访问网站。

### 在 VS Code 中使用 DevContainer

如果您使用 [Visual Studio Code](https://code.visualstudio.com/)，可以使用此仓库附带的 [Dev Container](https://code.visualstudio.com/docs/devcontainers/containers)。通常 VS Code 会检测到开发容器配置可用，并询问您是否要使用容器。如果这没有发生，您可以通过 **F1->DevContainer: Reopen in Container** 手动启动容器。这将在容器中重新启动您的 VS Code，并自动在 http://localhost:4000 上本地托管您的学术页面。所有更改将在几秒钟后实时更新到该页面。

# 维护

模板的错误报告和功能请求应[通过 GitHub 提交](https://github.com/academicpages/academicpages.github.io/issues/new/choose)。有关如何设置模板样式的问题，请随时在 [GitHub 上开始新的讨论](https://github.com/academicpages/academicpages.github.io/discussions)。

此仓库由 [Stuart Geiger](https://github.com/staeiou) 从 [Minimal Mistakes Jekyll Theme](https://mmistakes.github.io/minimal-mistakes/) 分叉（然后分离），该主题 © 2016 Michael Rose 并在 MIT 许可证下发布（参见 LICENSE.md）。目前由 [Robert Zupko](https://github.com/rjzupkoii) 维护，欢迎其他维护者加入。

## 错误修复和增强

如果您有想要作为拉取请求提交的错误修复和增强功能，您需要[分叉](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)此仓库，而不是将其用作模板。这也将允许您[同步您的副本](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)模板到您的分叉。

不幸的是，像 Academic Pages 这样的模板主题存在一个后勤问题，这使得将错误修复和更新传递到核心主题变得有点棘手。如果您使用此模板并对其进行自定义，如果您尝试同步，可能会遇到合并冲突。如果您想保存各种 .yml 配置文件和 markdown 文件，可以删除仓库并再次分叉它。或者您可以手动修补。

---
<div align="center">
    
![pages-build-deployment](https://github.com/academicpages/academicpages.github.io/actions/workflows/pages/pages-build-deployment/badge.svg)
[![GitHub contributors](https://img.shields.io/github/contributors/academicpages/academicpages.github.io.svg)](https://github.com/academicpages/academicpages.github.io/graphs/contributors)
[![GitHub release](https://img.shields.io/github/v/release/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/releases/latest)
[![GitHub license](https://img.shields.io/github/license/academicpages/academicpages.github.io?color=blue)](https://github.com/academicpages/academicpages.github.io/blob/master/LICENSE)

[![GitHub stars](https://img.shields.io/github/stars/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io)
[![GitHub forks](https://img.shields.io/github/forks/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/fork)
</div>
