# Git + GitHub + VS Code 管理代码


> [!info]
> **阅读约定**
>
> 说明性表格主要采用“图标 / 名词｜含义｜大白话”；教程资源表与对比表按用途命名列。“含义”列用于技术说明，“大白话”列保留原有个人表述，不因排版整理而改写。

> [!tip]
> **学习阶梯与阅读顺序：先图形，后命令**
>
> 数字越小越早学，不代表后面的内容不重要。综合章节看子节标记；这是本文的阅读建议，不是行业认证标准。
>
> - **L1 · 新手先学**：先查第 2 节基础名词 → 第 3 节认 VS Code 图标 → 第 4 节认 GitHub 页面 → 第 5～6 节完成首次建仓与日常图形流程。不要先把所有进阶名词背完。
> - **L2 · 日常熟练**：会用按钮以后，用第 3.3 节图标 / 命令对照表建立联系，再看第 8 节终端准备、日常命令与模拟实录；第 7 节 GitLens 是可选工具。
> - **L3 · 团队协作**：第 9 节按场景先看“方法 A：VS Code / GitHub”，再学“方法 B：命令行”，重点是分支、PR、同步、冲突与团队规则。
> - **L4 · 进阶按需**：日常与协作熟练后，再练提交整理、已发布历史改写、移植修复、Reflog 与 Bisect。没有完整 GUI 的部分会明确说明，不虚构按钮。
>
> **安全底线不分等级：**所有人先看 [[#10.1 忽略规则配置与敏感信息|敏感信息]] 与 [[#10.3 高风险操作的底线|高风险操作底线]]；每次提交前对照 [[#11.1 提交前检查|检查清单]]。两种方法通常二选一，练习双方法时重新准备初始状态。

> [!tip]
> **阅读导航**
>
> [[#1. 官方教程|1 教程]] · [[#2. 核心名词，不懂的概念看这里|2 核心名词]] · [[#3. VS Code 图标与菜单速查|3 VS Code 图标]] · [[#4. GitHub 网页图标与菜单速查|4 GitHub 界面]] · [[#5. 首次配置与创建仓库：先用 VS Code|5 首次配置]] · [[#6. VS Code 日常操作流程|6 图形日常流程]] · [[#7. GitLens 插件（可选）|7 GitLens]] · [[#8. 日常命令行与 PowerShell 实录|8 日常命令行]] · [[#9. 团队协作：先界面，后命令|9 团队协作]] · [[#10. 忽略规则与安全边界|10 忽略与安全]] · [[#11. 检查清单与双方法验收|11 验收]]
> [[#12. 实操记录：只把「代码管理」目录发布到 GitHub|12 本次真实发布记录]]

## 1. 官方教程

学习阶梯：**L1 · 新手先学**

| 教程 / 资源                                                                                          | 内容                               | 学习建议                                                                                     |
| ------------------------------------------------------------------------------------------------ | -------------------------------- | ---------------------------------------------------------------------------------------- |
| [GitHub Skills：Introduction to GitHub](https://github.com/skills/introduction-to-github)         | GitHub 官方动手练习：创建分支、提交文件、打开并合并 PR | 最先做一遍，练习仓库与真实项目分开；官方预计不到一小时                                                              |
| [Pro Git 第二版·简体中文](https://github.com/progit/progit2-zh)                                         | 系统讲解 Git 原理和使用方法                 | 作为长期参考书；可从 [Git 官网中文版](https://git-scm.com/book/zh/v2) 阅读                                |
| [Learn Git Branching](https://github.com/pcottle/learnGitBranching)                              | 用交互式提交图学习分支和 Git 命令              | 在 [在线练习站](https://learngitbranching.js.org/?locale=zh_CN) 观察 commit、merge、rebase 怎样改变提交图 |
| [Git Flight Rules·中文](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md) | 按“遇到什么问题”查找解决方法                  | 出错时查阅；涉及重置、清理、改写历史的命令不要直接照抄                                                              |
| [GitLens 源码与 README](https://github.com/gitkraken/vscode-gitlens)                                | 扩展功能、使用入口、Community 与 Pro 的说明    | 配合本文第 7 节学习，不必先开通付费功能                                                                    |

**建议学习路线：** 先做 GitHub Skills → 按第 5～6 节完成一次 VS Code 提交和推送 → 用 Learn Git Branching 理解分支 → 需要时查 Pro Git 和 Flight Rules。这是本文的学习安排，不是教程官方要求。

VS Code 操作细节以微软的 [源代码管理总览](https://code.visualstudio.com/docs/sourcecontrol/overview) 和 [首次提交教程](https://code.visualstudio.com/docs/sourcecontrol/quickstart) 为准，避免用老教程猜测新界面。

## 2. 核心名词，不懂的概念看这里

学习阶梯：**L1–L4 · 分层查阅，以子节标记为准**

> [!note]
> 本节集中解释整篇笔记出现的关键名词。后面的配置、日常流程和团队实操通过内部链接回到这里，不再在流程中插入长篇概念说明。


### 2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff

学习阶梯：**L1 · 新手先学**

- **Save（保存）**：把编辑器内容写入磁盘，不会生成提交。
- **Stage（暂存）**：选出这次**即将**Commit的内容；暂存后继续编辑的部分，要再次暂存才会进入本次Commit。
- **Commit（提交）**：把暂存 记入 本地历史，不等于上传到Github，只是作为一个历史版本。
- **Push（推送）**：把本地提交发送到远程（Github等）。
- **Pull（拉取）**：把 远程仓库（Github） 的 新提交（别人的） 下载到本地，并合并到当前分支。
- **Change / Diff （改动）**：相比于以前的版本，做出的代码改动。

- 个人理解：（王者荣耀版本）
	1. Commit一次，就是一次王者服务器的本地更新；Stage是属于Commit下的，Stage相当于这次更新的每一处小改动，可以微调。
	2. Push一次，就是一次正式的大规模赛季更新。推送到每个玩家的手机上（Github等远程分支上）

#### 2.1.1 Publish Branch 和 Push 的区别

学习阶梯：**L1 · 新手先学**

**Publish Branch = 第一次把“这个本地分支”发布到远程**
**Push = 这个分支已经发布到Github一次了，后续继续上传新的 commit**

依据：[Git Add](https://git-scm.com/docs/git-add)、[Git Commit](https://git-scm.com/docs/git-commit)、[Pro Git：记录更新](https://git-scm.com/book/zh/v2/Git-基础-记录每次更新到仓库)。

### 2.2 工作区、暂存区与本地仓库

学习阶梯：**L1 · 新手先学**

```
工作树 Working Tree
↓ git add
暂存区 Staging Area / Index
↓ git commit
本地仓库 Local Repository
↓ git push
GitHub 远程仓库
```

`working tree` 你可以直接理解成：**工作区**

> [!note]
> **你电脑上当前正在编辑的那份项目文件。**
>
> 也就是 VS Code 里打开的那些文件。

`Staging Area / Index` 就是存changes的地方。

`Local Repository` 可以粗略理解为：项目里的 `.git` 目录。


### 2.3 仓库、分支与远程名词

学习阶梯：**L1 · 新手先学**

| 名词                  | 含义                                                        | 大白话                                   |
| ------------------- | --------------------------------------------------------- | ------------------------------------- |
| `Repository / Repo` | 仓库：保存 项目内容 及 版本历史                                         | 整个 Git 项目                             |
| `Branch`            | 分支：指向某个提交的可移动引用                                           | 项目的一条版本路线                             |
| `main`              | 常见的主分支名称                                                  | 默认的名称，**可以改名**                        |
| `origin`            | 远程仓库的常用别名                                                 | 远程仓库的默认名称，就是GitHub仓库，**也可以改名**        |
| `origin/main`       | 本地的**远程跟踪引用**（很常见的描述）<br>**记录最新，最后一次commit获取的远程 main 位置** | Github的main分支<br>也可以指这个main分支的最尾部（最新） |
| `HEAD`              | 你当前的位置                                                    | 你现在站在哪条分支的哪个版本上                       |
| `upstream`          | 默认对接对象<br>比如本地的 main分支 默认 Push 的时候，会上传到 origin/main分支 里   | 说白了就是Github上对应的分支                     |
| `Pull Request / PR` | 请求把一个分支合并进另一个分支                                           | 两个分支要合二为一了                            |

例图👇

![[各种分支.png]]


#### 2.3.1 Pull Request：分支合并的请求

学习阶梯：**L3 · 团队协作**

- 假如说ai-polished 要 merge 合并到 main 一个分支了：
	`Pull Request = ai-polished 新增的改动 + main 新增的改动` 得到合并后的 `main`

**如果说，两个分支对同一个地方做出了改动呢？**

- VS Code 会让你手动选：
	1. Accept Current Change 保留当前分支 （HEAD的位置）
	2. Accept Incoming Change 保留要合进来的那个分支
	3. Accept Both Changes 两个都保留

**怎么看哪个是当前分支，哪个是要合进来的呢？**

- 两个方法：
	1. 点分支UI（左下角和Graph里的都可以），看**HEAD**的hash和哪一个分支的一样
	2. Graph 里 看这个球 `◎` ，球在哪个分支，就是当前分支


概念参考：[分支与工作树](https://code.visualstudio.com/docs/sourcecontrol/branches-worktrees)、[仓库与远程](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes)、[GitHub 官方入门练习](https://github.com/skills/introduction-to-github)。


### 2.4 .git：本地仓库的管理数据

学习阶梯：**L2 · 日常熟练**

**原有个人理解（比喻；技术边界见下文）：**

`git init`只是创建了一个 `.git` **隐藏**文件夹，我们在目录里看不到。
	`.git` 相当于一个保险库，暗中保存着一套 最新完整的文件。
	而我们在Vscode里面的工作区看到的呢，是我们可以在目录里看到的，是明着的一套 最新完整的文件。

- 所以说，Git其实分为**明一套暗一套**的。
	我们平时常见的是，明暗两套的文件是一模一样，同步的。
	但是，我们在Vscode的Graph里面看到的，就是`.git`里的整个历史版本。历史版本路线不分明暗

- 但是我们Fetch了之后，就不一样了：
	1. 它会把Github里的那一套 最新完整的文件 和 整个历史版本放到我们本地的`.git`隐藏文件夹里面。
	2. 但是我们在Vscode里面还是能看到我们原来的那些东西。

参考：[Git Init](https://git-scm.com/docs/git-init)。

#### 2.4.1 .git 与项目文件的关系

学习阶梯：**L1 · 新手先学**

下面是一个已经准备了 README、源码和忽略规则的项目示意，不是说这些文件都由 `git init` 自动创建：

```text
my-project/
├─ .git/          ← Git 的管理数据，通常隐藏
├─ .gitignore     ← 忽略规则文件，不是 .git 文件夹
├─ README.md      ← 项目文件
└─ src/           ← 项目源码
```

#### 2.4.2 .git 内部保存什么？

学习阶梯：**L4 · 进阶按需**

```
.git/
├── index        ← 暂存区
├── HEAD         ← 当前在哪个分支
├── refs/        ← 分支、标签引用
├── objects/     ← commit、文件快照等真正的数据
└── ...
```

| 文件                 | 含义                           | 大白话                             |
| ------------------ | ---------------------------- | ------------------------------- |
| `.git/`            | 保存 Git 仓库的管理数据与对象            | Git 的“保险库”和账本，不是拿来日常写代码的地方      |
| `.gitignore`       | 指定应忽略的未跟踪文件模式；不会让已跟踪文件自动退出历史 | 哪些新文件先别纳入版本管理，由这份规则说清楚          |
| `.git/index`       | 记录暂存区的路径、内容引用等信息             | 下一次 Commit 准备交哪些内容的清单（index工作区） |
| `.git/HEAD`        | 通常指向当前分支，也可能直接指向某个提交         | 记住“我现在站在哪个位置”                   |
| `.git/refs/` 等引用记录 | 记录分支、标签等引用的位置；部分引用可能以其他形式存储  | 记住各条版本路线走到了哪里                   |
| `.git/objects/`    | 存储已写入 Git 的内容、目录树、提交等对象      | Git 记录过的内容和历史，主要靠这些数据保存         |
| `.git/config`      | 当前仓库配置；关联远程后可包含远程地址等设置       | 这个仓库自己的设置本                      |

初始化时不会立即拥有全部历史记录；某些数据文件会在后续 Add、Commit 等操作后才出现。`.git/` 也不是给每个版本直接复制一个完整项目文件夹，而是用 Git 对象及引用组织历史。参考：[仓库目录结构](https://git-scm.com/docs/gitrepository-layout)、[Git Ignore](https://git-scm.com/docs/gitignore)。

#### 2.4.3 为什么经常看不到 .git？

学习阶梯：**L1 · 新手先学**

- Windows：Git 默认通常会给新建的 `.git/` 设置隐藏属性；文件管理器未开启显示隐藏项目时，就可能看不到它。Windows 上不是所有点开头的文件都会自动隐藏。
- VS Code：资源管理器还可能按 `files.exclude` 等规则不显示某些文件；“不显示”不代表它不存在，也不等于被 `.gitignore` 忽略。
- macOS / Linux：点开头的文件或目录通常按隐藏项处理。

参考：[Git 的 Windows 隐藏属性配置](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corehideDotFiles)、[VS Code 排除设置](https://code.visualstudio.com/docs/editing/codebasics)。


> [!warning]
> 只查看，不要随便删除或手工修改 `.git`
> 
> 删除它可能丢失本地历史、分支、暂存信息和仓库配置，即使项目文件还在，也不等于版本记录还在。少数场景（例如关联 Worktree）中，`.git` 可能是指向实际管理目录的文件，而非目录，不能一概理解成“必定有一个同名文件夹”。参考：[Git 仓库布局](https://git-scm.com/docs/gitrepository-layout)。

### 2.5 .gitignore：忽略规则文件

学习阶梯：**L1 · 新手先学**

> [!note]
> 比如你新建了一个文件夹，里面的文件长这样：
> 
> ```text
> my-project/
> ├─ .git/ （已被隐藏）
> ├─ src/
> ├─ node_modules/
> ├─ .env
> ├─ debug.log
> └─ README.md
> ```

但你不想让 Git 管：

```
node_modules/
.env
debug.log
```

那就在项目根目录创建一个纯文本文件，文件名必须是 `.gitignore`，不要带 `.txt` 后缀：

```
.gitignore
```

里面写：

```
node_modules/
.env
debug.log
```

这样Git就不会管这些垃圾文件啦

> [!tip]
> 已经被跟踪的文件不会仅因补写 `.gitignore` 就停止跟踪；补救步骤见 [[#10.2 已跟踪文件的补救：保留本机文件并停止跟踪|停止跟踪流程]]。

### 2.6 Fetch、Pull、Push 与 Sync Changes

学习阶梯：**L1 · 新手先学**

| 图标               | 含义                  | 大白话                                    | 是否改变本地代码（硬盘） | 是否上传到Github |
| ---------------- | ------------------- | -------------------------------------- | ------------ | ----------- |
| **Fetch**        | 获取远程提交并更新远程跟踪引用<br> | 去 GitHub 看一眼，把远程最新情况记下来，但先别动我现在的本地文件。  | ❌️           | ❌️          |
| **Pull**         | 获取并整合远程提交到当前分支<br>  | 把远程的新东西拿下来并合进当前分支                      | ✅️           | ❌️          |
| **Push**         | 推送本地提交到目标远程分支<br>   | 把你本地的提交传到远程                            | ❌️           | ✅️          |
| **Sync Changes** | 先 Pull，再 Push<br>   | 先 Pull，再 Push<br>（说白了就是把别人改的变成自己的正式版本） | ✅️           | ✅️          |
> [!note]
> 注意：pull 和 push 都是一次性推到最新进度，而不是一次一次地推。


#### 2.6.1 Fetch 更新什么，不更新什么？

学习阶梯：**L1 · 新手先学**

| Fetch后的改变     | 大白话                     |
| ------------- | ----------------------- |
| VS Code Graph | 地图上多出了远程的新路线信息，不代表你搬过去了 |
| 当前本地分支与 HEAD  | 你本人还站在原来的位置             |
| 工作区与暂存区       | 桌面上正在写的文件和待提交清单不被顶掉     |


> [!summary]
> **核心结论**
>
> **Graph 变了，不等于工作区文件变了。单纯 Fetch 不会把你正在编辑的项目文件顶掉。**
> **fetch = 更新地图，不搬家。**

> [!note]
> - 工作区 = 你桌面上摊开的那份文件
> - .git 数据库 = 柜子里保存的各个历史版本


- fetch已经得到了Github上的所有文件和整个git历史，并把它放进了 .git 数据库里面，但没有修改本地硬盘里的文件。

这里讨论普通工作仓库中的正常 `git fetch`，不是手动指定特殊引用更新方式或同时执行其他命令。参考：[Git Fetch](https://git-scm.com/docs/git-fetch)、[VS Code 历史图](https://code.visualstudio.com/docs/sourcecontrol/history)。

#### 2.6.2 Graph 已经知道 E，工作区却仍在 C

学习阶梯：**L2 · 日常熟练**

假设当前检出 `main`，工作区没有未提交改动。开始时，本地只知道提交 C；同事已经在 GitHub 的同一条主线上提交了 D、E。

```text
Fetch 前：
  本地 main           A---B---C
  本地 origin/main    A---B---C      ← 旧的远程位置记录
  GitHub 实际 main    A---B---C---D---E

执行 git fetch 后：
  本地 main           A---B---C      ← 没有移动，HEAD 仍指向 main
  本地 origin/main    A---B---C---D---E

  工作区：仍然是 C 对应的项目文件，不会自动变成 E
```

图中的 A、B、C 是同一批提交；本地 main 只是落后了，**并不是 Fetch 制造了一个新分叉**。Graph 可以显示 D、E，因为这些提交现在已经获取到本地，且远程跟踪引用指向了 E；你当前的 main 仍停在 C。

如果 Fetch 前还有自己没提交的change，工作区仍保留这些change，不能简单说成“纯粹的 C 版本”。Graph 也不会因为 Fetch 就丢掉原来只存在于本地的提交。参考：[Git Fetch](https://git-scm.com/docs/git-fetch)、[VS Code Graph](https://code.visualstudio.com/docs/sourcecontrol/history)。

#### 2.6.3 什么时候工作区才会更新？

学习阶梯：**L2 · 日常熟练**

- 执行 `git pull`，或在当前分支执行 `git merge origin/main` / `git rebase origin/main`，整合远程提交后，工作区才可能随结果更新。
- 执行 `git switch` 切换分支，或用 `git checkout` 检出某个版本，也可能改变工作文件；这是另一个操作，不是 Fetch 自动做的。
- `git reset --hard` 也能改变工作文件，但有丢失未提交内容的风险，**不要把它当成 Fetch 后的常规下一步**。

在上面的可快进示例中，如果随后成功 Pull，main 才会从 C 前进到 E，工作区也随之更新；如果双方分叉或发生冲突，先按实际状态处理，不能假定直接覆盖成功。参考：[Git Pull](https://git-scm.com/docs/git-pull)。


参考：[Git Fetch 的获取范围与对象机制](https://git-scm.com/docs/git-fetch)。

#### 2.6.4 Fetch 会覆盖原来的 .git 吗？

学习阶梯：**L2 · 日常熟练**

不会。普通 Fetch 是在现有仓库里获取缺少的对象、更新相应的远程跟踪记录，不是把 GitHub 的 `.git` 整个复制过来，替换你本地的 `.git`。

```text
不是：本地 .git → 被远程的 .git 整体替换

而是：现有本地仓库
      + 远程新增且本地缺少的对象
      + 更新后的远程位置记录
      = 获取完成后的本地仓库
```

- 也就是说，把本地的`.git`给缝缝补补，补成Github的历史记录了。

本地分支、由它们引用的本地提交、HEAD、仓库配置和暂存区，不会因为普通 Fetch 就被远程的同名内容整体顶掉。**会变化的是远程跟踪记录及相关获取数据，不是“本地所有数据都原封不动”，也不是“本地原来的版本没了”。**

> [!note]
> **柜子的比喻**
>
> Fetch 不是“把整个柜子换成别人家的柜子”，而是“把别人家新出现、我这里没有的档案复制进我的柜子，并更新一张‘远程现在到哪了’的标签”。

这里说的“放在一起保存”只是在描述对象共存，不等于已经执行了 Git Merge、把两边代码整合成一个版本。参考：[Git Fetch](https://git-scm.com/docs/git-fetch)。

#### 2.6.5 Fetch 后不想 Pull，需要恢复 .git 吗？

学习阶梯：**L2 · 日常熟练**

不用。假设本地停在 B，而远程已经有了 C1：

```text
Fetch 后，不执行 Pull：
  main         → B
  origin/main  → C1
  HEAD         → main

  工作区：仍是 B 的文件，加上你可能已有的未提交changes
```

`origin/main → C1` 只是说明“我现在知道远程到 C1 了”，不会强迫 `main` 也前进到 C1。**Fetch 后不想 Pull，就别 Pull；可以继续保留自己的版本、继续开发。**

通常没必要撤销远程位置记录或恢复 `.git`。远程跟踪引用的旧位置与恢复方法是另一类问题，不要为此删除 `.git`、Hard Reset 或强推。只是继续开发之后，仍要面对将来如何整合远程改动的问题。


#### 2.6.6 本地新提交 C2 会覆盖远程 C1 吗？

学习阶梯：**L3 · 团队协作**

不会。用 **C1 表示同事的远程提交，C2 表示你的本地提交**，就容易分清了。假设二者内容不同，确实形成了两个不同提交：

```text
最初双方：
  A---B

同事先提交 C1；你 Fetch 后：
  A---B---C1  ← origin/main
      ↑
     main    ← HEAD 仍指向 main

你不 Pull，从 B 继续修改并 Commit 得到 C2：
      C1  ← origin/main
     /
A---B
     \
      C2  ← main、HEAD
```

- 开始分叉了。

- **C1、C2 同时保存在本地仓库的对象数据中，不互相覆盖。**
- C1、C2 只是教学名字；Git 根据对象 ID（哈希）区分提交，例如 C1 是 `8f32a1b`，C2 是 `d91c47e`，并不是按照“第几个版本叫 C”保存。
- 你的新 Commit 推进当前本地 `main` 到 C2，不会顺便把 `origin/main` 从 C1 改到 C2；后者是本地对远程位置的记录。
- 此时叫**分支分叉（diverged）**：双方都从 B 出发，各自有了对方没有的提交。共存在 `.git` 里，不代表已经合并。
- 工作区对应你这一侧的 C2，以及后续可能继续产生的编辑；不会因为 C1 也在 `.git` 中，就自动混入 C1 的修改。

这种分叉来自双方各自创建了提交，不是 Fetch 凭空制造了新提交。若上游upstream是 `origin/main`，`git status` 通常会提示双方已分叉、各自有独有提交。参考：[Git Status](https://git-scm.com/docs/git-status)。

#### 2.6.7 怎样整合 C1 和 C2？

学习阶梯：**L3 · 团队协作**

这时才需要按团队规则选择 Merge 或 Rebase，而不是指望 Commit 自动整合远程：

```text
选择 Merge：保留 C1、C2，并产生同时连接两边的合并提交 M

      C1
     /  \
A---B    M  ← main、HEAD
     \  /
      C2

选择 Rebase：将你的改动重放到 C1 后面

A---B---C1---C2'  ← main、HEAD
        ↑
   origin/main
```

Merge 示例中，`origin/main` 仍记录 C1；M 是本地整合结果。Rebase 示例中，C2′ 通常是新的提交、哈希不同，不是把旧 C2 对象就地改掉。**两种方式都可能遇到冲突，需要解决并测试**

具体操作见第 9.6～9.9 节。参考：[Git Merge](https://git-scm.com/docs/git-merge)、[Git Rebase](https://git-scm.com/docs/git-rebase)。

> [!summary]
> **Fetch 的最短记忆版**
>
> **Fetch 不换掉本地柜子；不想 Pull 就先不 Pull；远程 C1 和本地 C2 可以同时存在。两边独立前进叫分叉，只有后续整合才叫合并或变基。**

### 2.7 Changes、文件状态与 Graph

学习阶梯：**L1 · 新手先学**

- **Changes**：尚未进入提交的文件变化。
- **Staged Changes**：已经选入暂存区、准备由下一次 Commit 记录的变化。
- **Outgoing Changes**：相对于上游upstream（Github），已经commit提交到本地、但尚未push到Github的commit；**不是changes**。

#### 2.7.1 U、M、D、A、R、C：文件状态

学习阶梯：**L1 · 新手先学**

| 图标  | 含义                          | 大白话                                                   |
| --- | --------------------------- | ----------------------------------------------------- |
| U   | Untracked：未跟踪               | Untracked，没上传过git<br>例：新增的图片、新创建的文件                   |
| M   | Modified：已跟踪文件有修改           | Modified，上传过git<br>例：`6.Ray Tracing.md`               |
| D   | Deleted：已跟踪文件被删除            | Deleted，上传过git，但已经被删除<br>例：原位置的 `unity集大成.md`，文件名带删除线 |
| A   | Added：新增文件已暂存               | Added，添加到暂存stage区                                     |
| R   | Renamed：重命名                 | Renamed，文件被重命名                                        |
| C   | Copied：Git 状态中的复制；冲突需结合工具提示 | Conflict，有冲突                                          |
> [!note]
> 表格中的个人说法保留原文。严格来说，文件是否被跟踪、是否被修改，与是否已推送是不同问题；`C` 可表示复制，冲突要结合 `UU` 等具体状态判断。截图判断见 [[#3.1.2 Changes工作区部分|文件状态截图]]。

#### 2.7.2 Graph：提交历史与分支位置

学习阶梯：**L2 · 日常熟练**

VS Code 把 `.git` 里那些平时看不见的 Git 历史，用可视化方式画出来了。

Graph 可以显示提交、分支与远程跟踪位置；图上的远程状态取决于最近获取的信息。
**读图示例见 [[#3.1.3 Graph工作区部分|Graph 截图]]，Fetch 的分叉图见 [[#2.6.6 本地新提交 C2 会覆盖远程 C1 吗？|C1 与 C2]]。

### 2.8 协作、撤销与排错名词

学习阶梯：**L2–L4 · 协作与进阶名词，按需查阅**

这里先认名词，具体操作与适用前提见 [[#9. 团队协作：先界面，后命令|团队协作双方法流程]]。

#### 2.8.1 整合与提交整理

学习阶梯：**L3 · 团队协作**

例图：
```
      C1
     /  \
A---B    M
     \  /
      C2
```

| 名词            | 含义                            | 大白话                    | 例图解释          |
| ------------- | ----------------------------- | ---------------------- | ------------- |
| Diverged / 分叉 | 双方都有对方没有的提交                   | 两边从共同起点各走了一段           | 从B            |
| Merge         | 合并分支；分叉时通常产生合并提交              | 把两条路线求个并集              | 求个并集M         |
| Rebase        | 在新的基点上重放提交，通常改变提交 ID          | 把自己的改动接到新主线后面          | C2接到C1后面，成一条线 |
| Conflict      | Merge / Rebase 时需要人工决定最终内容的情况 | 你要选择两条路线怎么Merge和Rebase |               |
| Merge Base    | 合并之前，两条历史最后共同经过的那个 commit。    | 从哪里分叉的，那个点就是。          | B点            |


| 名词          | 含义                        | 大白话                                 |
| ----------- | ------------------------- | ----------------------------------- |
| Cherry-pick | 把指定提交的改动移植到当前分支，通常创建新提交   | 不拿整条分支，只像**挑樱桃**一样，挑其中某一个 commit 过来 |
| Amend       | 用新提交替代最近一次提交，可调整说明或纳入暂存内容 | 修正最近一次 commit，比如改提交说明、补进漏掉的文件       |
| Reword      |                           | 把 commit message 重新写一遍              |
| Squash      | 挤压                        | 把几个Commit 挤成一个Commit                |

操作见 [[#9.6 功能分支接入主线：Merge / Rebase 二选一|整合主线]]、[[#9.7 冲突处理：会解决，也会安全退出|冲突处理]]、[[#9.8 提交整理：Amend、Reword、Squash / Fixup|整理提交]]、[[#9.9 改写已发布历史后：为什么不是直接 Force Push？|强推边界]]、[[#9.10 Cherry-pick：只移植一个修复，不合并整个分支|移植修复]]。

#### 2.8.2 Stash 与 Worktree

学习阶梯：**L2 · 日常熟练**

| 名词       | 含义                             | 大白话                    |
| -------- | ------------------------------ | ---------------------- |
| Stash    | 临时保存未提交改动                      | 把 change 存进去，就叫做 Stash |
| Worktree | 同一仓库另开工作目录；共享部分仓库数据，工作文件和暂存区独立 | 另开一张桌子处理急事，不是完全独立的新仓库  |
|          |                                |                        |
注意：working tree 不等于 worktree
	working tree是单个工作区
	worktree可以多开

操作见 [[#9.11 临时任务：Stash 与 Worktree|临时任务流程]]。

#### 2.8.3 Restore、Reset、Revert 与 Reflog

学习阶梯：**L3 · 团队协作**

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| Restore | 恢复工作文件 / 暂存区中的指定路径 | 恢复工作文件可能覆盖尚未提交的编辑 |
| Reset | 移动当前分支位置；不同模式还会重置暂存区 / 工作区 | 必须看模式，Hard 风险很高 |
| Revert | 新增反向提交，抵消已提交变化 | 不改写旧历史；也可能冲突，需要测试 |
| Reflog | 查本机引用位置的移动记录，寻找旧提交 | 不是所有文件的回收站，也不是永久远程备份 |

操作见 [[#9.12 撤销与救援：Restore / Reset / Revert / Reflog|撤销与救援流程]]。

#### 2.8.4 Log、Blame 与 Bisect

学习阶梯：**L4 · 进阶按需**

| 名词 | 含义 | 大白话 |
| --- | --- | --- |
| Log / History | 查看提交历史；可按路径、说明或补丁变化检索 | 找以前哪一笔记录改过这里 |
| Blame | 追踪每行最后一次修改涉及的提交 | 找上下文，不是直接判定谁负责 |
| Bisect | 在已知好、坏版本之间二分定位问题提交 | 一次排除一半，缩小 Bug 范围 |

操作见 [[#9.13 排查“谁改的、哪次引入了 Bug”|历史检索与 Bug 定位]]。

### 2.9 团队与命令行辅助名词

学习阶梯：**L1–L3 · 混合词表，遇到不懂的词再查**

| 名词                               | 含义                                   | 大白话                   |
| -------------------------------- | ------------------------------------ | --------------------- |
| Clone                            | 获取仓库的项目文件及 Git 历史，不是普通 ZIP 下载        | 从Github把项目连版本记录一起拿到本地 |
| Initialize Repository / git init | 初始化本地仓库，不会直接在 GitHub 创建仓库            | 先在本机建立版本管理            |
| Publish to GitHub                | 在 GitHub 建立远程仓库并发布本地项目               | 给本地项目建立远程存放位置         |
| Public / Private                 | 发布时选择的仓库可见性                          | 看清项目准备公开还是私有          |
| Remote                           | 远程仓库地址与相关配置；`origin` 是常用别名           | 本地项目准备与哪里收发提交         |
| Commit Hash / ID                 | 用于识别提交的哈希；界面也会显示短哈希                  | 一次提交的“身份证号”           |
| Commit Message                   | 提交说明                                 | 这次提交做了什么，起个能看懂的名字     |
| Fork                             | 在没有原仓库写权限等场景下，先从自己的仓库发起 PR           | 先在自己的仓库改，再请对方合入       |
| Issue                            | GitHub 集成中可管理的问题条目                   | 团队记录和讨论待处理事项的入口       |
| Tag / Release                    | Tag 标记特定提交，Tag 不等于完整的 GitHub Release | 给版本留标记，与完整发布流程区分开     |
| Submodule                        | 主仓库记录子模块的特定提交，不自动跟踪其最新代码             | 主项目记住子项目的某一版          |
| Git LFS                          | 用指针记录大文件的工作方式，需单独安装相关工具              | 大文件按项目规则走专门通道         |
| Hook                             | 可在提交等操作时执行检查；失败时需看具体输出               | 不要把绕过检查当作日常操作         |
| CI                               | PR 等流程中的持续集成检查                       | 本地测试通过，不代表平台检查也通过     |
| .gitattributes                   | 仓库用于文件属性、换行等约定的配置                    | 按项目规范处理，不随手改全局配置      |


创建与发布见 [[#5.2 两种起点：克隆或发布|首次建仓流程]]；团队约定见 [[#9.15 入职后的团队约定与按需能力|团队与发布规范]]；命令参数写法见 [[#9.2 先看懂命令的写法|命令行阅读约定]]。

### 2.10 GitHub 平台名词：界面背后的对象

学习阶梯：**L1–L3 · 先认识名称，配置细节以后再学**

| 名词 | 含义 | 大白话 |
| --- | --- | --- |
| Dashboard | 登录后的个人工作首页 | 从这里进入常用仓库与待办 |
| Issue / PR / Project | 事项、合并请求与组织工作计划的不同对象 | 记问题、审改动、排计划，不是同一个按钮 |
| Actions / Workflow / Run | 自动化平台 / 流程配置 / 某一次执行 | 脚本在哪跑、按什么流程跑、这次跑得怎样 |
| Runner | 执行自动化任务的环境或机器 | 干活的机器，不是 Git 分支 |
| Agents / Session | AI 代理任务入口与会话记录 | 看 AI 在做什么，结果仍需要审核 |
| Wiki / README | 独立的项目文档区 / 仓库中的说明文件 | 长篇说明书与项目首页简介是不同位置 |
| Watch / Star / Fork | 通知订阅 / 收藏关注 / 派生仓库 | 看动态、收藏、另开自己的仓库副本；都不等于 Clone |
| Codespaces | GitHub 提供的云端开发环境 | 在远端环境写代码，不是普通 ZIP 下载 |
| Security policy / Advisory | 安全报告约定 / 安全公告 | 规定怎么报告问题，并管理披露信息 |
| Dependabot / Code scanning / Secret scanning | 依赖风险 / 源码问题 / 凭据泄露等不同检查 | 第三方库、程序本身、钥匙泄露，分别处理 |
| Ruleset / Default branch | 仓库规则集 / 默认分支 | 什么能做、默认看哪条路线，不会切换本机分支 |
| Release / Package / Immutable release | 发行版 / 发布的软件包 / 带不可变保护的发行版 | 代码提交之外的发布对象与保护机制 |
| Secret / Variable / Deploy key | 机密值 / 配置变量 / 机器访问仓库的密钥 | 配自动化与访问权限，不是把密码写进笔记 |
| Webhook / GitHub App | 事件通知到外部系统 / 集成应用 | 让其他系统参与，先看清权限 |

上表只作查词入口。按钮位置、截图状态与英文名称见 [[#4. GitHub 网页图标与菜单速查|GitHub 界面速查]]。

## 3. VS Code 图标与菜单速查

学习阶梯：**L1–L2 · 界面速查，不必一次记住所有菜单**

> [!note]
> - 我先解释：整个大面板的各个图标含义
> - 然后再详细解释：每个菜单下面的选项含义

### 3.1 主面板图标

学习阶梯：**L1 · 新手先学**

![[有md文档的大面板截图.png]]

![[有红绿Changes的大面板截图.png]]

#### 3.1.1 编号图标含义

学习阶梯：**L1 · 新手先学**

[[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] / [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] / [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] / [[#2.6 Fetch、Pull、Push 与 Sync Changes|Sync Changes]] 的区别见 [[#2.6 Fetch、Pull、Push 与 Sync Changes|远程同步名词]]。

| 图标                                                                             | 含义                        | 大白话                                                                |
| ------------------------------------------------------------------------------ | ------------------------- | ------------------------------------------------------------------ |
| ① [[#2.8.2 Stash 与 Worktree\|Stash]] All [[#2.7 Changes、文件状态与 Graph\|Changes]] | 临时保存未提交改动；不是 Stage，也不会自动形成普通 Commit | 把changes存着，等着commit                                                |
| ② [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Commit]]                     | 把暂存内容记录为本地提交；不会自动上传 | 提交当前已经 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Stage]] 的修改 |
| ③ Create Pull Request                                                          | 在 GitHub 上创建分支间的 PR；通常由 GitHub PR 扩展提供，不是直接合并本地与云端文件 | 请求把 Github上的 和 本地的 合并                                              |
| ④ Refresh                                                                      | 重新读取源代码管理状态，不等于 Fetch | 刷新一下 Changes 工作区                                                   |
| ⑤ Open Changes                                                                 | 打开未提交文件差异；比较对象取决于所在列表 | 查看 Changes                                                         |
| ⑥ Discard All Changes                                                          | 丢弃未提交编辑；涉及未跟踪文件时可能删除文件，先确认范围 | 把所有changes撤销了                                                      |
| ⑦ Stash All Changes                                                            | 与 ① 同类；是否包含未跟踪文件取决于所选 Stash 操作 | 同 ①                                                                |
| ⑧ 筛选分支                                                                         | 可以筛选多个                    | 筛选你想看的分支                                                           |
| ⑨ Go to Current History Item                                                   | 让历史视图定位到当前提交，不会切换工作版本 | 去到 HEAD / 你现在所在的位置                                                 |
| ⑩ Fetch From All Remotes                                                       | 从全部已配置远程获取更新；不自动整合到当前分支 |                                                                    |
| ⑪ Pull                                                                         | 把远程的新提交拉下来并整合             | “GitHub → 我的电脑”                                                    |
| ⑫ Push                                                                         | 把本地已经 Commit 的提交推到远程      | “我的电脑 → GitHub”                                                    |
| ⑬ Refresh                                                                      | 刷新历史图的显示，不代表已获取远程新提交 | 刷新 Graph 工作区                                                       |
| ⑭ Current Branch                                                               | 显示当前所在分支，如 `ai-polished*` | “我现在在哪条分支”                                                         |
|                                                                                | 点击之后的部分截图：                |                                                                    |
| `ai-polished*` 的 `*`                                                           | 分支名后的 * 表示：存在未提交的changes  | 对于最近一次 commit 来说，还有changes。                                        |
| ⑮ [[#2.6 Fetch、Pull、Push 与 Sync Changes\|Synchronize Changes]] ↻               | 同步当前分支<br>都是先Pull，再Push   | ![[Sync Changes.png]]<br>我们点击commit后，弹出的这个也同理。                     |
| `0↓`                                                                           | Incoming commits = 0      | Github上没有要Pull的commit                                              |
| `1↑`                                                                           | Outgoing commits = 1      | 你本地有 1 个 commit 等待 Push                                            |
| ⑯ Open as Preview                                                              | 当你浏览md文档时，会出现             | 按照md格式来渲染，而不是代码格式                                                  |
| ⑰ Open Changes                                                                 | 打开当前文件的差异，结合列表位置确定比较对象 | 同⑤                                                                 |
| ⑱ Open Changes with Previous Revision                                          | 当前版本和上一个版本比较              | 看看这次相对上一次commit改了什么                                                |
| Open Changes with Revision...                                                  | 让你自己选一个历史版本来比较            | 拿当前版本和我指定的某个 commit 比                                              |
|                                                                                |                           |                                                                    |
| ⑲ Editor 类型下拉菜单                                                                | 切换当前文件用什么渲染格式打开           | 如 Text Editor / Markdown Preview                                   |
| ⑳ Open Files                                                                   | 打开文件本身，不是执行 Git 操作 | 打开这个文件                                                             |
| ㉑ Revert Block                                                                 | 丢弃这一块未提交修改；不是新增反向提交的 git revert | 撤销这一小块修改                                                           |
| ㉒ Stage Block                                                                  | 只将这一块内容放入暂存区，不等于提交 | 只暂存这一小块修改                                                          |
| ㉓ Previous Change                                                              | 在 Diff 编辑器中跳转到上一处差异 | 看上一处 Change                                                        |
| ㉔ Next Change                                                                  | 在 Diff 编辑器中跳转到下一处差异 | 看下一处 Change                                                        |


#### 3.1.2 Changes工作区部分

学习阶梯：**L1 · 新手先学**

文件状态名词统一见 [[#2.7.1 U、M、D、A、R、C：文件状态|文件状态对照表]]；下面结合截图判断具体情况。

👇

![[解释DMU的截图.png]]

👆

> [!note]
> **原话与技术含义分开看**
>
> 表格“大白话”中的原有表述保持不变。严格来说，U / M / D 表示跟踪与文件变化状态，不等于是否推送到 GitHub；Git 的 `C` 状态可表示复制，冲突应结合 [[#2.8.1 整合与提交整理|Merge]] [[#2.7 Changes、文件状态与 Graph|Changes]]、`UU` 等实际提示判断。技术定义见“含义”列。参考：[Git 状态格式](https://git-scm.com/docs/git-status)。

这里的 U 是未跟踪，不表示发生冲突。不过，命令行 `git status --short` 的双列状态里，`UU` 等组合可表示未合并状态，不能把两种显示混为一谈。依据：[VS Code 文件标记](https://code.visualstudio.com/docs/sourcecontrol/staging-commits)、[Git 状态格式](https://git-scm.com/docs/git-status)。

从截图推测，同名文件“一处 D、一处 U”**可能是移动位置**，但仅凭文件名无法确认。应打开内容比较；当新旧路径都被暂存后，Git 可根据内容相似性识别为重命名/移动。确认是移动且两部分都属于本次任务时，应一并暂存，避免只提交删除。

两个 JSON 看起来属于 Obsidian 工作区和插件状态文件，**并非都一定不该提交**；本文建议先检查 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]，再决定是否值得记录，避免混入与正文无关的自动状态变化。此判断只基于截图，没有读取这些配置文件。关于跟踪与重命名检测，参考：[Pro Git：记录更新](https://git-scm.com/book/zh/v2/Git-基础-记录每次更新到仓库)、[Git Status](https://git-scm.com/docs/git-status)。

#### 3.1.3 Graph工作区部分

学习阶梯：**L2 · 日常熟练**

![[解释Graph的截图.png]]

[[#2.7.2 Graph：提交历史与分支位置|Graph]] 的概念见 [[#2.7.2 Graph：提交历史与分支位置|Graph 与历史图]]；下面只结合截图读分支位置。

| 图标                 | 含义            | 大白话                                                           |
| ------------------ | ------------- | ------------------------------------------------------------- |
| 分支图标 + ai-polished |               | 显示筛选出来的分支<br>左键点击，选择你要筛选的分支<br>我只想看ai-polished这条分支，所以我把它筛选出来了 |
| `◎`                | 定位当前位置 / [[#2.3 仓库、分支与远程名词\|HEAD]] | 把视图跳回“我现在所在的位置”                                               |
| `↓ 带分叉`            | [[#2.6 Fetch、Pull、Push 与 Sync Changes\|Fetch]]         | 看远程有没有新提交，但不改变本地                                              |
| `↓`                | [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Pull]]          | 把远程提交拉下来并整合到当前分支，改变本地                                         |
| `↑`                | [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Push]]          | 把本地已经 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Commit]] 的提交推到远程                                          |
| `↻`                | Refresh       | 刷新 Git Graph 显示。卡了                                            |
| `...`              | More Actions  | 有 View As Tree ; View As List                                 |

截图中：

- [[#2.3 仓库、分支与远程名词|origin]] 可以理解为云端☁️，就是远程（Github）。
- `ai-polished` 是当前本地分支，标签位于“数学公式修改2”这个提交处。
- `origin/ai-polished` 显示在较早的“callout修改1”处。
- [[#2.3 仓库、分支与远程名词|origin/main]] 显示在“人工笔记”处。
- 上方的 **[[#2.7 Changes、文件状态与 Graph|Outgoing Changes]]** 表示相对于上游，存在本地已提交、尚未推送到远程的记录。
	这里指的就是：“数学公式修改2”。
	本地commit了，**但是相比于commit的东西，还有[[#2.7 Changes、文件状态与 Graph|changes]]**，并且还没有push到Github上。

按截图所示的线性关系，本地 `ai-polished` 看起来领先 `origin/ai-polished` 一次提交；这只是截图时、基于本地已知远程状态的判断，不是实时仓库核验。先 Fetch 才能确认远程是否又发生变化。参考：[VS Code 历史图](https://code.visualstudio.com/docs/sourcecontrol/history)。

> [!important]
> **两件独立的事**
>
> **上面的 7 项 Changes** [[解释DMU的截图.png]] ：还没进入提交的文件变化。
> **下面的 Outgoing Changes**：已经进入本地历史、还没推送的提交。
> 只点 Push 不会顺便上传那 7 项未提交改动；先 Commit 才能把所选改动纳入历史。

**如果此时Push会怎么样？**

- 那么Github会从“callout修改1”推到“数学公式修改2”这个版本。
- 但是，基于“数学公式修改2”的7项Changes，不会push到Github上。

### 3.2 菜单入口与选项速查

学习阶梯：**L2 · 日常熟练**

#### 3.2.1 右键 Graph 里的 Commit

学习阶梯：**L2 · 日常熟练**

![[右键Graph里的Commit.png|200]]

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| `Open Changes` | 打开这个提交改了哪些文件、哪些内容 | 看“这次 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|commit]] 到底改了啥” |
| `Open on GitHub` | 在 GitHub 网页打开对应提交/分支 | 去网页上看 |
| `Checkout` | 切换到这个分支/引用 | “我要去这个位置工作” |
| `Checkout (Detached)` | 直接切到某个 commit，不挂在分支上 | “只去旧版本看看” |
| `Create Branch...` | 从当前位置新建分支 | “从这里岔出一条新路线” |
| `Delete Branch` | 删除分支引用 | “把这个分支标签删掉” |
| `Create Tag...` | 给当前 commit 打标签 | “给这个版本起个固定纪念名” |
| [[#2.8.1 整合与提交整理\|Cherry Pick]] | 把这个 commit 单独搬到当前分支 | “只拿这一笔修改过来” |
| `Compare with Remote` | 和远程对应分支比较 | 看“本地和 GitHub 差在哪” |
| `Compare with Merge Base` | 和两条分支共同祖先比较 | 看“从分叉点之后改了什么” |
| `Compare with...` | 手动选另一个 commit / 分支比较 | “拿它和另一个版本对比” |
| `Copy Commit Hash` | 复制 commit 的唯一编号 | 复制类似 `e4f5a6b` |
| `Copy Commit Message` | 复制提交说明文字 | 复制“修复登录问题”这种内容 |
| `Add to Chat` | 把这个 Git 内容加到 AI 聊天上下文 | 让 AI 帮你分析 |
| `Explain Changes` | 让 AI 解释这个提交的变化 | “这次到底改了什么，讲人话” |

#### 3.2.2 鼠标停留在分支

学习阶梯：**L1 · 新手先学**

![[鼠标停留在分支的截图.png]]

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| `Ryel` | 这个 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|commit]] 的作者 | 谁提交的 |
| `23 hours ago (October 14, 2026 at 4:52 PM)` | 提交时间 | 什么时候提交的 |
| `人工笔记` | [[#2.9 团队与命令行辅助名词\|Commit Message]] | 这次提交的说明 |
| `530 files changed` | 这次提交影响了 530 个文件 | 改动范围有多大 |
| `207052 insertions(+)` | 新增了 207052 行 | 一共加了多少内容 |
| [[#2.3 仓库、分支与远程名词\|origin/main]] | 远程跟踪分支指向这个 commit | 你本地记录的远程 [[#2.3 仓库、分支与远程名词\|main]] 现在在这里 |
| `main` | 本地 `main` 分支也指向这个 commit | 本地 main 和远程 main 当前在同一个位置 |
| `6a4e97a` | 这个 commit 的短 [[#2.9 团队与命令行辅助名词\|Hash]] | 这次提交的“身份证号” |
| `Open on GitHub` | 在 GitHub 网页打开这个 commit | 去网页看这次提交 |

#### 3.2.3 Changes 的省略号

学习阶梯：**L2 · 日常熟练**

![[Changes的省略号截图.png|200]]

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| View as Tree； | 按文件夹树显示![[View As Tree.png\|200]] | 按目录一层层看文件 |
| View As List | 按文件列表显示![[View As List.png\|200]] | 把改动文件平铺出来 |
| View & Sort | 调整文件显示与排序<br>![[View & Sort.png\|200]] | 根据什么来排列[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|change]]的文件。<br>Status就是U M D这些字母。 |
| [[#2.9 团队与命令行辅助名词\|Clone]] | 克隆仓库 | 把远程仓库克隆到电脑 |
| Checkout to... | 切换分支或检出某个版本<br>和[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Commit]]里的一样 | 去另一个分支或版本 |
| [[#2.6 Fetch、Pull、Push 与 Sync Changes\|Fetch]]；[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Pull]]；[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Push]] | 获取远程状态；整合远程提交；上传本地提交 | 先看、再收、再发 |
| Commit | 提交相关操作；其中 [[#2.8.1 整合与提交整理\|Amend]]、Undo 等会改变本地提交历史，需要看清说明 | 把选好的修改记成一次本地历史 |
| [[#2.7 Changes、文件状态与 Graph\|Changes]] | 与文件改动相关的操作入口；不要把 Discard 当成 Unstage | 处理还没提交的文件改动 |
| Pull, Push | 更多拉取、推送和同步选项 | 更多收发与同步方式 |
| [[#2.3 仓库、分支与远程名词\|Branch]]；[[#2.9 团队与命令行辅助名词\|Remote]] | 分支管理；远程仓库地址与配置管理 | 管理本地路线和远程地址 |
| [[#2.8.2 Stash 与 Worktree\|Stash]] | 暂时收起未提交改动，处理别的任务后再恢复 | 没做完的先收起来 |
| [[#2.9 团队与命令行辅助名词\|Tags]] | 给特定提交打标签，例如版本发布点 | 给某个版本打个固定标记 |
| Show Git Output | 打开 Git 输出日志，操作失败时查看实际命令和错误 | 出错时看 Git 实际说了什么 |
| Show [[#2.7.2 Graph：提交历史与分支位置\|Commit Graph]]；Visualize [[#2.3 仓库、分支与远程名词\|Repository]] [[#2.8.4 Log、Blame 与 Bisect\|History]] | 打开提交历史可视化；可能来自不同内置功能或扩展，不能仅凭菜单统一归为 GitLens | 看版本历史是怎样分叉和前进的 |
| Compose Commits... | GitLens 的提交组织入口，详见第 7 节 | 把混在一起的修改整理成几次提交 |
| Generate [[#2.9 团队与命令行辅助名词\|Commit Message]] with GitLens | 根据变更生成提交说明，不等于已提交或已推送 | 让 AI 起草说明，仍要自己检查 |
| Add Co-authors... | 添加共同作者署名；不是授予 GitHub 仓库权限 | 给共同参与的人署名，不是加权限 |

#### 3.2.4 编辑器上侧的省略号

学习阶梯：**L2 · 日常熟练**

![[主面板上侧的省略号截图.png|200]]

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| `Claude Code: Open` | 打开 Claude Code | 打开 AI 编程助手 |
| `Show Revision Commit` | 查看当前文件对应的某个 Git 版本提交 | “这个版本来自哪次 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|commit]]？” |
| `Open Changes with Next Revision` | 把当前版本和下一个版本做对比 | “看看前后两个版本差了什么” |
| `File Annotations` | 显示文件的 Git 注释信息 | “每一行是谁改的、哪次 commit 改的” |
| `Stage Changes` | 把当前文件的改动加入暂存区 | “这个文件准备放进下一次 commit” |
| `Show Opened Editors` | 显示当前已打开的编辑器/文件 | “我现在开了哪些文件” |
| `Close All` | 关闭所有打开的编辑器标签 | “全关掉” |
| `Close Saved` | 只关闭已经保存的文件 | “没保存的留下，保存过的关掉” |
| `Enable Preview Editors` | 开启预览标签页模式 | 单击文件时先临时预览，不一定永久占一个标签 |
| `Lock Group` | 锁定当前编辑器组 | 防止这个编辑区域被别的文件顶替 |
| `Configure Editors` | 配置编辑器相关选项 | 调整标签页、预览、布局等 |
| `Reopen Editor With` | 用别的编辑器方式打开当前文件 | 比如文本编辑器、Markdown 预览等 |

菜单按截图归纳；通用功能参考 [VS Code 总览](https://code.visualstudio.com/docs/sourcecontrol/overview)、[分支与 Stash](https://code.visualstudio.com/docs/sourcecontrol/branches-worktrees)、[历史与共同作者显示](https://code.visualstudio.com/docs/sourcecontrol/history)，GitLens 专有入口参考 [官方 README](https://github.com/gitkraken/vscode-gitlens)。

#### 3.2.5 点击左下角 Current Branch：创建与切换分支

学习阶梯：**L1 · 新手先学**

![[点击左下角分支的截图.png]]

| 图标 / 选项 | 含义 | 大白话 |
| ---------------------- | -------------- | ----------------------------- |
| Create new branch      | 从**当前位置**创建新分支 | “从这里岔一条新路线”<br>“从当前位置岔出一条新分支” |
| Create new branch from | 指定其他分支 / 标签作为新分支起点，创建后切过去 | 从指定位置岔出新路线 |
| Checkout detached | 检出某次提交而不附着在分支上 | 只去旧版本看看；要继续写并保留成果，先建分支 |

### 3.3 VS Code 图标 / 菜单与命令行对照

学习阶梯：**L2 · 日常熟练；先会点，再理解对应命令**

> [!warning]
> **这是语义对照，不是把所有按钮翻译成一条固定命令**
>
> 图标可能按设置执行多个 Git 调用。下面使用最常见的等价 / 近似写法；文件、分支、提交 ID 都是占位示例。只看表即可，不要整列复制执行。删除、丢弃与历史改写先看安全提醒。

| 图标 / 菜单                                      | 对应命令或近似命令                                                                      | 等价边界 / 没有命令时怎么办                         |
| -------------------------------------------- | ------------------------------------------------------------------------------ | --------------------------------------- |
| Clone Repository / Git: Clone                | `git clone 仓库地址`                                                               | 下载并创建本地仓库；不是普通 ZIP 下载                   |
| Initialize Repository                        | `git init`                                                                     | 仅初始化本地，不创建 GitHub 远程                    |
| Publish to GitHub / Publish Branch           | 前者还创建 GitHub 仓库；后者的 Git 部分近似 `git push -u origin 分支名`                          | 平台建仓与推送分开；确认远程已存在及目标正确                  |
| ① / ⑦ Stash All Changes                      | `git stash push`；含新文件时 `git stash push -u`                                     | 看清是否包含未跟踪文件；不是 Add / Commit             |
| ② Commit ✓                                   | `git commit -m "说明"`                                                           | 前提是已检查暂存内容；智能提交等设置可能增加额外操作              |
| ③ Create Pull Request                        | 没有对应的单条 Git 命令                                                                 | PR 是 GitHub 平台对象；用扩展或 GitHub 网页创建       |
| ④ Refresh Changes                            | 近似重新查看 `git status`                                                            | 刷新显示，不等于下载远程提交                          |
| ⑤ / ⑰ Open Changes                           | Changes 中近似 `git diff -- "文件"`；Staged Changes 中近似 `git diff --staged -- "文件"`  | 先看它位于哪一个列表                              |
| ⑥ Discard All Changes                        | 对未暂存的已跟踪路径近似 `git restore --worktree -- "文件"`                                  | 不给全仓库一键清理配方；未跟踪文件的处理不同，可能真的被删除          |
| ⑧ 筛选分支                                       | 近似 `git log --graph --oneline 分支名`                                             | 图形筛选可组合多个引用，改变的是视图，不是当前分支               |
| ⑨ Go to Current History Item                 | 没有修改仓库的等价命令；`git rev-parse HEAD` 仅查看当前位置                                       | 它只定位图，不是 Checkout                       |
| ⑩ Fetch From All Remotes                     | `git fetch --all`                                                              | 只获取；是否 Prune 等取决于配置                     |
| ⑪ Pull ↓                                     | `git pull`                                                                     | 整合方式受配置影响；严格只允许快进时用后文的 `--ff-only`      |
| ⑫ Push ↑                                     | `git push`                                                                     | 只发送已提交记录，不上传未提交编辑                       |
| ⑬ Refresh Graph                              | 近似重新运行 `git log --graph --oneline --decorate`                                  | 不等于 Fetch                               |
| ⑭ Current Branch / Checkout to...            | 查看：`git branch --show-current`；切换：`git switch 分支名`                             | 查看与切换是两件事                               |
| Create new branch                            | `git switch -c 新分支名`                                                           | 从当前提交创建并切换                              |
| Create new branch from                       | `git switch -c 新分支名 起点引用`                                                      | 与“从当前版本建分支”区分                           |
| Checkout Detached                            | `git switch --detach COMMIT_ID`                                                | 会改变工作文件；新成果需要分支引用保存                     |
| ⑮ Synchronize Changes ↻                      | 先 `git pull`，成功后再 `git push`                                                   | 不是单条 Git 指令；Pull 冲突 / 失败就停，不应继续 Push    |
| `0↓` / `1↑`                                  | `git rev-list --left-right --count "HEAD...@{upstream}"`                       | 输出左列是本地独有，右列是上游独有；没有上游会报错               |
| ⑯ Open as Preview / ⑲ Editor 类型              | 无 Git 命令                                                                       | 只是编辑器渲染方式                               |
| ⑱ Open Changes with Previous Revision        | 比较两个明确提交可用 `git diff COMMIT_A COMMIT_B -- "文件"`                                | 历史文件的上一版本不一定是 HEAD 的第一父提交，不硬写成固定 HEAD~1 |
| Open Changes with Revision...                | `git diff COMMIT_ID -- "文件"` 等                                                 | 这是与当前工作文件比较的写法；历史端点比较要明确两端              |
| ⑳ Open Files                                 | 无 Git 命令                                                                       | 打开当前文件，不改版本状态                           |
| ㉑ Revert Block                               | 近似交互式 `git restore -p -- "文件"`                                                 | 丢弃所选编辑，先备份；不是 `git revert`              |
| ㉒ Stage Block / Stage Selected Ranges        | 近似 `git add -p -- "文件"`                                                        | 新文件与自动拆块行为可能不同，不能保证逐行完全一致               |
| ㉓ / ㉔ Previous / Next Change                 | 无 Git 命令                                                                       | 只是在 Diff 中导航                            |
| 文件旁 `+` Stage Changes                        | `git add -- "文件"`                                                              | 暂存此刻的文件内容；之后再编辑的部分仍需再次暂存                |
| Staged Changes 文件旁 `−`                       | `git restore --staged -- "文件"`                                                 | 保留编辑，只取消暂存；部分取消可用图形选定行                  |
| Create Tag...                                | 近似 `git tag 标签名 COMMIT_ID`                                                     | 注释标签 / 签名需按具体选择；创建本地标签不等于发布 Release     |
| Delete Branch                                | 正常安全删除近似 `git branch -d 分支名`                                                   | 先离开此分支；不把强制删除当默认                        |
| Cherry Pick                                  | `git cherry-pick COMMIT_ID`                                                    | 图标不保证带 `-x`，要记录来源时以明确参数为准               |
| Commit → Undo Last Commit                    | 普通非根提交近似 `git reset --soft HEAD~1`                                             | 只用于未共享提交；根提交特殊，不照抄 HEAD~1               |
| Commit (Amend)                               | `git commit --amend`                                                           | 改写最近一次提交，暂存内容会被带入                       |
| Git: Stash / Apply Stash / Pop Stash         | `git stash push` / `git stash apply "stash@{0}"` / `git stash pop "stash@{0}"` | Apply 保留记录，Pop 成功后通常移除；先核对条目            |
| Branch → Merge... / Git: Rebase Branch...    | `git merge 来源分支` / `git rebase 新基点`                                            | 当前分支接收变化；Merge 和 Rebase 二选一             |
| Show Git Output / Open on GitHub / AI 与编辑器菜单 | 无统一单条 Git 命令                                                                   | 前者用于看实际日志；网页跳转、AI 解释、布局不是 Git 版本操作      |

入口核对：[VS Code 暂存与撤销](https://code.visualstudio.com/docs/sourcecontrol/staging-commits)、[历史图](https://code.visualstudio.com/docs/sourcecontrol/history)、[内置 Git 命令定义](https://github.com/microsoft/vscode/blob/main/extensions/git/package.nls.json)。

## 4. GitHub 网页图标与菜单速查

学习阶梯：**L1–L3 · 先认识 Code / Clone，再学 Issues、PR 与自动化**

> [!note]
> **这节讲 GitHub 网页，不是 VS Code 本地面板**
>
> 以下逐张对应你提供的 11 张截图，按“图标 / 英文名称｜含义｜大白话”解释。界面会随账户、权限和版本变化；截图里的计数、开关和空列表只代表截图时的状态，没有在线检查你的仓库，也没有修改任何 GitHub 设置。
> 概念不懂仍回 [[#2.10 GitHub 平台名词：界面背后的对象|GitHub 平台名词]] 或 [[#2. 核心名词，不懂的概念看这里|核心名词]]；这里主要认位置、按钮与用途。

### 4.1 Dashboard：个人首页（图 2）

学习阶梯：**L1 · 新手先学；Copilot 部分可暂时跳过**

![[GitHub界面-02-Dashboard.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| 左上 GitHub 猫图标 / Dashboard | 个人首页入口 | 回到登录后的总首页，不是打开某个本地项目 |
| `☰` 全局导航 | 展开账户的全站导航 | 找仓库、项目等入口 |
| Home / Feed | 首页概览 / 社区动态 | 一个看自己常用工作，一个看动态 |
| Top repositories | 常用仓库快捷列表 | 点 `Games101` 才进入那个仓库 |
| 顶部 `Type / to search` / 放大镜 | 全站搜索；列表旁放大镜用于相应范围 | 搜仓库 / 代码 / 内容，先看搜索范围 |
| 中央 Ask / 输入框 / `➤` | Copilot 提问与发送入口 | 向 AI 提问，不是提交代码 |
| Auto / Optimized for: Balance | 截图中的 AI 选择与偏好控件 | 不影响你当前 Git 分支；具体选项看账户界面 |
| All repositories / `+` | AI 的仓库上下文与添加上下文入口 | 告诉 AI 要看什么，不是给仓库加文件 |
| Debug / Agent / Create issue / Write code / Git | AI / 工作任务的快捷入口 | 是进入相应任务，不是按钮一按就保证完成 Git 操作 |
| Pull requests / Issues / View all | 汇总待处理 PR 与事项 | 看跨仓库的工作清单 |
| 右上 `+` / 收件箱 / 头像 | 创建入口 / 通知 / 账户菜单 | 是 GitHub 全站操作，不是 Stage / Commit |
| Preview / 右侧活动卡片 | 预览界面标记与活动宣传 | 可以先忽略，不属于 Git 基础知识 |

参考：[GitHub 个人首页](https://docs.github.com/en/account-and-profile/get-started/personal-dashboard-quickstart)。右上方未展开、没有 Tooltip 的细小图标，不凭轮廓猜具体名称，悬停确认即可。

### 4.2 仓库主页：导航栏、分支与 Code 菜单（图 1）

学习阶梯：**L1 · 新手先学**

![[GitHub界面-01-仓库与克隆.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| `kairn-z71 / Games101` | 仓库所有者 / 仓库名 | 谁的哪一个项目 |
| Public | 仓库公开可见 | 别人能看，不代表别人有权直接 Push |
| `<> Code` 标签 | 仓库文件与代码页面 | 回项目文件列表 |
| Issues / Pull requests | 问题事项 / 合并请求页面 | 一个记要做什么，一个审查准备合入的改动 |
| Agents / Actions | AI 代理任务 / 自动化工作流 | AI 帮做任务，与自动跑脚本是两回事 |
| Projects / Wiki | 任务规划看板 / 项目文档区 | 管计划，或写说明书；截图没有展开 Projects，不据此判断有没有项目 |
| Security and quality / Insights / Settings | 安全与质量 / 活动统计 / 仓库设置 | 查风险、看活动、改仓库配置 |
| Pin | 固定仓库相关入口，目标以点击后的说明为准 | 把仓库固定到界面提供的位置，不是 Git 提交 |
| Watch / Star / Fork | 订阅通知 / 收藏关注 / 在 GitHub 建立派生仓库 | Watch 不是实时同步，Star 不是下载，Fork 不是本地分支 |
| `main ▼` | 网页正在浏览的分支 | 网页切分支不会切换你电脑上的分支 |
| `2 Branches` / `0 Tags` | 截图时可查看的分支 / 标签数量 | 看远程仓库有哪些路线和版本标记 |
| Go to file | 在此仓库中快速查找文件 | 找某个文件，不是搜索你电脑硬盘 |
| Add file | 网页新建 / 上传文件入口 | 网页保存时会形成远程提交，本地仍需获取更新 |
| 绿色 `<> Code ▼` | 获取仓库 / 打开开发环境的菜单 | 注意它与上方 Code 标签不是同一个东西 |
| Local / Codespaces | 本地获取方式 / 云端开发环境入口 | 想用自己电脑就看 Local；Codespaces 不是普通下载 |
| HTTPS / SSH / GitHub CLI | 三种获取仓库地址或指令的方式 | 使用方式不同，不是三个不同项目 |
| HTTPS 地址 / 两个重叠方框 | 克隆地址 / 复制地址 | 复制后到 VS Code 的 Clone 粘贴 |
| Open in GitHub Copilot app / Desktop | 用对应应用打开 | 不是已经在 VS Code 中克隆成功 |
| Download ZIP | 下载所选分支的文件归档 | 没有完整 Git 版本管理历史，不等于 Clone |
| 文件列表中的提交说明 / 时间 | 路径最近相关提交的提示 | 不是“每个文件都有一条独立分支” |
| README / About / 齿轮 | 项目简介 / 仓库简介区 / 编辑相关信息 | README 是说明文件，不等于 Wiki |
| Releases / Packages / Contributors | 发布版本 / 软件包 / 贡献者 | Commit 成功不代表已经发布了 Release 或 Package |

参考：[克隆仓库](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)、[Projects 与任务](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/best-practices-for-projects)。

### 4.3 Issues：记录问题与任务（图 3）

学习阶梯：**L2 · 日常熟练；个人项目也可以用**

![[GitHub界面-03-Issues.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| New issue | 创建问题、需求或任务条目 | 先把问题记下来，不是修改源码或 Commit |
| `is:issue state:open` / 搜索 / `×` | 当前筛选条件 / 搜索 / 清空输入 | 只看未关闭 Issue；没结果先检查过滤条件 |
| Open / Closed | 未关闭 / 已关闭的事项 | “关闭”不是删除源码，也不等于一定有代码改动 |
| Assigned to me / Created by me / Mentioned | 分配给我 / 我创建的 / 提到我的 | 按自己与事项的关系筛选 |
| Recent activity / Views | 最近活动 / 保存或组织的查看入口 | 快速找到关心的事项 |
| Author / Labels / Assignees | 作者 / 分类标签 / 负责人 | 谁提的、属于哪类、谁来处理 |
| Projects / Milestones | 项目计划 / 里程碑 | 放进计划，并归到某个阶段目标 |
| Newest / 列表布局按钮 | 排序与显示方式 | 改的是列表视图，不是项目版本 |
| No results matched your search | 当前条件下没有匹配项 | 不证明仓库没有代码，也不证明从未有过 Issue |

参考：[GitHub Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/about-issues)。

### 4.4 Pull requests：审查与合并请求（图 4）

学习阶梯：**L3 · 团队协作**

![[GitHub界面-04-Pull-requests.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| New pull request | 选择要比较的分支并创建 PR | 提议把一条分支的改动合进另一条，不是直接执行本地 Pull |
| `is:pr state:open` | 只看未关闭 PR | 现在列表只显示等待处理的请求 |
| Open / Closed | 进行中 / 已关闭的 PR | Closed 可能是合并，也可能只是关闭；看具体结果 |
| Authored by me / Assigned to me | 我创建的 / 分配给我的 | 找自己需要跟进的请求 |
| Involves me / Review requests | 与我有关 / 请求我审查 | 找需要自己参与或审核的改动 |
| Author / Label / Projects / Milestones | 作者、标签、计划与里程碑筛选 | 按任务维度查 PR |
| Reviews / Assignee | 审查状态 / 负责人筛选 | 区分谁在跟进与谁来审核 |
| Newest / 布局按钮 | 排序与显示方式 | 只是换一种看列表的方式 |
| No pull requests matched your search | 当前条件没有匹配 PR | 不等于本地没提交；Push 也不会必然自动新建 PR |

创建后还要检查 **base（接收方）** 与 **compare（提供改动的一方）**，再看 Diff、检查结果与审查意见。概念见 [[#2.3.1 Pull Request：分支合并的请求|PR]]，完整双方法流程见 [[#9.4 一次正常任务：从分支到 PR|从分支到 PR]]。

### 4.5 Agents：AI 任务会话（图 5）

学习阶梯：**L3 · 团队协作；可选功能**

![[GitHub界面-05-Agents.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| Agents / Sessions | 仓库相关的代理任务与会话入口 | 看 AI 被交办了什么任务，不是 Git 分支列表 |
| My sessions / Needs attention | 我的会话 / 需要处理的会话 | 找自己的 AI 任务和待办 |
| `is:open author:@me` | 仅筛选自己创建的开放会话 | 别把筛选后为空理解成所有人都没有会话 |
| Active / Completed | 活跃 / 已完成的任务会话 | 完成任务不等于代码已审查并合并 |
| Status / Type / Agent / Newest | 状态、类型、代理与排序筛选 | 按任务状态找记录 |
| Configure | 相关代理配置入口 | 可能涉及账户、权限与用量，不是必须启用的 Git 基础设置 |
| No sessions match your filters | 当前筛选下没有会话 | 不影响你正常 Clone、Commit、Push |

参考：[GitHub 代理会话管理](https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/manage-and-track-agents)。AI 结果仍需人工检查，不能把会话完成当成审查通过。

### 4.6 Actions：自动执行工作流（图 6）

学习阶梯：**L3 · 团队协作；先会看运行结果**

![[GitHub界面-06-Actions.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| All workflows / Workflows | 工作流与运行记录的查看范围 | 看自动化脚本有没有运行、怎样运行 |
| New workflow | 添加自动化工作流配置入口 | 配测试、构建或部署，不是普通保存 / Commit 按钮 |
| Search runs | 搜索运行记录 | 找某一次自动执行 |
| Workflow / Event / Status / Branch / Actor | 按工作流、触发事件、结果、分支与触发者筛选 | 哪套流程、谁在什么分支触发、结果怎样 |
| Auto-refresh: 30s | 运行列表的自动刷新间隔 | 只刷新网页，不会每 30 秒 Pull 你电脑的项目 |
| Caches | 自动化任务的缓存管理 | 加速运行，不是 Git 历史备份 |
| Attestations | 构建产物的来源 / 完整性证明入口 | 看产物来自哪里，不是每次 Commit 的说明文字 |
| Runners | 执行任务的机器 / 环境管理 | 自动脚本在哪台机器跑 |
| Lockfile | 工作流依赖锁文件相关入口，用固定提交约束运行的依赖版本 | 不是本地 `.git/index.lock`；看见入口也不代表仓库已经启用，实际可用性以账户与配置为准 |
| Usage metrics / Performance metrics | 使用量 / 性能统计 | 看自动化成本与效率 |
| No workflows found / 0 workflow runs | 截图里未列出工作流，也没有运行记录 | 不等于 Push 失败，更不等于项目坏了 |

工作流配置通常位于 `.github/workflows/`；上传代码不会凭空创建测试流程。参考：[GitHub Actions 的组成](https://docs.github.com/en/actions/get-started/understand-github-actions)。 Lockfile 说明另见 [GitHub 官方工作流锁文件说明](https://github.blog/changelog/2026-10-14-github-actions-workflow-lockfiles-in-public-preview/)。

### 4.7 Wiki：独立的项目说明区（图 7）

学习阶梯：**L2 · 日常熟练；可选**

![[GitHub界面-07-Wiki.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| Wiki / 书本图标 | 项目的长篇说明文档区域 | 给项目写使用手册、原理或约定 |
| Welcome to the Games101 wiki! | 截图中尚未建立首页的欢迎画面 | 功能已能打开，但不表示已经有文档 |
| Create the first page | 创建 Wiki 第一页 | 开始写说明书，不会自动把 Obsidian 笔记复制进来 |

Wiki 与仓库文件列表中的 README 是不同位置；公开仓库的 Wiki 不会因限制编辑者就变成私密文档。参考：[GitHub Wiki](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis)。

### 4.8 Security and quality：安全功能状态（图 8）

学习阶梯：**L1 · 先识别密钥风险；具体安全配置为 L3**

![[GitHub界面-08-Security.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| Overview | 本仓库安全功能概览 | 看哪些保护已开、哪些待设置 |
| Security policy / Set up a security policy | 安全问题的报告约定 | 告诉别人发现漏洞该怎么联系，不是修复漏洞本身 |
| Security advisories / View security advisories | 安全公告与相关处理入口 | 管漏洞信息，不是普通 Issue 列表 |
| Private vulnerability reporting | 私密报告潜在漏洞的入口 | 避免把尚未修复的细节直接公开 |
| Dependabot / Vulnerabilities / alerts | 依赖组件漏洞相关检查与告警 | 你用的第三方库可能有风险 |
| Malware | 截图中的恶意软件发现项分类 | 与常规依赖漏洞分类区分；具体范围看提示 |
| Code scanning / Set up code scanning | 源码安全与编码问题扫描入口 | 自动检查一部分问题，不代表全自动证明安全 |
| Secret scanning / View detected secrets | 检测提交内容中的密钥等敏感凭据 | 查有没有把钥匙上传了，不是“帮你保管钥匙” |
| Enabled / Disabled / Needs setup | 已启用 / 未启用 / 尚需配置 | 是功能状态，不是“安全 / 不安全”的最终判决 |

截图中 Secret scanning 显示 Enabled，也不能说明绝对没有泄露；若已泄露，先撤销 / 轮换凭据。参考：[仓库安全入门](https://docs.github.com/en/code-security/getting-started/quickstart-for-securing-your-repository)、[密钥扫描](https://docs.github.com/en/code-security/concepts/secret-security/secret-scanning)。

### 4.9 Insights：活动与统计（图 9）

学习阶梯：**L2 · 日常熟练；统计按需看**

![[GitHub界面-09-Insights.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| Pulse / Period: 1 week | 指定时间范围内的仓库活动摘要 | 看这一周发生了什么，不是全仓库历史总量 |
| Active / Merged / Open pull requests | 相关 PR 的活动与状态计数 | 看请求处理情况，不是本地待提交文件数 |
| Active / Closed / New issues | 相关事项的活动与状态计数 | 看任务情况，不是编译错误数量 |
| Summary / main / all branches | 按页面统计口径区分主分支与全部分支的活动 | main 与别的分支不一定同步；别混着读数字 |
| Top committers / Contributors | 提交活动排行 / 贡献者统计 | 用来看活动，不能只凭次数评判贡献质量 |
| Community / Community standards | 社区信息与项目规范情况 | 看项目协作资料是否完善 |
| Traffic | 访问与克隆等流量统计入口 | 看别人怎样访问仓库，不是你本地网络监控 |
| Commits / Code frequency | 提交与代码变化频率 | 看变化趋势，不是直接恢复某个版本 |
| Dependency graph | 依赖关系图 | 看项目依赖什么，不是 Git 分支图 |
| Network / Forks | 仓库历史连接与派生仓库关系 | Fork 关系不等于当前工作分支 |
| Actions usage / performance metrics | 自动化使用量与性能统计 | 查看工作流运行层面的情况 |

截图中的 `0 files changed` 只能按该页面的时间、分支与统计口径理解，不能据此断言仓库没有内容或提交没生效。参考：[仓库活动与数据](https://docs.github.com/en/repositories/viewing-activity-and-data-for-your-repository)。

### 4.10 Settings：仓库配置（图 10、11）

学习阶梯：**L1 · 认识位置；L3 · 修改权限、规则与自动化配置**

#### 4.10.1 General 与左侧设置入口（图 10）

学习阶梯：**L2–L3 · 先看说明，修改前确认影响**

![[GitHub界面-10-Settings-General.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| General / Repository name / Rename | 仓库通用设置与重命名 | 改远程仓库名，不是给本地文件夹改名 |
| Template repository | 允许别人据此生成新仓库的模板选项 | 复用结构，不等于建立持续同步的 Fork |
| Default branch / `main` / 铅笔与切换按钮 | 默认分支名称及相关修改入口；具体动作看 Tooltip | 默认进入哪条路线；不会替你切换电脑上的分支 |
| Releases / Enable release immutability | 为后续发布启用不可变保护 | 已发布的受保护附件与标签不能随便改，不是把全部源码冻结 |
| Social preview / Edit | 分享仓库链接时的预览图片 | 不是 README 正文，也不是提交者头像 |
| Collaborators / Moderation | 协作者权限 / 互动管理 | 谁能参与，与仅公开可读不同 |
| Rulesets / Branches / Tags | 分支、标签和推送等规则入口 | 配主线保护与版本约定，不是创建本地分支 |
| Actions / Webhooks | 自动化设置 / 事件通知到外部系统 | 管服务如何响应事件，不是手动 Push 本身 |
| Copilot / Planning | AI 与计划功能相关设置 | 按账户能力和团队需要配置 |
| Environments / Codespaces / Pages | 部署环境 / 云端开发 / 网站发布 | 三种用途不同；Pages 不是把整个仓库设为私有或公开 |
| Advanced Security / Deploy keys | 高级安全 / 仓库部署密钥 | 可能涉及计划与权限；不要随便发放机器访问能力 |

参考：[仓库规则](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository)、[Release 不可变保护](https://docs.github.com/en/code-security/how-tos/secure-your-supply-chain/establish-provenance-and-integrity/prevent-release-changes)。

#### 4.10.2 Features、Secrets 与集成（图 11）

学习阶梯：**L2–L3 · 按项目需要配置**

![[GitHub界面-11-Settings-Features.webp|1000]]

| 图标 / 英文名称 | 含义 | 大白话 |
| --- | --- | --- |
| Wikis 复选框 | 是否启用仓库 Wiki | 要不要有单独的项目说明区 |
| Restrict editing to collaborators only | 限制 Wiki 的编辑者 | 限制“谁能改”，不是限制公开 Wiki “谁能看” |
| Issues 复选框 | 是否启用问题跟踪 | 要不要给项目开事项列表 |
| Issue permissions / Creation allowed by: All users | 截图中的 Issue 创建权限 | 允许发问题，不等于允许直接推代码 |
| Set up templates | 配置 Issue 模板入口 | 让提 Bug / 提需求的人按格式填写 |
| Sponsorships | 赞助入口相关选项 | 项目支持渠道，不是给协作者授权 |
| Secrets and variables | 自动化等功能使用的机密与变量设置 | 不要把真实密钥写进普通仓库文件来代替 |
| GitHub Apps | 仓库的应用集成设置 | 外部应用可能申请权限，安装前看清范围 |
| Deploy keys | 为机器访问配置仓库密钥的入口 | 跟公开发布公钥 / 保存私钥的边界要分清 |

参考：[Wiki 访问边界](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis)、[GitHub 机密类型](https://docs.github.com/en/code-security/reference/secret-security/secret-types)。

> [!summary]
> **先记这条网页路线**
>
> 找仓库 → Code 看文件 / 复制 Clone 地址 → VS Code 修改、暂存、提交、推送 → GitHub 切到目标分支核对 → 需要合入主线时开 PR。Issues、Actions、Agents、Wiki 各管不同事情，不是这条流程中的同义按钮。

## 5. 首次配置与创建仓库：先用 VS Code

学习阶梯：**L1 · 新手先学**
### 5.1 安装、身份与认证

学习阶梯：**L1 · 新手先学**

安装 [Git](https://git-scm.com/downloads) 和 VS Code，打开项目后点击左侧 **Source Control** 图标；可通过 `… → Show Git Output` 查看 Git 检测与报错，再按提示完成 GitHub 浏览器授权。

首次设置 Git 的姓名、邮箱仍可能需要终端；没有统一的内置图标可代替。最小命令集中放在 [[#8.1 首次终端准备：安装检查、身份与克隆|首次终端准备]]，这里先认识操作入口。

姓名、邮箱会记入提交，它们**不是 GitHub 登录账号或密码**。在已有配置的电脑上不要无意覆盖。参考：[VS Code 配置教程](https://code.visualstudio.com/docs/sourcecontrol/quickstart)。

认证与提交身份分开处理：新手可以先使用 HTTPS，并按 VS Code 提示在浏览器授权。GitHub 的 Git HTTPS 认证不再接受账户密码；命令行可使用凭据管理器或令牌，SSH 则使用密钥。**不要把 Token、私钥写进笔记或仓库。**参考：[GitHub 认证方式](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)。

### 5.2 两种起点：克隆或发布

学习阶梯：**L1 · 新手先学**

#### 5.2.1 GitHub 上已有项目：Clone（克隆）

学习阶梯：**L1 · 新手先学**

1. 在 GitHub 仓库的 Code 菜单复制 HTTPS 地址。
2. VS Code 按 `Ctrl+Shift+P`，运行 `Git: Clone`。
3. 粘贴地址，选本地保存位置，再打开克隆后的项目文件夹。
	如下👇
![[Git Clone 2.png]]
![[Git Clone 1.png]]
![[Git Clone 3.png]]


[[#2.9 团队与命令行辅助名词|Clone]] 的概念见 [[#2.9 团队与命令行辅助名词|Clone：克隆仓库]]；不是普通下载 ZIP。登录也不会自动获得别人的仓库写权限。参考：[VSCode：GitHub 工作流](https://code.visualstudio.com/docs/sourcecontrol/github)。

#### 5.2.2 只有本地新项目：Initialize，再 Publish

学习阶梯：**L1 · 新手先学**

仅用于尚未初始化的新项目；练习时使用现有仓库之外的新文件夹。

1. 打开项目文件夹，先配置适合项目的 [[#2.5 .gitignore：忽略规则文件|.gitignore]]。
2. Vscode左侧边栏，点Git图标（源代码管理），选择 [[#2.9 团队与命令行辅助名词|Initialize Repository]]。
3. 检查文件、暂存并创建第一次提交。
4. 选择 [[#2.9 团队与命令行辅助名词|Publish to GitHub]]，确认仓库名称及 [[#2.9 团队与命令行辅助名词|Public]] / [[#2.9 团队与命令行辅助名词|Private]]。
	2-4的流程参考👉  [B站参考视频  11：06 - 21：05](https://www.bilibili.com/video/BV1Hkr7YYEh8/?spm_id_from=333.337.search-card.all.click&vd_source=ee3d43488dfeebc9a4aa0ee79c101cae)

- 只运行 `git init` 不会在 GitHub 上创建仓库。
	[[#2.4 .git：本地仓库的管理数据|.git 与 git init 原理]] 
- Publish 才会建立远程并上传。若选择手动关联远程，应先在 GitHub 创建**空仓库**，不要同时初始化另一套 README 历史。（这里我们不考虑手动关联远程，我们是通过Vscode自动关联的） 参考：[仓库的创建、克隆与发布](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes)。

## 6. VS Code 日常操作流程

学习阶梯：**L1 · 新手先学；本节只走图形流程**

### 6.1 推荐的日常操作流程

学习阶梯：**L1 · 新手先学**

#### 6.1.1 开始前：确认与更新

学习阶梯：**L1 · 新手先学**

假设你和同事共用一个 GitHub [[#2.3 仓库、分支与远程名词|Repository]]：

1. **确认仓库和分支**：检查左下角分支名，不要把试验改动直接做在主分支。
2. **开始工作前更新**：先 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]]，查看远程变化(别人在Github上干啥了)；工作区干净且确认需要整合时再 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]]。
3. **修改并保存到你的电脑硬盘里**：`Ctrl+S`。

#### 6.1.2 修改后：检查、暂存、提交与推送

学习阶梯：**L1 · 新手先学**


写完本次代码后，按下面顺序处理：

1. **查看差异**：打开左侧边栏的[[#2.9 团队与命令行辅助名词|Source Control]]，点文件检查 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]（就是[[#2.7 Changes、文件状态与 Graph|changes]]，代码的改动）；排除误删、凭据和无关改动。
2. **选择[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|stage]]暂存范围**：悬停文件点 `+`；文件内只想暂存一部分改动的话，可在 Diff 中按块或选定行暂存。
	补充：文件旁的 `−` 会取消该文件的暂存；在暂存 Diff 中，也可按选定行 / 块取消暂存。不要把 Unstage 与 Discard 混淆。
3. **检查 [[#2.7 Changes、文件状态与 Graph|Staged Changes]]**：这里才是下一次提交准备记录的内容。
4. **填写[[#2.9 团队与命令行辅助名词|message]]并 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]]**：message就是起个名字，能看懂这次commit干了什么就行。
5. **[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] / [[#2.1.1 Publish Branch 和 Push 的区别|Publish Branch]]**：将commit发送到对应远程分支，就是发到Github上了

操作依据：[暂存与提交](https://code.visualstudio.com/docs/sourcecontrol/staging-commits)、[远程同步](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes)。本文建议把不同目的拆成小提交，例如笔记内容修改和插件状态更新分别处理。

> [!tip]
> 如果写完代码后，根本没有管changes有没有stage，直接点了commit会怎么样？
> 
> 这取决于 Git / VS Code 设置：可能提示先暂存，也可能使用智能提交。不要假定一定只提交你想要的部分；新手应先点 `+`，检查 Staged Changes，再点 Commit。


[[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 后再看图，比反复点击 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Sync]] 更容易弄清发生了什么；图中的远程状态可能只是上一次获取的结果。依据：[VS Code 远程操作](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes)、[Git Pull](https://git-scm.com/docs/git-pull)、[Git Push](https://git-scm.com/docs/git-push)。


图形流程完成后，再到 [[#8. 日常命令行与 PowerShell 实录|命令行对照]] 学同一套操作，不必在入门流程中途背命令。

## 7. GitLens 插件（可选）

学习阶梯：**L2 · 日常熟练；可选扩展，不是入门前提**

### 7.1 它与内置 Git、GitHub 插件有什么区别？

学习阶梯：**L2 · 日常熟练**

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| VS Code 内置 Git | 查看修改、暂存、提交、推送、分支、冲突处理；本身也提供提交图、Timeline 和 [[#2.8.4 Log、Blame 与 Bisect\|Blame]] | 日常 Git 操作的基础工具 |
| GitHub [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Pull]] Requests and Issues | 在编辑器里创建、审查 [[#2.3 仓库、分支与远程名词\|PR]] 和管理 [[#2.9 团队与命令行辅助名词\|Issue]] | 在 VS Code 里处理 GitHub 的 PR 和 Issue |
| GitLens | 提供更丰富的行级追踪、历史比较、仓库导航及进阶可视化工作流 | 在基础 Git 之上，更方便地追踪历史 |

**不安装 GitLens 也能完整完成基本的 Git 提交与同步。** 安装 GitLens 也不等于安装了 Git，仍需要本机 Git。参考：[VS Code 内置功能](https://code.visualstudio.com/docs/sourcecontrol/overview)、[GitHub 集成](https://code.visualstudio.com/docs/sourcecontrol/github)、[GitLens 仓库](https://github.com/gitkraken/vscode-gitlens)。

### 7.2 安装与优先学习的功能

学习阶梯：**L2 · 日常熟练**

在扩展面板 `Ctrl+Shift+X` 搜索 **GitLens**，确认发布者是 **GitKraken**；扩展标识为 `eamodio.gitlens`。[官方扩展页面](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

先用这三类功能，不必一上来研究所有侧栏：

1. **[[#2.8.4 Log、Blame 与 Bisect|Blame]] 与悬浮信息**：光标放在某行，查看最后一次修改涉及的作者、时间、提交；继续打开 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]，理解当时改了什么。
2. **File / Line [[#2.8.4 Log、Blame 与 Bisect|History]]**：追踪整个文件或某一行的历史，寻找内容在哪次提交改变。
3. **版本比较与导航**：比较上一个版本、当前工作文件或其他提交，而不是依赖手工保存“最终版2”。

Blame 回答的是“哪次提交最后改了这一行”，不等于业务责任判断，也不能仅凭它确定最初作者。功能参考：[GitLens 官方 README](https://github.com/gitkraken/vscode-gitlens)。

### 7.3 GitLens Commit Graph

学习阶梯：**L2 · 日常熟练**

`Ctrl+Shift+P` 搜索 `GitLens: Show Commit Graph`。阅读顺序建议：

1. 找当前分支及 [[#2.3 仓库、分支与远程名词|HEAD]]。
2. 找它对应的 `origin/分支名`，先 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 再判断领先 / 落后。
3. 点具体提交，看文件和 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]。
4. 需要操作时才使用右键菜单；**查看提交不等于切换到该提交**。

它与源代码管理面板内置的 [[#2.7.2 Graph：提交历史与分支位置|Graph]] 不是同一个入口。可先用内置 Graph 满足基本需求，再决定是否需要 GitLens 的更多交互功能。参考：[GitLens Commit Graph](https://help.gitkraken.com/gitlens/gitlens-features/)、[VS Code 历史图](https://code.visualstudio.com/docs/sourcecontrol/history)。

### 7.4 截图中的两个 AI 入口

学习阶梯：**L3 · 团队协作**

**Generate [[#2.9 团队与命令行辅助名词|Commit Message]] with GitLens：生成说明。**先选择并暂存本次变更，再生成提交说明；手动检查是否准确，不要让说明声称做了实际没有做的测试或修复。它与“创建提交”“推送”是不同动作。

**Compose Commits...：组织提交。**适合一次改动混杂多个任务时，把变更组织成多个逻辑提交；不仅仅是写一条说明。不同版本的入口和确认流程有所变化，新版也可在 [[#2.7.2 Graph：提交历史与分支位置|Commit Graph]] 的详情面板中使用 Compose。应用前必须检查分组、每个 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 和提交说明；涉及重新组织既有提交时，只在理解改写历史影响后使用。参考：[GitLens 功能说明](https://help.gitkraken.com/gitlens/gitlens-features/)、[当前版本更新记录](https://help.gitkraken.com/gitlens/gitlens-release-notes-current/)。

> [!warning]
> **AI 不是提交审核员**
>
> AI 功能会按所选提供商处理变更内容；使用前核对账户、权限、提供商和数据政策，不要默认私有仓库内容始终只在本机处理。对于截图中的 7 项修改，本文更建议先手工按任务选文件，而不是直接让 AI 全部组织并提交。

### 7.5 免费、Pro 与账户要求

学习阶梯：**L2 · 日常熟练**

- **Community 的基础能力**包括 [[#2.8.4 Log、Blame 与 Bisect|Blame]]、悬浮信息、CodeLens 和历史导航，可先用这些功能学习。
- **部分可视化能力与仓库类型有关**：官方说明对公开、本地仓库提供部分免费能力，私有远程仓库上的相关高级能力需要 Pro / 试用。
- **AI、Compose 及部分协作工作流**涉及 Pro 或更高计划及相应账户要求；不能因安装成功就认定全部免费。
- 本次核对发现，官方 README 与帮助页对 [[#2.7.2 Graph：提交历史与分支位置|Commit Graph]] 是否需要免费账户的说法存在差异，因此不要把“永远免登录”或“所有仓库都免费”当作固定结论。以已安装版本提示、[Community / Pro 对比](https://help.gitkraken.com/gitlens/gitlens-community-vs-gitlens-pro/)、[具体功能说明](https://help.gitkraken.com/gitlens/gitlens-features/) 和 [README](https://github.com/gitkraken/vscode-gitlens) 为准。

建议：**先用内置 Git 完成日常提交，用 Community 追历史；真正需要某项高级能力时再评估付费。**不必为了基础 Git 操作购买 Pro。

### 7.6 信息太多时，减少界面干扰

学习阶梯：**L2 · 日常熟练**

在设置中搜索对应配置；下面只是可选示例，**并未修改当前 VS Code 配置**：

```json
{
  "gitlens.currentLine.enabled": true,
  "gitlens.codeLens.enabled": false
}
```

保留当前行提示，关闭文件 / 代码块上方的 GitLens CodeLens。若同时启用了 VS Code 原生 [[#2.8.4 Log、Blame 与 Bisect|Blame]] 和 GitLens Blame，可以按偏好关闭一方，避免重复。参考：[GitLens 设置参考](https://help.gitkraken.com/gitlens/gitlens-settings/)、[VS Code Blame 设置](https://code.visualstudio.com/docs/sourcecontrol/history)。

## 8. 日常命令行与 PowerShell 实录

学习阶梯：**L2 · 日常熟练；先完成第 5～6 节的图形流程**

> [!important]
> **两种方法是对照学习，不是顺序执行两次**
>
> 每个场景先看 VS Code 图标步骤，再看命令行。对真实的一次操作通常二选一；练习两种方法时用独立练习仓库或重新准备初始状态。尤其 Commit、Cherry-pick、Reset、Revert 不要重复执行。
> 命令面板中的 `Git: ...` 是 VS Code 的图形命令入口，不是让你在 PowerShell 输入的命令。菜单名称受版本、语言和扩展影响；没有对应按钮时会明确写“需要终端”。

### 8.1 首次终端准备：安装检查、身份与克隆

学习阶梯：**L1–L2 · 初次署名配置可能必须做；克隆也可直接用图形方式**

#### 8.1.1 检查 Git 与配置提交身份

学习阶梯：**L1 · 首次使用时配置，已有配置先检查**

**方法 A｜VS Code 入口与必要的终端例外**

1. 打开 Source Control，查看是否识别本机 Git；出错时选 `… → Show Git Output`。
2. 点击账户图标完成 GitHub 浏览器授权，但这不等于设置提交姓名、邮箱。
3. 内置 Git 没有统一的“修改提交署名”图标。首次提示需要姓名 / 邮箱时，打开 `Terminal → New Terminal` 做下面的最小配置；不要覆盖已有工作身份。

**方法 B｜对应命令行**

```powershell
git --version
git config --global user.name "你的名字"
git config --global user.email "你的提交邮箱"
```

这里保留原笔记的全局配置示例；只改当前项目时使用 `--local`，并先查看配置来源，见 [[#9.3 操作前的“体检”：我在哪，改了什么？|仓库身份检查]]。GitHub 登录凭据与提交署名分开管理。

#### 8.1.2 克隆已有仓库

学习阶梯：**L2 · 与图形克隆二选一**

**方法 A｜VS Code 图标步骤**

GitHub 绿色 Code → 复制 HTTPS 地址 → VS Code Source Control 的 Clone Repository，或 `Ctrl+Shift+P → Git: Clone` → 选择保存目录 → 打开项目。截图见 [[#5.2.1 GitHub 上已有项目：Clone（克隆）|首次克隆]]。

**方法 B｜对应命令行**

```powershell
# 示例：替换账户名和仓库名；在准备存放项目的父文件夹中运行
git clone https://github.com/OWNER/REPO.git
cd REPO

```

`cd REPO` 只是让终端进入克隆后的目录，不负责克隆或登录；目标父文件夹要自行选择。

#### 8.1.3 初始化本地新项目与发布的区别

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

Source Control → Initialize Repository → 配好 `.gitignore` → 选文件 `+` → 检查 Staged Changes → Commit → Publish to GitHub，确认名称与 Public / Private。完整图形流程见 [[#5.2.2 只有本地新项目：Initialize，再 Publish|初始化与发布]]。

**方法 B｜只对应本地初始化部分的命令**

```powershell
# 仅在尚未初始化的新练习项目目录中运行
git init
# 配好 .gitignore，创建 README 等项目文件后，按实际需要暂存
git add -- ".gitignore" "README.md"
git diff --staged
git commit -m "初始化项目"
```

上面不会创建 GitHub 远程仓库。发布仍可回 VS Code 点击 Publish to GitHub；若选纯手动方式，需要先在 GitHub 建空仓库，再明确关联远程，不能把 `git init` 当作上传命令。

### 8.2 PowerShell 日常命令流程

学习阶梯：**L2 · 日常熟练**

**方法 A｜先在 VS Code 中操作或检查**

1. 点击 Source Control，核对左下角分支与 Changes / Staged Changes。
2. 点 Graph 的 Fetch，读 Incoming / Outgoing；需要更新且确认可安全整合时才点 Pull。
3. 修改后保存，点文件看 Diff；点指定文件的 `+`，再点 Staged Changes 复查。
4. 填说明 → Commit → Push；首次分支发布用 Publish Branch。完整图形流程见第 6 节。

以下命令是同一流程的另一种做法；如果已用按钮完成，不要再重复提交。

**方法 B｜对应命令行**

```powershell
git status
# 看当前分支、工作区和暂存区状态

git fetch
# 获取远程最新提交信息，但不直接改当前工作区

git status
# 看本地分支是否落后/领先远程分支

git pull
# 如果远程有你本地没有的提交，把它拉下来并整合进当前分支

git diff
# 查看工作区相对暂存区的改动

git add -- "Git + Github + Vscode管理.md"
# 只暂存指定文件

git diff --staged
# 提交前复查：看看下一次 Commit 到底会提交什么

git commit -m "整理 Git 与 VS Code 工作流"
# 创建本地 Commit

git status
# 检查是否出现 ahead of origin/... by N commits

git push
# 把本地新增 Commit 推送到远程对应分支
```

### 8.3 PowerShell 模拟实录：逐步读懂终端

学习阶梯：**L2 · 日常熟练**

> [!important]
> **模拟前提**
> 
> 演示仓库为 `D:\Demo\git-notes`，当前分支为 `ai-polished` ，并且已经关联到Github上了。
> 开始时工作区干净。同事刚在远程提交了 README 的一行更新，而我们本地尚未 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]]。本例没有分叉或冲突，[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] 可以快进；Pull 完成后，你再编辑并保存笔记。
> 

**怎样读终端：**`PS D:\Demo\git-notes>` 是 PowerShell 提示符，只输入后面的命令，不要一起复制提示符或输出。下方省略部分传输进度和 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 元数据，中文文件名按易读形式展示。

#### 8.3.1 第 1 步：git status——查看开始时的状态

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

打开 Source Control（`Ctrl+Shift+G`），看左下角分支、Changes 和 Staged Changes；空列表不代表远程一定没有新提交。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git status
On branch ai-polished
Your branch is up to date with 'origin/ai-polished'.

nothing to commit, working tree clean
```

“up to date”的意思是，已经和Github同步到最新的状态。**但是电脑是错误的**，它只是根据本地已知的远程信息得出的判断：**还没 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]]，所以它不知道同事刚推送了新提交。** 

#### 8.3.2 第 2 步：git fetch——更新对远程的认识

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

点 Graph 工具栏的 Fetch（图中 ⑩ 为获取全部远程）；不要把 Refresh 当 Fetch。当前文件不会仅因 Fetch 自动更新。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git fetch
From https://github.com/OWNER/git-notes
   a1b2c3d..b2c3d4e  ai-polished -> origin/ai-polished
```

本地记录的 `origin/ai-polished` 从 `a1b2c3d` 更新到 `b2c3d4e`。**当前本地分支和工作文件还没有跟着更新**，只是远程的新提交已经获取到本地。

[[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 的原理统一见 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch 与同步]]；关于 [[#2.4 .git：本地仓库的管理数据|.git]] 不被整体覆盖、C1 / C2 分叉的问题，也在该节集中解释。

#### 8.3.3 第 3 步：再次 git status——发现本地落后

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

Fetch 后看 Graph 的 Incoming Changes / `↓` 数字与远程分支位置；它与“工作区干净”是两种信息。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git status
On branch ai-polished
Your branch is behind 'origin/ai-polished' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
```

现在明确知道：远程比本地多一次提交，而且可以快进（没有合并的操作，Pull可以一键到位）。`working tree clean` 说明没有未提交改动，不表示本地分支已经跟上远程。

#### 8.3.4 第 4 步：git pull——把远程提交整合进当前分支

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

确认工作区干净、目标分支正确且符合整合规则，再点 Graph 的 Pull ↓ 或 `… → Pull`。需要严格 ff-only 时用下面的显式命令，不把普通按钮当作相同保证。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git pull
Updating a1b2c3d..b2c3d4e
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

本地 `ai-polished` 快进到 `b2c3d4e`，工作区里的 README 也更新了。[[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 是“先获取远程信息”，[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] 则会再次获取并进行整合；因此前面 Fetch 过，再 Pull 并不矛盾。

这时才开始自己的修改：在 VS Code 打开笔记，新增下面演示的内容，按 `Ctrl+S` 保存。保存后再执行下一条命令；如果没有编辑，下一步 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 可能没有输出。

> [!warning]
> **Pull 不是每次必跑的固定动作**
>
> 如果没有远程新提交，可以跳过；如果本地和远程已经分叉，或工作区有需要保留的改动，先停下检查，再按团队规则处理。裸 `git pull` 的整合方式受配置影响，本例仅演示可快进的情况，不代表所有仓库都会得到同样结果。

#### 8.3.5 第 5 步：git diff——检查自己刚刚保存的修改

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

点 Changes 中的指定文件，打开 Diff；这里看未暂存编辑，不是刚拉取下来的已提交内容。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git diff
diff --git a/Git + Github + Vscode管理.md b/Git + Github + Vscode管理.md
--- a/Git + Github + Vscode管理.md
+++ b/Git + Github + Vscode管理.md
@@ -1,3 +1,5 @@
 # Git + GitHub + VS Code 管理代码
 
 日常流程：检查 → 暂存 → 提交 → 推送。
+
+注意：Commit 只写入本地历史，Push 才会发送到远程。
```

正文行前的 `+` 表示新增，这里模拟新增两行。**这次 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 展示的是你尚未暂存的修改，不是刚才 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] 下来的 README 更新**：README 已经属于当前提交，没有再被你编辑。若进入分页界面，按 `q` 返回终端。

#### 8.3.6 第 6 步：git add——只暂存指定笔记

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

悬停 Changes 中的目标文件，点 `+`；只选一部分时，在 Diff 选行 / 块后暂存。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git add -- "Git + Github + Vscode管理.md"
PS D:\Demo\git-notes>
```

成功时通常没有输出。当前文件内容已经选入暂存区，**还没有创建 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]]，也没有上传**。如果此后继续修改文件，需要再次 Add 才会把后来的修改也选进去。

#### 8.3.7 第 7 步：git diff --staged——复查即将Commit的内容

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

点 Staged Changes 中的文件，核对将要提交的 Diff；不要只看 Changes。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git diff --staged
```

此时会再次显示第 5 步中的新增两行，两次查看的对象不同：

- 第 5 步的 `git diff`：我还有哪些change没 Stage ？
- 这里的 `git diff --staged`：我已经 staged 的 change 有哪些？我要commit了。

#### 8.3.8 第 8 步：git commit——创建本地提交

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

在提交说明框写清本次修改，点击 Commit ✓；看暂存条目是否消失、Graph 是否多了本地提交。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git commit -m "整理 Git 与 VS Code 工作流"
[ai-polished e4f5a6b] 整理 Git 与 VS Code 工作流
 1 file changed, 2 insertions(+)
```

`e4f5a6b` 是模拟的新提交短哈希，父提交是刚才接入的 `b2c3d4e`。这条 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]] 已写入本地历史，**此时 GitHub 还没有收到它**。

#### 8.3.9 第 9 步：git status——确认本地出现待推送提交

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

检查 Graph 的 Outgoing Changes / `↑` 数字；Changes 为空也不代表已经上传。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git status
On branch ai-polished
Your branch is ahead of 'origin/ai-polished' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- `ahead ... by 1 commit`：本地比上游Github多一次提交，对应界面的 [[#2.7 Changes、文件状态与 Graph|Outgoing Changes]]。
- `working tree clean`：本例中所有文件改动都已处理，没有剩余修改，**不表示已经上传**。
- 如果还有没选入这次提交的其他文件，它们仍会留在工作区，本例的“clean”就不一定出现。

#### 8.3.10 第 10 步：git push——把本地新提交推送到对应远程分支

学习阶梯：**L2 · 日常熟练**

**方法 A｜VS Code 图标步骤**

点 Push ↑；若当前分支尚未发布，用 Publish Branch。成功后去 GitHub 切到同名分支核对提交。

**方法 B｜对应终端命令与模拟输出**

```text
PS D:\Demo\git-notes> git push
To https://github.com/OWNER/git-notes.git
   b2c3d4e..e4f5a6b  ai-polished -> ai-polished
```

远程 `ai-polished` 从 `b2c3d4e` 更新到 `e4f5a6b`。去 GitHub 切到这条分支，即可检查“整理 Git 与 VS Code 工作流”这次提交；**[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] 不会自动把功能分支合入 [[#2.3 仓库、分支与远程名词|main]]**。

需要再验证时，可额外执行一次 `git status`：本例中应显示与上游一致、工作区干净。若 Push 遇到认证失败、权限不足或远程又有新提交，先检查原因，不要为了套用成功示例而直接强推。

以上输出为模拟场景；命令语义参考：[Git Fetch](https://git-scm.com/docs/git-fetch)、[Git Pull](https://git-scm.com/docs/git-pull)、[Git Status](https://git-scm.com/docs/git-status)、[Git Diff](https://git-scm.com/docs/git-diff)、[Git Commit](https://git-scm.com/docs/git-commit)、[Git Push](https://git-scm.com/docs/git-push)。

## 9. 团队协作：先界面，后命令

学习阶梯：**L2–L4 · 每个场景先界面，后看精确命令**

> [!abstract]
> **目标不是背命令，而是能独立处理工作**
>
> “大厂可工作的 Git 水平”没有统一命令清单。本文把目标定为：**能独立完成分支开发和代码审查，解释历史变化，处理冲突与推送拒绝，安全回滚并找回误操作前的提交。**入职后仍需遵守团队的分支、审查、[[#2.9 团队与命令行辅助名词|CI]]、权限及发布规范。
> 两种方法对照学习，一次真实操作通常二选一，不要重复提交、重置或移植相同改动。
> 前文“日常操作大多能用 UI”不等于“命令行不重要”：许多进阶操作也有 UI；掌握命令行，是为了在任何编辑器、远程终端和故障现场都能明确控制操作，而不是盲点按钮。

### 9.1 学习分层，以及 UI / 命令行怎样分工

学习阶梯：**L2 · 日常熟练**

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| A：日常必会 | `status`、[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|diff]]、`add`、[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|commit]]、[[#2.8.4 Log、Blame 与 Bisect\|log]]、`switch`、[[#2.3 仓库、分支与远程名词\|branch]]、[[#2.6 Fetch、Pull、Push 与 Sync Changes\|fetch]]、[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|push]] | 不依赖按钮，也能完成一次小任务 |
| B：协作必会 | [[#2.8.1 整合与提交整理\|merge]]、[[#2.8.1 整合与提交整理\|rebase]]、[[#2.8.2 Stash 与 Worktree\|stash]]、[[#2.8.1 整合与提交整理\|cherry-pick]]、[[#2.8.3 Restore、Reset、Revert 与 Reflog\|restore]]、[[#2.8.3 Restore、Reset、Revert 与 Reflog\|revert]]，冲突的 [[#2.8.1 整合与提交整理\|Continue]] / [[#2.8.1 整合与提交整理\|Abort]] | 知道何时使用、会改变什么，不伤害共享历史 |
| C：恢复与排错 | [[#2.8.3 Restore、Reset、Revert 与 Reflog\|reflog]]、[[#2.8.3 Restore、Reset、Revert 与 Reflog\|reset]] 的区别、提交范围、[[#2.8.4 Log、Blame 与 Bisect\|blame]]、[[#2.8.4 Log、Blame 与 Bisect\|bisect]]、[[#2.8.2 Stash 与 Worktree\|worktree]] | 能定位问题，先保护现场再恢复 |
| D：按项目需要 | [[#2.9 团队与命令行辅助名词\|Tag]]、[[#2.9 团队与命令行辅助名词\|Submodule]]、[[#2.9 团队与命令行辅助名词\|Git LFS]]、签名、[[#2.9 团队与命令行辅助名词\|Hooks]]、[[#2.9 团队与命令行辅助名词\|CI]] 约束 | 查团队规范及官方文档，不要求一开始全部背熟 |

**推荐组合：**用 VS Code 看 Diff、按行暂存、编辑冲突；用命令行检查状态、精确选择比较范围、执行明确参数的历史操作；用 GitHub / 团队平台完成 [[#2.3 仓库、分支与远程名词|PR]]、审查与 CI 检查。以上是本文的工作方法建议，不是公司的统一标准。

### 9.2 先看懂命令的写法

学习阶梯：**L2 · 日常熟练**

- 下面均在**目标仓库根目录**的终端运行；`src/login.ts`、`feature/login` 都是示例，需要替换。
- `COMMIT_ID`、`OLD_TIP`、`GOOD_COMMIT` 等代表真实提交哈希，**不是可以原样执行的名字**。文中避免用尖括号占位，以免与 PowerShell 语法混淆。
- `-- "文件路径"` 用于分隔选项 / 版本与文件路径；路径带空格时加引号。
- [[#2.3 仓库、分支与远程名词|HEAD]] 是当前提交，`HEAD~1` 沿第一父提交向前一步；`HEAD~3` 是三步。合并提交存在多个父提交，`HEAD^2` 表示第二父提交。
- PowerShell 中给 `"@{upstream}"`、`"stash@{0}"`、`"HEAD@{1}"` 这类带大括号的 Git 引用加引号。下文用 `"@{upstream}"` 指当前分支的上游；未设置时会报错。
- `git log` 等若进入分页界面，按 `q` 退出。命令不熟时用 `git 命令 -h` 或 `git help 命令` 查帮助；不要把整段含多个可选方案的代码一次全运行。

参考：[Git 修订引用语法](https://git-scm.com/docs/gitrevisions)、[Git 命令入口](https://git-scm.com/docs/git)。

### 9.3 操作前的“体检”：我在哪，改了什么？

学习阶梯：**L2 · 日常熟练**

**方法 A｜先在 VS Code 中操作或检查**

1. 打开 Source Control，核对左下角分支与当前仓库；多仓库窗口不要选错。
2. 点 Changes 文件看未暂存 Diff，点 Staged Changes 看提交范围；新文件也要打开检查。
3. 打开 Graph，看 HEAD、上游与 Incoming / Outgoing；远程信息先 Fetch 再判断。
4. 用 `… → Show Git Output` 看实际 Git 调用与报错。精确列状态、配置来源和空白检查由下面命令补全。

依据：[VS Code 源代码管理](https://code.visualstudio.com/docs/sourcecontrol/overview)。

**方法 B｜对应命令行**

```powershell
git status                            # 第一诊断入口，也提示正在进行的操作
git status -sb                        # 分支、领先/落后、文件状态的简写
git branch --show-current             # 当前分支；detached HEAD 时为空
git branch -vv                        # 本地分支、上游关联及领先/落后信息
git remote -v                         # 确认 Fetch / Push 的仓库地址
git log --oneline --graph --decorate -15

git diff                              # 未暂存的已跟踪文件改动
git diff --staged                     # 下一次提交的暂存内容
git diff --stat                       # 未暂存改动的规模摘要
git diff --staged --check              # 检查暂存差异中的空白错误等问题
```

`git status -sb` 中，文件名前的两列通常是 **X：暂存区状态，Y：工作区状态**：`M ` 已暂存，` M` 未暂存，`MM` 两边都有修改，`??` 未跟踪，`UU` 是一种冲突状态。简写不熟时改用完整 `git status`。

`diff --check` **不是编译器、测试或安全扫描**；[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|diff]] 也不负责展示未跟踪文件的正文，仍需打开新文件检查。分支领先 / 落后信息基于已获取的远程引用，而非实时联网查询。参考：[Status](https://git-scm.com/docs/git-status)、[Branch](https://git-scm.com/docs/git-branch)、[Diff](https://git-scm.com/docs/git-diff)、[Remote](https://git-scm.com/docs/git-remote)。

公司项目身份与个人项目可能不同，可先查来源，再只对当前仓库配置，避免改动全部仓库：

**方法 A｜先在 VS Code 中操作或检查**

先通过账户菜单确认 GitHub 授权身份，再在 Source Control 核对当前仓库。**账户登录不等于 Commit 署名**；内置界面没有统一的配置来源 / 仓库邮箱编辑器，这一项需要打开集成终端查看与设置。

**方法 B｜对应命令行**

```powershell
git config --show-origin --get user.email
git config --local user.name "你的工作署名"
git config --local user.email "你的工作邮箱"
```

`--local` 写入当前仓库配置；遵守团队对提交邮箱和签名的要求。参考：[Git Config](https://git-scm.com/docs/git-config)。

### 9.4 一次正常任务：从分支到 PR

学习阶梯：**L3 · 团队协作**

**前提：**工作区干净、主分支叫 [[#2.3 仓库、分支与远程名词|main]]、远程叫 [[#2.3 仓库、分支与远程名词|origin]]，且有写权限。每一步成功再继续；如果提示冲突或失败，先停下检查。

**方法 A｜先在 VS Code 中操作或检查**

1. Source Control 先 Fetch，点左下角分支切到 `main`，检查远程与本地是否可安全快进。
2. 普通 Pull 按钮受配置影响；要严格只允许快进，使用下面的显式命令，不能承诺按钮等价。
3. 再点分支名 → Create new branch，输入 `feature/login`。
4. 修改并保存 → 点文件看 Diff → 指定文件 `+` → 检查 Staged Changes → Commit。
5. 点 Publish Branch，确认目标为 `origin/feature/login`；以后用 Push。
6. 用 GitHub Pull Requests and Issues 扩展的创建 PR 入口，或 GitHub 网页 `Pull requests → New pull request`；核对 base / compare、Diff、CI 与审查。

PR 不是 Git 命令，下面的 Git 命令完成本地分支与推送部分。

**方法 B｜对应命令行**

```powershell
git fetch origin --prune
git switch main
git merge --ff-only origin/main        # 更新本地 main；不能快进则停止
git switch -c feature/login            # 从当前最新 main 建任务分支

# 修改、保存并完成项目要求的检查后：
git diff -- "src/login.ts"
git add -- "src/login.ts"
git diff --staged
git diff --staged --check
git commit -m "fix: 修复登录失效后的重试逻辑"
git push -u origin feature/login       # 首次发布并关联上游
```

- 第二次及之后，正常提交后可用 `git push`；关键发布场景也可显式写明目标分支。
- `git add -p -- "src/login.ts"` 可按块暂存：`y` 加入、`n` 跳过、`s` 尝试拆块、`q` 退出；未跟踪新文件不应直接假定会被它展示。
- `git add -A` 会暂存全仓库范围的新增、修改和删除；不是禁用命令，但必须确认所有变化都属于本次任务。`git commit -am "说明"` 不会纳入未跟踪新文件，不能作为通用快捷替代。
- 提交说明的 `fix:`、`feat:`、`docs:` 只是常见约定，不是 Git 强制格式。按团队模板写动机、影响和验证方式。

然后在 GitHub 新建 [[#2.3 仓库、分支与远程名词|PR]]，确认 **base 是 main、compare 是 feature/login**，检查 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 与测试结果，再合并。合并后回到本地 `main`，在工作区干净时再次拉取。没有原仓库写权限时，一般先 [[#2.9 团队与命令行辅助名词|Fork]]，再从自己的仓库提交 PR。

PR 还需处理审查意见并确认 [[#2.9 团队与命令行辅助名词|CI]]；**本地测试通过不等于远程 CI 通过，[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] 成功也不等于代码已合并**。

参考：[Switch](https://git-scm.com/docs/git-switch)、[Add](https://git-scm.com/docs/git-add)、[Commit](https://git-scm.com/docs/git-commit)、[Push](https://git-scm.com/docs/git-push)。

### 9.5 Fetch 以后，到底该 Pull 还是 Push？

学习阶梯：**L3 · 团队协作**

这也补充前文“开始工作前先 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]]”的含义：**先更新远程信息，再判断差异，不是每次都必须 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] 一次。**

**方法 A｜先在 VS Code 中操作或检查**

点 Fetch 后观察 Graph：只领先 → 审查 Outgoing 后 Push；只落后 → 先确认整合规则再 Pull；两侧各有提交 → 先比较与按团队规则整合。可右键提交用 Compare with Remote / Compare with... 查看差异，但精确提交范围以下面的命令为准。不要用 Sync 掩盖分叉。

**方法 B｜对应命令行**

```powershell
git fetch origin --prune
git branch -vv
git log --oneline "@{upstream}..HEAD"   # 本地有、上游没有的提交
git log --oneline "HEAD..@{upstream}"   # 上游有、本地没有的提交
```

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| 双方没有差异 | 继续工作，不需要为“同步”额外制造操作 | 没有新东西，继续干活 |
| 只有本地领先 | 检查提交后正常 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Push]] | 我这边有新提交，检查后发出去 |
| 只有本地落后 | 工作区干净时 `git merge --ff-only "@{upstream}"`；或用 `git pull --ff-only` 再获取并快进 | 远程比我新，确认后接进来 |
| 双方都有新提交，出现分叉 | 先读两侧历史，再按团队规则 [[#2.8.1 整合与提交整理\|Merge]] / [[#2.8.1 整合与提交整理\|Rebase]]；不强推覆盖别人 | 双方都改了，先商量怎么合，别覆盖别人 |
| 没有上游关联 | 确认正确的目标分支，首次发布用 `git push -u origin feature/login`；已有远程分支可显式关联 | 先弄清楚这个本地分支要对应远程哪条分支 |

**方法 A｜先在 VS Code 中操作或检查**

若是新分支，Publish Branch 可以建立上游；若远程分支已经存在，先在分支列表 / Graph 确认完整名称。内置界面没有通用的“把任意本地分支重新关联到指定既有上游”的一键保证，精确设置用下面命令；这不是重新 Clone 或合并。

**方法 B｜对应命令行**

```powershell
# 只在当前本地分支确实应该跟踪它时设置；不会下载或合并内容
git branch --set-upstream-to=origin/feature/login
```

`fetch --prune` 通常清理所取远程中已删除分支对应的本地远程跟踪引用，**不等于删除本地功能分支**。参考：[Fetch](https://git-scm.com/docs/git-fetch)、[Branch](https://git-scm.com/docs/git-branch)。

**必须分清：更新“自己的远程同名分支”和接入“[[#2.3 仓库、分支与远程名词|main]] 的新变化”是两件事。**在 `feature/login` 上默认 Pull 通常整合其上游 `origin/feature/login`，不会自动接入 [[#2.3 仓库、分支与远程名词|origin/main]]。

比较范围也要看懂：

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| `git log A..B` | B 可达、A 不可达的提交 | 看 B 比 A 多出的提交 |
| `git log --left-right --oneline A...B` | 两侧独有提交；`<` 属于 A，`>` 属于 B | 看分叉后双方各自多了哪些提交 |
| `git diff A B` | 两个端点的文件快照差异 | 直接比较两个版本的文件 |
| `git diff A...B` | 从 A、B 的合并基点到 B 的文件差异；有方向性 | 从共同起点看 B 这一侧改了什么 |

查看功能分支相对主线的变更，可用 `git diff origin/main...HEAD`；但它不一定等同于托管平台所有情形下的最终合并结果。**[[#2.8.4 Log、Blame 与 Bisect|Log]] 的三点号与 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]] 的三点号不是同一语义。**参考：[Log](https://git-scm.com/docs/git-log)、[Diff](https://git-scm.com/docs/git-diff)。

### 9.6 功能分支接入主线：Merge / Rebase 二选一

学习阶梯：**L3 · 团队协作**

先保存工作、确认分支干净，并 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]]。以下两种是**可选方案，不要为了保险连续执行两种**。

**[[#2.8.1 整合与提交整理|Merge]] 方案：保留现有提交关系。**适合团队允许合并提交、或多人共同使用的功能分支。

**方法 A｜先在 VS Code 中操作或检查**

先点左下角分支切到 `feature/login` → Fetch → 命令面板 `Git: Merge...`（或 `… → Branch → Merge...`）→ 选择 `origin/main`。当前功能分支接收主线内容，不是把功能分支合入 main；有冲突先处理，再检查与测试。

**方法 B｜对应命令行**

```powershell
git switch feature/login
git fetch origin
git merge origin/main
# 若成功，检查、测试，再正常 git push
```

真正分叉时通常产生合并提交；能够快进时不一定新增合并提交。要注意方向：**当前检出的分支接收指定分支的内容**，这里更新的是功能分支，不是在本地把功能合进 [[#2.3 仓库、分支与远程名词|main]]。参考：[Git Merge](https://git-scm.com/docs/git-merge)。

**[[#2.8.1 整合与提交整理|Rebase]] 方案：重放自己的功能提交。**适合团队要求线性历史、且允许整理的个人功能分支。

**方法 A｜先在 VS Code 中操作或检查**

只在团队允许的个人分支操作：先在当前旧位置创建备份分支，再切回 `feature/login`，Fetch 后用命令面板 `Git: Rebase Branch...`，选择 `origin/main`。若当前版本没有这一入口，用终端；它不是交互式整理提交的完整 GUI。

菜单名核对：[VS Code 内置 Git 命令](https://github.com/microsoft/vscode/blob/main/extensions/git/package.nls.json)。

**方法 B｜对应命令行**

```powershell
git switch feature/login
git branch backup/login-before-rebase  # 留住旧提交位置，名字需要唯一
git fetch origin
git rebase origin/main
```

Rebase 把功能提交重放到新主线之上，通常改变提交 ID。完成后重新测试；首次发布 / 未改变已发布历史时正常 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]]；若改写了已发布历史，先看 9.9。**不擅自 Rebase 团队共享分支。**

示意：原来 main 为 `A—B—C`，功能从 B 分出 `D—E`；Rebase 后功能成为 `A—B—C—D′—E′`。原来的 D、E 并非直接“搬走而 ID 不变”。参考：[Git Rebase](https://git-scm.com/docs/git-rebase)。

### 9.7 冲突处理：会解决，也会安全退出

学习阶梯：**L3 · 团队协作**

开始前尽量保持工作区干净；不要在一场未完成的 [[#2.8.1 整合与提交整理|Merge]] / [[#2.8.1 整合与提交整理|Rebase]] 中又启动另一场历史操作。

#### 9.7.1 用 VS Code 检查与解决

学习阶梯：**L3 · 团队协作**

1. 打开 [[#2.8.1 整合与提交整理|Merge]] [[#2.7 Changes、文件状态与 Graph|Changes]] 中的文件，比较冲突双方；复杂冲突可用 Open in Merge Editor。
2. 逐处决定保留、组合或重写，清除冲突标记，检查最终 Result。
3. 保存、暂存全部已解决文件，并检查整体内容。
4. 按正在进行的操作完成：普通 Merge 解决并暂存后用 Commit 完成；Rebase / Cherry-pick / Revert 的明确 Continue / Abort 见下一小节，不把普通 Commit 按钮当作所有操作的通用结束方式。
5. 复查 Source Control 与 Graph，确认没有遗留冲突 / 未完成操作，再测试并推送；精确诊断见下一小节命令。

**Accept Both 只是同时保留两边文本，不保证逻辑正确。**Rebase 时 Current / Incoming 的含义也不同于普通 Merge，不要机械地理解成“我的 / 别人的”。想取消时，应使用对应操作的 [[#2.8.1 整合与提交整理|Abort]]；取消前保留需要的冲突处理成果。

#### 9.7.2 用命令行检查、继续或取消

学习阶梯：**L3 · 团队协作**

**方法 A｜先在 VS Code 中操作或检查**

先按上一小节打开 Merge Changes → Resolve in Merge Editor，逐处检查 Result → 保存 → 文件 `+` 标记解决。取消时可在命令面板搜索与当前操作对应的 Abort Merge / Abort Rebase / Abort Cherry Pick；未显示入口或需要精确 Continue / Abort 时，使用下面对应命令。**没有按钮就明确走终端，不凭空编一个“继续所有操作”的图标。**

依据：[VS Code 冲突处理](https://code.visualstudio.com/docs/sourcecontrol/merge-conflicts)。

**方法 B｜对应命令行**

```powershell
git status
git diff --name-only --diff-filter=U    # 查找未合并文件
# 在 VS Code 中编辑冲突、检查结果、保存
git add -- "src/login.ts"              # 标记该文件的解决结果
git diff --staged
```

随后**只执行与当前状态对应的一行**：

| 图标                                               | 含义                                                              | 大白话                                          |
| ------------------------------------------------ | --------------------------------------------------------------- | -------------------------------------------- |
| [[#2.8.1 整合与提交整理\|Merge]]                        | 继续：`git merge --continue`<br>放弃：`git merge --abort`             | 解决并暂存后才继续；想取消则用对应的 [[#2.8.1 整合与提交整理\|Abort]] |
| [[#2.8.1 整合与提交整理\|Rebase]]                       | 继续：`git rebase --continue`<br>放弃：`git rebase --abort`           | 解决并暂存后才继续；想取消则用对应的 Abort                     |
| [[#2.8.1 整合与提交整理\|Cherry-pick]]                  | 继续：`git cherry-pick --continue`<br>放弃：`git cherry-pick --abort` | 解决并暂存后才继续；想取消则用对应的 Abort                     |
| [[#2.8.3 Restore、Reset、Revert 与 Reflog\|Revert]] | 继续：`git revert --continue`<br>放弃：`git revert --abort`           | 解决并暂存后才继续；想取消则用对应的 Abort                     |

Rebase 可能在多个提交处依次停下，需要重复处理。`git rebase --skip` 是**跳过当前提交的重放**，不是“忽略报错但保留修改”；不要把它当万能继续按钮。Abort 会放弃本次操作中的处理成果，提前另存需要保留的编辑。

[[#2.8.2 Stash 与 Worktree|Stash]] 恢复冲突不使用上述 Merge / Rebase [[#2.8.1 整合与提交整理|Continue]] 流程，见 9.11。参考：[Merge](https://git-scm.com/docs/git-merge)、[Rebase](https://git-scm.com/docs/git-rebase)、[Cherry-pick](https://git-scm.com/docs/git-cherry-pick)、[Revert](https://git-scm.com/docs/git-revert)。

### 9.8 提交整理：Amend、Reword、Squash / Fixup

学习阶梯：**L4 · 进阶按需**

> [!warning]
> **适用边界**
>
> 默认只整理**尚未分享、无人依赖**的提交。已发布个人分支是否允许改写也要确认团队约定；主线和多人共享分支不要自行整理。

**改最近一次提交说明：**

**方法 A｜先在 VS Code 中操作或检查**

普通 Amend 有图形入口：先看 Staged Changes，确认不会带入无关内容 → Commit 按钮下拉里的 Commit (Amend)，或 `… → Commit → Commit Staged (Amend)` → 核对说明后确认。仅改说明时不应意外留下待提交内容。

依据：[VS Code 暂存与 Amend](https://code.visualstudio.com/docs/sourcecontrol/staging-commits)。

**方法 B｜对应命令行**

```powershell
git diff --staged                      # 先确认没有准备意外带入的内容
git commit --amend -m "fix: 修复登录失效后的重试逻辑"
```

把遗漏修改补进最近一次提交：先 `git add -- "文件路径"`，再 `git commit --amend --no-edit`。[[#2.8.1 整合与提交整理|Amend]] 会把**当前所有暂存内容**纳入替代提交，并非只改单个文件。参考：[Git Commit](https://git-scm.com/docs/git-commit)。

**整理最近三次普通本地提交：**

**方法 A｜先在 VS Code 中操作或检查**

交互式 Reword / Squash / Fixup：**内置 Git 没有与下面整个流程等价的完整图形面板**。可以先用 Graph 审查要整理的三个提交、创建备份分支；之后用终端启动交互式 Rebase。若 Git 编辑器已配置为 VS Code，编辑待办列表时仍可在 VS Code 完成，但这不等于纯图标操作。GitLens 的组织提交能力是可选方案，不把付费扩展当作内置功能。

**方法 B｜对应命令行**

```powershell
git branch backup/login-before-edit
git rebase -i HEAD~3
```

编辑器中的 `pick` 保留提交，[[#2.8.1 整合与提交整理|reword]] 改说明，[[#2.8.1 整合与提交整理|squash]] 合进前一个提交并编辑说明，[[#2.8.1 整合与提交整理|fixup]] 合入前一个提交但丢弃自己的说明，`drop` 删除该提交。保存关闭后执行；这不是“关闭窗口就自动取消”。例子要求存在 `HEAD~3`，且待整理范围没有需要特殊处理的合并拓扑。

更精准地修复某次提交，可在暂存修正后用 `git commit --fixup COMMIT_ID`，再按确定的范围 `git rebase -i --autosquash BASE_COMMIT`。`BASE_COMMIT` 必须位于目标提交之前；先确认范围再运行。参考：[Commit 的 Fixup](https://git-scm.com/docs/git-commit)、[Rebase 的交互与 Autosquash](https://git-scm.com/docs/git-rebase)。

### 9.9 改写已发布历史后：为什么不是直接 Force Push？

学习阶梯：**L4 · 进阶按需**

正常推送提示 `non-fast-forward`，既可能是同事推了新提交，也可能是自己 [[#2.8.1 整合与提交整理|Rebase]] / [[#2.8.1 整合与提交整理|Amend]] 改了历史，**不能只凭报错选择强推**。

确实需要替换自己已发布的个人分支、团队也允许时，可使用：

**方法 A｜先在 VS Code 中操作或检查**

先在 Graph Fetch 并比较本地与远程提交，核对当前分支和目标。菜单可能有 Push (Force)，但它使用什么保护取决于 `git.useForcePushWithLease` 等配置；**按钮名称不能证明等价于下面显式目标与 Lease 参数**。这里推荐界面只负责审阅，确认团队授权后用明确命令执行。不要因普通 Push 失败就点击 Force。

配置与命令定义：[VS Code 内置 Git](https://github.com/microsoft/vscode/blob/main/extensions/git/package.json)。

**方法 B｜对应命令行**

```powershell
# 危险操作：确认当前 HEAD、目标分支、协作者和远程差异后才运行
git push --force-with-lease origin HEAD:refs/heads/feature/login
```

`--force-with-lease` 会校验预期的远程位置，比裸 `--force` 多一层保护，但不是“保证无损”。无显式预期值时通常依赖本地远程跟踪引用；**编辑器后台 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 可能更新该引用，削弱“我已审阅过远程”的假设**。高级用法是明确绑定已人工审阅、在改写前保存的远程提交：`--force-with-lease=refs/heads/feature/login:EXPECTED_OLD_REMOTE_HASH`，不要在推送前随手取最新哈希充当预期值。

Lease 拒绝时，重新审阅新增提交并协商，不降级为裸 Force。分支保护禁止强推时也不要绕过；`backup/...` 分支只保护已有提交，不保存未提交文件。参考：[Git Push 的 Lease 及后台 Fetch 警告](https://git-scm.com/docs/git-push)。

### 9.10 Cherry-pick：只移植一个修复，不合并整个分支

学习阶梯：**L4 · 进阶按需**

例如主线上的普通修复提交需要回补维护分支，先确认目标分支和工作区干净：

**方法 A｜先在 VS Code 中操作或检查**

1. 先在 Graph 找来源提交，Open Changes 读修复与依赖，并复制提交哈希。
2. 点分支切到维护分支，确认已安全更新，再 Create new branch 建回补分支。
3. 在 Graph 右键来源提交 → Cherry Pick；冲突时回 Merge Editor。
4. 检查、测试并发布后开 PR。**若团队要求 `-x` 来源记录或严格 ff-only 更新，用下面命令；不要先点 Cherry Pick 再执行同一条命令，否则可能重复应用。**

入口依据：[VS Code 历史图](https://code.visualstudio.com/docs/sourcecontrol/history)。

**方法 B｜对应命令行**

```powershell
git show COMMIT_ID                     # 先读具体修复与前置依赖
git switch release/1.x                 # 示例：已经存在的本地维护分支
git fetch origin
git merge --ff-only origin/release/1.x
git switch -c hotfix/login-backport    # 单独建回补分支，后续走 PR
git cherry-pick -x COMMIT_ID
```

它通常创建新提交，不会合并来源分支的全部历史。`-x` 用于留下来源提交信息，适合可共同访问的维护分支间回补；冲突解决后要核查来源记录是否保留。原修复若依赖其他提交，需要一并评估，不能只看“摘取成功”。合并提交的 [[#2.8.1 整合与提交整理|Cherry-pick]] 需要额外选择主线父提交，初学不要盲加 `-m 1`。参考：[Git Cherry-pick](https://git-scm.com/docs/git-cherry-pick)。

### 9.11 临时任务：Stash 与 Worktree

学习阶梯：**L2–L3 · 先学 Stash，再按需要学 Worktree**

#### 9.11.1 Stash：临时收起未提交改动

学习阶梯：**L2 · 日常熟练**

`-u` 包括未跟踪文件，但不包括已忽略文件。`apply` 保留记录；`pop` 通常在成功恢复后移除记录，冲突时记录会保留。**[[#2.8.2 Stash 与 Worktree|Stash]] 不是已推送的远程备份**，重要成果仍应提交并推送。

指定条目比“凭记忆恢复最新项”更明确：

**方法 A｜先在 VS Code 中操作或检查**

命令面板运行 `Git: Stash (Include Untracked)`，填说明；用 `Git: View Stash...` 检查条目，再用 `Git: Apply Stash...` 选指定条目恢复。确认后才 Drop；想成功恢复后通常同时移除记录才选 Pop。普通 `Git: Stash` 不包括新文件。

依据：[VS Code Stash](https://code.visualstudio.com/docs/sourcecontrol/branches-worktrees#manage-stashes)。

**方法 B｜对应命令行**

```powershell
git stash push -u -m "登录任务进行中"
git stash list
git stash show -p -u "stash@{0}"       # 包括查看其中的未跟踪文件内容
git stash apply "stash@{0}"            # 恢复但保留记录
```

确认恢复正确后，再按最新 `stash list` 选择要 `git stash drop "stash@{0}"` 的条目；新增 / 删除条目会改变编号。需要恢复暂存状态时了解 `apply --index`，不要默认 Apply 会原样还原暂存选择。

恢复冲突时手工解决、暂存并继续正常开发，没有 `git stash --continue`；不要盲目丢弃工作区或删除 stash 记录。参考：[Git Stash](https://git-scm.com/docs/git-stash)。

#### 9.11.2 Worktree：另开目录处理急事

学习阶梯：**L3 · 团队协作**

适用于需要并行检出两个分支的情况：

**方法 A｜先在 VS Code 中操作或检查**

Source Control Repositories 视图 → 目标仓库 `… → Worktrees → Create Worktree` → 选择起点分支、新分支名与目录，打开新窗口。结束前检查有用的修改、未跟踪与忽略文件，再在主工作区用 `Git: Delete Worktree...` 核对路径后删除；没有此入口的旧版 VS Code 使用终端。

若界面不能同时指定下面示例的起点和新分支，改用显式命令，不将“任意新工作区”冒充等价结果。依据：[VS Code Worktree](https://code.visualstudio.com/docs/sourcecontrol/branches-worktrees#working-with-git-worktrees)。

**方法 B｜对应命令行**

```powershell
git fetch origin
git worktree add -b hotfix/login ../repo-hotfix origin/main
git worktree list
```

`../repo-hotfix` 是示例外部工作目录：**运行前自行确认解析后的完整路径、位置和磁盘空间**，不要在笔记库里直接照抄。不同 [[#2.8.2 Stash 与 Worktree|Worktree]] 共享提交、分支等仓库数据，但工作文件和暂存区独立；不是“完全独立的第二个仓库”。同一个本地分支通常不能同时检出到两个 Worktree。

结束后先检查另一个目录的未提交、未跟踪和忽略文件，再使用 `git worktree remove "实际工作目录"`；不要用 `--force` 绕过有用文件的保护。删除 Worktree 不等于删除对应分支。参考：[Git Worktree](https://git-scm.com/docs/git-worktree)。

### 9.12 撤销与救援：Restore / Reset / Revert / Reflog

学习阶梯：**L2–L4 · 分场景学习，不按顺序盲目执行**

四个名词的区别见 [[#2.8.3 Restore、Reset、Revert 与 Reflog|撤销与救援名词]]。本节只按具体场景说明操作。

#### 9.12.1 取消暂存与恢复单个文件

学习阶梯：**L2 · 日常熟练**

**方法 A｜先在 VS Code 中操作或检查**

取消暂存：Staged Changes 中悬停目标文件 → `−`，编辑会留下；也可以在暂存 Diff 中选定行 / 块取消暂存。

从旧版本取回内容：在 Timeline 打开该文件的 Git 历史，查看目标版，把确认要恢复的内容复制到当前文件并检查、暂存、提交；要精确按提交恢复整个指定路径，使用下面的 `--source` 写法。**Discard 不是“取回任意旧版本”。**

**方法 B｜对应命令行**

```powershell
git restore --staged -- "src/login.ts"
```

若只想从旧版本取回某个文件，而不是回退整个分支，可用 `git restore --source=COMMIT_ID -- "src/login.ts"`；它会覆盖该路径的工作区内容，先另存要保留的编辑，再检查、暂存、提交。参考：[Git Restore](https://git-scm.com/docs/git-restore)。

#### 9.12.2 撤回未分享的普通提交

学习阶梯：**L4 · 进阶按需**

先确认工作区 / 暂存区干净、至少有一个父提交，并留住旧提交位置。

**方法 A｜先在 VS Code 中操作或检查**

先在 Graph 创建备份分支保住旧位置，再切回原分支。要撤回最近一次未共享普通提交，用 `Source Control → … → Commit → Undo Last Commit`，检查修改是否留在 Staged Changes；这是下面 Soft Reset 场景的图形入口。不要用它撤销别人依赖的提交。根提交需要特殊处理，不套用 HEAD~1。

**方法 B｜对应命令行**

```powershell
git branch backup/login-before-reset
git reset --soft HEAD~1
```

结果是分支后退，改动留在暂存区。VS Code 的 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]] → Undo Last Commit 是另一种图形界面入口，适用于最近一次未推送提交；不要拿它删除共享历史。另一种选择 `git reset --mixed HEAD~1` 会后退并重置暂存区，文件内容留下但变为未暂存；**Soft 与 Mixed 是二选一，不要连续运行两次，否则会再退一步**。`--hard` 还重置工作文件，可能丢弃改动并覆盖挡路的未跟踪内容，不提供“出错就 Hard”的通用处方。参考：[Git Reset](https://git-scm.com/docs/git-reset)。

#### 9.12.3 抵消已经分享的普通提交

学习阶梯：**L3 · 团队协作**

工作区干净时运行：

**方法 A｜先在 VS Code 中操作或检查**

内置 Graph 可查目标提交、Open Changes 并复制哈希，但官方流程对已共享提交的 Revert 使用集成终端，**没有统一的内置“一键 Revert Commit”按钮可保证存在**。先在界面确认分支干净和目标，再执行下方命令，随后回 Graph 检查新增的反向提交、测试并走 PR。Diff 中的 Revert Block 只是丢弃编辑，不能代替它。

**方法 B｜对应命令行**

```powershell
git revert COMMIT_ID
# 检查、测试，然后推送该反向提交或走回滚 PR
```

[[#2.8.3 Restore、Reset、Revert 与 Reflog|Revert]] 不是删除历史；合并提交的 Revert 要明确主线父提交及后续再合并影响，不能照抄普通提交的命令。参考：[Git Revert](https://git-scm.com/docs/git-revert)。

#### 9.12.4 找回误操作前的提交

学习阶梯：**L4 · 进阶按需**

先找回提交，不再覆盖现场：

**方法 A｜先在 VS Code 中操作或检查**

内置 VS Code 没有完整 Reflog 救援面板。可先用 Timeline / Local History 检查文件级历史、Graph 查看仍有引用的提交，但它们不是 Reflog 的等价替代。不要继续点 Reset / Discard 覆盖现场；在终端找到旧哈希并建救援分支后，再回 Graph 验证。

**方法 B｜对应命令行**

```powershell
git reflog --date=iso
git show OLD_TIP                       # 从记录中找到并核对旧哈希
git branch rescue/login OLD_TIP        # 给旧提交挂一个新分支，先不切换
git log --oneline rescue/login -10
```

这个方案先增加救援引用，不用立即 Hard [[#2.8.3 Restore、Reset、Revert 与 Reflog|Reset]] 当前分支。[[#2.8.3 Restore、Reset、Revert 与 Reflog|Reflog]] 是本地记录，会过期；它能帮助找回仍存在的提交，但**通常不能找回从未被 Git 记录、后来又被覆盖或 Clean 的编辑**。处于 Detached [[#2.3 仓库、分支与远程名词|HEAD]] 且刚做了有价值的提交时，可先 `git branch rescue/detached HEAD` 保留它。参考：[Git Reflog](https://git-scm.com/docs/git-reflog)、[Git Branch](https://git-scm.com/docs/git-branch)。

### 9.13 排查“谁改的、哪次引入了 Bug”

学习阶梯：**L3–L4 · 从历史检索到二分排错**

#### 9.13.1 历史检索与 Blame

学习阶梯：**L3 · 团队协作**

**方法 A｜先在 VS Code 中操作或检查**

打开目标文件 → Explorer 中展开 Timeline，选 Git 提交读历史 Diff；查某行来源时启用原生 Git Blame 的编辑器 / 状态栏显示，悬停看提交，也可用已安装 GitLens 的 File / Line History。按字符串出现次数检索、跨重命名和精确行范围仍由下面命令补全。

依据：[VS Code 文件历史与 Blame](https://code.visualstudio.com/docs/sourcecontrol/history)。

**方法 B｜对应命令行**

```powershell
git log --oneline -- "src/login.ts"    # 哪些提交改过它
git log --follow -- "src/login.ts"     # 对单文件尝试跨重命名追踪
git log -p -5 -- "src/login.ts"        # 最近几次的具体补丁
git log --oneline --grep="login"       # 搜提交说明
git log -S "retryCount" -- "src/login.ts" # 搜字符串出现次数变化的提交
git blame -L 20,60 -- "src/login.ts"   # 追踪指定行的最后修改
git show COMMIT_ID -- "src/login.ts"   # 读完整提交上下文
```

`-S` 不是普通全文搜索：它寻找指定字符串出现次数变化的提交；寻找补丁行匹配可进一步查 `-G`。[[#2.8.4 Log、Blame 与 Bisect|Blame]] 用来找上下文和相关提交，不用来推断责任。参考：[Git Log](https://git-scm.com/docs/git-log)、[Git Blame](https://git-scm.com/docs/git-blame)。

#### 9.13.2 Bisect：二分定位 Bug

学习阶梯：**L4 · 进阶按需**

在“已知好版本”和“已知坏版本”之间二分定位。前提是有稳定可复现的判定方法，工作区干净；建议在独立 [[#2.8.2 Stash 与 Worktree|Worktree]] 或练习仓库操作。

**方法 A｜先在 VS Code 中操作或检查**

内置 Git 没有完整 Bisect 图形向导。先用 Graph 找到可确认的好 / 坏提交、复制哈希；在练习仓库或独立 Worktree 中用终端启动二分。每轮在 VS Code 构建、运行或测试，判断同一个问题后回终端标 good / bad；不能把逐个点击旧版本当成已经执行了 Bisect。

**方法 B｜对应命令行**

```powershell
git bisect start
git bisect bad                        # 当前版本已确认存在该问题
git bisect good GOOD_COMMIT            # 某个已确认没有该问题的祖先提交
# Git 检出中间版本；每轮构建/运行并判断同一个问题后，二选一：
git bisect good                       # 中间版本没有该问题
# 或 git bisect bad                   # 中间版本存在该问题
# 重复到定位首个坏提交，记录结果，最后：
git bisect reset                      # 回到开始前的位置
```

无法判断某版本可用 `git bisect skip`，但跳过版本可能导致无法唯一定位。脚本自动化 `git bisect run` 的退出码含义要先查文档；不要把构建环境问题错误标成业务 Bug。参考：[Git Bisect](https://git-scm.com/docs/git-bisect)。

### 9.14 工作中常见报错：先诊断，不乱改全局配置

学习阶梯：**L3 · 团队协作**

**方法 A｜先用 VS Code / GitHub 界面定位**

| 报错 / 现象 | 先看哪个界面 | 界面不能替代的部分 |
| --- | --- | --- |
| Push rejected / 分叉 | Show Git Output 看完整报错；Fetch 后看 Graph 两侧提交 | 用精确比较范围决定 Merge / Rebase，不先 Force |
| 没有上游 | 看左下角 Publish Branch 与 Graph 远程分支 | 关联到特定既有上游时用显式设置 |
| 切分支会覆盖改动 | Changes / Staged Changes，必要时 Stash | 不用强制切换掩盖未保存成果 |
| 忽略无效 / 新文件消失 | Explorer 看规则文件，Source Control 看当前条目 | 是否跟踪、哪条规则匹配，用 ls-files / check-ignore 诊断 |
| 认证 / 权限问题 | 账户菜单、Show Git Output、GitHub 仓库权限 | 检查协议与凭据来源，不关闭 SSL 校验 |
| Detached HEAD | Graph 看 HEAD 是否附着分支；有成果先 Create Branch | 找不到旧提交时用 Reflog，不随意清理 |
| 整个文件像被重写 | Diff 看换行 / 编码，编辑器状态栏看格式 | 具体配置来源由 git config 确认 |
| Hook / CI 失败 | Output / 终端详细日志；GitHub PR 的 Checks 或 Actions | 看实际检查输出修复，不把 --no-verify 当解法 |

清理文件前先在 Explorer 核对路径并另存有用文件；不要用 Discard All 代替“仅预览未跟踪文件”。下方 Clean 只给预览，不能据此直接删除。

**方法 B｜对应命令、精确诊断与边界**

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| `non-fast-forward` / [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Push]] rejected | [[#2.6 Fetch、Pull、Push 与 Sync Changes\|Fetch]] 后读双侧提交；区分别人有新提交和自己改写了历史，参见 9.5、9.9 | 先弄清谁比谁多了什么，别急着强推 |
| 没有 [[#2.3 仓库、分支与远程名词\|Upstream]] | `git branch -vv`；确认目标后 `push -u` 或显式设置上游 | 给分支找对远程对应关系 |
| [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Pull]] 提示分叉 / 需要选择整合策略 | 确认团队规则，再显式 [[#2.8.1 整合与提交整理\|Merge]] / [[#2.8.1 整合与提交整理\|Rebase]]；别为了消除提示就盲改全局 `pull.rebase` | 先按团队规则决定怎么合 |
| 切分支提示会覆盖本地修改 | 先检查并提交 / [[#2.8.2 Stash 与 Worktree\|Stash]]，或另开 [[#2.8.2 Stash 与 Worktree\|Worktree]]；不先用强制切换 | 先把手上的工作收好 |
| 文件明明被忽略却仍出现在提交里 | 查是否已经跟踪：`git ls-files -- "文件路径"`；已跟踪的文件不受普通忽略规则屏蔽 | 被跟踪过的文件，不是加忽略规则就能藏起来 |
| 新文件意外被忽略 | `git check-ignore -v -- "文件路径"` 查匹配的规则；不要直接 `add -f` | 先查是哪条规则把文件挡住了 |
| 权限拒绝 / Authentication failed | `git remote -v` 核实地址与协议，检查登录、令牌权限 / 过期、SSH 和组织 SSO；不关闭 SSL 校验 | 先查地址、登录和权限，别关安全校验 |
| `detached HEAD` | 先判断是否只是查看版本；有新成果先建救援分支再切换 | 先保住新提交，再决定去哪条分支 |
| 整个文件都显示改变 | 检查换行符、编码、格式化；按仓库 [[#2.9 团队与命令行辅助名词\|.gitattributes]] 和团队约定处理，不随手给全部项目改 `core.autocrlf` | 可能只是换行或格式变化，别一口气重写全部文件 |
| [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff\|Commit]] 被 [[#2.9 团队与命令行辅助名词\|Hook]] 拒绝，或 [[#2.3 仓库、分支与远程名词\|PR]] 的 [[#2.9 团队与命令行辅助名词\|CI]] 失败 | 读具体检查输出并修复；`--no-verify` 不是日常绕过检查的按钮 | 按报错修问题，不绕过检查 |

忽略诊断参考：[Check-ignore](https://git-scm.com/docs/git-check-ignore)；换行符与文件属性参考：[Git Attributes](https://git-scm.com/docs/gitattributes)。配置变更前先用 `git config --show-origin --get 配置名` 查来源，尽量理解并限定到当前仓库。参考：[Git Config](https://git-scm.com/docs/git-config)。

**Clean 只从预览开始：**`git clean -nd -- "准备清理的相对目录/"` 预览未跟踪文件 / 目录；确认实际路径、清单及备份以后，才考虑对相同范围使用 `-fd`。不要习惯性运行全仓库 `clean -fdx`：`-x` 连忽略文件也会纳入，可能包括本地环境文件和重要资产。Clean 删除的未跟踪内容通常不能靠 [[#2.8.3 Restore、Reset、Revert 与 Reflog|Reflog]] 救回。参考：[Git Clean](https://git-scm.com/docs/git-clean)。

### 9.15 入职后的团队约定与按需能力

学习阶梯：**L3 · 团队协作**

实际公司的工作流可能是 GitHub Flow、维护多个发布分支、Trunk-based 或自研平台；“所有大厂都用 Git Flow / 都必须 [[#2.8.1 整合与提交整理|Rebase]]”都不成立。接手项目先确认这些问题：

- 主干 / 发布分支是什么？功能分支怎样命名、多久合入？
- [[#2.3 仓库、分支与远程名词|PR]] 用 [[#2.8.1 整合与提交整理|Merge]]、[[#2.8.1 整合与提交整理|Squash]] Merge 还是 Rebase Merge？允许改写哪些分支？
- 需要几人审查、哪些 [[#2.9 团队与命令行辅助名词|CI]] 检查、提交邮箱 / 签名 / [[#2.9 团队与命令行辅助名词|Issue]] 关联？
- 线上回滚由谁审批，是 [[#2.8.3 Restore、Reset、Revert 与 Reflog|Revert]] 源码、回退部署，还是两者配合？
- 哪些目录是生成物，哪些大文件走 [[#2.9 团队与命令行辅助名词|LFS]]，是否存在 [[#2.9 团队与命令行辅助名词|Submodule]]？

保护分支可以要求 PR 审查、状态检查并限制强推；有权限也不代表应该绕开流程。参考：[GitHub 保护分支](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)。

**方法 A｜先用 VS Code / GitHub 界面定位**

先在 GitHub 的 PR、Settings / Rulesets、Actions 与仓库文档确认团队规则，再用下面的界面入口；未授权就不修改设置。

| 任务 | VS Code / GitHub 入口 | 不完全等价的边界 |
| --- | --- | --- |
| 清理本地分支 | 切到其他分支 → Git: Delete Branch，或 Graph 的分支菜单 | 看清安全删除提示，不盲目强删 |
| 删除远程分支 | Git: Delete Remote Branch，或 GitHub Branches 中指定分支的删除入口 | 影响别人，先确认任务已完成与权限 |
| 创建 / 发布 Tag | Graph 定位提交 → Create Tag；发布后去 GitHub Releases 管理发行版 | 注释、签名、明确目标标签的推送，使用下面命令；Tag 不等于 Release |
| Submodule | 在仓库视图识别子仓库与状态，逐个打开检查 | 初始化、递归更新与提交指针用终端；没有“点一下自动跟最新”的保证 |
| Git LFS | 在编辑器看 .gitattributes，依项目文档识别大文件 | 安装、追踪规则与迁移历史没有统一内置按钮；不要直接批量重写 |
| Rebase 前后审查 | Graph 与 Diff 辅助看提交、文件变化 | 两组补丁的精确 range-diff 仍需要终端，且不能代替测试 |

**方法 B｜对应命令、精确诊断与边界**

| 图标 | 含义 | 大白话 |
| --- | --- | --- |
| 清理本地任务分支 | 先切换离开，再 `git branch -d feature/login`。Squash 合并后可能无法按祖先关系认定已合并；核对 PR 和提交内容后再按团队流程处理，不因提示就立刻用 `-D` | 确认任务已经合入，再清理本地标签 |
| 删除远程任务分支 | `git push origin --delete feature/login` 会真实删除远程分支；只在任务完成、无人依赖且确认权限后操作 | 会影响远程和别人，确认后再删 |
| 查看 / 创建 [[#2.9 团队与命令行辅助名词\|Tag]] | `git tag --list`；发布流程允许时 `git tag -a v1.2.0 -m "Release v1.2.0" COMMIT_ID`，再 `git push origin v1.2.0`。Tag 不是完整的 GitHub [[#2.9 团队与命令行辅助名词\|Release]]，也不应擅自移动已发布标签 | 给确定版本留标记，按发布流程来 |
| Submodule | 项目使用子模块时了解 `git submodule status`、`git submodule update --init --recursive`；主仓库记录子模块的特定提交，不会自动跟踪它的最新代码 | 主项目记的是子项目的某次提交 |
| [[#2.9 团队与命令行辅助名词\|Git LFS]] | 二进制资产等按项目规则处理。LFS 用指针记录大文件；`git lfs` 需要单独安装，不能只看到指针文本就认定文件坏了，也不要擅自迁移全仓库历史 | 大文件走专门通道，先按项目规则配置 |
| 整理前后审查 | 进阶可用 `git range-diff OLD_BASE..OLD_TIP NEW_BASE..NEW_TIP` 对比两组补丁，辅助确认 Rebase 没意外改变意图；不能替代测试 | 整理完历史，再对照改动有没有走样 |

参考：[Branch](https://git-scm.com/docs/git-branch)、[Push](https://git-scm.com/docs/git-push)、[Tag](https://git-scm.com/docs/git-tag)、[Submodule](https://git-scm.com/docs/git-submodule)、[GitHub 的 LFS 说明](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-git-large-file-storage)、[Range-diff](https://git-scm.com/docs/git-range-diff)。

## 10. 忽略规则与安全边界

学习阶梯：**L1–L2 · 安全底线先读，补救流程按需练习**

### 10.1 忽略规则配置与敏感信息

学习阶梯：**L1 · 新手先学**

**方法 A｜VS Code 文件编辑步骤**

在 Explorer 打开现有 `.gitignore`，按实际项目追加规则 → 保存 → Source Control 看 Diff → `+` 暂存规则 → 检查后 Commit / Push。不要覆盖原有规则；下面是文件内容，不是 PowerShell 指令。已跟踪文件不会仅因保存规则而消失，需看下一节。

[[#2.5 .gitignore：忽略规则文件|.gitignore]] 的定义与基础例子见 [[#2.5 .gitignore：忽略规则文件|核心名词]]。这里讨论实际配置与安全边界：按项目选择忽略项，而不是复制一份“什么都忽略”的模板。

```gitignore
# 示例：本地凭据、环境文件
.env
.env.*
!.env.example
*.key
```

依赖、构建目录等应根据项目类型另行添加。针对截图中的 Obsidian 配置，是否忽略工作区状态取决于个人同步需要；不建议未经检查就忽略整个 `.obsidian/`。

已跟踪文件不会因加入 `.gitignore` 就停止跟踪。如果明确决定不再跟踪某文件，可用 `git rm --cached -- "文件路径"` 保留本地文件并暂存仓库中的移除，再提交；这不会清除旧历史。以上仅是说明，没有修改当前仓库的忽略规则。依据：[GitHub：忽略文件](https://docs.github.com/en/get-started/git-basics/ignoring-files)。

如果密钥已经提交或推送，先撤销 / 轮换密钥，再按需要协调清理历史；仅删除文件或加忽略规则不够。依据：[GitHub：移除敏感数据](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)。

### 10.2 已跟踪文件的补救：保留本机文件并停止跟踪

学习阶梯：**L2 · 日常熟练**

> [!question]
> 如果我一开始把垃圾文件传到Git上，形成[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]]历史了。现在我反悔了，想把这些垃圾文件丢到，不要在传到Github上了，怎么办？
> 
> （因为我就是这么干的，所以我会详细写这方面的东西）

补救办法：补上 [[#2.5 .gitignore：忽略规则文件|.gitignore]]，再让 Git 停止跟踪指定文件

> [!summary]
> **核心结论**
>
> **补写 `.gitignore` 仍然有用，但它不会自动取消之前文件的跟踪，也不会删除旧 Commit 里的内容。**
> 当前未被跟踪的文件，只要匹配忽略规则就会被忽略；已经被跟踪的文件，需要先用 `git rm --cached` 从暂存区移除跟踪项，再 Commit、[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] 这次变更。

```text
补写 / 完善 .gitignore
          ↓
对已跟踪且确认不再纳入版本管理的文件执行 git rm --cached
          ↓
检查暂存差异：忽略规则 + 指定路径的移除
          ↓
Commit → Push
          ↓
目标分支的后续版本不再跟踪这些路径，本机文件仍保留
```

这里看的是文件**当前是否被跟踪**，不是“历史上有没有出现过”；以前提交过、后来停止跟踪的文件，也可以按忽略规则处理。参考：[Git Ignore](https://git-scm.com/docs/gitignore)。

#### 10.2.1 停止跟踪，不等于删除本机文件

学习阶梯：**L2 · 日常熟练**

**方法 A｜先用 VS Code / GitHub 界面定位**

先在 VS Code 编辑并保存 `.gitignore`，但**不要在 Explorer 删除希望保留的本机文件，也不要用 Discard 删除它们**。内置 Git 没有统一的“停止跟踪但保留文件”图标，这个关键步骤需要终端；下面是几种命令的区别，不是让你全部执行。

**方法 B｜对应命令、精确诊断与边界**

| 图标                           | 含义                      | 大白话                      |
| ---------------------------- | ----------------------- | ------------------------ |
| [[#2.5 .gitignore：忽略规则文件\|.gitignore]]                 | 为未跟踪文件定义忽略模式            | 告诉 Git：以后这些文件先别收进版本记录    |
| `git rm --cached -- "文件"`    | 从暂存区移除该路径，保留当前工作区文件     | Git 的下一版不再带它，我电脑上仍留着     |
| `git rm -- "文件"`             | 从暂存区和工作区移除该文件           | 不只是取消跟踪，还会删掉本机文件；本场景不要误用 |
| `git rm -r --cached -- "目录"` | 递归移除目录中已跟踪的路径，保留当前工作区文件 | 这一整个目录以后别跟踪，本机先别删        |

其中 `-r` 表示递归处理目录；`--cached` 是**保留当前本机文件的关键参数**，不要漏写。命令若因暂存内容不一致等原因被拒绝，应先查 `git status` 和 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]，不要直接加 `-f`。参考：[Git Rm](https://git-scm.com/docs/git-rm)。

#### 10.2.2 命令行流程：只对确认过的路径操作

学习阶梯：**L2 · 日常熟练**

> [!warning]
> **执行前提**
>
> 下面是教学示例，不代表当前仓库确实包含或跟踪这些路径，也没有实际执行任何移除、提交或推送。
> 在仓库根目录操作，先确认仓库、分支和远程正确，保存 / 备份重要本地内容。工作区有无关改动时先处理，不要把它们混进这次提交。
> `.env` 可能包含凭据，不能简单当作垃圾文件：若真实密钥已泄露，先撤销或轮换密钥，再处理仓库记录，不能只依靠下面的流程。

**方法 A｜先在 VS Code 中操作或检查**

1. Source Control 核对仓库、分支、待提交内容；无关改动先处理。Fetch 后检查是否需要安全整合。
2. Explorer 打开 `.gitignore`，追加确认应忽略的规则并保存，避免存为 `.gitignore.txt`。
3. **内置图标没有完整替代 `rm --cached` 的入口。**打开集成终端，先核对已跟踪路径，再只对确认的路径停止跟踪；本机文件不应被删除。
4. 回 Source Control：删除条目已在 Staged Changes；点它们看 Diff，并把 `.gitignore` 的修改用 `+` 放入同一次提交。
5. 检查只有预期变更，再填说明 → Commit → Push；本地文件是否保留另行在 Explorer 核对。不要为了“让列表干净”继续 Add 这些要停止跟踪的文件。

如果严格要求只允许快进拉取，用下面 `--ff-only`，不把普通 Pull 图标当等价。

**方法 B｜对应命令行**

```powershell
git status
# 确认当前分支、暂存区和工作区状态；有无关改动时先停下来处理

git fetch
# 更新远程信息，不直接改工作区文件

git status
# 看与上游的差异；下面只在确实需要更新且工作区干净时执行

git pull --ff-only
# 只允许快进更新；如果分叉就停止，先按团队规则处理，不强行整合

# 在 VS Code 中编辑现有 .gitignore，按需要补充规则并保存
# 不要用新示例覆盖原有规则；也不要误存成 .gitignore.txt

git ls-files -- "node_modules" ".env" "debug.log" ".obsidian/cache"
# 先检查示例路径中哪些文件确实已被跟踪

git rm -r --cached -- "node_modules"
# 停止跟踪 node_modules 中已跟踪的文件，保留当前本机文件

git rm --cached -- ".env"
# 停止跟踪 .env，保留当前本机文件

git rm --cached -- "debug.log"
# 停止跟踪这个已跟踪的日志文件；*.log 规则不会自动移除旧的跟踪项

git rm -r --cached -- ".obsidian/cache"
# 只在该目录确实已跟踪且应该忽略时使用；保留当前本机文件

git status
# 检查准备停止跟踪的路径；它们通常在暂存区显示为 deleted / D

git add -- ".gitignore"
# 把新增或修改后的忽略规则也放进同一次提交

git diff --staged --name-status
# 查看暂存文件清单，确认只有预期的规则修改和路径移除

git diff --staged
# 查看实际差异；可能较长，按 q 可退出分页查看

git commit -m "添加 gitignore 并停止跟踪无关文件"
# 创建本地提交；先确认暂存区里没有无关内容

git push
# 在已设置正确上游且有权限时，推送到对应远程分支
```

[[#2.5 .gitignore：忽略规则文件|.gitignore]] 中按项目需要补充的规则示例：

```gitignore
node_modules/
.env
*.log
.obsidian/cache/
```

- 只运行适合自己项目的移除命令。某路径不存在、未被跟踪或本来就该保留时，跳过对应行；遇到 `pathspec ... did not match`，先检查路径与跟踪状态。
- 这里使用 `--ff-only` 比无条件 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Pull]] 更保守：远程没有新内容时可跳过 Pull；双方分叉时先停下处理。参考：[Git Pull](https://git-scm.com/docs/git-pull)。
- `.obsidian/cache/` 只是目录规则示例，不表示你的库里一定有这个目录；不要顺手忽略或取消跟踪整个 `.obsidian/`。

#### 10.2.3 为什么显示 D，本机文件却还在？

学习阶梯：**L2 · 日常熟练**

`git rm --cached` 已经把“下一次提交不再包含这些路径”的变化放进暂存区，所以 Git 会显示删除差异。这里删除的是下一版提交中的文件条目，不是说当前本机文件已经被删除。无需再对这些路径执行一次 Add；只需把 [[#2.5 .gitignore：忽略规则文件|.gitignore]] 一并暂存、检查并提交。

例如在执行对应移除操作后，可额外确认本机文件仍在：

**方法 A｜先在 VS Code 中操作或检查**

在 VS Code Explorer / Windows 文件资源管理器核对指定路径仍存在，只查文件是否在，不打开或输出 `.env` 凭据；再看 Source Control 的暂存删除条目。Explorer 的隐藏 / 排除规则可能影响显示，因此“看不见”不能单独证明已删，精确检查用下面命令。

**方法 B｜对应命令行**

```powershell
Test-Path -LiteralPath ".env"
# 如果该文件原本存在且保留成功，应输出 True；只检查存在性，不打印文件内容

git ls-files -- ".env"
# 成功停止跟踪后应没有该文件的输出
```

这是“当前这台机器保留文件”，**不是承诺其他协作者也永远保留它**：别人整合这次移除提交时，原先干净的已跟踪文件可能被删除。共享配置或不可再生资料应先通知团队并备份；需要的公共配置可另行保留不含秘密的模板。

#### 10.2.4 Commit / Push 后，旧历史会怎样？

学习阶梯：**L1 · 新手先学**

**先用界面核对：**Commit / Push 后，到 GitHub 切到目标分支看文件是否移除；再从历史提交打开旧版本，理解“当前不跟踪”和“旧历史还保留”不同。这里不需要为了核对就重写历史。

- 这次提交推送到目标分支后，该分支的新版本不再包含这些路径；**旧 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]] 仍可能查看到原内容，仓库体积也不会因此自动大幅缩小**。
- [[#2.5 .gitignore：忽略规则文件|.gitignore]] 不是数据擦除工具，也不是密钥保护工具。若目的是清除旧历史中的密码、Token 或大文件，需要另外评估历史清理流程并协调协作者，不要盲目重写或强推。
- 真正的凭据泄露应先撤销 / 轮换凭据；仅停止跟踪或删掉当前文件，不能让已经暴露的凭据重新安全。

参考：[GitHub：移除仓库中的敏感数据](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)。

> [!tip]
> **最短记忆版**
>
> **Ignore 管忽略规则，`rm --cached` 管停止跟踪，Commit 记录这次移除，[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] 同步到目标远程分支。保留本机文件，不等于清除了旧历史。**


### 10.3 高风险操作的底线

学习阶梯：**L1 · 新手先学；先记安全底线，不要求执行高风险命令**

> [!warning]
> **新手不要把这些当日常修复按钮**
>
> `reset --hard`、`clean -fd`、[[#2.8.1 整合与提交整理|Force Push]] 都可能造成内容丢失或覆盖共享历史。遇到推送被拒绝时，先 [[#2.6 Fetch、Pull、Push 与 Sync Changes|Fetch]] 并比较分支，不要先强推。对于已共享历史，优先考虑 [[#2.8.3 Restore、Reset、Revert 与 Reflog|Revert]]；复杂恢复先查 [Git Flight Rules 中文版](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md)。

## 11. 检查清单与双方法验收

学习阶梯：**L1–L4 · 先过提交检查，再按目标选择验收任务**

### 11.1 提交前检查

学习阶梯：**L1 · 新手先学**

- [ ] 当前仓库、当前分支正确。
- [ ] 已保存文件，并看过本次要提交的 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]。
- [ ] 没有误删、密钥、隐私资料或无关自动配置改动。
- [ ] [[#2.7 Changes、文件状态与 Graph|Staged Changes]] 只包含本次任务；文件移动包含旧路径删除和新路径加入。
- [ ] 提交说明与实际修改一致，相关检查 / 测试已完成。
- [ ] [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Commit]] 后知道是否还有未提交文件；[[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]] 后到 GitHub 确认目标分支。
- [ ] 需要更新 [[#2.3 仓库、分支与远程名词|main]] 时，另行审查并合并 [[#2.3 仓库、分支与远程名词|PR]]，而不是把 Push 当成合并。

### 11.2 团队协作实操验收

学习阶梯：**L3–L4 · 综合练习；先做协作任务，进阶任务后做**

**练习方式：先界面，后命令。**先照第 6、9 节的“方法 A”完成一次；重新准备练习仓库后，再照第 8、9 节的“方法 B”复现。没有完整图形入口的 Reflog / Bisect / 精确参数操作，允许“界面检查 + 终端执行”，不要编造按钮。

每项验收都应说清：点了哪个入口、对应什么命令、检查什么结果、失败时怎样停下。GitHub 的 PR 审查与 CI 结果还要到网页核对，不仅检查本地 Push 是否成功。

在**真实笔记库与工作项目之外**新建练习仓库，不含隐私数据。可用一个本地裸仓库和两个克隆目录模拟远程与两位开发者；也可使用自己的 GitHub 测试仓库。下面是本文设计的验收任务，不是“大厂认证标准”：

- [ ] 不看按钮，解释 `status -sb` 的两列，并把同一文件的两个修改分开提交。
- [ ] 从最新主线建分支，推送、开 [[#2.3 仓库、分支与远程名词|PR]]、处理审查，合并后更新本地主线。
- [ ] 用两个克隆制造同一分支分叉，读懂双方独有提交，再按要求整合，不丢另一边的工作。
- [ ] 分别制造一次 [[#2.8.1 整合与提交整理|Merge]] 冲突、[[#2.8.1 整合与提交整理|Rebase]] 冲突，能解决继续，也能放弃回到操作前状态。
- [ ] 用 [[#2.8.1 整合与提交整理|Amend]] / 交互式 Rebase 整理未分享提交，并解释为什么哈希改变、何时不能正常 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Push]]。
- [ ] 把普通修复 [[#2.8.1 整合与提交整理|Cherry-pick]] 到回补分支，处理依赖和冲突，检查来源记录并走 PR。
- [ ] 对已分享的错误普通提交创建 [[#2.8.3 Restore、Reset、Revert 与 Reflog|Revert]]，而不是强行删除历史。
- [ ] 在练习库中 Soft [[#2.8.3 Restore、Reset、Revert 与 Reflog|Reset]] 后用 [[#2.8.3 Restore、Reset、Revert 与 Reflog|Reflog]] 找到旧提交，建立救援分支，并说清不能恢复哪些未提交内容。
- [ ] [[#2.8.2 Stash 与 Worktree|Stash]] 保存并恢复含新文件的任务；另用 [[#2.8.2 Stash 与 Worktree|Worktree]] 完成一次并行小修复。
- [ ] 为一个可复现的问题定义好 / 坏判据，完成一次 [[#2.8.4 Log、Blame 与 Bisect|Bisect]]，并正确结束定位状态。

> [!summary]
> **真正需要形成的工作习惯**
>
> 操作前看 Status 和 [[#2.1 基础动作：Save、Stage、Commit、Push、Pull 与 Diff|Diff]]；协作前确认目标与规则；改写前留住旧提交；出错时先保存现场再诊断。
> UI 可以提高效率，命令行提供可解释、可复现的精确操作。能把两者结合，并在异常情况下安全收场，才比“记住几十条命令”更接近能独立工作的水平。

## 12. 实操记录：只把「代码管理」目录发布到 GitHub

学习阶梯：**L2 · 日常熟练；认识父仓库与独立子仓库的边界**

> [!important]
> **本节是真实执行记录，不是前面的教学模拟**
>
> 执行日期：2026-10-16（Asia/Shanghai）。本次已真实创建 GitHub 仓库、初始化本目录、提交并完成首次推送；随后打开 Obsidian 定位到本笔记，再补记本节。前文各教学示例中的“没有实际执行”仅描述那些示例，不代表本节没有执行。
> 本节已经通过第二次文档提交 [`b0aff13`](https://github.com/kairn-z71/git-vscode-workflow-notes/commit/b0aff13a73475b009a01505feffa4df3d1f95912) 同步到远程，并核对了远程 main 与本地一致。本次最终状态文字的校对同样在子仓库提交推送；最新提交以仓库历史为准，不把提交自身的哈希写进自身。

### 12.1 本次范围、结果与仓库地址

学习阶梯：**L1 · 先分清到底上传了哪个目录**

| 项目 | 本次实际结果 | 大白话 |
| --- | --- | --- |
| TA 父仓库 | 根目录已有 `.git`；当前分支 `ai-polished`，远程仍为 `https://github.com/kairn-z71/TA.git` | 原来的整库版本管理保留，不挪走、不重建 |
| 独立子仓库 | 在 `游戏开发 & 工作/杂项/代码管理/.git/` 新建 | 是的，这次在「代码管理」里又建了一个独立 `.git` |
| 新远程仓库 | [kairn-z71/git-vscode-workflow-notes](https://github.com/kairn-z71/git-vscode-workflow-notes) | 专门存这份 Git / GitHub / VS Code 学习资料 |
| 可见性 | **Private（私有）** | 用户未指定公开时，先避免把个人笔记直接公开 |
| 子仓库默认分支 | `main`；关联 `origin/main` | 这是子仓库自己的 main，与 TA 的分支不是同一套引用 |
| 上传内容 | 主笔记 1 篇、`Pictures/` 中图片 28 张、新增 `README.md` 和 `.gitignore`，共 **31 个文件** | 只发这个文件夹当前的内容，不带整套 TA |
| 首次提交 | [`4335697c2b81a6f8219d8cd1fd9e39ad3f58696f`](https://github.com/kairn-z71/git-vscode-workflow-notes/commit/4335697c2b81a6f8219d8cd1fd9e39ad3f58696f) | 一个新的根提交，不继承 TA 的旧提交历史 |
| 未上传内容 | TA 其他笔记、TA 的 `.git/`、`.obsidian/`、`.grimoire/` 等 | 没有把整个 TA 打包，也没有复制父仓库的管理数据 |

概念对应：[[#2.4 .git：本地仓库的管理数据|.git]]、[[#2.5 .gitignore：忽略规则文件|.gitignore]]、[[#2.3 仓库、分支与远程名词|仓库、origin 与分支]]。

### 12.2 我实际做了哪些检查与准备？

学习阶梯：**L2 · 先检查，再提交**

1. 检查 TA 的仓库根目录、当前分支、远程、HEAD 与暂存区：确认它原本就是父仓库，且没有需要我代为提交的暂存内容。
2. 检查「代码管理」：此前没有独立 `.git`，只有主笔记和 `Pictures/`，合计 29 个文件；检查文件均在目标目录内，没有通过符号链接把外部目录带进来。
3. 核对笔记的图片嵌入能在这个目录内找到对应文件，确认 `Pictures/` 一并发布，而不是只上传 Markdown 留下缺图。
4. 对文本检查常见 GitHub Token、私钥、云凭据等特征，没有发现匹配项。**这只是基础检查，不是绝对无敏感信息的保证**；截图也可能包含账户、路径等个人信息，所以默认私有。
5. 发现当前没有安装 `gh`。本次没有为了发布而安装 GitHub CLI，而是复用 Git Credential Manager 中已有的 GitHub 登录凭据，核验登录账户为 `kairn-z71`。
6. 检查新仓库名尚未占用，再通过 GitHub REST API 创建**空的私有仓库**，不自动生成远程 README，避免另起一套提交历史。认证秘密仅用于正常认证，没有写入笔记、README、仓库地址或 Git 配置。
7. 在本目录新增 `README.md`：说明学习资料入口、图片目录、Obsidian 专用语法的阅读方式和父子仓库边界。
8. 新增本目录自己的 `.gitignore`：忽略本地编辑器状态、临时文件和常见凭据文件。**没有改 TA 父仓库的忽略规则。**
9. 初始化独立仓库，将提交姓名、邮箱按 TA 当前已有值写入**子仓库局部配置**，没有改全局身份；为子仓库单独设置 `origin`。
10. 只暂存核对过的 31 个文件。首次空白检查出现 9 处已有 Markdown 空白格式告警；没有为消除这些告警而批量重写原笔记，复核范围后正常提交。

### 12.3 两种发布方式：图形复现与本次实际命令

学习阶梯：**L2 · 会用图标，也知道实际命令改了哪个仓库**

**方法 A｜VS Code 图形复现（说明等价思路，不声称本次逐个点击过）**

1. 在 VS Code 单独打开「代码管理」文件夹，先确认源代码管理当前选中的是这个目录，不是 TA 父仓库。
2. 尚未初始化时选 Initialize Repository；补好 README 和 `.gitignore`。
3. 查看 Changes，给本次目录里的文件点 `+`，检查 Staged Changes；不要提交 TA 的其他改动。
4. 填说明 → Commit → Publish to GitHub，命名 `git-vscode-workflow-notes`，选择 Private。本次已经创建过了，**现在不要再次 Publish 创建第二个仓库**，后续直接 Push。
5. 发布后到 GitHub 核对 `main` 的文件列表。按钮入口见 [[#3. VS Code 图标与菜单速查|VS Code 图标]] 和 [[#4. GitHub 网页图标与菜单速查|GitHub 网页]]。

**方法 B｜本次实际执行的 Git 操作**

下面从 TA 根目录指定子目录执行，避免把命令误作用到父仓库。记录供理解，**不要整段再次运行**。

```powershell
# 此命令已执行：在指定目录新建独立仓库，初始分支为 main
git -C "游戏开发 & 工作/杂项/代码管理" init --initial-branch=main

# 此前还将现有提交姓名、邮箱写入该子仓库的 --local 配置
# 具体邮箱不在笔记重复列出；没有修改 --global 配置

# GitHub 空仓库已经通过 API 创建；关联的是新仓库，不是 TA.git
git -C "游戏开发 & 工作/杂项/代码管理" remote add origin https://github.com/kairn-z71/git-vscode-workflow-notes.git

# 只暂存这几项；Pictures 中的图片均已核对
git -C "游戏开发 & 工作/杂项/代码管理" add -- .gitignore README.md "Git + Github + Vscode管理.md" Pictures
git -C "游戏开发 & 工作/杂项/代码管理" diff --cached --check

# 已创建的首次根提交
git -C "游戏开发 & 工作/杂项/代码管理" commit -m "docs: publish standalone Git and VS Code workflow notes"
git -C "游戏开发 & 工作/杂项/代码管理" push --set-upstream origin main

# 检查本地状态与远程 main
git -C "游戏开发 & 工作/杂项/代码管理" status --porcelain
git -C "游戏开发 & 工作/杂项/代码管理" ls-remote origin refs/heads/main
```

建远程仓库是 GitHub 平台操作，不是 `git init` 的附带效果。本次调用的是 `POST /user/repos`，关键参数为仓库名、`private: true`、`auto_init: false`；没有在命令行或本笔记中展示认证值。参考：[GitHub 建仓 API](https://docs.github.com/en/rest/repos/repos#create-a-repository-for-the-authenticated-user)、[Git Init](https://git-scm.com/docs/git-init)。

### 12.4 上传后做了哪些核对，以及怎样记到 Obsidian？

学习阶梯：**L2 · 不能只看到 Commit 成功就当作上传完成**

- 首次 Push 后，本地 `main` 与远程 `refs/heads/main` 都指向上表的 `4335697…`，并已设置上游。
- 通过 GitHub API 再次确认仓库为 Private、默认分支为 `main`，远程文件树有 31 个文件；未出现指向其他仓库的 gitlink，也没有上传 `.git/` 等管理目录。
- 首次推送后，子仓库工作区干净。补写本节后，已另外完成文档提交与推送；再次核对远程 31 个文件的 Git 对象哈希与本地提交一致。以后改笔记仍需重新提交推送，不能认为“自动保存到磁盘”就已经同步到 GitHub。
- 核对 TA 父仓库的 HEAD、分支、远程、Git 配置与暂存区索引未被改动；没有在父仓库 Commit / Push，没有将目录改成 Submodule，也没有执行父仓库的 `rm --cached`。
- 按用户要求调用 Obsidian 的打开链接，定位到 TA 库的这篇笔记；实际检测到窗口标题为 `Git + Github + Vscode管理 - TA - Obsidian 1.14.4`。笔记内容由文件工具补写，由 Obsidian 读取显示，并不是假装手工点了编辑器。
- 本节的同步方式是：补记实际结果 → 在**子仓库**提交文档更新 → Push → 再核对本地 HEAD 与远程 main。包含本节的最终提交可在 [仓库提交记录](https://github.com/kairn-z71/git-vscode-workflow-notes/commits/main) 中查看。

### 12.5 以后只更新这个仓库，应该怎样做？

学习阶梯：**L1–L2 · 最重要的是选对仓库**

**方法 A｜VS Code 操作**

单独打开「代码管理」目录，或在 Source Control Repositories 视图中明确选择它 → 修改并保存 → 检查 Diff → 选文件 `+` → Commit → Push。如果 VS Code 没自动发现嵌套仓库，单独打开这个目录即可，不要为了找到按钮就去重建 TA 的 `.git`。

**方法 B｜在 TA 根目录用明确的 `-C` 指定子仓库**

```powershell
git -C "游戏开发 & 工作/杂项/代码管理" status
git -C "游戏开发 & 工作/杂项/代码管理" diff

# 只暂存当前任务；有新增图片时再按实际路径追加
git -C "游戏开发 & 工作/杂项/代码管理" add -- "Git + Github + Vscode管理.md"
git -C "游戏开发 & 工作/杂项/代码管理" diff --staged
git -C "游戏开发 & 工作/杂项/代码管理" commit -m "docs: 更新代码管理笔记"
git -C "游戏开发 & 工作/杂项/代码管理" push
```

> [!warning]
> **嵌套仓库不是“自动从 TA 分家”**
>
> 父仓库之前已经跟踪的文件，可能仍同时被 TA 跟踪；对子目录创建新的 `.git`，或后来给父仓库加 `.gitignore`，都不会自动取消那些旧跟踪项。参考：[Git Ignore](https://git-scm.com/docs/gitignore)。
> 本次只完成独立发布，**没有删除 GitHub 上原 TA 仓库的既有内容，也没有清理它的旧历史**。若以后还要求“TA 从此不再跟踪这个目录”，需要另行确认并在父仓库做专门迁移；不要误删任何一个 `.git`，也不要未经确认把嵌套目录暂存成 gitlink。
> 新仓库默认私有。改为公开前还应检查截图中的个人信息及原有笔记内容；基础文本扫描不等于完整隐私审计。
