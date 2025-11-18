# 💬 WhatsApp Integration - Complete Guide

Direct customer communication for order inquiries and support.

---

## 🔗 How WhatsApp Integration Works

### User Flow:
1. Customer clicks "Order on WhatsApp" button on saree card
2. Browser redirects to WhatsApp Web/Mobile
3. Pre-filled message opens with:
   - Product name
   - Product price
   - Custom inquiry template
4. Customer sends message
5. Direct chat with business WhatsApp number

### No API Required:
- Uses WhatsApp Web link (free, instant)
- No authentication needed
- Works on mobile and desktop
- No monthly charges

---

## 📱 STEP 1: Get Your WhatsApp Business Number

### For Individuals/Small Business:
1. Have a WhatsApp account with the business number
2. Number must be verified by WhatsApp
3. Use that number in environment variables

### For Large Business (Optional - Paid):
1. Create WhatsApp Business Account
2. Get API access for automation
3. Setup webhooks for replies
4. (For now, use simple version)

---

## 🔧 STEP 2: Configure Environment Variables

**Backend .env:**
```env
WHATSAPP_BUSINESS_PHONE=916281720436
```

**Frontend .env.local:**
```env
REACT_APP_WHATSAPP_NUMBER=916281720436
```

**Important:** Phone number format:
- ✅ `916281720436` (country code + number, NO + sign)
- ❌ `+916281720436` (don't use + sign)
- ❌ `6281720436` (must include country code)

---

## 📝 STEP 3: WhatsApp Message Templates

### Basic Inquiry (Already Implemented)

```javascript
const waNumber = process.env.REACT_APP_WHATSAPP_NUMBER || "916281720436";
const waText = encodeURIComponent(
  `Hello, I'm interested in ${product.name} (₹${product.price}). Please share availability and delivery details.`
);
const waLink = `https://wa.me/${waNumber}?text=${waText}`;
window.open(waLink, "_blank");
```

**Result:**
```
WhatsApp Chat opens with:
"Hello, I'm interested in Handwoven Silk Saree (₹3500). Please share availability and delivery details."
```

### Custom Templates

**Template 1: Bulk Order**
```javascript
const bulkOrderText = encodeURIComponent(
  `Hi! I'm interested in bulk order of ${product.name}. Can you provide wholesale pricing for 10+ pieces?`
);
const link = `https://wa.me/${waNumber}?text=${bulkOrderText}`;
```

**Template 2: Custom Design**
```javascript
const customText = encodeURIComponent(
  `Hello! Can I get ${product.name} in custom colors? Please let me know available options.`
);
const link = `https://wa.me/${waNumber}?text=${customText}`;
```

**Template 3: Delivery Inquiry**
```javascript
const deliveryText = encodeURIComponent(
  `Hi! Interested in ${product.name}. What's the estimated delivery time to Bangalore?`
);
const link = `https://wa.me/${waNumber}?text=${deliveryText}`;
```

---

## 💻 IMPLEMENTATION IN REACT

### Already Implemented in SareeCard.js

```javascript
const SareeCard = ({ saree }) => {
  const waNumber = process.env.REACT_APP_WHATSAPP_NUMBER || "916281720436";

  const handleWhatsAppOrder = () => {
    const waText = encodeURIComponent(
      `Hello, I'm interested in ${saree.name} (₹${saree.price}). Please share availability and delivery details.`
    );
    window.open(
      `https://wa.me/${waNumber}?text=${waText}`,
      "_blank"
    );
  };

  return (
    <button onClick={handleWhatsAppOrder}>
      <FaWhatsapp /> Order on WhatsApp
    </button>
  );
};
```

### Create Reusable Hook

**frontend/src/hooks/useWhatsApp.js:**

```javascript
import { useCallback } from "react";

const useWhatsApp = (phoneNumber) => {
  const openWhatsApp = useCallback(
    (message) => {
      const encodedMessage = encodeURIComponent(message);
      const link = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;
      window.open(link, "_blank");
    },
    [phoneNumber]
  );

  return openWhatsApp;
};

export default useWhatsApp;
```

**Usage:**
```javascript
import useWhatsApp from "../hooks/useWhatsApp";

const MyComponent = () => {
  const sendWhatsApp = useWhatsApp("916281720436");

  const handleOrderClick = () => {
    sendWhatsApp("Hello! I'm interested in your sarees. Can you show me the latest collection?");
  };

  return <button onClick={handleOrderClick}>Contact Us</button>;
};
```

---

## 🎨 UI BUTTON IMPLEMENTATIONS

### Button with Icon (Already in SareeCard)

```jsx
import { FaWhatsapp } from "react-icons/fa";

<button className="whatsapp-btn" onClick={handleWhatsAppOrder}>
  <FaWhatsapp /> Order on WhatsApp
</button>
```

**CSS:**
```css
.whatsapp-btn {
  background-color: #25d366;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 6px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: 600;
  transition: background-color 0.3s ease;
}

.whatsapp-btn:hover {
  background-color: #1ebc59;
}
```

### Floating Action Button (FAB)

```jsx
import { FaWhatsapp } from "react-icons/fa";

const FloatingWhatsAppButton = ({ phoneNumber, message }) => {
  const handleClick = () => {
    const encodedMessage = encodeURIComponent(message);
    window.open(
      `https://wa.me/${phoneNumber}?text=${encodedMessage}`,
      "_blank"
    );
  };

  return (
    <button className="whatsapp-fab" onClick={handleClick}>
      <FaWhatsapp />
    </button>
  );
};

export default FloatingWhatsAppButton;
```

**CSS:**
```css
.whatsapp-fab {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 60px;
  height: 60px;
  background-color: #25d366;
  color: white;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.8rem;
  box-shadow: 0 4px 12px rgba(37, 211, 102, 0.3);
  transition: all 0.3s ease;
  z-index: 999;
}

.whatsapp-fab:hover {
  background-color: #1ebc59;
  transform: scale(1.1);
  box-shadow: 0 6px 20px rgba(37, 211, 102, 0.4);
}
```

---

## 📞 STEP 4: Additional Contact Options (Already in Navbar)

```jsx
import { FaPhone, FaEnvelope } from "react-icons/fa";

<div className="contact-buttons">
  {/* WhatsApp */}
  <button onClick={handleWhatsAppClick}>
    <FaWhatsapp /> WhatsApp
  </button>

  {/* Direct Call */}
  <a href="tel:+916281720436">
    <FaPhone /> Call
  </a>

  {/* Email */}
  <a href="mailto:mamakaramsareehouse@gmail.com">
    <FaEnvelope /> Email
  </a>
</div>
```

---

## 🔄 BACKEND API ENDPOINT (Optional)

If you want to log inquiries:

```javascript
// backend/routes/inquiries.js
import express from "express";
import Inquiry from "../models/Inquiry.js";

const router = express.Router();

// Log inquiry
router.post("/log", async (req, res) => {
  try {
    const { sareeId, sareeName, customerName, phone } = req.body;
    
    const inquiry = new Inquiry({
      sareeId,
      sareeName,
      customerName,
      phone,
      timestamp: new Date(),
    });

    await inquiry.save();
    res.json({ success: true, message: "Inquiry logged" });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

export default router;
```

**Model:**
```javascript
// backend/models/Inquiry.js
import mongoose from "mongoose";

const inquirySchema = new mongoose.Schema({
  sareeId: String,
  sareeName: String,
  customerName: String,
  phone: String,
  timestamp: { type: Date, default: Date.now },
});

export default mongoose.model("Inquiry", inquirySchema);
```

---

## 🧪 TESTING

### Test in Browser Console

```javascript
// Simulate WhatsApp order button click
const waNumber = "916281720436";
const message = "Hello, I'm interested in your sarees!";
const waLink = `https://wa.me/${waNumber}?text=${encodeURIComponent(message)}`;
window.open(waLink, "_blank");
```

### Test on Mobile

1. Open app on mobile phone
2. Click "Order on WhatsApp" button
3. Should open WhatsApp app with pre-filled message
4. Can send directly

---

## 💡 BEST PRACTICES

### ✅ DO:
- Personalize messages with product details
- Keep messages concise and clear
- Include business name in message
- Respond quickly to inquiries
- Use WhatsApp Business Account for branding

### ❌ DON'T:
- Send unsolicited messages
- Use WhatsApp for spam
- Share customer numbers publicly
- Automate replies without user consent
- Forget to include product details

---

## 🚀 ADVANCED: WhatsApp Business API (Optional)

For automated replies and analytics:

1. **Request API Access**
   - Go to https://www.facebook.com/business/apps
   - Apply for WhatsApp Business API

2. **Webhook Setup**
   - Verify webhooks for incoming messages
   - Set up bot responses

3. **Benefits:**
   - 24/7 automated replies
   - Message templates
   - Customer analytics
   - Team management

---

## 📊 ANALYTICS SUGGESTIONS

**Track in Backend:**
```javascript
// Log each WhatsApp inquiry
router.get("/analytics/inquiries", async (req, res) => {
  const inquiries = await Inquiry.find({});
  const stats = {
    total: inquiries.length,
    byProduct: {},
    thisMonth: inquiries.filter(i => {
      const d = new Date(i.timestamp);
      return d.getMonth() === new Date().getMonth();
    }).length,
  };
  res.json(stats);
});
```

---

## 🆘 TROUBLESHOOTING

### WhatsApp Link Not Opening
- Verify phone number format (no + sign)
- Check if WhatsApp is installed on device
- Try `https://wa.me/` protocol

### Message Not Pre-filling
- Ensure message is URL encoded
- Check for special characters
- Use `encodeURIComponent()`

### Number Invalid Error
- Verify country code is correct
- Check no + sign in number
- Test with international format: `country_code + number`

---

## ✅ VERIFICATION CHECKLIST

- [ ] WhatsApp number configured in .env files
- [ ] Frontend REACT_APP_WHATSAPP_NUMBER set correctly
- [ ] WhatsApp button visible on product cards
- [ ] Clicking button opens WhatsApp
- [ ] Pre-filled message contains product info
- [ ] Works on mobile and desktop
- [ ] No console errors
- [ ] Message is readable and professional

---

## 📚 USEFUL LINKS

- **WhatsApp Web Link Format:** https://faq.whatsapp.com/general/20952424
- **URL Encoding Reference:** https://www.w3schools.com/tags/ref_urlencode.asp
- **React Icons WhatsApp:** https://react-icons.github.io/react-icons/

---

**You're now ready to enable direct WhatsApp communication with customers! 💬✨**
