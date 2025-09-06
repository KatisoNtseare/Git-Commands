## Educore LMS – GitHub Branch Workflow Guide (Complete)

> A complete, beginner-friendly but professional Git workflow for the Educore LMS project.
> Use this guide every time you work on the repo.

---

## 📑 Table of Contents

1. Overview: How we work
2. Step-by-step workflow
3. Branching rules & naming conventions
4. Commit message rules
5. Branches I created (backend & frontend)
6. Pull Request (PR) checklist & template
7. Merge & conflict resolution flow
8. Troubleshooting common mistakes
9. Quick reference cheat sheet
10. Example workflows (backend & frontend)

---

## 1) Overview – How We Work

* **`main` branch** → stable, production-ready code.
* **Feature branches (`feature/...`)** → where all development happens.
* Work only in your feature branch, never directly on `main`.
* Always keep your branch up to date with `main` before PR.
* Every change must go through a **Pull Request (PR)** → code review → merge → cleanup.

---

## 2) Step-by-step Workflow (Developer Flow)

### Step 1 — Clone repo (first time only)

```bash
git clone https://github.com/KatisoNtseare/Educore-LMS-Assignment-2.git
cd Educore-LMS-Assignment-2
```

### Step 2 — Update main

```bash
git checkout main
git pull origin main
```

### Step 3 — Create or switch to your feature branch

* If branch exists on GitHub but not locally:

```bash
git checkout -b feature/backend/add-login-api origin/feature/backend/add-login-api
```

* If branch exists locally:

```bash
git checkout feature/backend/add-login-api
```

* If creating a new branch from main:

```bash
git checkout -b feature/backend/my-feature
git push -u origin feature/backend/my-feature
```

### Step 4 — Make changes

* Open project in IDE (Visual Studio, VS Code).
* Implement changes, save files.

### Step 5 — Commit changes

```bash
# Stage everything (new, updated, deleted)
git add -A
git commit -m "Add login API endpoint"
```

### Step 6 — Push branch

```bash
git push origin feature/backend/add-login-api
```

### Step 7 — Keep branch updated

git checkout main
git pull origin main          # Update local main with the latest remote changes
git checkout feature/<branch> # Switch back to your feature branch
git merge main                # Merge the latest main into your feature branch

```bash
git checkout main
git pull origin main
git checkout feature/backend/add-login-api
git merge main
```

### Step 8 — Open Pull Request

* GitHub → New Pull Request
* Base: `main` | Compare: your `feature/...` branch
* Fill in PR template (see section 6)
* Request review

### Step 9 — Merge & cleanup

After approval:

```bash
git checkout main
git pull origin main
git branch -d feature/backend/add-login-api
git push origin --delete feature/backend/add-login-api
```

---

## 3) Branching Rules & Naming Conventions

**General format:**

```
feature/<area>/<short-description>
hotfix/<short-description>
release/<version>
```

Examples:

* `feature/backend/authentication`
* `feature/frontend/dashboard-navigation`
* `hotfix/backend/fix-null-error`

❌ Avoid names like `fix2`, `johns-branch`.

---

## 4) Commit Message Rules

Use **imperative tense** + **clear description**.

Examples:
✅ `Add login API`
✅ `Fix null reference in UserService`
✅ `Update student dashboard UI`
❌ `fixed stuff`
❌ `update code`

---

## 5) Branches I Created (Backend & Frontend)

### Backend Branches

| Feature                                  | Branch Name                              |
| ---------------------------------------- | ---------------------------------------- |
| Role-based authentication                | feature/backend/authentication           |
| Admin: CRUD Users (Students & Lecturers) | feature/backend/admin-user-management    |
| Admin: Courses & Modules                 | feature/backend/course-module-management |
| Lecturer: Task Management                | feature/backend/lecturer-tasks           |
| Student: Task Status Update & Filtering  | feature/backend/student-tasks            |
| Search Functionality                     | feature/backend/search                   |
| Database Migrations                      | feature/backend/migrations               |

### Frontend Branches

| Feature                          | Branch Name                               |
| -------------------------------- | ----------------------------------------- |
| Authentication Pages             | feature/frontend/authentication           |
| Dashboard & Navigation           | feature/frontend/dashboard-navigation     |
| Admin: User Management UI        | feature/frontend/admin-user-management    |
| Courses & Modules UI             | feature/frontend/course-module-management |
| Lecturer: Task Management UI     | feature/frontend/lecturer-tasks           |
| Student: Task Status & Filtering | feature/frontend/student-tasks            |
| Search Functionality             | feature/frontend/search                   |

---

## 6) Pull Request (PR) Checklist & Template

### ✅ PR checklist

* [ ] Branch updated with `main`
* [ ] Tests (if any) pass locally
* [ ] No debug/logging left (`console.log`, `print`)
* [ ] Linting / formatting applied
* [ ] Documentation updated if needed
* [ ] Reviewer requested

### 📝 PR template

```
Title: [Feature] Add login API endpoint

Summary:
- Added login API endpoint for user authentication
- Users receive JWT token after login

Testing:
- Tested with Postman, valid/invalid credentials

Notes:
- Requires DB migration: Add User table

Reviewer Notes:
- Check error handling in AuthController
```

---

## 7) Merge & Conflict Resolution Flow

1. Update main:

```bash
git checkout main
git pull origin main
```

2. Merge into your feature branch:

```bash
git checkout feature/backend/add-login-api
git merge main
```

3. If conflicts:

   * Open conflict files in IDE
   * Fix manually (choose correct code)
   * `git add <file>`
   * `git commit -m "Resolve merge conflict in <file>"`
4. Push branch again:

```bash
git push origin feature/backend/add-login-api
```

5. Create/Update PR → Review → Merge.

---

## 8) Troubleshooting Common Mistakes

* **Accidentally worked on `main`**

  ```bash
  git checkout -b feature/fix-commit
  git push origin feature/fix-commit
  ```
* **Forgot to set upstream for new branch**

  ```bash
  git push -u origin feature/my-branch
  ```
* **Branch already exists locally**

  ```bash
  git checkout feature/my-branch
  ```
* **Undo last commit (keep changes)**

  ```bash
  git reset --soft HEAD~1
  ```

---

## 9) Quick Reference Cheat Sheet

| Action                  | Command                             |
| ----------------------- | ----------------------------------- |
| Clone repo              | `git clone <url>`                   |
| List all branches       | `git branch -a`                     |
| Switch branch           | `git checkout <branch>`             |
| Create new branch       | `git checkout -b <branch>`          |
| Pull updates            | `git pull origin <branch>`          |
| Merge main into feature | `git merge main`                    |
| Stage all changes       | `git add -A`                        |
| Commit                  | `git commit -m "Message"`           |
| Push                    | `git push origin <branch>`          |
| Delete local branch     | `git branch -d <branch>`            |
| Delete remote branch    | `git push origin --delete <branch>` |

---

## 10) Example Workflows

### Backend example

```bash
git checkout main
git pull origin main
git checkout -b feature/backend/student-tasks
# work on code...
git add -A
git commit -m "Implement student task submission"
git push origin feature/backend/student-tasks
```

### Frontend example

```bash
git checkout main
git pull origin main
git checkout -b feature/frontend/dashboard-navigation
# edit React code...
git commit -am "Add sidebar navigation for student dashboard"
git push origin feature/frontend/dashboard-navigation
```

---

## Final Note

This guide is the **official Educore LMS Git workflow**.
Follow it step-by-step. If stuck  run `git status`, check this doc.
