# Git 学习笔记
**系统环境**
```
$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.12.6
BuildVersion:   16G2136
```
**配置相关**
> 使用 `git config` 命令控制配置文件中的变量  
> `项目设置` > `用户设置` > `全局设置`
###### 影响全局, 使用 `--system` 修改 `/usr/local/git/etc/gitconfig`
```
sudo git config --system user.name cheeroncode
sudo git config --system user.email code@autodo.xyz
```
###### 影响用户, 使用 `--global` 修改 `~/.gitconfig`
```
git config --global user.name cheeroncode
git config --global user.email code@autodo.xyz
```
###### 影响项目, 修改项目根目录下的 `.git/config`
```
git config user.name cheeroncode
git config user.email code@autodo.xyz
```
###### 设置 `Git` 的默认编辑器为 `VsCode`
```
git config --global core.editor "/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code --wait"
```
###### 检查配置, `Git` 会从全局,用户和项目配置读取所有可用信息
```
git config --list
```
###### 配置 Git 别名命令
```
echo "查看配置" && git config -l --global
echo "配置 git last 查看最近两次提交" && git config --global alias.last 'log -2 HEAD'
echo "删除配置" && git config --global --unset alias.last
```
**初始化仓库**
###### 在现有目录初始化仓库
```
git init
```
###### 如果目录非空,可暂存需要追踪的文件并提交
```
git add notes.md
git commit -m "准备开始学习Git命令前,对Git环境进行部分设置;"
```
###### 克隆现有的仓库 `GitLearn`, 并在当前目录创建同名仓库 `GitLearn`
```
git clone https://github.com/cheeroncode/GitLearn.git
```
###### 克隆现有的仓库 `GitLearn`, 并在当前目录创建新仓库名 `Learn`
```
git clone https://github.com/cheeroncode/GitLearn.git Learn
```
**暂存文件**
###### 添加文件到暂存区
```
git add notes.md && echo "添加 notes.md 文件到暂存区"
```
###### 取消暂存的文件
```
git reset HEAD notes.md && echo "取消暂存的 notes.md 文件"
```
**提交文件**
###### 正常提交
```
git commit -m "提交说明"
```
###### 提交时遗漏了文件或需要修改提交说明
```
git add xxx.txt && echo "添加忘了添加的文件 xxx.txt"
git commit --amend -m "新的提交说明"
```
**取消对文件的修改**
```
git checkout -- xxx.txt && echo "从仓库复制文件覆盖工作区的文件"
```
**检查当前文件状态**
###### 详细显示文件状态
```
git status
```
###### 紧凑显示文件状态
###### `??` 未跟踪, `A` 新添到暂存区, `M` 被修改,左暂存,右未暂存,可同时出现
```
git status -s
```
**`GLOB` 模式, 指的是 `SHELL` 使用的简化版正则表达式**
> 空行和 `#` 开头的会被忽略  
> `*` 匹配零个或多个字符  
> `?` 匹配一个任意字符  
> `!` 在模式上取反  
> `[abc]` 匹配字符 `a` 或者 `b` 或者 `c`  
> `[a-z]` 匹配范围从 `a` 至 `z` 的 `26` 个字符,也可以是数字  
> `**` 匹配任意中间目录, 如 `a/**/c` 可匹配 `a/c`,`a/b/c` 或者 `a/b/d/c`  
> `/` 以此字符开头防止递归,以此字符结尾表示目录  

**忽略配置 `.gitignore`, 添加无需 `Git` 管理的 `GLOB` 文件模式**  
```
# 不追踪所有的 .log 文件
*.log
# 但追踪 panic.log 文件
!panic.log
# 只追踪当前目录下的 config 文件
/config
# 不追踪 temp 目录下的所有文件
temp/
# 不追踪 doc 目录下的所有 .txt 文件,但追踪其子目录
doc/*.txt
# 不追踪 doc 目录下的所有 .txt 文件,包括子目录
doc/**/*.txt
```
**比较文件差异**
###### 比较工作区与暂存区文件的修改差异
```
git diff
```
###### 比较暂存区与最后提交时文件的修改差异
```
git diff --cached
git diff --staged
```
**删除已跟踪文件**
###### 添加临时文件
```
touch try_rm1.txt
touch try_rm2.txt
touch try_rm2.txt
```
###### 直接删除工作区和暂存区的 try_rm1.txt
```
git rm try_rm1.txt
```
###### 如果已修改过 try_rm2.txt, 需要加 -f 参数强制删除
```
git rm -f try_rm2.txt
```
###### 只删除暂存区,但保留工作区, 使用 --cached 参数
```
git rm --cached try_rm3.txt
```
**移动文件**
```
git mv try_rm2.txt try.txt
```
**查看提交历史**
```
git log && echo "查看提交历史,详细模式"
git l && echo "查看提交历史,紧凑模式"
git l -2 && echo "查看提交历史,紧凑模式,最近2次提交"
git l -2 -p echo "查看提交历史,紧凑模式,最近2次提交和提交差异"
git l --stat && echo "查看提交历史的简略统计信息"
git l --graph --oneline && echo "查看提交历史和分支,合并历史"
git l --since=1.days && echo "--after 查看 1天前 至 今 的所有提交"
git l --until=1.days && echo "--before 查看 开始 至 1天前 的所有提交"
git l -S "hello" && echo "查看添加或删除过 hello 字符串的所有提交"
git l --pretty=format:"%h - %an, %ar : %s" && "查看提交历史,自定格式"
```
###### log --pretty=format:"..." 格式
```
%H 提交对象（commit）的完整哈希字串
%h 提交对象的简短哈希字串
%T 树对象（tree）的完整哈希字串
%t 树对象的简短哈希字串
%P 父对象（parent）的完整哈希字串
%p 父对象的简短哈希字串
%an 作者（author）的名字
%ae 作者的电子邮件地址
%ad 作者修订日期（可以用 --date= 选项定制格式）
%ar 作者修订日期，按多久以前的方式显示
%cn 提交者（committer）的名字
%ce 提交者的电子邮件地址
%cd 提交日期
%cr 提交日期，按多久以前的方式显示
%s 提交说明
```
###### log 常用参数
```
-p 按补丁格式显示每个更新之间的差异。
--stat 显示每次更新的文件修改统计信息。
--shortstat 只显示 --stat 中最后的行数修改添加移除统计。
--name-only 仅在提交信息后显示已修改的文件清单。
--name-status 显示新增、修改、删除的文件清单。
--abbrev-commit 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。
--relative-date 使用较短的相对时间显示（比如，“2 weeks ago”）。
--graph 显示 ASCII 图形表示的分支合并历史。
--pretty 使用其他格式显示历史提交信息。可用 oneline，short，full，fuller 和 format（后跟指定格式）。
```
###### log 限制参数
```
-(n) 仅显示最近的 n 条提交
--since, --after 仅显示指定时间之后的提交。
--until, --before 仅显示指定时间之前的提交。
--author 仅显示指定作者相关的提交。
--committer 仅显示指定提交者相关的提交。
--grep 仅显示含指定关键字的提交
-S 仅显示添加或移除了某个关键字的提交
```
## 远程仓库的使用
**查看已经配置的远程仓库服务器**
###### 简要查看远程仓库的信息 git remote
```
git remote && echo "列出远程仓库服务器的简写名称"
git remote -v && echo "列出名称与对应的URL链接"
```
###### 详细查看远程仓库的信息 git remote show [remote-name]**
```
git remote show origin
```
**添加远程仓库**
###### 添加引用名为 server_dev 的远程库
```
git remote add server_dev https://github.com/cheeroncode/GitLearn
```
**修改远程仓库的引用名**
###### 重命名远程库 server_dev 的引用名
```
git remote rename server_dev server_new_name
```
**删除远程仓库的引用名**
```
git remote rm server_dev
```
**从远程仓库抓取数据**
```
git fetch server_dev
```
**从远程仓库抓取数据并合并到当前分支**
```
git pull server_dev
```
**推送到远程仓库**
###### 推送本地 master 分支到远程 server_dev
```
git push server_dev master
```

## 标签命令
**查看标签**
###### 列出已有标签 
```
git tag
```
###### 按模式列出标签
```
git tag -l 'v1.8.5*'
```
**创建标签**
###### 附注标签 推荐日常使用这个
```
git tag -a v_learn_remote_cmd -m "学习完远程仓库命令"
echo "显示附注标签 v_learn_remote_cmd 的信息" && git show v_learn_remote_cmd
```
###### 轻量标签
```
git tag v_light_tag
echo "显示轻量标签 v_light_tag 的信息" && git show v_light_tag
```
**查看标签**
```
git show tag_name
```
**删除标签**
```
git tag -d tag_name
```
**补打标签**
###### 补打标签,在创建标签命令末尾补上指定提交的hash字符串
```
git tag -a v_later_tag 4454b43 -m "对历史提交创建标签"
```
**推送标签**
###### 推送标签到远程库,默认 git push 时标签不会推送上传
```
echo "推送单个标签" && git push origin v0.1.1
echo "推送所有未推送的标签" && git push origin --tags
```
**补打标签**
###### 签出标签,不会像分支一样来回移动,在新标签分支上工作提交需要注意,还需要总结??
```
git checkout -b newtag_name v0.1.1
```
## Git 分支命令
```
echo "创建分支" && git branch ver0.1.0
echo "查看分支" && git log --oneline --decorate
echo "切换分支" && git checkout ver0.1.0
echo "第一次尝试在分支里新建文件" >> ver0_1_0.md
echo "暂存新文件" && git add ver0_1_0.md
echo "提交新文件" && git c -m  "在分支 ver0.1.0 提交文件"
```