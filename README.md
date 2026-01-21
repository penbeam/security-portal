# Corporate Security Incident Portal

A professional security incident reporting system with automated alerts and dashboard.

## 🌐 Live Demo
- **Report Form:** https://penbeam.github.io/security-portal/
- **Dashboard:** https://penbeam.github.io/security-portal/dashboard.html

## 🚀 Features
- Professional web form for incident reporting
- Automated logging to Google Sheets
- Real-time Telegram alerts
- Professional HTML email notifications
- Mobile-responsive design
- Security dashboard with statistics

## 🛠️ Tech Stack
- **Frontend:** HTML, CSS, JavaScript (GitHub Pages)
- **Automation:** Make.com (free tier)
- **Database:** Google Sheets
- **Alerts:** Telegram Bot API, Email

## 📊 How It Works
1. Employee submits incident via web form
2. Data sent to Make.com automation
3. Incident logged to Google Sheets
4. Telegram alert sent to security team
5. Professional email notification sent
6. Dashboard updates with new incident

## 🔧 Setup Instructions

### 1. Google Sheets Setup
- Create spreadsheet with headers: Case ID, Timestamp, Status, Reporter Name, etc.
- Share with Make.com (Editor access)

### 2. Telegram Bot Setup
- Create bot via @BotFather
- Save API token
- Create private channel and add bot as admin

### 3. Make.com Setup
- Create webhook for form data
- Add Google Sheets module to log incidents
- Add Telegram module for alerts
- Add Email module for notifications

### 4. Form Setup
- Update webhook URL in index.html
- Deploy to GitHub Pages

## 📱 Mobile Support
- Fully responsive design
- Works on all devices
- Touch-friendly interface

## 📧 Contact
For questions about this security system, contact the Security Department.

---
*Built with free tools for corporate security operations*
