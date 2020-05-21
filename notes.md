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