# Setting Up Git, GitHub, and SSH

Resources
- [HowToForge | Installing and using Git and GitHub on Ubuntu Linux](https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu/) 
- [TOP | Setting up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git#introduction) 

Content
+ [Install Git](#install-git)
  + [Installing on Windows](#installing-on-windows)
  + [Installing on Linux](#installing-on-linux)
+ [Configure GitHub](#configure-github)
+ [Basic Git Workflow Example](#basic-git-workflow-example)
  + [Creating a local repository](#creating-a-local-repository)
  + [Staging Files in the Git Index](#staging-files-in-the-git-index)
  + [Committing changes made to the index](#committing-changes-made-to-the-index)
+ [Creating a repository on GitHub](#creating-a-repository-on-github)
+ [Pushing files from a local repository to a GitHub repository](#pushing-files-from-a-local-repository-to-a-github-repository)
+ [Creating an SSH Key](#creating-an-ssh-key)


## Install Git

### Installing on Windows

- Install [Git for Windows](https://gitforwindows.org/), which provides Git Bash (terminal emulator for running Git commands)
- Or, install using Windows Powershell
```bash
winget install --id Git.Git -e --source winget
```
- You can also install Linux for Windows via [WSL (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
  - Once setup, Git can be installed using the Linux package manager

### Installing on Linux
https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
- Install Git
  ```bash
  sudo apt install git
  ```

## Configure GitHub
- Configure GitHub, replacing `"Your name"` and `"your.email@example.com"` with your info (including the quotes) to link your local Git profile with GitHub

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

## Basic Git Workflow Example
### Creating a local repository
- Create a local repository `myTest` and change the current working directory to `myTest`:
  
  ```bash
  mkdir myTest && cd myTest
  ```

- Initialize a `.git` subdirectory in the current working directory
  - Contains a hidden `.git` folder with subdirectories for objects, refs, and template files
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
- Create a `sample.c` file:

  ```c
  #include<stdio.h>
  int main()
  {
      printf("hello world");
      return 0;
  }
  ```

### Staging Files in the Git Index

- Create and add files to the index. 

  ```bash
  git add README
  git add sample.c
  ```
### Committing changes made to the index
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
  - The first time running this command, you need to link the local `master` branch to the `master` branch on remote repository (`origin`)

```bash
git push -u origin master
# Can also use `git push --set-upstream origin master`

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
  - You may get a `permission denied` error when pushing to GitHub if SSH keys aren't set properly (See [Creating an SSH Key](#creating-an-ssh-key))

- Enable colorful output with git

  ```bash
  git config --global color.ui auto
  ```
---
## Creating an SSH Key
[Create an SSH key](https://www.theodinproject.com/lessons/foundations-setting-up-git#step-23-create-an-ssh-key)
 An SSH key is a cryptographically secure identifier. It’s like a really long password used to identify your machine, which can be used by GitHub without having to type in your username and password every time.


- [Check for Existing SSH Keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
  - Check for the presence of Ed25519 algorithm SSH keys
  - An error indicates you do not have an existing SSH key pair in the default location.
  ```bash
  ls ~/.ssh/id_ed25519.pub
  ```
- [Generate a New SSH Key on Your Local Machine and Add it to the SSH Agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
  - Run the following command in the terminal to create a new SSH key using your GitHub email as a label:
  ```bash
  ssh-keygen -t ed25519 -C "<youremail>"
  ```
  - When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location
  ```
  > Enter file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):[Press enter]
  ```
  ```
  > Generating public/private ed25519 key pair.
  ```
<br/>

- **Link SSH Key with GitHub**
  - Add the public key to your account on [GitHub.com](https://github.com/chxtio) to enable authentication for Git operations over SSH.
    - In GitHub, navigate to **Settings -> SSH and GPG keys -> New SSH Key**.
    - Name the key with a useful description of where it came from.
    - Copy the public SSH key from the terminal and paste it into the GitHub key section:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```
