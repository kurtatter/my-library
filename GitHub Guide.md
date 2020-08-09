## GitHub Guide



1. Регистрация на https://github.com/

2. ```bash
   sudo apt install git
   ```

3. Клонировать репозиторий 

   ```bash
   git clone https://github.com/g0v3r9m3n10/AtoTYC
   ```



Покажет состояни репозитория, например какого файла еще нет в репозитории

```bash
git status
```

И если есть файлы которые мы не добавили в репозиторий и хотим добавить

```bash
git add index.html
```

После команды выше файл находится в статусе готов отправиться в репозиторий, то есть он еще находится на нашем компьютере.

Чтобы отправить файл необходимо 

```bash
git commit -m "Add index page"
```

Он всё еще не отправлен и находиться на компьютере, теперь последняя команда которая закинет наш файл в репозиторий

```bash
git push
```

Новые файлы отправились в репозиторий. Для того чтобы другой компьютер обновил свой репозиторий и скачал эти новый файлы ему нужно 

```bash
git pull
```

Чтобы закинуть сразу все файлы, измененные и новые

```bash
git add -A
```

Ниже я приведу гит команды с [официальной](https://guides.github.com/introduction/git-handbook/?utm_source=onboarding-series&utm_medium=email&utm_content=week2&utm_campaign=beg) документации, просто на всякий случай. Там описаны комбинации команд на различные ситуации.

#### Example: Contribute to an existing repository

```bash
# download a repository on GitHub.com to our machine
git clone https://github.com/me/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch
```

#### Example: Start a new repository and publish it to GitHub

First, you will need to create a new repository on GitHub. You can learn how to create a new repository in our [Hello World guide](https://guides.github.com/activities/hello-world/#repository). **Do not** initialize the repository with a README, .gitignore or License. This empty repository will await your code.

```bash
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git

# push changes to github
git push --set-upstream origin master
```

#### Example: contribute to an existing branch on GitHub

```bash
# assumption: a project called `repo` already exists on the machine, and a new branch has been pushed to GitHub.com since the last time changes were made locally

# change into the `repo` directory
cd repo

# update all remote tracking branches, and the currently checked out branch
git pull

# change into the existing branch called `feature-a`
git checkout feature-a

# make changes, for example, edit `file1.md` using the text editor

# stage the changed file
git add file1.md

# take a snapshot of the staging area
git commit -m "edit file1"

# push changes to github
git push
```