 ## Git

```bash
apt-get install git
git --version
```

#### [GUI Clients Link](https://git-scm.com/downloads/guis)

#### [Download gitkraken for windows](https://www.gitkraken.com/download/windows64)


```bash
mkdir test-project

cd test-project

git init

```
### Add 3 files into ./git folder
### [opensource lincense](https://opensource.org/licenses)
### [Choose a license](https://choosealicense.com/)
### [Gitignore](https://github.com/github/gitignore)
```bash
cd .git/

touch .gitignore
touch README.md
touch LICENSE
```
```
git add .

git commit -m "initial commit"

git status

git log
```
```
git diff HEAD

git add .

git status
```
```
git restore --staged.
```
```
git commit -m "update readme"
```
```
git reset HEAD~1
git diff HEAD
```
### Contect local to github and push projects
### Add id_rsa.pub to your github account
```
git remote set-url origin git@github.com:{arazmoazzemi}/{DevOps-Days}.git

git log
git remote show

git pull -v
git pull

git push

```

### Remove commits 
```
git reset HEAD~1 --hard

```
```
git fetch
```

```bash
git revert <commit ID>

git checkout HEAD~1

ls

```

```bash
git checkout main

ls
```

### Create a new branch

```bash
git checkout <commit ID> -b mybranch

git branch
```



