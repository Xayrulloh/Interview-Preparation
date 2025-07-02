# Git Interview Questions

1. ## **What is git**

   Git is a distributed version control system used to track changes in files,
   particularly source code, during software development. It allows multiple
   developers to collaborate on the same project, manage different versions of
   the code, and easily revert to previous states if needed. Essentially, Git
   acts as a time machine for your code, enabling you to track modifications,
   experiment with new features, and collaborate efficiently

2. ## **What is a version control system (VCS)**

   A VCS keeps track of the contributions of the developers working as a team on
   the project. They maintain the history of code changes done and with project
   evolution

3. ## **What is a git repository**

   A repository is a file structure where git stores all the project based files

4. ## **What does git clone do**

   Clones a repository into our local machine

5. ## **What does the command git config do**

   It’s used to change the git config

6. ## **What is a conflict**

   When two separate branches have changes on the same line in a file or file
   deleted in one branch but in another it's modified

7. ## **What is the functionality of git ls-tree**

   This command returns a tree object representation of the current repository
   along with the mod and the name of each item and the SHA-1 value of the blob

8. ## **What does git status command do**

   To see the difference between the working directory and the index which is
   helpful for understanding git in depth and also keep track of the tracked and
   non tracked changes

9. ## **What does the git add command do**

   Adds changes into the index of the existing directory

10. ## **What has to be run to squash multiple commits (last N) into a single commit**

    git rebase

11. ## **What is the difference between git stash apply vs git stash pop command**
    - **git stash pop:** throws away the specified stash after applying it
    - **git stash apply:** leaves the stash in the stash list for future reuse

12. ## **What is the functionality of the “git cherry-pick” command**

    It’s used to introduce certain commits from one branch into another branch
    within the repository. The most common use case is when we want to forward
    or back port commits from the maintenance branch to the development branch

13. ## **Git pull vs Git fetch**
    - **git pull:** pulls new changes from the currently working branch
    - **git fetch:** pulls all commits and changes from desired branch and
      stores them in a new branch and for changes to be reflected in the
      current/target branch, **git fetch** should be followed by **git merge**
      command

14. ## **Git Merge vs Git Rebase**
    - **git merge:** preserves history by creating a new merge commit, keeping
      the branch structure **unchanged**. It’s safer for collaboration but can
      create cluttered history with multiple merge commits.
    - **git rebase** rewrites history by applying commits on top of another
      branch, creating a linear history. It keeps the commit log clean but
      alters history, making it risky for shared branches.

15. ## **Git revert vs Git reset**
    - **git revert:** It’s used to creating a new commit that undoes the changes
      of the previous commit
    - **git reset:** It’s used for undoing the local changes done in the git
      repository

16. ## **Can you explain head in terms of git and also tell the number of heads that can be present in a repository**

    It’s a last commit object of a branch and it can be only one

17. ## **How do you find a commit which broke something after a merge operation**
    git bisect \<start | bad\>
