# Git / GitHub / VS Code 工作流笔记

这是从 TA Obsidian 笔记库中单独发布的「代码管理」目录，不包含整个 TA 库，也不继承 TA 的旧提交历史。

- [主笔记](Git%20%2B%20Github%20%2B%20Vscode%E7%AE%A1%E7%90%86.md)：核心名词、VS Code / GitHub 图标、双方法操作与实际发布记录。
- Pictures/：笔记引用的 28 张截图。
- .gitignore：本目录的编辑器状态、临时文件和常见凭据文件忽略规则。

## 阅读方式

主笔记使用 Obsidian 的内部链接、图片嵌入和 callout。GitHub 网页不一定原生渲染这些 Obsidian 专用语法；要完整阅读，使用 Obsidian 打开克隆后的目录或在原 TA 库中阅读。此仓库没有复制 TA 的 .obsidian/ 与 .grimoire/ 配置。

## 版本管理边界

本目录有自己的 Git 仓库，远程为 https://github.com/kairn-z71/git-vscode-workflow-notes.git，默认分支为 main。
原 TA 仓库、其远程及已有历史保持不动。父仓库此前已经跟踪的文件，不会因为新增子仓库就自动停止跟踪；发布此仓库不等于清除 TA 远程原有内容。

在本目录更新后，需选择本目录的仓库完成 Commit / Push，不能把 TA 父仓库的 Push 当作本仓库的同步。
