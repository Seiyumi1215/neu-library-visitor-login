# 📚 NEU Library Visitor Log (Firebase Version)

A secure, modern, and responsive visitor logging system for the NEU Library. Built with HTML, JavaScript, Tailwind CSS, and Firebase.

---

# 🚀 Live Deployment

View Live App *(add your Firebase Hosting link here)*

---

# ✨ Features

## 🔐 Authentication

* Google Authentication via Firebase Auth
* Restricts login to **@neu.edu.ph institutional email only**

---

## 👥 Role-Based Access

### 🎓 Student (Kiosk Mode)

* Login using Google account
* Must use **@neu.edu.ph email**
* Select:

  * College/Program
  * Purpose of Visit (Reading, Studying, Researching, Use of Computer)
* Automatically logs **date and time**
* Displays: **"Welcome to NEU Library!"** after submission

---

### 🛠️ Admin

* Login using authorized admin email
* Access to **Admin Dashboard**
* View all visitor logs
* Search records by:

  * Email
  * Course
  * Purpose
* *(Optional)* Filter by date
* *(Optional)* Block users

---

## 📊 Admin Dashboard

* Displays visitor records:

  * Email
  * Course/Program
  * Purpose of Visit
  * Date & Time
* Real-time data from Firebase Firestore
* Search bar for filtering
* *(Optional Upgrade)* Dashboard cards:

  * Total Visitors per Day
  * Most Common Purpose
  * Course Distribution

---

## 🖥️ Kiosk System

* Simple and fast student interface
* No student dashboard (kiosk-only mode)
* Designed for quick entry logging

---

## 📱 Responsive Design

* Works on desktop and mobile
* Suitable for kiosk deployment

---

# 🛠️ Tech Stack

* **Frontend:** HTML, JavaScript, Tailwind CSS
* **Backend / Database:** Firebase Firestore
* **Authentication:** Firebase Auth (Google Sign-In)
* **Hosting:** Firebase Hosting

---

# ⚙️ Installation & Setup

## 1. Clone the repository

```bash
git clone https://github.com/your-username/neu-library-visitor-log.git
cd neu-library-visitor-log
```

---

## 2. Firebase Setup

1. Go to Firebase Console
2. Create a new project
3. Enable:

   * **Authentication → Google Sign-In**
   * **Firestore Database**

---

## 3. Firebase Configuration

Create a file:

📁 `js/firebase.js`

```javascript
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getAuth, GoogleAuthProvider } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
import { getFirestore } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
};

const app = initializeApp(firebaseConfig);

export const auth = getAuth(app);
export const provider = new GoogleAuthProvider();
export const db = getFirestore(app);
```

---

## 4. Firestore Database Structure

Create a collection:

📂 `logs`

Each document:

```json
{
  "email": "student@neu.edu.ph",
  "course": "BS Information Technology",
  "purpose": "Studying",
  "time": "timestamp"
}
```

---

## 5. Firestore Security Rules

Go to **Firestore → Rules** and paste:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /logs/{doc} {
      allow create: if true;
      allow read: if request.auth != null;
    }

  }
}
```

---

## 6. Run the Application

Option 1 (Recommended - Live Server):

* Right click `index.html`
* Open with Live Server

Option 2 (Vite or Node):

```bash
npm install
npm run dev
```

---

# 🔐 Admin Account

The system identifies admin using email:

```
jcesperanza@neu.edu.ph
```

Example check in code:

```javascript
if (user.email === "jcesperanza@neu.edu.ph") {
  window.location.href = "admin.html";
}
```

---

# 🚫 Block User Feature (Optional)

Create a collection:

📂 `blocked_users`

Example document:

```json
{
  "email": "blocked@neu.edu.ph"
}
```

Then check before allowing login:

```javascript
// If email exists in blocked_users → deny access
```

---

# 📦 Future Improvements

* 📊 Charts (Bar & Pie)
* 📅 Date filtering
* 📤 Export to CSV
* 🪪 RFID integration
* 🎨 Full UI enhancement using Tailwind
* 🔒 Stronger Firestore security rules

---

# 📝 License

This project is licensed under the **Apache-2.0 License**.

---

# 👨‍💻 Author

Developed for NEU Library System Project
