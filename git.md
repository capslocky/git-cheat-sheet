# git cheet sheet #

## git basic commands ##

Command | Description
--- | ---
git clone [url] | Download remote repository and checkout master branch
git checkout --track origin/[branch_name] | Create local branch as a copy of existing remote branch <br> (and set as upstream)
git checkout -b [branch_name] | Create new local branch and switch to it
git checkout [branch_name] | Switch to another local branch
git status -sb | Show current branch, changed files and ahead/behind status
git commit -m '[message]' | Create new local commit from index
git push -u origin HEAD | Send current local branch as **new** remote branch <br> (and set as upstream)
git push | Send new local commits of the current branch to its <br> **existing** upstream branch (remote expects fast-forward)
git push -f [remote_name] [branch_name] | The same, but with forced overwrite and explicit names. <br> Warning: remote branch tip overwriting
git fetch | Download new commits of all remote branches without merging <br> (just updating local references to remote branches)
git fetch --tags | The same, but with tags as well
git pull | Download and merge new commits to the current branch from its <br> upstream (fast-forward possible here)
git pull --rebase | The same, but using rebase instead of merge
git branch -d [branch_name] | Delete the local branch
git branch -D [branch_name] | The same, but force
git push origin -delete [branch_name] | Delete the remote branch on remote repository
git init | Initialize current directory as a new empty git repository

Note: you interact with remote repository only in case of 'clone', 'fetch', 'pull' or 'push', all other operations are local and don't need network connection


## git terms ##

Term | Description
--- | ---
commit | Fixed (immutable) snapshot which describes complete and certain state of the project (not changeset!) referring entire previous snapshot history. It has unique hash, arbitrary message, author, committer, author date, commit date and references its parent commits
[commit_hash] | Unique identifier of any commit, the principal way to refer certain project state. <br> Looks like f5b5e37, which is a short form - just a unique substring of full value <br> f5b5e3719202bc5a78d97fc48aa089ca3034ce04 - calculated as SHA-1 hash from every data mentioned above
changeset&nbsp;(changes,&nbsp;diff) | A set of changes. Always dynamically calculated difference between two certain project states. When you watch a commit - it's a difference against its previous commit (direct parent). In case of watching index (staging) - against last commit. And unstaged changes - is a changeset between index and working copy.
branch | An independent line of development which "grows" by appending new commits
branch tip (HEAD) | Is a last commit of the branch. <br> The tip of local branch gets promoted by performing commit and pull. <br> Whereas tip of remote branch - by fetch and push
[branch_name] | Just a reference to branch tip (local or remote). Typically consists of two parts with jira ticket id <br> ('feature/ASD-4385-shop-workflow', 'bugfix/ASD-4512', 'origin/bugfix/ASD-4512')
working copy (tree) | Your current state of files, it's what you see and edit. HEAD + uncommitted changes
HEAD | Automatic reference to the current (base, last) commit of your working copy
to checkout | Make working copy represent given commit (typically by branch name)
detached HEAD | When your HEAD is not a tip of any branch
[remote_name] | Remote repository (by default you have only one named 'origin')
remote branch | Remote repository branch, works as a local reference, always contains remote prefix ('origin/develop')
upstream (or remote-tracking) branch | Linked remote branch, typically with the same name: <br> 'origin/bugfix/ASD-4512', to push/pull local branch commits from
master branch | The only branch existing in every git repository from the beginning, <br> typically holds production-ready code
develop branch | Permanent branch with latest developed features for the next release
feature branch | Temporary branch for separate developing of specific feature
release branch | Temporary branch targeting preparation of specific release 
hotfix branch | Temporary branch just for fixing bug found on production
tag | Fixed reference to the fixed commit, <br> typically to mark certain release, like 'v1.8.5-rc2'
index (staged files) | Next commit will be created from this set of changes
ahead 3 / behind 5 | Amount of unique new commits in comparison with upstream, <br> ahead 3 - is yours, behind 5 - in upstream. All others are common.
fast-forward | Special case of merge, when you merge commits from another branch <br> to your current branch, and your branch is completely behind it (ahead is 0, behind > 0), <br> there is no need in merge commit, current branch tip is just lifted up (by default)
dangling&nbsp;(orphan,&nbsp;lost) commit | Commit that isn't referenced by any branch or tag (not visible in gui client), <br> but still visible through 'git reflog' and 'git fsck' until garbage collection. <br> Can be restored by 'git merge [commit_hash]' or 'git reset --hard [commit_hash]' or by creating new branch for that commit
to merge | Integrate another branch into current branch
merge commit | Commit with two parent commits (first - direct one and second - tip of merged branch)
merge conflict | TO DESCRIBE
to amend commit | Recreate last commit as a new commit in order to append more changes or fix its message. <br> Warning: if commit has been pushed and used by other developer, don't do amend
to rebase | Place current branch on the top of another branch. Rebase will replay (recreate) commits as if branch has been started from another project state. Technically for every commit it takes its changeset and applies on the top (so conflicts are possible). <br> Warning: if branch has been pushed and used by other developer, don't do rebase
pull request | TO DESCRIBE
gitflow workflow | TO DESCRIBE
bare repository | TO DESCRIBE
patch | A single set of changes (typically output of git diff) exported to text file


## git file commands ##

Command | Description
--- | ---
git add [file_name] | Add the file change to the index (staging)
git add -A | Add all changes to the index
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
git reset --hard [commit_hash] | Reset working copy and current branch tip to the given commit. <br> Warning: orphan commits may appear
git commit --amend --no-edit | Add changes to the last commit from index without message editing
git commit --amend -m 'New commit message' | Change the message of last commit
git cherry-pick [commit_hash] | Copy given commit into current branch (copy changes)
git cherry-pick [commit_hash_1]^..[commit_hash_2] | The same but take multiple commits from given range
git remote prune origin | TO DESCRIBE
git branch [branch_name] [commit_hash] | Create new local branch for a specfic commit
git checkout -b [branch_name] [commit_hash] | The same, but also switch to it
git branch -f [branch_name] [commit_hash] | Move tip of local branch to the specific commit <br> Warning: orphan commits may appear
git revert | TO DESCRIBE
git rebase -i HEAD~3 | TO DESCRIBE
git pull --ff-only | TO DESCRIBE
git branch -u origin/[branch_name] | Set new upstream for current branch


## git basic combos ##
Command | Description
--- | ---
git reset --hard HEAD | Discard all uncommitted changes in working copy (reset to last local commit)
git reset --hard @{u} | Make working copy and current branch exact as its upstream
git reset --soft HEAD~1 | Disassemble last commit into index (with preserving all uncommitted changes)
git commit --amend --no-edit <br> git push -f | Amend and repush last commit. <br> Warning: remote branch tip overwriting, see git status -sb


## git merge and rebase ##
Command | Description
--- | ---
git merge [another_branch] | Integrate another branch into current branch
git merge [another_branch] --no-edit | Use standard merge message without starting text editor
git merge [another_branch] --no-ff | No fast-forward, create merge commit anyway
git merge --abort | Abort merge and return to inital state
git merge --continue | Continue merge after resolving conflict
git rebase [another_branch] | Place current branch on the top of another branch
git rebase --abort | Abort rebase and return to inital state
git rebase --continue | Continue rebase after resolving conflict
ours | Destination branch changes (during merge - current branch, during rebase - another branch)
theirs | Source branch changes (during merge - another branch, during rebase - current branch
git merge [another_branch] -X ours | Automatically resolve merge conflicts choosing changes from current branch
git merge [another_branch] -X theirs | Automatically resolve merge conflicts choosing changes from another branch
git rebase [another_branch] -X ours | Automatically resolve rebase conflicts choosing changes from another branch
git&nbsp;rebase&nbsp;[another_branch]&nbsp;&#8209;X&nbsp;theirs | Automatically resolve rebase conflicts choosing changes from current branch


## git investigating ##

Command | Description
--- | ---
git cherry -v | Show local commits yet to be pushed to upstream
git branch -v | Show all local branches with respective tip commits and ahead/behind status
git branch --no-merged develop | Show all local branches not merged to develop branch
git branch --merged develop | Show all local branches merged to develop branch
git branch --merged develop -r | The same, but for remote branches <br> (-a to see both remote and local)
git remote -v | TO DESCRIBE
git tag --list --contains d485e45 | Show all tags containing given commit
git rev-list --left-right <br> --count [branch_name_1]...[branch_name_2] | Display ahead/behind between two given branches
git merge-base [branch_name_1] [branch_name_2] | Show last common parent commit between two given branches
git describe --tags [commit_hash] | Show the most recent tag among parent commits
git describe --contains [commit_hash] | Show tag which contains given commit
git blame | TO DESCRIBE


## git log ##
Command | Description
--- | ---
git log -10 --pretty=format:'%h - %<(20)%an \| %<(14)%ar \| %s' | Show last 10 commits with pretty formatting
git log [commit_hash_1]..[commit_hash_2] | Show given commit range
git log HEAD..@{u} | Show all new commits from upstream
git log --grep 'strange bug'  | Filter by commit message containing text 'strange bug'
git log --follow \*ShopController.js | Filter by affected file 'ShopController.js'
git log --author='John' | Filter by author name or email (case-sensitive)
git log HEAD~100..HEAD -S 'console.log(' | Filter by changed source code text 'console.log('
git log -p | Show the full diff of each commit
git log --oneline | Show only one line per commit
git log --stat | Show file change statistics
git log --first-parent | TO DESCRIBE


## git diff ##
Command | Description
--- | ---
git diff | Show only non-staged changes (difference between working copy and index)
git diff --staged | Show only staged changes (difference between index and last commit), the same as `git diff --cached`
git diff HEAD | Show all uncommitted changes (difference between working copy and last commit)
git&nbsp;diff&nbsp;develop&nbsp;--staged&nbsp;--&nbsp;\*ShopController.js | Show changes regarding specific file between index and develop
git diff [commit_hash_1] [commit_hash_2] | Show changes between two given commits
git diff [commit_hash_1] [commit_hash_2] > some.patch | Dump changes as patch file
git apply some.patch | Apply that patch file
git diff --name-only [other_args] | Show only file names
git diff --name-status [other_args] | The same, but also with file status
git diff --check | Show any left merge conflict markers and whitespace errors
git show | Show changes in last commit


#### How to check if one commit is parent for another (copy-paste it to shell) ####
```bash
left=origin/develop; right=14bcbf1;\
read leftCount rightCount <<< $(git rev-list --left-right --count $left...$right); echo;\
echo "left '$left' contains $leftCount unique commits" ;\
echo "right '$right' contains $rightCount unique commits" ;\
if [[ $leftCount > 0 && $rightCount == 0 ]]; then echo "so right is parent for left";\
elif [[ $leftCount == 0 && $rightCount > 0 ]]; then echo "so left is parent for right";\
else echo "so they don't refer one another";fi
```

## git tricks ##

Command | Description
--- | ---
git clean -xdf | Delete all untracked (ignored) files and folders
git clean -nxdf | Just display what would be deleted
git archive --format zip --output filename.zip [commit_hash] | Create zip archive of project state according given commit
git shortlog -sne | List all developers


## git references ##

Reference | Description
--- | ---
[commit_hash] | See git terms
[branch_name] | See git terms (don't forget about 'origin/[branch_name]')
[tag_name] | See git terms
HEAD | See git terms
@ | Equal to HEAD
@\{u\} | The upstream of current branch: @{upstream}
HEAD@{1} | Take previous HEAD location
HEAD@{N} | Take HEAD location from history (see git reflog)
@{-1} | Take previous checked out branch
\- | The same, but only in `git checkout -` and `git merge -`
@{-N} | Take N-th last checked out branch
MERGE_HEAD | The tip of branch you are merging from
ORIG_HEAD | During merge or rebase, the original tip of current branch
[ref] | Any of above, points to certain commit
[ref]~1 | Take its parent (exactly direct one in case if multiple parents)
[ref]~ | The same
[ref]~2 | Take grandparent
[ref]~~ | The same
[ref]~N | Take commit located N steps back in hierarchy
[ref]^1 | Take exactly first parent of merge commit, i.e. direct one, equal to [ref]~1
[ref]^ |  The same
[ref]^2 | Take exactly second parent of merge commit, i.e. tip of merged branch
[ref]^N | Take exactly Nth parent (one step back in hierarchy anyway), see octopus merge
[ref]^^ | Equal to [ref]~2 (two steps back)
[ref]\~5^2\~3 | Go 5 commits back, then turn to second parent and then 3 commits back more
develop@{yesterday} | TO DESCRIBE


## git setup ##

Command | Description
--- | ---
git version | Show your git version
which git | Show your git location
git config --global user.name '[firstname lastname]' | Set your default name across all repos
git config --global user.email '[your_email@site.com]' | Set your default e-mail
git config --global push.default current | TO DESCRIBE
git config --global alias.f '!git fetch && git status -sb' | Create an alias 'git f' for given git commands
git config --global -e | Open global git config file in text editor
git fsck  | Checks local repo integrity
diff.renameLimit | TO DESCRIBE
merge.renameLimit | TO DESCRIBE


## git advanced commands ##
Command | Description
--- | ---
git merge $(git commit-tree [commit_hash]^{tree} -p HEAD -m 'Any message') | Create new commit on the current branch so its project state will be the same as in another commit



## git tips ##
* Because [commit_hash], [branch_name], HEAD, etc. are just only references, you can use one in place of another
* Local branches, remote branches, remote urls are stored as easy-to-edit text files in .git folder
* You can clone (instead of just copy) your local repo into another local folder (and probably fix origin after it)
* You can add one existing local repo as a remote for another
* Before performing some operations (like big rebase) do create and store a separate backup branch
* Close and open gui client if no changes visible there
* Press TAB to autocomplete commands, their options, branch names (may be you need to set it up)
* You can use git aliases - [example](https://github.com/capslocky/my-git-config#aliases)
* How to exit vim text editor: with saving changes - just type [ESC :wq], without saving [ESC :q!]
* Prefer SSD over HDD to boost git operation performance
* `git help`, `git help pull` - embedded documentation
* `GIT_TRACE=1` - enable git tracing (there are others like `GIT_CURL_VERBOSE=1`)
* Typically you need only high-level commands (aka porcelain). But there also plumbing (low-level) commands, which allow you to implement much more advanced scenarios


## why use git shell? ##
* You just can't do most of operations with gui client
* You don't have to stop using your gui client, because shell greatly complements any gui client
* It is the fastest way in many everyday cases
* Much less chance to involve your repo into 'bad' state and much easier to fix it
* You always have the shell and can rely on it
* You can introduce aliases and scripts for frequent operations
* You directly interact with repository (useful shell output, no gui bugs or stuck)
* You better understand how git works and get more 'aha!' moments 
* You will be cool


## interesting things about git ##
* Git was created by Linus Torvalds back in 2005 for Linux kernel development collaboration specifically
* Repository can have more than 1 root (inital) commit, there are 4 in Linux kernel
* Octopus merge is a merge from more than 2 parent commits, it inspired octocat - mascot of GitHub
* Official git manual starts with line 'git - the stupid content tracker'


## git links ##
* https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
* https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf
* https://orga.cat/posts/most-useful-git-commands
* https://github.com/git-tips/tips
* https://github.com/luisbg/git-cheat-sheet
* https://github.com/arslanbilal/git-cheat-sheet
* https://www.sourcetreeapp.com/
