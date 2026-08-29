## Daily Workflow

- **`git status`**: Shows the state of your working directory. Run this constantly to see which files are modified, staged, or untracked.
    
      
    
- **`git add .`**: Stages all modified and new files in the current directory, preparing them for the next commit. (Use `git add [file]` to stage a single file).
    
      
    
- **`git commit -m "Your message"`**: Records your staged changes permanently in the local repository's history.
    
      
    
- **`git push`**: Uploads your local commits to the remote repository (like GitHub or GitLab).
    
      
    
- **`git pull`**: Downloads the latest changes from the remote repository and immediately merges them into your current local branch.
    
      
    

## Branching & Navigation

- **`git switch -c [branch-name]`**: Creates a new branch and immediately switches you to it. (You will also frequently see the older command `git checkout -b [branch-name]`).
    
      
    
- **`git switch [branch-name]`**: Moves you to an existing branch.
    
      
    
- **`git branch`**: Lists all your local branches. The branch you are currently on will be highlighted with an asterisk (`*`).
    
      
    
- **`git merge [branch-name]`**: Takes the commits from the specified branch and combines them into the branch you are currently on.
    
      
    

## Reviewing History & Changes

- **`git log --oneline`**: Shows your commit history in a compact, easy-to-read format (one line per commit).
    
      
    
- **`git diff`**: Shows exactly what lines of code you have changed but haven't staged yet.
    
      
    
- **`git diff --staged`**: Shows the changes you have already staged (added) that will go into your next commit.
    
      
    

## The Lifesavers (Undoing & Stashing)

- **`git stash`**: Temporarily shelves (stashes) your uncommitted changes, returning your working directory to a clean state. Perfect when you need to switch branches quickly but aren't ready to commit.
    
      
    
- **`git stash pop`**: Retrieves your most recently stashed changes and applies them back to your working directory.
    
      
    
- **`git restore [file]`**: Discards unstaged changes in a specific file, returning it to exactly how it looked at your last commit. (Older equivalent: `git checkout -- [file]`).
    
      
    
- **`git reset --soft HEAD~1`**: Undoes your very last commit, but keeps all your modified files in the staging area so you can fix them and re-commit.
    
      
    
- **`git revert [commit-hash]`**: Creates a brand new commit that perfectly does the exact opposite of a previous commit, effectively undoing it without altering your repository's public history.

---
# How to configure git and check configured or not?

