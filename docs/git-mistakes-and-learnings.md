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
