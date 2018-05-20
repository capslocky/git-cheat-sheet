## git basic commands ##

Command | Description
--- | ---
git clone [url] | Download remote repository and checkout master branch
git checkout --track origin [branch_name] | Create local branch based on existing remote branch <br> (and set as upstream)
git checkout -b [branch_name] | Create new local branch and switch to it
git checkout [branch_name] | Switch to another local branch
git status | Show current branch and changed files
git status -sb | The same, but shortly
git commit -m "[message]" | Create new local commit from index
git push -u origin head | Send current local branch as **new** branch for remote <br> (and set as upstream)
git push | Send new local commits of the current branch to its <br> **existing** upstream branch
git push -f [remote_name] [branch_name] | The same, but force and explicitly
git fetch | Download new commits of all remote branches (updating references)
git pull | Download and apply (merge) new commits to the current branch
git pull --rebase | The same, but using rebase instead of merge
git branch -d [branch_name] | Delete the local branch
git branch -D [branch_name] | The same, but force
git push origin -d [branch_name] | Delete the remote branch on remote repository


## git terms ##

Term | Description
--- | ---
[remote_name] | Remote repository (by default you have only one named 'origin')
[branch_name] | Typically consists of two parts with jira ticket id <br> ('feature/ASD-4385-workflow-for-shop', 'bugfix/ASD-4512')
branch tip (head) | Is a last commit of the branch <br> (manually moved reference, typically by commit or pull)
head | Automatic reference to the current (base) commit of your working copy
upstream (or remote-tracking) branch | Automatic reference to the remote branch, typically with the same name <br> ('origin/bugfix/ASD-4512'), to push/pull local commits from
working copy | Your current state of files, it's what you see and edit
detached head | When your current commit is not a tip of any branch
index (staged files) | Next commit will be created from this set of changes
ahead 3 / behind 5 | Amount of unique new commits in comparison with upstream, <br> ahead 3 - is yours, behind 5 - in upstream
fast-forward | If you merge commits from another branch to your current branch, <br> and your branch is completely behind it (ahead is 0), <br> there is no need in merge commit, just current branch tip is lifted up (by default)
dangling (orphan, lost) commit | Commit that isn't a part of any branch or tag (not visible in gui client). <br> But still visible through 'git reflog' and 'git fsck' until garbage collection. <br> Can be restored by 'git merge [commit_hash]' or 'git reset --hard [commit_hash]' <br> or by creating new branch for that commit

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
git branch -f [branch_name] [commit_hash] | Move tip of local branch to the specific commit <br> Warning: orphan commits can arise
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
git branch -v | Show all local branches with respective tip commits and ahead/behind info
git branch --no-merged develop | Show all local branches not merged to develop branch
git branch --merged develop | Show all local branches merged to develop branch
git branch --merged develop -r | The same, but for remote branches <br> (-a to see both remote and local)
git log -3 --stat --pretty=format:"%h - %an (%ar): %s" | Show last 3 commits with file statistics
git log head..origin --pretty=format:"%h - %an (%ar): %s" | Show all new commits from upstream
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
git reset --hard head | Discard all uncommitted changes in current branch (reset to last local commit)
git reset --hard [commit_hash] | Reset current branch to the given commit. Warning: orphan commits can arise
git reset --hard origin/[branch_name] | The same, but by remote branch name
git reset --soft head~1 | Disassemble last commit into index (with preserving all local changes)
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
git fsck  | Checks local repo integrity

## git tips ##
* You can easily clone your local repo into another local folder
* Moreover you can add one local repo as a remote for another
* Before performing some operations (like big rebase) do create and store a separate backup branch
* Close and open gui client if no changes visible there
* You can use aliases - TO DESCRIBE
* How to exit vim text editor: with saving changes - just type [ESC :wq], without saving [ESC :q!]


## why use git shell? ##
* You just can't execute most of operations with gui client
* You don't have to stop using your gui client, because shell greatly complements any gui client
* It is the fastest way in many everyday cases
* Much less chance to involve your repo into 'bad' state and much easier to fix it
* You always have the shell and can rely on it
* You can introduce aliases and scripts for frequent operations
* You directly interact with repository (useful shell output, no gui bugs)
* You better understand how git works
* You will be cool


## git links ##
* https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
* https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf
* https://orga.cat/posts/most-useful-git-commands
* https://github.com/git-tips/tips
* https://github.com/luisbg/git-cheat-sheet
* https://github.com/arslanbilal/git-cheat-sheet
* https://www.sourcetreeapp.com/
