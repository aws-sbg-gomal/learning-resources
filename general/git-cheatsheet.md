# Git Cheat Sheet

Quick reference for commonly used Git commands. For the full workflow used in this organization, see the [Git Workflow Guide](../onboarding/git-workflow-guide.md).

---

## Setup

```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Check your configuration
git config --list
```

---

## Repository

```bash
# Clone a repository
git clone https://github.com/aws-gomal-university/<repo>.git

# Initialize a new repo
git init

# View remote URLs
git remote -v
```

---

## Branching

```bash
# List all branches
git branch -a

# Create and switch to a new branch
git checkout -b feature/your-branch-name

# Switch to an existing branch
git checkout branch-name

# Delete a local branch
git branch -d branch-name

# Delete a remote branch
git push origin --delete branch-name
```

---

## Staging and Committing

```bash
# Check status
git status

# Stage specific files (preferred)
git add path/to/file

# Stage all changes in a folder
git add projects/your-project/

# Commit with a message
git commit -m "feat: add S3 bucket configuration"

# Amend the last commit message (unpushed only)
git commit --amend -m "feat: corrected S3 bucket configuration"
```

---

## Syncing

```bash
# Fetch changes without merging
git fetch origin

# Pull latest changes into current branch
git pull origin branch-name

# Push current branch to remote
git push origin feature/your-branch-name

# Set upstream on first push
git push -u origin feature/your-branch-name
```

---

## Rebasing

```bash
# Rebase your branch onto dev
git rebase dev

# Continue after resolving conflicts
git rebase --continue

# Abort a rebase
git rebase --abort

# Push after rebase (safer than --force)
git push --force-with-lease origin feature/your-branch-name
```

---

## Stashing

```bash
# Stash current changes
git stash

# List stashes
git stash list

# Apply the most recent stash
git stash pop

# Apply a specific stash
git stash apply stash@{2}

# Drop a stash
git stash drop stash@{0}
```

---

## Viewing History

```bash
# Compact one-line log
git log --oneline

# Log with branch graph
git log --oneline --graph --all

# View changes in a specific commit
git show <commit-hash>

# View differences between branches
git diff main..feature/your-branch
```

---

## Undoing Changes

```bash
# Discard unstaged changes in a file
git checkout -- path/to/file

# Unstage a file (keep changes)
git reset HEAD path/to/file

# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset --mixed HEAD~1

# Revert a pushed commit (safe, creates new commit)
git revert <commit-hash>
```

---

## Tagging

```bash
# Create an annotated tag
git tag -a v1.0.0 -m "Release v1.0.0"

# Push tags to remote
git push origin --tags

# List tags
git tag
```
