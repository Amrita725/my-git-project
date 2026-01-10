# Git Workflows

Git workflows define **how developers collaborate and manage code**. They ensure a clean main branch, reduce conflicts, and provide structure for development.  

This document covers **common workflows**, including working with **remote repositories** and creating a **new repo locally**.

---

## Workflow 1: Working with a Cloned Repository

This is the **typical workflow** for developers joining an existing project.

### Steps:

1. **Clone the repository** (first time only):
```bash
git clone <repo-url>
```
2. **Navigate to project**
```bash
cd project-folder
```
3. **Pull latest changes** (for updates):
   ```bash
   git pull origin main
   ```
4. ** Create a new branch for a feature/bug: **
   ```bash
   git checkout -b feature-login
   ```
5. **Make changes in your local files** 
6. **Stage changes for commit**:
   ```bash
   git add .
   ```
7. **Commit changes locally**:
   ```bash
   git commit -m "Add login feature"
   ```
8. **Push branch to remote**:
  ```bash
     git push -u origin feature-login
```
9. **Open a Pull Request to merge into main.**

---

## 2. Workflow 2: Creating a Local Repository & Pushing to Remote

1. **Create Project Repository** 
```bash
mkdir my-project  
cd my-project
```  

2. **Initialize Git Repository**  
```bash
git init
```

4. **Create a file**  
```bash
touch app.txt
echo "Hello Git" >> app.txt
```

6. **Check Repository status**  
```bash
git status
```

8. **Stage File**  
```bash
git add app.txt
```

10. **Commit Changes**   
```bash
git commit -m "Initial commit"
```  

12. **Create GitHub Repository using CLI** 
```bash
gh repo create my-project --public --source=. --remote=origin
```  

14. **Push local commits to GitHub** 
```bash
git push -u origin main
```  
