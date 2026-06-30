# EDU720 Microteaching - Setup Instructions

## ✅ Your new booking page is ready!

**File:** `microteaching.html` in your GitHub repository

---

## 🔧 Step 1: Create the Supabase Table for Microteaching Bookings

1. Go to your Supabase project: **https://app.supabase.com**
2. Click **SQL Editor** on the left sidebar
3. Copy and paste **THIS CODE**:

```sql
-- Create the bookings_microteaching table
CREATE TABLE bookings_microteaching (
  id BIGSERIAL PRIMARY KEY,
  slot_id TEXT NOT NULL,
  group_name TEXT NOT NULL,
  email TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(email, slot_id)
);

-- Enable RLS (Row Level Security)
ALTER TABLE bookings_microteaching ENABLE ROW LEVEL SECURITY;

-- Create a policy to allow anyone to insert bookings
CREATE POLICY "Allow anyone to insert microteaching bookings" ON bookings_microteaching
  FOR INSERT WITH CHECK (true);

-- Create a policy to allow anyone to read bookings
CREATE POLICY "Allow anyone to read microteaching bookings" ON bookings_microteaching
  FOR SELECT USING (true);
```

4. Click **Run** (or press Ctrl+Enter)
5. You should see: ✅ **"Success. No rows returned"**

---

## 📋 Step 2: Update Vercel Deployment

Your existing Vercel deployment will automatically pick up the new file!

**Access your new booking page at:**
```
https://teaching-lab-booking.vercel.app/microteaching.html
```

---

## 🎯 The New Booking System Details

✅ **Sessions:** 
- Thursday 9 July: 10-12 am & 2-4 pm
- Friday 10 July: 10-12 am & 2-4 pm

✅ **Capacity:** 24 places total per time slot
- 3 parallel sessions × 8 students each

✅ **Slots:** 12 total slots (4 time slots × 3 parallel sessions)

✅ **Features:**
- Students can only book once
- Slots automatically close when they reach 8 students
- Real-time availability updates
- Green theme for Microteaching

---

## 📊 View Your Microteaching Bookings

1. Go to your Supabase project
2. Click **Table Editor** on the left
3. Select **`bookings_microteaching`** table
4. All bookings will appear here ✅

---

## 🔗 Share These Links

**With Students:**
- Microteaching bookings: `https://teaching-lab-booking.vercel.app/microteaching.html`
- Digital Tools (original): `https://teaching-lab-booking.vercel.app/index.html`

---

## ❓ Troubleshooting

**"Table not found" error?**
- Run the SQL code above to create the table

**Slots not loading?**
- Check browser console (F12) for errors
- Make sure you ran the SQL code

**Need to create more booking pages?**
- Just ask! I can create new pages for other workshops following the same pattern

---

**Your booking system is ready to go!** 🚀
