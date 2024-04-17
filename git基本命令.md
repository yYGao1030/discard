[Git - 下载 (git-scm.com)](https://git-scm.com/downloads)

git可用于很多代码托管平台，包括但不限于队库，像一些大型免费平台也是同样的原理,能备份代码，大胆改bug，反正能够复原代码，也便于协调工作，最后也能在队库中留有足迹

-   Github（全球最牛的开源项目托管平台，没有之一）
-   `Gitlab`（对代码私有性支持较好，因此企业用户较多）
-   `Gitee`（又叫做码云，是国产的开源项目托管平台。访问速度快、纯中文界面、使用友好）
-   A&T（独家设计，版权所有）

# 一. 基本命令

```bash
git init  # 初始化新的 Git 存储库
git add .  # 添加任务文件到暂存区
git commit -m '注释'  # 提交暂存区文件到本地仓库

git push <远程主机名> <本地分支名>:<远程分支名>  # 推送到远程服务器
			origin		main
git push <远程主机名> <本地分支名>  # 如果本地分支名与远程分支名相同，则可以省略冒号：

git branch “new branch”  # 创建新分支
git checkout “new branch”  # 切换分支
git branch -d “new branch”  # 删除分支
git remote add [shortname] [url]  # 添加远程版本库
```

# 二. 一般推送流程 （首次）

初始化 -> 添加任务文件到暂存区 -> 提交暂存区文件到本地仓库 -> (创建分支) -> 添加远程版本库 -> 提交到远程仓库

```bash
git init  # 初始化(首次使用，记得加.gitignore文件)
git add . # 添加任务文件到暂存区
git commit -m "注释"  # 提交暂存区文件到本地仓库
git branch "new branch"  # 创建分支
git remote add origin https://github.com/...... # 添加远程版本库
git push -u origin main # 推送到远程服务器（-u为首次推送，之后推送应去除）

 #此后推送可直接从工作区提交到本地仓库直接推送
git commit -a -m '注释'
git push oorigin main
 #便可直接更新版本
```

# 三. 分支

```bash
git branch  # 列出分支
>>> (输出)
* master
↑ 有 * 表示当前分支为 master

git branch [new branch name]  # 创建新分支
git checkout [branch name]  # 切换分支
git merge  # 合并分支
git branch -d [branch name]  #
删除分支
git push origin -d [branch name]  # 删除远程仓库分支
# 分支冲突 .... 
```

# 四. 远程仓库相关

```bash
git remote -v  # 显示所有远程仓库
git remote show [remote]  # 显示某个远程仓库信
git remote add [shortname] [url]  # 添加远程版本库
git remote rm name  # 删除远程仓库
git remote rename [old_name] [new_name]  # 修改仓库名

git push <远程主机名> <本地分支名>:<远程分支名>  # 推送到远程服务器  
git push <远程主机名> <本地分支名>  # 如果本地分支名与远程分支名相同，则可以省略冒号：
git push origin -d [branch name]  # 删除远程仓库分支
```

# 五. 其他(关于一些错误信息的解决)

在第一次提交后，之后的提交提示

```
Everything up-to-date
branch 'branch' set up to track 'origin/branch'.
```

可以尝试一下 三种方法之一 (是按简单程度，没有按使用效果排)，或者直接看这个博客

https://blog.csdn.net/boysky0015/article/details/78160825  (这个就是第三种方法)

1. 先切换到该分支再提交

2. 强制提交

    ```
    git push -u origin [branch name] -f
    ```

    这种没有试过

3. 创建新分支 提交到新创建的分支 合并两个分支(这种应该可以)

    ```bash
    # 创建新分支
    git branch dev # 创建一个dev分支  dev是分支的名字 可以随便命名
    
    # 添加到暂存区
    git add .
    
    # 提交到版本库，也就是当前分支
    git commit -m "注释"
    
    # 提交到远程仓库
    git push origin dev
    
    # 切换到mater分支
    git checkout master
    
    # 把dev分支合并到maste上
    git merge dev
    
    # 最后提交到远程仓
    git push -u origin master
    
    # 可以选择是否删除之前创建的新分支
    git push origin -d dev  # 删除远程仓库分支
    ```


# 六.回退历史版本

1.获取上次推送的版本到工作区（代码改崩直接复原）

```bash
git pull origin main
```

2.获取历史版本（路线不对直接回归）

```bash
 #获取远程仓库历史版本号（commit后的一长串）
git log

 #复制想退回的历史版本号
git reset --hard 历史版本号 #工作区返回历史版本并在下次推送时删去历  史版本后的版本 
 #修改完后添加到暂存区
git add .

 #从暂存区提交到本地仓库
git commit -m '注释'

 #版本号不同，需要强推-f给远程仓库
git push -f origin main
 #远程仓库将显示到回退历史版本的下一版
```

3.下载远程仓库（好的代码直接克隆）

```bash
git clone 仓库网址
```

