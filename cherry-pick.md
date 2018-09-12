# cherry-pick

[TOC]

## cherry-pick的基本操作

git中一个比较实用的命令：cherry-pick，使用该命令可以将任意的commit通过其commit号将其合并到你想要的分支上。

下方就演示了cherry-pick命令的使用方法。在 master 分支上，执行  git cherry-pick <一些commit的哈希值>  然后将这些提交合并到master分支上。这些分支会根据cherry-pick的顺序进行merge，每次merge都会形成一个新的提交。与rebase命令不同，虽然会产生一个新的提交，而之前的提交是不变的。具体如下所示: 

![image](F:\doc\github\git-doc\images\545446-20180101211735987-1396135304.gif)

接下来我们来看一下具体在终端上cherry-pick的操作命令。下方是目前分支的状态，并且处于master分支上。现在我们要做的事情是将 d98ff43  这个commit 拿到master上。

![image](F:\doc\github\git-doc\images\545446-20180101215658393-1019260859.png)

下方就是我们执行cherry-pick的命令，如下所示。下方执行cherry-pick时是非常顺利的，没有产生冲突。当提交进行合并时会产生冲突，就不是这个样子了，稍后会演示到。

![image](F:\doc\github\git-doc\images\545446-20180101220103034-1238339560.png)

下方就是顺利的cherry-pick后的样子。

![image](F:\doc\github\git-doc\images\545446-20180101215813831-302458645.png)

## cherry-pick的冲突解决

在cherry-pick时遇到冲突是避免的，下方特地搞了一个cherry-pick冲突的例子。为了更进一步的了解冲突的解决方式，下方cherry-pick了多个提交，而且这多个提交在merge时都会有冲突。下方我们会对这些冲突进行解决。

> - 首先我们在master分支上通过 git cherry-pick <一系列提交的哈希值>来将 4f8e019、dbe9e8a、5c52520这三个提交摘到master分支上。
>
> - 然后我们会先看到在cherry-pick 4f8e019 这个提交时产生了冲突，报了一个Error：提升不能将cherry-pick命令应用于4f8e019。并且下方给了一系列的提示（解决此错误可以通过正确的方式解决冲突，然后通过git add 或者 git rm将更改的文件进行追踪，最后可以使用 git commit进行提交）
>
> - 解决一个冲突并commit后，使用 git cherry-pick --continue可以进一步的进行下一个提交的cherry-pick。下方再次执行git cherry-pick --continue时，又出现了冲突，此刻我们还是按照上述的步骤对冲突进行解决，解决完毕后接着git cherry-pick --continue。直到所有的commit被合并完毕即可。

**具体操作步骤如下所示：**

![image](F:\doc\github\git-doc\images\545446-20180101223030237-1095076859.png)

下方是上述操作的最终结果，cherry-pick了三个commit，冲突了三次，解决了三次。如下所示：

![image](F:\doc\github\git-doc\images\545446-20180101222817003-1032690423.png)

