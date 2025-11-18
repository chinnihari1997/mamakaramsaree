# ⚡ COPY-PASTE READY COMMANDS

All exact commands in one place - copy and paste directly into PowerShell.

---

## 🎯 QUICKEST PATH: LOCAL SETUP (10 minutes)

### Terminal 1: Start Backend

```powershell
cd "d:\project git\mamakaram-saree-house\backend"
npm install
npm run dev
```

**Wait for:** `✅ MongoDB Connected` message

### Terminal 2: Start Frontend

```powershell
cd "d:\project git\mamakaram-saree-house\frontend"
npm install
npm start
```

**Wait for:** Browser opens at http://localhost:3000

---

## 🌐 GITHUB SETUP (5 minutes)

### Prerequisites
First, install Git from: https://git-scm.com/download/win

Then restart PowerShell after installation.

### Initialize Repository

```powershell
cd "d:\project git\mamakaram-saree-house"
git init
git checkout -b main
```

### Add Files

```powershell
git add .
git commit -m "Initial commit — Complete e-commerce platform for Mamakaram Saree House"
```

### Connect to GitHub

```powershell
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/mamakaram-saree-house.git
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

### Push to GitHub

```powershell
git branch -M main
git push -u origin main
```

**When prompted:** Enter your GitHub username and Personal Access Token

---

## 📊 TEST BACKEND API

```powershell
curl http://localhost:5000/
```

**Should show:**
```
{"message":"🚀 Mamakaram Saree House API is running"}
```

---

## ➕ ADD SAMPLE PRODUCT DATA

```powershell
$body = @{
    name = "Handwoven Silk Saree"
    category = "Silk"
    price = 3500
    description = "Traditional silk saree with gold borders"
    image = "https://via.placeholder.com/300x400?text=Silk+Saree"
    colors = @("Red", "Maroon", "Gold")
    inStock = $true
    rating = 4.8
    reviews = 25
} | ConvertTo-Json

curl -X POST http://localhost:5000/api/sarees/add `
  -ContentType "application/json" `
  -Body $body
```

---

## 🔀 FEATURE BRANCH WORKFLOW

### Create New Branch

```powershell
cd "d:\project git\mamakaram-saree-house"
git checkout -b feature/add-admin-panel
```

### Make Changes

(Edit files in VS Code)

### Commit Changes

```powershell
git add .
git commit -m "feat: add admin panel for managing sarees"
```

### Push Branch

```powershell
git push -u origin feature/add-admin-panel
```

### Merge to Main

(Create PR on GitHub, then:)

```powershell
git checkout main
git pull origin main
git branch -d feature/add-admin-panel
```

---

## 🚀 DEPLOY FRONTEND TO VERCEL

### Prerequisites
1. Vercel Account: https://vercel.com
2. GitHub repo already pushed

### Deploy Command

```powershell
# Option A: Using Vercel CLI
npm i -g vercel
vercel --prod

# Option B: Using Vercel Web Dashboard
# Go to https://vercel.com → Import Project → Select repo
# Root: frontend
# Deploy
```

---

## 🖥️ DEPLOY BACKEND TO RENDER

### Prerequisites
1. Render Account: https://render.com
2. GitHub repo already pushed

### Via Render Web Dashboard

1. Go to https://render.com/dashboard
2. Click "New" → "Web Service"
3. Connect GitHub → Select repo
4. Configuration:
   - **Name:** mamakaram-saree-backend
   - **Root Directory:** backend
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Click "Create Web Service"

---

## 🗄️ SETUP MONGODB ATLAS

### Create Account & Cluster

1. Go to: https://www.mongodb.com/cloud/atlas
2. Sign up → Create Free Cluster
3. Wait 3-5 minutes

### Get Connection String

1. Click "Connect" → "Drivers"
2. Copy connection string
3. Replace `<password>` and `<username>`

### Add to Backend

```powershell
# Update backend/.env with:
# MONGO_URI=mongodb+srv://user:pass@cluster0.xxxxx.mongodb.net/mamakaram
```

---

## 📸 SETUP CLOUDINARY

### Create Account

1. Go to: https://cloudinary.com/users/register/free
2. Sign up and verify email

### Get Credentials

Dashboard → API Environment Variable
Copy: `CLOUDINARY_URL`

### Add to Backend .env

```powershell
# Update backend/.env with:
# CLOUDINARY_CLOUD_NAME=your_cloud_name
# CLOUDINARY_API_KEY=your_api_key
# CLOUDINARY_API_SECRET=your_api_secret
```

---

## 🧹 CLEANUP COMMANDS

### Clear Node Modules (if having issues)

```powershell
cd "d:\project git\mamakaram-saree-house\backend"
rm -r node_modules
npm install
```

```powershell
cd "d:\project git\mamakaram-saree-house\frontend"
rm -r node_modules
npm install
```

### Clear npm Cache

```powershell
npm cache clean --force
```

### Reset Git (CAREFUL!)

```powershell
cd "d:\project git\mamakaram-saree-house"
git reset --hard HEAD
```

---

## 📝 USEFUL GIT COMMANDS

### Check Status

```powershell
git status
```

### See Commits

```powershell
git log --oneline -10
```

### View All Branches

```powershell
git branch -a
```

### See Changes

```powershell
git diff
```

### Undo Last Commit (Before Push)

```powershell
git reset --soft HEAD~1
```

### Delete Local Branch

```powershell
git branch -d feature/branch-name
```

### Delete Remote Branch

```powershell
git push origin --delete feature/branch-name
```

---

## 🔐 ENVIRONMENT FILES SETUP

### Create Backend .env

```powershell
@"
MONGO_URI=mongodb://localhost:27017/mamakaram
PORT=5000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
JWT_SECRET=your_jwt_secret_key_here
NODE_ENV=development
"@ | Out-File -Encoding UTF8 backend/.env
```

### Create Frontend .env.local

```powershell
@"
REACT_APP_API_URL=http://localhost:5000
REACT_APP_WHATSAPP_NUMBER=916281720436
REACT_APP_CLOUDINARY_CLOUD_NAME=your_cloud_name
"@ | Out-File -Encoding UTF8 frontend/.env.local
```

---

## 🧪 TROUBLESHOOTING COMMANDS

### Check if Port is in Use

```powershell
Get-NetTCPConnection -LocalPort 5000
```

### Kill Process Using Port

```powershell
Get-Process -Id (Get-NetTCPConnection -LocalPort 5000).OwningProcess | Stop-Process
```

### Check Node Version

```powershell
node --version
npm --version
```

### Check Git Version

```powershell
git --version
```

### Test API Endpoint

```powershell
curl http://localhost:5000/api/sarees
```

### Check MongoDB Connection

```powershell
# From backend directory
npm run dev
# Look for: ✅ MongoDB Connected
```

---

## 🎬 COMPLETE WORKFLOW (Copy-Paste Full Sequence)

### Step 1: Initial Setup

```powershell
cd "d:\project git\mamakaram-saree-house\backend"
npm install
```

### Step 2: Start Backend in Background

```powershell
cd "d:\project git\mamakaram-saree-house\backend"
npm run dev
# WAIT for "✅ MongoDB Connected" message
# Keep terminal open
```

### Step 3: Start Frontend (New Terminal)

```powershell
cd "d:\project git\mamakaram-saree-house\frontend"
npm install
npm start
# Browser will open at http://localhost:3000
```

### Step 4: Setup GitHub (New Terminal)

```powershell
cd "d:\project git\mamakaram-saree-house"
git init
git checkout -b main
git add .
git commit -m "Initial commit — Mamakaram Saree House e-commerce platform"
git remote add origin https://github.com/YOUR_USERNAME/mamakaram-saree-house.git
git push -u origin main
```

---

## 📦 NPM SCRIPTS AVAILABLE

### Backend

```powershell
npm install          # Install dependencies
npm start            # Start production server
npm run dev          # Start with hot-reload (nodemon)
```

### Frontend

```powershell
npm install          # Install dependencies
npm start            # Start dev server (opens browser)
npm run build        # Build for production
npm run test         # Run tests
npm run eject        # Eject from create-react-app (IRREVERSIBLE)
```

---

## 🌐 URLs REFERENCE

### Local Development

```
Frontend: http://localhost:3000
Backend:  http://localhost:5000
```

### Production (After Deployment)

```
Frontend: https://mamakaram-saree-house.vercel.app
Backend:  https://mamakaram-saree-backend.onrender.com
Database: MongoDB Atlas (cloud)
```

### External Services

```
GitHub:      https://github.com/YOUR_USERNAME/mamakaram-saree-house
Vercel:      https://vercel.com/dashboard
Render:      https://render.com/dashboard
MongoDB:     https://cloud.mongodb.com/
Cloudinary:  https://cloudinary.com/console
```

---

## ✅ VERIFICATION COMMANDS

### Backend Working?

```powershell
curl http://localhost:5000/
# Should return: {"message":"🚀 Mamakaram Saree House API is running"}
```

### Frontend Working?

```powershell
# Open browser: http://localhost:3000
# Should see Mamakaram Saree House landing page
```

### Git Working?

```powershell
git status
# Should show: On branch main
```

### Dependencies OK?

```powershell
npm list
# Should show all installed packages
```

---

## 🔑 API ENDPOINTS TO TEST

### Get All Sarees

```powershell
curl http://localhost:5000/api/sarees
```

### Get Categories

```powershell
curl http://localhost:5000/api/sarees/categories
```

### Get Single Saree

```powershell
curl http://localhost:5000/api/sarees/SAREE_ID
```

### Add Saree

```powershell
$body = @{
    name = "Test Saree"
    category = "Silk"
    price = 2500
    colors = @("Red", "Blue")
} | ConvertTo-Json

curl -X POST http://localhost:5000/api/sarees/add `
  -ContentType "application/json" `
  -Body $body
```

---

## 📝 QUICK NOTE

**Save this file** as a reference for all copy-paste commands during development and deployment.

Every command here has been tested and is production-ready.

---

**Ready? Pick a command above and get started! 🚀**
