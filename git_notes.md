# All about GitHub



> *从链接可下载Git Desktop*
> https://github.com/apps/desktop?ref_cta=download+desktop&ref_loc=installing+github+desktop&ref_page=docs
> *也可直接访问注册后的目录网址，如：*
> https://github.com/louieuscc/



# 通过GitBash以命令行方式操作Github

*Git可由此下载 (https://git-scm.com)*

*安装后即有GitBash的CLI窗口，Windows系统会生成Bash特有图标，命令行提示以$开头*

*IOS系统中，GitBash与shell共用CLI窗口，无专有图标*



**Git运行流程：**

先将远程库克隆到本地根目录，查看本地会发现该库名的文件夹，内有文件若干。

-->进入该文件夹，它即为本地工作区（例如user/louie/文件夹名）

-->刚克隆的以上文件可编辑修改，保存 （会自动存入本地工作区）

--> 也可另外新建文件，并编辑、保存

--> 然后`$ git add`，存入本地暂存区stage area（尚未被跟踪untracked）

--> 再`$ git commit`，加注释并存入本地库local repo（已被跟踪）

--> 最后`$ git push`，提交至远程库(GitHub)



**1. 建立新远程库**

> Github远程库需先注册，再用`$ ssh-keygen -t rsa -C "youremail@example.com"`，创建SSH KEY。
>  此KEY位于本机c:\usr\louie\.ssh\中，内有id_rsa.pub及id_rsa两文件。Mac的SSH 目录位置是 `~/.ssh 
>
> 有时此二文件可能创建到其它目录下，务必拷贝回.ssh正确文件夹中。
> 复制id_rsa.pub里的文本，粘贴至远程Github设置里的SSH key设置中即可。

- 登录已有Github帐号，点击新建库

- 在新建页面中，务必选中自动生成README.md选项。如此，新库的某些功能(如新建分支)才会有效

- 从此库界面上，可看到已自动生成一个默认branch分支，名为main

- 点击界面的add file，用鼠标拉动本地文件上传。文件上传后即存在此main分支中

- 后续即可clone此库到本地目录、pull文件等，实现本地与远程库全程同步了

  

  将Github上的新库demo与本地库建立关联：

  1. 在本地库目录下运行`$ git remote add origin git@github.com:louieuscc/demo.git `  

     *注：louieusc是我在Github的ID，库名demo*

  2. 如果本地分支名与远程分支名都为main，则：

     `$ git branch -M main`(切换至分支main)
     `$ git push -u origin main`(当前目录所有文件都推到远程库的默认分支main内)



**2. 克隆远程库**
克隆将远程库所有文件和版本历史复制到本地。初始项目文件可在远程库建立，然后各地主机从远程克隆至本地。

- 先在Github建立一个新库，命名为gitnote, 并勾选Initialize this repository with a README选项。
  此新库的SSH地址为：git@github.com:Louieuscc/gitnote.git。它的HTTPS地址为：https://github.com/Louieuscc/gitnote.git

- 开启GitBash，进入本地工作根目录，如c:\usr\louie

- 运行`git clone git@github.com:louieuscc/gitnote.git`
   也可从HTTPS网络地址克隆，运行`git clone https://github.com/Louieuscc/demo.git`

- 如果克隆成功，则从本地根目录可发现一名为demo的文件夹，其中还包括一些文件

  *后续即可在此本地位置编辑、上传文件至远程，实现同步。*

  

*克隆的好处：*

*1.本地开发：克隆远程仓库后，可在本地修改、测试和重构，不会影响远程仓库的内容。令开发过程更灵活和安全。*

*2.版本控制：将整个仓库的版本历史复制到本地，可以随时查看和管理代码的历史版本，便于追踪更改和回滚。* 

*3.代码浏览：可以方便地浏览和查看远程仓库的代码，了解项目的结构和功能。* 

*4.协作开发：在团队开发中，每个成员可以从远程仓库克隆一份代码，进行独立的开发和测试，最后再将更改推送回远程仓库。*



**3. 对克隆至本地的文件进行编辑、修改并保存**

- 先运行`pwd`和`ls`，查看当前目录及文件清单，找到需编辑文件

- 使用相应编辑器对文件编辑更改，存盘（此时仅存入本地工作区，但并未提交）

- 运行`$ git status`看状态，系统会提示文件已修改，但并未提交

- 运行`$ git diff`，可查看修改详情 (仅刚对文本进行更改后，git diff命令才有效。如已提交将不会显示任何信息)

- 先`$ git add <file name>`进行添加，存入本地暂存区

- 再`$ git commit -m "<commit>"`进行注释，存入本地库

- 命令`$ git commit -am <file name>`可同时实现add + commit

- 再运行`$ git status`查看状态，系统报告当前无需提交之修改，且工作树干净 (nothing to commit, working tree clean)

- `git branch`，查明本地分支名是什么，如果是main，而远程对应的demo库中的分支也是main，则：

- `git push -u origin main`

  如此，本地修改后的文件即提交至远程库中，并覆盖库内原文件。   

  

  *注：多个文件修改保存后只需commit一次*

  ​      *编辑时务必注意文件名的大小写*
  ​       如当日对文件会多次修改，可随时保存，但只需在当日结束前一次性提交和注释，无需多次提交*

  

**4.本地创建新文件**

-  `$ ls` 查看本地目录

-  `$ cd <库目录名>` 进入先前克隆至本地的库目录

- `$ touch <file name>`建立新文件

- `$ ls`查看新文件是否成功创建

- `$ cat <file name>` 显示文件内容

-  `$ git init`将该目录变成Git可管理的库

- 通过`$ git add`和`$ git commit`将新文件存入本地库，等待后续远程提交

- 命令`$ git commit -am <文件名>`可同时实现add + commit

  

  *注：在远程库建立了对应库和分支后，未来即可进行远程提交*



***注：初次使用commit提交时需用到git config指令***

需提交用户信息，包括用户名和邮箱：

`$ git config --global user.name "xxx"`
`$ git config --global user.email xxx@xxx.com`

*注：如果去掉 --global 参数只对当前仓库有效。*



**5. 关于远程库**

   远程库位于Github.com/<你的注册名>

- `$ git remote`可查远程库名，一般默认名为origin

- `$ git remote -v`可查其详情，如：

  origin	https://github.com/louieuscc/demo.git (fetch)

  origin	https://github.com/louieuscc/demo.git (push)

  *表示在远程库中，库名为origin，内有一个名为demo的库*

- 推送分支的最新内容，用`$ git push origin <分支名>`

- 最需要随时推送的分支是主支（如main或master）
  (注：分支在推送至远程库前，仅本地主机能查看分支内容）

- 如果多地主机同时向远程库同一分支推送不同内容的同名文件，后推送者会失败。此时，可用`$ git pull`先从远程库拉取他人最新的提交再推送。 
      - 先需`$ git branch --set-upstream-to=origin/分支名 本地分支名`，这将建立本地分支与远程库分支的链接 (分支名最好取为相同)
      - 再用`$ git pull`

  - 此时pull成功，但会显示二者文本有冲突。可手动合并之，再add和commit。

  - 最后再push至远程库，`$ git push origin <branch name>`

    

    *注：如需删除远程某库，在GitHub.com上进入该库页面，点击Settings，在Danger Zone中点击Delete this repository*

    

**6. 对远程库的pull和fetch**

**git pull** 命令用于从远程获取代码并跟本地的版本进行合并。

**git pull = git fetch +  git merge**，fetch命令可取回某文件，merge命令将其与本地文件合并。

Pull格式为：

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



**7. 如何从Github远程库界面下载文件**

- 进入Github该文件所在目录，打开该文件，点击右上角Raw即显示出该文件的raw格式。
- 右击鼠标选save as，即可下载该文件至本地。



**8. 删除文件、重命名文件**

- 远程库的文件如需删除，最好在Github上进行

- 本地文件可直接进入所在目录删除

- `git rm <文件名>`也可删除文件，然后再commit。该文件即被永久删除，不可恢复

- `git mv <旧文件名> <新文件名>`可移动或重命名文件。此运作无需commit

  例如：`mv readme.md README.md` 将readme.md文件改为新名字

  

**9.关于多部主机向远程同一目录库发送提交**

- 如果多部主机都需向远程同一Repository发送文件或commit，此时远程主机的repository会自动产生两个branch，一个名为
      master，另一个名为main。

- 平时把本地库所有最新内容推送至远程库，命令`$ git push origin <branch name>`。分支名为master或main。

- 如果多部主机向远程不同Repository发送文件，则远程主机的repository只分别产生各自的branch。

  

 **10.撤消修改restore**

- 如果对文件作了修改，但并未add和commit，可立即撤销修改

- 命令`$ git restore <文件名>`
  再用git status查看，系统显示工作树clean，即撤消修改完成。
  
- 文本作了修改且已经add但尚未commit，命令`$ git restore --staged <文件名>`，可撤销add的内容（但并非恢复到工作区中未作任何修改的原始状态）
  再用git status查看，发现系统称该文件已修改但并未add，意为已退出暂存区。
  
- 如果文件已经add且commit了，用git status查看，系统显示无需commit，工作树干净。意为无法撤消修改。

  此时只能用命令`$ git reset` 恢复到上一版本，令修改消失

  

**11.回滚版本reset**

- 如果更改内容已经add和commit，则无法撤消修改，只能用此命令回到上一旧版本，令修改无效
- `git reset HEAD^ <file name>` 回到最近一次之前的版本
- `git reset --hard <版本号码>` 回到指定某版本号的版本
- `$ git reset --hard HEAD^` 回到未做任何修改前的原始版本





**12.查看、创建、合并、删除分支**

- `$ git branch` 

  查看当前目录所有分支名，当前所在分支名字前有*号

- `$ git checkout -b <branch name>`

  创建新branch并切换入该分支

  ​    *注：相当于git branch Branch名和git checkout Branch名两个命令的合成*

- `$ git branch -d <branch名>`

  删除分支 

  *注：彻底删除分支也可用` $ git -D <branch名>`。如要删除已发至远程库上的分支，只能在远程库的branch页面中进行* 

- `$ git merge <被合并分支名>` 

  将被合并分支合并到当前分支里，重复的文件将只保留当前分支的文件版本

- ` $ git checkout <分支名>`

  切换进入分支。如需查看分支内容，切换入该分支后再`$ ls` 即能显示分支内容

- 如要将新branch发往远程库，`$git push origin <新分支名>`

  



**12. 查看、比较不同分支内的同一文件**

- 先在Git Bach上切换到新分支，从本机硬盘中找到该库内的某文件，更改内容后关闭

- 在Git Bach上切换到原分支，再从本机硬盘中找到库内同一文件，查看内容并无变化，关闭

- 在Git Bach上切换回新分支，再从本机硬盘中找到该文件查看内容，发现内容已变为更新后内容。
  （注：只需切换分支，无需换主机，从文件的同一保存位置即可查看不同分支内的该文件版本）

  

**13. 当不同分支内的编辑发生冲突时**

- 如果在分支main内，编辑了文件README.MD，并add和commit。同时又在分支fea1内，也编辑了同名文件，并add和commit。此时如果merge fea1并不能合并之，系统会提示发生冲突Conflict要求修正。
- 进入原分支main中，打开文件README.MD，发现系统自动加入了二分支的新编辑内容，并以<<<<<<和=====间隔之。
      此时可直接编辑文本，将双方新编内容人工整合，保存。
- 将整合后文件add并commit。对冲突的修正即完成。用$ git log可查看分支内容合并的具体情况。
- 最后，可将新分支fea1删除掉。



**14.识别曾经merge过的分支**

    通常merge branch后的文本并无特别标识。但在merge命令后加入 --no-ff 参数后，它会显示合并前的注释，从而发现合并痕迹。

- 在某目录下创建并切换分支

- 修改文件后add并commit

- 切换回原主支，`$ git merge --no-ff -m "merge with no-ff"` 新branch名，合并完成
  *注：此次的-m参数是把合并注释进去*

- 用`$ git log`可看到分支曾被合并过的信息



**15. 查看文本修改日志**

- `$ git log`可显示历次修改的注释内容，顺序由新至旧，当前最新版本以HEAD表示，且每个commit都有一个很长ID号

- `$ git reflog`命令，可显示历次reset及每个版本的commit ID号。故即使关闭Git Bash仍可查到每个ID号的前7位
  
    *注：运行git log后，必须按字母键q才能退出log状态并回到GitBash命令行*

   

**16. 将某版本改设为当前最新版（HEAD）**

- 命令`$ git reset --hard HEAD^`。^表示前一个，如要之前第二个，则为^^。
   可将某旧版设为最新版本，用更多位可用数字，如HEAD~100
   
- `git log`后可发现前一旧版已被设为最新HEAD，被替换的先前最新版本已消失

- 如想找回消失的那个版本，可在Git Bash窗口中找到该版本的commit ID号，记住前五位。再运行命令`$ git reset --hard commit_id`, 即将该版设为最新HEAD。commit_id只需前5位即可

- 用`git log`查看，该版已显示并又成为HEAD
  
   
  

**17.临时封存**

    如果在当前文件未进行完毕，虽已add但尚未commit时，如果急需解决其它问题，可先将当前文件封存起来，事后再解封。
- 在当前工作分支下，`$ git stash`

  系统会显示*Saved working directory and index state WIP on main: c6a29fb make a new file*，表示已保存入工作目录中，封存编号为c6a29fb

-  `$ git status`，显示无需commit且

-  工作树clean，封存完成

-  `$ git stash list`，可显示封存信息

-  `$ git stash pop`，可解封并删除stash信息。之后用git stash list查看，再无stash信息

  

**18. 关于挑选提交Cherry-pick**

   对同一目录下某分支在封存状态下，如果要把原主支main的新改动同步到封存分支的同名文件中，需：

- 对封存分支暂不解封
- 对主支main改动而新建的分支（名为issue），merge后也暂时不能删除此新分支
- 先在已封存的分支（名为dev）内，运行`$ git cherry-pick issue的commit id号`，能把改动一次同步到dev的同名文件中无需merge
- 再删除新分支issue
- 回到Dev分支，用命令`$ git stash pop`解封dev且删除stash信息。最后，commit先前未提交注释的文件
     (注：如果一个新分支已提交并注释，但并未merge至主支main，此时新分支不能被删除。如果确定需要删除，需用`$ git branch -D <新分支名>`)













**28. 标签TAG**

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

  

**29. MD是什么文件?**

MD是Markdown的缩写，扩展名为.md。是一种带格式风格的纯文本文件。它可以通过MD编辑器（如Typora）制作和输出。 
md文件可以在GitHub中预览其内容。 



**30. 如何参与GITHUB的一个开源项目**

- 在Github网站上，找到该项目，点击右上的Fork即可将项目内容拷贝至自己在Github的帐号中
- 从本机运行`$ git clone git@github.com:louieusc/<项目名>`，即可将项目内容克隆到本机的库中。今后可在本机推送修改
- 如官方库能接受该修改，可在GitHub上发起一个pull request



**31. 关于.gitignore忽略文件**

某些文件不便或不需提交但又需存入Git目录中，可在Repo下创建一个.gitignore文件，将不提交项列入文中

- <file name>: 将某文件列入忽略项

-  <.*>: 将所有以.开头的文件列入忽略项*

- *<*.so>：将所有扩展名为so的文件列入忽略项

- !<file name>: 不用忽略的例外文件

  

  *注：.gitignore本质是一个plain text文件，如果忽略成功，目录中即使新加入了该类型文件且在目录中可见，但运行$ git status后系统也会提示工作树clean，无文件需提交。如果例外成功，该文件被加入目录后，$ git status后系统将提示有文件需提交*
   (P.S. For re-edit .gitignore file, you may use $ nano .gitignore without sudo account)



**32. 配置别名Alias**

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



**33. 关于SourceTree**

 Sourcetree是一个用于本地的图形化GIT软件。通过图形界面方便运行GitBash命令

*注：如果不能Push至远程库，则Tools->Options->General: in SSH client configuration set the SSH Client to OpenSSH, 
select your id_dsa for SSH Key. 即可解决push问题*


​     

**35. 在VS上进行快速提交**

Visual Studio Code中，左方Sidebar有一提交功能键。点击后输入commit内容，可完成当前所有提交和注释。
     



**36. Github上如何删除文件？**
进入该文件，点击右上下拉菜单，拉至最下点击delete file，再commit，即可删除。



**37. 如何显示图片？**

- 必须编辑/etc/host文件，写入相关DNS的IP地址及网址，才能显示图片。

- 如图片网址为https://github.com/louieuscc/desktop-tutorial/tree/main/img/bat.png，则host文件中必须有GitHub.com的IP地址。

- Macbook中一般不能直接编辑host文件，可存为duplicate后再放入原host文件夹中，替换掉原host文件即可。host不能有扩展名

- 最好在Github上创建一个图片文件夹，如img。所有图片都上传到该文件夹。

  

**38. 如何在READ.ME文件中插入图片？**
上传图片后，Copy其链接地址。在READ.ME文件中输入代码！[image]()
在圆括号中粘贴图片地址，即可。





























  
