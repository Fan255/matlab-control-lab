# Git 与 GitHub 基本操作

本文中的命令均在 Windows PowerShell 中执行。MATLAB 程序和 `ver` 等 MATLAB 命令应在 MATLAB 中运行。

## 本地仓库与远程仓库
- 本地仓库：`D:\matlab-control-lab`。
- GitHub 仓库：[Fan255/matlab-control-lab](https://github.com/Fan255/matlab-control-lab)。
- 当前使用的分支：`main`。

Git 保存版本历史，GitHub 托管远程仓库。两份仓库不会自动实时同步；本仓库已经克隆，无需再次执行 `git clone` 或 `git init`。

## 开始工作前
先进入仓库并查看状态：

```powershell
cd D:\matlab-control-lab
git status
```

工作区没有未提交改动时，可以拉取远程更新：

```powershell
git pull --ff-only
```

`pull` 将远程更新带到本地。`--ff-only` 在分支发生分叉时停止，不会自动生成合并提交；遇到错误先检查原因，不强制覆盖已有工作。

## 修改完成后提交和推送
先查看修改：

```powershell
git status
git diff
```

`git status` 会列出新文件；`git diff` 主要显示已跟踪文件尚未暂存的修改，新文件内容需要自行打开检查。

确认当前目录内的改动都是本次需要提交的内容后，再加入暂存区：

```powershell
git add .
git diff --cached
git status
```

`git add .` 会暂存当前目录及其子目录中的新增、修改和删除。若存在其他工作，应只选择本次文件；例如只提交基础阶段说明时，可使用以下命令代替 `git add .`：

```powershell
git add 01_basics/README.md
```

检查暂存内容无误后，提交到本地历史，再上传：

```powershell
git commit -m "更新MATLAB学习记录"
git push
git status
```

提交说明应概括本次实际修改。`commit` 只保存在本地，`push` 成功后才上传到 GitHub。推送后可刷新仓库网页检查文件。

## 三个步骤的区别
| 命令 | 作用 |
|---|---|
| `git add` | 选定本次提交的文件内容，放入暂存区 |
| `git commit` | 将暂存内容保存为一次本地提交 |
| `git push` | 将本地提交上传到远程仓库 |

## 提交者身份
本仓库已设置提交者姓名和邮箱，可以查看：

```powershell
git config --local --get user.name
git config --local --get user.email
```

该配置保存在 `.git/config`，仅对当前仓库生效，用于提交署名。GitHub 登录认证另行处理；不要将密码或访问令牌写入仓库文件。

## 空文件夹与忽略规则
Git 不记录空文件夹。各学习目录放入 `README.md` 后，提交这些文件即可在 GitHub 上看到相应目录。

根目录的 `.gitignore` 用于忽略自动保存文件和生成缓存。它不会删除本地文件，也不会自动取消对已跟踪文件的管理。学习源码、模型、必要数据和代表性结果应按实际需要提交。

## 常见提示
- `Untracked files`：新文件尚未加入 Git 管理。
- `Changes to be committed`：文件已暂存，等待提交。
- `nothing to commit, working tree clean`：当前没有需要提交的改动；是否上传成功还要看推送结果和分支状态。
- `LF will be replaced by CRLF`：换行符转换提示，通常不妨碍提交。
- `Author identity unknown`：提交者身份尚未配置，先核对当前仓库的姓名和邮箱。
- 推送或拉取报错：保留完整报错，先检查网络、认证或分支状态，不使用强制推送或清理命令覆盖工作。
