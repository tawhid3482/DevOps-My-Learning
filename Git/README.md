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


🌿 তুমি যদি main branch-এর সব কিছু feature branch-এ নিতে চাও, তাহলে সবচেয়ে সহজ উপায় হলো merge বা checkout + reset। নিচে দুইটা safe method 👇

✅ Method 1 (Recommended): Merge করে নেওয়া

এটা সবচেয়ে safe way

git checkout feature
git merge main

👉 এর মানে:

তুমি feature branch-এ চলে গেলে
তারপর main এর সব changes feature এ merge হয়ে যাবে
✅ Method 2: Direct reset (exact copy করতে চাইলে)

যদি তুমি চাও feature একদম main এর মতো হয়ে যাক (সব history সহ):

git checkout feature
git reset --hard main

👉 এটা করলে:

feature branch পুরোপুরি main এর মতো হয়ে যাবে
পুরানো changes থাকলে delete হয়ে যাবে (⚠️ risky)
✅ Method 3: Force exact sync (remote থাকলে)
git checkout feature
git reset --hard origin/main
🔥 Best Practice (Interview friendly answer)

👉 সাধারণত বলা হয়:

“We use git merge main into feature branch to sync latest changes safely without losing history.”

⚡ Quick Summary
Safe: git merge main
Exact copy: git reset --hard main