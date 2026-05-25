# HESCOM Web Admin Portal Deployment Guide

This folder contains a fully self-contained HTML/CSS/JS application that allows you to log in with your admin account credentials, select Excel spreadsheets, parse them, and upload/sync them to your Firebase Realtime Database in the exact format required by the Android application.

## Prerequisites
* The website is fully configured using your project's Firebase details from the `google-services.json` file.
* You need to have an Admin user account created in Firebase (i.e. an account registered through the Android app whose email address contains `"admin"`, e.g., `admin@example.com`, or one that you manually set `role` to `"admin"` under the database `/users/{uid}/role` path).

---

## Hosting on GitHub Pages (Free)

To publish this website on GitHub Pages so you can access it from any browser, follow these simple steps:

### Option A: Via GitHub Desktop or Web Interface
1. Create a new public or private repository on GitHub (e.g., named `hescom-admin`).
2. Upload the `index.html` file from the `web-admin/` folder to the root of that repository.
3. In your repository on GitHub:
   * Go to **Settings** (top tab).
   * Click on **Pages** in the left-hand sidebar (under the "Code and automation" section).
   * Under **Build and deployment**, set the Source to **Deploy from a branch**.
   * Under **Branch**, select `main` (or `master`) and folder `/ (root)`.
   * Click **Save**.
4. Within 1-2 minutes, GitHub will give you a live URL (e.g., `https://<your-username>.github.io/hescom-admin/`).

---

### Option B: Via Command Line (Git Bash / PowerShell)
If you have Git installed, run these commands in this directory:
```bash
git init
git add index.html
git commit -m "Initial commit for HESCOM admin website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
git push -u origin main
```
Then follow Step 3 above on GitHub to enable Pages.

---

## Security & Verification Details
* **Admin Verification**: The website performs two checks when a user logs in:
  1. Checks if the user exists and is authenticated via Firebase Auth.
  2. Pulls their database record from `/users/{uid}` and checks that `banned` is not true, and `role` is exactly `"admin"`. If not, it triggers `auth.signOut()` and displays *"Access denied. You are not an admin."*
* **Automatic Column Mapping**: The web portal implements the identical dynamic column mapping algorithm as the Android app (detects matching columns for `rrNo`, `conId`, `customerName`, `tcAreaName`, `mrGvpName`, `tariff`, `phoneNo`, `status`, `serviceDate`, and `onlinePayUrl`).
