## Learning 1: `main` branch did not exist after `git init`

### ❌ What I did

I initialized a repository and immediately created a new branch:

```bash
git init
git checkout -b feature-branch
```
### ⚠️ What went wrong

When I ran:
```bash
git branch
```
I could not see the main branch at all.
Git also did not allow me to checkout or merge into main.

### 🔍 Why this happened

A Git branch is only created when there is at least one commit.
Since I never made an initial commit on main, the main branch was never created.

The first branch created after git init becomes the default branch.

### ✅ Correct approach

Always create an initial commit before branching:
```bash
git init
git add .
git commit -m "Initial commit"
git checkout -b feature-branch
```
---
## Learnng 2: Folder Structure in GitHub UI  
### ❌ The Mistake / Confusion  

While creating folders in my GitHub repository using the GitHub UI, I noticed something confusing:  
I created a folder called example, inside it, I created another folder project-one. Inside project-one, I added a README.md  
However, in the GitHub repository view, instead of showing: example/, it showed: example/project-one  
This made me think that GitHub was not recognizing example as a proper folder or that I had created the structure incorrectly.  

### 🔍 What I Learned  

This behavior is expected and correct.Git does not track folders/directories. Git only tracks files  

A directory is considered meaningful by Git only if it contains at least one file. Empty directories are not considered. In my case, The example/ folder had no files directly inside it. Because of this, GitHub UI collapses the directory path and displays it as: example/project-one  

### ✅ How to Fix / Avoid This Confusion

To make a folder appear properly in GitHub, ensure the folder contains at least one file  
Example: example/README.md  
Or add a placeholder file: example/.gitkeep  

---
## Learning 3: Cannot push directly into a subfolder on GitHub

### ❌ What I tried to do

I wanted to push my code directly into a specific folder path inside my repository on GitHub: my-git-project/examples/project-1-simple-blog. To do this, I added the following remote URL, Then I tried to push my branch:

```bash
git remote add origin https://github.com/Amrita725/my-git-project/tree/main/examples/project-1-simple-blog
git push -u origin feature-add-post
```

### ⚠️ What went wrong
Git returned the following error and I could not push my changes to GitHub.
```bash
fatal: repository 'https://github.com/Amrita725/my-git-project/tree/main/examples/project-1-simple-blog/' not found
```

### 🔍 Why this happened
GitHub does not allow pushing to a subfolder path inside a repository. The /tree/main/... URL is a browser URL, not a Git repository endpoint. Git can only push to the repository root. A Git remote must always point to a .git repository, not a folder

### ✅ Correct approach
Clone or initialize the repository at the root level:

```bash
git clone https://github.com/Amrita725/my-git-project.git
cd my-git-project
```

### 🧩 Key takeaway
GitHub does not allow pushing into subfolders.
The repository root is the only push target.
Folder structure must exist locally before pushing.
Clone the repository.

---

## Learning 4: Push rejected because remote has existing commits
### ❌ What happened

When pushing my local `main` branch:

```bash
git push -u origin main
```
I received:
```bash
! [rejected] main -> main (fetch first)

hint: You have divergent branches and need to specify how to reconcile them.
fatal: Need to specify how to reconcile divergent branches.
```
### 🔍 Why this happened

The GitHub repository already contained commits (README created via UI),but my local repository was initialized separately.This caused the local and remote branches to have different histories. Your local main and remote main (origin/main) both have commits

### ✅ Correct fix
Run this once:
```bash
git pull --no-rebase
```

This tells Git:
“Merge remote changes into my local branch.”
If Git opens an editor.Just save & close (default message is fine)

After that, push normally
```bash
git push -u origin main
```
This will now work.
