# Git Workflow Guide

This guide covers the Git conventions and workflow used across all repositories in the AWS SBG Gomal University organization. Follow this process for every contribution.

---

## Branch Structure

Every track repository uses three branch types:

| Branch | Purpose | Direct commits allowed? |
|---|---|---|
| `main` | Always stable and deployable | No |
| `dev` | Active integration branch | No |
| `feature/<short-description>` | Your working branch | Yes |

All work happens on a `feature/` branch. Changes are merged into `dev` via pull request, and `dev` is merged into `main` by a maintainer after review.

---

## Step-by-Step Workflow

### 1. Clone the track repository

```bash
git clone https://github.com/aws-gomal-university/<track-repo>.git
cd <track-repo>
```

### 2. Create your feature branch from `dev`

Always branch from `dev`, not `main`:

```bash
git checkout dev
git pull origin dev
git checkout -b feature/your-feature-name
```

Use descriptive branch names:

```
feature/serverless-cost-dashboard
feature/resume-screening-bot
feature/fix-lambda-timeout
```

### 3. Make your changes

Work within your project folder under `projects/`. Do not modify files outside your folder unless you are a maintainer.

### 4. Stage and commit your changes

Stage specific files rather than using `git add .`:

```bash
git add projects/your-project-folder/
git commit -m "feat: add initial Lambda function and S3 trigger"
```

### 5. Push your branch

```bash
git push -u origin feature/your-feature-name
```

### 6. Open a pull request

Go to the repository on GitHub and open a pull request from your `feature/` branch into `dev`. Fill in the pull request template completely.

---

## Commit Message Standards

This organization follows the [Conventional Commits](https://www.conventionalcommits.org/) specification. Every commit message must follow this format:

```
<type>: <short description>
```

| Type | When to use |
|---|---|
| `feat` | Adding a new feature or project |
| `fix` | Fixing a bug |
| `docs` | Documentation changes only |
| `chore` | Maintenance tasks, dependency updates, config changes |
| `refactor` | Code restructuring without changing behavior |
| `test` | Adding or updating tests |
| `ci` | Changes to CI/CD pipeline configuration |

**Good examples:**

```
feat: add S3 lifecycle policy for cost optimization
fix: resolve Lambda cold-start timeout issue
docs: update architecture diagram for VPC setup
chore: update .gitignore to exclude CDK output
```

**Bad examples:**

```
update files
fixed it
WIP
misc changes
```

Rules:
- Use the imperative present tense: "add" not "added", "fix" not "fixed"
- Keep the subject line under 72 characters
- Do not end the subject line with a period

---

## Keeping Your Branch Up to Date

If `dev` has been updated while you are working, sync your branch before opening a PR:

```bash
git checkout dev
git pull origin dev
git checkout feature/your-feature-name
git rebase dev
```

Resolve any conflicts, then continue:

```bash
git rebase --continue
git push --force-with-lease origin feature/your-feature-name
```

> Use `--force-with-lease` instead of `--force`. It is safer and prevents overwriting others' changes.

---

## Pull Request Rules

- Every PR must reference its issue: `Closes #<issue-number>`
- At least one reviewer approval is required before merging
- PRs must be scoped to a single feature, fix, or task
- Do not merge your own PR without a reviewer approval
- Resolve all review comments before requesting a re-review

---

## Common Commands Reference

| Task | Command |
|---|---|
| Check current branch | `git branch` |
| Check status of changes | `git status` |
| View commit history | `git log --oneline` |
| Discard unstaged changes | `git checkout -- <file>` |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |
| View differences | `git diff` |
| Stash work in progress | `git stash` |
| Apply stashed changes | `git stash pop` |
