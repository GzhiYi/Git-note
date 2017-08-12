# Git-note
quick to check the right instruction on git



## 1.Install Git
linux:  
```bash
$ sudo apt-get install git
```
Windows: 

install git windows package

after installed,type in userName and user.email
```bash
$ git config  --global user.name "You Name"
$ git config  --global user.email "You Email"
```

## 2.Create repo ..repo name: "learngit"
```bash
$ git init                                 //initialized package "learngit"
```

```bash
$ git add [fileName] 
$ git commit  -m "commit messages"
$ git add .                                //will add all modified files
```

## 3.版本回退
```bash
$ git log --pretty=oneline
```
展示commit记录，如下：

![commit](https://github.com/GzhiYi/Git-note/blob/master/img/git-log.png)
 
 ```bash
$ git reset --hard HARD^                   //一个^为回退上一版本，多个版本就多个^
$ git reset --hard 6af290200               //回退反悔，可以按commit id进行回退
$ git reflog                               //记录指令，可以找到曾经的commit id
```

## 4.撤销修改
```bash
$ git checkout -- readme.txt               //撤销readme.txt在工作区的修改，这在add之前操作。注意有 --
$ git reset HEAD readme.txt                //add了不好的修改到暂存区，没有commit就用这个命令撤销
```
当然，撤销暂存区的修改还得按第一步再撤销一次工作区的修改

## 5.删除文件
在图形界面删除了文件，git监测到会提示什么文件被删除，有两个选择:
```bash
$ git rm readme.txt                        //删除吧，文件不要了
$ git checkout -- readme.txt               //不删除了。注意 -- 左右空格不然报错
```

## 6.远程仓库 
### [先有本地仓库，后在远程创建空repo]
需要关联远程仓库，需要SSH Key
```bash
$ ssh-keygen -t rsa -C youremail@example.com
```
复制id_rsa.pub全部内容，用以关联
```bash
$ git remote add origin git@github.com:michaelliao/learngit.git            //本地仓库管理到远程仓库
$ git push -u origin master                                                //推送本地内容到远程仓库
```
注意： -u 用于远程仓库为空 右边的master为本地主分支，origin为远程主分支，然后两个主分支合并
之后简化命令: 
```bash
$ git push origin master
```
### [主要，先有远程仓库，再拉取]
```bash
$ git clone git@github.com:michaelliao/gitskills.git                        //本地克隆远程仓库
```
## 7.分支
```bash
$ git checkout -b dev                                                       //创建dev分支并切换至dev分支
$ git branch                                                                //查看当前有啥分支，带*为当前所在分支
```
分支合并
首先要去主分支[实际上你要合并到哪的那个分支]
```bash
①$ git checkout master
②$ git merge dev
```
注意：其实是将master分支的指针指向dev分支，默认master没改的意思，只适合单人工作，所以有Faster-forward的提示。合并后可以删除dev分支，需要再创建
```bash
$ git branch -d dev 
```
删除dev分支，当然也可以不删除

## 8.解决冲突
远程仓库内容修改后本地仓库也修改了，如果合并就会冲突。
查看冲突文件会有如下图示：
 	
手动查看修改的文件然后手动把想留下的留下来
手动解决冲突后可以将dev[举例]分支删除，再开发时可以pull下合并后的分支内容
注意：如果出现如下错误：

![merge-fault](https://github.com/GzhiYi/Git-note/blob/master/img/fetch.png)
 
意在没有把远端的fetch下来，先fetch下来再合并。
```bash
$ git log --graph --pretty=oneline --abbrev-commit                           //形象显示merge情况
```
 ![merge-result](https://github.com/GzhiYi/Git-note/blob/master/img/merge--result.png)
