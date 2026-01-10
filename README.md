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

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#Basic Term Explanation

```
What is a Personal Access Token (PAT) ?
A Personal Access Token (PAT) is a secure authentication mechanism provided by GitHub that is used instead of a GitHub password for Git operations such as git push and git pull.
Instead of manually generating a PAT from the GitHub UI, the GitHub CLI (gh) was used to authenticate and configure access.
brew install gh
gh auth login
During authentication:

GitHub.com was selected

HTTPS protocol was chosen

Authentication was completed via browser login

What is a Remote URL in Git?
A remote URL tells your local Git repository:  
“Where should I push my code?”  
“From where should I pull updates?”
So,  
Local repo → your laptop  
Remote repo → GitHub  

What is origin in Git?
It is not a command, not a branch, not a server — just a label. origin is the default name given to a remote repository.

git remote -v  
It shows which REMOTE repositories your local repo is connected to.  
Output  
origin  https://github.com/amritasingh/abc.git (fetch)  
origin  https://github.com/amritasingh/abc.git (push)  

Meaning:  
Your local git folder is connected to a remote repo on GitHub  
The nickname for that remote is origin  

- git push -u origin main  
origin is basically my remote repo, and main is the main branch.
So,  
“origin is the default remote alias that points to the GitHub repository.
When we run git push origin main, we are pushing the local main branch to the main branch of the remote repository.”

```
