# Lab0: GitLab

Due: 30 Sep, 23:59:59

## TODO

1. 认真阅读[文档](https://ics-26fall-fdu.github.io/labs/lab0-git-lab/)，学习 Git 的基本用法，并在报告中回答文档中的问题。（15 分）

    - 你之前有过多人协同开发的经历吗？如果有，你们是使用什么方式分工协作的？
    - 答：有过：1月的数学建模美赛，使用的是微信文件传输；
    - 9月的数学建模美赛，使用的是VScode+GitHub，大部分时候使用vscode里面的push和pull就可以完成大部分协作任务，但是仍然需要及时沟通，否则容易出现不同人commit的更改冲突。
  
    - 
    - 思考一下，Git 为什么要设计“暂存-提交”两个步骤？
    - 答：我认为 Git 设计“暂存—提交”两步，是因为正式提交前往往需要一个整理和检查修改的中间阶段。
    
    - 如果只有“修改—提交”，那么改完文件后，要么一直不提交，要么只能把所有改动一次性记入版本历史。但实际开发中，一次可能改了很多地方，它们未必属于同一个功能。比如一边修 bug，一边顺手改了注释，一边维护了功能A，一边维护功能B，可能四个同时进行，然后过了一段时间A好了，然后B好了。。。。。。这时如果直接提交，相当于四个修改同时提交,但是逻辑上四个修改对项目的贡献内容可能天差地别，把四个完全不同类型的修改打包在一起提交，容易使得提交记录重点不清，阅读者不知道这次修改的重点是什么。
    
    - 因此 Git 增加了暂存区。用户可以先挑选已完成、准备提交的修改放入暂存区，不确定或还要继续改的内容留在工作区。这样，暂存区就像提交前的“草稿区”或“候选区”。而且这样可以使逻辑更清晰：即使同时改了A和B，A先改好，那么就不必把A和修改了一部分的B同时上传，而是把A的改动暂存然后直接上传，这样就能进行一次只修改A部分内容的上传，逻辑更清晰，且可以有选择性地只上传已经改动的部分。

   - 它也提供了检查和撤回空间：某个修改不该进入下次提交，可以从暂存区移除，而不用删除实际修改；提交内容不完整，也可以继续加入其他修改再提交。

   - 所以，“暂存—提交”把两个问题分开了：哪些修改进入下一次版本？什么时候正式记录为一个版本？

   - 这种设计让用户可以先组织修改，再生成完整、清晰的提交，而不是把当前所有变化一次性记录下来。

   - 因此，Git 暂存区的核心意义在于：让用户有选择地组织一次提交，使版本历史更清晰、可控，也让一个提交更准确地对应一个完整的功能、修复或逻辑变化。


    - `git branch` 和 `git branch -a` 的区别是什么？查阅资料并回答。
    - 答：前者只查看本地分支；后者包括本地分支和远程分支。也就是说，加上 -a（即 --all）选项后，会列出本地分支和远程跟踪分支。
    - 例如：我自己实验中使用这两个指令：
    - PS C:\Users\crmin\OneDrive\test-git> git branch -a
      dev
      dev2
    * main
      remotes/origin/main
      说明带上-a的结尾可以查到已经publish的远程分支。
    PS C:\Users\crmin\OneDrive\test-git> git branch
      dev
      dev2
    * main
    * 这说明如果不附带-a，只能查到本地的分支。
    - （另外，还有一个-r（即--remotes）远程分支，只列出远程跟踪分支。）
    - 

3. 使用此仓库建立个人仓库，完成 `main.c` 文件中的 `TODO` 部分并进行一次 commit。（50 分）
   - 只要填入任意字符串就算完成，当然你也可以随意发挥（程序的正确性不纳入计分，有修改即可）。
   - 如果你想要编译运行 `main.c`，执行

   ```bash
   make
   ./main
   make cl·ean
   ```
   已完成，记录存在main.c中。

   编译main.c的terminal记录：
    crmind@crmindnotebook:~/ICS-26Fall-FDU.github.io/Gitlab_25300180031_changjun$ make
    gcc -Wall -O2 -c main.c -o main.o
    gcc -Wall -O2 -o main main.o
    crmind@crmindnotebook:~/ICS-26Fall-FDU.github.io/Gitlab_25300180031_changjun$ ./main
    This is my hw.Cheer up!Hello, world!
    crmind@crmindnotebook:~/ICS-26Fall-FDU.github.io/Gitlab_25300180031_changjun$ make clean
    rm -f main.o main
       

4. 在下面的三个网页中任选其二进行阅读，简要概括其内容，并谈谈你对“为什么要学习 Git”这个问题的理解。（15 分）

    - [Commit Message 规范](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
    - [Git Flow 分支控制](https://www.dafaycoding.com/article/git-gif-flow)
    - [语义化版本](https://semver.org/lang/zh-CN/)

5. 学习 Git 分支管理，新建 `feature` 分支，在该分支以及 `main` 分支上对 `main.c` 分别进行一次修改与提交（10 分）。随后将 `feature` 分支 merge 到 `main` 分支（即切换回 main 分支执行 `git merge feature`），并处理发生的合并冲突（10 分）。

    - 在两个分支上的提交必须要满足：在 `main` 分支合并时会出现冲突。请你解决这个冲突，并在实验报告里截图表明你遇到并解决了冲突。

    - 请阅读 `git merge` 部分，思考如何修改 `main.c` 会出现冲突。

    - 如果你两次提交之后合并没有出现冲突，不必担心，你可以不用撤回之前的提交，而是继续尝试提交修改并 merge，直到出现冲突并解决。

6. 在 `main` 分支提交一份实验报告（实验报告单独评分），格式要求为 `PDF` 或 `Markdown`。内容包括：

    - 文档中要求回答的问题
    - 你的实验步骤
    - 必要的截图
    - 你的建议（可选）
