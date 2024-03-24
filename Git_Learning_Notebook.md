# Git学习笔记

## 符号说明

&lt;分支名&gt; ：如bugFix、main等。

&lt;哈希值&gt;：在本笔记中常用Cn表示，实际使用中是SHA-1值（commit ID），也可以是SHA-1值的简短形式。

&lt;指针&gt;：分支名或HEAD。

## 本地命令

### git init

初始化。win操作系统下，右键->git bash here之后，在git命令行中要输入的第一条命令。这样可以初始化一个仓库。

### git commit

 提交一个新版本。

### git commit --amend (-m "注释")

在不增加新节点的情况下将新修改的代码追加到前一次的提交中。但只能修改最新一次的提交，如果想修改的不是最新一次，要通过```git rebase -i```或```git cherry-pick```将要修改的节点放到最新的位置。

### git branch &lt;分支名&gt; 

创建新分支，但没有更新节点。然后需要checkout到新分支，才能在新分支提交新版本，否则还是在老分支上提交。

### git branch -f &lt;分支名&gt; &lt;任何引用&gt;

将分支名强制指向引用的位置。

* git branch -f main HEAD~2：将main强制指向HEAD后退2步的位置。
* git branch -f main C2：将main强制指向C2节点。

### git checkout &lt;分支名&gt; 

切换到新分支。

### git checkout -b &lt;分支名&gt; 

创建新分支，并切换到新分支。

### git checkout &lt;哈希值&gt; 

分离HEAD并指向哈希值代表的节点。

### git checkout &lt;指针&gt;~$n$

分离HEAD并指向指针指向的的上n个节点。

* git checkout main^：分离HEAD并指向main最新节点的上一个节点。
* git checkout HEAD^：指向HEAD节点的上一个节点。
* git checkout HEAD~4：HEAD后退4步。

~n表示向上n步。^表示向上1步。 当指针指向的节点存在多个parent的时候，可以通过^n选择向上追溯到第几个parent。

同时，这些操作可以链式操作。

* git checkout HEAD\~2\^2\~3：在HEAD节点先向上走2步，到达了一个拥有多个parent的节点，选择第二个parent，再向上走3步。

### git merge bugFix

合并分支。当前所在分支是main，节点是C3（哈希值），将bugFix分支最后一个节点C2（哈希值）连接到main并产生一个新节点哈希值是C4（哈希值）。

### git rebase main

把当前分支所有节点换屁股到main。当前所在分支是bugFix，节点是C3、C4（哈希值）。在main分支下复制并提交当前节点，于是main分支最新提交为C3'（与C3完全相同）、C4'（与C4完全相同）。

### git rebase -i &lt;指针&gt;~$n$

以图形化界面重新排布指针及之前的共n个版本。注意，指针本身也算在n步之中。

### git reset

回退。只用于本地库。退回上次提交的版本。

### git revert

回退。用于远程仓库和协作。新建一个节点，内容是上次提交的版本。

### git cherry-pick C3 C4

当前指针指向main，选择C3 （哈希值）和C4（哈希值）依次添加到main后面。

### git tag v1.1.2 (C3)

给C3节点打标签v1.1.2。如果C3条件缺省，则默认给HEAD打标签。

### git describe (&lt;任何引用&gt;)

返回引用位置（若缺省则为HEAD）最近的打了标签的节点。该标签节点与引用位置必须在同一分支。将返回：```<标签内容>_<引用位置与tag相差几个节点>_g<引用位置哈希值简短形式>;```。当引用位置本身就有标签时，则输出标签名称。

### git rev-parse HEAD

显示当前节点哈希值。

### git rev-parse --short HEAD

显示当前节点哈希值的简短形式。

## 远程命令

### git clone &lt;服务器地址&gt; 

从服务器地址处获取一份远程仓库的拷贝。

### git fetch

将本地仓库中的**所有**远程分支更新成了远程仓库相应分支最新的状态。从远程仓库下载本地仓库中缺失的提交记录，并更新远程分支指针的位置。```git fetch```**不会改变本地分支的状态，不会更新本地分支指针的指向。**你可以用这条命令对远程分支进行检查。

### git fetch origin &lt;远程分支&gt; 

到远程仓库中的 &lt;远程分支&gt; 中，获取所有本地不存在的提交，下载到本地的origin/&lt;远程分支&gt; 分支上。注意，```git fetch```**不会改变本地分支的状态，不会更新本地分支指针的指向**。你可以用这条命令对远程分支进行检查。

### git fetch origin &lt;源指针(远程)&gt;:&lt;目标分支(本地)&gt; 

&lt;源指针(远程)&gt;：远程仓库中要拉取到本地分支的东西。这个指针可以是哈希值（如C3）、分支（如bugFix）、相对引用（如HEAD^、main~2）。特别需要说明的是，这次下载并不是只下载指针指向的单一节点，而是以指针指向的节点为末尾下载末尾之前的所有未被下载过的所有节点。

&lt;目标分支(本地)&gt;：本地仓库中要提交到的目的地。但不能是当前所在的分支。如果本地仓库中尚不存在这个 &lt;目标分支&gt; ，那么git会自动创建这个分支。

**这条命令会直接修改本地分支。使用需谨慎。**

### git fetch origin :&lt;本地分支&gt; 

相当于下载“空”到本地的 &lt;本地分支&gt; 。通常用于在本地新建名为 &lt;本地分支&gt; 的分支。

### git pull

等于git fetch+git merge。把远程仓库拉下来，更新远程仓库分支的状态，并和本地分支合并。

### git pull --rebase; git push

如果远程仓库有更新（你的队友提交了新版本，如远程仓库变为C3-C7），而你的本地仓库中的新提交基于C3（本地仓库为C3-C4-C5），则单纯的```git push```命令无效。此时要先```git pull --rebase```然后```git push```。

当```git pull --rebase```后，本地仓库基于C3新建了一个origin/main分支为C3-C7，然后把原来的分支接到后面，变成C3-C7-C4'-C5'。然后```git push```就可以了。

这样提交的好处是所有提交记录是线性的。如果想保留更多的历史分支，可以通过```git pull; git merge; git push```来完成，这样处理提交记录将产生分支后再合并。

### git pull origin bugFix

等同于```git fetch origin bugFix; git merge origin/bugFix```，先下载到本地的远程分支上，然后合并到当前所在分支，合并后的分支名是当前所在分支。

### git pull origin &lt;源指针(远程)&gt;:&lt;目标分支(本地)&gt; 

等同于```git fetch origin <源指针(远程)>:<目标分支(本地)>; git merge <目标分支(本地)>  ```，先把远程指针指向的一系列提交下载到本地的目标分支上（如果不存在则新建），然后把本地的目标分支合并到当前所在分支。

### git push

将本地仓库的提交更新到远程仓库。前提是本地仓库中的新提交与远程仓库中的提交没有冲突，即本地仓库的新提交均基于远程仓库中的最新提交。例如，远程仓库中的最新提交是C3，而你的本地仓库中的提交为C3-C4-C5，则可以把C4、C5push上去。

### git push &lt;远程分支&gt; &lt;本地分支&gt; 

可以无视当前所在的分支位置，将 &lt;本地分支&gt; 提交到 &lt;远程分支&gt; 上去。例如```git push origin main```，就是将本地的main分支提交到远程的origin/main分支上去。

### git push origin &lt;源指针(本地)&gt;:&lt;目标分支(远程)&gt; 

&lt;源指针(本地)&gt;：本地要提交到远程仓库的东西。这个指针可以是哈希值（如C3）、分支（如bugFix）、相对引用（如HEAD^、main~2）。特别需要说明的是，这次提交并不是只提交指针指向的单一节点，而是以指针指向的节点为末尾提交末尾之前的所有未被提交过的所有节点。

&lt;目标分支(远程)&gt;：远程仓库中要提交到的目的地。如果远程仓库中尚不存在这个 &lt;目标分支&gt; ，那么git会自动创建这个分支。

### git push origin :&lt;远程分支&gt; 

相当于提交“空”到&lt;远程分支&gt; ，也就是在远程仓库中删除了它。

### git checkout -b &lt;分支名&gt; origin/main

**创建一个分支**，并远程跟踪(track remote) origin/main分支。例如，```git checkout -b branch1 origin/main```，这样branch1分支相当于原来的main分支的作用。在branch1分支上的提交在```git push```时可以提交到远程仓库的main分支上。

需要注意的是，本地仓库中的origin/main分支始终指向最近一次本地与远程通信时的远程main分支的位置。

### git branch -u o/main (&lt;分支名&gt;)

让&lt;分支名&gt;远程跟踪(track remote) origin/main分支，但 &lt;分支名&gt;必须已经存在。这是这条命令与上一条命令的不同点。如果当前分支即为&lt;分支名&gt;，则&lt;分支名&gt;参数可以缺省。

