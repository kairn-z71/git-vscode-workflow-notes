# Git / GitHub / VS Code 工作流笔记

这是从 TA Obsidian 笔记库中单独发布的「代码管理」目录，不包含整个 TA 库，也不继承 TA 的旧提交历史。

- [主笔记](Git%20%2B%20Github%20%2B%20Vscode%E7%AE%A1%E7%90%86.md)：核心名词、VS Code / GitHub 图标、双方法操作与实际发布记录。
- Pictures/：笔记引用的 28 张截图。
- .gitignore：本目录的编辑器状态、临时文件和常见凭据文件忽略规则。

## 阅读方式

> [!IMPORTANT]
> **建议使用 Obsidian 打开这份笔记，而不是只在 GitHub 网页中阅读。**
>
> 笔记包含大量照片 / 截图、内部链接和 callout，主要按 Obsidian 的阅读方式整理。GitHub 的 Markdown 渲染与 Obsidian 不完全兼容，可能出现排版异常、原始语法符号（看起来像“乱码”）、内部链接不能跳转，以及正文图片无法显示。
> 这些通常是语法兼容问题，不代表中文编码损坏或图片文件损坏；图片原文件仍可在 [Pictures/](Pictures/) 中单独查看。

| 笔记中的写法 | 在 Obsidian 中 | 在 GitHub 网页中可能出现的情况 |
| --- | --- | --- |
| `[[#章节标题]]` 等内部链接 | 点击跳转到笔记内对应位置 | 显示原始符号，不能按 Obsidian 规则跳转 |
| `![[图片文件名.png]]` 等图片嵌入 | 在正文显示对应图片 | 不能按 Obsidian 的图片查找规则显示截图 |
| `[!question]`、`[!info]`、`[!summary]` 等 callout | 显示提示框、问题框等样式 | 与 GitHub 支持的提示类型和格式不同，部分只能显示为普通引用或原始标记 |

**推荐打开方法：**

1. 克隆整个仓库，或下载 ZIP 后完整解压；**保留主笔记和 `Pictures/` 的目录关系，不要只下载 Markdown 文件**。
2. 在 Obsidian 中选择“打开文件夹作为仓库”，打开这个完整目录；如果已经在原 TA 库中，也可以直接在那里阅读。
3. 打开主笔记，使用阅读视图或实时预览查看图片、内部链接与 callout。

callout 的书写约定是：首行只保留类型标记（以及可选的折叠符号），标题或说明放到下一行正文，不写在标记后面。本仓库没有复制 TA 的 `.obsidian/` 与 `.grimoire/` 配置。

格式参考：[Obsidian 内部链接与嵌入](https://help.obsidian.md/links)、[Obsidian callout](https://help.obsidian.md/callouts)、[GitHub Markdown 与提示框](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts)。

## 版本管理边界

本目录有自己的 Git 仓库，远程为 https://github.com/kairn-z71/git-vscode-workflow-notes.git，默认分支为 main。
原 TA 仓库、其远程及已有历史保持不动。父仓库此前已经跟踪的文件，不会因为新增子仓库就自动停止跟踪；发布此仓库不等于清除 TA 远程原有内容。

在本目录更新后，需选择本目录的仓库完成 Commit / Push，不能把 TA 父仓库的 Push 当作本仓库的同步。
