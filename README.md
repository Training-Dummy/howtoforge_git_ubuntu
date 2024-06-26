# Setting Up Git and GitHub on Ubuntu Linux
https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu/

- Install Git 
  ```bash
  sudo apt install git
  ```
- Configure GitHub:
  - Replace `"user_name"` with your GitHub username and `"email_id"` with the email you used to create your GitHub account.

  ```bash
  git config --global user.name "user_name"
  git config --global user.email "email_id"
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


## 4. Creating a README File

- Create a README file to describe the repository:

  ```bash
  nano README.md
  # Add some text, example:
  This is a git repo
  ```

## 5. Adding Files to the Index

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
  - - Enter your GitHub login credentials when prompted.

  ```bash
  git push origin master
  ```



