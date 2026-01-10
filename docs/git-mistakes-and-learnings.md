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
