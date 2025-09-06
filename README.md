# Educore LMS – GitHub Branch Workflow Guide (Complete)

> A complete, developer-ready reference for cloning, branching, working, PRs, merging and cleaning up for the Educore LMS project.

---

## Table of contents
1. Step-by-step workflow (Clone → Merge → Cleanup)
2. Branching rules & naming conventions
3. Common cases and commands
4. Pull Request (PR) checklist & template
5. Branches I created (backend & frontend)
6. "When you have a task" — quick action checklist
7. Merge & conflict resolution steps
8. Troubleshooting & tips
9. Quick reference cheat sheet & printable checklist

---

## 1) Step-by-step workflow (developer-friendly)

### Step 1 — Clone the repository (first-time setup)
Cloning downloads a copy of the repository to your local machine.

```bash
git clone https://github.com/KatisoNtseare/Educore-LMS-Assignment-2.git
cd Educore-LMS-Assignment-2
```

> You now have a local copy. Work will be done on feature branches, not `main`.

### Step 2 — Check available branches
```bash
git branch -a
```
- `main` — stable/production-ready code
- `feature/...` — active feature branches

### Step 3 — Create or switch to your feature branch
**Never work on `main`.** Always use a feature branch.

**If branch exists on GitHub but not locally:**
```bash
git checkout -b feature/backend/add-login-api origin/feature/backend/add-login-api
```
- `-b` creates local branch and sets it to track the remote.

**If branch exists locally:**
```bash
git checkout feature/backend/add-login-api
```

**If branch does not exist anywhere and you want to create & push:**
```bash
git checkout -b feature/backend/my-feature
git push -u origin feature/backend/my-feature
```

### Step 4 — Make your changes
- Open backend in Visual Studio or frontend in VS Code.
- Implement code changes, save files.

**NB:** When pushing or pulling, we recommend VS/IDE closed to avoid file locks — but you can still work with Git while editors are open; the note is a team preference to avoid accidental conflicts.

### Step 5 — Stage & commit changes
```bash
git add .
# OR add specific files: git add path/to/file

git commit -m "Add login API endpoint"
```
**Commit message conventions:** use imperative tense and be descriptive: `Add`, `Fix`, `Update`, `Remove`.

### Step 6 — Push your branch to GitHub
```bash
git push origin feature/backend/add-login-api
# OR when creating new branch: git push -u origin feature/backend/my-feature
```

### Step 7 — Pull latest changes before new work
If you're on a feature branch and want updates from main:
```bash
git pull origin main        # from main into current branch (if on main first)
# OR
git pull origin feature/backend/add-login-api  # pull remote updates for your current branch
```

### Step 8 — Create a Pull Request (PR)
1. GitHub → your branch → Pull Request → New Pull Request
2. Base: `main`, Compare: your `feature/...` branch
3. Add description and link relevant issues
4. Request one or more reviewers
5. After approval, **Merge** into `main`

### Step 9 — Clean up after merge
```bash
git checkout main
git pull origin main
git branch -d feature/backend/add-login-api           # delete locally
git push origin --delete feature/backend/add-login-api # delete remote
```

**If you need to keep the branch for further work, do not delete.**

---

## 2) Branching rules & naming conventions
Use clear, consistent names. Examples:
- Feature branches: `feature/{area}/{short-description}`
  - `feature/backend/authentication`
  - `feature/frontend/dashboard-navigation`
- Hotfix / bug: `hotfix/{descr}`
- Release: `release/{version}` (if used)

**Good:** `feature/backend/add-login-api`
**Avoid:** short/ambiguous names like `fix2` or `katiso_branch`

---

## 3) Common Cases (NB cases) — and commands

### Case 1 — Local branch already exists (error on -b)
If you run `git checkout -b feature/...` and see:
```
fatal: A branch named 'feature/backend/add-login-api' already exists.
```
**Solution:** switch to it:
```bash
git checkout feature/backend/add-login-api
```

### Case 2 — Branch exists on GitHub but not locally
```bash
git checkout -b feature/backend/add-login-api origin/feature/backend/add-login-api
```
This creates the local branch and sets it to track the remote branch.

### Case 3 — Branch exists both locally and on GitHub
```bash
git checkout feature/backend/add-login-api
git pull origin feature/backend/add-login-api
```

### In all cases
- **Don’t create a local branch if it already exists remotely.**
- If branch exists on remote but not locally, use `git checkout -b <branch> origin/<branch>`.
- Always `git pull` before starting work to avoid conflicts.

---

## 4) Pull Request (PR) checklist & template
Use a PR template for fast reviews.

**PR checklist:**
- [ ] Branch is up-to-date with `main` (merged locally)
- [ ] Tests (if any) pass locally
- [ ] No debug/logging statements left
- [ ] Run linting / formatters
- [ ] Add or update documentation or README if needed
- [ ] Request reviewer(s)

**Suggested PR description template:**
```
Title: [Feature] Add login API endpoint

Summary:
- What: Add login API endpoint for user authentication
- Why: Allow students/lecturers to login and receive JWT
- How: New controller, service, DB migration

Testing:
- How I tested locally
- Any unit tests added

Notes:
- Any manual steps or migrations required

Reviewer notes:
- Areas to focus on during review
```

---

## 5) Branches I created (backend & frontend)

### Backend branches
| Feature | Branch Name |
|---|---|
| Role-based authentication | feature/backend/authentication |
| Admin: CRUD Users (Students & Lecturers) | feature/backend/admin-user-management |
| Admin: Courses & Modules | feature/backend/course-module-management |
| Lecturer: Task Management | feature/backend/lecturer-tasks |
| Student: Task Status Update & Filtering | feature/backend/student-tasks |
| Search Functionality | feature/backend/search |
| Database Migrations | feature/backend/migrations |

### Frontend branches
| Feature | Branch Name |
|---|---|
| Authentication Pages | feature/frontend/authentication |
| Dashboard & Navigation | feature/frontend/dashboard-navigation |
| Admin: User Management UI | feature/frontend/admin-user-management |
| Courses & Modules UI | feature/frontend/course-module-management |
| Lecturer: Task Management UI | feature/frontend/lecturer-tasks |
| Student: Task Status & Filtering | feature/frontend/student-tasks |
| Search Functionality | feature/frontend/search |

---

## 6) To do when you have a task (step-by-step)
1. Make sure you're on the correct branch
   - `git status` — shows current branch and staged changes
   - `git checkout feature/backend/<branch-name>`
   - OR if the branch exists on GitHub but not locally:
     `git checkout -b feature/backend/<branch-name> origin/feature/backend/<branch-name>`
2. Pull latest changes from GitHub for your branch
   - `git pull origin feature/backend/<branch-name>`
3. Pull latest changes from `main` and merge into your branch
   - `git checkout main`
   - `git pull origin main`
   - `git checkout feature/backend/<branch-name>`
   - `git merge main`
4. Resolve conflicts (if any)
   - Edit conflicting files
   - `git add <file>` for resolved files
   - `git commit -m "Resolve conflict: <file>"
5. Push updates after merging
   - `git push origin feature/backend/<branch-name>`

---

## 7) Merge & conflict resolution — full flow
**Before merging to main on GitHub:**
1. Ensure your feature branch is up to date with `main` locally:
   ```bash
   git checkout main
   git pull origin main
   git checkout feature/backend/<branch-name>
   git merge main
   ```
2. Resolve merge conflicts:
   - Open conflict file(s), fix the conflicting code
   - `git add <file>`
   - `git commit -m "Resolve merge conflicts before PR"
   ```
3. Push the resolved branch:
   ```bash
   git push origin feature/backend/<branch-name>
   ```
4. Open PR on GitHub (Reviewer will confirm, approve, then merge)

**After merging on GitHub:**
```bash
git checkout main
git pull origin main
# Delete branch locally and remotely
git branch -d feature/backend/<branch-name>
git push origin --delete feature/backend/<branch-name>
```

**If you are allowed to merge locally into main (only when agreed):**
```bash
git checkout main
git pull origin main
git merge feature/backend/<branch-name>
git push origin main
```
> Only do the above when the team agreed—otherwise use PRs on GitHub.

---

## 8) Troubleshooting & tips
- **`git status` is your friend** — use it frequently.
- If you accidentally committed to `main` and pushed:
  - Prefer `git revert <commit>` to undo a commit safely.
  - **Do not** force-push to `main` unless the team explicitly agrees.
- If `git checkout -b` fails: switch instead: `git checkout <branch>`.
- To set upstream for local branch:
  ```bash
  git push -u origin feature/backend/<branch-name>
  ```
- To rename a local branch:
  ```bash
  git branch -m old-name new-name
  git push origin :old-name new-name
  git push -u origin new-name
  ```
- If you see merge conflicts after merging main:
  - Resolve in IDE/editor, `git add`, `git commit`, `git push`.

**Why close VS when pulling/pushing?**
- Sometimes IDEs lock files or auto-restore state that conflicts with Git operations; closing reduces chance of locked files and accidental commits. If you prefer to keep it open, just be mindful of any auto-save/format-on-save hooks.

---

## 9) Quick reference cheat sheet & printable checklist

### Action → Command
| Action | Command |
|---|---|
| Check branch | `git status` |
| List local branches | `git branch` |
| List local & remote | `git branch -a` |
| Switch to branch | `git checkout <branch>` |
| Create & track remote branch | `git checkout -b <branch> origin/<branch>` |
| Create new local branch & push | `git checkout -b <branch>` → `git push -u origin <branch>` |
| Pull remote for current branch | `git pull origin <branch>` |
| Pull main | `git pull origin main` |
| Merge main into feature | `git checkout <branch>` → `git merge main` |
| Stage changes | `git add .` or `git add <file>` |
| Commit changes | `git commit -m "Message"` |
| Push branch | `git push origin <branch>` |
| Delete local branch | `git branch -d <branch>` |
| Delete remote branch | `git push origin --delete <branch>` |

### Printable checklist — before opening PR
- [ ] Branch name follows convention
- [ ] Branch up-to-date with `main`
- [ ] Unit tests pass (if any)
- [ ] No debug logs
- [ ] Linting passed
- [ ] PR description is clear
- [ ] Reviewer requested

---

## Appendix — small useful examples
**Set branch to track remote after creating it locally:**
```bash
git push -u origin feature/backend/my-feature
```

**Revert a bad commit (safe):**
```bash
git revert <commit-hash>
# Creates a new commit which undoes the changes in <commit-hash>
```

**Force push (DANGEROUS — avoid unless agreed):**
```bash
git push --force origin <branch>
```

---

### Final note
This document consolidates the entire workflow you supplied plus practical additions: branch naming, PR template, commit message guidance, conflict resolution, and a cheat sheet to hand to new teammates. Use this as the canonical workflow for Educore LMS.

> If you'd like, I can:
> - export this to PDF for sharing,
> - produce a one-page flow diagram for onboarding,
> - or convert this into a `CONTRIBUTING.md` for the repo.


---

*Document last updated: Sep 6, 2025*

