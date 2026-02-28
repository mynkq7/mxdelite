# Firebase CMS Setup Guide

## Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **Create a project** → name it "Mxdelite"
3. Enable **Google Analytics** (optional)
4. Wait for project creation

## Step 2: Get Firebase Credentials

1. In Firebase Console, click the **gear icon** → **Project Settings**
2. Scroll down to "Your apps" → click **Web** icon (or add app)
3. Copy the Firebase config object
4. Paste it into `firebase-config.js` replacing the placeholder values:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY_HERE",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef123456"
};
```

## Step 3: Enable Firestore Database

1. In Firebase Console → **Build** → **Firestore Database**
2. Click **Create database**
3. Start in **Production mode** 
4. Choose a region close to you
5. Click **Create**

## Step 4: Set Firestore Security Rules

1. In Firestore → **Rules** tab
2. Replace the default with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /content/pages {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

3. Click **Publish**

## Step 5: Enable Authentication

1. Firebase Console → **Build** → **Authentication**
2. Click **Get started** → **Email/Password**
3. Toggle **Enabled** → **Save**

## Step 6: Create Admin User

1. Auth → **Users** tab
2. Click **Add user**
3. Enter email and password for your admin account
4. Click **Add user**

## Step 7: Initialize Firestore Content

1. In Firestore → **Collections** → **+ Create collection**
2. Name it: `content`
3. Add document with ID: `pages`
4. Click **+ Add field** and add this structure:

```
{
  "hero": {
    "eyebrow": "Websites — Social Media — Brand Identity",
    "title": "Your Brand",
    "outline": "Elevated",
    "subtitle": "Built for businesses that refuse to be ordinary...",
    "buttonText": "Start Your Project"
  },
  "services": [
    {
      "title": "Websites",
      "description": "Custom-built, high-performance websites..."
    },
    {
      "title": "Social Media",
      "description": "A consistent, considered presence..."
    },
    {
      "title": "Brand Identity",
      "description": "Logos, color systems, typography..."
    }
  ],
  "why": {
    "text": "We do not do average. Every project is built from scratch...",
    "stat1": "100%",
    "stat2": "3x",
    "stat3": "0",
    "stat4": "Full"
  },
  "process": [
    {
      "title": "Discovery",
      "description": "We learn your business, your audience, and your vision..."
    },
    {
      "title": "Strategy",
      "description": "We map out what to build, how it looks..."
    },
    {
      "title": "Build",
      "description": "We design and develop with precision..."
    },
    {
      "title": "Launch",
      "description": "We deliver a finished, polished product..."
    }
  ],
  "contact": {
    "email": "mxdelitehq@gmail.com",
    "instagram": "@mxdelite",
    "location": "Available Worldwide"
  },
  "footer": {
    "copyright": "© 2025 Mxdelite. All rights reserved."
  }
}
```

## Step 8: Access the Admin Panel

1. Open `admin.html` from your local machine or server
2. Login with your admin email and password
3. Edit any section and click **Save Changes**
4. Changes appear on the main site instantly

## How It Works

- **Main Site** (`index.html`): Fetches and displays content from Firestore on page load
- **Admin Panel** (`admin.html`): Login required to edit content
- **Fallback**: If Firestore is down, site shows hardcoded content
- **Real-time**: Once saved, changes appear immediately

## Troubleshooting

**"Firebase is not defined"**
- Make sure `firebase-config.js` is in the same folder as `index.html` and `admin.html`
- Check Firebase CDN scripts loaded correctly

**"Authentication failed"**
- Verify admin user created in Firebase Console
- Check email/password are correct

**"Content not updating"**
- Check Firestore has `content/pages` document
- Verify Security Rules allow read access

**Need help?**
- Firebase Docs: https://firebase.google.com/docs
- Firestore Setup: https://firebase.google.com/docs/firestore/quickstart
