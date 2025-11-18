# 👗 Mamakaram Saree House - E-Commerce Platform

> **Mana Kutumbam Mamathanuragala Anubandham** (Our Family, Filled with Care and Love)

Welcome to the complete e-commerce platform for **Mamakaram Saree House** — a family saree business offering traditional and modern sarees from Andhra Pradesh.

---

## 📋 Project Overview

A full-stack MERN (MongoDB, Express, React, Node.js) e-commerce application featuring:
- 🎨 Modern, responsive React frontend
- 🚀 Robust Node.js/Express REST API backend
- 💾 MongoDB database for scalability
- ☁️ Cloudinary integration for image hosting
- 💬 WhatsApp integration for direct customer inquiries
- 📱 Mobile-friendly design
- 🔍 Advanced search and filtering
- ⚡ Production-ready deployment setup

---

## 🏪 Business Information

**Company Name:** Mamakaram Saree House  
**Address:** Kommireddygari Palli Village, Pulicherla Mandal, Chittoor District, Andhra Pradesh - 517172  
**Phone/WhatsApp:** +91 62817 20436  
**Email:** mamakaramsareehouse@gmail.com  
**Repository:** mamakaram-saree-house

---

## ✨ Features

### Frontend (React)
- ✅ Responsive landing page with hero section
- ✅ Dynamic saree listing with grid layout
- ✅ Search functionality (real-time)
- ✅ Category-based filtering (right sidebar)
- ✅ Price range filter
- ✅ Multiple sort options (price, rating, newest)
- ✅ Product detail page
- ✅ WhatsApp "Order Now" button
- ✅ Contact information display
- ✅ Mobile-optimized responsive design

### Backend (Node.js + Express)
- ✅ REST API with CRUD operations
- ✅ GET `/api/sarees` - Fetch sarees with filters, search, sorting
- ✅ POST `/api/sarees/add` - Add new saree (admin)
- ✅ GET `/api/sarees/:id` - Get single saree details
- ✅ PUT `/api/sarees/:id` - Update saree (admin)
- ✅ DELETE `/api/sarees/:id` - Delete saree (admin)
- ✅ GET `/api/sarees/categories` - Get all categories
- ✅ CORS enabled for frontend integration
- ✅ Error handling middleware
- ✅ Environment variable configuration

### Database (MongoDB)
- ✅ Saree Schema with fields: name, category, price, image, colors, rating, stock status
- ✅ Flexible document structure
- ✅ Indexed for fast queries
- ✅ Local development support + MongoDB Atlas production support

### Additional Features
- ✅ Cloudinary integration for image uploads (framework ready)
- ✅ WhatsApp API integration for order inquiries
- ✅ Admin form for adding sarees with image upload
- ✅ Production deployment guides (Vercel, Render, MongoDB Atlas)

---

## 📁 Project Structure

```
mamakaram-saree-house/
├── backend/
│   ├── models/
│   │   └── Saree.js                 # MongoDB Schema
│   ├── routes/
│   │   └── sarees.js                # API Routes
│   ├── controllers/
│   │   └── sareeController.js       # Business Logic
│   ├── package.json                 # Backend Dependencies
│   ├── server.js                    # Express Server
│   └── .env                         # Environment Variables
│
├── frontend/
│   ├── public/
│   │   └── index.html               # HTML Entry Point
│   ├── src/
│   │   ├── api/
│   │   │   └── api.js               # Axios API Wrapper
│   │   ├── components/
│   │   │   ├── Navbar.js            # Navigation Bar
│   │   │   ├── Navbar.css
│   │   │   ├── SareeList.js         # Listing with Filters
│   │   │   ├── SareeList.css
│   │   │   ├── SareeCard.js         # Individual Product Card
│   │   │   ├── SareeCard.css
│   │   │   ├── ProductDetail.js     # Product Detail Page (TODO)
│   │   │   └── ProductDetail.css
│   │   ├── pages/
│   │   │   ├── Home.js              # Home Page
│   │   │   └── Home.css
│   │   ├── App.js                   # Main App Component
│   │   ├── App.css
│   │   ├── index.js                 # React Entry Point
│   │   ├── index.css                # Global Styles
│   │   └── .env.local               # Frontend Environment Variables
│   ├── package.json                 # Frontend Dependencies
│   └── .gitignore
│
├── README.md                         # This File
└── .gitignore                        # Git Ignore Rules

```

---

## 🚀 Quick Start

### Prerequisites
- Node.js v16+ and npm
- MongoDB (local or MongoDB Atlas account)
- Git

### 1️⃣ Backend Setup

```bash
cd backend
npm install

# Create .env file and add:
# MONGO_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/mamakaram?retryWrites=true&w=majority
# PORT=5000
# CLOUDINARY_CLOUD_NAME=your_cloud_name
# CLOUDINARY_API_KEY=your_api_key
# CLOUDINARY_API_SECRET=your_api_secret
# JWT_SECRET=your_secret_key

# Start development server
npm run dev

# Or production
npm start
```

**Expected Output:**
```
✅ MongoDB Connected
🚀 Server running on http://localhost:5000
```

### 2️⃣ Frontend Setup

```bash
cd frontend
npm install

# Frontend will automatically pick up backend from package.json proxy
# Or add to .env.local:
# REACT_APP_API_URL=http://localhost:5000

npm start
```

**Expected Output:**
```
Compiled successfully!
You can now view mamakaram-saree-frontend in the browser.
Local: http://localhost:3000
```

---

## 📡 API Endpoints

### Public Endpoints

#### Get All Sarees (with filters)
```
GET /api/sarees
Query Parameters:
  - q (search term)
  - category (filter by category)
  - minPrice, maxPrice (price range)
  - sort (price_asc, price_desc, newest, rating)
  - inStock (true/false)

Response:
{
  "success": true,
  "count": 5,
  "data": [
    {
      "_id": "...",
      "name": "Silk Saree",
      "category": "Silk",
      "price": 2500,
      "image": "url",
      "colors": ["Red", "Blue"],
      "inStock": true,
      "rating": 4.5,
      "reviews": 12
    }
  ]
}
```

#### Get Single Saree
```
GET /api/sarees/:id

Response:
{
  "success": true,
  "data": { ... }
}
```

#### Get All Categories
```
GET /api/sarees/categories

Response:
{
  "success": true,
  "data": ["All", "Silk", "Cotton", "Chiffon", ...]
}
```

### Admin Endpoints (Protected - Add JWT later)

#### Add Saree
```
POST /api/sarees/add
Body: {
  "name": "Designer Silk Saree",
  "category": "Silk",
  "price": 3500,
  "description": "Beautiful handwoven silk saree",
  "image": "cloudinary-url",
  "colors": ["Red", "Gold"],
  "inStock": true
}
```

#### Update Saree
```
PUT /api/sarees/:id
Body: { ...fields to update }
```

#### Delete Saree
```
DELETE /api/sarees/:id
```

---

## 🛠️ Configuration Guide

### Environment Variables

**Backend (.env)**
```env
# MongoDB
MONGO_URI=mongodb+srv://username:password@cluster0.mongodb.net/mamakaram?retryWrites=true&w=majority

# Server
PORT=5000

# Cloudinary (optional for now)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# JWT (for future admin authentication)
JWT_SECRET=your_secret_key_here

# Environment
NODE_ENV=development
```

**Frontend (.env.local)**
```env
# API Base URL
REACT_APP_API_URL=http://localhost:5000

# WhatsApp Number (without + sign)
REACT_APP_WHATSAPP_NUMBER=916281720436

# Cloudinary Upload URL (optional)
REACT_APP_CLOUDINARY_UPLOAD_URL=https://api.cloudinary.com/v1_1/your_cloud_name/image/upload

# Production
# REACT_APP_API_URL=https://mamakaram-backend.onrender.com
```

---

## 🐛 Troubleshooting

### Issue: "Cannot find module 'express'"
**Solution:**
```bash
cd backend
npm install
```

### Issue: "MongoDB connection failed"
**Solution:**
- Verify MONGO_URI in .env
- Check MongoDB Atlas IP whitelist (add 0.0.0.0/0 for dev)
- Ensure database name matches in URI

### Issue: "CORS error when fetching from frontend"
**Solution:**
- Ensure backend has `app.use(cors())` in server.js
- Check REACT_APP_API_URL matches backend URL in .env.local
- Verify backend is running on correct port

### Issue: "Frontend can't connect to backend"
**Solution:**
```bash
# Check if backend is running
curl http://localhost:5000/

# Should return: {"message":"🚀 Mamakaram Saree House API is running"}
```

---

## 📦 Adding Sample Data

### Via API (using Postman or curl)
```bash
curl -X POST http://localhost:5000/api/sarees/add \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Handwoven Silk Saree",
    "category": "Silk",
    "price": 3500,
    "description": "Traditional silk saree with gold borders",
    "image": "https://via.placeholder.com/300x400?text=Silk+Saree",
    "colors": ["Red", "Maroon", "Gold"],
    "inStock": true,
    "rating": 4.8,
    "reviews": 25
  }'
```

### Via Frontend Admin Panel (create later)
- Access admin form at `/admin`
- Upload image via Cloudinary
- Fill details and submit

---

## ☁️ Cloudinary Setup (Image Hosting)

### Step 1: Create Free Account
1. Go to [cloudinary.com](https://cloudinary.com)
2. Sign up (free tier includes 25GB storage)
3. Copy `Cloud Name`, `API Key`, `API Secret`

### Step 2: Add to Backend .env
```env
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Step 3: Frontend Upload Setup (create Admin form)
```javascript
// Add this to admin form later
const handleImageUpload = async (file) => {
  const formData = new FormData();
  formData.append("file", file);
  formData.append("upload_preset", "your_unsigned_preset");
  
  const response = await fetch(
    `https://api.cloudinary.com/v1_1/${process.env.REACT_APP_CLOUDINARY_CLOUD_NAME}/image/upload`,
    {
      method: "POST",
      body: formData
    }
  );
  const data = await response.json();
  return data.secure_url; // Use this URL in database
};
```

---

## 📱 WhatsApp Integration

### How It Works
- Customer clicks "Order on WhatsApp" button
- Opens WhatsApp with pre-filled message containing product details
- Direct chat with business (phone number from .env)

### Message Template
```
"Hello, I'm interested in [PRODUCT_NAME] (₹[PRICE]). 
Please share availability and delivery details."
```

### WhatsApp Business Account (Optional)
For automated replies and business features:
1. Upgrade to WhatsApp Business Account
2. Set up webhook for message automation
3. Integrate WhatsApp Business API (paid)

---

## 🚢 Deployment Guide

### Frontend Deployment (Vercel)

1. **Push to GitHub**
   ```bash
   git push origin main
   ```

2. **Connect to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "Import Project"
   - Select your GitHub repository
   - Select `frontend` as root directory
   - Add environment variables:
     ```
     REACT_APP_API_URL=https://your-backend-url.onrender.com
     REACT_APP_WHATSAPP_NUMBER=916281720436
     ```
   - Click "Deploy"

3. **Access Your Site**
   - Vercel will provide a URL like: `https://mamakaram.vercel.app`

### Backend Deployment (Render)

1. **Push to GitHub**
   ```bash
   git push origin main
   ```

2. **Connect to Render**
   - Go to [render.com](https://render.com)
   - Click "New" → "Web Service"
   - Connect GitHub account
   - Select repository and select `backend` folder
   - Set:
     - **Name:** mamakaram-saree-backend
     - **Environment:** Node
     - **Build Command:** `npm install`
     - **Start Command:** `npm start`
   - Add environment variables:
     ```
     MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/mamakaram
     PORT=5000
     NODE_ENV=production
     ```
   - Click "Deploy"

3. **Update Frontend .env**
   ```env
   REACT_APP_API_URL=https://mamakaram-saree-backend.onrender.com
   ```

### Database Deployment (MongoDB Atlas)

1. **Create Free Cluster**
   - Go to [mongodb.com/atlas](https://mongodb.com/atlas)
   - Create account and cluster
   - Wait for cluster to build (~5 min)

2. **Get Connection String**
   - Click "Connect" → "Connect Your Application"
   - Copy connection string
   - Replace `<password>` and database name

3. **Update Backend .env**
   ```env
   MONGO_URI=mongodb+srv://username:password@cluster0.mongodb.net/mamakaram
   ```

4. **Verify Connection**
   ```bash
   npm run dev
   # Should show: ✅ MongoDB Connected
   ```

---

## 🔄 Git Workflow & GitHub

### Initial Setup (One Time)

```bash
# In project root
git init
git checkout -b main
git add .
git commit -m "Initial commit — project scaffold with frontend and backend"

# Create GitHub repo: mamakaram-saree-house
# Then:
git remote add origin https://github.com/YOUR_USERNAME/mamakaram-saree-house.git
git push -u origin main
```

### Making Changes

```bash
# 1. Create feature branch
git checkout -b feature/add-search-filters

# 2. Make changes and test locally

# 3. Commit changes
git add .
git commit -m "feat: add search and category filters to saree listing"

# 4. Push to GitHub
git push -u origin feature/add-search-filters

# 5. Create Pull Request on GitHub
# - Go to https://github.com/YOUR_USERNAME/mamakaram-saree-house
# - Click "Compare & pull request"
# - Add description
# - Request review if working in team

# 6. Merge to main
# - After review/approval, click "Merge pull request"

# 7. Back to local main
git checkout main
git pull origin main
```

### Useful Git Commands

```bash
# Check status
git status

# View all branches
git branch -a

# Delete local branch
git branch -d feature/branch-name

# Delete remote branch
git push origin --delete feature/branch-name

# View commit history
git log --oneline

# Undo last commit (before push)
git reset --soft HEAD~1

# Fix remote URL if wrong
git remote remove origin
git remote add origin https://github.com/username/mamakaram-saree-house.git
```

---

## 📝 Development Roadmap

### Phase 1: ✅ Complete
- [x] Project structure setup
- [x] Backend API with CRUD operations
- [x] Frontend components and styling
- [x] Search and filtering
- [x] WhatsApp integration
- [x] Environment configuration

### Phase 2: In Progress
- [ ] Admin dashboard for adding sarees
- [ ] Cloudinary image upload integration
- [ ] Product detail page
- [ ] JWT authentication for admin
- [ ] Cart functionality

### Phase 3: Future
- [ ] Payment gateway integration (Razorpay/Stripe)
- [ ] Order management system
- [ ] Customer reviews and ratings
- [ ] Email notifications
- [ ] Analytics and sales dashboard
- [ ] Mobile app (React Native)

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📞 Support & Contact

- **Business WhatsApp:** +91 62817 20436
- **Email:** mamakaramsareehouse@gmail.com
- **Address:** Kommireddygari Palli Village, Pulicherla Mandal, Chittoor District, Andhra Pradesh - 517172

---

## 📜 License

This project is proprietary to Mamakaram Saree House. All rights reserved.

---

## 🙏 Acknowledgments

- Built with React, Node.js, Express, and MongoDB
- Hosted on Vercel (frontend) and Render (backend)
- Images hosted on Cloudinary
- Special thanks to the Mamakaram Saree House family for making this possible

---

**Made with 💜 for saree lovers everywhere**

Last Updated: November 2024
