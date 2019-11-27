<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-08-21 14:03:56
 * @LastEditTime: 2019-08-21 16:13:35
 * @Description: 
 -->
# <center>Git常用命令</center>

---

## 一、Git安装和基本用法
1.在官网下载安装即可。[git下载](https://git-scm.com/downloads)
2.设置账号和邮箱关联，账号和邮箱可以是码云、GitLab...的账号都行：

    git config --global user.name "Your Name"

    git config --global user.email "email@example.com"

生成公钥和秘钥：
在git命令行输入以下命令

    ssh-keygen -t rsa -C xxx@qq.com

然后命令行会出现如下代码：

    Enter file in which to save the key (/c/Users/xxxx_000/.ssh/id_rsa):       //此时我们什么都不需要操作，直接回车就好

    Enter passphrase (empty for no passphrase):            //此时要你输入码（可以为空，直接回车就好，也可以输入你的密码，这个密码在你最后把本地资源推送到github上面的时候回会让你填写密码，此时密码隐藏，你输入进去是看不到的）

    Enter same passphrase again: //再次确认密码（如果你第一次有输入密码，这次就再输一次，如果没有直接回车就行了）

    Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa. //生成的密钥

    Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub. //生成的公钥

    命令行输入cat ~/.ssh/id_rsa.pub，将得到公钥

3.克隆项目

    git clone url            //从仓库中复制url，按insert键粘贴

4.在对应的文件夹中添加新有项

    git status

5.提交

    git add mmm.sss          //mmm为文件名称，sss为文件拓展名（常用git add .）

    git commit -m "hhh"      //hhh为git commit 提交信息，是对这个提交的概述

    git log                  //用于查看提交日志

    git push                 //更新GitHub上的仓库

6.用git创建仓库

    mkdir nnn                //nnn为仓库名

    cd nnn                   //进入到nnn文件

    git init                 //初始化仓库
    
    ls                       //查看文件

    ls -ah                   //如果.git目录是影藏的话，可以通过这个命令查看.git目录

    git status               //查看仓库状态

    touch README.md          //创建READEME.md文件

    git add ERADME.md        //添加ERADME.md至暂存区

    git commit -m '提交的备注' //告诉Git把文件提交到仓库，此时是吧暂存区的所有内容提交到当前分支，可一次提交很多文件

    git commit "hhh"      //如果想要提交信息记录的更详细，请不要加 -m

    git log --pretty=short   //加--pretty=short 只显示提交信息的第一行

    git log ggg              //ggg是指指定的文件或目录，用于查看指定的目录、文件的日志

    git log -p               //查看提交所带来的改动

    git log -p ggg           //查看指定文件的改动

    git diff                 //可以查看工作树，暂存区，最新提交之间的差别

    git diff HEAD            //查看工作树与最新提交的差别

7.分支操作

    git branch               //显示分支一览表，同时确认当前所在的分支

    git checkout -b aaa      //创建名为aaa的分支，并且切换到aaa分支

    git branch aaa           //创建名为aaa的分支

    git branch -b aaa        //创建名为aaa的分支，并且切换到aaa分支

    git checkout aaa         // 切换到aaa分支

    git checkout -           //切换到上一分支

    git branch -d dev     //删除dev分支

8.合并分支

    git checkout master      //切换到master分支

    git merge --no--ff aaa   // 加--no--ff 参数可以在历史记录中明确地记录本次分支的合并

    git log --graph          //以图表形式查看分支

9.更改提交的操作

    git reset                //回溯历史版本

    git reset --hard         //回溯到指定状态，只要提供目标时间点的哈希值

    git log                          //显示从最近到最远的提交日志

    git log   --pretty== oneline     //显示log,但是不显示很多凌乱的信息

    q                                //显示log版本信息有很多，使用q键停止查看

    git reset —hard head^            //回退到上一个版本

    git reset —hard head^^           //回退到上上个版本

    git reset —hard head~100         //回退到之前100个版本

    git reset —hard +commit_id       //回到某个版本号的版本

    git reset — hard 版本号           //版本回退多次后需要恢复最新版本

    git reflog                       //查看曾经使用过的命令

10.推进历史

    git reflog                      //查看仓库的操作日志，找到要推历史的哈希值

    git checkout master

    git reset --hrad ddd            //ddd为要推进历史的哈希值

11.撤销修改

    git checkout -- test.html

12.删除文件

    rm test.index                  //可直接在文件管理中删除文件，要不用rm 命令去删除

    git rm test.html               //从版本库中删除

    git commit -m '删除 test.html文件'

    git branch -D <name>           //丢弃一个没有被合并过的分支，可以通过强行删除。

13.解决冲突

同一文件修改冲突，需要手动解决冲突后再提交。git status可查看冲突，根据标记可修改冲突部分，修改结束后再重新提交。

    git pull                      //拉取远程内容

    git log --graph               //命令可以看到分支合并图。

14.关联本地仓库和远程仓库

    git branch --set-upstream-to <branch-name> origin/<branch-name>

15.创建标签

    git branch 

    git checkout dev

    git tag v1.0                 //为当前需要打标签的分支打新标签

    git tag                      //查看所有标签

    git tag -a 指定标签信息 -m "blablabla..."            //可指定标签信息 

16.操作标签

    git push origin <tagname>                          //可以推送一个本地标签；

    git push origin --tags                             //可以推送全部未推送过的本地标签；

    git tag -d <tagname>                               //可以删除一个本地标签；
    
    git push origin :refs/tags/<tagname>               //可以删除一个远程标签。
