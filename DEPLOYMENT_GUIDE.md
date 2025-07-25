# Netlify Deployment Guide - Retail-Lite POS

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Method 1: Drag & Drop Deployment](#method-1-drag--drop-deployment)
3. [Method 2: Git-based Deployment](#method-2-git-based-deployment)
4. [Method 3: Netlify CLI Deployment](#method-3-netlify-cli-deployment)
5. [Updating Your Site](#updating-your-site)
6. [Custom Domain Setup](#custom-domain-setup)
7. [Environment Configuration](#environment-configuration)
8. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### What You Need:
- ✅ A Netlify account (free at [netlify.com](https://netlify.com))
- ✅ Your website files (HTML, CSS, JS, images)
- ✅ A modern web browser
- ✅ (Optional) Git/GitHub account for advanced deployment

---

## Method 1: Drag & Drop Deployment (Easiest)

### Step 1: Prepare Your Files
1. **Download all your site files** (see download section below)
2. **Create a folder** called `retail-lite-pos`
3. **Place all files** in this folder:
   ```
   retail-lite-pos/
   ├── index.html
   ├── dashboard.html
   ├── Tuma-Biasahara-yako-ju.html
   ├── hero-1.png
   ├── Dashboard Retaillite.png
   ├── Retail-lite Pos Logo.png
   ├── web adds (1).png
   ├── web adds (2).png
   ├── web adds (3).png
   ├── web adds (4).png
   ├── web adds (5).png
   ├── web adds (6).png
   └── LICENSE
   ```

### Step 2: Create ZIP File
1. **Select all files** in your folder
2. **Right-click** → "Compress" or "Add to ZIP"
3. **Name it** `retail-lite-pos.zip`

### Step 3: Deploy to Netlify
1. **Go to** [netlify.com](https://netlify.com)
2. **Sign up/Login** to your account
3. **Click** "Add new site" → "Deploy manually"
4. **Drag and drop** your ZIP file OR browse and select it
5. **Wait** for deployment (usually 30-60 seconds)
6. **Your site is live!** You'll get a random URL like `amazing-pastry-123456.netlify.app`

### Step 4: Customize Your URL (Optional)
1. **Go to** Site settings → Site details
2. **Click** "Change site name"
3. **Enter** your preferred name: `retail-lite-pos`
4. **Your new URL:** `retail-lite-pos.netlify.app`

---

## Method 2: Git-based Deployment (Recommended)

### Step 1: Create GitHub Repository
1. **Go to** [github.com](https://github.com)
2. **Create** new repository named `retail-lite-pos`
3. **Make it public** (or private if you prefer)
4. **Don't** initialize with README (we'll upload existing files)

### Step 2: Upload Your Files
**Option A: GitHub Web Interface**
1. **Click** "uploading an existing file"
2. **Drag & drop** all your files
3. **Commit** with message: "Initial deployment"

**Option B: Git Command Line**
```bash
# Clone your repository
git clone https://github.com/YOUR_USERNAME/retail-lite-pos.git
cd retail-lite-pos

# Copy your files here
# Add, commit and push
git add .
git commit -m "Initial deployment"
git push origin main
```

### Step 3: Connect to Netlify
1. **Go to** Netlify dashboard
2. **Click** "Add new site" → "Import an existing project"
3. **Choose** "Deploy with GitHub"
4. **Authorize** Netlify to access GitHub
5. **Select** your `retail-lite-pos` repository
6. **Configure settings:**
   - Branch: `main`
   - Build command: (leave empty)
   - Publish directory: (leave empty or `/`)
7. **Click** "Deploy site"

### Benefits of Git Deployment:
- ✅ Automatic deployments when you push changes
- ✅ Version control and history
- ✅ Easy collaboration
- ✅ Rollback capabilities

---

## Method 3: Netlify CLI Deployment

### Step 1: Install Netlify CLI
```bash
# Install Node.js first (from nodejs.org)
# Then install Netlify CLI
npm install -g netlify-cli
```

### Step 2: Login and Deploy
```bash
# Navigate to your project folder
cd path/to/retail-lite-pos

# Login to Netlify
netlify login

# Deploy to a new site
netlify deploy

# Follow prompts:
# - Create & configure a new site
# - Publish directory: . (current directory)

# Deploy to production
netlify deploy --prod
```

---

## Updating Your Site

### For Drag & Drop Method:
1. **Make changes** to your local files
2. **Create new ZIP** file with updated files
3. **Go to** Netlify dashboard → Your site
4. **Click** "Deploys" tab
5. **Drag & drop** new ZIP file to deploy area
6. **Wait** for deployment to complete

### For Git-based Method:
1. **Make changes** to your local files
2. **Commit and push** changes:
   ```bash
   git add .
   git commit -m "Update: describe your changes"
   git push origin main
   ```
3. **Netlify automatically** rebuilds and deploys

### For CLI Method:
```bash
# Deploy changes
netlify deploy --prod
```

---

## Custom Domain Setup

### Step 1: Add Your Domain
1. **Go to** Site settings → Domain management
2. **Click** "Add custom domain"
3. **Enter** your domain (e.g., `retaillitepos.com`)
4. **Verify** ownership

### Step 2: Configure DNS
**Option A: Use Netlify DNS (Recommended)**
1. **Update nameservers** at your domain registrar
2. **Point to Netlify's nameservers:**
   ```
   dns1.p03.nsone.net
   dns2.p03.nsone.net
   dns3.p03.nsone.net
   dns4.p03.nsone.net
   ```

**Option B: Keep Current DNS**
1. **Add CNAME record:**
   ```
   CNAME www your-site-name.netlify.app
   ```
2. **Add A record for root domain:**
   ```
   A @ 75.2.60.5
   ```

### Step 3: Enable HTTPS
1. **Go to** Domain settings
2. **Click** "Verify DNS configuration"
3. **Enable** "Force HTTPS"
4. **SSL certificate** will be automatically provisioned

---

## Environment Configuration

### Create `netlify.toml` file:
```toml
[build]
  publish = "."

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[build.environment]
  NODE_VERSION = "18"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
```

### Add this file to your project root for enhanced functionality.

---

## Download Code for Manual Updates

### Method 1: Direct Download from Browser
1. **Right-click** on any page → "View Page Source"
2. **Copy** the HTML code
3. **Save** as `.html` file
4. **Repeat** for each page and asset

### Method 2: Browser Developer Tools
1. **Open** Developer Tools (F12)
2. **Go to** Sources tab
3. **Navigate** to your domain
4. **Right-click** files → "Save as"

### Method 3: Website Scraping Tools
**Using wget (Linux/Mac):**
```bash
wget --recursive --no-clobber --page-requisites --html-extension --convert-links --restrict-file-names=windows --domains your-site.netlify.app --no-parent https://your-site.netlify.app/
```

**Using HTTrack (Windows/Mac/Linux):**
1. **Download** HTTrack from [httrack.com](https://httrack.com)
2. **Install** and launch
3. **Enter** your site URL
4. **Configure** download settings
5. **Start** mirroring process

### Method 4: GitHub Download (If using Git)
1. **Go to** your GitHub repository
2. **Click** green "Code" button
3. **Select** "Download ZIP"
4. **Extract** files to your local machine

---

## Updating Workflow

### Daily Development Workflow:
```bash
# 1. Make changes locally
# 2. Test in browser
# 3. Commit changes
git add .
git commit -m "Feature: Add new functionality"

# 4. Push to GitHub (triggers auto-deploy)
git push origin main

# 5. Verify deployment on Netlify
```

### For Non-Git Users:
1. **Edit** files locally
2. **Test** changes in browser
3. **Create** new ZIP file
4. **Upload** to Netlify via drag & drop
5. **Verify** deployment

---

## Troubleshooting

### Common Issues:

#### 1. **Site Not Loading**
```
Problem: Blank page or 404 errors
Solution: 
- Check file names (case-sensitive)
- Ensure index.html is in root directory
- Verify all file paths in HTML
```

#### 2. **Images Not Showing**
```
Problem: Broken image links
Solution:
- Check image file paths
- Ensure images are uploaded
- Verify file extensions match
```

#### 3. **JavaScript Errors**
```
Problem: Functionality not working
Solution:
- Check browser console for errors
- Verify script tags are correct
- Ensure all dependencies are included
```

#### 4. **CSS Not Loading**
```
Problem: No styling applied
Solution:
- Check CSS file paths
- Verify style tags are in <head>
- Ensure CSS files are uploaded
```

#### 5. **Custom Domain Issues**
```
Problem: Domain not working
Solution:
- Wait 24-48 hours for DNS propagation
- Verify DNS records are correct
- Check domain registrar settings
```

### Getting Help:
- 📧 **Netlify Support:** support@netlify.com
- 📚 **Documentation:** [docs.netlify.com](https://docs.netlify.com)
- 💬 **Community Forum:** [community.netlify.com](https://community.netlify.com)

---

## Performance Optimization

### Before Deployment:
1. **Compress images** (use tools like TinyPNG)
2. **Minify CSS/JS** files
3. **Optimize** file sizes
4. **Remove** unused code

### Netlify Optimizations:
1. **Enable** Asset Optimization in Build settings
2. **Use** Netlify Forms for contact forms
3. **Enable** Gzip compression
4. **Configure** caching headers

---

## Security Best Practices

### Recommended Settings:
1. **Enable** HTTPS redirect
2. **Set** security headers
3. **Use** environment variables for sensitive data
4. **Regular** dependency updates
5. **Monitor** deployment logs

---

## Backup Strategy

### Recommended Approach:
1. **Keep** local copies of all files
2. **Use** Git for version control
3. **Export** Netlify site settings
4. **Document** all configurations
5. **Regular** backups to cloud storage

---

*This guide covers all aspects of deploying and maintaining your Retail-Lite POS site on Netlify. For additional support, refer to Netlify's official documentation or contact their support team.*