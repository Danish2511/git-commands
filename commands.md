Great, Danish! Let’s dive into Git in a way that’s **clear, practical, and example-rich**—perfect for building a solid understanding. I'll cover all the core Git commands **from A to Z**, explain similar ones with **key differences**, and highlight **best practices** and whether commands are **latest or outdated**.

We’ll go in **sections grouped by purpose** rather than strict A–Z, so you can use Git effectively.

---

## 🔧 1. Git Configuration & Setup

| Command      | Description                                 | Example                                  | Notes                                |
| ------------ | ------------------------------------------- | ---------------------------------------- | ------------------------------------ |
| `git config` | Set Git configurations (user, editor, etc.) | `git config --global user.name "Danish"` | Use `--global` to apply to all repos |
| `git init`   | Start a new Git repository                  | `git init`                               | Initializes `.git` folder            |

---

## 📁 2. Creating & Cloning Repos

| Command     | Description        | Example                                      | Notes                                    |
| ----------- | ------------------ | -------------------------------------------- | ---------------------------------------- |
| `git clone` | Copy a remote repo | `git clone https://github.com/user/repo.git` | Recommended over `init` for remote repos |

---

## 📄 3. File Status & Staging

| Command      | Description            | Example                          | Notes                                     |
| ------------ | ---------------------- | -------------------------------- | ----------------------------------------- |
| `git status` | See current repo state | `git status`                     | Often used to check staged/unstaged files |
| `git add`    | Stage file(s)          | `git add file.txt` / `git add .` | `.` adds all changes                      |
| `git reset`  | Unstage file           | `git reset file.txt`             | Doesn’t delete file, just unstages        |
| `git rm`     | Remove file from repo  | `git rm file.txt`                | Deletes file and stages the deletion      |

---

## 💾 4. Committing Changes

| Command              | Description               | Example                                   | Notes                   |
| -------------------- | ------------------------- | ----------------------------------------- | ----------------------- |
| `git commit -m`      | Save changes with message | `git commit -m "Initial commit"`          | Use meaningful messages |
| `git commit --amend` | Edit last commit          | `git commit --amend -m "Updated message"` | Overwrites last commit  |

---

## 🔄 5. Branching

| Command          | Description              | Example                      | Notes                                |
| ---------------- | ------------------------ | ---------------------------- | ------------------------------------ |
| `git branch`     | List or create branches  | `git branch feature/login`   | `*` shows current branch             |
| `git checkout`   | Switch branch or file    | `git checkout feature/login` | Also used to restore files (old way) |
| `git switch` ✅  | Switch branches (modern) | `git switch main`            | Newer, simpler than `checkout`       |
| `git restore` ✅ | Restore file (modern)    | `git restore file.txt`       | Preferred over `checkout` for files  |

**➡️ `switch` and `restore` are recommended** for clarity over the older `checkout`.

---

## 🔁 6. Merging & Rebasing

| Command           | Description          | Example                    | Notes                             |
| ----------------- | -------------------- | -------------------------- | --------------------------------- |
| `git merge`       | Combine branches     | `git merge feature/login`  | Creates a merge commit            |
| `git rebase`      | Move/Replay commits  | `git rebase main`          | Cleaner history, but riskier      |
| `git cherry-pick` | Copy specific commit | `git cherry-pick <commit>` | Pull one commit to another branch |

**➡️ `merge` is safer for teams. `rebase` is cleaner for solo work.**

---

## 🚀 7. Working with Remotes

| Command      | Description           | Example                     | Notes                           |
| ------------ | --------------------- | --------------------------- | ------------------------------- |
| `git remote` | Manage remote URLs    | `git remote add origin URL` | `origin` is default remote name |
| `git fetch`  | Get changes, no merge | `git fetch origin`          | Safer, manual review            |
| `git pull`   | Get + merge changes   | `git pull origin main`      | `pull = fetch + merge`          |
| `git push`   | Upload commits        | `git push origin main`      | Push local changes to remote    |

---

## 📚 8. Logs, Diffs, History

| Command    | Description           | Example             | Notes                                |
| ---------- | --------------------- | ------------------- | ------------------------------------ |
| `git log`  | Show commit history   | `git log --oneline` | Use `--graph` for visual tree        |
| `git diff` | Show file differences | `git diff`          | Compare working dir vs staged/commit |
| `git show` | Show commit or object | `git show <commit>` | Full info on a commit                |

---

## 🔄 9. Undoing Changes

| Command            | Description              | Example                   | Notes                                 |
| ------------------ | ------------------------ | ------------------------- | ------------------------------------- |
| `git reset --soft` | Keep files, reset commit | `git reset --soft HEAD~1` | Undo commit but keep staged           |
| `git reset --hard` | Discard everything       | `git reset --hard HEAD`   | ⚠️ Dangerous, use carefully           |
| `git revert`       | Reverse a commit safely  | `git revert <commit>`     | Keeps history safe, preferred in team |
| `git clean -fd`    | Remove untracked files   | `git clean -fd`           | Deletes untracked files/dirs          |

---

## 🛠️ 10. Advanced & Useful

| Command      | Description                       | Example                       | Notes                         |
| ------------ | --------------------------------- | ----------------------------- | ----------------------------- |
| `git stash`  | Save uncommitted changes          | `git stash` / `git stash pop` | Useful during switches        |
| `git bisect` | Find bug commit via binary search | `git bisect start`            | Advanced debugging            |
| `git tag`    | Mark commit with version          | `git tag v1.0.0`              | Often used for releases       |
| `git blame`  | See who changed each line         | `git blame file.txt`          | Helpful for debugging history |

---

## 🧠 Summary Tips

- **Use `git status` all the time** to stay aware of your changes.
- Prefer **`switch` and `restore` over `checkout`** for clarity.
- Use **`merge` for team safety**, `rebase` for clean solo histories.
- Always **stash or commit before switching branches**.

---

Would you like a **printable cheat sheet**, or shall we go deep into real **daily Git workflows** (e.g. branching strategies, rebasing flows, undoing mistakes, GitHub PR flow)?

Let me know what’s next!

---

Awesome, Danish! Let’s level up your Git skills by diving into **real-world Git workflows**—things you’ll use daily as a professional developer.

---

## 🚀 1. **Branching Strategy (Feature Branch Workflow)**

### 💡 Why?

Keeps your `main` branch clean and production-ready. Work is done in isolated branches.

### 🔧 Workflow:

```bash
git checkout main
git pull origin main       # Always start with latest code
git checkout -b feature/login-page
```

💬 You now work on your `feature/login-page` branch. When done:

```bash
git add .
git commit -m "Add login page UI"
git push origin feature/login-page
```

👉 Go to GitHub → **Create Pull Request (PR)**

---

## 🔁 2. **Rebasing Before Merging**

Keeps commit history clean and avoids merge commits on small features.

### 🧠 Example:

You branched from `main`, but meanwhile others pushed to `main`.

Before merging:

```bash
git checkout feature/login-page
git pull origin main --rebase
# OR
git fetch origin
git rebase origin/main
```

This replays your commits **on top of latest main**.

Then push:

```bash
git push --force-with-lease   # Needed after rebase
```

➡️ Now your branch is up to date and PR is clean.

---

## 👨‍👩‍👧‍👦 3. **Pull Request (PR) Best Practices**

| Tip                         | Description                                    |
| --------------------------- | ---------------------------------------------- |
| ✅ Small PRs                | Keep PRs focused and under ~300 lines          |
| ✅ Descriptive Title & Body | Explain what and why                           |
| ✅ Self-review              | Run through your code before requesting review |
| ✅ Tag reviewers            | Use `@username` for feedback                   |

---

## 🔄 4. **Undoing Mistakes (Real-life Fixes)**

### ❌ Committed wrong file?

```bash
git reset HEAD^       # Undo commit but keep changes
git restore .         # OR git checkout . (old way)
```

### ❌ Committed secret accidentally?

```bash
git rebase -i HEAD~3   # Reword or drop bad commit
git push --force-with-lease
```

🛑 Never force push to `main` on shared repos.

---

## 🧪 5. **Stashing Work When Switching**

You're midway on a task, and need to switch branches urgently:

```bash
git stash
git switch main
# After your task
git switch feature/login-page
git stash pop
```

---

## 🧹 6. **Cleaning Up Old Local Branches**

After merging a branch on GitHub:

```bash
git branch -d feature/login-page        # Delete local
git fetch -p                            # Remove stale remotes
```

---

## 🧭 7. **Rebasing Flow (Team-friendly)**

When teams prefer linear history:

```bash
# While working:
git checkout -b feature/profile-update
# do work...

# Before merging PR:
git fetch origin
git rebase origin/main
# Resolve conflicts if needed
git push --force-with-lease
```

⚠️ Avoid rebase if branch is already merged or shared with others.

---

## 🛠️ 8. **Hotfix Workflow (e.g., urgent bug in prod)**

```bash
git checkout main
git pull
git checkout -b hotfix/crash-on-login
# fix bug
git commit -am "Fix login crash"
git push origin hotfix/crash-on-login
```

Then create a PR → merge → deploy → delete branch.

---

## 🎯 Pro Tip: Use Aliases for Speed

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.cm "commit -m"
```

Then you can do:

```bash
git co -b new-feature
git st
git cm "Add new feature"
```

---

## 🗺️ Summary Git Workflow Map

```
main  <── develop (optional)
   │
   ├── feature/*
   ├── bugfix/*
   ├── hotfix/*
   └── release/*
```

---

Would you like a **visual Git flow diagram**, or should we move to **collaboration with GitHub (e.g. resolving PR feedback, squash merging, fork-and-clone flow)?**

Let’s build this into a full mastery guide 👨‍💻
