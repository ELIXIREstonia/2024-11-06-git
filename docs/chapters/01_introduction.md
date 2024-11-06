Git is a powerful distributed version control system that allows multiple people to work on a project simultaneously without overwriting each other's changes. It keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members.

In this course, participants will learn:  
- The basics of Git and version control  
- How to set up and configure Git  
- How to create and manage repositories  
- Branching and merging strategies  
- Collaboration workflows using Git

## Core Concepts of Git

Git is a distributed version control system that allows each user to have their own local repository, which contains the full history of the project. This makes Git fast and flexible, as users can work offline and only need to connect to a remote repository when they want to share their changes.

### Version Control

Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. With Git, every time you save the state of your project (commit), Git takes a snapshot of all your files and stores a reference to that snapshot. If a file has not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored.

### Three States of Files

In Git, files can reside in one of three states[@git_book2014]:  
- **Working Directory**: The files that you see in your file system. These are the files that you are currently working on.  
- **Staging Area**: A file that has been marked to be included in the next commit. The staging area allows you to prepare a set of changes before committing them to the repository. This gives you more control over what changes are included in each commit.  
- **Repository (.git directory)**: The committed files that are safely stored in your local Git repository.

The workflow in Git typically involves moving files between these three states.  
&emsp;1. You modify files in your working directory.  
&emsp;2. You stage them to the staging area.  
&emsp;3. you then commit them to the repository.

!!! note "Note"
    Commiting should be part of your daily workflow when working on a project. It is a good practice to commit your changes whenever you reach a logical stopping point or complete a task. 

### Key Concepts:
- **Repository**: A directory which contains your project work, as well as a few files (hidden by default) which are used by Git to keep track of changes.
- **Commit**: A snapshot of your repository at a specific point in time.
- **Branch**: A parallel version of your repository. It is contained within your repository but does not affect the primary or main branch.
- **Merge**: The process of combining changes from different branches.
- **Clone**: A copy of a repository that lives on your computer instead of on a website's server somewhere.
- **Push**: Sending your committed changes to a remote repository, such as a repository hosted on GitHub.
- **Pull**: Fetching changes from a remote repository and merging them into your local repository.

## Working with Repositories

A Git repository can be local (on your computer) or remote (on a server). You can create a new repository from scratch, or you can clone an existing repository to get a copy of it on your local machine.

### Creating a Repository:
To create a new local repository, navigate to your project directory and run:
```bash
git init
```
This command creates a new subdirectory named `.git` that contains all of your necessary repository files.

### Cloning a Repository:
To clone a remote repository, use the `git clone` command followed by the repository URL:
```bash
git clone https://github.com/user/repo.git
```
This command creates a directory named `repo`, initializes a `.git` directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version.

### Managing Repositories:
You can add files to your repository using the `git add` command, commit changes with `git commit`, and push your changes to a remote repository with `git push`.

### Example Workflow:
1. **Create a new repository**:
    ```bash
    mkdir myproject
    cd myproject
    git init
    ```

2. **Add a new file and commit it**:
    ```bash
    echo "Hello, Git!" > hello.txt
    git add hello.txt
    git commit -m "Add hello.txt"
    ```

3. **Connect to a remote repository**:
    ```bash
    git remote add origin https://github.com/user/myproject.git
    git push -u origin main
    ```

4. **Make changes and push them**:
    ```bash
    echo "Some changes" >> hello.txt
    git add hello.txt
    git commit -m "Update hello.txt"
    git push
    ```

By understanding these core concepts and commands, you'll be well on your way to mastering Git and improving your workflow.

## First-Time Git Setup

Before you start using Git, you need to configure some settings. These settings are stored in your Git configuration file and include your name and email address, which will be associated with your commits.

### Required Git Config Commands

To set up Git for the first time, you need to configure your username and email. Open your terminal and run the following commands:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

These commands set your name and email address for all Git repositories on your system.

### Checking Existing Configurations

To check your current Git configuration, use the following command:

```bash
git config --list
```

This command will display a list of all the Git configurations that are currently set.

### Defining Required Configurations

If you need to change any configuration, you can use the `git config` command again with the appropriate options. For example, to change your email address, you can run:

```bash
git config --global user.email "new.email@example.com"
```

### Using VS Code for Git

During the lessons, we will be working with Visual Studio Code (VS Code). VS Code has built-in support for Git, making it easier to manage your repositories. To configure Git in VS Code, follow these steps:

1. Open VS Code.
2. Go to the Command Palette by pressing `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac).
3. Type `Git: Configure User Name` and press Enter. Enter your name when prompted.
4. Type `Git: Configure User Email` and press Enter. Enter your email address when prompted.

By setting up these configurations, you'll be ready to start using Git effectively in your projects.

Also see using git in VS Code[@vscode2024sourcecontrol].