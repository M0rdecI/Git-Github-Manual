# THIS IS GIT !!!

Well, afetr some time, I figured I'd come around and have a handy "manual" for all this version control thing that most of us IT professionals talk about.
So here's a basic markdown of what you need to get started with git and github. (PS> Got to hand it to the vrious AI tools out there that aided in my research. Though the whole manual compilation process and evaluation based on my own personal experience was quite the workload). Anyway, enjoy :).

# Git Commands Summary (you're welcome by the way)
## `git config`
The `git config` command is used to set configuration options for Git. These options can control everything from your user information to how Git interacts with remote repositories. There are three levels of configuration:

1. **System-wide configuration**: Applies to all users on the system and all their repositories. The configuration file is usually located at `/etc/gitconfig`.
2. **Global configuration**: Applies to a single user and all their repositories. The configuration file is located at `~/.gitconfig` or `~/.config/git/config`.
3. **Local configuration**: Applies to a specific repository. The configuration file is located at `.git/config` within the repository.

Here are some common uses of the `git config` command:

### Setting Your Identity
```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "you@example.com"
```

### Viewing Configuration
```bash
# View all settings
git config --list

# View a specific setting
git config user.name
```

### Editing Configuration
```bash
# Edit the global configuration file in your default text editor
git config --global --edit

# Edit the local configuration file in your default text editor
git config --local --edit
```

### Configuring Aliases
```bash
# Create a shortcut for a git command
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

### Changing the Default Text Editor
```bash
# Set nano as the default editor
git config --global core.editor "nano"

# Set Visual Studio Code as the default editor
git config --global core.editor "code --wait"
```

### Configuring Line Endings
```bash
# Configure automatic line ending conversion for Windows
git config --global core.autocrlf true

# Configure automatic line ending conversion for Unix/Linux/OSX
git config --global core.autocrlf input

# Disable automatic line ending conversion
git config --global core.autocrlf false
```

### Working with Remotes
```bash
# Set the URL for a remote repository
git config remote.origin.url https://github.com/user/repo.git

# Set the push behavior for a remote
git config remote.origin.push refs/heads/master:refs/heads/master
```

### Configuring Merge and Diff Tools
```bash
# Set the merge tool
git config --global merge.tool vimdiff

# Set the diff tool
git config --global diff.tool vimdiff
```

These are just a few examples. The `git config` command has many options to customize your Git environment according to your needs. For more detailed information, you can refer to the [official Git documentation](https://git-scm.com/docs/git-config).
## `git init`
The `git init` command is used to create a new Git repository. This command sets up the necessary files and directories that Git needs to manage and track changes in a project. Here’s a detailed explanation of how to use `git init` and what it does:

### Basic Usage
To initialize a new Git repository, navigate to your project directory and run the following command:

```bash
cd /path/to/your/project
git init
```

This will create a new subdirectory named `.git` in your project directory. This `.git` directory contains all the information and metadata that Git uses to manage the repository, including configuration settings, commit history, and pointers to branches and tags.

### What Happens When You Run `git init`?
1. **.git Directory**: A new subdirectory named `.git` is created in your project directory. This directory contains all the Git-related data, including:
   - `HEAD`: A reference to the current branch.
   - `config`: Repository-specific configuration file.
   - `description`: A description of the repository.
   - `hooks/`: Directory for client-side hook scripts.
   - `info/`: Directory for miscellaneous information.
   - `objects/`: Directory for all the content objects (blobs, trees, commits).
   - `refs/`: Directory for all the branch and tag references.

2. **Initial Configuration**: Some initial configuration settings are established. For example, Git sets the default branch name to `master` (or `main`, depending on your Git version and configuration).

### Initializing a Bare Repository
A bare repository is a repository that does not contain a working directory. It is typically used as a remote repository that developers push to and pull from. To create a bare repository, use the `--bare` option:

```bash
git init --bare /path/to/repository.git
```

A bare repository does not have a working directory, so it is not intended for active development. Instead, it is used as a central repository that developers can clone and push changes to.

### Examples
#### Initialize a Git Repository in an Existing Directory
If you have an existing project and want to start tracking it with Git, navigate to the project directory and initialize the repository:

```bash
cd my-project
git init
```

#### Initialize a Bare Git Repository
To create a bare repository, use the `--bare` option:

```bash
mkdir my-repo.git
cd my-repo.git
git init --bare
```

### Post Initialization Steps
After initializing a Git repository, you usually want to add files and make an initial commit:

1. **Add Files**: Add files to the staging area using `git add`:

```bash
git add .
```

2. **Commit Changes**: Commit the added files to the repository:

```bash
git commit -m "Initial commit"
```

### Checking the Repository Status
After initialization, you can check the status of your repository using:

```bash
git status
```

### Summary
- `git init` initializes a new Git repository by creating a `.git` directory that contains all the necessary Git files and metadata.
- You can use `git init --bare` to create a repository without a working directory, typically for use as a remote repository.
- After initializing the repository, you can add files, commit changes, and start tracking your project with Git.

## `git add`
The `git add` command is used to add changes in the working directory to the staging area. This command is a key part of the process of preparing changes to be committed to the repository. Here’s a detailed explanation of how to use `git add` and what it does:

### Basic Usage
To add a file or files to the staging area, you use `git add` followed by the file name or a pattern that matches multiple files.

#### Adding a Single File
To add a specific file to the staging area:

```bash
git add filename
```

#### Adding Multiple Files
To add multiple files, you can list each file name:

```bash
git add file1 file2 file3
```

#### Adding All Changes
To add all changes in the current directory and its subdirectories:

```bash
git add .
```

This will stage all new, modified, and deleted files.

#### Adding Changes Interactively
You can add changes interactively, which allows you to review each change before staging it:

```bash
git add -i
```

#### Adding All Tracked Files
To add all changes to tracked files (excluding untracked files):

```bash
git add -u
```

### Common Scenarios

#### Adding a New File
If you have created a new file and want to add it to the staging area:

```bash
touch newfile.txt
git add newfile.txt
```

#### Adding Changes to an Existing File
If you have made changes to an existing file and want to add those changes:

```bash
echo "Some changes" >> existingfile.txt
git add existingfile.txt
```

#### Adding All Changes Including Deletions
If you want to stage all changes, including deletions:

```bash
git add -A
```

### Understanding the Staging Area
The staging area (or index) is a place where Git keeps track of changes that are going to be included in the next commit. When you run `git add`, the specified changes are added to the staging area. These changes can be reviewed and modified before they are committed to the repository.

### Example Workflow
Here is a typical workflow involving `git add`:

1. **Make Changes**: Modify, create, or delete files in your working directory.
2. **Check Status**: See which files have been changed using `git status`.

```bash
git status
```

3. **Add Changes**: Add the desired changes to the staging area.

```bash
git add .
```

4. **Commit Changes**: Commit the changes in the staging area to the repository.

```bash
git commit -m "Describe your changes"
```

### Summary
- `git add` is used to add changes to the staging area, preparing them to be included in the next commit.
- You can add individual files, multiple files, or all changes in the working directory.
- Use `git add -A` to add all changes, including deletions, or `git add -u` to add changes to tracked files only.
- After staging changes with `git add`, you can commit them to the repository with `git commit`.
## `git rm`
The `git rm` command is used to remove files from both the working directory and the staging area (index). This is useful when you want to delete files from your repository. Here’s a detailed explanation of how to use `git rm` and what it does:

### Basic Usage
To remove a file from the working directory and the staging area, you use `git rm` followed by the file name.

#### Removing a Single File
To remove a specific file:

```bash
git rm filename
```

This command removes the file from the working directory and stages the removal for the next commit.

#### Removing Multiple Files
To remove multiple files, you can list each file name:

```bash
git rm file1 file2 file3
```

#### Removing Files Recursively
To remove files in a directory and its subdirectories:

```bash
git rm -r directoryname
```

### Keeping the File in the Working Directory
If you want to remove the file from the repository but keep it in your working directory, you can use the `--cached` option:

```bash
git rm --cached filename
```

This stages the file for removal from the repository, but the file itself remains in your working directory.

### Common Scenarios

#### Removing a Tracked File
If you have a file that is currently tracked by Git and you want to remove it:

```bash
git rm unwantedfile.txt
git commit -m "Remove unwantedfile.txt"
```

#### Removing a File but Keeping It Locally
If you want to remove a file from the repository but keep it on your local disk:

```bash
git rm --cached localfile.txt
git commit -m "Remove localfile.txt from repository"
```

#### Removing a Directory
If you want to remove an entire directory and its contents:

```bash
git rm -r directoryname
git commit -m "Remove directoryname"
```

### Using Wildcards
You can use wildcards to remove multiple files that match a pattern:

```bash
git rm '*.log'
```

This will remove all `.log` files from the working directory and stage them for removal.

### Example Workflow
Here is a typical workflow involving `git rm`:

1. **Check Status**: See which files are currently tracked and which are staged for removal.

```bash
git status
```

2. **Remove Files**: Remove the desired files using `git rm`.

```bash
git rm filename
```

3. **Commit Changes**: Commit the removal to the repository.

```bash
git commit -m "Remove filename"
```

### Summary
- `git rm` removes files from both the working directory and the staging area.
- Use `git rm --cached` to remove a file from the repository while keeping it in the working directory.
- Use `git rm -r` to remove directories and their contents.
- Wildcards can be used to remove multiple files that match a pattern.
- After removing files with `git rm`, commit the changes to update the repository.

## `git log`
The `git log` command is used to view the commit history of a repository. It shows a list of commits made to the repository in reverse chronological order (most recent commits first). Here’s a detailed explanation of how to use `git log` and some of its options:

### Basic Usage
To view the commit history, simply run:

```bash
git log
```

This command will display the commit history with details such as the commit hash, author, date, and commit message.

### Common Options

#### Pretty Formats
You can customize the output format using the `--pretty` option:

- **oneline**: Show each commit on a single line.

  ```bash
  git log --pretty=oneline
  ```

- **short**: Show a summary of each commit.

  ```bash
  git log --pretty=short
  ```

- **full**: Show the full commit message.

  ```bash
  git log --pretty=full
  ```

- **fuller**: Show even more detailed information.

  ```bash
  git log --pretty=fuller
  ```

- **format**: Use a custom format.

  ```bash
  git log --pretty=format:"%h - %an, %ar : %s"
  ```

#### Limiting Output
You can limit the number of commits displayed:

- **-n**: Show only the last `n` commits.

  ```bash
  git log -5
  ```

- **--since, --until**: Show commits made after or before a specific date.

  ```bash
  git log --since="2 weeks ago"
  git log --until="2024-01-01"
  ```

- **--author**: Show commits by a specific author.

  ```bash
  git log --author="Author Name"
  ```

- **--grep**: Search commit messages for a specific keyword.

  ```bash
  git log --grep="fix"
  ```

#### Showing Changes
You can show the changes introduced in each commit:

- **-p**: Show the patch (diff) introduced in each commit.

  ```bash
  git log -p
  ```

- **--stat**: Show statistics about changes in each commit.

  ```bash
  git log --stat
  ```

- **--name-only**: Show only the names of files changed in each commit.

  ```bash
  git log --name-only
  ```

- **--name-status**: Show the names and status (e.g., added, modified) of files changed in each commit.

  ```bash
  git log --name-status
  ```

### Example Usage

#### View Basic Log
```bash
git log
```

#### View Log with One Line Per Commit
```bash
git log --oneline
```

#### View Log with Custom Format
```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

#### View Last 3 Commits
```bash
git log -3
```

#### View Commits by a Specific Author
```bash
git log --author="Jane Doe"
```

#### View Commits with a Keyword in Message
```bash
git log --grep="bugfix"
```

#### View Commits with Detailed Changes
```bash
git log -p
```

#### View Commits with File Change Statistics
```bash
git log --stat
```

### Summary
- `git log` is used to view the commit history.
- You can customize the output format with options like `--pretty`, `--oneline`, and `--format`.
- Limit the number of commits shown with `-n`, `--since`, `--until`, `--author`, and `--grep`.
- Display detailed changes with `-p`, `--stat`, `--name-only`, and `--name-status`.
- Combine multiple options to tailor the commit history view to your needs.

## `git commit`
The `git commit` command is used to save changes to the local repository. When you make changes in your working directory and stage them using `git add`, the `git commit` command records these changes along with a descriptive message. This command is crucial in version control as it creates a snapshot of your project’s current state. Here’s a detailed explanation of how to use `git commit` and its options:

### Basic Usage
To commit staged changes with a message, use the `-m` option followed by the commit message in quotes:

```bash
git commit -m "Your commit message here"
```

### Common Options

#### Writing a Commit Message
You can write a commit message using the `-m` option. For example:

```bash
git commit -m "Add new feature to the project"
```

#### Multi-Line Commit Messages
For a more detailed commit message, you can use multiple `-m` options:

```bash
git commit -m "Title of the commit" -m "Detailed description of the changes made"
```

Alternatively, you can omit the `-m` option to open your default text editor, allowing you to write a multi-line commit message:

```bash
git commit
```

#### Amending the Last Commit
If you want to modify the last commit (for example, to change the commit message or include new changes), you can use the `--amend` option:

```bash
git commit --amend -m "Updated commit message"
```

If you’ve made additional changes that you want to include in the last commit:

```bash
git add .
git commit --amend
```

This command will open your default text editor to edit the commit message and include any newly staged changes.

#### Including All Changes
You can automatically stage and commit all changes in your working directory by using the `-a` option:

```bash
git commit -a -m "Commit message for all changes"
```

Note that this only stages and commits changes to tracked files. Untracked files will not be included.

#### Signing a Commit
If you have GPG set up, you can sign your commit to verify its authenticity:

```bash
git commit -S -m "Signed commit message"
```

### Example Workflows

#### Simple Commit
1. Make changes to your files.
2. Stage the changes:

    ```bash
    git add .
    ```

3. Commit the changes:

    ```bash
    git commit -m "Describe the changes made"
    ```

#### Amending a Commit
1. Make additional changes.
2. Stage the new changes:

    ```bash
    git add .
    ```

3. Amend the last commit:

    ```bash
    git commit --amend
    ```

#### Committing All Changes
1. Make changes to your files.
2. Commit all changes (tracked files only):

    ```bash
    git commit -a -m "Commit all changes"
    ```

### Viewing Commit History
After making commits, you can view the commit history using:

```bash
git log
```

### Summary
- `git commit` records changes to the local repository with a descriptive message.
- Use `git commit -m "message"` to commit with a message.
- Use `git commit --amend` to modify the last commit.
- Use `git commit -a -m "message"` to stage and commit all tracked changes.
- Signed commits can be made using `git commit -S -m "message"` if GPG is configured.

### Best Practices for Commit Messages
- **Keep it concise**: The first line should be a concise summary of the changes, ideally 50 characters or less.
- **Separate subject and body**: Use a blank line to separate the summary from the body of the commit message.
- **Explain the why**: Use the body to explain the reasoning behind the changes, not just what was changed.
- **Use imperative mood**: Write the message as if you are giving an order, e.g., "Fix bug" instead of "Fixed bug".

By following these best practices, you can ensure that your commit messages are clear, informative, and useful for understanding the history and context of changes in your project.

## `git diff`
The `git diff` command is used to show the differences between various states of a Git repository. It's a powerful tool to view what changes have been made, either in the working directory, staging area, or between commits. Here’s a detailed explanation of how to use `git diff` and its options:

### Basic Usage
To see changes that have been made but not yet staged (changes in the working directory):

```bash
git diff
```

### Viewing Changes Between Different States

#### Changes in Staging Area vs. Last Commit
To see changes that have been staged for the next commit but not yet committed:

```bash
git diff --staged
```
or
```bash
git diff --cached
```

#### Changes Between Commits
To see changes between two commits, you can specify the commit hashes or references:

```bash
git diff commit1 commit2
```

For example:
```bash
git diff HEAD^ HEAD
```

#### Changes Between Commit and Working Directory
To see changes between a commit and the current working directory:

```bash
git diff commit
```

For example:
```bash
git diff HEAD
```

#### Changes Between Branches
To see changes between two branches:

```bash
git diff branch1 branch2
```

For example:
```bash
git diff main feature-branch
```

### Viewing Changes for Specific Files
To see changes in a specific file:

```bash
git diff filename
```

To see changes in a specific file that have been staged for the next commit:

```bash
git diff --staged filename
```

### Common Options

#### Output Format Options
- **--name-only**: Show only the names of files that have changed.

  ```bash
  git diff --name-only
  ```

- **--name-status**: Show the names and statuses (e.g., added, modified) of files that have changed.

  ```bash
  git diff --name-status
  ```

- **--color**: Force color output.

  ```bash
  git diff --color
  ```

#### Filtering by Type of Change
- **--diff-filter**: Show only changes of a certain type (e.g., added, modified, deleted).

  ```bash
  git diff --diff-filter=A
  ```

  Common filter codes:
  - `A` for added
  - `M` for modified
  - `D` for deleted
  - `R` for renamed
  - `C` for copied
  - `T` for changed in the type
  - `U` for unmerged
  - `X` for unknown

### Example Workflows

#### Viewing Unstaged Changes
1. Make changes to files in your working directory.
2. View unstaged changes:

    ```bash
    git diff
    ```

#### Viewing Staged Changes
1. Stage changes:

    ```bash
    git add .
    ```

2. View staged changes:

    ```bash
    git diff --staged
    ```

#### Comparing Two Branches
1. Ensure you have the latest changes from both branches:

    ```bash
    git fetch
    ```

2. Compare the branches:

    ```bash
    git diff main feature-branch
    ```

#### Viewing Changes for a Specific File
1. Make changes to a specific file, e.g., `example.txt`.
2. View changes for that file:

    ```bash
    git diff example.txt
    ```

### Summary
- `git diff` shows the differences between various states in a Git repository.
- Use `git diff` to see changes in the working directory.
- Use `git diff --staged` to see changes staged for the next commit.
- Specify commit hashes to compare different commits.
- Use `git diff branch1 branch2` to compare branches.
- Various options like `--name-only`, `--name-status`, and `--diff-filter` help customize the output.

By understanding and utilizing the `git diff` command, you can efficiently track changes and review modifications at different stages of your development process.

## `git restore`
The `git restore` command is used to discard changes in the working directory or to restore files from the staging area or a specific commit. It was introduced in Git 2.23 as a more user-friendly alternative to some uses of `git checkout` and `git reset`. Here's a detailed explanation of how to use `git restore` and its options:

### Basic Usage

#### Restore Unstaged Changes
To discard changes in your working directory for a specific file (restoring it to the last committed state):

```bash
git restore filename
```

#### Restore Staged Changes
To unstage a file, keeping its changes in the working directory:

```bash
git restore --staged filename
```

### Restoring Files from a Specific Commit
To restore a file from a specific commit, you can specify the commit hash:

```bash
git restore --source=commit_hash filename
```

For example:

```bash
git restore --source=HEAD~1 filename
```

This restores the file to its state in the specified commit.

### Common Options

#### Interactive Mode
To interactively choose hunks of changes to restore:

```bash
git restore -p filename
```

#### Restore All Files
To discard all changes in the working directory:

```bash
git restore .
```

To unstage all files:

```bash
git restore --staged .
```

### Examples

#### Discard Changes in a Single File
Suppose you've modified `example.txt` and want to discard those changes:

```bash
git restore example.txt
```

#### Unstage a File
If you've staged `example.txt` but want to unstage it:

```bash
git restore --staged example.txt
```

#### Restore a File from a Previous Commit
To restore `example.txt` from the commit with hash `abc123`:

```bash
git restore --source=abc123 example.txt
```

#### Discard All Changes in the Working Directory
To discard all changes in the working directory:

```bash
git restore .
```

#### Interactive Restore
To interactively choose which changes to discard in `example.txt`:

```bash
git restore -p example.txt
```

### Summary
- **Discard Working Directory Changes**: `git restore filename`
- **Unstage Changes**: `git restore --staged filename`
- **Restore from Commit**: `git restore --source=commit_hash filename`
- **Interactive Restore**: `git restore -p filename`
- **Discard All Changes**: `git restore .`
- **Unstage All Files**: `git restore --staged .`

### Comparison with Similar Commands
- **`git checkout -- filename`**: Previously used to discard changes in the working directory. Replaced by `git restore filename` for this purpose.
- **`git reset HEAD filename`**: Previously used to unstage changes. Replaced by `git restore --staged filename` for this purpose.

By using `git restore`, you can more clearly express your intention to either discard changes in your working directory or unstage changes, making your Git workflows more intuitive and less error-prone.

## `git push`
The `git push` command is used to upload local repository content to a remote repository. By pushing changes, you share commits, branches, and tags with other collaborators. This command is typically used after `git commit` to synchronize your local repository with the remote repository.

### Basic Usage
To push changes to the remote repository:

```bash
git push
```

This command pushes commits from your local branch to the corresponding remote branch that it tracks.

### Pushing to a Specific Branch
To push changes to a specific branch on the remote repository:

```bash
git push origin branch_name
```

For example, to push the `main` branch:

```bash
git push origin main
```

### Common Options

#### Set Upstream
When pushing a new branch for the first time, you can set the remote branch to track the local branch with the `-u` (or `--set-upstream`) option:

```bash
git push -u origin branch_name
```

This command sets the remote branch as the upstream branch for the local branch, meaning future `git push` and `git pull` commands will default to this remote branch.

#### Force Push
To forcefully push changes, overwriting the remote branch history:

```bash
git push --force
```

**Caution**: Force pushing can overwrite commits in the remote repository, potentially causing data loss for collaborators.

#### Push All Branches
To push all local branches to the remote repository:

```bash
git push --all
```

#### Push Tags
To push all tags to the remote repository:

```bash
git push --tags
```

### Examples

#### Push Current Branch
Assuming you are on the `feature` branch and want to push it to the remote repository:

```bash
git push origin feature
```

#### Set Upstream for a New Branch
If you create a new branch `new-feature` and want to push it while setting the upstream branch:

```bash
git push -u origin new-feature
```

#### Force Push to a Branch
If you need to force push changes to the `main` branch:

```bash
git push --force origin main
```

#### Push All Local Branches
To push all your local branches to the remote repository:

```bash
git push --all
```

#### Push All Tags
To push all tags to the remote repository:

```bash
git push --tags
```

### Summary
- **Basic Push**: `git push`
- **Push to Specific Branch**: `git push origin branch_name`
- **Set Upstream**: `git push -u origin branch_name`
- **Force Push**: `git push --force`
- **Push All Branches**: `git push --all`
- **Push All Tags**: `git push --tags`

### Best Practices
- **Avoid Force Push**: Force pushing can overwrite remote history, which can be disruptive to collaborators. Use it with caution.
- **Set Upstream**: Use `-u` option when pushing new branches to simplify future pushes and pulls.
- **Communicate**: When pushing significant changes or force pushing, communicate with your team to avoid conflicts and data loss.

By understanding and using the `git push` command and its options, you can effectively share your work with others and keep your remote repository in sync with your local changes.

## `git remote`
The `git remote` command is used to manage remote repositories in a Git project. Remote repositories are versions of your project that are hosted on the internet or a network. Here are the main subcommands of `git remote` and how they are used:

### Basic Usage

#### List Remote Repositories
To list the remote repositories associated with your local repository:

```bash
git remote
```

This command will list the names of the remote repositories, typically `origin` by default if you have cloned a repository.

#### Show Details of Remote
To show more details about a specific remote, such as its URL:

```bash
git remote show remote_name
```

Replace `remote_name` with the name of the remote repository, such as `origin`.

#### Add a Remote
To add a new remote repository:

```bash
git remote add remote_name remote_url
```

Replace `remote_name` with the desired name for the remote repository, and `remote_url` with the URL of the remote repository.

#### Remove a Remote
To remove a remote repository:

```bash
git remote remove remote_name
```

Replace `remote_name` with the name of the remote repository you want to remove.

### Common Options

#### Rename a Remote
To rename an existing remote repository:

```bash
git remote rename old_name new_name
```

Replace `old_name` with the current name of the remote repository and `new_name` with the new name you want to assign.

#### Change URL of a Remote
To change the URL of an existing remote repository:

```bash
git remote set-url remote_name new_url
```

Replace `remote_name` with the name of the remote repository and `new_url` with the new URL you want to set.

#### Show Remote URLs
To show the URLs associated with a remote repository:

```bash
git remote show remote_name
```

Replace `remote_name` with the name of the remote repository.

### Examples

#### List Remote Repositories
```bash
git remote
```

#### Show Details of Remote
```bash
git remote show origin
```

#### Add a Remote
```bash
git remote add upstream https://github.com/example/repository.git
```

#### Remove a Remote
```bash
git remote remove upstream
```

#### Rename a Remote
```bash
git remote rename origin main-origin
```

#### Change URL of a Remote
```bash
git remote set-url origin https://github.com/example/new-repository.git
```

### Summary
- **List Remotes**: `git remote`
- **Show Details**: `git remote show remote_name`
- **Add Remote**: `git remote add remote_name remote_url`
- **Remove Remote**: `git remote remove remote_name`
- **Rename Remote**: `git remote rename old_name new_name`
- **Change Remote URL**: `git remote set-url remote_name new_url`

Managing remote repositories is crucial for collaboration and syncing your work with others. Understanding these `git remote` commands will help you effectively work with remote repositories in your Git projects.

## `git branch`
The `git branch` command in Git is used to create, list, rename, and delete branches in a Git repository. Here's a detailed explanation of how to use `git branch` and its options:

### Basic Usage

#### List Branches
To list all branches in your repository:

```bash
git branch
```

The branch you are currently on will be highlighted with an asterisk (`*`).

#### Create a Branch
To create a new branch:

```bash
git branch branch_name
```

Replace `branch_name` with the desired name for your new branch.

#### Switch to a Branch
To switch to an existing branch:

```bash
git checkout branch_name
```

This command also puts you on the specified branch.

#### Create and Switch to a Branch
To create a new branch and switch to it in one step:

```bash
git checkout -b new_branch_name
```

Replace `new_branch_name` with the desired name for your new branch.

### Common Options

#### Rename a Branch
To rename an existing branch:

```bash
git branch -m old_branch_name new_branch_name
```

Replace `old_branch_name` with the current name of the branch and `new_branch_name` with the new name you want to assign.

#### Delete a Branch
To delete a branch:

```bash
git branch -d branch_name
```

Replace `branch_name` with the name of the branch you want to delete. Use `-D` instead of `-d` to force delete a branch that has unmerged changes.

#### Show Remote Branches
To list remote branches:

```bash
git branch -r
```

This command shows branches from remote repositories.

#### Show All Branches
To show all local and remote branches:

```bash
git branch -a
```

### Examples

#### List Branches
```bash
git branch
```

#### Create a Branch
```bash
git branch new_feature
```

#### Switch to a Branch
```bash
git checkout main
```

#### Create and Switch to a Branch
```bash
git checkout -b bugfix
```

#### Rename a Branch
```bash
git branch -m old_feature new_feature
```

#### Delete a Branch
```bash
git branch -d outdated_branch
```

#### Show Remote Branches
```bash
git branch -r
```

#### Show All Branches
```bash
git branch -a
```

### Summary
- **List Branches**: `git branch`
- **Create Branch**: `git branch branch_name`
- **Switch Branch**: `git checkout branch_name`
- **Create and Switch Branch**: `git checkout -b new_branch_name`
- **Rename Branch**: `git branch -m old_branch_name new_branch_name`
- **Delete Branch**: `git branch -d branch_name`
- **Show Remote Branches**: `git branch -r`
- **Show All Branches**: `git branch -a`

Understanding how to manage branches is fundamental to Git workflows, allowing you to work on different features or versions of your code concurrently and manage collaboration effectively.

## `git pull`
The `git pull` command is used to fetch changes from a remote repository and merge them into your current branch. It is a combination of `git fetch` and `git merge`. This command helps you keep your local repository up-to-date with changes made by other collaborators.

### Basic Usage

#### Pull Changes from Remote Repository
To pull changes from the remote repository to your current branch:

```bash
git pull
```

This command fetches changes from the remote repository (defaulting to `origin`) and merges them into your current branch.

### Pull from a Specific Remote and Branch

To pull changes from a specific remote repository and branch:

```bash
git pull remote_name branch_name
```

Replace `remote_name` with the name of the remote repository (e.g., `origin`) and `branch_name` with the name of the branch you want to pull changes from.

### Common Options

#### Rebase Instead of Merge

To rebase the current branch on top of the upstream branch after fetching:

```bash
git pull --rebase
```

This option applies your local commits on top of the fetched commits, providing a linear history.

#### Specify a Different Repository

To pull changes from a specific repository URL:

```bash
git pull repository_url
```

#### Specify the Depth of the Fetch

To perform a shallow fetch and merge (only fetching the most recent commits):

```bash
git pull --depth=1
```

### Examples

#### Pull from Default Remote and Branch

```bash
git pull
```

This command fetches and merges changes from the `origin` remote's branch that your current branch is tracking.

#### Pull from a Specific Branch

```bash
git pull origin feature-branch
```

This command fetches and merges changes from the `feature-branch` on the `origin` remote.

#### Pull with Rebase

```bash
git pull --rebase
```

This command rebases your current branch on top of the fetched commits.

#### Pull from a Specific Repository URL

```bash
git pull https://github.com/example/repo.git
```

This command fetches and merges changes from the specified repository URL.

#### Shallow Pull

```bash
git pull --depth=1
```

This command fetches only the most recent commit from the remote repository and merges it.

### Summary

- **Pull from Default Remote**: `git pull`
- **Pull from Specific Remote and Branch**: `git pull remote_name branch_name`
- **Pull with Rebase**: `git pull --rebase`
- **Pull from Specific Repository URL**: `git pull repository_url`
- **Shallow Pull**: `git pull --depth=1`

### Best Practices

- **Commit Local Changes**: Before running `git pull`, make sure you commit or stash any local changes to avoid conflicts.
- **Use Rebase for Clean History**: Use `git pull --rebase` to maintain a cleaner, linear project history.
- **Communicate with Team**: Communicate with your team when pulling large or critical changes to avoid conflicts and ensure everyone is on the same page.

Understanding `git pull` is crucial for keeping your local repository synchronized with the remote repository and collaborating effectively with others.

## `git merge`
The `git merge` command is used to combine multiple branches into a single branch. It integrates changes from the specified branch into the current branch, preserving the commit history. Here's a detailed explanation of how to use `git merge` and its options:

### Basic Usage

#### Merge a Branch into the Current Branch
To merge changes from one branch into the current branch:

```bash
git merge branch_name
```

Replace `branch_name` with the name of the branch you want to merge into your current branch.

### Fast-Forward Merge
If the current branch has not diverged from the branch being merged, Git performs a fast-forward merge. This simply moves the HEAD forward to the latest commit of the branch being merged.

### Three-Way Merge
If the branches have diverged, Git performs a three-way merge, creating a new commit that combines the changes from both branches.

### Common Options

#### No Fast-Forward Merge
To create a merge commit even if the merge could be resolved as a fast-forward:

```bash
git merge --no-ff branch_name
```

This option is useful for keeping a clear history of feature branches.

#### Squash and Merge
To combine all commits from the branch being merged into a single commit:

```bash
git merge --squash branch_name
```

This option prepares the changes for squashing but does not automatically commit them. You need to run `git commit` after using this option.

#### Abort a Merge
To abort a merge and return to the pre-merge state if conflicts occur:

```bash
git merge --abort
```

This command undoes the changes made by the merge and restores the state before the merge started.

### Examples

#### Basic Merge
Assume you are on the `main` branch and want to merge changes from the `feature` branch:

```bash
git checkout main
git merge feature
```

#### No Fast-Forward Merge
To create a merge commit even if a fast-forward is possible:

```bash
git checkout main
git merge --no-ff feature
```

#### Squash and Merge
To squash commits from the `feature` branch into a single commit:

```bash
git checkout main
git merge --squash feature
git commit -m "Merged feature branch"
```

#### Abort a Merge
If you encounter conflicts during a merge and want to abort:

```bash
git merge --abort
```

### Summary

- **Basic Merge**: `git merge branch_name`
- **No Fast-Forward Merge**: `git merge --no-ff branch_name`
- **Squash and Merge**: `git merge --squash branch_name`
- **Abort a Merge**: `git merge --abort`

### Handling Merge Conflicts

When merging branches, conflicts can occur if the same part of a file has been modified in different ways in the branches being merged. Here's how to handle merge conflicts:

1. **Identify Conflicts**: Git will notify you of conflicts and mark the conflicted areas in the files.
2. **Resolve Conflicts**: Manually edit the conflicted files to resolve the differences. Git marks conflicts with `<<<<<<<`, `=======`, and `>>>>>>>` markers.
3. **Mark as Resolved**: After resolving the conflicts, mark the files as resolved:

    ```bash
    git add resolved_file
    ```

4. **Complete the Merge**: Complete the merge by committing the changes:

    ```bash
    git commit
    ```

### Best Practices

- **Commit Changes**: Ensure your working directory is clean (commit or stash changes) before starting a merge.
- **Review History**: Review commit history to understand changes in the branches being merged.
- **Communicate**: Communicate with your team, especially when merging significant changes or feature branches.

Understanding `git merge` is essential for combining changes from different branches and collaborating effectively in a version-controlled environment.

## `git rebase`
The `git rebase` command is used to move or combine a sequence of commits to a new base commit. Rebasing is often used to maintain a linear project history and to simplify the integration of changes from different branches. Here's a detailed explanation of how to use `git rebase` and its options:

### Basic Usage

#### Rebase Current Branch onto Another Branch
To rebase the current branch onto another branch:

```bash
git checkout feature
git rebase main
```

This command replays the commits from the `feature` branch onto the `main` branch, effectively moving the base of the `feature` branch to the tip of the `main` branch.

### Interactive Rebase

Interactive rebase allows you to edit, reorder, and squash commits. To start an interactive rebase:

```bash
git rebase -i HEAD~n
```

Replace `n` with the number of commits you want to rebase. For example, `HEAD~3` will open an interactive rebase for the last three commits.

### Common Options

#### Abort a Rebase
To abort an ongoing rebase and return to the original branch state:

```bash
git rebase --abort
```

#### Continue a Rebase
To continue a rebase after resolving conflicts:

```bash
git rebase --continue
```

#### Skip a Commit
To skip the current commit during a rebase:

```bash
git rebase --skip
```

#### Preserve Merge Commits
To rebase while preserving merge commits:

```bash
git rebase --preserve-merges
```

#### Autosquash Commits
To automatically squash fixup commits into the previous commit:

```bash
git rebase --autosquash
```

### Examples

#### Basic Rebase
Assume you are on the `feature` branch and want to rebase it onto the `main` branch:

```bash
git checkout feature
git rebase main
```

#### Interactive Rebase
To interactively rebase the last three commits:

```bash
git rebase -i HEAD~3
```

#### Abort a Rebase
To abort an ongoing rebase:

```bash
git rebase --abort
```

#### Continue a Rebase
After resolving conflicts during a rebase:

```bash
git add resolved_file
git rebase --continue
```

#### Skip a Commit
To skip the current commit during a rebase:

```bash
git rebase --skip
```

### Summary
- **Basic Rebase**: `git rebase branch_name`
- **Interactive Rebase**: `git rebase -i HEAD~n`
- **Abort a Rebase**: `git rebase --abort`
- **Continue a Rebase**: `git rebase --continue`
- **Skip a Commit**: `git rebase --skip`
- **Preserve Merge Commits**: `git rebase --preserve-merges`
- **Autosquash Commits**: `git rebase --autosquash`

### Handling Rebase Conflicts

During a rebase, conflicts can occur if changes in your commits overlap with changes in the branch you are rebasing onto. Here's how to handle rebase conflicts:

1. **Identify Conflicts**: Git will notify you of conflicts and mark the conflicted areas in the files.
2. **Resolve Conflicts**: Manually edit the conflicted files to resolve the differences. Git marks conflicts with `<<<<<<<`, `=======`, and `>>>>>>>` markers.
3. **Mark as Resolved**: After resolving the conflicts, mark the files as resolved:

    ```bash
    git add resolved_file
    ```

4. **Continue the Rebase**: Continue the rebase process:

    ```bash
    git rebase --continue
    ```

5. **Abort if Necessary**: If you want to abort the rebase and return to the original branch state:

    ```bash
    git rebase --abort
    ```

### Best Practices

- **Use with Caution**: Rebasing can rewrite commit history, which can be problematic when working with shared branches. Use it with caution and communicate with your team.
- **Interactive Rebase**: Use interactive rebase to clean up commit history before merging branches.
- **Resolve Conflicts Carefully**: Carefully resolve conflicts during a rebase to avoid introducing errors.

Understanding `git rebase` helps you maintain a clean and understandable commit history, making it easier to collaborate and manage changes in a project.

## `Handling Conflicts`
When working with Git, conflicts can occur during operations like merging, rebasing, or pulling changes from a remote repository. A conflict arises when Git is unable to automatically resolve differences between branches. Here’s a guide on how to handle Git conflicts.

### Understanding Git Conflicts

#### When Do Conflicts Occur?
Conflicts typically occur when:
- Two branches modify the same line in a file differently.
- A file is modified in one branch and deleted in another.
- There are differences in binary files that Git cannot automatically merge.

### Identifying Conflicts

When a conflict occurs, Git will:
- Halt the merge, rebase, or pull operation.
- Mark the conflicting files in the working directory.
- Add conflict markers within the files.

### Conflict Markers

Git uses conflict markers to indicate the sections of the file that are in conflict. The markers look like this:

```
<<<<<<< HEAD
Changes from the current branch
=======
Changes from the branch being merged
>>>>>>> branch_name
```

### Steps to Resolve Conflicts

#### 1. Identify Conflicted Files
After a merge conflict, Git will list the conflicted files. You can see these files with:

```bash
git status
```

Files with conflicts will be listed under "Unmerged paths".

#### 2. Open Conflicted Files
Open each conflicted file in your text editor. Look for the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

#### 3. Resolve Conflicts
Manually edit the file to resolve the differences between the conflicting changes. Remove the conflict markers after resolving.

Example:
```diff
<<<<<<< HEAD
Current branch changes
=======
Other branch changes
>>>>>>> branch_name
```

Resolve by choosing one side, combining changes, or writing a new resolution:
```diff
Combined or resolved changes
```

#### 4. Mark the Conflicts as Resolved
After resolving the conflicts and saving the changes, mark the file as resolved:

```bash
git add resolved_file
```

#### 5. Continue with the Operation
If you are merging:
```bash
git commit
```

If you are rebasing:
```bash
git rebase --continue
```

If you want to abort the rebase or merge:
```bash
git merge --abort
git rebase --abort
```

### Example Workflow: Resolving a Merge Conflict

1. **Merge Command**:
    ```bash
    git merge feature-branch
    ```

2. **Identify Conflicts**:
    ```bash
    git status
    ```

3. **Open Conflicted File**: Open the file listed in the conflict, e.g., `example.txt`.

4. **Resolve Conflicts**:
    Before:
    ```diff
    <<<<<<< HEAD
    Current branch changes
    =======
    Other branch changes
    >>>>>>> feature-branch
    ```

    After:
    ```diff
    Combined or resolved changes
    ```

5. **Mark as Resolved**:
    ```bash
    git add example.txt
    ```

6. **Complete the Merge**:
    ```bash
    git commit
    ```

### Example Workflow: Resolving a Rebase Conflict

1. **Rebase Command**:
    ```bash
    git rebase main
    ```

2. **Identify Conflicts**:
    ```bash
    git status
    ```

3. **Open Conflicted File**: Open the file listed in the conflict, e.g., `example.txt`.

4. **Resolve Conflicts**:
    Before:
    ```diff
    <<<<<<< HEAD
    Current branch changes
    =======
    Other branch changes
    >>>>>>> main
    ```

    After:
    ```diff
    Combined or resolved changes
    ```

5. **Mark as Resolved**:
    ```bash
    git add example.txt
    ```

6. **Continue the Rebase**:
    ```bash
    git rebase --continue
    ```

### Best Practices for Avoiding and Resolving Conflicts

- **Communicate with Your Team**: Regularly sync with your team to avoid conflicts.
- **Make Frequent Commits**: Smaller commits are easier to merge and resolve conflicts.
- **Pull Changes Regularly**: Keep your branch updated with changes from the remote repository.
- **Use Feature Branches**: Work on separate branches for new features or bug fixes.
- **Resolve Conflicts Promptly**: Address conflicts as soon as they arise to avoid complex resolutions.

Understanding and managing Git conflicts is essential for maintaining a smooth workflow in collaborative projects. Proper conflict resolution ensures that all changes are correctly integrated and the project history remains clean and understandable.

## `git show`
The `git show` command is used to display various types of objects in Git, such as commits, trees, and blobs. By default, it shows the details of a specific commit, including the commit message, author, date, and the diff showing changes introduced by the commit. Here’s a comprehensive guide on how to use `git show` and its options.

### Basic Usage

#### Show Details of a Specific Commit
To show the details of a specific commit:

```bash
git show commit_hash
```

Replace `commit_hash` with the SHA-1 hash of the commit you want to inspect. For example:

```bash
git show 9fceb02
```

### Examples and Options

#### Show the Latest Commit
To show the details of the latest commit:

```bash
git show
```

#### Show a Specific Commit
To show a specific commit by its hash:

```bash
git show a1b2c3d
```

#### Show Changes in a Specific File for a Commit
To show changes introduced by a commit for a specific file:

```bash
git show commit_hash:path/to/file
```

For example:

```bash
git show 9fceb02:path/to/file.txt
```

#### Show Summary of Changes
To show a summary of changes (diffstat) instead of the full diff:

```bash
git show --stat commit_hash
```

For example:

```bash
git show --stat 9fceb02
```

#### Show Abbreviated Commit
To show a more abbreviated commit message with minimal diff:

```bash
git show --oneline --no-patch commit_hash
```

For example:

```bash
git show --oneline --no-patch 9fceb02
```

#### Show Commit Details Without Diff
To show commit details without showing the diff:

```bash
git show --no-patch commit_hash
```

For example:

```bash
git show --no-patch 9fceb02
```

### Formatting Options

#### Show Pretty Formatted Output
To format the output in a more readable way, use the `--pretty` option with formats like `short`, `medium`, `full`, `fuller`, or `format`:

```bash
git show --pretty=short commit_hash
```

For example, using a custom format:

```bash
git show --pretty=format:"%h - %an, %ar : %s" commit_hash
```

#### Show Custom Diff
To show a custom diff format, use the `--format` option:

```bash
git show --format=short commit_hash
```

### Examples

1. **Show the latest commit**:

    ```bash
    git show
    ```

2. **Show a specific commit**:

    ```bash
    git show 9fceb02
    ```

3. **Show changes in a specific file for a commit**:

    ```bash
    git show 9fceb02:path/to/file.txt
    ```

4. **Show a summary of changes**:

    ```bash
    git show --stat 9fceb02
    ```

5. **Show an abbreviated commit message**:

    ```bash
    git show --oneline --no-patch 9fceb02
    ```

6. **Show commit details without the diff**:

    ```bash
    git show --no-patch 9fceb02
    ```

7. **Show a pretty formatted output**:

    ```bash
    git show --pretty=short 9fceb02
    ```

8. **Show a custom formatted output**:

    ```bash
    git show --pretty=format:"%h - %an, %ar : %s" 9fceb02
    ```

### Summary

- **Show Specific Commit**: `git show commit_hash`
- **Show Latest Commit**: `git show`
- **Show Changes in Specific File**: `git show commit_hash:path/to/file`
- **Show Summary of Changes**: `git show --stat commit_hash`
- **Show Abbreviated Commit**: `git show --oneline --no-patch commit_hash`
- **Show Commit Details Without Diff**: `git show --no-patch commit_hash`
- **Show Pretty Formatted Output**: `git show --pretty=format:"format" commit_hash`

Understanding `git show` helps in inspecting changes introduced by commits and analyzing the details of specific commits in a Git repository. This command is essential for reviewing the history and understanding the context of changes in your project.

To set up Git for your GitHub repositories on your Linux machine, follow these steps:

---

### **Install Git**
First, check if Git is already installed:
```bash
git --version
```
If not installed, install it using your package manager:

- **Debian/Ubuntu**:
  ```bash
  sudo apt update && sudo apt install git -y
  ```
- **Fedora**:
  ```bash
  sudo dnf install git -y
  ```
- **Arch Linux**:
  ```bash
  sudo pacman -S git
  ```

---

### **Configure Git**
Set your global username and email (must match your GitHub email):
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
Verify your configuration:
```bash
git config --global --list
```

---

### **Generate SSH Key (Recommended)**
To securely connect GitHub via SSH:

**Check for an existing SSH key**:
   ```bash
   ls ~/.ssh/id_rsa.pub
   ```
   If the file exists, you can use it. If not, generate a new key.

**Generate a new SSH key**:
   ```bash
   ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
   ```
   Press `Enter` to accept the default save location (`~/.ssh/id_rsa`), and set a passphrase (optional).

**Start SSH agent**:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_rsa
   ```

**Copy SSH key to GitHub**:
   ```bash
   cat ~/.ssh/id_rsa.pub
   ```
   Copy the output and add it to GitHub:
   - Go to [GitHub SSH Keys](https://github.com/settings/keys)
   - Click **New SSH Key**, paste the key, and save.

**Test the SSH connection**:
   ```bash
   ssh -T git@github.com
   ```
   If successful, it should say:
   ```
   Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.
   ```

---

### **4. Clone a Repository**
To clone a repository:
```bash
git clone git@github.com:your-username/repository-name.git
```

Navigate into the directory:
```bash
cd repository-name
```

---

### **Work with Git**
- **Check repository status**:
  ```bash
  git status
  ```
- **Add changes**:
  ```bash
  git add .
  ```
- **Commit changes**:
  ```bash
  git commit -m "Your commit message"
  ```
- **Push changes to GitHub**:
  ```bash
  git push origin main
  ```

If the branch is not set, use:
```bash
git push --set-upstream origin main
```

---

### **Pull Latest Changes**
To update your local repository:
```bash
git pull origin main
```

---

### **Creating a New Repository on GitHub & Push**
Create a new repository on GitHub.
Initialize Git in your local project folder:
   ```bash
   git init
   ```
Add a remote origin:
   ```bash
   git remote add origin git@github.com:your-username/repository-name.git
   ```
Add and push files:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

---
