# Financial Planner Pro

A single-file, production-ready personal finance planner with Firebase Authentication and Firestore sync, Material Design 3.0 UI, Chart.js reports, and GitHub Pages-friendly deploy.

## Features
- Firebase Auth (Google + Email/Password), password reset, profile view
- Income tracker with variable increments, Expense tracker with inflation categories
- 8 pre-defined goals with progress bars, status badges, and monthly contribution
- Chart.js dashboards, JSON export, night mode, responsive UI

## Setup
1) Open `index.html` and replace the placeholder Firebase config with your project keys:
   - `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`

2) Firestore Rules (user-owned data):
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Local Preview
Just open `index.html` in your browser. For auth redirects, prefer a simple static server:
```
python3 -m http.server 8000
# or
npx serve .
```

## Deploy to GitHub Pages
1) Create a new repo on GitHub named `financial-planner-pro`.
2) Push the code:
```
git init
git add .
git commit -m "Initial commit: Financial Planner Pro"
git branch -M main
git remote add origin https://github.com/<your-username>/financial-planner-pro.git
git push -u origin main
```
3) In GitHub → Settings → Pages → Build and deployment:
   - Source: Deploy from a branch
   - Branch: `main` / root

Once published, your app will be available at:
`https://<your-username>.github.io/financial-planner-pro/`

## Notes
- All CSS/JS is embedded in `index.html`. Uses CDNs for Firebase, Chart.js, Font Awesome.
- Password tools: strength indicator, generator, and optional local saved-passwords manager.


