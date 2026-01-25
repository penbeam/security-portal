# 🛡️ Security Incident Response & Dashboard System

A professional, end-to-end security incident reporting system featuring a web portal, automated logging, Telegram alerts, and a real-time data dashboard. Designed to be **completely beginner-friendly** - no technical experience required.

## 🌐 Live Demo
- **Report Form:** https://penbeam.github.io/security-portal/
- **Dashboard:** https://penbeam.github.io/security-portal/dashboard.html


## 📋 Table of Contents
1. [Overview](#-overview)
2. [Prerequisites](#-prerequisites)
3. [Step-by-Step Setup](#-step-by-step-setup-guide)
4. [File Customization](#-file-customization)
5. [Testing & Launch](#-testing--launch)
6. [Troubleshooting](#-troubleshooting)
7. [FAQs](#-frequently-asked-questions)



## 📖 Overview

This system consists of 4 main components that work together:

1. **Web Portal** (`index.html`) - Where users report incidents
2. **Database** (Google Sheets) - Where all incident data is stored
3. **Automation** (Make.com) - Processes and routes incident reports
4. **Dashboard** (`dashboard.html`) - Real-time view of all incidents
5. **Alerts** (Telegram + Email) - Instant notifications to your team

---

## 🧰 Prerequisites

You need these FREE accounts (click links to sign up):

|     Account    |             Purpose             |   Free Tier?   |
|----------------|---------------------------------|----------------|
| **[Google Account](https://accounts.google.com/signup)** | For Google Sheets database | ✅ Yes |
| **[Make.com](https://www.make.com/)** | Automation logic (connects everything) | ✅ Yes (Free plan available) |
| **[Telegram](https://telegram.org/)** | Mobile alerts on your phone | ✅ Yes |
| **[GitHub](https://github.com/signup)** | Hosting the web portal files | ✅ Yes |

> **Note:** All services offer free tiers that are sufficient for this project.



## 📝 Step-by-Step Setup Guide

Follow these steps **in order**. Each step is explained in detail.

### Step 1: Database Setup (Google Sheets)

This will be your secure database where all incidents are stored.

1. **Go to [Google Sheets](https://sheets.google.com)**
   - Click the "+" button to create a new spreadsheet
   
2. **Rename the spreadsheet**
   - Click on "Untitled spreadsheet" at the top
   - Type exactly: `Security Incidents Log`
   - Press Enter

3. **Set up the column headers** (VERY IMPORTANT - Must be EXACT):
   - Click on **cell A1** (first cell, top-left)
   - Type `Case ID` (capital C, capital I, capital D)
   - Press **Tab** key to move to cell B1
   - Continue typing all headers in this exact order:

| Cell |     Type This Exactly     |         What It Means         |
|------|---------------------------|-------------------------------|
|  A1  |    `Case ID`              |    Automatic case number      |
|  B1  |    `Timestamp`            |    Date and time of report    |
|  C1  |    `Status`               |    Open/Closed status         |
|  D1  |    `Reporter Name`        |    Who reported it            |
|  E1  |    `Reporter Email`       |    Their email address        |
|  F1  |    `Department`           |    Their department           |
|  G1  |    `Incident Type`        |    Type of incident           |
|  H1  |    `Priority`             |    High/Medium/Low            |
|  I1  |    `Description`          |    What happened              |
|  J1  |    `User Timezone`        |    Their timezone             |

4. **Share your spreadsheet** (CRITICAL STEP):
   - Click the green **"Share"** button (top-right)
   - Click **"Change to anyone with the link"**
   - Make sure it says **"Viewer"** (not "Editor")
   - Click **"Copy link"**
   - Click **"Done"**

5. **Get your Sheet ID** (save this for later):
   - Look at your browser's address bar
   - The URL looks like: `https://docs.google.com/spreadsheets/d/1ABC123xyz/edit`
   - Copy the part between `/d/` and `/edit`
   - Example: If URL is `.../d/1aB2c3D4eF5g/edit`, then Sheet ID is `1aB2c3D4eF5g`
   - Save this ID in a Notepad or TextEdit file

✅ **Step 1 Complete:** Your database is ready!



### Step 2: Telegram Bot Setup

This will send alerts to your phone when incidents are reported.

1. **Open Telegram app** on your phone or computer
   
2. **Search for @BotFather** (Telegram's official bot creator)
   - Click "Start" or "Send Message"
   
3. **Create your bot:**
   - Type `/newbot` and send
   - It asks: "Alright, a new bot. How are we going to call it?"
   - Type: `Security Alert Bot` (or any name you like)
   - It asks: "Good. Now let's choose a username for your bot..."
   - Type: `YourCompanySecurityBot` (must end with "bot", e.g., `CompanySecBot`)
   
4. **Save your Bot Token:**
   - BotFather will give you a long string like:
     `1234567890:ABCdefGHIjklMNOPqrswXYZ`
   - **SAVE THIS TOKEN SECURELY** - This is your bot's password
   
5. **Create a private channel:**
   - In Telegram, click the hamburger menu (≡)
   - Click "New Channel"
   - Name it: `Security Incidents`
   - Make it **Private** (important!)
   - Add your bot as an **Administrator**
   
6. **Get your Channel ID:**
   - Send any message to your new channel
   - Forward that message to **@RawDataBot** or **@getidsbot**
   - It will reply with numbers like `-1001234567890`
   - **SAVE THIS CHANNEL ID**

✅ **Step 2 Complete:** Your alert system is ready!



### Step 3: Make.com Automation Setup

This is the "brain" that connects everything together.

1. **Log in to [Make.com](https://www.make.com/)**
   
2. **Create a new scenario:**
   - Click **"Create a new scenario"** (blue button)
   - Click the **"+"** button to add first module
   
3. **Module 1: Webhook** (Receives data from web portal)
   - Search for **"Webhooks"**
   - Select **"Custom Webhook"**
   - Click **"Add"**
   - Click **"Copy"** next to the webhook URL
   - **SAVE THIS WEBHOOK URL** - You'll need it soon
   - Click **"OK"**

4. **Module 2: Google Sheets** (Saves data to database)
   - Click the **"+"** button below Module 1
   - Search for **"Google Sheets"**
   - Select **"Add a Row"**
   - Click **"Add"** then **"Connect"**
   - Log in with your Google account
   - Select your **"Security Incidents Log"** spreadsheet
   - Select **"Sheet1"** as the worksheet
   - Map the fields exactly as shown below:

|      Make.com Field      |               Map To This Data               |
|--------------------------|----------------------------------------------|
|        `Case ID`         |   `{{1.caseId}}` (auto-generates ID)         |
|        `Timestamp`       |   `{{1.timestamp}}`                          |
|        `Status`          |   Type Manually: `NEW`                       |
|        `Reporter Name`   |   `{{1.reporterName}}`                       |
|        `Reporter Email`  |   `{{1.reporterEmail}}`                      |
|        `Department`      |   `{{1.department}}`                         |
|        `Incident Type`   |   `{{1.incidentType}}`                       |
|        `Priority`        |   `{{1.priority}}`                           |
|        `Description`     |   `{{1.description}}`                        |
|        `User Timezone`   |   `{{1.userTimezone}}`                       |

5. **Module 3: Telegram** (Sends mobile alert)
   - Click **"+"** button below Module 2
   - Search for **"Telegram"**
   - Select **"Send a Text Message"**
   - Click **"Add"** then **"Connect"**
   - Enter your **Bot Token** (from Step 2)
   - In **"Chat ID"** field, enter your **Channel ID** (from Step 2)
   - In **"Text"** field, paste this exact message:


🚨 NEW SECURITY INCIDENT
Case ID: {{1.caseId}}
Priority: {{1.priority}}
Type: {{1.incindentType}}
Reported by: {{1.reporterName}}
Department: {{1.department}}

Description: {{1.description}}


6. **Module 4: Gmail** (Sends email alert)
   - Click **"+"** button below Module 3
   - Search for **"Gmail"**
   - Select **"Send an Email"**
   - Click **"Add"** then **"Connect"**
   - Log in with your Google account
   - Fill in these fields:
     - **To:** (Your email, e.g., `security@yourcompany.com`)
     - **Subject:** `Security Incident #{{1.caseId}} - {{1.priority}} Priority`
     - **Content Type / Parse Mode:** HTML
     - **Content:** Paste this exact code:

```html
<div style="font-family: Arial, sans-serif; max-width: 600px; border: 1px solid #eee; border-radius: 8px; overflow: hidden;">
  <div style="background-color: {{if(trim(lower(1.priority)) == 'high'; '#dc3545'; if(trim(lower(1.priority)) == 'medium'; '#ffc107'; '#28a745'))}}; color: white; padding: 15px; text-align: center;">
    <h2 style="margin: 0; font-size: 20px;">
      {{if(trim(lower(1.priority)) == 'high'; '🔴 HIGH PRIORITY'; if(trim(lower(1.priority)) == 'medium'; '🟡 MEDIUM PRIORITY'; '🟢 LOW PRIORITY'))}}
    </h2>
  </div>
  
  <table style="width: 100%; border-collapse: collapse; background-color: white;">
    <tr><td style="padding: 12px; border-bottom: 1px solid #eee; color: #666;"><strong>Case ID:</strong></td><td style="padding: 12px; border-bottom: 1px solid #eee;">{{1.caseId}}</td></tr>
    <tr><td style="padding: 12px; border-bottom: 1px solid #eee; color: #666;"><strong>Incident Time:</strong></td><td style="padding: 12px; border-bottom: 1px solid #eee;">{{1.timestamp}}</td></tr>
    <tr><td style="padding: 12px; border-bottom: 1px solid #eee; color: #666;"><strong>Reporter:</strong></td><td style="padding: 12px; border-bottom: 1px solid #eee;">{{1.reporterName}} ({{1.reporterEmail}})</td></tr>
    <tr><td style="padding: 12px; border-bottom: 1px solid #eee; color: #666;"><strong>Department:</strong></td><td style="padding: 12px; border-bottom: 1px solid #eee;">{{1.department}}</td></tr>
    <tr><td style="padding: 12px; border-bottom: 1px solid #eee; color: #666;"><strong>Incident Type:</strong></td><td style="padding: 12px; border-bottom: 1px solid #eee;">{{1.incidentType}}</td></tr>
  </table>
  
  <div style="background-color: #f8f9fa; padding: 15px; border-top: 1px solid #eee;">
    <strong style="color: #333;">Description:</strong><br>
    <p style="color: #444; line-height: 1.5;">{{1.description}}</p>
  </div>
  
  <div style="padding: 15px; text-align: center; color: #999; font-size: 11px; background-color: #ffffff;">
    🛡️ This alert was automatically generated by the Security Incident System.
  </div>
</div>
```

**NOTE:** For better user experience, wrap this code in proper HTML format that include html, style, head, body tags.

7. **Turn on your scenario:**
   - Click the toggle switch at the bottom left (it will turn from gray to blue)
   - Click **"Save"**

✅ **Step 3 Complete:** Your automation is ready!



### Step 4: GitHub Setup (Hosting Web Portal)

1. **Go to [GitHub.com](https://github.com)**
   - Sign in or create account
   
2. **Create a new repository:**
   - Click **"+"** icon (top-right) → **"New repository"**
   - Repository name: `security-portal`
   - Make it **Public**
   - Check **"Add a README file"**
   - Click **"Create repository"**

3. **Upload your files:**
   - Download the two files from this project:
     - `index.html` (reporting portal)
     - `dashboard.html` (dashboard view)
   - In your GitHub repository, click **"Add file"** → **"Upload files"**
   - Drag and drop both HTML files
   - Click **"Commit changes"**

4. **Enable GitHub Pages:**
   - Go to **Settings** (tab at top)
   - Scroll down to **"Pages"** section (left sidebar)
   - Under **"Source"**, select: **"Deploy from a branch"**
   - Under **"Branch"**, select: **"main"** and **"/ (root)"**
   - Click **"Save"**
   - Wait 1-2 minutes, then refresh page
   - You'll see: **"Your site is live at https://username.github.io/security-portal/"**

✅ **Step 4 Complete:** Your web portal is live!



## 🛠️ File Customization

### Customize Web Portal (`index.html`)

1. **Download the file** to your computer
2. **Open with Notepad** (Windows) or **TextEdit** (Mac)
3. **Find these lines**:

   **javascript**
     // ⚠️ REPLACE THIS WITH YOUR ACTUAL WEBHOOK URL ⚠️
            const webhookUrl = "YOUR_CUSTOM_WEBHOOK_URL";

4. **Replace it** with your actual Make.com webhook URL so it should looks like:
       **javascript**
       const webhookUrl = "https://hook.make.com/your-actual-webhook-url";

5. **Save the file** and re-upload to GitHub

### Customize Dashboard (`dashboard.html`)

1. **Open the file** with Notepad or TextEdit
2. **Find these lines**:
      **javascript**
      // Your Google Sheet ID (get it from the URL)
             // Example URL: https://docs.google.com/spreadsheets/d/1ABC123XYZ/edit
            // Sheet ID is: 1ABC123XYZ
            const SHEET_ID = 'YOUR_ACTUAL_GOOGLE_SHEET_ID';

3. **Replace it** with your actual Google Sheet ID so it should looks like:
      **javascript**
   const SHEET_ID = '1aB2c3D4eF5g'; // Your actual ID here

4. **Save the file** and re-upload to GitHub



## 🧪 Testing & Launch

### Test 1: Form Submission
1. Go to your GitHub Pages URL
2. Fill out the form completely
3. Click "Submit Incident Report"
4. You should see: "Report submitted successfully!"

### Test 2: Check Database
1. Open your Google Sheet
2. You should see a new row with today's date and your test data

### Test 3: Check Alerts
1. Check your Telegram channel - you should see an alert
2. Check your email - you should receive an email

### Test 4: Check Dashboard
1. Go to your dashboard: `https://username.github.io/security-portal/dashboard.html`
2. You should see your test incident in the table



## 🔧 Troubleshooting

**Problem**: **Form shows error**
**Solution**: Check your Make.com webhook URL is correct in `index.html`

**Problem**: **No data in Google Sheet**
**Solution**: 1. Check Make.com scenario is ON (blue toggle)<br>2. Check Google Sheets connection in Make.com

**Problem**: **No Telegram alert**
**Solution**: 1. Bot is admin in channel?<br>2. Channel ID correct?<br>3. Bot token correct?

**Problem**: **Dashboard shows "No data"**
**Solution**: 1. Google Sheet shared publicly?<br>2. Sheet ID correct in `dashboard.html`<br>3. Column headers exactly as specified?

**Problem**: **Priority always shows "Low"**
**Solution**: In Make.com, use `trim(lower(2.Priority))` in email HTML

**Problem**: **"Access denied" on dashboard**
**Solution**: Google Sheet → Share → "Anyone with link can VIEW"


## ❓ Frequently Asked Questions

**Q: Is this system secure?**  
A: Yes. Google Sheets has view-only access. No sensitive data is stored on GitHub (only HTML files).

**Q: Can multiple people use this?**  
A: Yes! Share the portal link with your team. All reports go to the same dashboard.

**Q: What if I exceed free limits?**  
A: Make.com free tier has 1,000 operations/month. Google Sheets and GitHub Pages are completely free.

**Q: How do I update the system?**  
A: Just edit the HTML files and re-upload to GitHub. Changes go live instantly.

**Q: Can I customize the incident types?**  
A: Yes! Edit the dropdown options in `index.html`.



## 🆘 Need Help?

If you get stuck at any step:

1. **Double-check** you followed each step exactly
2. **Compare** your setup with the screenshots/variable names
3. **Contact support** by opening an issue in the GitHub repository


## 📊 System Architecture

User Submits Form
        ↓
(index.html - GitHub Pages)
        ↓
(Make.com Webhook Receives Data)
        ↓
        ├──→ Saves to Google Sheets (Database)
        ├──→ Sends Telegram Alert (Mobile)
        └──→ Sends Email Alert (Inbox)
                ↓
(dashboard.html - GitHub Pages)
        ↓
(Reads from Google Sheets)
        ↓
Displays Real-time Dashboard


## 🎉 Congratulations!

Your complete Security Incident Response System is now live. You have:

✅ **Web Portal** for reporting incidents  
✅ **Automated Database** in Google Sheets  
✅ **Mobile Alerts** via Telegram  
✅ **Email Notifications**  
✅ **Live Dashboard** for monitoring  

**Your Portal URLs:**
- Reporting Form: `https://[your-username].github.io/security-portal/`
- Dashboard: `https://[your-username].github.io/security-portal/dashboard.html`

**Next Steps:**
1. Bookmark both URLs
2. Test with a few sample reports
3. Share the portal link with your team
4. Monitor the dashboard regularly


**Last Updated: [Current Date]**
**System Version: 2.0**  
**For support, open an issue in the GitHub repository.**
