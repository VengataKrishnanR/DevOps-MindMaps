# 🧠 Git Learning Mind Map

## 🔹 1. Git Basics
- Git is a distributed version control system
- Tracks changes to files in a project over time
- Allows multiple developers to collaborate

---

## 🔹 2. Common Git Commands

### ✅ Repository Setup
- Initialize new repo:
  ```bash
  git init
  ```
- Clone remote repo:
  ```bash
  git clone <repo-url>
  ```

### ✅ Tracking Changes
- Check status:
  ```bash
  git status
  ```
- Add files to staging:
  ```bash
  git add <file>
  git add .
  ```
- Commit changes:
  ```bash
  git commit -m "your message"
  ```

### ✅ Remote Management
- Add remote origin:
  ```bash
  git remote add origin <repo-url>
  ```
- Push to remote:
  ```bash
  git push -u origin main
  ```
- Pull latest changes:
  ```bash
  git pull origin main
  ```

---

## 🔹 3. Branching
- Create branch:
  ```bash
  git branch <branch-name>
  ```
- Switch branch:
  ```bash
  git checkout <branch-name>
  ```
- Create and switch:
  ```bash
  git checkout -b <branch-name>
  ```
- Merge branches:
  ```bash
  git merge <branch-name>
  ```
- Delete branch:
  ```bash
  git branch -d <branch-name>
  ```

---

## 🔹 4. Logs and Diffs
- View commit history:
  ```bash
  git log
  ```
- Show diff:
  ```bash
  git diff
  ```
- View commit summary:
  ```bash
  git show <commit-id>
  ```

---

## 🔹 5. Undoing Changes
- Undo staged file:
  ```bash
  git reset <file>
  ```
- Uncommit last commit:
  ```bash
  git reset --soft HEAD~1
  ```
- Discard all local changes:
  ```bash
  git restore .
  ```

---

## 🔹 6. Collaboration Best Practices
- Pull before you push
- Commit frequently with clear messages
- Use feature branches
- Resolve conflicts carefully
- Never push directly to `main` (use pull requests)

---

## 🧠 Tips to Remember
- `.gitignore` to exclude files from tracking
- Use `git stash` to temporarily save work
- Use `git rebase` for cleaner history (advanced)
- Keep commits atomic and meaningful

---

## 🗂 Example Workflow
```bash
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin git@github.com:user/repo.git
git push -u origin main
```

---

## ✅ Helpful Aliases (Optional)
```bash
git config --global alias.s status
git config --global alias.c commit
git config --global alias.a "add ."
git config --global alias.l "log --oneline --graph --all"
```
