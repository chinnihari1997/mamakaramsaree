# 🔀 GIT WORKFLOW & BRANCH STRATEGY

Complete guide for managing code changes, creating branches, and pull requests.

---

## 📚 GIT BASICS REVIEW

### Key Concepts

**Repository (Repo):** Project folder with version control
**Branch:** Parallel version of code
**Commit:** Snapshot of changes with message
**Pull Request (PR):** Request to merge changes into main branch
**Merge:** Combine changes from one branch into another

---

## 🎯 BRANCH STRATEGY

### Main Branches

```
main
 ├─ Always production-ready code
 ├─ Only merge after testing & review
 └─ Automatically deploys to Vercel/Render

develop (optional)
 ├─ Integration branch for features
 ├─ Staging environment
 └─ More flexible than main
```

### Feature Branches

```
feature/add-search-filter
feature/admin-dashboard
feature/whatsapp-integration
feature/cloudinary-upload
```

### Naming Convention

```
feature/descriptive-name
bugfix/issue-description
docs/documentation-topic
hotfix/critical-issue
```

---

## 📝 STEP-BY-STEP: CREATE FEATURE BRANCH

### 1. Update Main Branch

```powershell
cd "d:\project git\mamakaram-saree-house"
git checkout main
git pull origin main
```

**Expected:** Main branch is up-to-date with GitHub

### 2. Create Feature Branch

```powershell
git checkout -b feature/add-product-filters
```

**Expected:**
```
Switched to a new branch 'feature/add-product-filters'
```

### 3. Make Changes

Edit files in VS Code:
- Add new component
- Modify existing files
- Delete if necessary

### 4. Check Status

```powershell
git status
```

**Expected:**
```
On branch feature/add-product-filters

Changes not staged for commit:
  modified:   frontend/src/components/SareeList.js
  new file:   frontend/src/components/CategoryFilter.js

Untracked files:
  frontend/src/styles/category-filter.css
```

### 5. Stage Changes

```powershell
# Stage specific files
git add frontend/src/components/SareeList.js
git add frontend/src/components/CategoryFilter.js

# Or stage all
git add .
```

### 6. Create Commit

```powershell
git commit -m "feat: add advanced category filtering to product list

- Implement right-side category filter component
- Add dynamic category fetching from API
- Include price range and stock filters
- Optimize search performance with debouncing"
```

**Commit Message Format:**
```
<type>: <subject>

<body>
<footer>
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `refactor:` Code restructuring
- `style:` Code style (no logic change)
- `test:` Adding tests

### 7. View Commits

```powershell
git log --oneline -5
```

**Expected:**
```
a1b2c3d (HEAD -> feature/add-product-filters) feat: add advanced category filtering
xyz1234 (origin/main) Initial commit
```

### 8. Push to GitHub

```powershell
git push -u origin feature/add-product-filters
```

**Expected:**
```
Enumerating objects: 12, done.
...
 * [new branch]      feature/add-product-filters -> feature/add-product-filters
Branch 'feature/add-product-filters' set up to track remote branch 'feature/add-product-filters' from 'origin'.
```

---

## 🔄 STEP-BY-STEP: CREATE PULL REQUEST

### 1. Go to GitHub

Visit: https://github.com/YOUR_USERNAME/mamakaram-saree-house

### 2. Create PR

1. Click **"Compare & pull request"** (yellow button)
2. Or click **"Pull requests"** → **"New pull request"**

### 3. Fill PR Details

**Title:**
```
feat: add advanced category filtering to product list
```

**Description:**
```markdown
## Changes
- Added new CategoryFilter component
- Implemented price range filter
- Added stock status filter

## Testing
- ✅ Tested on Chrome, Firefox
- ✅ Verified API integration
- ✅ Checked mobile responsiveness

## Screenshots
[Add before/after screenshots]

## Checklist
- [x] Code follows project style
- [x] No console errors
- [x] Tested locally
- [x] Updated README if needed
```

### 4. Review Process

**Others review:**
- Comment on code quality
- Suggest improvements
- Request changes if needed

**As author:**
- Respond to comments
- Make requested changes
- Push updates (auto-updates PR)

### 5. Merge PR

Once approved:
1. Click **"Merge pull request"**
2. Select **"Squash and merge"** (keeps history clean) or **"Create a merge commit"**
3. Click **"Confirm merge"**

**Expected:**
```
Pull request successfully merged and closed
```

---

## 🔃 KEEP BRANCH UP-TO-DATE

### If Main Changes While You Work

```powershell
# Fetch latest changes
git fetch origin

# Rebase your branch on main
git rebase origin/main feature/add-product-filters

# Or merge main into your branch
git merge main feature/add-product-filters

# Push updated branch
git push origin feature/add-product-filters
```

---

## 🔧 COMMON GIT COMMANDS

### View Branches

```powershell
# Local branches only
git branch

# All branches (local + remote)
git branch -a

# Show branch tracking
git branch -vv
```

### Switch Branches

```powershell
# Switch to existing branch
git checkout main

# Switch and create new
git checkout -b feature/new-feature

# Switch to remote branch
git checkout origin/feature-name
```

### Delete Branches

```powershell
# Delete local branch
git branch -d feature/completed-feature

# Force delete
git branch -D feature/abandoned-feature

# Delete remote branch
git push origin --delete feature/old-feature
```

### View Changes

```powershell
# See uncommitted changes
git diff

# See staged changes
git diff --staged

# See commit history
git log --oneline

# See specific commit
git show abc1234
```

### Undo Changes

```powershell
# Undo uncommitted changes in one file
git checkout frontend/src/App.js

# Undo all uncommitted changes
git reset --hard HEAD

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (create new commit that undoes it)
git revert abc1234
```

### Staging & Committing

```powershell
# Stage all changes
git add .

# Stage specific file
git add frontend/src/App.js

# Stage specific lines (interactive)
git add -p

# Unstage file
git reset frontend/src/App.js

# Amend last commit (add forgotten changes)
git add forgotten_file.js
git commit --amend --no-edit

# Modify last commit message
git commit --amend -m "new message"
```

---

## 🔀 MERGE CONFLICTS

### What Causes Conflicts

When same line edited in different branches:

```
main:     const name = "Mamakaram";
feature:  const name = "Saree House";
```

### Resolve Conflicts

```powershell
# Try to merge
git merge main

# Get conflict message:
# CONFLICT (content): Merge conflict in frontend/src/App.js

# Open file in editor - look for:
<<<<<<< HEAD
  Your changes
=======
  Main branch changes
>>>>>>> main

# Choose one (or combine):
const name = "Mamakaram Saree House";

# Remove conflict markers

# Stage resolved files
git add frontend/src/App.js

# Complete merge
git commit -m "fix: resolve merge conflict in App.js"
```

---

## 📋 EXAMPLE WORKFLOW

### Scenario: Add Admin Dashboard

```powershell
# 1. Update main branch
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/admin-dashboard

# 3. Create files
# (Create frontend/src/pages/Admin.js, AdminForm.js, etc.)

# 4. Test locally
npm start  # Verify changes work

# 5. Check what changed
git status
git diff

# 6. Stage & commit
git add frontend/src/pages/Admin.js
git add frontend/src/components/AdminForm.js
git add frontend/src/components/AdminForm.css
git commit -m "feat: add complete admin dashboard for saree management

- Create admin page with dashboard overview
- Implement add/edit/delete saree forms
- Integrate Cloudinary image upload
- Add form validation and error handling
- Style with responsive design"

# 7. Push to GitHub
git push -u origin feature/admin-dashboard

# 8. Create pull request on GitHub
# (Fill title, description, add screenshots)

# 9. Address review comments
git add frontend/src/pages/Admin.js
git commit -m "refactor: improve admin form validation per review feedback"
git push origin feature/admin-dashboard

# 10. Merge on GitHub (after approval)

# 11. Back to main locally
git checkout main
git pull origin main

# 12. Delete feature branch locally
git branch -d feature/admin-dashboard

# 13. Continue with next feature
git checkout -b feature/product-detail-page
```

---

## 🏷️ COMMIT MESSAGE BEST PRACTICES

### ✅ Good Examples

```
feat: add WhatsApp order button to product cards
fix: resolve CORS error in API requests
docs: update README with deployment instructions
refactor: extract common filter logic to utility function
style: improve navigation bar styling on mobile
test: add unit tests for SareeCard component
chore: update dependencies to latest versions
```

### ❌ Bad Examples

```
updated files
fix bug
changes
working version
test
wip
```

### Detailed Format

```powershell
git commit -m "feat: add real-time product search with debouncing

BREAKING CHANGE: Search now requires 3+ characters minimum

- Implement search input with 300ms debounce
- Integrate with backend GET /api/sarees?q= endpoint
- Cache search results for performance
- Add search result counter in UI
- Show 'no results' message when empty

Fixes #42
Closes #51"
```

---

## 🔐 SENSITIVE DATA PROTECTION

### ✅ DO:

```powershell
# Keep .env files local
# (Already in .gitignore)

# Use Git credential manager
git config --global credential.helper wincred

# Verify .gitignore before committing
git check-ignore -v backend/.env
```

### ❌ DON'T:

```powershell
# Never do:
git add .env
git add backend/.env

# Never commit:
API_KEY=abc123
DATABASE_PASSWORD=secret
```

### If You Accidentally Commit Secrets

```powershell
# Remove file from history
git filter-branch --tree-filter 'rm -f backend/.env' HEAD

# Or use BFG Repo-Cleaner (easier):
# https://rtyley.github.io/bfg-repo-cleaner/

# CRITICAL: Regenerate all exposed credentials!
```

---

## 📊 VIEWING REPOSITORY STATUS

### See Commits

```powershell
git log --oneline --graph --all

# Output:
# * abc1234 (HEAD -> main) Merge pull request #12
# |\
# | * xyz7890 (feature/search) feat: add search
# |/
# * def5678 Initial commit
```

### Compare Branches

```powershell
git diff main feature/search

# Shows all differences between branches
```

### See Who Changed What

```powershell
git blame frontend/src/App.js

# Shows which commit changed each line
```

---

## 🚀 QUICK WORKFLOW REFERENCE

```powershell
# Daily workflow:

# 1. Start day - get latest
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/your-feature

# 3. Work on code
# (edit files in VS Code)

# 4. Throughout day - commit regularly
git add .
git commit -m "feat: description"

# 5. Push to GitHub
git push origin feature/your-feature

# 6. When done - create PR on GitHub

# 7. After merge - clean up locally
git checkout main
git pull origin main
git branch -d feature/your-feature
```

---

## ✅ VERIFICATION CHECKLIST

- [ ] Local main branch up-to-date with GitHub
- [ ] Feature branch created with descriptive name
- [ ] Changes tested locally
- [ ] No `node_modules/` or `.env` files staged
- [ ] Commits have clear, descriptive messages
- [ ] Branch pushed to GitHub
- [ ] Pull request created with description
- [ ] Code review completed
- [ ] PR merged to main
- [ ] Deployed successfully after merge
- [ ] Feature branch deleted locally and remotely

---

## 📚 ADDITIONAL RESOURCES

- **Git Cheat Sheet:** https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf
- **Conventional Commits:** https://www.conventionalcommits.org/
- **GitHub Guides:** https://guides.github.com/
- **Pro Git Book:** https://git-scm.com/book/en/v2

---

**You're now a Git workflow master! 🎯✨**
