# Git 常用或常见的命令
- [1 git](#1-git)
- [2 配置用户名和邮箱](#2-配置用户名和邮箱)
- [3 初始化仓库](#3-初始化仓库)
- [4 查看文件的状态](#3-查看文件的状态)
- [5 gti add](#5-gitadd)
- [6 提交更行](#6-提交更新)
- [7 查看提交历史提交记录](#7-查看历史提交记录)
- [8 回退指定版本](#8-回退指定版本)
- [9 撤销对文件的修改](#9-撤销对文件的修改)
- [10 将纳入git管理的文件移除](#10-将纳入git管理的文件移除)
- [11 忽略某些文件，不需要被git管理](#11-忽略某些文件，不需要被git管理)
- [12 中文乱码解决](#12-中文乱码解决)
- [13 VSCode 配置git bash](#13-VSCode配置gitbash)
- [14 一些常见的命令](#14-一些常见的命令)
- [15 推送到远端](#15-推送到远端)
- [16 ssh配置（用国内gitee代替）](#16-打开gitee网站上查看ssh右下角怎么生成秘钥)
- [17 之后的每次推送](#17-之后的每次推送)
- [18 分支branch](#18-分支-branch)
- [19 合并冲突](#19-合并冲突)
- [20 远端分支](#20-远端分支)
- [21 推送本地的分支到远端](#21-推送本地的分支到远端)
- [22 将远端分支下载到本地](#22-将远端分支下载到本地)
- [23 删除远端分支](#23-删除远端分支)
- [24 初学者刚开始时，实际开发的情况](#24-实际开发的情况)
- [25 刚去公司的第一天](#25-去公司的第一天)
#### 1. git

```js
VCS  version  control system 版本控制系统
git 开源的分布式版本控制系统

// 作用： 版本控制，存档
```

#### 2. 配置用户名和邮箱

```js
git config --global user.name "用户名"
git config --global user.email "邮箱"

查看配置
git config --list 
查看全局配置
git config --list --global
```

#### 3. 初始化仓库

```js
1. 新建一个空文件夹，  右键 git bash here 
2. ===>  git init 
```

#### 4. 查看文件的状态

```bash
git status  
# 简写 
git status --short 
git status -s

红色： 工作区     绿色： 暂存区

?? 文件未跟踪
A  文件刚纳入跟踪
M  表示文件已经修改了

```

#### 5. git add 

```js
// 1. 将未纳入跟踪（管理）的文件，纳入管理
git add 文件名 
git add .

// 2. 将修改后的文件，（工作区中），添加到暂存区 
git add .

// ==> git add . 
```

#### 6. 提交更新（存档，记录一个版本）

```js
只要commit之后，这次版本就永久的记录下来了 

git commit -m "本次提交的信息"

// 每次提交的时候 

工作区  --->  暂存区  ---> git仓库
git add . 
git commit -m "update"

===> 跳过暂存区， 前提是文件已经被git纳入跟踪管理
git commit -am "跳过暂存区" 


// 修改最近一次提交说明 amend修正
git commit --amend -m "修改最近一次提交信息"

// 1. 先修改文件 
// 2. git add .  / git commit -m "提交信息"
// 3. git commit --amend -m "修改提交信息"
// 4. git log --oneline 查看
```

#### 7. 查看历史提交记录

```js
git log  详细信息
git log -2 查看两条
git log --oneline  简洁的查看  ==> 推荐

// 如果回退到某个版本之后，还想切换另一个版本 查看所有的提交记录
git reflog 
```

#### 8. 回退指定版本

```js
1. 回退
git reset --hard 版本id   

2. 将暂存区的文件 移动到 工作区
git reset HEAD .  （所有的文件）
```

#### 9. 撤销对文件的修改

```js
// 用的很少 
// 就是将工作区的文件，用仓库中当前版本替换掉。
git checkout 文件名 
// 类似ctrl + Z
```

#### 10 将纳入git管理的文件移除

```js
// 将纳入git管理的文件变为未跟踪的状态

git rm --cached 文件名  // 一个文件
git rm --cached -r .   // 所有文件 
git rm -r --cached .  // -r的位置可以交换
```

#### 11. 忽略某些文件，不需要被git管理

```js
// 创建一个新的文件 sercet.js
1. 创建一个.gitignore 文件
2. 将不需要纳入git管理的这个文件，写到里面  # 表示注释
3. git add .
4. git commit -m "添加gitignore文件"
5. 再修改这个文件， git status查看一下状态

----
.gitignore 只忽略没有跟踪的文件 如果文件已经纳入git管理了，则修改.gitignore无效 

// 解决方案
1. 在gitignore文件中写需要忽略的文件信息
2. 让所有纳入git管理的文件，都变为未跟踪
git rm -r --cached .
3. git add .  重新添加到暂存区 ，再提交
4. 提交当前的更新，备注说明 （添加了gitignore）
```

#### 12 中文乱码解决

```js
// 解决git status中文显示问题
git config --global core.quotepath false

```

#### 13 VSCode 配置git bash

```js
// Ctrl + j  
// cmd + j

Ctrl + shift + p  ==> 输入 JSON 

// where git 
// path 修改为Git bash的路径

"terminal.integrated.profiles.windows": {
    "PowerShell -NoProfile": {
      "source": "PowerShell",
      "args": [
        "-NoProfile"
      ]
    },
    "Git-Bash": {
      "path": "D:\\Program Files\\Git\\bin\\bash.exe",  
    }
  },
"terminal.integrated.defaultProfile.windows": "Git-Bash",
```

#### 14  一些常见的命令

```bash
cd 文件夹名字  进入某个文件夹
cd ..  返回上一层       ./ 一个点表示当前目录 .. 上级目录

clear 清屏 （git-bash）
cls  清屏  window黑色终端 cmd中 

# 查看文件内容
cat 文件名
# 创建文件夹
mkdir 文件夹名  
# 创建文件
touch 文件名 

# 查看文件列表
ls 
# 显示当前目录
pwd


使用 Vim编辑器 修改内容


vi 文件名  
# 进入vim编辑模式 
进入这个模式之后， 按键盘 i   ==》 插入模式 可以输入内容

# 退出？
1. 按ESC 
2. shift+:  => 冒号（英文）

:q   不保存退出
:q!  不保存强制退出
:w   保存
:wq   保存并退出
:wq!  强制保存退出
```

#### 15 推送到远端

```js
1. HTTPS   ==> 直接用链接推送  推送完之后要输入账号密码   
2. SSH    ==> 推荐的方式，密钥对 。

私钥  本地电脑上
公钥  需要配置到github / gitee / gitlab 平台上
```

#### 16 打开gitee网站上，查看SSH，右下角怎么生成秘钥

```js
1. 生成密钥对 
https://gitee.com/help/articles/4181#article-header0

ssh-keygen -t ed25519 -C "xxxxx@xxxxx.com"   改一下邮箱

2. 将公钥配置到gitee/github平台上
cat ~/.ssh/id_ed25519.pub

3. 验证是否配置秘钥成功 
ssh -T git@gitee.com‘

4. 先移除原来的origin名称 
git remote rm origin 
git remote -v 查看 

5. 重新关联仓库
git remote add origin git地址 （ssh）

6. 第一次推送
git push -u origin master
```

#### 17 之后的每次推送

```js
推送 把本地（电脑上的修改的版本更新  同步到远端）
// 修改代码，修改之后
1. git add . 
2. git commit -m "msg"
3. git push 
```



#### 18 分支 branch

```bash
# 1. 查看分支
git branch  
# 2. 新建一个分支 
git branch 新分支名字  （基于当前的分支，创建一个新分支）
# 3. 切换分支
git checkout 分支名字
# 4. 简写 创建一个分支，并切换分支
git checkout -b 新分支的名字 

# 5. 合并 
# 1. 在其他分支上修改的内容，一定要记得提交更新（记录）
# 2. 合并之前 切换到master分支上合并
git merge 分支名字

# 6. 删除分支
git branch -d 分支的名字  不能自己删除自己

# 下载项目（拉项目）
git clone  项目地址 （SSH / HTTPS）
```

#### 19 合并冲突

```js
1. 产生的场景 不同的分支，对同一份文件，（同一个位置）做了不同的修改，再合并这两个分支的时候，就会产生冲突。conflict

2. 在新分支中 找一个文件 记下位置，修改代码，
git add .
git commit -m "提交"
（目前处于刚创建好的分支）

3. 选择一个要保留的分支代码  
保存之后，
git add .
git commit -m "解决了冲突"

// 1. 采用当前的更改  2. 采用传入的修改  3. 保留两个分支的修改  4. 比较变更
// 还可以手动操作  ===> 不要忘记了删除哪些  ==== >>>> <<<<<<
```

### 20 远端分支

```js
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例   :重命名    原来名字:新名字
git push -u origin payment:pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化
git push -u origin payment
```

#### 21 推送本地的分支到远端

```js
1. 创建一个本地的分支并切换  local
2. 修改部分代码
3. git add . /  git commit -m "msg"
4. 本地这个local推送到远端 

git push -u origin 本地分支的名字:远端分支名字
git push -u origin local 
```

#### 22 将远端分支下载到本地

```js
1. 先删除本地的分支  
git branch -d 本地分支名字
2. git checkout 远端分支名字 
==> 下载远端分支，并切换到那个分支上去
```

#### 23 删除远端分支

```js
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称

# 示例
git push origin --delete pay
```

#### 24 实际开发的情况

```js
dev  开发环境
test 测试环境
master 主分支 （线上环境）

master-login --> 把这个分支的代码 合并到test分支上 ， 测试人员测试我们的代码功能等是否有问题

master-login  最后等待上线 。。  某个周五的晚上 
git push   ==》 把这个分支推送到远端仓库

gitlab 你的组长 帮你合并分支 
```



### 25 去公司的第一天

```js
1. leader 给你分配邮箱，账号
2. leader 给你一个 gitlab的地址， 同时，配套给你邮箱和密码    zxd@公司名字.com  密码 
3. 用公司给的邮箱密码，登录gitlab
4. 配置SSH， 方式和我们今天讲的一样   
5. 需要你的leader给你一个访问项目的权限 ，如果没有，是拉不了代码的   git pull(下载)
6. git clone 项目地址  下载项目。
7. 熟悉代码 
```



```js
1. git status
2. git add .
3. git commit -m "update"
4. git push 
5. 新建分支，基于master新建分支并切换到那个分支
git checkout -b 分支名 
6. 合并分支  git merge 

推送到远端仓库的时候，远端仓库的地址 
git remote add origin 地址名 
移除它
git remote rm origin
git remote -v 查看关联上了哪个分支 

代码回退 
git reset --hard id  
git reflog 
git log --oneline
```

