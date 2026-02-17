# Grade-Level Meeting Form - Complete Setup Guide

## Overview
This form sends submissions to TWO places:
1. **Your email** (tarcisio.melo@ear.com.br) using EmailJS
2. **Google Forms** for organized tracking and spreadsheet export

---

## Step 1: Set Up EmailJS (Free Email Service)

EmailJS allows you to send emails directly from your website without a backend server.

### 1.1 Create an EmailJS Account:
1. Go to https://www.emailjs.com/
2. Click "Sign Up" (FREE for up to 200 emails/month)
3. Create your account using any email

### 1.2 Add Email Service:
1. After logging in, click "Email Services" in left sidebar
2. Click "Add New Service"
3. Choose **Gmail** (or your preferred provider)
4. Click "Connect Account"
5. Log in with **tarcisio.melo@ear.com.br**
6. Grant permissions when prompted
7. **COPY THE SERVICE ID** (looks like: service_abc123)
8. Click "Create Service"

### 1.3 Create Email Template:
1. Click "Email Templates" in left sidebar
2. Click "Create New Template"
3. Give it a name: "Grade Meeting Submission"
4. In the template editor, set:

**Subject line:**
```
{{subject}}
```

**Content (Body):**
```
Teacher: {{teacher_name}}
Grade: {{grade_level}}

{{message}}
```

5. Click "Save"
6. **COPY THE TEMPLATE ID** (looks like: template_xyz789)

### 1.4 Get Your Public Key:
1. Click "Account" in left sidebar
2. Click "General" tab
3. Scroll to "Public Key" section
4. **COPY YOUR PUBLIC KEY** (looks like: a1b2c3d4e5f6g7h8)

**Write these down:**
- ✅ Service ID: service_________
- ✅ Template ID: template_________
- ✅ Public Key: ________________

---

## Step 2: Create Google Forms

You need TWO separate Google Forms.

### 2.1 Form 1: Individual Student (FAST Protocol)
1. Go to https://forms.google.com
2. Create a new form
3. Title: "Individual Student Concern - FAST Protocol"
4. Add these questions **IN THIS EXACT ORDER** (all as "Short answer" or "Paragraph"):

| # | Question | Type | Required? |
|---|----------|------|-----------|
| 1 | Your Name | Short answer | Yes |
| 2 | Grade Level | Dropdown: 6th & 7th, 8th, 9th & 10th, 11th & 12th | Yes |
| 3 | Student Name | Short answer | Yes |
| 4 | F - Focus | Paragraph | Yes |
| 5 | A - Actions Tried | Paragraph | Yes |
| 6 | S - Support Needed | Paragraph | Yes |
| 7 | T - Talk | Paragraph | Yes |
| 8 | Additional Information | Paragraph | No |

### 2.2 Form 2: Grade Trends (GRADE Protocol)
1. Create another new form
2. Title: "Grade-Wide Trends - GRADE Protocol"
3. Add these questions **IN THIS EXACT ORDER**:

| # | Question | Type | Required? |
|---|----------|------|-----------|
| 1 | Your Name | Short answer | Yes |
| 2 | Grade Level | Dropdown: 6th & 7th, 8th, 9th & 10th, 11th & 12th | Yes |
| 3 | G - Group Patterns | Paragraph | Yes |
| 4 | R - Red Flags | Paragraph | Yes |
| 5 | A - Academics | Paragraph | Yes |
| 6 | D - Dynamics | Paragraph | Yes |
| 7 | E - External | Paragraph | Yes |

---

## Step 3: Get Google Forms Entry IDs

For **EACH** form, follow these steps:

### 3.1 Get the Form URL:
1. Click "Send" button (top right)
2. Click the link icon
3. Copy the form URL (looks like: `https://docs.google.com/forms/d/e/1FAIpQLSe.../viewform`)

### 3.2 Find Entry IDs:
1. Open the form URL in a **new tab**
2. Right-click anywhere on the page → **"View Page Source"**
3. Press `Ctrl+F` (Windows) or `Cmd+F` (Mac)
4. Search for: `entry.`
5. You'll find entries like: `entry.1234567890`

### 3.3 Match Entry IDs to Questions:
The entry IDs appear in the SAME ORDER as your questions. Write them down:

**For FAST Protocol Form:**
- Question 1 (Your Name): entry.___________
- Question 2 (Grade Level): entry.___________
- Question 3 (Student Name): entry.___________
- Question 4 (Focus): entry.___________
- Question 5 (Actions): entry.___________
- Question 6 (Support): entry.___________
- Question 7 (Talk): entry.___________
- Question 8 (Additional): entry.___________

**For GRADE Protocol Form:**
- Question 1 (Your Name): entry.___________
- Question 2 (Grade Level): entry.___________
- Question 3 (Group Patterns): entry.___________
- Question 4 (Red Flags): entry.___________
- Question 5 (Academics): entry.___________
- Question 6 (Dynamics): entry.___________
- Question 7 (External): entry.___________

---

## Step 4: Update the HTML File

Open `index.html` in a text editor (Notepad, VS Code, etc.)

### 4.1 Update EmailJS Configuration (Line ~466):
Find this line:
```javascript
emailjs.init("YOUR_EMAILJS_PUBLIC_KEY");
```

Replace with:
```javascript
emailjs.init("a1b2c3d4e5f6g7h8"); // Your actual Public Key
```

### 4.2 Update Service and Template IDs (Line ~480):
Find this section:
```javascript
await emailjs.send(
    "YOUR_SERVICE_ID",
    "YOUR_TEMPLATE_ID",
```

Replace with:
```javascript
await emailjs.send(
    "service_abc123",    // Your actual Service ID
    "template_xyz789",   // Your actual Template ID
```

### 4.3 Update Google Forms URLs (Line ~470):
Find this section:
```javascript
const GOOGLE_FORMS = {
    individual: 'https://docs.google.com/forms/d/e/YOUR_INDIVIDUAL_FORM_ID/formResponse',
    trends: 'https://docs.google.com/forms/d/e/YOUR_TRENDS_FORM_ID/formResponse'
};
```

Replace `YOUR_INDIVIDUAL_FORM_ID` and `YOUR_TRENDS_FORM_ID`:
- Take your form URL: `https://docs.google.com/forms/d/e/1FAIpQLSe.../viewform`
- Replace `viewform` with `formResponse`
- Result: `https://docs.google.com/forms/d/e/1FAIpQLSe.../formResponse`

### 4.4 Update Entry IDs (Line ~476):
Find this section and replace ALL the entry numbers:

```javascript
const FIELD_MAPPINGS = {
    individual: {
        teacherName: 'entry.1234567890',     // Replace with YOUR entry ID
        gradeLevel: 'entry.0987654321',      // Replace with YOUR entry ID
        studentName: 'entry.1122334455',     // Replace with YOUR entry ID
        focus: 'entry.5544332211',           // Replace with YOUR entry ID
        actions: 'entry.6677889900',         // Replace with YOUR entry ID
        support: 'entry.1231231234',         // Replace with YOUR entry ID
        talk: 'entry.4564564567',            // Replace with YOUR entry ID
        additional: 'entry.7897897890'       // Replace with YOUR entry ID
    },
    trends: {
        teacherName: 'entry.1111111111',     // Replace with YOUR entry ID
        gradeLevel: 'entry.2222222222',      // Replace with YOUR entry ID
        groupPatterns: 'entry.3333333333',   // Replace with YOUR entry ID
        redFlags: 'entry.4444444444',        // Replace with YOUR entry ID
        academics: 'entry.5555555555',       // Replace with YOUR entry ID
        dynamics: 'entry.6666666666',        // Replace with YOUR entry ID
        external: 'entry.7777777777'         // Replace with YOUR entry ID
    }
};
```

---

## Step 5: Deploy to GitHub Pages

1. Go to https://github.com
2. Click "New Repository" (green button)
3. Name it: `grade-level-meeting-form`
4. Make it **Public**
5. Click "Create Repository"
6. Upload `index.html` file
7. Go to **Settings** → **Pages**
8. Under "Source", select **main** branch
9. Click **Save**
10. Wait 2-3 minutes

Your form will be live at:
`https://YOUR-USERNAME.github.io/grade-level-meeting-form/`

---

## Step 6: Test Everything

1. Visit your GitHub Pages URL
2. Fill out the FAST form with test data
3. Click Submit
4. **Check your email** (tarcisio.melo@ear.com.br) - you should receive the submission
5. **Check your Google Form** responses - data should be there too
6. Repeat with GRADE form

---

## Troubleshooting

### Email not arriving?
- ✅ Check spam/junk folder
- ✅ Verify EmailJS Public Key is correct
- ✅ Verify Service ID is correct
- ✅ Verify Template ID is correct
- ✅ Check EmailJS dashboard for error logs
- ✅ Make sure you're within the 200 emails/month limit

### Google Forms not receiving data?
- ✅ Verify formResponse URLs are correct (not viewform)
- ✅ Double-check entry numbers match EXACTLY
- ✅ Make sure Google Forms are set to accept responses
- ✅ Check browser console (F12) for error messages

### GitHub Pages not working?
- ✅ File MUST be named `index.html`
- ✅ Repository MUST be Public
- ✅ Wait 2-3 minutes after enabling Pages
- ✅ Clear browser cache

---

## Summary Checklist

Before deploying, make sure you've updated:
- [ ] EmailJS Public Key
- [ ] EmailJS Service ID
- [ ] EmailJS Template ID
- [ ] Individual FAST Form URL
- [ ] Trends GRADE Form URL
- [ ] All 8 entry IDs for FAST form
- [ ] All 7 entry IDs for GRADE form

---

## Need Help?

If you're stuck:
1. Check EmailJS dashboard for error messages
2. Open browser console (F12) when submitting
3. Verify all IDs are copied correctly (no extra spaces)
4. Test one form at a time

## Support

For technical issues, contact your IT department or check:
- EmailJS Documentation: https://www.emailjs.com/docs/
- GitHub Pages Documentation: https://pages.github.com/
