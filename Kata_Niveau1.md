# Git Niveau 1 - Rapide Learning Meritis 
## 0. Considerations
* Asuming root directory \<root> for **Windows** as "*/c/demo*" and for **Linux** "*/tmp/demo*" 
## 1. Config - First time Git setup
```
# Check git installation
$ git -v
git version 2.39.2.windows.1
```
```
# show current git config
$ git config --list --show-origin
```
```
# set user name
git config --global user.name "name lastname"
```
```
# set email
git config --global user.email name.lastname@meritis.fr
```

## 2. Init - Creating local repo
### **Client 1**
```
# init git working directory
mkdir <root>/Client1
git init <root>/Client1
```
Take a look of what's inside:
```
cd <root>/Client1
cd .git
ls -l
```
## 3. Commit - Add files 
### **Client 1**
```
# creating a simple file1.txt
echo 'Hello world!' >file1.txt

# Status - checking working dir status
git status

# Add - track files/dir
git add file1.txt

# checking working dir status
git status

# Commit - snapshot current working directory status
git commit -m "this is my first commit"

# checking working dir status
git status
```

Take a look of what's inside:
```
cd <root>/Client1
cd .git
ls -l
```
## 4. Init - Add remote
### **Client 2**
```
# init Client 2 git working directory
mkdir <root>/Client2
cd <root>/Client2
git init .

# Remote - set origin Client1
git remote add origin <root>/Client1
```
Take a look of what's inside:
```
cd <root>/Client2
cd .git
cat config
```
## 5. Pull - Fetch others changes
### **Client 2**
```
cd <root>/Client2

# Pull - fetch remote status (current branch)
git pull

# check 
ls -l


touch file2.txt
nano file2.txt
nano file1.txt

git status
git add file2.txt

cd <NewWorkingDirectoyPath>
git pull

```
Take a look of what's inside:
```
cd <root>/Client2
ls -l
cd .git
cat config
```

## 6. Push - Share your changes
### **Client 2**
```
# making some changes
echo 'Hello Hello world!' >file1.txt
echo 'Shakira' >file1_final.txt

# as you already know...
git status
git add file1_final.txt
git commit -m "Hips dont lie"

# Push  - pushing your curent snapshop
git push 
Error! --> It's not a bare Repository

# Branch - create a fork from current status
git branch otherBranch
git checkout otherBranch

# Push  - pushing your curent snapshop
git push 
Bingo!

```
Take a look of what's inside:
```
cd <root>/Client1
cd .git
git checkout master
```
## 7. Init - Remote/Bare Repository
### **Remote**
```
mkdir <root>/remote.git
cd <root>/remote.git

# Init repo without working directory (no direct commit possible)
git init --bare

# Or just...
git init --bare <root>/remote.git

```

### **Client 1**
```
cd <root>/Client1
git remote add <root>/remote.git

git push
Bingo! no need to switch branch

```
Take a look of what's inside:
```
cd <root>/remote.git
cd .git
cat config
```
## 8. Move your bare to a remote server
Many posibilities:
* Share folder (Drive, Dropbox...)
* Remote folder, using ssh
* Web server
* ...
### **Client 1**
```
# Remote (a real one!) server
git remote add origin http://git.aquilest.fr/remote.git
Error! --> Origin exist already

git remote set-url origin http://git.aquilest.fr/remote.git 

#Sharig all history!
git push

# The authentification was disable in the server. In order to facilitate the exercise. 
```

## 9. Clone - Turnkey solution
### **Client 3**
```
cd <root>

#Clone - clonning remote repo in working directory Client 3
git clone http://git.aquilest.fr/remote.git Client3


```
Take a look of what's inside:
```
cd <root>/Client3
cd .git
cat config
```
