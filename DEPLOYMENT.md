# 🚀 RentAFruit Deployment Guide

Complete guide for deploying RentAFruit to various hosting platforms.

---

## 📦 Pre-Deployment Checklist

- [ ] All dependencies installed (`pnpm install`)
- [ ] Build succeeds locally (`pnpm build`)
- [ ] No TypeScript errors (`pnpm type-check`)
- [ ] Environment variables configured (if needed)
- [ ] Git repository initialized
- [ ] Code pushed to GitHub

---

## 🌐 Deployment Options

### Option 1: Vercel (Recommended)

**Why Vercel?**
- Zero configuration
- Automatic HTTPS
- Global CDN
- Perfect for React/Vite apps
- Free tier available

**Steps:**

1. **Via Vercel Dashboard:**
   ```bash
   # Push to GitHub first
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/yourusername/rentafruit.git
   git push -u origin main
   ```

2. Go to [vercel.com](https://vercel.com)
3. Click "Import Project"
4. Select your GitHub repository
5. Vercel auto-detects Vite
6. Click "Deploy"

**Via Vercel CLI:**
   ```bash
   # Install Vercel CLI globally
   npm i -g vercel

   # Login
   vercel login

   # Deploy
   vercel

   # Deploy to production
   vercel --prod
   ```

**Custom Domain:**
   - Go to Project Settings → Domains
   - Add your custom domain
   - Update DNS records as instructed

---

### Option 2: Netlify

**Why Netlify?**
- Simple drag-and-drop deployment
- Built-in CI/CD
- Form handling (useful for future features)
- Free SSL certificates

**Steps:**

1. **Build the project:**
   ```bash
   pnpm build
   ```

2. **Via Netlify Dashboard:**
   - Go to [app.netlify.com](https://app.netlify.com)
   - Click "Add new site" → "Import an existing project"
   - Connect to GitHub
   - Configure build settings:
     - Build command: `pnpm build`
     - Publish directory: `dist`
   - Click "Deploy"

**Via Netlify CLI:**
   ```bash
   # Install Netlify CLI
   npm install -g netlify-cli

   # Login
   netlify login

   # Initialize
   netlify init

   # Deploy
   netlify deploy --prod
   ```

**Netlify Configuration File (`netlify.toml`):**
   ```toml
   [build]
     command = "pnpm build"
     publish = "dist"

   [[redirects]]
     from = "/*"
     to = "/index.html"
     status = 200
   ```

---

### Option 3: GitHub Pages

**Why GitHub Pages?**
- Free hosting
- Simple for static sites
- Integrated with GitHub

**Steps:**

1. **Install gh-pages:**
   ```bash
   pnpm add -D gh-pages
   ```

2. **Update vite.config.ts:**
   ```typescript
   export default defineConfig({
     base: '/rentafruit/', // Replace with your repo name
     // ... other config
   })
   ```

3. **Add scripts to package.json:**
   ```json
   {
     "scripts": {
       "predeploy": "pnpm build",
       "deploy": "gh-pages -d dist"
     }
   }
   ```

4. **Deploy:**
   ```bash
   pnpm deploy
   ```

5. **Enable GitHub Pages:**
   - Go to repo Settings → Pages
   - Source: `gh-pages` branch
   - Save

---

### Option 4: Railway

**Why Railway?**
- Simple CLI
- Automatic deployments
- Support for databases (for future backend)

**Steps:**

   ```bash
   # Install Railway CLI
   npm i -g @railway/cli

   # Login
   railway login

   # Initialize
   railway init

   # Deploy
   railway up
   ```

---

### Option 5: Render

**Why Render?**
- Free tier with custom domains
- Auto-deploy from Git
- Easy to add backend services later

**Steps:**

1. Go to [render.com](https://render.com)
2. New → Static Site
3. Connect GitHub repository
4. Configure:
   - Build Command: `pnpm build`
   - Publish Directory: `dist`
5. Create Static Site

---

## 🔐 Environment Variables

If you add backend integration (Supabase, Firebase, etc.), set environment variables:

### Vercel
```bash
vercel env add VITE_API_URL
vercel env add VITE_SUPABASE_URL
vercel env add VITE_SUPABASE_ANON_KEY
```

### Netlify
- Dashboard → Site Settings → Environment Variables
- Or use Netlify CLI:
  ```bash
  netlify env:set VITE_API_URL "your-value"
  ```

### GitHub Pages
- Not recommended for sensitive env vars
- Use GitHub Actions secrets instead

---

## 🚨 Common Issues

### Build Fails

**Problem:** `Module not found` errors

**Solution:**
```bash
# Clear cache and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm build
```

### Routes Don't Work (404 on refresh)

**Problem:** React Router routes return 404 on direct access

**Solution for Vercel:**
Create `vercel.json`:
```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/" }
  ]
}
```

**Solution for Netlify:**
Create `public/_redirects`:
```
/*    /index.html   200
```

### Blank Page After Deploy

**Problem:** White screen, no errors

**Solution:**
1. Check `base` in `vite.config.ts`
2. Ensure `dist` folder is being deployed
3. Check browser console for errors

---

## 📊 Post-Deployment

### Performance Optimization

1. **Enable Gzip/Brotli:**
   - Most platforms enable this automatically
   - Vercel/Netlify handle it by default

2. **Add Analytics:**
   ```bash
   # Example with Vercel Analytics
   pnpm add @vercel/analytics
   ```

3. **Setup Monitoring:**
   - [Sentry](https://sentry.io) for error tracking
   - [LogRocket](https://logrocket.com) for session replay

### Custom Domain Setup

1. Purchase domain (Namecheap, Google Domains, etc.)
2. Add to hosting platform
3. Update DNS records:
   - **A Record:** Points to hosting IP
   - **CNAME:** Points subdomain to hosting

**Example (Vercel):**
- Add domain in Vercel dashboard
- Update DNS:
  - Type: `A`, Name: `@`, Value: `76.76.21.21`
  - Type: `CNAME`, Name: `www`, Value: `cname.vercel-dns.com`

---

## 🔄 Continuous Deployment

### GitHub Actions (Example)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install pnpm
        run: npm install -g pnpm
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Build
        run: pnpm build
      
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
          vercel-args: '--prod'
```

---

## 📝 Deployment Checklist

- [ ] Code pushed to GitHub
- [ ] Build succeeds locally
- [ ] Environment variables configured
- [ ] Platform selected (Vercel/Netlify/etc.)
- [ ] Site deployed successfully
- [ ] All routes work correctly
- [ ] Custom domain configured (optional)
- [ ] HTTPS enabled
- [ ] Analytics setup (optional)
- [ ] Error monitoring enabled (optional)

---

## 🎯 Next Steps

After deployment:
1. Test all features on live site
2. Setup backend (Supabase recommended)
3. Add authentication
4. Enable real-time features
5. Setup database
6. Add payment integration (if needed)

---

## 🆘 Need Help?

- **Vercel Docs:** https://vercel.com/docs
- **Netlify Docs:** https://docs.netlify.com
- **Vite Docs:** https://vitejs.dev/guide/static-deploy.html
- **GitHub Issues:** Open an issue on the repo

---

**Happy Deploying! 🚀**
