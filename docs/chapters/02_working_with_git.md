## Basic Git Commands and Workflow

### Initializing a Repository
To start using Git, you need to initialize a repository in your project directory. This creates a `.git` directory that tracks all changes.

```bash
git init
```

### Checking the Status of Your Repository
Use `git status` to see the state of your working directory and staging area. It shows which changes have been staged, which haven't, and which files aren't being tracked by Git.

```bash
git status
```

### Adding Files to the Staging Area
Before committing changes, you need to add them to the staging area using `git add`. This prepares the files to be included in the next commit.

```bash
git add <filename>
```

To add all changes in the directory:

```bash
git add .
```

### Committing Changes
After staging the files, commit them to the repository with a message describing the changes.

```bash
git commit -m "Your commit message"
```

### Git Workflow
![git_life_cycle](https://git-scm.com/book/en/v2/images/lifecycle.png)

The image above illustrates the Git workflow[@git_book2014]. It starts with modifying files in your working directory. Once changes are made, you add them to the staging area using `git add`. After staging, you commit the changes to the repository with `git commit`. This cycle repeats as you work on your project.

### Pushing Changes to a Remote Repository
To share your changes with others, push them to a remote repository like GitHub.

```bash
git push origin main
```

!!! example "Creating a New Repository"

    Create a new Git repository in a new directory and add a file to it. Stage and commit the changes.

    ??? success "Solution"

        - Create a new directory and navigate to it:
        ```bash
        mkdir myproject
        cd myproject
        ```

        - Initialize a Git repository:
        ```bash
        git init
        ```

        - Add a new file and commit it:
        ```bash
        echo "Hello, Git!" > hello.txt
        git add hello.txt
        git commit -m "Add hello.txt"
        ```

!!! Note
    Keep in mind that Git local repository is a hidden directory `.git` in the root of your project directory. It contains all the necessary metadata for version control. If you delete this directory, you will lose your project history as well. To serve as a backup, you can push your changes to a remote repository.

!!! example "Create repository on GitHub"

    Create a new repository on GitHub and connect it to your local repository. Push your changes to the remote repository.

    ??? success "Solution"

        - Create a new repository on GitHub. Do not initialize it with a README, .gitignore, or license.

        - Connect your local repository to the remote repository:
        ```bash
        # substitute your username and repository name
        git remote add origin https://github.com/yourusername/your-repository.git 
        ```

        - Push your changes to the remote repository:
        ```bash
        git push -u origin main
        ```

## Branching and Merging

### Working with Branches
Branches are an essential part of Git, allowing you to work on different features or fixes independently. This helps in maintaining a clean and organized project history.

### Creating a Branch
To create a new branch, use the git branch command followed by the branch name:

```bash
git branch <branch-name>
```

Switch to the new branch using git checkout:

```bash
git checkout <branch-name>
```

Or, you can create and switch to a new branch in one command:

```bash
git checkout -b <branch-name>
```

### Why Use Branches?
 * **Isolation**: Keep different lines of development separate.
 * **Collaboration**: Multiple team members can work on different features simultaneously.
 * **Experimentation**: Safely try out new ideas without affecting the main codebase.
 * **History**: Each branch maintains its own history of commits, making it easy to track changes and revert if necessary.
 * **Merging**: Once the work on a branch is complete, it can be merged back into the main branch, integrating the changes.

### Merging a Branch
First, switch to the branch you want to merge into:

```bash
git checkout main
```

Then, merge the feature branch:

```bash
git merge <branch-name>
```

### Best Practices for Merging
 * Regularly Sync with Main: Frequently merge changes from the main branch into your feature branch to minimize conflicts.
 * Use Pull Requests: For collaborative projects, use pull requests to review and discuss changes before merging.
 * Resolve Conflicts Carefully: If conflicts arise, carefully resolve them to ensure the codebase remains stable.

### Handling Merge Conflicts
Merge conflicts occur when changes in different branches conflict with each other. Git will mark the conflicts in the affected files, and you will need to resolve them manually.

### Steps to Resolve Conflicts

&emsp;1. Identify Conflicts: Git will highlight the conflicting areas in the files.  
&emsp;2. Edit Files: Manually edit the files to resolve conflicts.  
&emsp;3. Stage Resolved Files: Once resolved, stage the files using git add.  
&emsp;4. Complete the Merge: Commit the merge to complete the process.

```bash
git add <resolved-file> git commit
```

By following these practices, you can effectively manage branches and merges in your Git workflow, ensuring a smooth and efficient development process.

!!! example "Creating and Merging Branches"

    Create a new branch, make changes, and merge it back into the main branch.

    ??? success "Solution"

        - Create a new branch and switch to it:
        ```bash
        git checkout -b feature-branch
        ```

        - Make changes to your files and commit them:
        ```bash
        git add .
        git commit -m "Add new feature"
        ```

        - Switch back to the main branch and merge the feature branch:
        ```bash
        git checkout main
        git merge feature-branch
        ```

!!! example "Resolving Merge Conflicts"

    Using VS Code, clone the [playgound](https://github.com/ELIXIREstonia/2024-11-06-git-playground) repository and follow instructions to create a merge conflict and resolve it.

    ??? success "Solution"

        ```bash
        git clone git@github.com:ELIXIREstonia/2024-11-06-git-playground.git
        git checkout ugly-conflict # this is needed to fetch the branch from origin
        # make changes to the README.md file if you feel like it
        git add README.md
        git commit -m "Change README.md"
        git checkout main
        git merge ugly-conflict
        # resolve the conflict in the README.md file (VS Code will help you)
        git add <resolved-file>
        git commit
        ```

## Navigating Git History

### Exploring Git Logs and History
Understanding the history of your project is crucial for tracking changes, debugging issues, and collaborating with others. Git provides several commands to help you navigate and manage your project's history.

### Viewing Commit History
The `git log` command displays the commit history of your repository.

```bash
git log 
```

This command shows a list of commits, including the commit hash, author, date, and commit message. You can use various options to customize the output:

 * `--oneline`: Show each commit on a single line.
 * `--graph`: Display a graphical representation of the commit history.
 * `--decorate`: Show branch and tag names alongside commit messages.

```bash
git log --oneline --graph --decorate 
```

### Reverting Changes
If you need to undo changes, Git provides several options:

### Reverting a Commit
The `git revert` command creates a new commit that undoes the changes from a previous commit.

```bash
git revert <commit-hash> 
```

### Resetting to a Previous Commit
The git reset command moves the current branch to a specified commit. This can be used to undo commits or unstage changes.

 * `--soft`: Keep changes in the working directory and staging area.
 * `--mixed`: Keep changes in the working directory but unstage them.
 * `--hard`: Discard all changes and reset the working directory to the specified commit.

```bash
git reset --hard <commit-hash> 
```

!!! Note
    Be cautious when using `git reset --hard`, as it permanently removes changes and cannot be undone. Almost always a better option is to use `git revert`, especially if changes have been pushed to a (collaborative) remote repository.

## Collaborating with Remote Repositories

### Collaboration and Remote Workflows
Collaborating with others on a project often involves using remote repositories. These repositories, hosted on platforms like GitHub, GitLab, or Bitbucket, allow multiple contributors to work on the same codebase.

### Setting Up a Remote Repository
To start collaborating, you need to set up a remote repository and connect your local repository to it.

### Adding a Remote Repository
Use the `git remote add` command to add a remote repository. Replace <remote-url> with the URL of your remote repository.

```bash
git remote add origin <remote-url>
```

### Verifying Remote Repositories
To verify that the remote repository has been added, use the `git remote -v` command.

```bash
git remote -v
```

### Pushing Changes to a Remote Repository
After committing your changes locally, you can push them to the remote repository to share with others.

```bash
git push origin main
```

### Pulling Changes from a Remote Repository
To update your local repository with changes from the remote repository, use the `git pull` command.

```bash
git pull origin main
```

### Creating and Managing Pull Requests
Pull requests (PRs) are a way to propose changes to a repository. They allow team members to review and discuss changes before merging them into the **main** branch.

!!! Note
    You can clone all public repositories without authentication. However, to push changes to a repository, you need to authenticate with the remote platform. Also you can't push to a repository you don't have write access to (you are not part of the team -- collaborators). Most open source projects are such public repositories and you can  
    1. fork them to your own account and push changes to your fork.  
    2. then create a pull request to the original repository.

## Creating a Pull Request
 1. Push Your Branch: Push your feature branch to the remote repository. `git push origin <branch-name>`
 2. Open a Pull Request: On the remote repository platform (e.g., GitHub), navigate to the repository and open a new pull request from your feature branch to the main branch.

### Reviewing and Merging Pull Requests
Team members can review the pull request, leave comments, and suggest changes. Once the changes are approved, the pull request can be merged into the main branch.

### Best Practices for Teamwork
 * Branch Naming Conventions: Use clear and consistent naming conventions for branches (e.g., `feature/`, `bugfix/`, `hotfix/`).
 * Code Reviews: Conduct thorough code reviews to maintain code quality and share knowledge.
 * Frequent Commits: Commit changes frequently with **meaningful** commit messages.
 * Sync Regularly: Regularly pull changes from the remote repository to stay up-to-date with the latest codebase.
 * Resolve Conflicts Early: Address merge conflicts as soon as they arise to avoid larger issues later.


!!! example "Creating a pull request"

    Create a new branch, make changes, push the branch to the remote repository, and create a pull request.
    You can use the [playground](https://github.com/ELIXIREstonia/2024-11-06-git-playground) repository to practice.

## Handling Common Issues

### Tips for Managing Git Challenges
Handling merge conflicts, using .gitignore, and maintaining a clean Git history.

### Handling Merge Conflicts
Merge conflicts occur when changes in different branches conflict with each other. Git will mark the conflicts in the affected files, and you will need to resolve them manually.

### Steps to Resolve Conflicts

&emsp;1. Identify Conflicts: Git will highlight the conflicting areas in the files.  
&emsp;2. Edit Files: Manually edit the files to resolve conflicts.  
&emsp;3. Stage Resolved Files: Once resolved, stage the files using git add.  
&emsp;4. Complete the Merge: Commit the merge to complete the process.

```bash
git add <resolved-file>
git commit
```

### Using .gitignore
The .gitignore file specifies which files and directories to ignore in a project. This is useful for excluding temporary files, build artifacts, and other files that should not be tracked by Git.

### Creating a .gitignore File
Create a .gitignore file in the root of your repository and add patterns for files and directories to ignore.

```bash
# Example .gitignore file
*.log
*.tmp
node_modules/
dist/
```

### Maintaining a Clean Git History
A clean Git history makes it easier to understand the evolution of a project and track down issues. Here are some tips for maintaining a clean history:

 * **Frequent Commits**: Commit changes frequently with meaningful commit messages.
 * **Squash Commits**: Squash multiple related commits into a single commit before merging.

## Wrap-Up and Best Practices

Summary of key points, practical tips for effective use of Git, and a Q&A section for participants.

### Key Points
 * **Version Control**: Git is a powerful version control system that helps you track changes, collaborate with others, and manage your project's history.
 * **Basic Commands**: Familiarize yourself with basic Git commands like `git init`, `git add`, `git commit`, `git status`, `git push`, and `git pull`.
 * **Branching and Merging**: Use branches to work on different features or fixes independently, and merge them back into the main branch when ready.
 * **Collaboration**: Use remote repositories and pull requests to collaborate with others and review changes before merging.

### Practical Tips
 * **Commit**: Make commits with clear semantic messages.
 * **Use Branches**: Create branches for new features, bug fixes, and experiments.
 * **Sync Regularly**: Pull changes from the remote repository frequently to stay up-to-date.
 * **Resolve Conflicts Early**: Address merge conflicts as soon as they arise to avoid larger issues later.
 * **Review Code**: Conduct thorough code reviews to maintain code quality and share knowledge.

