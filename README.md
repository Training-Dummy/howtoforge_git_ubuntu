# Setting Up Git and GitHub on Ubuntu Linux
Tutorials: [HowToForge | Installing and using Git and GitHub on Ubuntu Linux](https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu/) | [TOP | Setting up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git#introduction) 

- Install Git
  ```bash
  sudo apt install git
  ```
- Configure GitHub:
  - Replace `"Your name"` and `"your.email@example.com"` with your personal details (including the quotes) to link your local Git profile with GitHub

  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  # Verify
  git config --get user.name
  git config --get user.email
  # List all settings
  git config --list
  ```
- Create a local repository `myTest` and change the current working directory to `myTest`:
  - This will create a local folder `Mytest` and a hidden subdirectory named `.git`
  ```bash
  mkdir myTest && cd myTest
  ```

  - Create hidden `.git` subdirectory in the current working directory
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
  ```

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

- Commit the changes with a message:

  ```bash
  git commit -m "Initial commit"
  ```

- Create a repository on GitHub with the same name as your local repository (e.g., "Mytest").
  - Then, connect your local repository to the GitHub repository (Replace `'user_name'` with your GitHub username):

  ```bash
  git remote add origin https://github.com/user_name/Mytest.git
  ```

- Push the local repository contents to GitHub
  - The first time running this command, you need the `--set-upstream` flag to link the local `master` branch to the `master` branch on remote repository (`origin`)
  - You may get a 'permission denied' error when pushing to GitHub if SSH keys aren't set properly (See [Creating an SSH Key](#creating-an-ssh-key))

  ```bash
  # For first push (Can also use `git push -u origin master`)
  git push --set-upstream origin master
  # For subsequent pushes
  git push origin master
  ```

- Enable colorful output with git

  ```bash
  git config --global color.ui auto
  ```

## Creating an SSH Key
An SSH key is a cryptographically secure identifier. It’s like a really long password used to identify your machine. GitHub uses SSH keys to allow you to upload to your repository without having to type in your username and password every time. [Create an SSH key](https://www.theodinproject.com/lessons/foundations-setting-up-git#step-23-create-an-ssh-key)

- **Check for Existing SSH Keys**
  [Checking for Existing SSH Keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
  - Check for the presence of Ed25519 algorithm SSH keys:

  ```bash
  ls ~/.ssh/id_ed25519.pub
  ```
  - An error indicates you do not have an existing SSH key pair in the default location.

- **Generate a New SSH Key on Your Local Machine**
  [Generating a New SSH Key and Adding it to the SSH Agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
  - Run the following command in the terminal to create a new SSH key using your GitHub email as a label:
  ```bash
  ssh-keygen -t ed25519 -C "<youremail>"
  ```

  ```
  > Generating public/private ed25519 key pair.
  ```

- **Link SSH Key with GitHub**
  - Add the public key to your account on [GitHub.com](https://github.com/chxtio) to enable authentication for Git operations over SSH.
    - In GitHub, navigate to **Settings -> SSH and GPG keys -> New SSH Key**.
    - Name the key with a useful description of where it came from.
    - Copy the public SSH key from the terminal and paste it into the GitHub key section:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```