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
> 比较工作区与暂存区文件的修改差异
```
git diff
```
> 比较暂存区与最后提交时文件的修改差异
```
git diff --cached
git diff --staged
```