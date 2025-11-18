# ☁️ CLOUDINARY SETUP & IMAGE UPLOAD INTEGRATION

Complete step-by-step guide for free image hosting and management.

---

## 📋 STEP 1: Create Cloudinary Account

1. **Visit:** https://cloudinary.com/users/register/free
2. **Sign Up** with:
   - Email address
   - Password
   - Account name (use: `mamakaram-saree`)
3. **Verify Email** - Click verification link
4. **Welcome Screen** - You'll see your dashboard

---

## 🔑 STEP 2: Get Your Credentials

1. Go to **Dashboard** (top right after login)
2. You'll see **API Environment variable** at the bottom:
   ```
   CLOUDINARY_URL=cloudinary://api_key:api_secret@cloud_name
   ```

3. Extract these values:
   - **Cloud Name:** The part after `@`
   - **API Key:** The number part before `:`
   - **API Secret:** The part after `:`

**Example:**
```
If: CLOUDINARY_URL=cloudinary://123456:abcdef@my-cloud
Then:
- CLOUD_NAME = my-cloud
- API_KEY = 123456
- API_SECRET = abcdef
```

---

## 🛠️ STEP 3: Create Upload Preset (Optional - For Client-Side Upload)

**For Unsigned (Public) Uploads:**

1. Go to **Settings** (gear icon)
2. Click **Upload** tab
3. Scroll to **Upload presets**
4. Click **Add upload preset**
5. Fill:
   - **Name:** `mamakaram-unsigned`
   - **Unsigned:** Toggle ON
   - **Folder:** `mamakaram-sarees`
6. Click **Save**

---

## 🔧 STEP 4: Update Backend .env

```env
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

**Example:**
```env
CLOUDINARY_CLOUD_NAME=my-business
CLOUDINARY_API_KEY=123456789
CLOUDINARY_API_SECRET=abc_def_ghijk_lmnop
```

---

## 🔧 STEP 5: Update Frontend .env.local

```env
REACT_APP_CLOUDINARY_CLOUD_NAME=your_cloud_name
REACT_APP_CLOUDINARY_UPLOAD_PRESET=mamakaram-unsigned
```

---

## 📤 IMPLEMENTATION OPTIONS

### Option A: Client-Side Upload (Recommended for Admin Panel)

**Advantages:**
- ✅ No server-side processing needed
- ✅ Faster uploads
- ✅ User-friendly immediate feedback
- ✅ Free tier friendly

**Implementation:**

Add this to `AdminForm.js` (already implemented):

```javascript
const uploadImageToCloudinary = async () => {
  if (!image) {
    setError("Please select an image");
    return null;
  }

  const formDataUpload = new FormData();
  formDataUpload.append("file", image);
  formDataUpload.append(
    "upload_preset",
    process.env.REACT_APP_CLOUDINARY_UPLOAD_PRESET || "mamakaram-unsigned"
  );

  try {
    const response = await fetch(
      `https://api.cloudinary.com/v1_1/${process.env.REACT_APP_CLOUDINARY_CLOUD_NAME}/image/upload`,
      {
        method: "POST",
        body: formDataUpload,
      }
    );

    const data = await response.json();
    return data.secure_url; // Use this URL in database
  } catch (err) {
    console.error("Upload error:", err);
    return null;
  }
};
```

### Option B: Server-Side Upload (Signed - More Secure)

**Advantages:**
- ✅ More secure (signatures prevent unauthorized uploads)
- ✅ Better for production
- ✅ Can set upload limits per user

**Backend Implementation:**

```javascript
// backend/routes/upload.js
import express from "express";
import cloudinary from "cloudinary";
import multer from "multer";

cloudinary.v2.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET,
});

const router = express.Router();
const upload = multer({ storage: multer.memoryStorage() });

// Generate upload signature
router.post("/signature", (req, res) => {
  const timestamp = Math.round(Date.now() / 1000);
  const signature = cloudinary.v2.utils.api_sign_request(
    { timestamp },
    process.env.CLOUDINARY_API_SECRET
  );

  res.json({ timestamp, signature });
});

// Upload image
router.post("/upload", upload.single("file"), async (req, res) => {
  try {
    const result = await new Promise((resolve, reject) => {
      const stream = cloudinary.v2.uploader.upload_stream(
        {
          folder: "mamakaram-sarees",
          resource_type: "auto",
        },
        (error, result) => {
          if (error) reject(error);
          else resolve(result);
        }
      );
      stream.end(req.file.buffer);
    });

    res.json({ url: result.secure_url });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

export default router;
```

**Add to backend server.js:**

```javascript
import uploadRoutes from "./routes/upload.js";
app.use("/api/upload", uploadRoutes);
```

---

## 🖼️ IMAGE OPTIMIZATION

### Cloudinary Transformations

Use these in URLs for automatic optimization:

**Resize & Compress:**
```
https://res.cloudinary.com/your-cloud/image/upload/
  w_300,h_400,c_fill,q_auto/mamakaram-sarees/image.jpg
```

**Auto Format (WebP for modern browsers):**
```
https://res.cloudinary.com/your-cloud/image/upload/
  f_auto,q_auto/mamakaram-sarees/image.jpg
```

**Display in React:**

```javascript
// Use optimized URL
const optimizedImageUrl = `${imageUrl}?w_300&h_400&c_fill&f_auto&q_auto`;

<img src={optimizedImageUrl} alt="Saree" />
```

---

## 📁 FOLDER ORGANIZATION

In Cloudinary Dashboard → Media Library:

Create folders:
- `/mamakaram-sarees` - Main product images
- `/mamakaram-sarees/category-silk` - Category-specific
- `/mamakaram-sarees/thumbnails` - For listings

---

## 🧪 TESTING UPLOAD

### Using cURL

```bash
curl -X POST https://api.cloudinary.com/v1_1/YOUR_CLOUD_NAME/image/upload \
  -F "file=@/path/to/image.jpg" \
  -F "upload_preset=mamakaram-unsigned"
```

**Response Example:**
```json
{
  "public_id": "mamakaram-sarees/xyz123",
  "url": "http://res.cloudinary.com/...",
  "secure_url": "https://res.cloudinary.com/...",
  "width": 1024,
  "height": 768
}
```

### Using Frontend Admin Form

1. Open http://localhost:3000 (or access admin at `/admin`)
2. Select an image
3. Fill product details
4. Click "Add Saree"
5. Image automatically uploads and URL saved to database

---

## 🔐 SECURITY BEST PRACTICES

### ✅ DO:
- Use unsigned presets ONLY for trusted users (admin)
- For public uploads, use signed requests
- Enable `Restrict to folder` for each preset
- Regularly rotate API secrets
- Monitor upload usage in Cloudinary dashboard

### ❌ DON'T:
- Never expose `API_SECRET` in frontend code
- Don't put unsigned preset in public uploads
- Don't share API credentials in repositories
- Don't upload sensitive files

---

## 📊 MONITORING & LIMITS

### Free Tier Includes:
- ✅ 25 GB storage
- ✅ 25 GB bandwidth per month
- ✅ 300,000 total transformations per month
- ✅ Auto WebP conversion
- ✅ Responsive breakpoints
- ✅ 1,000 monthly credits

### Monitor Usage:
1. Go to **Dashboard**
2. Check **Usage** section (top right)
3. View monthly bandwidth and transformations

---

## 🚀 ADVANCED FEATURES

### Delete Images

**Backend Method:**

```javascript
// controllers/sareeController.js
export const deleteSareeImage = async (publicId) => {
  try {
    await cloudinary.v2.uploader.destroy(publicId);
    console.log("Image deleted successfully");
  } catch (error) {
    console.error("Error deleting image:", error);
  }
};
```

### Generate Thumbnails

**Cloudinary Automatically Generates:**
```
Original: https://res.cloudinary.com/.../image.jpg
Thumb 50x50: https://res.cloudinary.com/.../c_fill,w_50,h_50/image.jpg
Thumb 150x150: https://res.cloudinary.com/.../c_fill,w_150,h_150/image.jpg
```

### Batch Upload

```javascript
// Upload multiple images
const uploadMultiple = async (files) => {
  const uploadPromises = files.map((file) => uploadImageToCloudinary(file));
  return Promise.all(uploadPromises);
};
```

---

## 🆘 TROUBLESHOOTING

### Error: "Invalid upload preset"
**Solution:**
- Verify preset name in frontend .env
- Check preset exists in Cloudinary Settings

### Error: "CORS error"
**Solution:**
- Cloudinary accepts CORS by default
- Check network tab for actual error
- Verify Content-Type header

### Error: "File size exceeded"
**Solution:**
- Default limit: 100MB
- Compress image before upload
- Use `resource_type: "image"` for size optimization

### Images not appearing on production
**Solution:**
- Use `https://` URLs (secure_url)
- Check CORS headers
- Verify Cloudinary credentials are correct

---

## 📚 USEFUL LINKS

- **Cloudinary Dashboard:** https://cloudinary.com/console
- **API Documentation:** https://cloudinary.com/documentation/image_upload_api_reference
- **SDK Reference:** https://cloudinary.com/documentation/node_integration
- **Transformations Guide:** https://cloudinary.com/documentation/image_transformation_reference

---

## ✅ VERIFICATION CHECKLIST

- [ ] Cloudinary account created
- [ ] Cloud name, API key, API secret obtained
- [ ] Backend .env updated with credentials
- [ ] Frontend .env.local updated
- [ ] Upload preset created (for client-side upload)
- [ ] AdminForm component working locally
- [ ] Test upload successful to Cloudinary
- [ ] Image URL stored in MongoDB
- [ ] Images displaying in product listing
- [ ] No CORS errors in browser console

---

**All set! You're ready to handle image uploads like a pro! 🚀📸**
