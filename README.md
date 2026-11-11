# Git Basics Demo

A tiny Python program to practice the basic Git workflow.

## Run the program

From this folder, run:

```powershell
python hello.py
```

## What was done to create this local repository

The demo folder was created inside the workspace, a Python file and this README
were added, and Git was initialized with `main` as the default branch. The first
commit contains both files.

To repeat these steps for a new project:

```powershell
mkdir my-project
cd my-project
git init -b main
```

Create your project files, then save the first version:

```powershell
git status
git add .
git commit -m "Initial commit"
```

`git status` shows which files are new or changed. `git add .` stages all files
in the current folder. `git commit` saves the staged snapshot in your local
repository.

## Connect this repository to GitHub

1. Sign in to GitHub and create a **new, empty** repository (for example,
   `git-basics-demo`). Do not initialize it with a README, license, or
   `.gitignore`; this local repository already has a commit.
2. Copy the repository's HTTPS URL, then run this from this folder, replacing
   `<USERNAME>` with your GitHub username:

   ```powershell
   git remote add origin https://github.com/<USERNAME>/git-basics-demo.git
   git remote -v
   git push -u origin main
   ```

`origin` is the conventional name for the remote GitHub repository. The first
push publishes the local `main` branch and sets its upstream, so later you can
usually use `git push` and `git pull`.

## Everyday commands

```powershell
git status                    # See current changes
git diff                      # Inspect unstaged edits
git add hello.py              # Stage a specific file
git commit -m "Update greeting" # Save staged changes locally
git log --oneline             # View recent commits
git pull                      # Bring down remote changes
git push                      # Publish local commits
```

If GitHub asks you to authenticate, follow its browser or credential-manager
prompt. Do not put a password or access token in the remote URL or commit it to
the project.
