🚀 Git Mastery Roadmap (Interview Ready)
🧠 1. Version Control System (VCS) – Basic Concept
❓ Git কী?

Git হলো একটি Distributed Version Control System (DVCS)

👉 মানে:

প্রতিটা developer এর কাছে পুরো project history থাকে
offline কাজ করা যায়
changes track করা যায়
🔥 Git vs Other VCS
Feature	Git	SVN (Other VCS)
Type	Distributed	Centralized
Speed	Fast	Slow
Offline work	Yes	No
Branching	Lightweight	Heavy

📌 Interview line:

Git is a distributed version control system that allows multiple developers to work on the same project efficiently with full history tracking.

🌿 2. Git Branching (Very Important)
🧩 Branch কী?

Branch = আলাদা development line

Common branches:
main / master → production code
develop → development code
feature/* → new feature
hotfix/* → urgent bug fix
🔥 Basic Commands:
git branch
git checkout -b feature/login
git merge feature/login
git branch -d feature/login
🧠 Branching Strategy (Interview Favorite)
Git Flow:
main
 ├── develop
 │     ├── feature/login
 │     ├── feature/payment
 │
 └── hotfix/bug-fix

📌 Interview line:

We use feature branching strategy where each feature is developed in a separate branch and merged via pull request.