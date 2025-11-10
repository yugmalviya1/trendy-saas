# Vercel Deployment Guide

## 🚀 Deploy Your Trendy SaaS App to Vercel

### Prerequisites
- ✅ GitHub repository (already set up)
- ✅ Vercel account (sign up at https://vercel.com)
- ✅ Firebase project configured

---

## 📝 Deployment Steps

### 1. Push to GitHub
```bash
git add .
git commit -m "Ready for deployment"
git push
```

### 2. Import Project to Vercel

1. Go to https://vercel.com/new
2. Click **"Import Git Repository"**
3. Select your GitHub repo: `yugmalviya1/trendy-saas`
4. Click **"Import"**

### 3. Configure Environment Variables

In Vercel project settings, add these environment variables:

```
NEXT_PUBLIC_FIREBASE_API_KEY=AIzaSyBwDd08cOdZRrc7SG51_BMTe1tAKnDiZtI
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=trendy-saas-a59aa.firebaseapp.com
NEXT_PUBLIC_FIREBASE_DATABASE_URL=https://trendy-saas-a59aa-default-rtdb.firebaseio.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=trendy-saas-a59aa
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=trendy-saas-a59aa.firebasestorage.app
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=376929802779
NEXT_PUBLIC_FIREBASE_APP_ID=1:376929802779:web:a44fea7323721d605476be
```

**How to add:**
- Go to your Vercel project
- Click **Settings** → **Environment Variables**
- Add each variable one by one
- Click **Save**

### 4. Deploy

Click **"Deploy"** and wait for the build to complete!

---

## ⚙️ Build Settings (Auto-detected)

Vercel will automatically detect:
- **Framework**: Next.js
- **Build Command**: `npm run build`
- **Output Directory**: `.next`
- **Install Command**: `npm install`

No need to change these!

---

## 🔥 Firebase Configuration

### Update Firebase Authorized Domains

After deployment, add your Vercel domain to Firebase:

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select project: **trendy-saas-a59aa**
3. Go to **Authentication** → **Settings** → **Authorized domains**
4. Click **Add domain**
5. Add your Vercel domain: `your-app.vercel.app`
6. Click **Add**

---

## 🎯 Post-Deployment Checklist

### 1. Enable Firebase Services
- ✅ Enable Email/Password Authentication
- ✅ Create Firestore Database
- ✅ Create Realtime Database
- ✅ Set up Security Rules

### 2. Test Your Deployment
Visit these pages to verify everything works:
- `/` - Landing page
- `/home` - Home page
- `/signin` - Sign in
- `/signup` - Sign up
- `/test-auth` - Test authentication
- `/test-firebase` - Test Firestore
- `/test-realtime-db` - Test Realtime DB

### 3. Remove Test Pages (Optional)
For production, you may want to remove:
- `/test-auth`
- `/test-firebase`
- `/test-realtime-db`

---

## 🔒 Security Best Practices

### 1. Firebase Security Rules

**Firestore Rules:**
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    match /{document=**} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
  }
}
```

**Realtime Database Rules:**
```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
```

### 2. Environment Variables
- ✅ Never commit `.env.local` to Git
- ✅ Always use environment variables in Vercel
- ✅ Rotate API keys if exposed

---

## 🐛 Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Ensure all dependencies are in `package.json`
- Verify environment variables are set

### Authentication Not Working
- Enable Email/Password in Firebase Console
- Add Vercel domain to Firebase Authorized domains
- Check Firebase credentials in environment variables

### Database Connection Issues
- Verify Firebase databases are created
- Check security rules
- Ensure environment variables are correct

---

## 📊 Monitoring

### Vercel Analytics
Enable in: **Project Settings** → **Analytics**

### Firebase Console
Monitor:
- Authentication users
- Database usage
- Storage usage
- Error logs

---

## 🔄 Continuous Deployment

Vercel automatically deploys when you push to GitHub:

```bash
git add .
git commit -m "Update feature"
git push
```

Vercel will:
1. Detect the push
2. Build your app
3. Deploy automatically
4. Provide a preview URL

---

## 🎉 Your App is Live!

Your Trendy SaaS app will be available at:
- **Production**: `https://your-app.vercel.app`
- **Custom Domain**: Configure in Vercel settings

---

## 📚 Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Next.js Deployment](https://nextjs.org/docs/deployment)
- [Firebase Documentation](https://firebase.google.com/docs)
- [Vercel Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables)

---

## 💡 Tips

1. **Use Preview Deployments**: Every branch gets a preview URL
2. **Set up Custom Domain**: Add your own domain in Vercel settings
3. **Enable Analytics**: Track your app's performance
4. **Monitor Logs**: Check Vercel logs for errors
5. **Use Edge Functions**: For better performance

Happy Deploying! 🚀
