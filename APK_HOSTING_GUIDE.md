# APK Hosting Guide for Vercel

The APK file isn't showing up on your Vercel site because:
1. Java isn't installed yet (needed to build the APK)
2. APK files are typically too large for git repositories
3. Vercel has file size limits for deployments

## Best Solution: GitHub Releases

Instead of hosting the APK on Vercel, use GitHub Releases (free, unlimited storage for release files):

### Step 1: Install Java & Build APK

```bash
# Install Java
brew install openjdk@17
export JAVA_HOME=$(/usr/libexec/java_home -v 17)

# Build APK
cd /Users/nelson/projects/rial/android-sdk
./gradlew assembleDebug

# APK will be at:
# sample-app/build/outputs/apk/debug/sample-app-debug.apk
```

### Step 2: Create GitHub Release

```bash
# Go to your zkimg-website repo
cd /Users/nelson/projects/zkimg-website

# Create and push a tag
git tag -a v0.1.0 -m "Release v0.1.0 - Android app"
git push origin v0.1.0
```

### Step 3: Upload APK to GitHub Release

1. Go to: `https://github.com/YOUR_USERNAME/zkimg-website/releases/new`
2. Select tag: `v0.1.0`
3. Title: "Rial Android App v0.1.0"
4. Upload the APK file:
   - From: `/Users/nelson/projects/rial/android-sdk/sample-app/build/outputs/apk/debug/sample-app-debug.apk`
   - Rename to: `rial-app-v0.1.0.apk`
5. Click "Publish release"

### Step 4: Update download.html

The GitHub release URL will be:
```
https://github.com/YOUR_USERNAME/zkimg-website/releases/download/v0.1.0/rial-app-v0.1.0.apk
```

Update `download.html`:

```html
<a href="https://github.com/YOUR_USERNAME/zkimg-website/releases/download/v0.1.0/rial-app-v0.1.0.apk"
   class="download-btn"
   id="download-apk"
   download="rial-app-v0.1.0.apk">
    Download APK (v0.1.0)
</a>
```

Then commit and push:
```bash
git add download.html
git commit -m "Update APK download link to GitHub release"
git push
```

Vercel will auto-deploy the updated page!

## Alternative: Use External CDN

If you prefer not to use GitHub Releases:

### Option 1: Firebase Hosting (Free)
```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login and init
firebase login
firebase init hosting

# Upload APK
firebase deploy --only hosting
```

### Option 2: Cloudflare R2 (Free tier)
- Upload APK to R2 bucket
- Get public URL
- Update download.html with URL

### Option 3: Google Drive (Quick & Free)
1. Upload APK to Google Drive
2. Make it public
3. Use direct download link in download.html

## Current Workaround

Until you build the APK, the download page shows:
- ✅ "Coming Soon" button (disabled)
- ✅ "Build from Source" option (working)
- ✅ Link to GitHub repo

## Quick Commands

Once Java is installed:

```bash
# 1. Build APK
cd /Users/nelson/projects/rial/android-sdk && ./gradlew assembleDebug

# 2. Create release tag
cd /Users/nelson/projects/zkimg-website
git tag v0.1.0
git push origin v0.1.0

# 3. Upload APK at:
# https://github.com/YOUR_USERNAME/zkimg-website/releases/new

# 4. Update download.html with release URL

# 5. Push changes
git add download.html
git commit -m "Add APK download link"
git push
```

## Why Not Commit APK to Git?

❌ APK files are ~15MB (too large for git)
❌ Git LFS costs money on most platforms
❌ Makes repository bloated
❌ Slows down clone/push operations

✅ GitHub Releases are FREE and designed for binary files
✅ Unlimited storage for release artifacts
✅ Fast CDN delivery
✅ Version tracking built-in

---

**Next Step**: Install Java with `brew install openjdk@17`
