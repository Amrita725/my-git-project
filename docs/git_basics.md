# Git Basics

This document provides a comprehensive overview of **Git fundamentals**, It is intended as a reference for beginners and for interview preparation.

---

## 1.  What is Git?

- Git is a **distributed version control system**.
- Tracks changes to files in a project.
- Enables multiple developers to work on the same project simultaneously.
- Keeps a full history of commits, allowing rollback and collaboration.

---

## 2.  Git Workflow Concepts

### Working Directory
- The files and folders you are actively working on.

### Staging Area (Index)
- Intermediate area where you prepare changes before committing.
- Use `git add <file>` to stage changes.

### Local Repository
- Stores commits locally in `.git` directory.
- Your changes are tracked here before pushing to a remote.

### Remote Repository
- Hosted version of your repo (e.g., GitHub, GitLab, Bitbucket)
- Enables collaboration across teams.

---

## 3.  Basic Git Commands

| Command | Purpose |
|---------|---------|
| `git init` | Initialize a new Git repository |
| `git clone <repo-url>` | Copy a remote repo to your local machine |
| `git status` | Check the status of files (modified, staged, etc.) |
| `git add <file>` | Stage changes for commit |
| `git commit -m "message"` | Save staged changes in local repository |
| `git log` | View commit history |
| `git diff` | See changes between working directory and staging area |
| `git push` | Send local commits to the remote repository |
| `git pull` | Fetch and merge changes from remote repository |

---

## 4. Branching

- **Branch**: independent line of development.
- Helps isolate features, bug fixes, or experiments.
- HEAD: pointer to the current commit or branch.
- **Commands:**
```bash
git branch             # List branches
git branch <name>      # Create new branch
git checkout <name>    # Switch to branch
git checkout -b <name> # Create and switch to branch
git merge <branch>     # Merge branch into current branch
```
## 5. Git Remote & Origin

- **Remote repository**: Online version of your repo. 
- **Origin**: It is not a command, not a branch, not a server — just a label. Origin is the default name given to a remote repository.
- **Remote URL**:  tells your local Git repository "Where should I push/pull my code?”  
```
git remote -v                   # It shows which REMOTE repositories your local repo is connected to.  
git remote add origin <url>     # Add a remote
git remote remove origin        # Remove a remote
git push -u origin main         # Push the origin which is basically my remote repo, and main is the main branch.
git pull origin main            # Pull changes from remote
```
