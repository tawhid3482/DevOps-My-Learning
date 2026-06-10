# 🚀 Git Mastery Roadmap (Interview Ready)

> **লক্ষ্য:** Git এর মৌলিক ধারণা থেকে interview-ready advanced topics — সব এক জায়গায়।  
> ভাষা: বাংলা + English (interview lines)

---

## 📑 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Version Control System (VCS)](#-1-version-control-system-vcs--basic-concept) |
| 2 | [Git Branching](#-2-git-branching-very-important) |
| 3 | [Repository Roles](#-3-repository-roles-github--gitlab) |
| 4 | [Branch Protection](#-4-branch-protection-security) |
| 5 | [Forking Workflow](#-5-forking-workflow-open-source-এ-ব্যবহার-হয়) |
| 6 | [Origin vs Upstream](#-6-origin-vs-upstream-খুব-গুরুত্বপূর্ণ) |
| 7 | [Pull Request (PR)](#-7-pull-request-pr-কী) |
| 8 | [Advanced Git](#-8-advanced-git-interview-booster) |
| 9 | [Conflict Resolution](#-9-conflict-resolution-খুব-common-interview-topic) |
| 10 | [`.gitignore` & Best Practices](#-10-gitignore--best-practices) |
| 11 | [Most Important Commands](#-11-git-most-important-commands-full-explanation-in-bangla) |
| 12 | [Quick Cheat Sheet](#-12-quick-cheat-sheet) |

---

## 🧠 1. Version Control System (VCS) – Basic Concept

### ❓ Git কী?

**Git** হলো একটি **Distributed Version Control System (DVCS)**।

| বৈশিষ্ট্য | ব্যাখ্যা |
|----------|---------|
| Distributed | প্রতিটা developer এর কাছে পুরো project history থাকে |
| Offline | ইন্টারনেট ছাড়াই কাজ করা যায় |
| Tracking | সব changes track ও compare করা যায় |

### 🔥 Git vs Other VCS

| Feature | Git | SVN (Other VCS) |
|---------|-----|-----------------|
| Type | Distributed | Centralized |
| Speed | Fast | Slow |
| Offline work | ✅ Yes | ❌ No |
| Branching | Lightweight | Heavy |

> **📌 Interview line:**  
> *"Git is a distributed version control system that allows multiple developers to work on the same project efficiently with full history tracking."*

---

## 🌿 2. Git Branching (Very Important)

### 🧩 Branch কী?

**Branch** = আলাদা development line

| Branch | উদ্দেশ্য |
|--------|---------|
| `main` / `master` | Production code |
| `develop` | Development code |
| `feature/*` | নতুন feature |
| `hotfix/*` | জরুরি bug fix |

### 🔥 Basic Commands

```bash
git branch                          # সব branch দেখা
git checkout -b feature/login       # নতুন branch + switch
git merge feature/login             # branch merge
git branch -d feature/login         # branch delete
```

### 🧠 Branching Strategy (Interview Favorite)

**Git Flow:**

```
main
 ├── develop
 │     ├── feature/login
 │     ├── feature/payment
 │
 └── hotfix/bug-fix
```

> **📌 Interview line:**  
> *"We use feature branching strategy where each feature is developed in a separate branch and merged via pull request."*

---

### 🔄 Main → Feature Branch Sync (দুইটা Safe Method)

#### ✅ Method 1 (Recommended): Merge করে নেওয়া

```bash
git checkout feature
git merge main
```

| Step | কী হয় |
|------|--------|
| 1 | তুমি `feature` branch-এ চলে যাও |
| 2 | `main` এর সব changes `feature`-এ merge হয়ে যায় |

> **Best practice:** *"We use `git merge main` into feature branch to sync latest changes safely without losing history."*

#### ✅ Method 2: Direct reset (exact copy)

```bash
git checkout feature
git reset --hard main
```

| ⚠️ সতর্কতা | |
|------------|--|
| Feature branch পুরোপুরি `main` এর মতো হয়ে যায় | |
| পুরানো changes delete হতে পারে | **Risky** |

#### ✅ Method 3: Remote থাকলে force exact sync

```bash
git checkout feature
git reset --hard origin/main
```

| Method | কখন ব্যবহার |
|--------|------------|
| `git merge main` | ✅ Safe — সাধারণত এটাই |
| `git reset --hard main` | Exact copy দরকার হলে (local only) |

---

## 🏢 3. Repository Roles (GitHub / GitLab)

Git এ সবাই এক রকম access পায় না — **Role-based access control (RBAC)**।

| Role | Permissions |
|------|-------------|
| **Owner** | সব কিছু control, repo delete |
| **Admin** | Settings manage, users add/remove |
| **Maintainer** | PR merge, branch manage |
| **Developer** | Code push, PR open |
| **Viewer** | শুধু code দেখা |

> **📌 Interview line:**  
> *"Role-based access control ব্যবহার করা হয় যাতে production code নিরাপদ থাকে।"*

---

## 🚫 4. Branch Protection (Security)

Production branch (`main`) কে protect করা খুব important।

### 🔒 কী কী restrict করা যায়?

- ❌ Direct push বন্ধ
- ❌ Force push বন্ধ
- ❌ Branch delete বন্ধ
- ✅ PR ছাড়া merge না করা
- ✅ CI/CD pass না হলে merge না করা
- ✅ Minimum reviewer approval

> **📌 Interview line:**  
> *"Branch protection rules ব্যবহার করা হয় যাতে কেউ ভুল করে production code নষ্ট করতে না পারে।"*

---

## 🔀 5. Forking Workflow (Open Source এ ব্যবহার হয়)

### 🧠 Fork মানে কী?

**Fork** = অন্যের repo এর একটা copy নিজের account এ নেওয়া।

### 🔥 Flow

```
1. Repo fork করো
2. নিজের machine এ clone করো
3. নতুন branch বানাও
4. কাজ করো → push করো
5. Pull Request দাও
```

### 🔧 Commands

```bash
git clone https://github.com/your-username/repo.git
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git merge upstream/main
```

> **📌 Interview line:**  
> *"Forking workflow open-source contribution এ ব্যবহার হয়, যেখানে developer নিজের copy তে কাজ করে এবং পরে PR দেয়।"*

---

## 🌐 6. Origin vs Upstream (খুব গুরুত্বপূর্ণ)

| নাম | মানে |
|-----|------|
| `origin` | তোমার repo (fork বা own) |
| `upstream` | Original repo (source) |

```bash
git remote -v
git remote add upstream <original-repo-url>
git fetch upstream
git merge upstream/main
```

> **📌 Interview line:**  
> *"Upstream ব্যবহার করা হয় original repository এর সাথে sync রাখার জন্য।"*

---

## 🔁 7. Pull Request (PR) কী?

**PR** = তোমার code অন্যরা review করে `main` branch এ merge করবে।

### 🔥 PR Flow

```
নতুন branch → code লিখো → push → PR তৈরি → review → approve → merge
```

### ✅ ভালো PR এর বৈশিষ্ট্য

| Rule | কারণ |
|------|-------|
| ছোট রাখো | Review সহজ হয় |
| Clear description | Reviewer বুঝতে পারে |
| Bug/feature mention | Context clear থাকে |
| Screenshots (UI change হলে) | Visual verification |

> **📌 Interview line:**  
> *"Pull request code review এর মাধ্যমে quality maintain করে এবং team collaboration সহজ করে।"*

---

## 💣 8. Advanced Git (Interview Booster)

### merge vs rebase

| Command | History | Use case |
|---------|---------|----------|
| **merge** | সব history থাকে (merge commit) | Team/shared branches |
| **rebase** | Clean linear history | Local feature branch cleanup |

```bash
git merge feature/login      # merge commit তৈরি
git rebase main              # commits replay করে linear history
```

### reset vs revert

| Command | কী করে | Safety |
|---------|--------|--------|
| **reset** | History change/delete | ⚠️ Dangerous (shared branch এ না) |
| **revert** | নতুন commit দিয়ে undo | ✅ Safe for team |

```bash
git reset --hard HEAD~1      # last commit remove (local only!)
git revert <commit-id>       # safe undo
```

### ⚠️ Force push

```bash
git push --force   # বা git push --force-with-lease (safer)
```

> History overwrite হয় — shared/production branch এ **কখনো না**।

### 🏷️ git tag (Release versioning)

```bash
git tag v1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin v1.0.0
git push origin --tags
```

### 🍒 git cherry-pick

```bash
git cherry-pick <commit-hash>   # specific commit অন্য branch এ নেওয়া
```

---

## ⚔️ 9. Conflict Resolution (খুব Common Interview Topic)

Merge বা rebase এর সময় একই file এর একই line এ দুইজন change করলে **conflict** হয়।

### 🔧 Conflict solve করার steps

```bash
# 1. Conflict দেখো
git status

# 2. File খুলে marker গুলো ঠিক করো
<<<<<<< HEAD
তোমার code
=======
অন্যের code
>>>>>>> feature/login

# 3. Marker remove করে final code রাখো, তারপর:
git add <resolved-file>
git commit -m "resolve merge conflict"
```

> **📌 Interview line:**  
> *"I resolve conflicts by reviewing both changes, keeping the correct logic, removing conflict markers, staging, and committing."*

---

## 📁 10. `.gitignore` & Best Practices

### `.gitignore` কী?

Git কে বলে কোন file/folder **track করবে না**।

```gitignore
# Dependencies
node_modules/
vendor/

# Environment & secrets
.env
.env.local
*.pem
credentials.json

# Build output
dist/
build/
*.log

# OS files
.DS_Store
Thumbs.db
```

### ✅ Commit Message Best Practice (Conventional Commits)

```
feat: add user login
fix: resolve payment timeout
docs: update API readme
chore: upgrade dependencies
refactor: simplify auth middleware
```

| Prefix | মানে |
|--------|------|
| `feat` | নতুন feature |
| `fix` | bug fix |
| `docs` | documentation |
| `chore` | maintenance |
| `refactor` | code restructure |

---

## 🚀 11. Git Most Important Commands (Full Explanation in Bangla)

---

### 🧠 1. `git init`

```bash
git init
```

| | |
|--|--|
| **কী কাজ করে** | নতুন Git repository তৈরি করে |
| **বিস্তারিত** | Folder কে tracking এ নেয়, `.git` hidden folder তৈরি হয় |
| **Use case** | নতুন project শুরু |

---

### 📥 2. `git clone`

```bash
git clone https://github.com/user/project.git
```

| | |
|--|--|
| **কী কাজ করে** | Remote repo থেকে পুরো code + history copy |
| **Use case** | Existing project local এ আনা |

---

### 📊 3. `git status`

```bash
git status
```

| | |
|--|--|
| **কী কাজ করে** | Working directory ও staging area এর অবস্থা |
| **দেখায়** | Changed files, staged files, uncommitted files |

> **📌 Interview line:** *"It shows the current state of working directory and staging area."*

---

### ➕ 4. `git add`

```bash
git add index.js    # specific file
git add .           # সব file
```

| | |
|--|--|
| **কী কাজ করে** | File কে staging area তে পাঠায় |
| **মানে** | "এই file commit করার জন্য ready" |

---

### 💾 5. `git commit`

```bash
git commit -m "add login feature"
```

| | |
|--|--|
| **কী কাজ করে** | Staged changes history তে save |
| **মানে** | Project এর একটা snapshot/version |

> **📌 Interview line:** *"Commit is a snapshot of project at a specific time."*

---

### 🚀 6. `git push`

```bash
git push origin main
git push origin feature/login
```

| | |
|--|--|
| **কী কাজ করে** | Local commits remote (GitHub) এ upload |

---

### 📥 7. `git pull`

```bash
git pull origin main
```

| | |
|--|--|
| **কী কাজ করে** | `git fetch` + `git merge` একসাথে |
| **Use case** | Team project এ latest update নেওয়া |

---

### 🔄 8. `git fetch`

```bash
git fetch
```

| fetch | pull |
|-------|------|
| শুধু data আনে | data আনে + merge করে |
| Safe preview | Direct update |

---

### 🌿 9. `git branch`

```bash
git branch              # list
git branch -a           # সব (remote সহ)
```

---

### 🌱 10. `git checkout` / `git switch`

```bash
git checkout branch-name    # switch (legacy)
git switch branch-name      # switch (modern)
```

---

### 🌿 11. `git checkout -b` / `git switch -c`

```bash
git checkout -b feature/login
git switch -c feature/login   # modern equivalent
```

---

### 🔀 12. `git merge`

```bash
git merge feature/login
```

| | |
|--|--|
| **কী কাজ করে** | এক branch এর code অন্য branch এ যুক্ত |

---

### ❌ 13. `git branch -d`

```bash
git branch -d feature/login     # merged branch delete
git branch -D feature/login     # force delete
```

---

### 🌍 14. `git remote`

```bash
git remote -v
```

Connected remote repositories দেখায়।

---

### 🔗 15. `git remote add`

```bash
git remote add origin <url>
```

Local project কে remote repo এর সাথে connect করে।

---

### 📝 16. `git diff`

```bash
git diff                  # unstaged changes
git diff --staged         # staged changes
git diff main feature     # দুই branch এর পার্থক্য
```

> Interview এ খুব common — changes review করার জন্য।

---

### ⚠️ 17. `git reset`

```bash
git reset --soft HEAD~1     # commit undo, changes staged থাকে
git reset --mixed HEAD~1    # commit undo, changes unstaged
git reset --hard HEAD~1     # সব delete (⚠️ dangerous)
```

---

### 🔁 18. `git revert`

```bash
git revert <commit-id>
```

| | |
|--|--|
| **কী কাজ করে** | নতুন commit দিয়ে safe undo |
| **Use case** | Production / shared branch |

---

### 🧠 19. `git log`

```bash
git log
git log --oneline --graph --all    # visual history
git log -5                         # last 5 commits
```

---

### 🔥 20. `git stash`

```bash
git stash           # কাজ temporary save
git stash list      # সব stash দেখা
git stash pop       # ফিরিয়ে আনা
git stash apply     # pop ছাড়াই apply
```

| | |
|--|--|
| **Use case** | Incomplete কাজ রেখে branch switch |

---

## 📋 12. Quick Cheat Sheet

### Daily Workflow

```bash
git pull origin main
git checkout -b feature/my-task
# ... কাজ করো ...
git add .
git commit -m "feat: describe your change"
git push origin feature/my-task
# → GitHub/GitLab এ PR খোলো
```

### Three Areas of Git

```
Working Directory  →  Staging Area  →  Repository
     (edit)      →   git add      →   git commit
```

### Golden Rules

| Rule | কারণ |
|------|-------|
| `main`-এ সরাসরি push করো না | Branch protection |
| Shared branch এ `reset --hard` করো না | Team history নষ্ট হয় |
| Secret `.env` commit করো না | Security risk |
| ছোট, focused commit রাখো | Debug ও review সহজ |
| PR merge করার আগে `git pull` করো | Conflict কম হয় |

---

<p align="center">
  <strong>Happy Learning! 🎯</strong><br>
  <em>Practice করো → Interview crack করো</em>
</p>
