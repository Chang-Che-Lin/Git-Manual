# Git-Manual

## Git Rule

++: new file

--: delete file

+-: modify file

## Git Initial Set

### user set

```bash
git config --global user.name "Zhe-Lin"
git config --global user.email "s1023165@g.ncyu.edu.tw"
```

### view .gitconfig

```bash
git config --list
```

### edit .gitconfig

```bash
sudo vim ~/.gitconfig 
```

### abridge status to st

```bash
git config --global alias.st status
```

### initial git of directory

```bash
git init
```

## Git Use Command

### view git status

```bash
git status
```

### add file to Staging Area

```bash
git add *.html  # Add .html file to Staging Area
git add --all   # Add all file to Staging Area
```

### commit file to Repository from Staging Area

```bash
git commit -m "Test"
git commit --allow-empty -m "Empty"   # Commit empty file
```

### add & commit  file at the same time

```bash
git commit -a -m "Test"
```

### view commit record

```bash
git log             # Detailed
git log --oneline   # Simple
git log --graph     # GUI interface
```

### give up all modify

```bash
git checkout .    # = git reset --hard @ ; All file return to last commit status
```

### give up part file modify

```bash
git checkout test.html    # Partial file return to last commit status
```

### remove file

```bash
git rm test.html
```

### untracked file

```bash
git rm --cached test.html
```

### rename file

```bash
git mv test1.html test2.html
```

### modify last commit message

```bash
git commit --amend -m "test2"
```

### add file to last commit

```bash
git commit --amend --no-edit
```

### untrack git file

```bash
git rm -rf --cached filename
```

### add ignore file

```bash
touch .gitignore  # .gitignore plase file's name that you want to ignore
```

### delete ignore file

```bash
git clean -fX
```

### view file detailed commit

```bash
git log -p test.html
```

## Git File History

### view file change

```bash
git blame test.html
git blame -L 5,10 test.html   # Show 5~10 lines
```

### compare status currently with last commit

```bash
git diff        # Before add file
git diff HEAD   # Before commit file
```

### compare status currently with assign commit

```bash
git diff commit
```

### compare commit currently with assign commit

```bash
git diff --cached commit    # = git diff --staged commit
```

### compare with two commit

```bash
git diff commit1 commit2
```

## Git Reset File

```bash
git log --oneline

e12d8ef (HEAD -> master) update test3
85e7e30 add test3
657fce7 update test2
abb4f43 add test2
cef6e40 update test
cc797cd add test
```

### replace file currently

```bash
git checkout test.html          # Replace file from Repository
git checkout HEAD~2 test.html   # Replace file from Repository before 2 HEAD
```

### unstage file

```bash
git reset   # File be placed to Working Directory from Staging Area
```

### go to HEAD before 1 master

```bash
git reset HEAD^ --mixed   # File be placed to Working Directory
                          # = git reset HEAD^ = git reset @^
git reset HEAD^ --soft    # File be placed to Staging Area
git reset HEAD^ --hard    # File be placed to Repository
```

### go to HEAD before 2 master

```bash
git reset master^^    # = git reset master~2
git reset HEAD^^      # = git reset HEAD~2
git reset 85e7e30     # 85e7e30 is HEAD number
```

### go back original HEAD

```bash
git reset e12d8ef --hard
```

### view all log

```bash
git reflog
git log -g
```

## Git Find Data

### find auther

```bash
git log --oneline --author="Leo"
```

### find commit message include "Test"

```bash
git log --oneline --grep="Test"
```

### find commit content include "test"

```bash
git log -S "test"
```

### find commit since 9am to 12am

```bash
git log --oneline --since="9am" --until="12am"
```

### find commit since 9am to 12am after 2017-01

```bash
git log --oneline --since="9am" --until="12am" --after="2017-01"
```

## Git Branch

```bash
git branch

* master    # e12d8e
  test      # b174a5
```

```bash
git log --oneline

e12d8ef (HEAD -> master) update test3
85e7e30 add test3
657fce7 update test2
abb4f43 add test2
cef6e40 update test
cc797cd add test
```

### view branch currently

```bash
git branch
git branch --remote   # Show remote branch
```

### new a branch

```bash
git branch test
```

### change branch

```bash
git checkout test
```

### new & change branch

```bash
git checkout -b test
```

### new & change branch from 657fce7

```bash
git checkout -b new_test 657fce7
```

### rename branch name

```bash
git branch -m test TEST
```

### delete branch

```bash
git branch -d test    # Delete branch have merged
git branch -D test    # Delete branch not merged
```

### delete remote branch

```bash
git branch --delete --remote origin/master    # = git branch -dr origin/master
```

### merge branch

```bash
git merge test
```

### rebuild original branch

```bash
git branch new_test b174a5a
```

### go back original branch after merge,rebase,reset

```bash
git reset ORIG_HEAD --hard
```

### view all branch

```bash
git reflog
git log -g
```

## Git Rebase

```bash
git log --oneline

e12d8ef (HEAD -> master) update test3
85e7e30 add test3
657fce7 update test2
abb4f43 add test2
cef6e40 update test
cc797cd add test
```

### add original branch to test branch

```bash
git rebase test   # HEAD -> original (HEAD isn't test)
```

### start interactive mode

```bash
git rebase -i cc797cd   # Interactive mode include e12d8ef to cef6e40
```

1. pick->reword
   - amend commit message

2. pick->squash
   - merge past commit
     - a. squash lines will merge upper pick
     - b. amend merge commit message

3. pick->edit
   - separate past commit
     - a.
       - git reset HEAD^
       - git status
     - b.
       - git add test_1.html
       - git commit -m "separate test to test_1"
     - c.
       - git add test_2.html
       - git commit -m "separate test to test_2"
     - d.
       - git rebase --continue
   - add past commit
     - a.
       - git reset HEAD^
       - git status
     - b.
       - touch test4.html
       - git add test4.html
       - git commit -m "add test4"
     - c.
       - git rebase --continue

## Git Revert

### add a commit to cancel last commit

```bash
git revert HEAD --no-edit
```

## Git Tag

```bash
git log --oneline

e12d8ef (HEAD -> master) update test3
85e7e30 add test3
657fce7 update test2
abb4f43 add test2
cef6e40 update test
cc797cd add test
```

### add a lightweight tag

```bash
git tag Test_Tag 85e7e30
```

### add a annotated tag

```bash
git tag Test_Tag 85e7e30 -a -m "add a annotated tag"
```

### show tag

```bash
git show Test_Tag
```

### delete tag

```bash
git tag -d Test_Tag
```

## Git Stash

### save working program to stash

```bash
git stash -u
```

### show stash list

```bash
git stash list
```

### take stash

```bash
git stash apply stash@{0}
```

### delete stash

```bash
git stash drop stash@{0}
```

### take & delete stash

```bash
git stash pop stash@{0}
```

## Git Filter-Branch

### massive modify data in every commit

```bash
git filter-branch --tree-filter "rm -f test.html"
```

### go back original HEAD after filter-branch

```bash
git reset refs/original/refs/heads/master --hard
```

### force remove data

1. force massive modify data in every commit

   - ```bash
     git filter-branch -f --tree-filter "rm -f test.html"
     ```

2. remove filter-branch backup

   - ```bash
     rm .git/refs/original/refs/heads/master
     ```

3. clear reflog
   - a.

      ```bash
      git reflog expire --all --expire=now
      ```

   - b.

      ```bash  
      git fsck --unreachable
      ```

   - c.

      ```bash
      git gc --prune=now
      ```

   - d.

      ```bash
      git fsck
      ```

## Git Cherry-Pick

### take commit from other branch

```bash
git cherry-pick 6a498ec               # Merge to original branch
git cherry-pick 6a498ec --no-commit   # Not merge to original branch
```

## Git Remote

### add a point to remote

```bash
git remote add origin https://github.com/Zhe-Lin/Git-Manual.git
```

### push master to origin's master

```bash
git push -u origin master   #-u: set remote origin/master is local master's upstream
```

### if local master have upstream

```bash
git push
git push -f   #--force
```

### if local master havn't upstream

```bash
git push origin master    # = git push origin master:master
```

### push local master to remote origin/test

```bash
git push origin master:test
```

### delete remote origin/test

```bash
git push origin :test
```

### download remote file

```bash
git fetch
```

### merge remote file

```bash
git merge origin/master
```

### download & merge remote file

```bash
git pull
```

### download & merge remote file don't generate commit

```bash
git pull --rebase
```

### copy other remote file

```bash
git clone https://github.com/Zhe-Lin/Git-Manual.git    #Download & place to the same directory
```

```bash
git clone https://github.com/Zhe-Lin/Git-Manual.git Test   #Download & place to Test directory
```

## Github Pages

### bulid remote web page

```bash
git push -u origin master:gh-pages
```

### delete remote web page

```bash
git push -u origin :gh-pages
```

## Git Patch

```bash
git log --oneline

e12d8ef (HEAD -> master) update test3
85e7e30 add test3
657fce7 update test2
abb4f43 add test2
cef6e40 update test
cc797cd add test
```

### make last 2 commit patch file

```bash
git format-patch 657fce7..e12d8ef     # = git format-patch -2
git format-patch -2 -o /tmp/patches   # Assign location to generate patch file
```

### use patch file

```bash
git am /tmp/patches/*
```

## Git Submodule

### add submodule to project

```bash
git submodule add https://github.com/Zhe-Lin/Git-Manual.git
```

### view submodule status

```bash
git submodule status
```

### update submodule

```bash
git submodule update                    # Update from local. If havn't local, update from remote
git submodule update --remote           # Update from remote
git submodule update --remote --merge   # Update from remote,and merge commit to master
                                        # = git submodule update --remote --rebase
```

### clone submodule

1. clone data
   - git clone https://github.com/Zhe-Lin/Git-Manual.git
2. init submodule
   - git submodule init
3. update submodule
   - git submodule update --recursive

```bash
git submodule update --init --recursive   # Run step2 ~ step3
```

```bash
git clone --recurse-submodules https://github.com/Zhe-Lin/Git-Manual.git    # Run step1 ~ step3
```

### delete submodule

1. delete .git/config setting
   - git submodule deinit test
2. delete .gitmodules
   - delete [submodule "test"] data
3. untrack file
   - git rm --cached test
4. delete .git/modules/test
   - rm -rf .git/modules/test
5. delete test
   - rm -rf test
6. add & commit
   - git add --all
   - git commit -m "-- test" -m "remove test submodule"

### renew submodule url

```bash
git submodule sync            # Synchronizes all submodules
git submodule sync -- test    # Synchronizes submodule only test
```
