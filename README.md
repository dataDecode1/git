# Git Guide

git add >100mb files - https://www.youtube.com/watch?v=W4RCeVSs1Fg

tagging git repos - https://stackoverflow.com/a/18223354/5757129

create a new branch than default - https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/creating-and-deleting-branches-within-your-repository

move repos from GHE 2 GH - https://gist.github.com/stevemar/06ace005f82691435d0b

All git commands at one place - https://twitter.com/data_decode/status/1275126824159379457?s=09

https://guides.github.com/

https://developer.github.com/

- Generate ssh keys - https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#platform-windows

- [Cheatsheet-All commands at one palce](https://github.ibm.com/Krishna-Damarla1/git/blob/master/github-git-cheat-sheet.pdf)

- [Install git, textmate, p4merge](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Git%20tools%20installations%20guide.pdf)

- [Initiate a project and project status check](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Initiate_project.png)

- [Make a existing project a git repo](https://github.ibm.com/Krishna-Damarla1/git/blob/master/existing_project_make_git_repo.png)

# Connect to remote repo from local and pull / push the changes
  - If ssh keys dont exist, generate them in .ssh folder - Generate ssh keys - https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#platform-windows
  - cd to location where you instantiated the git project with *git init . *
  - git **remote** add origin git@github.ibm.com:Krishna-Damarla1/rhel.git (ibm.com accepts only ssh connections)
    - add takes remote url asddress
    - origin is the name of the remote repo
  - git remote -v (after linking shows us 2 urls. one for fetch and another for push)
  - git clone git@github.ibm.com:Krishna-Damarla1/rhel.git (for cloning a existing git repo) 
  - git add . 
  - git commit
- [ssh connection](https://help.github.com/en/articles/connecting-to-github-with-ssh)
    - [Example sample](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Screenshots/Pull%2C%20change%2C%20push.png) of forking a remote repo, make changes in local and push back to remote 
-  HTTPS Connection
    - git **push** -u origin master --tags
      - origin is the name of the remote repo (if you name your remote repo something else, use that name here)
      - master is the name of the branch we gonna push from local to remote git repo. As we are currently in master branch, we wrote the name master.
    - When prompoted for remote repo connection details like username, pwd - get them from settings page of the page and enter in terminal.
 - [fetch all branches of a repo](https://stackoverflow.com/a/10312587/5757129)

# git add files
- git add * - add all files
- git add file1 file2 file 3 - add multiple specific files 
- git add folder-name
- git add -u 

# git commit and push
- git commit -m "deleted"
- git push origin master

# git remove files / directories / hidden files
- Remove directory and files inside it - ```git rm -r one-of-the-directories another_file another_dir```
- Remove file - ```git rm filename```
- Remove hidden files - ```rm -v .hiddenfile*``` (-v to delete hidden files)
- Delete all files and directories that git does not track - ``git clean -fdx```
  
- git rename file -  ```git mv actual_filename new_filename```

# Basics - commit, history, rename, gitignore
- Multiple file changes at once 
  -  Add & Commit in 2 steps
     - git add . 
     - git commit (Enter your multiline commit message in textmate editor and save)
  - Add & commit in single step
     - git **commit** -am "commit message" (-am parameter adds and commits at sametime)
- Get previous commits info
  - git show
  - [git log](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)
  - git **log** --oneline --graph --decorate --all 
      - --online - prettfied commit history in single line
      - --graph - branching hierarchy history
      - --decorate - which commits are of which brnaches
      - -- all - provides history for all branches that is provided in that repo
  - git doesnot have official history commnad to get all the commit history. Lets create one commands with alias
    - git config --global alias.history "log --oneline --graph --decorate --all"
      - --global creates the alias command "history" at user level (not at system level)
    - double check the newly created alias.history command 
      - git config --global --list
  - git **history**
    - shows all the history
  - git reflog 
    -  git log shows us the commit messages and commit ids. reflog shows us what actions we have taken at those commit ids. 
- Get all files that git is tracking
  - git ls-files
- Unstage the changes after adding with git add . but before commit
  - git reset HEAD file_to_be_unstaged
    - HEAD points to last commit of current branch
- git help for a specific command 
  - git **help** log
- Add files to git that are updated outside git
  - git add -A (-A covers all type of modificatiosn than -a)
- Exclude unwanted files in our git repo (like compiled files or log files)
  - Create a ignore file and all all files you want to ignore
    - mate .gitignore
       - enter the filename which you want to ignore
       - *.log (exclueds all log files)
       - *.pyc (exclueds all pyc files)
  - Add & commit the ignore file
     - git add **.gitignore**
     - git commit -m "Adding ignore files"

# Compare diff, Branch, Merge, tags, stash, reset
- [See differences between 2 commit points](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Screenshots/commit%20differences.png) 
   - get the all commit history with 
      - git hist
   - git **diff** pointer_number_commit_message HEAD. 
   - git difftool pointer_number_commit_message HEAD. Differences in [p4merge difftool](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Screenshots/commit%20diff%20in%20p4merge%20tool.png)
 - Create / Merge / Delete branches 
    - [Create and switch branches](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Screenshots/create%2C%20switch%20branches.png) 
      - Create **branch** - git checkout -b brach_name
      - Switch branch - git checkout branch_name
        -  Notice the head while checking history. Head pointer always points to the current branch
    - [Merge and delete branches](https://github.ibm.com/Krishna-Damarla1/git/blob/master/Screenshots/Merge%2C%20delete.png)
      - Before merging, switch to master branch
      - Merge branch to master - git **merge** branch_name
      - git history shows that head pointer now pointing to both master and branch_name. once branch got merged to main master branch, we no longer need it. Hence delete it
      - git branch -d branch_name
  -  Tags are labels we can keep at any commit point. 
      - git **tag** -a v1.0 -m "Release 1.0" (-a is annotated tag)
        - git tag --list (Displays all tags)
      - git show v1.0 (Shows all messages associated with major milestones)
  - save temporary changes with stashing
      - git **stash**
      - git stash list ( shows last commits)
  - Time travel using reset 
      - git **reset** commit_id --soft (reset to particular commit_id)
        - git history
        - git status
      - git reset commit_id --mixed (unstaged changes after reset)
        - head now points to reseted commit_id
      - git reset commit_id --hard (destructive of all reset modes)
      
## Push >100mb files
- https://git-lfs.github.com/
- tar -xzf git-lfs-darwin-amd64-v2.10.0.tar.gz
- sudo yum install git-lfs (in rhel7)

# Ref
- https://gist.github.com/VEnis/7465176
