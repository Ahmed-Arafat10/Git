# Git Version Control

- To Configure git on Ubuntu install SSH and generate a key_pair, then copy public key and put it in SSH
Option in Your GitHub Account, then go to your repo then just copy SSH link {Not HTTPS}


## 2. Version Control Systems & Git - Overview :
------------------------------------------------

- Git Workflow:
```
Working             Staging         .git directory
Directory            Area             {Local Repo}
```

- Three different states:
    1) ```Modified``` : You modified the file but you have not committed your changes yet
    2) ```Staged``` : You have marked a modified file to be present in the next snapshot of your file system,
    information about such changes are present in file with name index thats why we can say files are staged
    or file at index {Both are correct}
    3) ```Committed``` : Data is safely stored in your local database {Snapshot}


- Every snapshot of the files contains information about the author of the snapshot, this is done
to easily identify who broke system or created defect file

- Configuration levels:
    - ```System```: All local users in PC + All their repositories
    - ```Global```: All repositories on the computer for current user
    - ```Local```: Only current repository {After running $ git init to create .git folder}

- Note : Values on the lower level overrides valued of the upper level

- Example:
```
git config --global user.name
```

- All of git command are written in git bash {Windows} OR in terminal {Linux}


- To Tell git who you are
```
git config --global user.name "AA"
git config --global user.email "AA@gmail.com"
```

- Note: Any commit will save your email and your name to know who did what


- To check value of user.name
```
git config user.name
```

- To check value of user.nemail
```
git config user.email
```

- List all properties with values
```
git config -l
```
OR
```
git config --list
```

- To change default text editor, make vi editor your default editor
```
git config --global core.editor "vi"
```
OR Use Notepad++ in windows
```
git config --global core.editor "C:/Prgram Files/Notepad++/Notepad++.exe"
```


## 6. Git repo init, First commit and main branch  :
----------------------------------------------------


- Two ways to create a repository:
    - Create repo locally
    - Clone existing remote repo


- Create a local repo {Creating a .git directory}
```
git init
```

- Add file.txt to stage area
```
git add file.txt
```

- Add some specific files to staging area
```
git add file1.txt file2.txt file3.txt
```

- Add all files that end with .cpp extension to stage area {Mask Method}
```
git add *.cpp
```

- Add all files/folders to stage area
```
git add .
```

- Check status of repo in your current branch
```
git status
```

- Check status of repo in your current branch with short version flag ```-s```
```
git status -s
```
> A : stands for files are ADDED to staging area and need to be committed <br>
> ?? : untracked file {file that is created in working directory while its not in staging area}


- If you forgot any command use --help flag
```
git status --help
```
OR
```
git status -h
```

- Commit new changes {Create a snapshot (version)}
```
git commit -m "Message"
```
> -m : message that describes changes that happened in that snapshot (version)


- Note : Usually commit message of first commit is "init commit"


- Add to stage area & Commit in one line
```
git commit -a -m "Message"
```
> -a : Tell the command to automatically stage files that have been modified and deleted, but new files
you have not told Git about are not affected.
- VIP Note : This works only if you have modified an existing file NOT creating a new one




## 7. Git ignoring & Git log :
------------------------------

- It does not make any sense to track all files in project as some of them are just
logs files or binaries files that are generated during program compilation, so track only source code
and configuration files


- Remove a file from staging area
```
git rm --cached file.txt
```
> If you didn't use flag ```--cached``` it is going to remove file from file system too, Be Curefull


- Remove a folder from staging area
```
git rm -r --cached <DirName>
```
> If you didn't use flag ```--cached``` it is going to remove folder from file system too, Be Curefull


- Ignore Files Or Directories
```
touch .gitignore
nano .gitignore
```
Inside it :
```
    *.class     # All files that ends with extension .class
    bin/        # Any file in bin folder
    file1.txt   # Ignore Specific file
```
- Then you can use ```git add .``` and those files are not going to be added to staging area

- After adding ```.gitignore``` file it will be shown as an untracked file {that is needed to be added to staging area}
you also can ignore it by typing it in ```.gitignore``` file HAHAHAHA


- View previous log of created commits in your current local branch
```
git log
```

- View last 2 log of created commits in your current local branch
```
git log -2
```

- Change formatting to show only Checksum (Hash ID) and Commit message {Not used widely}
```
git log --pretty=oneline
```


## 8. Git undoing things & Vi text editor :
-------------------------------------------

- Change comment of last commit {You are NOT creating a new commit}
```
git commit --amend
```
> And then terminal will open VI to edit message of last commit
- VIP Note: if your staging area is same as your last local commit then you used ```--amend``` option, this will just
change message of last commit, but if your staging area is different from last commit {you have added a new file for example}, then after using ```--amend``` option last commit will contains your new staging area {Will be overridden}
{```--amend``` takes your current staging area and override last commit content (if both are same nothing will be changed) + being able to change its message} <br>
> Checksum {Hash Code} of commit will change


- Add latest staging area in previous commit {You are NOT creating a new commit}
```
git commit --amend --no-edit
```
> ```--amend --no-edit``` option is same as ```--amend``` but without allowing you to change the last commit message <br>
> Checksum {Hash Code} of commit will change


- Unstage a file from staging area
```
git restore --staged <FileName>
```
OR
```
git restore --staged *
```
> VIP Note : ```git rm --cached <FileName>``` command will remove file from staging area whether this file is modified or just added, while ```git restore --staged <FileName>``` command For modified file its not going to remove it from staging area, its going to neglect changes of it {this is done if you added new modified file to staging area accidentally but you don't want to commit that change so you undo it from staging area} OR it removes new ADDED file from staging area


- Restore a file from last commit {Will remove any changes in that file}
```
git restore <FileName>
```
> Note : this can take place when changed file is not in staging area {you didn't yet use ```git add .```},
if file is changed (from last commit) but in staging area you cannot restore it,
you only can restore it when changed file is in modified area

- Note: we can restore anything that is committed, while changes that aren't saved in commits can not be restored
{```git reflog```}
    
- Show files in staging area
```
git ls-files
```



## 9. Git remote repositories :
-------------------------------

    
- Check if your local repo is connected to remote repo
```
git remote -v
```
> Will list all created remote repos


- Add a new remote repo with shorthand name "origin"
```
git remote add origin <GitHubLink>
```
> ```origin``` will now be used instead of GitHub URL to make referencing much more easier


- Push your commits & Connect local master branch with remote master branch
```
git push origin -u <master>
```
> -u : stands for upstream {This will link local repo to remote one, then when you enter ```git pull``` it will understand that you want to pull changed from exactly that remote branch}


- Clone remote repo to your machine
```
git clone <GitHubLink>
```



## 10. SSH Connection :
-----------------------


- SSH {Secure Socket Shell} : its a secured protocol that allows you to connect to remote computer using terminal
using SSH you can log in to another computer from anywhere and perform any command on it
- The goal of SSH is to make remote connections to computers much more secure
- Establish a SSH connection to identify yourself without using username/password everytime
- SSH keys comes in pairs : public and private
- Public key can be stored in any remote server as GitHub
- Private key is stored in your machine


- Change remote URL of already created remote repo {EX: origin}
```
git remote set-url origin <NewGitHubLink>
```

- Remove a remote repo from your machine
```
git remote rm <RemoteRepoName>
```


## 11. Git Branching :
----------------------


- Create a new LOCAL branch
```
git branch <BranchName>
```

- List all LOCAL Branches
```
git branch
```

- List all REMOTE Branches
```
git branch -r
```
> -r: stands for remote


- List ALL Branches {LOCAL + REMOTE}
```
git branch -a
```
> -a: stands for all {Linux}


- Note : ```git branch``` command is not used among developers as this only create the
branch but not switch to it, they prefer to use ```git checkout``` command that creates the branch then switch to the created branch


- Switch to a branch
```
git checkout <BranchName>
```

- Create a new Local branch then switch to it
```
git checkout -b <BranchName>
```
> -b: stands for branch


- New command in latest git version: {Not common as it is new}
- Switch to a branch
```
git switch <BranchName>
```

- Create a new branch then switch to it
```
git switch -c <BranchName>
```
> -c: stands for create


- Navigate back to previous branch
```
git switch -
```

- Note: Branch name should be descriptive {what changes or features will be in this branch}


- Show commits of current branch
```
git log
```
> Note : your branch will have same commits history of master + commits of it {In future}, as Git creates a pointer to last commit of master so it have the commits history of master branch
```
A--B--C <-- Master/Branch
       \    Branch {No commits yet}
```
            
- Show commits of ALL branch
```
git log -all
```

- Show commits of a specific branch
```
git log <BranchName>
```
> Can also work with remote repo example : ```git log origin/master```


- Remove a LOCAL branch
```
git branch -d|D <BranchName>
```
> -d: stands for delete


- Remove a REMOTE branch {In GitHub}
```
git push <RemoteName> --delete <BranchName>
```
- Example:
```
git push origin --delete Branch#2
```
- If you forget that command {or any other one} use Linux grep : ```git push origin --help | grep delete```
    
- VIP Note :
- You can navigate to different commits using commit checksum {Hash ID}
```
git checkout <checksum>
```
- Now you are in ```detached HEAD``` state, you are not in a specific branch
- You can use this feature to navigate to different versions of your codes and observe changes in working directory files
- you can also create a commit in this state {Not Recommended} but once you have switched ```git switch -```  from this state, you wont be able to see this commit in commit tree history {Not saved in it}, but you can navigate to it again if you have saved
its commit checksum, For Example : ```$ git checkout 739d1d3a21b379147efe5e3622d4cd674871eb1a```



## 12. Pull Requests & Merge Requests :
---------------------------------------


- Three types of merging Requests:
        1) Merge commit
        2) Squash and Merge
        3) rebase and Merge

- Rest is in GitHub Pull Request Menu
    
    
    
## 13. Updating local repository (fetch, merge, pull) & Team development demo :
-------------------------------------------------------------------------------


- Master branch -> branch on your PC {local}
- Region Master Branch -> branch in GitHub Repo


- In case some commits are exist in Region Master Branch, while local is not aware of use ```git fetch``` command

- VIP note: if you are on Devloper#1 branch LOCALLY then using fetch will search for any changes in REMOTE Devloper#1 branch
- LOCAL Devloper#1 branch -> REMOTE Devloper#1 branch
- LOCAL Master branch -> REMOTE Master branch
```
git fetch
```
> if there is a message, this means that some changes were downloaded from remote, if not you are up to date
- Note : it just tells you that some changes are exist in remote but not in your local machine, but it don't pull them {merge them to your local branch}
- VIP Note : ```git fetch``` command will work only one time and after fetching data from remote repo into local one, if you use this
command again it wont work {As you already fetched new changes}

- Then what is the purpose of this command at all?
- Imagine that you are working on the new changes and you don't want to merge latest code into your branch, And you would like to know whether there are any changes in remote branch that are needed to be merged
then use ```git fetch``` command


- If you want to download all changes from region master branch to your local master branch {VIP Note in Line #458 is also applied}
```
git merge
```

- Git pull is combination of fetch + merge {both in one step} {VIP Note in Line #458 is also applied}
```
git pull origin master
```


    
## 14. Merge Conflicts :
------------------------

-> Image if you in remote master branch have a [Web/index.html] that contains
```
<html>
<head>
</head>
<body>
<h1>Hello World</h1>
</body>
</html>
```

- Now you have created a new branch ```developer#1``` from remote master for first developer
in this branch developer add a ```style/index.css``` file and edit ```Web/index.html``` to be:
```
<html>
<head>
<link rel="stylesheet" href="../style/index.css">
</head>
<body>
<h1>Hello World</h1>
</body>
</html>
```
- Then push this branch into new remote branch called ```developer#1```


- Now you have created a new branch ```developer#2``` from remote master for second developer
in this branch developer add a ```style1/index123.cdd``` file and edit ```Web/index.html``` to be:
```
<html>
<head>
<link rel="stylesheet" href="../style1/index123.css">
</head>
<body>
<h1>Hello World</h1>
</body>
</html>
```
- Then push this branch into new remote branch called ```developer#2```

- Now if you pull then merged ```developer#1``` branch into master in GitHub Menu, this will be fine but if you then want to pull then merged ```developer#2``` branch into master {master + developer#1} in GitHub there will be a conflict , why??
- Because commit of ```developer#1``` branch is that it added a new ```style/index.css``` then edited line #3 in ```Web/index.html```
and after merging it into master branch, the last commit will be this commit
- Then as last commit of ```developer#2``` branch is that it added a new ```style1/index123.css``` then edited ALSO line #3 in ```Web/index.html``` {Same file, Same Line}
- This means that there will be a conflict in  line #3 in ```Web/index.html``` as in both commits this line is edited, so you cannot merge ```developer#2``` branch unless you fixed this conflict, this is done by first
```
git pull origin master
```
> Add new changes from remote master {these changes are commit of developer#1 branch Line #500 here}
- Then edit this file
```
nano Web/index.html
```
- Then use ```git add .``` and ```git commit``` then pull to remote ```developer#2``` branch, at this moment, there will be no conflicts in pull page in GitHub, and you can now merge it into master branch only by {MERGE COMMIT Option} will know later why

- NOTE : This method for fixing conflicts is not best practice




## 15. Git Rebasing & Force Update of remote repository :
---------------------------------------------------------


```
git rebase
```
> To rebase changes from another Branch
VS
```
git pull --rebase 
```
> fetch + rebase command, this means that it first fetch from remote repo 
and then rebase

```
  0--
 /   \
0-----0
 \
  0---0
```
- After solving a conflict {Editing files} use this command to continue rebase process
```
git rebase --continue
```

- To Stop rebase process
```
git rebase --abort
```

- To skip conflict {Not recommended at all}
```
git rebase --skip
```

    
- Now after resloving the conflict add modified files in staging area ``` git add .``` then continue rebase process ```$ git rebase --continue```

```
  0--               Feature#1
 /   \
0-----0
        \
         0---0      Feature#2
```

- Now if you ```git push``` into Feature#2 it will gives you an error, thats because remote Feature#2 branch has a different commit history compared to local one, because ```git rebase``` command changes git history. Now both local and remote Feature#2 branch
commit history is not same as each other

- I need to tell git which version is correct
```
git push -f
```
> BE CAREFUL as it will overrides remote branch commit history with your local one <br>
> Use it with only branches not with MASTER branch

```
Remote A---B---C---D
Local  A--E
$ git push -f
Now remote branch will be: Remote A--E
{ALL of remote tree will be same as local tree}
```


- Four rules of happiness:
    1) Always create branched from master, not from the other development branches.
    2) Force update and change commit history only on your branch you are sure no body use it
    3) use ```--force-with-lease``` instead of ```-f```
    4) Always rebase on the origin master branch before creating a pull request

- It is a safer option that will not override any work on the remote branch if more commits were added to the remote branch by another team member.
```
git push --force-with-lease
```
> Best practice : rebase on the region master as often as you can to fix conflicts gradually and to test your implementation on the latest version of the code during the development to not spend a lot of time.




## 16. Git Interactive Rebase :
-------------------------------


- If you want to change message of last Commit
```
git commit --amend
```
- But what if you want to change second last one

- ```Interactive Rebase``` : It makes it easy to clean up your commits before they get rebased or moved into another branch

```
git rebase -i HEAD~3
```
> i: stands for interactive rebase

- Then substitute for ```r``` -> ```reward``` instead of ```pick``` in commit you want to change its message
then save and close editor



- You can combine {squash} many commits into just one commit to ensure git clean history {If they are all related to same feature}
```
git rebase -i HEAD~3
```
- Then substitute for ```s``` -> ```squash``` instead of ```pick``` for all commits except first one then save and close editor

- Note : merge conflict may happens during squashing so you will fix it manually
- It then will merge those commits in just one new commit that will have a different checksum {Hash ID}
- As we are changing Git commit history of local repo, so to pull these changes into your remote feature branch you have to force pull as tree history of local becomes different from remote one, then use:
```
git push --force-with-lease origin <BranchName>
```
> Remember : ```--force-with-lease``` It is a safer option that will not override any work on the remote branch if more commits were added to the remote branch by another team member.



## 17. Git reset :
------------------


- When to use ```git reset```:
    - Undo last changes
    - Change commit history
    - Restore state of the remote branch
    - Restore state of the branch after unsuccessful rebase

- Go back to a commit, in which all files in latest commit will present in working directory but changes between old
and latest commit will be in staging area waiting to be committed ```git commit -m```
```
git reset --soft <CommitID>
```
OR
```
git reset --soft HEAD~n
```
    
```
Commit #10 : p1,p2,p3,p4,p5
..
..
Commit #5 : p1,p2
use : $ git reset --soft HEAD~5
Now working directory is : p1,p2,p3,p4,p5 {Not changed from latest Commit}
Now Staging Area is : p3,p4,p5 are waiting to be committed { Staging Area of Commit #10 }
Now latest commit is : p1,p2 { Commit #5 }
```

- Go back to a commit, in which all files in latest commit will present in working directory but changes between old
and latest commit are in untracked mode waiting to be in staging area ```git add .```, then to be committed ```$ git commit -m```
```
git reset --mixed <CommitID>
```
OR
```
git reset --mixed HEAD~n
```
OR
```
git reset <CommitID>
```
> Default option without any flags is ```--mixed```

```
Commit #10 : p1,p2,p3,p4,p5
..
..
Commit #5 : p1,p2
use : $ git reset --mixed HEAD~5
Now working directory is : p1,p2,p3,p4,p5 {Not changed from latest Commit}
Now Staging Area is : p3,p4,p5 are untracked files { Staging Area of Commit #5 so, needed to use $ git add .}
Now latest commit is : p1,p2 { Commit #5 }
```



- Go back to a commit in which files in working directory will be same as commit you have chosen {Replace them}
```
git reset --hard <CommitID>
```

- Go back 3 previous commit
```
git reset --hard HEAD~3
```
OR
```
git reset --hard <CheckSumID>
```
    
```
Commit #10 : p1,p2,p3,p4,p5
..
..
Commit #5 : p1,p2
use : $ git reset --hard HEAD~5
Now working directory is : p1,p2 { Same As Commit #5 }
Now Staging Area is : p1,p2 { Same As Commit #5 }
Now latest commit is : p1,p2 { Same As Commit #5 }
```

- If you want to rest working tree as it is in a remote repo :
- To fetch latest state of remote repository
```
git fetch --all
```
- To restore the state of remote master branch
```
git reset --hard origin/master
```



## 18. Git stash :
------------------


- When to use stash:
    - Temporarily put work aside
    - Apply the same changes on multiple branches
    - Create new Branch based on the current changes later

- Now if you have modified some files and used ```git status```, those files will be presented in section of waiting to be Staged
- Add modified OR new files to stash {Not presented yet in staging area}
```
git stash
```
> Now changes are in stash


- Now if you used ```git status```, working tree will be clean {Nothing to commit}

- If you need changes that are saved in TOP of stash {Import them}
```
git stash apply
```


- Stash works like a stack and applies LIFO

- list all changes in stash stack
```
git stash list
```
> Last stash has index {0} its on top of stack

- Import {Apply} changes from a stack with index N
```
git stash apply stash@{n}
```

- Add modified OR new files to stash {Not present in staging area} with a MESSAGE {Best Practice}
```
git stash save "Message"
```

- If you need changes that are saved in TOP of stash {Import them} and then REMOVE IT
```
git stash pop
```

- VIP Note : - You can only stash files that are in staging area OR files that are tracked by Git
             - Stash only save file that is modified {Not all other files in working directory}
             - A conflict may arise will using stash so fix it manually


- Stash can save untracked files {files that are created but not in staging area}
- To add them in stash
```
git stash -u
```
> -u : stands for untracked files


- Add file that are untracked + ignored by ```.gitignore``` {Rare To Use}
```
git stash -a
```
> -a : stands for ALL


- Create a branch from stash
```
git stash branch <BranchNameYouWantToCreate> <StashID>
```
> Without specifying stash ID first stash from stack will be used


- Remove a stash form stack {without applying it}
```
git stash drop stash@{N}
```

- Clear ALL stash form stack {without applying it}
```
git stash clear
```



## 19. Git reflog :
-------------------

- While using git you may lose a commit foe example you used force delete or hard reset or interactive rebase to squash
commits
- In git anything that is commited can be restored, git wont never restore files that were never in staging are or not committed before

- While we are working, Git silently records what our head pointer and how does it look like
- Each time we create a snapshot or switch branches the reflog is updated

- Navigate history of all changes in repo using :
```
git reflog
```
    
- Each commit, reset on origin/master branch, different branches


- Show all commits with reflog reference and copy Checksum of deleted commit
```
git log -g
```

- Create a new branch with Checksum of deleted commit
```
git branch lost_changes <CommitCheckSum>
```   
> Now ```lost_changes``` branch will contains same files as deleted commit


- Note : information in reflog is stored for 90 days

- Simulate a situation -> if you have used ```git reset --hard``` command to go back to previous commit {from commit ```REMOVINGGG``` to commit ```SQUASHINGGG```},
then you want to restore deleted Commit ```REMOVINGGG```

- Show reflog for past 1 hour
```
git reflog --since="1.hour"
```
> ```day``` is used also instead of ```hour```


```
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{0}: reset: moving to HEAD@{1}
981ecb1 (lost_changes) HEAD@{1}: reset: moving to HEAD@{3}
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{2}: reset: moving to HEAD@{1}
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{3}: reset: moving to HEAD@{0}
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{4}: reset: moving to a2ef2d547d4e34f47c22fc6a499f632ec14a7a32
981ecb1 (lost_changes) HEAD@{5}: commit: REMOVINGGG
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{6}: checkout: moving from test1 to master
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{7}: checkout: moving from master to test1
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{8}: checkout: moving from test to master
b0326e1 (test) HEAD@{9}: commit: ddd
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{10}: checkout: moving from master to test
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{11}: reset: moving to HEAD
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{12}: checkout: moving from test to master
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{13}: checkout: moving from master to test
a2ef2d5 (HEAD -> master, origin/master, test1) HEAD@{14}: checkout: moving from test to master
```


- Now restore commit history to that commit
```
git reset --hard HEAD@{n}
```
- Above Example : 
```
git reset --hard HEAD@{5}
```

- Now deleted commit will be restored




## 20. Git cherry-pick :
------------------------

- Used to modify commit history {Not The Best Practice}, regular merge is preferred when it is possible

- When to use cherry-pick : - Deliver hotfix to the end user as fast as possible
                            - Undoing changes and restoring lost commits
                            - Regular team collaboration


```

    G--H                  Feature
   /
A--B--C--D--E--F--H*      Production
       \
        I
```

- cherry-pick is used to just take one commit from a feature branch and put it on top of another branch
- Not The Best Practice

- Go to branch you want to copy commit in and type :
```
git cherry-pick <CommitCheckSum>
```

- To continue cherry-picking process after resolving a conflict
```
git cherry-pick --continue
```

- If something went wrong during resolving a conflict and want to stop cherry-picking process
```
git cherry-pick --abort
```

- Cherry-pick multiple commits at once
```
git cherry-pick <CommitCheckSum1> <CommitCheckSum2> <CommitCheckSum3>
```

- Best practices of using cherry pick:
    - Prefer merge or rebase when possible
    - Avoid creating any duplication
    - Use 'x' option during cherry-pick command, this will specify hash code of original commit
      ```git cherry-pick -x```
    - This will automatically add hash code of original commit in comment message of new one




## 21. Cloning remote repository: git clone :
---------------------------------------------

```
git clone <GitHubURL>
```



----------------------------EXTRA-------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------
- If you want to remove a file from last commit
- first copy commit to staged area and then remove commit
```
git reset --soft HEAD~1
```

- Then remove file you don't want
```
git reset HEAD <file>
```
----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------



----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------
## Combining Git commits with squash :
--------------------------------------

- We’ll say my starting point is my bug fix branch with 3 commits.

It would be nice if I didn’t have to preserve these extraneous commits as separate entities since they are all related to a bug fix.
- I’d rather combine them together into one clean commit.

- With my bug fix branch checked out, I’ll start by running the interactive rebase command with HEAD~3. This lets
Git know I want to operate on the last three commits back from HEAD.
```
git rebase -i HEAD~3
```
- Git will open up your default terminal text editor (most likely vim) and present you with a list of commits:

```
pick 7f9d4bf Accessibility fix for frontpage bug
pick 3f8e810 Updated screenreader attributes
pick ec48d74 Added comments & updated README

# Rebase 4095f73..ec48d74 onto 4095f73 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
```

- There are a couple options here, but we’ll go ahead and mark commits we’d like to meld with it’s successor by
changing pick to squash. (If you’re using VIM, type i to enter insert mode)
```
pick 7f9d4bf Accessibility fix for frontpage bug
squash 3f8e810 Updated screenreader attributes
squash ec48d74 Added comments & updated README
Press ESC then type :wq to save and exit the file (if you are using VIM)
```

- At this point Git will pop up another dialog where you can rename the commit message of the new, larger squashed commit:

```
# This is a combination of 3 commits
# This is the 1st commit message:

Accessibility fix for frontpage bug

# This is the commit message for #1:

Updated screenreader attributes

# This is the commit message for #2:

Added comments & updated README

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit
```

- Simply saving this file without making changes will result in a single commit with a commit message that is a
concatenation of all 3 messages. If you’d rather rename your new commit entirely, comment out each commit’s message,
and write you’re own. Once you’ve done, save and exit:

- That’s it. You can either ```merge``` or ```rebase``` your branch back to mainline.
----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------


----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------
## Rebase:
----------


- When I start development I always make sure the code on my local machine is synced to the latest commit from remote master
# With my local master branch checked out
```
git pull
```

- Next, I’ll check out {Create} a new branch so I can write and commit code to this branch – keeping my work separated from the
master branch
```
git checkout -b my_cool_feature
```
    
```
         /      Feature_Branch
A---B---C       Master
```

- As I’m developing my feature, I’ll make a few commits…
```
git add .
```
```
git commit -m 'This is a new commit, yay!'
```

- Do this step three time {For Example} to have three commits in that branch

```
              X --- Y --- Z Feature_Branch
             /
A --- B --- C               Master
```

- Note: while I’m developing it’s likely that my fellow developers will have shipped some of their own changes to
remote master. That’s ok, we can deal with that later.

- Now that I’m done developing my feature, I want to merge my changes back into remote master. To begin this process
I’ll switch back to local master branch and pull the latest changes. This ensures my local machine has any new
commits submitted by my teammates.
```
git checkout master
```
    
```
git pull
```
    
```
              X --- Y --- Z     Feature_Branch
             /
A --- B --- C --- D -- E        Master
```

- What I want to do now is make sure my feature will jive with any new changes from remote master OR i just want the
changes from master as I will continue working based on them so I want to have them in my feature branch. To do this,
I’ll checkout {Switch To} my feature branch and rebase against my local master. This will re-anchor my branch against the latest
changes I just pulled from remote master. Additionally at this point, Git will let me know if I have any conflicts
and I can take care of them on my branch
```
git checkout my_cool_feature
```
    
```
git rebase master
```
> Note : when you use ```git rebase``` you are rebasing from LOCAL master repo, so make sure first that in local master Branch you have pulled new changes from remote master branch

```
                         X^--- Y^ --- Z^    Feature_Branch
                        /
A --- B --- C --- D -- E                    Master
```

- Now that my feature branch doesn’t have any conflicts, I can switch back to my master branch and place my changes onto master,
this will put all of Feature_Branch commits on top of master branch {It now will includes all of changes in Feature_Branch}
```
git checkout master
```
    
```
git rebase my_cool_feature
```
- Since I synced with remote master before doing the rebase, I should be able to push my changes up to remote master without issues.

```
git push origin -u master
```

- VIP Note: Don't use ```git rebase``` command in a shared Feature Branch {Just in a branch you are the only one working on}
- Because time arrangement of commits will not be accurate For Example :

```
  3                       3               3--4                                   3--4
 /                       /               /                                      /
1--2   Rebase-->     1--2            1--2--5       Rebase-->             1--2--5
```

- In that case its not timely accurate

----------------------------------------------------------------------
----------------------------------------------------------------------
----------------------------------------------------------------------
