---
layout: page
title: "gitmp"
date: 2015-12-21 17:11
comments: true
sharing: true
footer: true
---
在Linux上安装Git
==================================
首先,你可以试着输入<font color=#0099ff size=3 face="黑体">`which -a git`</font>看看系统有没有安装Git

如果你碰巧用Debian或Ubuntu Linux，通过一条<font color=#0099ff size=3 face="黑体">`sudo apt-get install git`</font>就可以直接完成Git的安装，非常简单。

老一点的Debian或Ubuntu Linux，要把命令改为<font color=#0099ff size=3 face="黑体">`sudo apt-get install git-core`</font>

查看正在使用的git版本<font color=#0099ff size=3 face="黑体">`git --version`</font>

配置环境变量编辑文件<font color=#0099ff size=3 face="黑体">`vim /etc/profile`</font>或者`vim ~/.bashrc`输入内容<font color=blue>`export PATH=/usr/local/git/bin:$PATH`</font>然后使其生效
<font color=#0099ff>`source /etc/profile`</font>

> 自动完成配置:
> 浏览器地址栏输入： [https://github.com/git/git](https://github.com/git/git "git源码下载").下载并解压git源码，
> 拷贝git-master/contrib/completion文件夹下的<font color=#0099ff>`cp git-completion.bash ~/`</font>
> 和<font color=#0099ff>`cp git-prompt.sh ~/`</font>，编辑<font color=#0099ff>`vim ~/.bashrc`</font>
> 加上以下内容<font color=blue>`. ~/git-completion.bash`</font>回车<font color=blue>`. ~/git-prompt.sh`</font>
> 保存退出，使其生效<font color=#0099ff>`source ~/.bashrc`</font>
> 

-----------------------------------------

#Git基本配置
> <font color=#0099ff>`git config --global user.name "Your Name"`</font>
> 
> <font color=#0099ff>`git config --global user.email "email@example.com"`</font>

-------------------------------------------------

#Git命令

> 增加用户：<font color=#0099ff>`git config --global --add user.name eoe`</font>
> 
> 查看用户：<font color=#0099ff>`git config user.name`</font>或<font color=#0099ff>`git config --get user.name`</font>
> 
> 删除用户：<font color=#0099ff>`git config --global --unset user.name`</font>或
> <font color=#0099ff>`git config --global --unset user.name eoe`</font>
> 
> 查看全部用户：<font color=#0099ff>`git config --list --global`</font>
> 
> 起别名：<font color=#0099ff>`git config --global alias.co checkout`</font>、
> <font color=#0099ff>`git config --global alias.lol "log --oneline --decorate --graph --all"`</font>
> 
> 初始化本地git仓库（创建新仓库）：<font color=#0099ff>`git init`</font>（git init /app/MyGit）
> 会创建一个.git文件夹
> 
> 创建裸仓库(不带工作区)：<font color=#0099ff>`git init --bare /app/MyGit`</font>
> 
> Git从远程服务器仓库克隆：<font color=#0099ff>`git clone git@github.com:git/git.git`</font>
> 
> 删除暂存区和工作区的文件：<font color=#0099ff>`git rm file`</font>
> 
> 查看当前版本状态：<font color=#0099ff>`git status`</font>
> 
> 还原删除的文件：通过查看当前版本状态先还原到暂存区，然后使用命令<font color=#0099ff>`git checkout -- <file>`</font>
> 还原到工作区
> 
> 只删除暂存区的文件：<font color=#0099ff>`git rm --cached file`</font>
> 
> 重命名文件：<font color=#0099ff>`git mv file1 file2`</font>其实际上并没有重命名一说，只是一系列的操作组合,本地操作
> <font color=#0099ff>`mv file1 file2`</font>然后添加到暂存区<font color=#0099ff>`git add file1 file2`</font>
> 
> 把整个工作区添加到暂存区：<font color=#0099ff>`git add .`</font>或
> <font color=#0099ff>`git add -A`</font>
> 
> 文件提交：<font color=#0099ff>`git commit -m "Initial commit"`</font>
> 
> .gitignore文件说明哪些不需要提交，eg:*.[oa]会不提交以.o或.a结尾的文件，*.pyc不提交以.pyc结尾的文件但是test.pyc需要提交，
> !test.pyc这样就行了，如果要忽略!test.py这样的文件，\!test.py

本地项目同步到coding.net
-------------------------------------------------
> <font color=#0099ff>`mkdir myCoding`</font>
> 
> <font color=#0099ff>`cd myCoding`</font>
> 
> <font color=#0099ff>`git init`</font>
> 
> <font color=#0099ff>`echo "# myCoding" >> README.md`</font>
> 
> <font color=#0099ff>`git add README.md`</font>
> 
> <font color=#0099ff>`git commit -m "first commit"`</font>
> 
> <font color=#0099ff>`git remote add origin https://git.coding.net/***/myCoding.git`</font>
> 
> <font color=#0099ff>`git push -u origin master`</font>

SSH公钥设置
-----------------------------------------------------
> <font color=#0099ff>`ssh-keygen -t rsa -C "your_email@example.com"`</font>
> 
> <font color=#0099ff>`eval "$(ssh-agent -s)"`</font>
> 
> <font color=#0099ff>`ssh-add ~/.ssh/id_rsa`</font>
> 
> <font color=#0099ff>`vim ~/.ssh/id_rsa.pub`</font>
> 拷贝里面的内容SSH公钥，公钥名称可以随便起
> 
> <font color=#0099ff>`ssh -T git@github.com`</font>验证github，
> <font color=#0099ff>`ssh -T git@git.coding.net`</font>验证coding.net

git clone
-------------------------------------------------------
> <font color=#0099ff>`git clone <版本库的网址>`</font>
> 
> eg:克隆jQuery的版本库<font color=#0099ff>`git clone https://github.com/jquery/jquery.git`</font>该命令会在本地主机生成一个目录，与远程主机的版本库同名
> 
> 如果要指定不同的目录名，可以将目录名作为git clone命令的第二个参数<font color=#0099ff>`git clone <版本库的网址> <本地目录名>`</font>
> 
> 克隆版本库的时候，所使用的远程主机自动被Git命名为origin。如果想用其他的主机名，需要用git clone命令的-o选项指定
> <font color=#0099ff>`git clone -o jQuery https://github.com/jquery/jquery.git`</font>
> 
> <font color=red size=3 face="黑体">注：在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”origin/master分支</font>

git remote
---------------------------------------------------------
> 为了便于管理，Git要求每个远程主机都必须指定一个主机名。<font color=#0099ff>`git remote`</font>命令就用于管理主机名。
> 不带选项的时候，git remote命令列出所有远程主机。
> 
> 使用-v选项，可以参看远程主机的网址<font color=#0099ff>`git remote -v`</font>
> 
> git remote show命令加上主机名，可以查看该主机的详细信息<font color=#0099ff>`git remote show <主机名>`</font>
> 
> git remote add命令用于添加远程主机<font color=#0099ff>`git remote add <主机名> <网址>`</font>
> 
> git remote rm命令用于删除远程主机<font color=#0099ff>`git remote rm <主机名>`</font>
> 
> git remote rename命令用于远程主机的改名<font color=#0099ff>`git remote rename <原主机名> <新主机名>`</font>

git fetch
-------------------------------------------------------
> 一旦远程主机的版本库有了更新（Git术语叫做commit），需要将这些更新取回本地，这时就要用到git fetch命令
> 
> <font color=#0099ff>`git fetch <远程主机名>`</font>
> 
> 上面命令将某个远程主机的更新，全部取回本地。
> 
> 默认情况下，git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。
> 
> <font color=#0099ff>`git fetch <远程主机名> <分支名>`</font>
> 
> 比如，取回origin主机的master分支<font color=#0099ff>`git fetch origin master`</font>
> 
> 所取回的更新，在本地主机上要用”远程主机名/分支名”的形式读取。比如origin主机的master，就要用origin/master读取
> 
> 在本地分支上合并远程分支<font color=#0099ff>`git merge origin/master`</font>在当前分支上，合并origin/master

git branch
-------------------------------------------------------
> 查看本地分支：<font color=#0099ff>`git branch`</font>
>
> 查看服务器分支：<font color=#0099ff>`git branch -r`</font>
> 
> 显示本地、服务器所有分支：<font color=#0099ff>`git branch -a`</font>
> 
> 创建本地分支：<font color=#0099ff>`git branch <new_branch_name>`</font>
> 
> 切换分支：<font color=#0099ff>`git checkout <branch_name>`</font>
> 
> 创建并切换分支：<font color=#0099ff>`git checkout -b <new_branch_name>`</font>
> 
> 创建切换分支并还原当前之前的一个提交：<font color=#0099ff>`git checkout -b <new_branch_name> HEAD~`</font>
>  
> 删除本地分支：<font color=#0099ff>`git branch -d <branch_name>`</font>
> 
> 删除远程分支：<font color=#0099ff>`git push origin --delete <branch_name>`</font>或
> <font color=#0099ff>`git push origin :<branch_name>`</font>
> 
> 建立追踪关系：<font color=#0099ff>`git branch --set-upstream master origin/master`</font>
> 这个已经废弃，马上删除
> 
> <font color=#0099ff>`git branch --set-upstream-to=<远程主机名/远程分支名> <本地分支名>`</font>

git pull
------------------------------------------------------------
> git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并，这等同于先做git fetch，再做git merge
> 
> 完整格式：<font color=#0099ff>`git pull <远程主机名> <远程分支名>:<本地分支名>`</font>
> 
> 如果远程分支是与当前分支合并，则冒号后面的部分可以省略：
> <font color=#0099ff>`git pull <远程主机名> <远程分支名>`</font>
> 
> 如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名：
> <font color=#0099ff>`git pull <远程主机名>`</font>
> 
> 如果当前分支只有一个追踪分支，连远程主机名都可以省略：
> <font color=#0099ff>`git pull`</font>

git push
---------------------------------------------------------------
> git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。
> 
> <font color=#0099ff>`git push <远程主机名> <本地分支名>:<远程分支名>`</font>
> 
> <font color=red size=3 face="黑体">注意，分支推送顺序的写法是<来源地>:<目的地>，所以git pull是<远程分支>:<本地分支>，而git push是<本地分支>:<远程分支>。</font>
> 
> 如果省略远程分支名，则表示将<font color=red>“本地”</font>分支推送与之存在”追踪关系”的远程分支（通常两者同名），如果该远程分支不存在，则会被新建
> 
> <font color=#0099ff>`git push <远程主机名> <本地分支名>`</font>
> 
> 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。
> 
> <font color=#0099ff>`git push origin :master`</font> 等同于<font color=#0099ff>`git push origin --delete master`</font>表示删除origin主机的master分支
> 
> 如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略，
> <font color=#0099ff>`git push origin`</font>表示，将<font color=red>“当前”</font>分支推送到origin主机的对应分支
> 
> 如果当前分支只有一个追踪分支，那么主机名都可以省略<font color=#0099ff>`git push`</font>
> 
> 如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push
> 
> <font color=#0099ff>`git push -u origin master`</font>
> 
> 上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了
> 
>     不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。
>     Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
> <font color=#0099ff>`git config --global push.default matching`</font>或者
> <font color=#0099ff>`git config --global push.default simple`</font>
> 
> 还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用–all选项
> 
> <font color=#0099ff>`git push --all origin`</font>
> 
> 上面命令表示，将所有本地分支都推送到origin主机
> 
> 如果远程主机的版本有更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用–force选项
> 
> <font color=#0099ff>`git push --force origin`</font>
> 
> 上面命令使用–force选项，结果导致在远程主机产生一个”非直进式”的合并（non-fast-forward merge）。除非你很确定要这样做，否则应该尽量避免使用–force选项
> 
> 最后，git push不会推送标签（tag），除非使用–tags选项
> 
> <font color=#0099ff>`git push origin --tags`</font>

git tag
-------------------------------------------------
> 让引用指向固定的提交
> 
> 先使用<font color=#0099ff>`git log --oneline --decorate --graph --all`</font>查看Hash码
> 
> <font color=#0099ff>`git tag <"tagName"> <Hash码>`</font>轻量级的本地引用,eg:<font color=#0099ff>`git tag "v0" alaba30`</font>,如果不带Hash的话，默认指向当前的commit
> 
> <font color=#0099ff>`git tag -a <"tagName"> <Hash码>`</font>带注解的，当你需要的时候可以推送到服务器上用于共享
> 
> <font color=#0099ff>`git tag`</font>查看当前的tag
> 
> <font color=#0099ff>`git show <tagName>`</font>
> 
> <font color=#0099ff>`git checkout <tagName>`</font>指向一个commit，而不是一个分支名，当切换回其他分支的时候，这部分历史就会丢弃掉，可以使用<font color=#0099ff>`git checkout -b <new_branch_name>`</font>创建一个分支并切换到这个分支上面，当你做了一些操作，只是git add -A，而没有git commit，这时候要git checkout <branch_name>切换到其他分支的时候会提示报错，提示你本地一些修改还没有被提交，这个时候可以使用 <font color=#0099ff>`git stash save -a <"stash_name">`</font>,-a参数可以把暂存区保存起来，你就可以切换到其他分支
> 
> <font color=#0099ff>`git stash list`</font>可以查看当前的tag里面的stash
> 
> <font color=#0099ff>`git stash pop --index <stash_name>`</font> ,index参数会把暂存区也还原回去，这个命令会把stash里面的记录给清除掉
> 
> <font color=#0099ff>`git stash apply --index <stash_name>`</font>,还原工作区和暂存区，但不删除stash里面的记录
> 
> <font color=#0099ff>`git stash drop <stash_name>`</font>用于清除stash记录
> 
> 如果有多个stash记录要清理使用<font color=#0099ff>`git stash clear`</font>

分支合并
----------------------------------------------------
> <font color=#0099ff>`git merge <branch_name>`</font>合并到当前分支
> 
> <font color=#0099ff>`git merge --abort`</font>放弃合并

历史记录
--------------------------------------------------
> <font color=#0099ff>`git log`</font>按空格或者f向下翻页，按b向上翻页，或者键盘上下键单行翻页，按q退出
> <font color=#0099ff>`git log -p`</font>输出每一个commit之间的差异信息
> 
> <font color=#0099ff>`git log --stat`</font>输出每一个commit之间差异的统计信息
> 
> <font color=#0099ff>`git log --oneline`</font>输出单行的信息
> 
> <font color=#0099ff>`git log --decorate`</font>输出commit引用的信息
> 
> <font color=#0099ff>`git log --graph`</font>输出图形化的历史信息
> 
> <font color=#0099ff>`git log --all`</font>输出所有分支的信息
> 
> <font color=#0099ff>`git show HEAD`</font>查看当前分支最新的提交
> 
> <font color=#0099ff>`git show <branch_name>`</font>
> 
> <font color=#0099ff>`git show <Hash码>`</font>
> 
> <font color=#0099ff>`git show --oneline --stat master^`</font>或者<font color=#0099ff>`git show --oneline --stat master~`</font>
> 
> <font color=#0099ff>`git show --format=%T master`</font>格式化输出master
> 
> <font color=#0099ff>`git diff`</font>输出工作区和暂存区的差异
> 
> <font color=#0099ff>`git diff --cached`</font>暂存区和历史提交的差异
> 
> <font color=#0099ff>`git diff> HEAD~2`</font>当前工作区与其他历史提交的差异
> 
> <font color=#0099ff>`git diff> HEAD~2 -- <file>`</font>当前工作区与其他历史提交的某个特定文件的差异
> 
> <font color=#0099ff>`git diff HEAD HEAD~2`</font>比较两个commit对象的差异
> 
> <font color=#0099ff>`git diff HEAD HEAD~2 -- <file>`</font>
> 
> <font color=#0099ff>`git diff --color-words`</font>
> 
> <font color=#0099ff>`git diff --word-diff`</font>

撤销修改
--------------------------------------------------------
> <font color=#0099ff>`git checkout`</font>还原工作区
> 
> <font color=#0099ff>`git checkout -- <file>`</font>
> 
> <font color=#0099ff>`git checkout <tag_name|Hash> -- <file>`</font>
> 
> <font color=#0099ff>`git checkout HEAD -- <file>`</font>还原工作区和暂存区到最新的提交
> 
> <font color=#0099ff>`git checkout HEAD~ -- <file>`</font>还原工作区和暂存区到之前的提交
> 
> <font color=#0099ff>`git reset`</font>还原暂存区
> 
> <font color=#0099ff>`git reset <tag_name|Hash> -- <file>`</font>
> 
> <font color=#0099ff>`git clean`</font>清理未添加进暂存区的文件(未跟踪文件)，默认不清理.gitignore里面的文件
> 
> <font color=#0099ff>`git clean -n`</font>查看要删除的文件
> 
> <font color=#0099ff>`git clean -f`</font>删除未跟踪文件
> 
> <font color=#0099ff>`git clean -n -X`</font>查看要删除的文件
> 
> <font color=#0099ff>`git clean -X -f`</font>清理.gitignore里面的文件，保留之外的文件
> 
> <font color=#0099ff>`git revert HEAD`</font>产生一个新的提交覆盖之前的提交所产生的修改

历史重写
-------------------------------------------------------
> <font color=#0099ff>`git commid --amend`</font>重写上一个提交历史记录
> 
> <font color=#0099ff>`git rebase <分支名>`</font>线性历史
> 
> <font color=#0099ff>`git rebase --abort`</font>撤销
> 
> <font color=#0099ff>`git rebase --continue`</font>有冲突的话先修改冲突，然后再`git add <file>`
> 
> <font color=#0099ff>`git reflog`</font>
> 
> <font color=#0099ff>`git reset --hard <HEAD@{num}>`</font>还原暂存区和工作区
> 
> <font color=#0099ff>`git reset --soft <HEAD@{num}>`</font>什么都不还原
> 
> <font color=#0099ff>`git reset --mixed HEAD~`</font>只还原暂存区
> 
> <font color=#0099ff>`git reset -10>`</font>最近10条HEAD引用




ruby安装
=================================================
主要注意在选择安装位置的时候一定要勾选上Add Ruby exeoutables to your PATH 这个选项，就是把ruby添加到环境变量,右击Git Bash Here，输入<font color=#0099ff>`ruby --version`</font>

ruby关联DevKit
============================================
安装DevKit,然后打开DevKit的安装目录

右击Git Bash Here输入命令<font color=#0099ff>`ruby dk.rb init`</font>,这时候如果没有出现
found RubyInstaller v2.1.3 at <filePath>(ruby目录)，
则需要编辑<font color=#0099ff>`vi config.yml`</font>添加上ruby的目录即可再执行<font color=#0099ff>`ruby dk.rb install`</font>

Octopress安装
==========================================
官网：octopress.org

克隆Octopress至本地

<font color=#0099ff>`git clone git://github.com/imathis/octopress.git octopress`</font>

安装依赖项
---------------------------------------

配置安装网址：<font color=#0099ff>`gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/`</font>

查看配置：<font color=#0099ff>`gem sources -l`</font>

修改<font color=#0099ff>`vi Gemfile`</font>,修改里面的source为：https://ruby.taobao.org/

其实直接执行下面两部就可以安装，但是由于上面的设置把安装网址改成了国内的，如果不修改有可能安装失败

执行安装：<font color=#0099ff>`gem install bundler`</font>

继续安装：<font color=#0099ff>`bundle install`</font>

安装并使用默认主题
---------------------------------------------------------

安装使用默认主题：<font color=#0099ff>`rake install`</font>

生成本地预览 <font color=#0099ff>`rake generate`</font>

本地开服务器：<font color=#0099ff>`rake preview`</font>

浏览器输入 localhost:4000这时打开会很慢，编辑\octopress\source\_includes\head.html,
把jquery的jar引用改成`<script src="//libs.baidu.com/jquery/1.9.1/jquery.min.js"></script>`

生成博客与单页面
=========================================================
新建博客：
--------------------
rake new_post["title"]

新建单页面：
----------------------------
	rake new_page[jikexueyuan]
	# creates/source/jikexueyuan/index.markdown

	rake new_page[jikexueyuan/page.html]
	# ctreates/source/jikexueyuan/page.html


部署网址至GitHub
========================================================
gitHub上面新建仓库：username.github.io

与本地Octopress目录绑定：

rake setup_github_pages

rake deploy


自定义网站域名：
===================================================
echo "domai.com" >> source/CNAME 

# OR

echo "www.domain.com" >> source/CNAME

使用子域名

 对于子域名（www.jikexueyuan.com）,创建CNAME记录指向charlie.github.io

使用顶级域名
 
对于顶级域名（jikexueyuan.com）,s使用A记录指向192.30.252.153(154)




