[README.md](https://github.com/user-attachments/files/25162681/README.md)
# Workout Tracker - Setup Instructions

A mobile-friendly workout tracker with Firebase backend for cross-device synchronization.

## Features
- ✅ Log workouts with weight and reps
- 📊 Track progress over time with graphs
- 💾 Export/Import CSV data
- ☁️ Cross-device sync via Firebase
- 📱 Mobile-optimized interface

## Setup Instructions

### Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Enter a project name (e.g., "workout-tracker")
4. Disable Google Analytics (optional)
5. Click "Create project"

### Step 2: Set Up Firestore Database

1. In your Firebase project, click "Firestore Database" in the left sidebar
2. Click "Create database"
3. Choose **"Start in production mode"**
4. Select a location closest to you
5. Click "Enable"

### Step 3: Configure Security Rules

1. In Firestore, go to the "Rules" tab
2. Replace the rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /workouts/{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Click "Publish"

**Note:** These rules allow anyone to read/write. For production, you should add authentication.

### Step 4: Get Firebase Configuration

1. In Firebase Console, click the gear icon ⚙️ next to "Project Overview"
2. Click "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon `</>`
5. Register your app with a nickname (e.g., "Workout Tracker Web")
6. Copy the `firebaseConfig` object

### Step 5: Update the HTML File

1. Open `workout-tracker.html`
2. Find the Firebase configuration section (around line 215):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

3. Replace with your actual Firebase config values

### Step 6: Deploy to GitHub Pages

#### Option A: Using GitHub Website

1. Go to [GitHub](https://github.com) and create a new repository
2. Name it `workout-tracker` (or any name you prefer)
3. Make it **Public**
4. Click "uploading an existing file"
5. Upload `workout-tracker.html`
6. Rename it to `index.html` after upload
7. Go to repository Settings → Pages
8. Under "Source", select "main" branch
9. Click "Save"
10. Your site will be live at: `https://YOUR_USERNAME.github.io/workout-tracker/`

#### Option B: Using Git Command Line

```bash
# Create a new repository on GitHub first, then:
git clone https://github.com/YOUR_USERNAME/workout-tracker.git
cd workout-tracker

# Copy your updated workout-tracker.html file here and rename it
cp path/to/workout-tracker.html index.html

git add index.html
git commit -m "Initial commit - workout tracker"
git push origin main

# Enable GitHub Pages in repository settings
```

### Step 7: Access Your App

Visit your GitHub Pages URL:
- `https://YOUR_USERNAME.github.io/workout-tracker/`

Add it to your phone's home screen for easy access:
- **iPhone**: Safari → Share → "Add to Home Screen"
- **Android**: Chrome → Menu → "Add to Home Screen"

## Usage

### Logging Workouts
1. Go to "Log" tab
2. Select an exercise
3. View your last workout for reference
4. Enter weight and reps
5. Click "Add Entry"

### Viewing Progress
1. Go to "Progress" tab
2. Filter by muscle group (optional)
3. View graphs showing weight progression
4. See your latest workout for each exercise

### Data Management
1. Go to "Data" tab
2. **Export**: Download all data as CSV
3. **Import**: Upload a CSV to restore/add data
4. **Clear**: Delete all workout data

## Troubleshooting

### Data Not Syncing
- Check browser console for errors (F12)
- Verify Firebase config is correct
- Ensure Firestore rules are published

### Can't Save Workouts
- Check Firebase Firestore is enabled
- Verify security rules allow writes
- Check browser console for errors

### Graphs Not Showing
- Ensure you have multiple data points for an exercise
- Try refreshing the page
- Check browser console for errors

## Data Format

CSV Export format:
```
Muscle Group,Exercise,Equipment,Weight (lbs),Reps,Date
CHEST,Bench Press,Barbell,225,8,2024-02-08
```

## Security Considerations

The current setup allows **anyone with the URL** to read and write data. For better security:

1. Enable Firebase Authentication
2. Update Firestore rules to require authentication
3. Add user-specific data separation

## License

Free to use and modify for personal use.
