## Git Learning Notes – Understanding Nested Repositories, Rebase, Merge and Submodules
### Scenario

I had a project called

Kubernetes_in_one_shot

Inside it, I had another folder called
```
projects/  
    expense-tracker/  
    full-stack_chatApp/  
```
My goal was to push the entire Kubernetes_in_one_shot folder into a single GitHub repository.

While doing this, I encountered multiple Git issues that helped me understand some very important Git concepts.

### 1. Mistake #1 – Initializing Git Multiple Times (Nested Git Repository)

Initially my folder structure looked something like this:

```
Kubernetes_in_one_shot
│
├── .git
│
└── projects
      │
      ├── .git
      │
      ├── expense-tracker
      │      └── .git
      │
      └── full-stack_chatApp
             └── .git
```
I had accidentally executed

```
git init 
```

inside multiple folders.

For example,

git init

inside

Kubernetes_in_one_shot

and again

git init

inside

/projects

and again inside

/ expense-tracker

Why is this a problem?

Whenever Git finds a .git directory, it assumes

"This folder is a completely independent repository."

That means

expense-tracker

is no longer considered a normal folder.

Instead, Git thinks

expense-tracker

is another project.

Therefore, when I execute

git add .

from the parent repository,

Git does not recursively copy all files.

Instead, it stores a reference to that repository.

Think of it like this
Normal Folder
Kubernetes
      │
      └── expense-tracker
               │
               ├── package.json
               ├── src
               ├── README.md

Everything becomes part of one repository.

Nested Git Repository
Kubernetes
      │
      └── expense-tracker
               │
               └── .git

Git says

"I won't copy all these files."

Instead it stores only

Repository Reference
Result

GitHub showed

expense-tracker →

instead of

expense-tracker/

The arrow icon means

"This is another Git repository."

Not a normal folder.

Correct Structure

If my goal is

One GitHub repository

there should be only one

.git
Kubernetes_in_one_shot
│
├── .git
│
├── docs
├── README.md
│
└── projects
      │
      ├── expense-tracker
      └── full-stack_chatApp

Only the root repository should contain

.git
2. What is a Git Commit?

Git never stores files continuously.

Every time we commit,

Git creates a snapshot.

Example

Commit 1

README

Commit 2

README
docs

Commit 3

README
docs
projects

Git internally stores

Commit A

↓

Commit B

↓

Commit C

This chain is called commit history.

3. Local Repository vs Remote Repository

This was another important concept.

I had

Local

Kubernetes_in_one_shot

GitHub

K8-in-one-shot

The GitHub repository already contained

README.md

docs/

which means GitHub already had one commit.

My local repository had

projects/

but no commits yet.

Git therefore saw

Local

History A

GitHub

History B

These histories had no relationship.

Why Git got confused

Git expects history to look like

Commit A

↓

Commit B

↓

Commit C

Instead it saw

Local

(No commits)

and

Remote

Commit A

There was no common parent.

Git therefore called them

Unrelated Histories

4. git pull --allow-unrelated-histories

Running

git pull origin main --allow-unrelated-histories

tells Git

I know these two repositories started independently.

Merge them anyway.

Without this option Git refuses to merge because it cannot determine how these two repositories are related.

5. Why Git Asked About Rebase

When I ran

git pull

Git responded

Need to specify how to reconcile divergent branches

Initially I didn't understand what this meant.

What are Divergent Branches?

Suppose

GitHub

Commit A

Local

Commit B

Neither contains the other.

Git sees

Commit A

Commit B

Now Git asks

"How should I combine these?"

There are two ways.

Method 1 — Merge

Git creates a new commit.

Commit A
     \
      Merge Commit
     /
Commit B

History becomes

A

 \

  Merge

 /

B

Nothing changes.

Both histories remain intact.

Advantages

Easy

Safe

Never rewrites history

Recommended for beginners.

Method 2 — Rebase

Rebase literally means

"Move my commits on top of another branch."

Instead of

Commit A

Commit B

Git changes history into

Commit A

↓

Commit B

It looks as though

Commit B

was created after

Commit A.

Think of rebase like rewriting history.

Suppose

Remote

A

Local

B

Merge

A

 \

  M

 /

B

Rebase

Git removes

B

temporarily,

puts

A

first,

then recreates

B

on top.

Final history

A

↓

B

Much cleaner.

When should we use Merge?

Use merge when

working in teams
learning Git
preserving history
avoiding accidental history rewrites
When should we use Rebase?

Rebase is commonly used:

before creating Pull Requests
to maintain a clean linear history
while working on feature branches

Example

feature/login

Before merging into

main

developers often do

git rebase main

so the feature branch appears as if it started from the latest version of main.

Important Warning

Rebase rewrites commit history.

Because of that,

never rebase commits that other developers have already pulled.

Otherwise their history and yours will no longer match.

6. Merge Conflicts

A merge conflict occurs when Git cannot automatically decide which change should be kept.

Example

Remote

README

Docker Notes

Local

README

Kubernetes Notes

Now Git asks

Which version should I keep?

It cannot decide.

It therefore creates

<<<<<<< HEAD

Kubernetes Notes

=======

Docker Notes

>>>>>>> origin/main

The developer manually edits the file.

After resolving,

git add .
git commit

Git only reports merge conflicts when

two people modify the same part of the same file.

If different files are modified,

Git merges automatically.

7. Why GitHub Still Showed Arrow Icons

After successfully pushing,

GitHub displayed

expense-tracker →

instead of a normal folder.

Initially I thought

there were still multiple .git folders.

Running

find . -name ".git"

returned

./.git

meaning there was only one repository.

However,

running

git ls-tree -r HEAD

showed

160000 commit projects/expense-tracker
160000 commit projects/full-stack_chatApp

The number

160000

is very important.

It means

Git is storing

a gitlink (submodule reference),

not actual project files.

Normal files appear as

100644 blob README.md

Submodules appear as

160000 commit

That explains why GitHub displayed an arrow instead of the project contents.

Why Did This Happen?

Although I removed the nested .git folders,

Git had already recorded these directories as submodules in its index.

The index still remembered

expense-tracker

as

Another Git repository

instead of

A normal folder.

How It Was Fixed

We removed the incorrect gitlink entries from Git's index (without deleting the local files), then added the folders back as ordinary directories and committed the changes.

After pushing again, GitHub displayed the folders normally and all the project files became browsable.

Key Learnings
Only initialize Git once when the entire directory should be a single repository.
A .git folder makes that directory an independent Git repository.
A Git commit is a snapshot of the repository at a point in time.
Merge preserves both histories by creating a merge commit.
Rebase rewrites commit history to create a clean, linear sequence.
Use --allow-unrelated-histories only when combining repositories that started independently.
A merge conflict occurs when Git cannot automatically determine which changes to keep.
An arrow icon on GitHub usually indicates a submodule (gitlink), not a normal folder.
git ls-tree -r HEAD is an excellent debugging command to verify whether Git is tracking files (100644 blob) or submodules (160000 commit).
