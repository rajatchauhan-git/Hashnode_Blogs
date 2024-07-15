---
title: "Git Cheat Sheet"
datePublished: Mon Jul 15 2024 18:52:26 GMT+0000 (Coordinated Universal Time)
cuid: clyncddb500010ai97hi5cv3c
slug: git-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721069416377/f7029009-13e2-402f-a2ba-f7c2a6630446.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721069508532/a3d9c437-edc3-41d1-b0bc-088d82584884.png
tags: github, technology, git, devops, cheatsheet, gitcommands, cheat-sheet, 90daysofdevops

---

| Git init | It is used to initialize the GIT |
| --- | --- |
| Git status | To know the current state of the repository |
| Git add &lt;filename&gt; | It will move a single file to the stagging |
| Git add . | It will move all the files to the stagging |
| Git commit -m "message" | It is used to create a new commit in GIT with a specific commit message |
| Git log | It will display a list of commits in a GIT repository |
| Git ls-files | It will show all the files that have committed in the GIT repository |
| Git log --oneline | It will show the on-line/short commit ID details |
| Git log --oneline -10 | It will show the last 10 commit ID's |
| Git show &lt;commit ID&gt; | It will show all the details of the particular commit ID |
| Git diff &lt;commit ID1&gt; &lt;commit ID2&gt; | It will show the difference between the two commit ID's |
| Git commit -a -m "message" | used to create a new commit in Git, automatically including all tracked files that have been modified or deleted |
| Git config --global [user.name](http://user.name) &lt;name&gt; | command is used to set the global Git configuration for your username |
| Git config --global [user.email](http://user.email) &lt;email&gt; | command is used to set the global Git configuration for your email address |
| .gitignore | text file used in Git repositories to specify which files and directories should be ignored and not tracked by Git. |
| Git tag --a &lt;tag&gt; &lt;commit-ID&gt; -m "message" | It is used to add a tag to a commit ID |
| Git show &lt;tag ID&gt; | used to display information about a specific Git tag |
| Git diff &lt;tag ID1&gt; &lt;tag ID2&gt; | Used to show the difference between the two tag ID |
| **Steps to create a Repository on GIT-HUB** | Open [github.com](http://github.com) in browser and sign-in/sing-up To create a repository click on "+" button from the top-right corner. From the dropdown menu select "New Repository" and it will redirect you to "create a new repository" page. Enter Details:  
a. Repository Name  
b. Description  
c. Select if you want to create Public/Private repository Click on create repository |
| Git remote add origin &lt;link of the repository&gt; | command is used to add a remote repository to your local Git repository  
  
Origin - it is a short name that refer to the default remote repository when setting up a new repository or cloning an existing one |
| Git remote -v | To check if we have connected to any remote repository |
| Git push -u origin main | used to push your local branch named "main" to the remote repository named "origin" and set it as the upstream branch |
| **Steps to Generate a TOKEN in GITHUB** | Go to [github.com](http://github.com) Click on account icon from top-right corner. Click on settings from the menu Click on developer settings Click on personal access token and from the dropdown menu select Tokens(classic) Click on generate new token(classic) Enter Details:  
a. name  
b. Expiration  
c. Select all the checkbox Click on generate token  
Note: after creating the token copy the alpha numeric token before refreshing/going to other page. |
| Git push -u origin main --tags | used to push both the main branch and all tags to the remote repository named "origin." |
| Git cone &lt;link of the repo&gt; | It will clone the remote repository to another machine |
| Git pull origin main | It will pull the changes from the remote repository to local |
| Git fetch origin main | It will fetch the changes from the remote repository |
| Difference between CLONE, PULL, FETCH and MERGE | CLONE: it will clone the code from the remote repository to local  
  
PULL: it will bring the changes from the remote repository to local  
  
FETCH: it will check for the difference between remote repository and local.  
  
MERGE: it will merge the changes from remote to |
| Git rm &lt;filename&gt; | It will move the file to the staging area |
| Git mv &lt;old\_filename&gt; &lt;new\_filename&gt; | It will change the file name and move it to the staging area |
| Git reset --soft &lt;commit ID&gt; | allows you to move the branch pointer to a specific commit while preserving the changes introduced in the subsequent commits  
  
It will bring back all the items to the staging area |
| Git restore --stage &lt;filename&gt; | It will move the file from staging area to untracked state. |
| Git reset  --hard &lt;commit ID&gt; | It will directly move files to the untracked state and remove the changes will that commit ID |
| Git revert &lt;commit ID&gt; | It is used to create a new commit that undoes the changes made in a previous commit. It allows you to effectively revert or undo the changes introduced by a specific commit while keeping a record of the reversion in the commit history. |
| Git branch | It will show the branch you on |
| Git branch &lt;branch name&gt; | It will create a new branch |
| Git checkout &lt;branch name&gt; | It will switch to the other branch |
| Git checkout -b &lt;branch name&gt; | It will create and switch to the new branch |
| Git branch -d &lt;branch name&gt; | It will delete the branch |
| Git branch -D &lt;branch name&gt; | It will delete the branch forcefully |
| Git rebase main | It is used to integrate changes from one branch into another by moving or combining commits |
| Git push -d origin &lt;branch name&gt; | To delete remote branches from local  
  
and we can run this command from the main branch |
| Git checkout -b &lt;branch name&gt; &lt;commit ID&gt; | It is used to create a new branch from any particular branch |
| Git stash | used to save changes that you have made in your working directory but do not want to commit yet. It allows you to temporarily store your changes and revert your working directory to the state of the last commit |
| Git stash list | It will list the modification in stash |
| Git stash pop | It will bring back the files from stash state to staging state |
| Git commit --amend | It will change the message for latest commit ID |
| Git rebase -I HEAD~1 | It will Squash the two commit ID from HEAD  
  
Pick - to keep  
squash - To Squash |
| git show \[SHA\] | show any object in Git in human-readable format |