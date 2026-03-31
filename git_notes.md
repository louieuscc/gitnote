# All about GitHub



> *从链接可下载Git Desktop*
> https://github.com/apps/desktop?ref_cta=download+desktop&ref_loc=installing+github+desktop&ref_page=docs
> *也可直接访问注册后的目录网址，如：*
> https://github.com/louieuscc/



# 通过GitBash以命令行方式操作Github

*Git可由此下载 (https://git-scm.com)*



**Git运行流程：**

先进入本地工作区（例如user/louie/）。操作如新建、编辑等指令，并保存到本地工作区

--> 然后`git add`，存入本地暂存区 

--> 再`git commit`，加注释并存入本地库

-->最后`git push`，提交至远程库  



**1.GIT安装后即有GitBash的CLI窗口**

   Windows系统会生成Bash特有图标，命令行提示以$开头

   IOS系统中，GitBash与shell共用CLI窗口，无专有图标



**2.创建新目录mygit**

  `$ mkdir mygit`创建

  `$ cd mygit` 进入该目录
  `$ pwd` 显示当前目录路径
  `$ git init`将该目录变成GIT可管理的库



**3.新建文件并添加入暂存区**

- 先用VSC写一个新文件，保存至先前的mygit目录下（可能需手动添加扩展名.txt）

- 用命令`$ git add 新文件名`，将此文本存入暂存区（Staged）

- `$ git commit -m "<简要说明此次动作>"`，为此次动作加注解 (bash可能问who are you, 按提示输入user email和user name即可)

- 用ls命令查看当前目录是否已有该文件
  
    *注：勿使用Windows记事本编辑任何文本文件，用VS Code编辑之*
    
    

**4.对已有文件进行修改并存至暂存区**

- 在VS Code中更改文本，改后可随时存盘，但并未提交（commit）

- 在Git Bash运行命令`$ git status`看状态，系统会提示文件已修改，但并未提交

- 运行`$ git diff`，可查看修改详情 (仅刚对文本进行更改后，git diff命令才有效。如已提交将不会显示任何信息)

- 先运行`$ git add <file name>`进行提交，再运行`$ git commit -m "<commit>"`进行注释

- 再运行命令`$ git status`查看状态，系统说当前无需要提交之修改，且工作树是干净的 (nothing to commit, working tree clean)

- 如需一次提交多个文件，可用：`$ git add <file-1> <file-2> <file-3>...`    且多个文件提交后只需commit一次

  *注：Git为大小写敏感，编辑时务必注意文件名的大小写
           如果当日对文本会进行多次修改，只需在当日结束前一次性提交和注释，无需多次提交*
  
  

**5. 查看文本被历次修改的记录及Commit ID号**

- `$ git log`命令，即可显示历次修改的注释内容，顺序由新至旧，当前最新版本以HEAD表示，且每个commit都有一个很长的ID号。

- `$ git reflog`命令，可显示历次reset及每个版本的commit ID号。故即使关闭Git Bash仍可查到每个ID号的前7位
  
    *注：运行git log后，必须按字母键q才能退出log状态并回到GitBash命令行*

   

**6. 将某版本改设为当前最新版（HEAD）**

- 如想将之前一步的旧版本设为最新版本，用命令`$ git reset --hard HEAD^`。^表示前一个，如要之前第二个，则为^^。
       更多位可用数字，如HEAD~100
   
- 用git log发现，前一旧版已被设为最新HEAD，而且被替换的先前最新版本已消失。

- 如果想找回消失的那个版本，可在Git Bash窗口中找到该版本的commit ID号，记住前五位。再运行命令`$ git reset --hard commit_id`, 即可又将该版设为最新HEAD。commit_id只需前5位即可。

- 用git log查看，该版已显示并又成为HEAD
  
   *注： 命令git reset --hard commit_id，可将历次任一版本设置为最新HEAD*
   
   


**7. 撤消修改**

- 如果对文本作了一次修改，但并未add也未commit，现在要立即撤销修改，可用命令`$ git restore --文件名`
       然后用git status查看，系统显示工作树clean，即撤消修改完成。
   
- 如果对文本作了修改，且已经add(staged)但未commit，现在要撤销修改，可用命令`$ git restore --staged文件名`
       再用git status查看，发现系统称该文件并未add，即已退出stage目录区。
       此时再用命令`git restore --文件名`，然后用git status查看，系统显示工作树clean，完成撤消。
       *注：可从VS Code查看原文件代码，发现需要撤消的修改已经消失*
   
- 如果将修改既add也commit了，就用命令`$ git reset --hard HEAD^`，恢复到上一版本，修改自然消失

   

**8. 删除文件、重命名文件**

- 可直接在文本所在文件夹删除。如果误删想恢复，可用命令`git checkout -- 文件名`。
- 另也可用命令`git rm <文件名>`也可删除文件，然后再commit。该文件即被永久删除，不可恢复。
- `git mv <文件名>`可移动或重命名文件，之后再commit。
- 远程库的文件如需删除，最好在Github上进行。



**9. 建立远程库并上传文件至远程库**

- Github远程库需先注册，再在Git bash上用`$ ssh-keygen -t rsa -C "youremail@example.com"`，创建SSH KEY。
       此KEY位于本机c:\usr\louie\.ssh\中，内有id_rsa.pub及id_rsa两文件 
   
   *注：有时此二文件可能创建到其它目录下，务必拷贝回.ssh正确文件夹中。Mac上的SSH 目录的位置是 `~/.ssh`*
          *拷贝id_rsa.pub里的文本，粘贴至远程Github设置里的SSH key设置中即可。*
   
- 在Github上新建一个库（Repository），名字与本机已有库相同。然后将二者建立关联：

   1. 在本地mygit库下运行命令`$ git remote add origin git@github.com:louieusc/mygit.git `  

         *注：louieusc是我在Github的ID*

   2. 首次把本地库的所有内容推送到远程库上并建立关联，用命令:
         `$git branch -M main`(切换至分支main)
         `$git push -u origin main`(当前目录所有文件都推到远程库的默认分支main内)
         用命令`$git push -u origin master`   (注：当前目录所有文件都推到远程库的指定分支master内)
         *注：如需删除远程某库，在网站GitHub.com上进入repository页面，在需删除的库下点击Settings，在Danger Zone中点击Delete this repository*

         

**10. 关于多部主机向远程同一目录库发送提交**

- 如果多部主机都需向远程同一Repository发送文件或commit，此时远程主机的repository会自动产生两个branch，一个名为
        master，另一个名为main。
- 平时把本地库所有最新内容推送至远程库，命令`$ git push origin <branch name>`。分支名为master或main。
- 如果多部主机向远程不同Repository发送文件，则远程主机的repository只分别产生各自的branch。



**11. 克隆远程库**
克隆（Clone）是将远程库的所有文件和版本历史复制到本地的操作。初始项目文件可在远程库建立，然后各地主机从远程克隆至本地。好处：

- 本地开发：克隆远程仓库后，开发人员可以在本地进行修改、测试和重构，而不会影响远程仓库的内容。这使得开发过程更加灵活和安全。 
- 版本控制：克隆操作会将整个仓库的版本历史复制到本地，开发人员可以随时查看和管理代码的历史版本，便于追踪更改和回滚。 
- 代码浏览：通过克隆，开发人员可以方便地浏览和查看远程仓库的代码，了解项目的结构和功能。 
- 协作开发：在团队开发中，每个成员可以从远程仓库克隆一份代码，进行独立的开发和测试，最后再将更改推送回远程仓库。 

   1. 先在Github建立一个新库，命名为gitnote, 并勾选Initialize this repository with a README选项。
      此新库的SSH地址为：git@github.com:Louieuscc/gitnote.git。它的HTTPS地址为：https://github.com/Louieuscc/gitnote.git
   2. 开启GitBash，进入c:\usr\louie
      C. 运行命令`git clone git@github.com:louieuscc/gitnote.git`
         如从HTTPS地址克隆，则运行`git clone https://github.com/Louieusc/gitskill.git`

   

**12. 创建、合并、删除、查看分支**

- `$ git checkout -b <Branch name>`
  
    创建新Branch并切换入该分支
    
    ​    *注：相当于git branch Branch名和git checkout Branch名两个命令的合成*
    
    
    
- `$ git branch` 

   查看当前目录所有分支名，当前所在分支名字前有*号

- 在新branch路径下，更改本库的README.md文件并保存、add、commit。新branch随即会产生一个修改后的README.md文件。只要不切换回原branch（main），可对该文件持续编辑多次。而原branch中的README.me并无改变，且新分支仅本机可见，原分支并无痕迹。

- 如要将新branch发往远程库，`$git push origin <新分支名>`

- 如需将新编辑的README.md文件合并回原branch(main)，需：
      （1）切换回原branch，`$ git checkout <原branch名>`
      （2）$ git merge 新branch名
  
- `$ git branch -d <branch名>`，可删除该分支 
  
  *注：彻底删除分支也可用` $ git -D <branch名>`。如要删除已发至远程库上的分支，只能在远程库的branch页面中进行*
  
- 如需进入分支并查看内容，可` $ git checkout <分支名>`即切换入该分支内，再`$ ls` 即能显示分支内所有内容

   

**13. 查看、比较不同分支内的同一文件**

- 先在Git Bach上切换到新分支，从本机硬盘中找到该库内的某文件，更改内容后关闭

- 在Git Bach上切换到原分支，再从本机硬盘中找到库内同一文件，查看内容并无变化，关闭

- 在Git Bach上切换回新分支，再从本机硬盘中找到该文件查看内容，发现内容已变为更新后内容。
    （注：只需切换分支，无需换主机，从文件的同一保存位置即可查看不同分支内的该文件版本）

  


**14. 当不同分支内的编辑发生冲突时**

- 如果在分支main内，编辑了文件README.MD，并add和commit。同时又在分支fea1内，也编辑了同名文件，并add和commit。此时如果merge fea1并不能合并之，系统会提示发生冲突Conflict要求修正。

- 进入原分支main中，打开文件README.MD，发现系统自动加入了二分支的新编辑内容，并以<<<<<<和=====间隔之。
        此时可直接编辑文本，将双方新编内容人工整合，保存。

- 将整合后文件add并commit。对冲突的修正即完成。用$ git log可查看分支内容合并的具体情况。

- 最后，可将新分支fea1删除掉。

  


**15. 识别曾经merge过的分支**

    通常merge branch后的文本并无特别标识。但在merge命令后加入 --no-ff 参数后，它会显示合并前的注释，从而发现合并痕迹。
- 在某目录下创建并切换分支

- 修改文件后add并commit

- 切换回原主支，`$ git merge --no-ff -m "merge with no-ff"` 新branch名，合并完成
   *注：此次的-m参数是把合并注释进去*

- 用`$ git log`可看到分支曾被合并过的信息

  

**16. 封存当前工作状态**

    如果在当前文件未进行完毕，虽已add但尚未commit时，如果急需解决另外文件问题，可先将当前文件封存起来，事后再解封。
- 在当前工作分支下，`$ git stash`

-  `$ git status`，显示工作树clean，封存已完成

-  `$ git stash list`，可显示封存信息

-  `$ git stash pop`，可解封并删除stash信息。之后再用git stash list查看，再无stash信息了。

  

**17. 关于Cherry-pick命令**

   对在同一目录下某分支Dev又在封存状态下，如果要把原主支（名为main）的新改动同步到封存分支的同名文件中，需以下步骤：

- 封存分支暂时不要解封
- 为对主支main改动而新建的分支（名为issue），merge后也暂时不能删除此新分支
- 先在已封存的分支（名为dev）内运行`$ git cherry-pick issue的commit id号`，这样就能把改动一次同步到dev的同名文件中。无需merge
- 此时再删除新分支issue
- 回到Dev分支，用命令`$ git stash pop`解封dev且删除stash信息。最后，commit先前未提交注释的文件
     (注：如果一个新分支已提交并注释，但并未merge至主支main，此时新分支不能被删除。如果确定需要删除，需用`$ git branch -D <新分支名>`)



**18. 关于远程库**

   远程库默认名为origin

- `$ git remote`可查远程库名，一般默认名为origin

- `$ git remote -v`可查其详情

- 推送分支的最新内容，用`$ git push origin <分支名>`

- 最需要随时推送的分支是主支（如main或master），其他是否推送视情况而定。
     (注：分支在推送至远程库前，仅本地主机能查看分支内容）
     
- 如果多地主机同时向远程库同一分支推送不同内容的同名文件，后推送者会失败。此时，可用`$ git pull`从远程库拉取他人最新的提交，再合并、推送。 
       - 先需`$ git branch --set-upstream-to=origin/分支名 本地分支名`，这将建立本地分支与远程库分支的链接 (分支名最好取为相同)
   
       - 再用`$ git pull`
        
       - 此时pull成功，但会显示二者文本有冲突。可手动合并之，再add和commit。
        
       - 最后再push至远程库，`$ git push origin <branch name>`
   
   
   ​      

**19. 标签TAG管理**

    TAG相当于一个commit的别名，但简洁有意义。通过它可以快速查找某个特定commit，从而进行相关处理。
-  `$ git tag <tag name>` 可创建新标签，为分支内的最新commit

-  `$ git tag`可查看当前分支内的所有标签号

- 如果要指定为先前某个commit创建标签，需先找到此commit的ID:
       a. 查找commit的ID，可运行`$ git log --pretty=oneline --abbrev-commit`，能显示历次commit的ID短号、注释和已有Tag信息
       b. 再运行`$ git tag <tag name> <commit id短号>`，即可创建标签

-  `$ git show <tagname>`可查看标签具体信息

- 将标签全部推送至远程库 `$ git push origin --tags` 
      推送某一个标签至远程库 `$ git push origin <branch name>`
      *注：标签无论是在哪个分支内创建，它在目录内所有分支中都可见*

- 删除标签`$ git tag -d <tag name>`

- 删除远程库的某标签: 先删除本地某标签，再运行` $ git push origin :refs/tags/<tag name>`

  

**20. 带.MD扩展名的是什么文件?**

MD是Markdown的缩写，是一种带格式风格的纯文本文件。它可以通过MD编辑器（如Typora）制作和输出。 
md文件可以在GitHub中预览其内容。 



**21. 如何参与GITHUB的一个开源项目**

- 在Github网站上，找到该项目，点击右上的Fork即可将项目内容拷贝至自己在Github的帐号中
- 从本机运行$ git clone git@github.com:louieusc/<项目名>，即可将项目内容克隆到本机的库中。今后可在本机推送修改
- 如官方库能接受该修改，可在GitHub上发起一个pull request



**22. 关于.gitignore忽略文件**

某些文件不便或不需提交但又需存入Git目录中，可在Repository下创建一个.gitignore文件，将不提交项列入文中

- <file name>: 将某文件列入忽略项

-  <.*>: 将所有以.开头的文件列入忽略项*

- *<*.so>：将所有扩展名为so的文件列入忽略项

- !<file name>: 不用忽略的例外文件

  

  *注：.gitignore本质是一个plain text文件，如果忽略成功，目录中即使新加入了该类型文件且在目录中可见，但运行$ git status后系统也会提示工作树clean，无文件需提交。如果例外成功，该文件被加入目录后，$ git status后系统将提示有文件需提交*
   (P.S. For re-edit .gitignore file, you may use $ nano .gitignore without sudo account)



**23. 配置别名Alias**

可将某些较复杂的命令设为简短的别名，之后运行命令时以别名代之

- `$ git config --global alias.<alias> original name`
  *注：alias后有一点*
- 设置好的别名会自动存在GIT根目录下的.gitconfig文件中
- 也可在.gitconfig文件中直接创建、更改、删除别名
  (我已设如下别名：
  st = status
  cm = commit
  br = branch
  sw = switch)



**24. 关于SourceTree**

 Sourcetree是一个用于本地的图形化GIT软件。通过图形界面方便运行GitBash命令

*注：如果不能Push至远程库，则Tools->Options->General: in SSH client configuration set the SSH Client to OpenSSH, 
select your id_dsa for SSH Key. 即可解决push问题*



**25. 关于 RM 命令

   删除一个带空格的文件名的文件，用命令：
   `$ git rm "<xxx xxx xx">`
     

**26. 在网络浏览器上进行提交**

Visual Studio Code中，左方Sidebar有一提交功能键。点击后输入commit内容，可完成当前所有提交和注释。
     

**27. 如何从Github远程库下载文件**

- 进入Github该文件所在目录，打开该文件，点击右上角Raw即显示出该文件的raw格式。
- 右击鼠标选save as，即可下载该文件至本地。



**28. 关于对远程库的pull和fetch命令**

**git pull** 命令用于从远程获取代码并跟本地的版本进行合并。

**git pull = git fetch +  git merge**，fetch命令可取回某文件，merge命令将其与本地文件合并。

Pull命令格式为：

```
$ git pull <远程库名> <分支名>
```

将远程主机 origin 的 master 分支拉取下来，与本地分支brantest 合并：

```
git pull origin master:brantest
```

如果远程分支master是与当前分支合并，则冒号后部分可省略：

```
git pull origin master
```

该命令表示取回 origin/master 分支，再与本地的 brantest 分支合并。

以 https://github.com/tianqixin/runoob-git-test 为例如下：

```
$ git remote -v  # 查看信息
origin    https://github.com/tianqixin/runoob-git-test (fetch)
origin    https://github.com/tianqixin/runoob-git-test (push)

$ git pull origin master
From https://github.com/tianqixin/runoob-git-test
 * branch            master     -> FETCH_HEAD
Already up to date.
```

以上命令表示取回远程库origin的master 分支，再与本地的 master 分支合并。



**29. Github上如何删除文件？**
进入该文件，点击右上下拉菜单，拉至最下点击delete file，再commit，即可删除。



**30. 如何显示图片？**

- 必须编辑/etc/host文件，写入相关DNS的IP地址及网址，才能显示图片。

- 如图片网址为https://github.com/louieuscc/desktop-tutorial/tree/main/img/bat.png，则host文件中必须有GitHub.com的IP地址。

- Macbook中一般不能直接编辑host文件，可存为duplicate后再放入原host文件夹中，替换掉原host文件即可。host不能有扩展名

- 最好在Github上创建一个图片文件夹，如img。所有图片都上传到该文件夹。

  

**31. 如何在READ.ME文件中插入图片？**
上传图片后，Copy其链接地址。在READ.ME文件中输入代码！[image]()
在圆括号中粘贴图片地址，即可。



**32. Mac上的.ssh目录在哪里？**

Mac上的SSH 目录的位置是 `~/.ssh`



























  
