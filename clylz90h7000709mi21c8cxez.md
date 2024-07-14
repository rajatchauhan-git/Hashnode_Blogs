---
title: "Advance Git & GitHub for DevOps Engineers"
datePublished: Sun Jul 14 2024 19:57:22 GMT+0000 (Coordinated Universal Time)
cuid: clylz90h7000709mi21c8cxez
slug: advance-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720986869702/69e39486-89a3-4164-8378-a55c9fae1d79.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720987036144/c4d5c8c8-7b85-47b3-9468-80ec8861ceab.png
tags: github, git, conflict-management, 90daysofdevops, trainwithshubham, branching-strategies

---

### Git Branching

Branches are a core concept in Git that allow you to isolate development work without affecting other parts of your repository. Each repository has one default branch, typically called `main` or `master`, and can have multiple other branches. Branches let you develop features, fix bugs, or safely experiment with new ideas in a contained area of your repository. You can merge a branch into another branch using a pull request, which allows for code review and integration testing before the changes are incorporated into the main codebase.

![](https://miro.medium.com/v2/resize:fit:1400/1*ZfQc3rU1MYnVTBOwg7DQkg.gif align="left")

### Git Revert and Reset

**Git reset** and **git revert** are two commonly used commands that allow you to remove or edit changes you’ve made in the code in previous commits. Both commands can be very useful in different scenarios.

* **Git reset:** This command is used to undo changes by moving the HEAD and the current branch pointer to a specified commit. It can modify the staging area and working directory, making it a powerful but potentially dangerous command if not used carefully. There are three main options: `--soft`, `--mixed`, and `--hard`.
    
    * `--soft`: Moves the HEAD to the specified commit, but leaves the index and working directory unchanged.
        
    * `--mixed` (default): Moves the HEAD to the specified commit and resets the index, but leaves the working directory unchanged.
        
    * `--hard`: Moves the HEAD to the specified commit and resets both the index and working directory.
        
* **Git revert:** This command creates a new commit that undoes the changes made by a previous commit. It is a safer way to undo changes, especially in a shared repository, because it does not alter the commit history.
    

### Git Rebase and Merge

**Git rebase** and **git merge** are two commands that integrate changes from one branch into another, but they handle the commit history differently.

* **Git rebase:** This command allows users to move or combine a sequence of commits to a new base commit. Rebasing modifies the commit history by creating new commits for each commit in the original branch, starting from the new base commit. This results in a linear, cleaner project history, but it can be dangerous if not used correctly, as it rewrites commit history.
    
    Example:
    
    ```bash
    git checkout feature-branch
    git rebase main
    ```
    
* **Git merge:** This command integrates changes from one branch into another by creating a new commit, called a merge commit, which preserves the history of both branches. The commit logs on branches remain intact, providing a complete history of how the codebase has evolved.
    
    Example:
    
    ```bash
    git checkout main
    git merge feature-branch
    ```
    

---

### Task 1: Feature Development with Branches

1. **Create a Branch and Add a Feature:**
    
    * Add a text file called `version01.txt` inside the `Devops/Git/` directory with “This is the first feature of our application” written inside.
        
    * Create a new branch from `main`
        

```bash
git checkout -b dev
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720972734826/570ef34e-782a-4462-83dd-25e66a9bb6e6.png align="center")

* Commit your changes with a message reflecting the added feature.
    

```bash
git add version01.txt
git commit -m "Adding new feature"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720974531948/c586dfc5-9297-416f-abd9-69617fc41379.png align="center")

**Push Changes to GitHub:**

* Push your local commits to the repository on GitHub
    

```bash
git push origin dev
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720974627468/2bcd28fd-2717-4f20-867d-9bed4c8dc6b1.png align="center")

**Add More Features with Separate Commits:**

* Update `version01.txt` with the following lines, committing after each change:
    
    * 1st line: `This is the bug fix in development branch`
        

```bash
echo "This is the bug fix in development branch" >> version01.txt
git commit -am "Added feature2 in development branch"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720974974852/09be92ff-19db-4f25-a5b6-bde3d6119676.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720976671185/76f81903-e322-4b61-b107-fa7fe2e10537.png align="center")

2nd line: `This is gadbad code`

```bash
echo "This is gadbad code" >> version01.txt
git commit -am "Added feature3 in development branch"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720976809358/86787680-a6d6-42ce-b619-6b1dceb030ee.png align="center")

* 3rd line: `This feature will gadbad everything from now`
    

```bash
echo "This feature will gadbad everything from now" >> version01.txt
git commit -am "Added feature4 in development branch"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720977224250/739d4be9-9ba6-424b-b8d5-951c386c5e8c.png align="center")

**Restore the File to a Previous Version:**

* Revert or reset the file to where the content should be “This is the bug fix in development branch”
    

```bash
git revert HEAD~2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720981161525/727c8372-e97f-4b02-8072-43a29d0b2c25.png align="center")

### Task 2: Working with Branches

1. **Demonstrate Branches:**
    
    * Create 2 or more branches and take screenshots to show the branch structure.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720983350922/872bb0c9-0c89-40e9-a28d-2a4ecd07b6a6.png align="center")
    
2. **Merge Changes into Master:**
    
    * Make some changes to the `dev` branch and merge it into `master`.
        
        ```bash
        git checkout master
        git merge dev
        ```
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720983228248/1e3c4ffe-dc24-4a77-a875-683cad09b457.png align="center")