## git basic commands ##

Command | Description
--- | ---
git clone [url] | Download repository and checkout master branch
git checkout --track origin [branch_name] | Download remote branch as local branch
git checkout -b [branch_name] | Create a new local branch and switch to it
git checkout [branch_name] | Switch to another local branch
git status | Show current branch and changed files
git status -sb | The same, but shortly
git commit -m "[message]" | Create a new local commit from index
git push -u origin head | Take current local branch and create a **new** remote branch <br> (so it will be upstream)
git push | Send new local commits of the current branch to its **existing** <br> remote (upstream) branch
git push -f [remote_name] [branch_name] | The same, but force and explicitly
git fetch | Download new commits of remote-tracking branches
git pull | Downlad and apply (merge) new commits to the current branch
git pull --rebase origin | The same, but using rebase instead of merge <br> and explicit remote
git branch -d [branch_name] | Delete the local branch
git branch -D [branch_name] | The same, but force
git push origin --delete [branch_name] | Delete the remote branch


#### notes ####
**[remote_name]** - by default you have only one remote repository named 'origin'  
**[branch_name]** - typically consists of two parts ('feature/ASD-4385-workflow-for-shop', 'bugfix/ASD-4512')  
**working copy** - checked out copy of files, which you can see and edit  
**head**  - reference to current (base) commit of your working copy  


## git file commands ##

Command | Description
--- | ---
git add [file_name] | Add the file change to the index (staging)
git add . | Add all changes to the index
git reset [file_name] | Remove the file change from the index (unstaging)
git rm [file_name] | Remove committed file
git mv [file_name] [new_file_name] | Move/rename committed file
git stash | TO DESCRIBE
git stash pop | TO DESCRIBE


## git extra commands ##

Command | Description
--- | ---
git commit --amend | TO DESCRIBE
git cherry-pick | TO DESCRIBE
git remote prune origin | TO DESCRIBE


## git merging ##
Command | Description
--- | ---
git merge | TO DESCRIBE
git rebase | TO DESCRIBE
git revert | TO DESCRIBE


## git investigating ##

Command | Description
--- | ---
git tag --list --contains d485e45 | Show all tags containing given commit
git log --pretty=format:"%h - %an, %ar: %s" \| grep 'strange' | Show all commits with word 'strange'


### How to check if one commit contains another commit (copy-paste to shell) ###
```bash
parent=d485e45; child=9dcd29d; echo; echo -n "Result: commit" $parent;\
if (git merge-base --is-ancestor $parent $child);\
then echo -n " IS "; else echo -n " IS NOT "; fi;\
echo -n "a parent for commit" $child; echo;
```


## git tricks ##

Command | Description
--- | ---
git reset --hard head | Reset all files to the last commit (losing all changes)
git reset --soft head~1 | Disassemble last commit into index (preserving all changes)
git clean -xdf | Delete all untracked (ignored) files and folders
git clean -nxdf | Just display what would be deleted


## git setup ##

Command | Description
--- | ---
git init | Initialize current directory as a repository
git config --global user.name "[firstname lastname]" | Set your default name across all repos
git config --global user.email "[your_email@site.com]" | Set your default e-mail
git config --global push.default current | TO DESCRIBE


## git tips ##
* You can easily clone your local repo into another local folder
* Moreover you can add one local repo as a remote for another


## git links ##
* https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
* https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf
* https://orga.cat/posts/most-useful-git-commands
* https://github.com/git-tips/tips
* https://github.com/luisbg/git-cheat-sheet
* https://github.com/arslanbilal/git-cheat-sheet
* https://www.sourcetreeapp.com/
