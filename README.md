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

## Deploy to Custom Domain

### Option 1: GitHub Pages with Custom Domain (Recommended)

**Step 1: Configure Custom Domain in GitHub**
1. Go to your repo → Settings → Pages
2. Under "Custom domain", enter your domain (e.g., `financialplanner.com` or `app.financialplanner.com`)
3. Click "Save"
4. GitHub will create a `CNAME` file (or you can create it manually)

**Step 2: Configure DNS**
For a **root domain** (e.g., `financialplanner.com`):
```
Type: A
Name: @
Value: 185.199.108.153
              185.199.109.153
              185.199.110.153
              185.199.111.153
```

For a **subdomain** (e.g., `app.financialplanner.com`):
```
Type: CNAME
Name: app
Value: <your-username>.github.io
```

**Step 3: Update Firebase Authorized Domains**
1. Go to Firebase Console → Authentication → Settings → Authorized domains
2. Add your custom domain: `financialplanner.com` or `app.financialplanner.com`
3. Save

**Step 4: Enable HTTPS (Auto by GitHub)**
- GitHub Pages automatically provides SSL certificates via Let's Encrypt
- Wait 24-48 hours after DNS propagation
- Check SSL status in repo Settings → Pages

### Option 2: Netlify/Vercel (Alternative)

**Netlify:**
1. Sign up at netlify.com
2. Drag & drop your `index.html` or connect GitHub repo
3. Add custom domain in Site settings → Domain management
4. Update Firebase authorized domains

**Vercel:**
1. Sign up at vercel.com
2. Import GitHub repository
3. Add custom domain in Project settings
4. Update Firebase authorized domains

### Option 3: Own Server/Hosting

1. Upload `index.html` to your web server
2. Ensure HTTPS is enabled (required for Firebase)
3. Update Firebase authorized domains
4. Configure server to serve `index.html` for all routes (SPA routing)

### Post-Deployment Checklist

✅ DNS configured and propagated (check with `nslookup`)  
✅ Custom domain added to Firebase authorized domains  
✅ HTTPS enabled (required for Firebase Auth)  
✅ Test authentication (Google Sign-In, Email/Password)  
✅ Test Firestore writes/reads  
✅ Verify CORS settings if using APIs  

**Note:** DNS propagation can take 24-48 hours. Check status with:
```bash
dig financialplanner.com
# or
nslookup financialplanner.com
```

## Notes
- All CSS/JS is embedded in `index.html`. Uses CDNs for Firebase, Chart.js, Font Awesome.
- Password tools: strength indicator, generator, and optional local saved-passwords manager.
- **Important:** Firebase requires HTTPS for production. Ensure your custom domain has SSL enabled.


