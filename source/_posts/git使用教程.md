---
title: git使用教程
date: 2026-05-02 20:17:50
tags:
---

## 1. 核心流程：Git 的“三个空间”

在操作指令前，必须先理解 Git 的工作逻辑。你的代码通常在三个区域流转：

1. **工作区 (Working Directory)**：你电脑里实际操作的文件目录。
2. **暂存区 (Staging Area / Index)**：准备提交的“临时存放点”。
3. **本地仓库 (Local Repository)**：最终存档点。

------

## 2. 基础指令集：从入门到提交

### 初始化与配置

在开始前，你需要告诉 Git 你是谁。

Bash

```
# 初始化一个 Git 仓库
git init

# 配置全局用户信息
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

### 文件提交操作

这是最常用的“三部曲”。

Bash

```
# 查看当前状态（哪些改了，哪些没暂存）
git status

# 1. 将文件添加到暂存区（. 代表所有文件）
git add .

# 2. 将暂存区内容提交到仓库（写下你的改动记录）
git commit -m "这次改了什么功能的描述"

# 查看提交历史
git log --oneline
```

------

## 3. 分支管理：并行开发的艺术

分支让你可以在不影响主线代码（Master/Main）的前提下，尝试新功能。

| **命令**                 | **描述**                             |
| ------------------------ | ------------------------------------ |
| `git branch`             | 查看所有本地分支                     |
| `git branch <name>`      | 创建一个新分支                       |
| `git checkout <name>`    | 切换到指定分支                       |
| `git checkout -b <name>` | **神级指令**：创建并直接切换到新分支 |
| `git merge <name>`       | 将指定分支的代码合并到当前分支       |
| `git branch -d <name>`   | 删除已合并的分支                     |

------

## 4. 远程协作：与 GitHub/GitLab 同步

当你需要把代码上传到云端，或者和队友协作时，你会用到这些：

Bash

```
# 关联远程仓库
git remote add origin <远程仓库URL>

# 第一次推送代码（关联并上传）
git push -u origin main

# 下载远程仓库代码（克隆）
git clone <URL>

# 拉取最新的远程改动并合并
git pull

# 推送本地改动到云端
git push
```

------

## 5. 进阶“后悔药”：撤销与回滚

人总会犯错，Git 最伟大的地方就在于它能让你“吃后悔药”。

- **撤销工作区的修改**（回到上一次 commit 的状态）：

  `git checkout -- <filename>`

- **撤销暂存区文件**（把 add 的文件拿回来）：

  `git reset HEAD <filename>`

- **彻底回滚到某个版本**：

  `git reset --hard <commit_id>`

  > **警告**：`--hard` 会抹除你所有未提交的代码，请务必谨慎操作。

------

## 💡 几条金牌法则

1. **频繁提交，小步快跑**：不要写了 1000 行才 commit 一次，这样出错了很难定位。
2. **描述清晰**：`commit -m "fixed bugs"` 是坏习惯，最好写成 `commit -m "fix: 修复了登录页面的手机号验证逻辑"`。
3. **先 Pull 后 Push**：在多人协作时，先拉取队友的代码，解决冲突后再上传。
