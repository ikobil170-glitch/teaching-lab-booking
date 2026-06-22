# Teaching Lab Booking System - Setup Guide

## ✅ Step 1: GitHub Repository
Your repository is ready at: `https://github.com/ikobil170-glitch/teaching-lab-booking`

---

## ✅ Step 2: Supabase Database Setup

### Create the `bookings` table:

1. Go to your Supabase project: https://app.supabase.com
2. Click **SQL Editor** on the left sidebar
3. Copy and paste this SQL code:

```sql
-- Create the bookings table
CREATE TABLE bookings (
  id BIGSERIAL PRIMARY KEY,
  slot_id TEXT NOT NULL,
  group_name TEXT NOT NULL,
  email TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(email, slot_id)
);

-- Enable RLS (Row Level Security)
ALTER TABLE bookings ENABLE ROW LEVEL SECURITY;

-- Create a policy to allow anyone to insert bookings
CREATE POLICY "Allow anyone to insert bookings" ON bookings
  FOR INSERT WITH CHECK (true);

-- Create a policy to allow anyone to read bookings
CREATE POLICY "Allow anyone to read bookings" ON bookings
  FOR SELECT USING (true);
```

4. Click **Run** (or press Ctrl+Enter)
5. You should see: "Success. No rows returned" ✅

---

## ✅ Step 3: Deploy to Vercel

### Method 1: Connect GitHub to Vercel (Automatic)

1. Go to https://vercel.com
2. Click **Add New** → **Project**
3. Click **Import Git Repository**
4. Search for `teaching-lab-booking` and click **Import**
5. Click **Deploy** (Vercel will automatically build and deploy)
6. Your site will be live at: `https://teaching-lab-booking.vercel.app` ✅

### Method 2: Manual Deployment (If Method 1 doesn't work)

1. Go to https://vercel.com/new/blank
2. Upload the `index.html` file
3. Click **Deploy**

---

## 🔧 How It Works

1. **User selects a slot** → JavaScript fetches booking counts from Supabase
2. **Slot reaches 30 bookings** → Card turns grey and becomes unclickable
3. **User fills form** → Data is submitted to Supabase `bookings` table
4. **Confirmation page** → Success message displayed

---

## 📊 View Your Bookings

1. Go to your Supabase project
2. Click **Table Editor** on the left
3. Select the `bookings` table
4. All submitted bookings will appear here ✅

---

## 🌐 Your Live URL

Once deployed on Vercel, share this link with students:
```
https://teaching-lab-booking.vercel.app
```

---

## ⚙️ Customization

To change slot details, edit `index.html` line ~150:

```javascript
const SLOTS = [
  { id: 'thu-am',  day: 'Thursday 25 June', time: '10:00 am – 12:00 pm', ... },
  // etc.
];
```

---

## ❓ Troubleshooting

**Slots not loading?**
- Check Supabase API keys in the HTML (they should already be set)
- Check browser console (F12) for errors

**Getting "30 people limit" error?**
- Go to Supabase → Table Editor → bookings
- Check the count manually
- Delete test entries if needed

**Vercel deployment failing?**
- Make sure `index.html` is in the root of your GitHub repo ✅

---

**Need help?** Check the GitHub repository README or create an issue!
