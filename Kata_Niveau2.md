# Git Niveau 2 - Rapide Learning Meritis 
## 0. Considerations
* Asuming root directory \<root> for **Windows** as "*/c/demo*" and for **Linux** "*/tmp/demo*" 
## 1. Reminder
```
# show current git config
git config --list --show-origin

# create working directory + repository
git init <root>/WorkingDir

# add remote origin 
git remote add origin http://git.aquilest.fr/niveau2.git 

# creating a simple file1.txt
echo 'Hello world!' >file1.txt

# Add - track files/dir
git add file1.txt

# Commit - snapshot current working directory status
git commit -am "First commit"

# share your local repository status
git push --set-upstream origin master

# or just clone remote
git clone http://git.aquilest.fr/niveau2.git WorkingDirectory
```
Take a look of what's inside:
```
cd <root>/WorkingDir
ls .git/
# all objects are in /objects
find .git/objects -type f

git log --stat
git cat-file -p <commit_id>
```
## 2. Create Branch
```
# list branches
cd <root>/WoringDir
git branch

# create branch
git branch testing

# checkout branch
git checkout testing

# new branch + checkout
git checkout -b testing

```
Take a look of what's inside:
```
git log --oneline --decorate
```
## 3. BONUS: Detached Head
```
# modify file1
git checkout master
echo 'Hi world!' >file1.txt
git add file1.txt
git status

git commit -am "Second commit"

# checking working dir status
git status

# listing commits history
git log --oneline --decorate

# listing all commits graph
git log --graph --oneline --decorate --all

# modify again file1
echo 'Hi world!' >file1.txt
git add file1.txt
git status

# listing all commits graph
git log --graph --oneline --decorate --all

# pick a commit reference <commit> and <head>

# checkout a commit
git checkout <commit>

# detached Head Messaje! 

# modify again file1 on detached head, it works!
echo 'Hello world2!' >file1.txt
git commit -am "Experimental commit"

# fix1: remember head ref
git checkout <head>

# fix2: checkout branch
git checkout <branch>

# fix3: force checkout branch (override local changes)
git checkout --force <branch>

```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
```

## 4. Workflow - Branching
```
# create feature branch and checkout
git checkout -b feature/REF-1234_feature1

# check head
git log --graph --oneline --decorate --all

# add changes x 2
echo 'I love Git' >file2.txt
git add file2.txt
git commit -am "Fourth Commit"

# check head
git log --graph --oneline --decorate --all

# back to master
git checkout master

# back to master
git checkout master

# create feature branch 2
git checkout -b feature/REF-2345_feature2

# add changes
echo 'I dont love Git' >file3.txt
git add file3.txt
git commit -am "Sixth Commit"

```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
```
## 5. Workflow - Merging
```
# checkout branch to merge into - checkout master
git checkout master

# merge with feature1 (default fast-forward possible)
git merge feature/REF-1234_feature1

# merge with feature2 (merge commit)
git merge feature/REF-2345_feature2

# share status
git push 
```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
```

## 6. Merging - Conflicts
```
# create a new branch feature3
git checkout -b feature/REF-9876_feature3

# add changes in feature branch
git checkout feature/REF-9876_feature3
echo 'I dont love Git' >file3.txt
git commit -am "Conflict Commit"

# add a hot fix in master
git checkout master
echo 'I really really love Git \n Honnestly' >file3.txt
git commit -am "Conflict Commit master"

# merge with master
git checkout master
git merge feature/REF-9876_feature3

# resolve conflict and commit
git commit -am "Merge conflict"

```
Take a look of what's inside:
```
git log --graph --oneline --decorate --all
```