# Git入门

[【2021年Git全集教程】大牛4小时带你精通Git玩转GitHub（最新版）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Zz4y1C7vg?vd_source=34f258c10dffd1ad2b0976714550c032)

> [Git 远程仓库(Github) | 菜鸟教程](https://www.runoob.com/git/git-remote-repo.html)

`Ctrl+Alt+G` 打开 git bash

## 初始化本地仓库

1. 本地创建一个文件夹 `GitResp` 保存仓库（非必须）
2. Git Bash Here (Ctrl + 滑轮 调整字体大小 / Options 设置)

git 命令与 linux 相同

```bash
git --version 
clear # 清屏
```



1. 设置签名： 设置用户名和邮箱：

   

   ```bash
   git config --global user.name "***" 
   git config --global use.email "***"
   ```

   

2. 本次仓库初始化 `git init` 生成 `.git` 隐藏文件夹

   **.git 文件夹下文件不要轻易修改**

## 常用命令

1. 在工作区创建一个文件
2. 将文件提交到暂存区 `git add <filename>`
3. 将暂存区提交到本地库 `git commit -m "comment" <filename>`
4. `git status` 查看缓存区状态 （修改本地文件需要用 add, commit 命令更新本地库）

**注意事项：**

1. 不放在工作区的文件，git 不进行管理
2. 即使放在工作区的文件，**必须通过 add，commit 命令操作将内容提交到本地库 git 才能管理**

### fg 命令

```bash
# Ctrl+Z挂起作业
# jobs查看挂起的作业
# fg 将后台的作业切换到前台

$ jobs
[1]+  Stopped                 vim Git学习笔记.md

$ fg 1
vim Git学习笔记.md

[1]+  Stopped                 vim Git学习笔记.md

Shinelon@DESKTOP-69E8U3H MINGW64 /e/坚果云/Notes/Git
$ fg
vim Git学习笔记.md

```

### log 命令

方法 1：`git log` 日志 (q 退出) 太多时分页(b 上一页)

方法 2：`git log --pretty=oneline`

方法 3： `git log --online` (更简洁)

方法 4：`git reflog` 多了信息：HEAD@{number} – 指针回到这个历史版本需要多少步

### reset 命令

前进或后退历史版本

1. `git reset --hard <hash>` (hash 在 HEAD@前)

   本地库指针移动的同时，**重置暂存区和工作区**

2. `git reset --mixed <hash>` 本地库指针移动的同时，**重置暂存区，工作区不变**

3. `git reset --soft <hash>` 本地库指针移动的，**暂存区和工作区都不动**

常用 `hard` 参数

### 删除文件

- 删除工作区中的 test2.txt `rm test2.txt`，或者选中文件手动删除
- 将删除操作同步到暂存区 `git rm test2.txt`
- 将删除操作同步到本地库 `git commit -m '删除test2.txt文件'`
- 找回本地库中删除的文件，实际上就是切换到历史版本

找回 **暂存区删除** 的文件：

```bash
git rm test2.txt
git add test2.txt
```

- 恢复暂存区的数据：`git reset --hard <HEAD_hash>` / `git reset --hard HEAD`

### diff 命令

- **比较工作区和暂存区文件** 更改工作区 test.txt 文件后，比较工作区和暂存区 test.txt 文件：`git diff test.txt` 比较工作区和暂存区所有文件差异：`git diff`
- **比较暂存区和本地库文件** 通过 **HEAD 指针** 比较：`git diff HEAD test.txt`
  通过 **hash 索引** 比较：`git diff <hash> test.txt`

## 分支

在版本控制中，使用多条线同时推进多个任务，这里面的多条线就是多个分支。



同时多个分支可以并行开发，互不影响，提高开发效率

如果有一个分支功能开发失败，可以直接删除该分支

### 操作分支

- 查看分支：`git branch -v`
- 创建分支：`git branch <branchname>` (当前所在分支由*表示)
- 切换分支：`git checkout <branchname>`

将 branch01 分支 **合并到主分支** 中：

- 切换到主分支中 `git checkout master`
- `git merge branch01**`

**在同一个文件的同一个位置修改时，会 出现冲突 问题 （mater|MERGING)**

解决：认为决定，留下需要的部分

`git add <filename>` `git commit -m "解决了冲突问题"` (**不能带文件名**)

## 远程库

### **克隆远程库**

```
git clone <远程库地址>
```

克隆作用：

- 初始化本地仓库
- 将远程库内容完整克隆到本地
- 替我们创建远程库别名(`origin`)

### 查看远程库

`git remote -v`：显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL

```bash
$ git remote -v
bakkdoor  https://github.com/bakkdoor/grit (fetch)
bakkdoor  https://github.com/bakkdoor/grit (push)
cho45     https://github.com/cho45/grit (fetch)
cho45     https://github.com/cho45/grit (push)
defunkt   https://github.com/defunkt/grit (fetch)
defunkt   https://github.com/defunkt/grit (push)
koke      git://github.com/koke/grit.git (fetch)
koke      git://github.com/koke/grit.git (push)
origin    git@github.com:mojombo/grit.git (fetch)
origin    git@github.com:mojombo/grit.git (push)

```

### 添加远程仓库

运行 `git remote add <shortname> <url>` 添加一个新的远程 Git 仓库，同时指定一个方便使用的简写：

```bash
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
pb	https://github.com/paulboone/ticgit (fetch)
pb	https://github.com/paulboone/ticgit (push)

```



现在你可以在命令行中使用字符串 `pb` 来代替整个 URL。 例如，如果你想拉取 Paul 的仓库中有但你没有的信息，可以运行 `git fetch pb`.

如果你使用 `clone` 命令克隆了一个仓库，命令会自动将其添加为远程仓库并默认以 “origin” 为简写。 所以，`git fetch origin` 会抓取克隆（或上一次抓取）后新推送的所有工作

#### 查看远程仓库

如果想要查看某一个远程仓库的更多信息，可以使用 `git remote show <remote>` 命令。 如果想以一个特定的缩写名运行这个命令，例如 `origin`，会得到像下面类似的信息：

```bash
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)

```

#### 远程仓库的重命名与移除

如果想要查看某一个远程仓库的更多信息，可以使用 `git remote show <remote>` 命令。 如果想以一个特定的缩写名运行这个命令，例如 `origin`，会得到像下面类似的信息：

```bash
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)

```



### 远程库修改的拉取操作

#### fetch+merge 操作

1. 抓取操作：fetch `git fetch <别名> <分支>` 只是将远程库内容下载到本地，工作区并没有更新 可以先检查远程库的文件 `git checkout origin master`，查看内容是否正确
2. 合并操作：merge
   - 切换到当前工作区主分支 `git merge chekout master`
   - 合并：`git merge origin master`

#### pull 操作

可以直接利用 pull 命令：

```
git pull origin master
```

`fetch+pull` 更保险一点

### **推送分支**

`git push <remote> <branch>`。 当你想要将 `master` 分支推送到 `origin` 服务器时（再次说明，克隆时通常会自动帮你设置好那两个名字）， 那么运行这个命令就可以将你所做的备份到服务器：

```bash
$ git push origin master  (目前github主分支改用main)
```

## 省略

29-31 团队合作部分

## SSH 免密登录

1. 进入都用户主目录中 `cd ~`
2. 执行命令 `ssh-keygen -t rsa -C <your github email>` 生成.ssh 文件夹 （三次回车确认默认值）
3. 打开./ssh/id_rsa.pub 文件，复制密钥
4. 密钥添加到 github 的 setting 中
5. 生成密钥后，就可以正常进行 push 操作了

在工作区进行如下操作：

```bash
echo "# guocfu.github.io" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:guocfu/guocfu.github.io.git
git push -u origin main
```

