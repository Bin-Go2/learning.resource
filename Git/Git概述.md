
#### 什么是git？
分布式版本控制系统
1.分布式
2.版本控制

管理文件内容的变更，并记录下每个版本。

相较于本地版本控制系统（文件夹）和集
中化的版本控制系统

注意：所有的版本控制系统，其实只能跟踪文本文件的改动，二进制文件不行，只能知道个大概（例：文件大小变化）

#### 版本库 repository
文件仓库，在这里面的文件才可以被git管理
![226bf92f5a2899542c4c7c65cd5170b9.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p495)
* remote repository: 配有专用的服务器，为了多人共享而建立的版本库。
* local repository: 为了方便用户个人使用，在自己的机器上配置的版本库。

##### 创建版本库
1.新建一个版本库
2.复制远程版本库

```
#创建版本库
cd dest_dir
git init 
# 这样子的话 dest_dir文件夹下的所有文件都可以被管理，dest_dir变成Git可以管理的仓库
```

##### 添加文件到版本库
![12c3d36ee4c0d1a2d7367364825b5a86.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p496)

```
git add test.pdf
git commit -m '本次提交的说明'
git status  #查看工作区状态
git diff 文件名 $查看修改文件的修改信息 输入q可退出查看

一般工作流程：
首先输入git status查看工作区做了哪些修改，输入git diff 查看具体修改，确保没有问题之后进行git add 和commit

文件修改之后添加到版本库需要先add后commit两步操作
add 提交到暂存区，commit提交到当前分支（本地版本库）

```

#### 版本回溯
![3229214b110bb901ffdb8d207dd6f455.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p497)

* git通过版本编号和次序来进行版本的回溯

![6642e990061f767d3d35762b3fc471bb.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p500)

![d29ebb4affe71daf5fc5a546e010d75c.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p499)

```
git log #查看版本历史记录
git log --pretty=oneline #一行显示一个记录

head表示当前版本,使用git reset --hard 进行版本回退
1.git reset  --hard  HEAD^1 #退回上一个版本
  git reset  --hard  HEAD~n #退回上n个版本
2.git reset  --hard 版本号   #通过commit_id

#当回退到之前到版本的时候 git log后发现该版本之后的版本记录消失了，可以通过git reflog 查看记录 后根据版本号回退回去

git reflog #查看命令行中输入的命令历史记录
```

#### 撤销修改
Git跟踪并管理的是修改，而非文件
![0b2272a28bbb25bf74d35b3cbe4196d0.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p503)

![efe9ebb0ac363bfcba8ea56102f5c0e4.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p502)
```

1.文件尚未放到暂存区（即没有git add）
git checkout -- file_name ## 丢弃工作区的修改


2.文件已经放到暂存区
步骤1:git reset HEAD file_name  ## 将文件从暂存区取出来
步骤2:git checkout -- file_name ## 丢弃工作区的修改

3.文件已经从暂存区提交到了版本库
版本回退

==>git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区

```

#### 删除文件
![d3ddf81f32efdd78a41f46d214d70066.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p504)
```
删除文件也算是一种修改，所以git也会进行记录
1.确实要从版本库中删除该文件
步骤1:git rm file_name 
步骤2:git commit
2.删除错误（相当于撤销修改）
git checkout -- file_name
```

#### 远程仓库(Github服务器)
本地Git仓库和GitHub仓库之间的传输是通过SSH加密

![6a314db9546eb32c68793a293202be2f.png](evernotecid://8E70B44D-1DD4-44CE-925E-E2BC7B38721D/appyinxiangcom/18963837/ENResource/p505)

```
1、github上建一个版本库 
2、本地和远程关联 
git remote add origin  远程版本库地址
（更简单的操作为 直接复制远程仓库  git clone  远程版本库地址）
3、将本地版本库的内容传到远程库中
git push -u origin master
4、随后本地提交 不需要-u
git push origin master
```