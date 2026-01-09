This repository demonstrates a complete Git workflow starting from a local folder to a remote GitHub repository.  
It is created as a learning, practice, and documentation exercise to showcase Git fundamentals, GitHub CLI usage, and clean documentation practices.

This repository is intentionally simple to focus on **version control concepts** rather than application complexity.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#Objectives
- Initialize a local Git repository  
- Track files using Git  
- Commit changes with meaningful messages  
- Create a GitHub repository using GitHub CLI  
- Push local commits to GitHub  
- Maintain proper documentation using README  

#Prerequisites  
- macOS / Linux  
- Git installed  
- GitHub account  
- GitHub CLI (gh) installed and authenticated  

#Verify Installation  
```
      git --version  
      gh --version   
      gh auth status
```  

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#Step-by-Step  

1. Create Project Repository  
```mkdir my-project```  
```cd my-project```  

2. Initialize Git Repository  
```git init```

3. Create a file  
```touch app.txt```  
```echo "Hello Git" >> app.txt```

4. Check Repository status  
```git status```

5. Stage File  
```git add app.txt```

6. Commit Changes   
```git commit -m "Initial commit"```  

7. Create GitHub Repository using CLI  
```gh repo create my-project --public --source=. --remote=origin```  

8. Push local commits to GitHub 
```git push -u origin main```  
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#Common Command Reference  
```
git status  
git branch  
git checkout -b <branchname>  
git log --oneline  
git diff  
git remote -v  
git push  
git pull
```
