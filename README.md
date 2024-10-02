# Setting Up Git and GitHub on Ubuntu Linux

Tutorials: [HowToForge | Installing and using Git and GitHub on Ubuntu Linux](https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu/) | [TOP | Setting up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git#introduction) | Repo: [Training-Dummy/howtoforge_git_ubuntu](https://github.com/Training-Dummy/howtoforge_git_ubuntu)

## Contents
+ [Install Git](#install-git)
  + [Windows](#windows)
  + [Linux](#linux)
+ [Configure GitHub](#configure-github)
+ [Creating a local repository](#creating-a-local-repository)
+ [Adding repository files to an index](#adding-repository-files-to-an-index)
+ [Committing changes made to the index](#committing-changes-made-to-the-index)
+ [Creating a repository on GitHub](#creating-a-repository-on-github)
+ [Pushing files from a local repository to a GitHub repository](#pushing-files-from-a-local-repository-to-a-github-repository)


## Install Git

### Windows
- Install Git using [WSL (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
  - Once setup, Git can be installed using the Linux package manager
- Alternatively, install [Git for Windows](https://gitforwindows.org/), which provides Git Bash (terminal emulator for running Git commands)

### Linux
https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
- Install Git
  ```bash
  sudo apt install git
  ```

## Configure GitHub
- Configure GitHub:
  - Replace `"Your name"` and `"your.email@example.com"` with your personal details (including the quotes) to link your local Git profile with GitHub

  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

  - Verify configuration
  
  ```bash
  git config --get user.name
  git config --get user.email
  # List all settings
  git config --list
  ```

## Creating a local repository
- Create a local repository `myTest` and change the current working directory to `myTest`:
  
  ```bash
  mkdir myTest && cd myTest
  ```

- Create a (hidden) `.git` subdirectory in the current working directory
  - Contains subdirectories for objects, refs, and template files
  - A HEAD file is also created which will point to the currently checked out commit
  
  ```bash
  git init
  ```

  - If successful, you'll see a message like:

  ```
  Initialized empty Git repository in /home/user/Mytest/.git/
  ```

- Check the current state of the working directory and the staging area.
  - Shows which changes have been staged, which haven’t, and which files aren’t being tracked by Git.
  ```bash
  git status
  ```


- Create a README file to describe the repository:

  ```bash
  nano README.md
  # Add some text, example:
  This is a git repo
  # Save the file by pressing CTRL + O, then press Enter
  # Exit nano by pressing CTRL + X
  ```

## Adding repository files to an index

- Create and add files to the index. For example, create a `sample.c` file:

  ```c
  #include<stdio.h>
  int main()
  {
      printf("hello world");
      return 0;
  }
  ```

- Add the files to the index:

  ```bash
  git add README
  git add sample.c
  ```
## Committing changes made to the index
- Commit the changes with a message:

  ```bash
  git commit -m "Initial commit"
  ```
##  Creating a repository on GitHub
- Create a repository on GitHub with the same name as your local repository (e.g., "Mytest").
  - Then, connect your local repository to the GitHub repository (Replace `'user_name'` with your GitHub username):

  ```bash
  git remote add origin https://github.com/user_name/Mytest.git
  ```

## Pushing files from a local repository to a GitHub repository
- Push the local repository contents to GitHub
  - The first time running this command, you need the `--set-upstream` flag to link the local `master` branch to the `master` branch on remote repository (`origin`)

```bash
# Can also use `git push -u origin master`
git push --set-upstream origin master

# Note: Some repositories may use 'main' as the default branch instead of 'master'.
# In that case, use the following command:
# git push --set-upstream origin main
```

  - For subsequent pushes
  ```bash
git push origin master

# Or if your default branch is 'main':
# git push origin main
  ```
  - You may get a `permission denied` error when pushing to GitHub if SSH keys aren't set properly (See [[SSH]])

- Enable colorful output with git

  ```bash
  git config --global color.ui auto
  ```
