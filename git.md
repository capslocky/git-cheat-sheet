## git basic commands ##

Command | Description
--- | ---
git clone [url] | Download repository and checkout master branch
git checkout --track origin [branch_name] | Download remote branch as local branch
git checkout -b [branch_name] | Create new local branch and switch to it
git checkout [branch_name] | Switch to another local branch
git status | Show current branch and changed files
git status -sb | The same, but shortly
git commit -m "[message]" | Create new local commit from index
git push -u origin head | Take current local branch and create **new** remote branch as upstream
git push | Send new local commits of the current branch to its **existing** upstream branch
git push -f [remote_name] [branch_name] | The same, but force and explicitly
git fetch | Download new commits of remote-tracking branches (updating references)
git pull | Downlad and apply (merge) new commits to the current branch
git pull --rebase | The same, but using rebase instead of merge
git branch -d [branch_name] | Delete the local branch
git branch -D [branch_name] | The same, but force
git push origin -d [branch_name] | Delete the remote branch


## git terms ##

Term | Description
--- | ---
[remote_name] | By default you have only one remote repository named 'origin'  
[branch_name] | Typically consists of two parts with jira ticket id ('feature/ASD-4385-workflow-for-shop', 'bugfix/ASD-4512')  
upstream (or remote-tracking) branch | Automatic reference to the remote branch, <br> typically with the same name, to push/pull local commits from
working copy | Current copy of files, it's what you see and edit  
head | Reference to the current (base) commit of your working copy  
index (staged files) | Next commit will be created from this set of changes 
fast-forward | When you merge commits from another branch to the current branch, <br> but the current branch has no any own unique commits, <br> so no need in merge commit, only reference is moved


## git file commands ##

Command | Description
--- | ---
git add [file_name] | Add the file change to the index (staging)
git add . | Add all changes to the index
git reset [file_name] | Move the file change out of index (unstaging)
git reset | Unstage all the changes
git rm [file_name] | Remove committed file
git mv [file_name] [new_file_name] | Move/rename committed file
git checkout [commit_hash] -- [file_name] | Restore file state from the specific commit
git checkout -- [file_name] | The same but from last commit, i.e. undo changes
git stash | TO DESCRIBE
git stash pop | TO DESCRIBE


## git extra commands ##

Command | Description
--- | ---
git commit --amend | TO DESCRIBE
git cherry-pick | TO DESCRIBE
git remote prune origin | TO DESCRIBE
git branch [branch_name] [commit_hash] | Create new local branch for a specfic commit
git checkout -b [branch_name] [commit_hash] | The same, but also switch to it
git branch -f [branch_name] [commit_hash] | Move tip of local branch to the specific commit, <br> you will lose commits if there is no another branch containing them
git revert | TO DESCRIBE


## git merging ##
Command | Description
--- | ---
git merge | TO DESCRIBE
git merge [branch_name] --no-ff --no-edit | TO DESCRIBE
git merge --abort | TO DESCRIBE
git rebase | TO DESCRIBE


## git investigating ##

Command | Description
--- | ---
git cherry -v | Show local commits yet to be pushed to upstream
git branch -v | TO DESCRIBE
git branch --no-merged develop | Show all local branches not merged to develop branch
git branch --merged develop | Show all local branches merged to develop branch
git branch --merged develop -r | The same, but for remote branches (-a to see both remote and local)
git log -3 --stat --pretty=format:"%h - %an (%ar): %s" | Show last 3 commits with file statistics
git log --grep 'strange bug' --pretty=format:"%h - %an (%ar): %s" | Show all commits with text 'strange bug'
git tag --list --contains d485e45 | Show all tags containing given commit


#### How to check if one commit contains another commit (copy-paste it to shell) ####
```bash
parent=d485e45; child=9dcd29d; echo; echo -n "Result: commit" $parent;\
if (git merge-base --is-ancestor $parent $child);\
then echo -n " IS "; else echo -n " IS NOT "; fi;\
echo -n "a parent for commit" $child; echo;
```


## git tricks ##

Command | Description
--- | ---
git reset --hard head | Discard all uncommitted changes (reset to last local commit)
git reset --hard [commit_hash] | Reset current branch to the given commit (with losing all orphan commits)
git reset --hard origin/[branch_name] | The same but by remote branch name
git reset --soft head~1 | Disassemble last commit into index (preserving all changes)
git reset --soft [commit_hash] | The same, but to the given commit
git clean -xdf | Delete all untracked (ignored) files and folders
git clean -nxdf | Just display what would be deleted


## git setup ##

Command | Description
--- | ---
git version | Show your git version
which git | Show your git location
git init | Initialize current directory as a repository
git config --global user.name "[firstname lastname]" | Set your default name across all repos
git config --global user.email "[your_email@site.com]" | Set your default e-mail
git config --global push.default current | TO DESCRIBE


## git tips ##
* You can easily clone your local repo into another local folder
* Moreover you can add one local repo as a remote for another
* Before performing some operations (like big rebase) do create and store a backup branch ('backup/ASD-4385-workflow-for-shop-2018-05-14')
* Close and open gui client if no changes visible there
* You can use aliases - TO DESCRIBE
* How to exit vim text editor - just type ESC :wq


## git links ##
* https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
* https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf
* https://orga.cat/posts/most-useful-git-commands
* https://github.com/git-tips/tips
* https://github.com/luisbg/git-cheat-sheet
* https://github.com/arslanbilal/git-cheat-sheet
* https://www.sourcetreeapp.com/
