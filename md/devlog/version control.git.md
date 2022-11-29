---
created: 1655912367989
desc: ''
id: qkp5jc6pta8a9f35evsbvod
title: Git
updated: 1660771781218
---
   
Git is one of the most popular implementation of Version Control. Among others such as [version control.fossil](../devlog/version%20control.fossil.md), [version control.SVN](../devlog/version%20control.SVN.md).   
   
Version Control is just what it sounds like. It helps you share code with different developers across different teams. Code can be hosted centrally on a Code Repository using different Git repository providers such as Github, Gitlab, Bitbucket, companies also host their own Git servers.   
   
Git helps developers to collaborate with each other using features like branches, pushing, pulling, merging, forking etc.   
   
## Basics   
   
   
- Git knows how to merge changes automatically(but not always).   
  - This is when a "merge conflict" happens. These have to be solved manually.   
- It is a best practice to push and pull often to avoid merge conflicts. (basically, **Continuous Integration**).   
- When someone pushes breaking changes, it doesn't affect your codebase until you "pull" those changes to your "local repository".   
- Git keeps history of every code change which allows you to "revert" a commit (go back to the previous version of your codebase).   
- Each change/commit is labelled with a commit message.   
   
   
- Git has different parts:   
  - Git server (usually has a UI).   
  - Git repository (where the code lives).   
  - Local repository (local copy of remote repository).   
  - History (`git log`).   
  - Staging (uncommited changes).   
  - Git client (to execute git commands, can be a cli or a UI tool).   
   
## Getting Started   
   
You can choose publicly hosted Git repository providers such as Github, Gitlab, Bitbucket among others.   
   
   
- Create an account on one of these platforms to get started.   
- Create a remote repository(project).   
- Install Git locally. [Git - Downloads](https://git-scm.com/downloads)   
- Clone the remote repository locally.   
  - Usually, the provider will list the instructions you need to set up the repository locally.   
- Make changes. Check changes `git status`.   
- Add all the changes `git add -A` or `git add .` aka staging.   
- Commit changes with a message `git commit -m "message"` or `git commit`.   
- Push to remote repository `git push origin main`.   
   
## First Time Set Up   
   
   
- Copy your machine's public SSH key to the Git repository provider to be able to access it from your local machine.   
- Configure your username and email globally or locally(for only a specific repo).   
  - `git config --global user.email name@example.com`.   
  - `git config --global user.name username`.   
   
## Init Git Locally   
   
If you already have a codebase(project) you've been working on locally that you want to set up git repository for.   
   
   
- Initialize git using `git init` from the working directory of your codebase.   
  - A `.git` folder will be created with all the configuration inside it.   
- Create remote repository with one of the providers.   
- `git add -A`   
- `git commit -m "first commit"`   
- You can name the default branch name using `git branch -M main` or git will use a default name.   
- Configure remote repository with the local repository `git remote add <name> <url>`   
  - E.g: `git remote add origin https://github.com/zubayrrr/project.git`   
- Set current branch as the upstream branch.   
  - `git push --set-upstream origin main` branch will now be connected.   
   
## Branches   
   
A branch is created by default. Which can be renamed. You can add new branches to work on different changes across your codebase. Branches will help you organize your codebase and the different changes incoming from different developers.   
   
It is a best practice to create a new branch for a new feature/bug fix.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660744959/wiki/mqe4xcj2pco8qa5jxwb0.png)   
   
You can either create a branch from your repository provider or locally.   
   
   
- Run `git fetch`, which will retrieve all branches and updates, and after that, run `git checkout <branch>` to switch to that account.   
  - You can also do `git pull` to fetch all the new branches from the remote repository.   
- OR to create a branch locally and switch to it   
   
   
  - `git checkout -b test origin/test`   
   
   
- Make changes and push   
  - `git push --set-upstream origin test`   
   
It is a common practice to have “Master” and “Development” branch.   
   
Master branch is usually used in production while develop branch is an intermediary master branch.   
   
Pipeline is triggered whenever a new branch is merged into master, which is not ideal so a develop branch is used to collect the code from all the different branches and then this develop(Dev) branch is merged with the production Master branch.   
   
**The proper way of doing Continuous Integration is to NOT have the intermediary master branch called Dev and instead merge all the branches to one Master branch.**   
   
## Merging   
   
When developers create their own branches while working on features/bug fixes they need to “merge” the code to the Main branch.   
   
Big feature branches long open, increase the the chance of merge conflicts.   
   
### Merge Request   
   
   
- Other developer reviews code changes before merging.   
- A pull request(PR) or merge request is made to pull code from your branch to the master branch, which is reviewed and processed using the Git server UI.   
- The PR is assigned to a reviewer whi will approve or reject the merge request.   
- Branches, once merged can be deleted. You can do it using the UI on the remote repository but locally   
  - `git checkout master` switch to master branch   
  - `git pull` pull the changes that were merged   
  - `git branch -D test` delete the branch   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660747518/wiki/ght2gvahyfsqdqgsl6ke.png)   
   
### `git merge`   
   
Let's say you want to bring new changes from the master branch to your working branch. You'll `git pull` to sync your local master branch with remote master branch and `git merge master` to merge the master branch with your working branch. After which you can make a pull/merge request to merge your working branch into the master branch.   
   
## Rebase (Avoiding Merge Commits)   
   
`git pull` VS `git pull --rebase`   
   
When two developers are working on a same branch. One developer’s changes are not in sync with the other’s and one of the developers pushes to that branch but turns out there are already some changes pushed by the other developer to that branch. So the developer will need to `git pull` before they can push, which will result in two commits: 1. The changes the developer made, 2. The merge commit.   
   
These merge commits are redundant and to avoid them you should do `git pull -r` it pulls the changes from the remote branch and stacks our changes on top so there is no merge branch commit.   
   
## Resolving Merge Conflicts   
   
Let’s say two developers are working on a same file in parallel, which obviously will cause merge conflicts when you do `git pull -r` and merge will not be possible. You must tell git which change to keep.   
   
To resolve, you can use your editor. You’ll have your remote changes, your local changes and the end result(which you decide). You’ve git extension on your editor installed which can help you achieve this.   
   
`git rebase --continue` to apply the changes and `git push`   
   
## .gitignore   
   
To ignore/not track some files/folders you can add a `.gitignore` file in the root of the project and mention the file/folder line by line, you can even use [glob](../devlog/glob.md) patterns to exclude files without having to mention each and every one of them. Use a tool like [Glob tester - tool for testing glob patterns](https://globster.xyz/).   
   
To untrack/remove already tracked/pushed files from remote repository: `git rm --cached .`   
   
## Stashing   
   
Save work-in-progress for later. When you've unfinished business that you don't want to commit just yet(this will create problem when you try to checkout to a different branch) in cases like these you should use `git stash` which will basically hide the changes you made and will give you a clean/up to date branch.   
   
When you're finally ready to go with the changes you stashed previously, you can do `git stash pop`.   
   
Another use-case of stashing is when you want to temporarily undo the changes you made.   
   
## History or Log   
   
`git log` keeps track of your activity on a codebase.   
   
Each commit has a HASH which you can use to go back in time to a state of the codebase at the time of that commit.   
   
`git checkout <commit-hash>` will take you to that commit and you'll be in "Detached HEAD" state which means you're not completely up to date.   
   
You can create a branch based on a commit hash.   
   
## Undoing and Modifying Commits   
   
### Hard   
   
Let's say you've made a commit(not yet pushed) and you want to revert the change, the whole commit. Since your remote repository does'nt yet have that commit, you can use the HEAD(the last commit) to hard reset your changes. It'll completely discard the changes you made in that last commit.   
   
`git reset --hard HEAD~1` where 1 signifies how many commits you want to undo.   
   
### Soft   
   
What if you didn't want to reset/discard the commit but just repair/correct something in the code, you can use a soft reset instead.   
   
`git reset --soft` default reset option. It'll uncommit but keep the changes.   
   
### Forceful   
   
When you want to revert a commit that you've already pushed to remote repository, basically undo a push, you can do `git reset --hard HEAD~1` will discard the changes locally. To discard changes even from the remote repository you'll need to forcefully sync local state with remote state of the codebase. `git push --force` will help you achieve that, it'll **override** the previous commit. It'll not allow you to `git push` as your local repo doesn't have some of the changes remote repo has. Git thinks remote repo is ahead and local repo is behind.   
   
This shouldn't be done on important/production/development branches as other developers might already have those changes(that you just undid) in their local repo.   
   
### Amend   
   
If you want some changes to be part of a commit that you haven't yet pushed(simply merge the change in the last commit without creating a new commit) you can use `git commit --amend`.   
   
### Revert   
   
`git revert <commit-hash>` and `git push` will not override the previous commit but add a new commit thus preserving the history.   
   
## Tagging   
   
Tags are ref's that point to specific points in Git history. Tagging is generally used to capture a point in history that is used for a marked version release (i.e. v1. 0.1). A tag is like a branch that doesn't change.   
   
## Misc   
   
   
- **HEAD**: Latest Commit. A pointer to the last commit.   
- Git is used extensively in [devops](../topics/devops.md) (**Infrastructure as Code**) for tracking files such as:   
  - [Kubernetes](../devlog/kubernetes.md) configuration files   
  - [Terraform](../devlog/terraform.md) and [Ansible](../devlog/ansible.md) files   
  - [languages.bash](../devlog/languages.bash.md) and [languages.python](../devlog/languages.python.md) scripts   
- Just like developers collaborate on developing applications, different DevOps engineers will collaborate on writing scripts, config files. For which, using `git` is ideal.   
- Git is also used by DevOps engineers in their CI/CD pipelines in tandem with build tools.