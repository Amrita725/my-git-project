# Learning: Resolving a Merge Conflict by Keeping Feature Branch Changes

## Context
While working on a Git project, I created a feature branch to introduce new functionality and styling changes.  
At the same time, the `main` branch already contained an older version of the same file (`style.css`).

When I attempted to merge the feature branch into `main`, Git detected a conflict because **the same file was modified in both branches**.
```
###error
Auto-merging example/project-2-Conflict-Resolution/style.css
CONFLICT (content): Merge conflict in example/project-2-Conflict-Resolution/style.css
Automatic merge failed; fix conflicts and then commit the result.
```

This situation simulates a real-world scenario where multiple developers work on the same file simultaneously.

---

## Steps That Led to the Conflict

1. Created and committed `style.css` in the `main` branch:
   ```bash
   git checkout main
   git add style.css
   git commit -m "Add initial CSS in main"

   ```
2. Created a feature branch and modified the same file differently:

```bash
git checkout -b feature/add-note
git add style.css
git commit -m "Add new styles in feature branch"
```

3. Attempted to merge the feature branch into main:
```bash
git checkout main
git merge feature/add-note
```

4. Git stopped the merge and reported a conflict in style.css.  

## What the Conflict Looked Like  

Inside style.css, Git inserted conflict markers:  
```bash
<<<<<<< HEAD
/* Main branch CSS */
=======
/* Feature branch CSS */
>>>>>>> feature/add-note
```
 
This indicates:  
HEAD → current branch (main)  
feature/add-note → incoming branch  

Resolution Strategy: 
- Keep main only
- Keep feature only
- Combine both

## How the conflict was resolved  
Removed all conflict markers  
Finalizing the Merge  
git add style.css  
git commit -m "Resolve merge conflict by keeping feature branch changes"  
git push origin main  

## Key Learnings

A merge conflict occurs when the same file is modified differently in multiple branches.   
Git does not resolve conflicts automatically — it only highlights them.  
Resolving a conflict is a logical and business decision, not a Git decision.   
Conflict markers (<<<<<<<, =======, >>>>>>>) must be removed before committing.   
