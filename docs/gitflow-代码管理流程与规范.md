# Git Flow 代码管理流程与规范

## Git Flow

推荐使用 Git Flow 的规范流程来管理项目的版本管理、代码协作。

## Git Flow 常用分支

Git Flow 在管理过程中一般拥有 5 类常用分支：

* **master 分支，又名 production 分支**：这是我们常用的 master 分支，只有这个分支的代码才会发布到生产环境。注意，这个分支只能从其他分支合并，工程师不能再这个分支直接修改；

* **develop 分支**：这是我们的主开发分支，工程师所有的功能性开发都会基于 develop 分支。develop 分支包含所有要发布到下一个 release 的代码。这个分支有以下特性：不主动向其他分支合入代码；作为 feature 分支的源分支，最终接受 feature 分支的代码合入；作为 release 分支的源分支，接受最终 release 分支的合入；

* **feature 分支**：这是工程师用来开发一个新功能的分支，一旦开发完成，Maintainer 将其合入 develop 分支，从而将这些功能准备进入下一个 release。**注意：一旦 feature 分支合入 develop 分支，Maintainer 应立即删除该 feature 分支；** 

* **release 分支**：当 develop 分支发展到一定阶段，我们需要发布一个 release 分支时，Maintainer 需要基于 develop 分支，创建相应的 release 分支。完成 release 分支之后，Maintainer 需要将 release 分支同时合入 master 分支以及合回 develop 分支（合入 master 分支之后，立即完成 master 分支的 tag 操作，最终 maintainer 删除 release 分支）；

* **hotfix 分支**：只有当 master 分支上出现 bug 时，我们会采用 hotfix 分支。hotfix 分支源于 master 分支，完成 bug 修复之后，同时合入 master 分支以及 develop 分支，**注意: hotfix 合入 master 分支之后，额外立即完成 master 分支的 tag 操作**。

## Git Flow 如何工作
	
### 1. 初始 master 分支和 develop 分支

第一个分支来源于 master 分支。所有来到 master 分支的 commit 都应该被打 tag。因此，不论是 **release 分支合入 master 分支**，还是**hotfix 分支合入 master 分支**，都应该在当前的 commit 号上打 tag。develop 分支来源于 master 分支。Master 的初始情况如下图：

![初始 master 分支和 develop 分支](./static_files/git-workflow-release-cycle-1historical.png "初始 master 分支和 develop 分支")

### 2. 正常开发使用 feature 分支

feature 分支命名形式为 feature/* 。

日常的功能代码贡献都通过 feature 分支来完成。每当工程师开发完 feature 分支，需要完成两个步骤：

* 必须将 feature 分支 merge 回 develop 分支；
* 合并完分支之后**务必将该 feature 分支删除**。

feature 分支的示意图如下：

![正常开发使用 feature 分支](./static_files/git-workflow-release-cycle-2feature.png "正常开发使用 feature 分支")

### 3. 发布版本所用的 release 分支

release 分支名为 release/* 。

release 分支基于 develop 分支创建。创建 release 分支之后，工程师可以在这个 release 分支上完成测试，修复 bug 等。如果此时，其他的开发工程师需要开发新的功能，则依旧可以基于 develop 分支创建 feature 分支开发新的功能。**注意：一旦打了 release 分支之后，请勿从 develop 分支上合并新的代码改动到 release 分支。**

release 分支正式完成之后，需要发布 release 分支，此时需要完成三个步骤：

* 将 release 分支合入 master 分支，并在 master 分支上打好release 的版本 Tag 号；
* 将 release 分支合入 develop 分支，将 release 分支上修改的 bug 回归开发分支 develop；
* 删除 release 分支，分支内容已经由 tag 号记录。

release 分支的示意图如下：

![发布版本所用的 release 分支](./static_files/git-workflow-release-cycle-3release.png "发布版本所用的 release 分支")

### 4. hotfix 维护分支

hotfix 分支名为 hotfix/* 。

由于生产环境发布的版本都是基于 master 分支的，而 master 分支的代码依然有可能出现 bug，此时代码管理需要针对 master 分支做 hotfix 操作。hotfix 分支基于 master 分支来创建，开发完毕之后，需要完成三个步骤：

* 将 hotfix 分支合入 master 分支，完成 master 分支上的 Tag 操作；
* 将 hotfix 分支合入 develop 分支；
* 删除 hotfix 分支，分支内容已经由 tag 号记录。

hotfix 分支的示意图如下：

![hotfix 维护分支](./static_files/git-workflow-release-cycle-4hotfix.png "hotfix 维护分支")



**本篇源于暂未开源的 DaoCloud dao-style 相关流程文档，未经允许请勿转载！**