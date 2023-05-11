# Git Niveau 3 - Rapide Learning Meritis 
## 0. Considerations
* Asuming root directory \<root> for **Windows** as "*/c/demo*" and for **Linux** "*/tmp/demo*" 
## 1. Reminder
```
# checkout an existing branch
git checkout feature/REF-1234_feature1

# create feature branch and checkout
git checkout -b feature/REF-1234_feature1

# merge with feature1 (default fast-forward possible)
git merge feature/REF-1234_feature1

# merge with feature2 (merge commit)
git merge feature/REF-2345_feature2

# visualize command
git log --graph --oneline --decorate --all
```
## 2. With Merge
```
# clone remote virgin repository
git clone https://github.com/torresaa/git_kata3.git WithMerge

# switch to master
git checkout master

# merge hotfix (fast forward)
git merge hotfix/missing_real_name

# update develop with master
git checkout develop
git merge master

# Sync unit test feature with develop
git checkout feature/REF-004_UnitTests
git merge develop

# update failing test (update file src/test/java/com/git/kata/KataApplicationTests.java)
git commit -am "Updating test"

# merge feature2 with develop
git checkout feature/REF-002_adding_nice_html_page
git merge develop
# good practice!: resolve conflicts in local branch before merging
git commit -am "resolve git conflicts"

# merge develop with feature2 (equivalent to Merge request)
git checkout develop
git merge feature/REF-002_adding_nice_html_page
# fest-forward merge commit, as conflicts already resolved

# Sync unit test feature with develop
git checkout feature/REF-004_UnitTests
git merge develop
# update failing test (update file src/test/java/com/git/kata/KataApplicationTests.java)
git commit -am "Updating test"

# merge unit test with develop (equivalent to merge request)
git checkout develop
git merge feature/REF-004_UnitTests

# release
git checkout master
git merge develop
git tag v1.0

```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
gitk --all
```
## 3. With Rebase and squash
```
# clone remote virgin repository
git clone https://github.com/torresaa/git_kata3.git WithRebase

# squash hot fix (keep just one commit)
git checkout hotfix/missing_real_name
git rebase -i <origin commit ref>
# and follow the interactive mode

# merge hotfix (fast forward)
git checkout master
git merge hotfix/missing_real_name

# update develop with master
git checkout develop
git merge master

# Sync unit test feature with develop
git checkout feature/REF-004_UnitTests
# --check log before
git rebase develop
# --check log after

# update failing test (update file src/test/java/com/git/kata/KataApplicationTests.java)
git commit -am "Updating test"

# merge feature2 with develop
git checkout feature/REF-002_adding_nice_html_page
git rebase develop
# good practice!: resolve conflicts in local branch before merging
git commit -am "resolve git conflicts"
git rebase --continue

# squash feature2
git rebase -i <origin commit ref>
# --follow interactive instructions

# merge develop with feature2 (equivalent to Merge request)
git checkout develop
git merge feature/REF-002_adding_nice_html_page
# fast-forward merge commit, as conflicts already resolved

# Sync unit test feature with develop
git checkout feature/REF-004_UnitTests
git rebase develop
# update failing test (update file src/test/java/com/git/kata/KataApplicationTests.java)
git commit -am "Updating test"

# squash is not mandatory in rebase. It's a good practice. 

# merge unit test with develop (equivalent to merge request)
git checkout develop
git merge feature/REF-004_UnitTests

# Selective release
git checkout master
git cherry-pick <a commit ref>
git tag v0.9
git merge develop
# --the commit is identified
git tag v1.0

```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
gitk --all
```