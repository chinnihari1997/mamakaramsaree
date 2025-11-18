# 🚀 COMPLETE STEP-BY-STEP GUIDE: GitHub Setup & Deployment

## ⚙️ PREREQUISITES

### 1. Install Required Software (if not already installed)

#### Git Installation
- **Windows:** Download from https://git-scm.com/download/win
  - Run installer with default settings
  - Verify: Open PowerShell and run: `git --version`
  
- **Mac:** `brew install git`
- **Linux:** `sudo apt install git`

#### Node.js Installation
- Download from https://nodejs.org/ (LTS version recommended)
- Verify: `node --version` and `npm --version`

#### MongoDB Installation (Local Dev Only)
- **Option A:** Install locally from https://www.mongodb.com/try/download/community
- **Option B:** Use MongoDB Atlas (cloud) - recommended for production

---

## 📋 STEP-BY-STEP EXECUTION

### STEP 1: Navigate to Project Directory

```powershell
cd "d:\project git\mamakaram-saree-house"
```

### STEP 2: Initialize Git Repository

```powershell
git init
```

**Expected Output:**
```
Initialized empty Git repository in d:/project git/mamakaram-saree-house/.git/
```

### STEP 3: Create Main Branch

```powershell
git checkout -b main
```

**Note:** If it says "switched to a new branch", that's expected.

### STEP 4: Add All Files to Git

```powershell
git add .
```

### STEP 5: Create Initial Commit

```powershell
git commit -m "Initial commit — Complete e-commerce platform for Mamakaram Saree House with React frontend, Node.js backend, and MongoDB"
```

**Expected Output:**
```
[main (root-commit) abc1234] Initial commit — Complete e-commerce platform...
 45 files changed, 3200 insertions(+)
 create mode 100644 backend/models/Saree.js
 create mode 100644 backend/routes/sarees.js
 ...
```

---

## 🌐 GITHUB SETUP

### Create Repository on GitHub

1. Go to https://github.com/new
2. Fill in:
   - **Repository name:** `mamakaram-saree-house`
   - **Description:** "E-commerce platform for Mamakaram Saree House - React frontend, Node.js backend, MongoDB database"
   - **Visibility:** Public (or Private if you prefer)
   - **DO NOT initialize with README** (we already have one)
3. Click **"Create repository"**

### STEP 6: Add Remote Repository

```powershell
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/mamakaram-saree-house.git
```

**Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username**

**To verify:**
```powershell
git remote -v
```

**Expected Output:**
```
origin  https://github.com/YOUR_GITHUB_USERNAME/mamakaram-saree-house.git (fetch)
origin  https://github.com/YOUR_GITHUB_USERNAME/mamakaram-saree-house.git (push)
```

### STEP 7: Push to GitHub

```powershell
git branch -M main
git push -u origin main
```

**This will prompt you to log in to GitHub. Use:**
- Your GitHub username
- A Personal Access Token (create at: https://github.com/settings/tokens)
  - Go to Settings → Developer settings → Personal access tokens
  - Click "Generate new token"
  - Select scopes: `repo`, `workflow`
  - Copy and paste in terminal when prompted

**Expected Output:**
```
Enumerating objects: 45, done.
Counting objects: 100% (45/45), done.
Delta compression using up to 8 threads
Compressing objects: 100% (40/40), done.
Writing objects: 100% (45/45), 125.34 KiB | 2.50 MiB/s, done.
...
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

**Verify on GitHub:** Visit https://github.com/YOUR_USERNAME/mamakaram-saree-house

---

## 🔧 LOCAL DEVELOPMENT SETUP

### Install Backend Dependencies

```powershell
cd backend
npm install
```

**Creates:** `node_modules/` folder (ignore in .gitignore)

### Configure Backend Environment

```powershell
# Windows PowerShell - create .env file
@"
MONGO_URI=mongodb://localhost:27017/mamakaram
PORT=5000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
JWT_SECRET=your_jwt_secret_key_here
NODE_ENV=development
"@ | Out-File -Encoding UTF8 .env
```

### Start Backend Server

```powershell
npm run dev
```

**Expected Output:**
```
✅ MongoDB Connected
🚀 Server running on http://localhost:5000
```

**If MongoDB error:** Use MongoDB Atlas instead (see Deployment Guide in README.md)

### Install Frontend Dependencies

```powershell
cd ../frontend
npm install
```

### Start Frontend

```powershell
npm start
```

**Expected Output:**
```
Compiled successfully!
You can now view mamakaram-saree-frontend in the browser.
Local: http://localhost:3000
```

---

## 📱 TESTING LOCALLY

### Test Backend API

```powershell
# In new terminal/PowerShell window
curl http://localhost:5000/
```

**Expected Response:**
```json
{"message":"🚀 Mamakaram Saree House API is running"}
```

### Add Sample Data

```powershell
$body = @{
    name = "Handwoven Silk Saree"
    category = "Silk"
    price = 3500
    description = "Traditional silk saree"
    image = "https://via.placeholder.com/300x400"
    colors = @("Red", "Gold")
    inStock = $true
    rating = 4.8
    reviews = 25
} | ConvertTo-Json

curl -X POST http://localhost:5000/api/sarees/add `
  -ContentType "application/json" `
  -Body $body
```

### Access Frontend

Open browser: http://localhost:3000

---

## 🔀 GIT WORKFLOW: Making Changes

### Create Feature Branch

```powershell
git checkout -b feature/add-admin-panel
```

### Make Your Changes

Edit files using VS Code or your editor.

### Commit Changes

```powershell
git add .
git commit -m "feat: add admin panel for managing sarees"
```

### Push Branch to GitHub

```powershell
git push -u origin feature/add-admin-panel
```

### Create Pull Request

1. Go to https://github.com/YOUR_USERNAME/mamakaram-saree-house
2. Click "Compare & pull request"
3. Add title and description
4. Click "Create pull request"
5. After review, click "Merge pull request"

### Update Local Main

```powershell
git checkout main
git pull origin main
```

---

## 🚢 DEPLOYMENT GUIDE

### Deploy Frontend to Vercel

1. Push to GitHub first
2. Go to https://vercel.com and sign up
3. Click "Import Project"
4. Select your GitHub repository
5. Set Root Directory: `frontend`
6. Add Environment Variables:
   ```
   REACT_APP_API_URL=https://your-backend.onrender.com
   REACT_APP_WHATSAPP_NUMBER=916281720436
   ```
7. Click "Deploy"

**Get URL:** Vercel will give you something like `https://mamakaram-saree-house.vercel.app`

### Deploy Backend to Render

1. Go to https://render.com and sign up
2. Click "New" → "Web Service"
3. Connect GitHub
4. Select your repository
5. Configuration:
   - **Name:** mamakaram-saree-backend
   - **Root Directory:** backend
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
6. Add Environment Variables:
   ```
   MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/mamakaram
   PORT=5000
   NODE_ENV=production
   CLOUDINARY_CLOUD_NAME=...
   CLOUDINARY_API_KEY=...
   CLOUDINARY_API_SECRET=...
   ```
7. Click "Create Web Service"

**Get URL:** Render will give you something like `https://mamakaram-saree-backend.onrender.com`

### Update Frontend for Production

1. Update `frontend/.env.local`:
   ```
   REACT_APP_API_URL=https://mamakaram-saree-backend.onrender.com
   ```

2. Commit and push:
   ```powershell
   git add .
   git commit -m "config: update API URL for production backend"
   git push origin main
   ```

3. Vercel will auto-redeploy

### Setup MongoDB Atlas (Free Tier)

1. Go to https://www.mongodb.com/cloud/atlas
2. Sign up → Create free cluster
3. Wait for cluster creation (~5 min)
4. Click "Connect" → "Connect Your Application"
5. Copy connection string
6. Replace in your backend `.env`:
   ```
   MONGO_URI=mongodb+srv://username:password@cluster0.mongodb.net/mamakaram?retryWrites=true&w=majority
   ```

---

## 🐛 TROUBLESHOOTING

### Error: "git: The term 'git' is not recognized"
**Solution:** Restart PowerShell after installing Git

### Error: "Cannot find module 'express'"
**Solution:** Run `npm install` in backend directory

### Error: "MONGO_URI is not set"
**Solution:** Create `.env` file with MONGO_URI value

### Error: "CORS error from frontend"
**Solution:** Verify:
- Backend has `app.use(cors())`
- REACT_APP_API_URL matches backend URL
- Backend is running on correct port

### Error: "Port 5000 already in use"
**Solution:** Either:
```powershell
# Kill process using port 5000
Get-Process -Id (Get-NetTCPConnection -LocalPort 5000).OwningProcess | Stop-Process

# OR change PORT in .env
PORT=5001
```

---

## ✅ VERIFICATION CHECKLIST

- [ ] Git is installed (`git --version` works)
- [ ] Node.js is installed (`node --version` works)
- [ ] Repository created on GitHub
- [ ] Code pushed to GitHub (`git push` works)
- [ ] Backend starts with `npm run dev`
- [ ] Frontend starts with `npm start`
- [ ] Can access http://localhost:3000
- [ ] Backend API responds at http://localhost:5000
- [ ] No CORS errors in browser console
- [ ] Frontend .env.local has correct API URL
- [ ] Backend .env has MONGO_URI

---

## 📞 QUICK REFERENCE COMMANDS

```powershell
# Navigation
cd "d:\project git\mamakaram-saree-house"

# Git
git init                                    # Initialize repo
git status                                  # Check status
git add .                                   # Stage all changes
git commit -m "message"                     # Create commit
git push                                    # Push to GitHub
git pull                                    # Pull from GitHub
git checkout -b feature/name                # Create feature branch
git branch -a                               # List all branches

# Node/npm
npm install                                 # Install dependencies
npm start                                   # Start dev server
npm run dev                                 # Start with nodemon
npm run build                               # Build for production

# Backend
cd backend && npm run dev                   # Start backend
curl http://localhost:5000/                # Test backend

# Frontend
cd frontend && npm start                    # Start frontend
```

---

## 📊 Current Project Status

✅ **Completed:**
- Project structure created
- All backend files generated (server, models, routes, controllers)
- All frontend components created (React, CSS, API wrapper)
- Environment configuration files (.env, .env.local, .gitignore)
- Comprehensive README.md with deployment guide
- Git initialized and repository created

⏭️ **Next Steps:**
1. Install dependencies: `npm install` in both backend and frontend
2. Configure `.env` files with your credentials
3. Start backend and frontend locally to test
4. Deploy to Vercel (frontend) and Render (backend)
5. Create MongoDB Atlas cluster for production database

---

**All ready to go! Follow the commands above to get up and running. 🚀**
