# Download Page Setup

A professional download page has been added to the zkimg-website for the Rial Android app.

## What Was Added

### New Files
- **[download.html](download.html)** - Complete Android app download page

### Modified Files
- **[index.html](index.html)** - Updated navigation to link to download page
  - Changed "Get Started" button to "Download App"
  - Hero CTA now links to download page

## Features of the Download Page

### 1. Download Options
- **Direct APK Download** - Button for downloading the APK file
- **Build from Source** - Links to GitHub repository

### 2. Feature Showcase
Highlights all production-ready features:
- AI Fraud Detection (95%+ accuracy)
- Hardware Security (Android Keystore)
- Image Transformations (15+ operations)
- GPS & Timestamp Proofs
- Zero-Knowledge Proofs
- Blockchain Ready

### 3. Technical Specifications
Complete specs table including:
- Version: 0.1.0 Beta
- Android 7.0+ (API 24+)
- Target: Android 14 (API 34)
- App size: ~15 MB
- Proof system: Groth16/Halo2
- Detection accuracy: 95%+

### 4. Installation Guides
Two methods provided:
1. **Direct APK Install** - Step-by-step for non-technical users
2. **Build from Source** - For developers

### 5. System Requirements
Clear list of requirements:
- Android version
- Permissions needed
- Storage requirements
- Internet connection

### 6. Support Section
Links to:
- Documentation
- GitHub Issues
- Contact form

## Viewing the Page

### Local Development
```bash
cd /Users/nelson/projects/zkimg-website

# Serve locally
python3 -m http.server 8000

# Open in browser
open http://localhost:8000/zkimg-website/download.html
```

### Direct File
```bash
# Open the HTML file directly
open /Users/nelson/projects/zkimg-website/download.html
```

## Deploying the APK

The download page includes a placeholder for APK downloads. To enable actual downloads:

### Option 1: GitHub Releases (Recommended)

1. **Build the APK**:
   ```bash
   cd /Users/nelson/projects/rial/android-sdk
   ./gradlew assembleRelease
   ```

2. **Create GitHub Release**:
   ```bash
   # Tag the release
   git tag -a v0.1.0 -m "Release v0.1.0"
   git push origin v0.1.0

   # Upload APK via GitHub web interface
   # Go to: https://github.com/windsurftemplate/rial/releases/new
   # Upload: android-sdk/sample-app/build/outputs/apk/release/sample-app-release.apk
   ```

3. **Update download.html**:
   ```javascript
   // In download.html, uncomment this line and update URL:
   window.location.href = 'https://github.com/windsurftemplate/rial/releases/download/v0.1.0/rial-sample-app.apk';
   ```

### Option 2: Direct Hosting

1. **Upload APK to web hosting**:
   - Upload to your web server
   - Or use services like Firebase Hosting, Netlify, etc.

2. **Update download link**:
   ```html
   <a href="/path/to/rial-sample-app.apk" class="download-btn" download>
       Download APK (v0.1.0)
   </a>
   ```

### Option 3: Google Play Store (Future)

For wider distribution:
1. Create Google Play Developer account
2. Build signed release APK
3. Upload to Play Store Console
4. Update download page to link to Play Store

## Customization

### Update Version Number

Search and replace `v0.1.0` with your version number in:
- Download badge
- Download buttons
- Specs table
- Installation instructions

### Change Backend URL

If using a different backend:
```html
<!-- In download.html -->
<tr>
    <td>Backend API</td>
    <td>Your Backend URL</td>
</tr>
```

### Update Features

Edit the features grid in download.html:
```html
<div class="feature-item">
    <div class="feature-icon">🆕</div>
    <h4>New Feature</h4>
    <p>Description of new feature</p>
</div>
```

## SEO and Metadata

The download page includes:
- Proper meta tags for SEO
- Open Graph tags (can be added)
- Descriptive title and description
- Semantic HTML structure

### Add Open Graph Tags (Optional)

```html
<meta property="og:title" content="Download Rial Android App">
<meta property="og:description" content="Zero-knowledge image authentication">
<meta property="og:image" content="https://yoursite.com/images/og-image.png">
<meta property="og:url" content="https://yoursite.com/download.html">
```

## Analytics (Optional)

To track downloads, add:

```javascript
document.getElementById('download-apk').addEventListener('click', function(e) {
    // Track with Google Analytics
    gtag('event', 'download', {
        'event_category': 'APK',
        'event_label': 'v0.1.0'
    });

    // Or Plausible Analytics
    plausible('Download', {props: {version: 'v0.1.0'}});

    window.location.href = 'your-apk-url';
});
```

## Mobile Optimization

The download page is fully responsive:
- Mobile-first design
- Touch-friendly buttons
- Readable on all screen sizes
- Fast loading time

Test on mobile:
```bash
# Use Chrome DevTools mobile emulation
# Or scan QR code to test on real device
```

## QR Code for Easy Mobile Download

Generate a QR code for the download page:

```bash
# Install qrencode
brew install qrencode

# Generate QR code
qrencode -o download-qr.png "http://yoursite.com/download.html"
```

Add to website:
```html
<img src="download-qr.png" alt="Scan to download">
<p>Scan with your phone to download</p>
```

## Integration with Main Site

The download page is integrated with the main site:

1. **Navigation** - "Download App" button in nav bar
2. **Hero CTA** - Main call-to-action button
3. **Consistent Styling** - Uses same styles.css
4. **Footer** - Includes download link

## Beta Warning

The page includes a prominent beta warning:
```html
<div style="background: #fef3c7; border-left: 4px solid #f59e0b;">
    <h4>⚠️ Beta Software Notice</h4>
    <p>This is beta software for testing purposes...</p>
</div>
```

Remove this when ready for production release.

## Next Steps

1. **Build Release APK**:
   ```bash
   cd /Users/nelson/projects/rial/android-sdk
   ./gradlew assembleRelease
   ```

2. **Sign APK** (for production):
   ```bash
   # Generate keystore
   keytool -genkey -v -keystore rial-release.keystore \
     -alias rial -keyalg RSA -keysize 2048 -validity 10000

   # Sign APK
   jarsigner -verbose -sigalg SHA256withRSA \
     -digestalg SHA-256 \
     -keystore rial-release.keystore \
     sample-app-release-unsigned.apk rial
   ```

3. **Upload to GitHub Releases**

4. **Update download.html with real APK URL**

5. **Test download flow on real device**

6. **Deploy website** (if not already deployed)

## Current Status

✅ Download page created
✅ Navigation updated
✅ Hero CTA updated
✅ Features documented
✅ Installation guides added
⏳ APK not yet uploaded (placeholder currently)
⏳ Waiting for release build

## Deployment

If using the same hosting as the main site:
```bash
# The page is ready to deploy with the rest of the site
# Just commit and push
git add download.html index.html DOWNLOAD_PAGE_SETUP.md
git commit -m "Add Android app download page"
git push
```

---

**Created**: November 2025
**Status**: Ready for APK upload
**APK Version**: 0.1.0 Beta
