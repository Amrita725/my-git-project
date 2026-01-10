# Git Authentication

This document explains the different ways to securely authenticate with GitHub repositories. It covers **Personal Access Tokens (PATs)** and **SSH authentication**, showing how each method works,
when to use them, and why they are preferred over traditional password-based authentication.

---

## Personal Access Token (PAT) 
A Personal Access Token (PAT) is a secure authentication mechanism provided by GitHub that is used instead of a GitHub password for Git operations such as git push and git pull.
Instead of manually generating a PAT from the GitHub UI, the GitHub CLI (gh) was used to authenticate and configure access.  
```
brew install gh
gh auth login
```
During authentication:  
GitHub.com was selected  
HTTPS protocol was chosen  
Authentication was completed via browser login  

---

## SSH Authentication
SSH authentication allows secure access to Git repositories without using passwords.  

### SSH Key Types
- ED25519 : Modern, fast, secure, better performance, more preferred
- RSA : Older, widely supported (requires larger key sizes)

Command:
```
ssh-keygen -t ed25519 -C "email@example.com"  
ssh-keygen -t rsa -b 4096 -C "email@example.com"  
```

---

## When to Use What?

### Use SSH when:
- You are a developer  
- Working from your personal laptop  
- Pushing code frequently  
- Want seamless auth without tokens  

### Use PAT when:
- Using GitHub CLI (gh)  
- Automating workflows  
- Using CI/CD pipelines  
- Working behind restricted firewalls  
