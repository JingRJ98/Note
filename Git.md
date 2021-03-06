# Git
分布式的版本控制系统

(集中式的版本控制系统)SVN  
代码保存在同一服务器 便于管理  
集中式版本控制系统有可能服务器宕机丢失所有历史记录  
SVN保存的是差异，所需空间小 但是回溯麻烦  

客户端不只是提取最新版本的文件快照，而是把代码仓库完整地镜像下来，每一次的提取操作，实际上都是一次对代码仓库的完整备份 压缩算法比较好  

去中心化  
特点：  
1.直接记录快照，而非差异比较  
2.近乎所有操作都是本地执行  
3.时刻保持数据的完整性  
4.多数操作仅添加数据  
5.文件的三种状态  

# 初始化
检查已有配置

git config --list

配用户名与邮箱

git config --global user.name "Isaac"

git config --global user.email 239611376@qq.com

# 区域
工作区 
沙盒 一般不保存 可以修改


暂存区
保存 
版本库
最终

# 对象
Git对象

树对象

提交对象

# 初始化新仓库

git init

初始化，在当前目录下出现一个.git目录，所有的数据和资源都存放在这个目录中

# .git目录

## hooks
目录包含客户端和服务端的钩子脚本

## info
包含一个全局性排除文件

## logs
保存日志信息

## objects！
目录存储所有数据内容

## refs！
目录存储指向数据（分支）的数据对象指针

## config
文件包含项目特有的配置选项

## description
用来显示对仓库的描述信息

## Head！
文件指示目前被检出的分支

## index！
文件保存暂存区信息

# 常见linux命令
clear 清除屏幕

echo 打印信息
echo 'test content' > text.txt  创建一个txt文件

ll 将当前目录下的子目录子文件平铺在控制台

find 将对应目录下的子孙文件 子孙目录显示平铺在控制台

find -type f 将对应文件下的子孙文件显示在控制台

rm 删除文件

mv 重命名

cat url 查看地址对应的 文件内容

vim url 
按i进入编辑模式
按esc键 进入命令的执行

q! 强制退出

wq 保存退出

set nu 设置行号
 
# Git对象（文件快照）

key-value组成的键值对  
key是value的hash
键值对在GIt内部是一个blob类型


## 对一个对象进行简单的版本控制

### 创建一个文件并将其存入数据库

`echo "version 1" > test.txt`
`git hash-object -w test.txt`

两个命令可以使用`|`隔开

git hash-object -w fileURL 
生成一个key(hash值)：val(压缩后的文件内存)存到.git/objects
### 向文件中写入新的内容，并将其存入数据库

`echo "version 2" > test.txt`
`git hash-object -w test.txt`

### 查看数据库内容

`git cat-file -p hash`
拿对应的对象的内容

`git cat-file -t hash`
拿对应的对象的类型
## Git对象的存储是工作区与版本库的交互

# 树对象（项目快照）

我们可以通过update-index; write-tree; read-tree等命令来构建树对象并塞入暂存区

## 将数据库Git对象引入暂存区

首次加入--add
`git update-index --add --cacheinfo 100644 hash test.txt`
 向暂存区添加一条记录 让Git对象 对应上文件名

## 查看暂存区！

`git ls-files -s`

## 创建树对象(项目快照)存入数据库

`git write-tree`

##  将数据库中树对象引入暂存区

`git read-tree --prefix=bak hash`

## 创建新的嵌套树对象

`git write-tree`

# 提交对象（对树对象进行封装进行解释补充）

`echo "first commit" | git commit-tree 树对象hash`
生成一个提交对象存到.git/objects


# 高层命令（CRUD）
版本库是增量的 暂存区是覆盖的
git操作最基本的流程
1、创建工作目录 对工作目录进行修改
2、git add命令 ./
3、git commit -m "注释内容"

## Git操作最基本的流程

1.创建工作区，对工作区进行修改

2.`git add ./`
底层相当于 `git hash-object -w`  `git update-index`
相当于将工作区的文件转为Git对象存入数据库
再将它们从数据库引入暂存区

3.`git commit -m "注释内容"`
底层相当于`git write-tree` `git commit-tree`
相当于先创建树对象存入数据库
再创建提交对象存入数据库

## git init

初始化新仓库

## git add 路径

将文件转为Git对象存入数据（版本）库再引入暂存区

## git commit -m "注释"

创建树对象以及提交对象存入数据库

-a 修改文件跳过暂存区直接提交

## git status

查看文件的状态

工作区下所有文件有两种状态： 已跟踪 与 未跟踪
已跟踪文件有三种状态：已修改 已暂存 已提交

## git diff (--cached/--staged)

git diff
当前哪些文件修改后还未暂存

git diff --cached
当前哪些文件已暂存还未提交

## git log --oneline

查看历史提交记录

## git rm 文件名

工作区删除文件且将修改存入暂存区

## git mv 原文件名 新文件名

将工作区对应文件重命名且将修改存入暂存区

# 高层命令（分支）
分支的本质就是一个提交对象
HEAD是一个指针，默认指向master分支 切换分支其实就是切换

HEAD指向
每当有新的提交时，HEAD带着分支一起向前

## git branch 

查看分支列表

## git branch name
在当前提交对象上创建新的分支

## git branch 分支名 commithash

在指定提交对象上创建分支

## git branch --merged

查看哪些分支已经合并到当前分支

## git checkout -b 分支名

切换分支（当前commit对象）

## git branch -D 分支名

强制删除分支

## git log --oneline --decorate --graph --all

查看项目完整分支历史

## 切换分支的一些问题

1.切换分支时，如果当前分支有首次未暂存的修改或首次未提交的暂存，分支可以切换成功，但是会污染其他分支
    就是切分支的时候注意一下有没有保存 
    没有保存也可以切成功  但是会污染别的分支

    
2.切换分支改变三个位置：HEAD 暂存区 工作区

## git merge 分支名

快进合并（同一主线上）

典型合并（不同主线）

# Git实例
```js
git init 创建仓库
echo "a.txt v1" > a.txt  写文件
git status 检查状态（此时未跟踪）
git add a.txt 跟踪这个文件
git status 已经跟踪
git commit -m "1 commit for a.txt"  
提交 -m后添加提交的注释 请一定注意暂存区是否存在没有git add
vim a.txt 进入编辑a.txt
    按i进入编辑模式
    esc + : +wq保存退出

git checkout -b test 新建一个分支并切换过去
git checkout master 切换分支 （会删除b.txt 同时清除暂存区）

```
当遇到突发问题时，先给手头的添加跟踪并提交
git add./ 
git commit -m " 注释"

回到主分支 master
git checkout master
创建一个新的分支用于解决突发情况（hotbug）
git checkout -b "bug1"
提交后，回到原来的工作继续


# Git存储

## git stash

git stash会将未完成的修改保存到一个栈上

## git stash apply 

栈顶应用但不出栈

## git stash list

查看存储

## git stash pop

栈顶应用且出栈

## git stash drop

出栈，若不小心没用应用直接出栈 git fsck 找回悬空的hash git stash apply hash

# 撤回修改

## 工作区修改撤回

git restore filename

## 暂存区修改撤回

git restore --staged filename

## 提交对象修改注释

git commit --amend
git commit --amend = git reset --soft HEAD~ + git commit

# 重置

## Reset三部曲

### git reset --soft HEAD~

只修改HEAD和分支指向
HEAD以及分支移到前一个提交对象
HEAD~可改为指定hash

### git reset [--mixed] HEAD~

修改HEAD和分支指向以及暂存区

### git reset --hard HEAD~ 危险！

修改HEAD和分支指向，暂存区及工作区

### git reset --hard 与 git checkout 区别

checkout：改变HEAD，暂存区，工作区，但是它对于工作区是安全的
--hard：改变HEAD，分支，暂存区，工作区，强制覆盖工作目录，可能会造成工作区文件丢失

## checkout

### git checkout hash

改变HEAD，暂存区，工作区

### git checkout --filename

只改变工作区

# 数据恢复

## git reflog

找到需要恢复的提交对象的hash，在那个对象上开新的分支

# TAG

Git可以给历史中某一个提交打上标签，以示重要，比较有代表性的是使用这个功能来标记发布节点

## 列出标签

### git tag

## 创建标签

Git使用两种主要类型的标签：轻量标签 与 附注标签

### git tag v1.0 commithash

轻量标签像是一个不会改变的分支，它只是一个特定提交的引用

## 查看标签

### git show tagname

## 删除标签

### git tag -d tagname

## 检出标签

### git checkout tagname

问题，通过checkout检出标签会出现HEAD与分支头部分离的情况，所以要在检出的提交对象创建分支git checkout -b 分支名

# Git + ESlint + husky

package.json
```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "eslint": "eslint ./",
    "eslint:create": "eslint --init"
  },
  "husky": {
    "hooks": {
      "pre-commit": "npm run eslint",
      "pre-push": "npm test"
    }
  }
```

或者
npx eslint --init
npx eslint 目录

# 远程仓库GitHub

## 团队协作

1.项目经理在GitHub初始化远程仓库

2.项目经理创建本地仓库
    git init （初始化本地仓库
    git remote add 别名 仓库地址 （连接远程仓库
    git config user.name（修改用户名邮箱
    git add ./
    git commit

3.项目经理推送本地仓库到远程仓库
    git push -u 别名 分支 （本地生成远程跟踪分支

4.项目邀请成员

5.成员克隆远程仓库
    git clone 仓库地址 （本地生成.git 默认为远程仓库配别名 origin，创建一个跟踪 origin/master 的 本地 master 分支

6.成员工作
    修改源码
    git add ./
    git commit
    git push -u 别名 分支 （本地生成远程跟踪分支

7.项目经理更新修改
    git fetch 别名（修改同步到远程跟踪分支上
    git merge 远程跟踪分支

## 本地分支 跟踪 远程跟踪分支

### 1.新建本地分支跟踪远程跟踪分支

git checkout -b 本地分支名 远程跟踪分支名
git checkout --track 远程跟踪分支名

### 2.在已有本地分支情况下

git branch -u 远程跟踪分支

跟踪之后可直接在本地分支下使用 
git push git pull 与远程库进行交互

git branch -vv 查看所有跟踪分支

## 删除远程分支

### git push origin --delete 远程分支名

### git remote prune origin --dry -run

列出远程分支删除后仍然存在的远程跟踪分支

### git remote prune origin

清除无用的远程跟踪分支

# pull request

# SSH

ssh-keygen -t rsa -C 邮箱
