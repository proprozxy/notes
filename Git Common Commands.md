## Git Common Commands

### Configure Git

- `git config --global user.name "<name>"`: Set a global username.
- `git config --global user.email "<email address>"`: Set a global email address.
- `git config --list`: List all Git configurations.

### Initialize and Clone Repositories

- `git init`: Initialize a new Git repository in an existing directory.
- `git clone <repository URL>`: Clone an existing Git repository.

### Basic Operations

- `git add <file>`: Add file changes to the staging area.
- `git status`: Check the status of the working directory and staging area.
- `git commit -m "<commit message>"`: Commit the changes in the staging area to the repository history.
- `git log`: View the commit history.

### Branch Management

- `git branch`: List all local branches.
- `git branch <branch name>`: Create a new branch.
- `git checkout <branch name>`: Switch to a specified branch.
- `git merge <branch name>`: Merge a specified branch into the current branch.
- `git branch -d <branch name>`: Delete a branch.

### Remote Repository Operations

- `git remote add <remote name> <repository URL>`: Add a new remote repository.
- `git fetch <remote name>`: Download new branches and data from a remote repository.
- `git pull <remote name> <branch name>`: Fetch from and integrate with a remote repository or a local branch.
- `git push <remote name> <branch name>`: Upload local branch changes to a remote repository.

### Undo Changes

- `git checkout -- <file>`: Discard changes in the working directory for the specified file.
- `git reset HEAD <file>`: Unstage changes for the specified file.
- `git revert <commit>`: Create a new commit that undoes all changes made in the specified commit.
- `git reset --hard <commit>`: Reset the current branch's HEAD to the specified commit and reset the working directory and staging area, **caution**.

### Tagging

- `git tag`: List all tags.
- `git tag <tag name>`: Create a new lightweight tag based on the current commit.
- `git tag -a <tag name> -m "<tag message>"`: Create an annotated tag.

### Advanced Operations

- `git stash`: Temporarily store uncommitted changes to clean the working directory.
- `git stash pop`: Apply stored changes back to the working directory.
- `git cherry-pick <commit>`: Apply the changes from a commit from another branch onto the current branch.
- `git rebase <base branch>`: Reapply changes from the current branch onto a base branch.