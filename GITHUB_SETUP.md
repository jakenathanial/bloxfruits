# 📚 GitHub Repository Setup Guide

Step-by-step guide to push RentAFruit to GitHub and make it deployment-ready.

---

## 🎯 Quick Setup (5 minutes)

### Step 1: Initialize Git Repository

```bash
# Navigate to project directory
cd rentafruit

# Initialize git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: RentAFruit gaming platform"
```

### Step 2: Create GitHub Repository

**Option A: Via GitHub Website**
1. Go to https://github.com/new
2. Repository name: `rentafruit`
3. Description: "Dark-themed gaming platform for trading fruits and hunting Leviathans"
4. Visibility: Public or Private
5. **DO NOT** initialize with README (we already have one)
6. Click "Create repository"

**Option B: Via GitHub CLI**
```bash
# Install GitHub CLI if not installed
# macOS: brew install gh
# Windows: winget install GitHub.cli

# Login to GitHub
gh auth login

# Create repository
gh repo create rentafruit --public --source=. --remote=origin --push
```

### Step 3: Push to GitHub

```bash
# Add remote origin (skip if using gh CLI)
git remote add origin https://github.com/YOUR_USERNAME/rentafruit.git

# Rename branch to main (if needed)
git branch -M main

# Push code
git push -u origin main
```

---

## 📋 Repository Configuration

### Add Repository Topics

Make your repo discoverable by adding topics:
1. Go to repo on GitHub
2. Click ⚙️ next to "About"
3. Add topics:
   - `react`
   - `typescript`
   - `tailwindcss`
   - `vite`
   - `gaming`
   - `trading-platform`
   - `dark-theme`
   - `responsive-design`

### Create Repository Description

```
🍎 RentAFruit - A dark futuristic gaming platform for trading legendary fruits and conquering Leviathan hunts. Built with React, TypeScript, and Tailwind CSS.
```

### Set Homepage

Add your deployment URL once deployed (e.g., `https://rentafruit.vercel.app`)

---

## 🏷️ Create Releases

### Initial Release (v1.0.0)

```bash
# Create and push tag
git tag -a v1.0.0 -m "Initial release: RentAFruit v1.0.0"
git push origin v1.0.0
```

On GitHub:
1. Go to Releases
2. Click "Create a new release"
3. Tag: `v1.0.0`
4. Title: "RentAFruit v1.0.0 - Initial Release"
5. Description:
   ```markdown
   ## 🎉 Initial Release

   ### Features
   - ✅ Trading system with fruit marketplace
   - ✅ Leviathan hunt rooms (Tiki Outpost & Hydra Island)
   - ✅ User profiles with boat equipment
   - ✅ Real-time chat functionality
   - ✅ Admin panel for fruit management
   - ✅ Fully responsive dark-themed UI
   - ✅ Mobile-first design with bottom navigation

   ### Tech Stack
   - React 18.3.1
   - TypeScript
   - Tailwind CSS v4
   - React Router 7
   - Vite 6

   ### Getting Started
   See [README.md](README.md) for installation and deployment instructions.
   ```

---

## 🛡️ Repository Settings

### Branch Protection (Recommended)

1. Go to Settings → Branches
2. Add rule for `main` branch:
   - ✅ Require pull request reviews before merging
   - ✅ Require status checks to pass
   - ✅ Require branches to be up to date

### GitHub Pages (Optional)

1. Settings → Pages
2. Source: Deploy from branch `gh-pages`
3. See [DEPLOYMENT.md](DEPLOYMENT.md) for setup

---

## 📁 Recommended Files

Your repository should include:

- ✅ `README.md` - Main documentation
- ✅ `DEPLOYMENT.md` - Deployment guide
- ✅ `GITHUB_SETUP.md` - This file
- ✅ `.gitignore` - Ignored files
- ✅ `LICENSE` - Open source license
- ⬜ `CONTRIBUTING.md` - Contribution guidelines
- ⬜ `CODE_OF_CONDUCT.md` - Community guidelines
- ⬜ `CHANGELOG.md` - Version history

---

## 📝 Optional: Add License

### MIT License

Create `LICENSE` file:

```
MIT License

Copyright (c) 2026 RentAFruit

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

Or use GitHub's license picker:
1. Add file → Create new file
2. Name it `LICENSE`
3. Click "Choose a license template"
4. Select MIT License
5. Commit

---

## 🎨 Add Social Preview

Create an eye-catching social preview image:

1. Create 1280x640px image with:
   - RentAFruit logo
   - Tagline: "Trade. Hunt. Rise."
   - Dark purple/blue theme
   - Fruit emojis

2. Upload:
   - Settings → General
   - Social preview → Upload an image

---

## 🔗 Repository Sections

### Code

Add useful links to your README:
```markdown
[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://rentafruit.vercel.app)
[![GitHub](https://img.shields.io/github/stars/yourusername/rentafruit?style=social)](https://github.com/yourusername/rentafruit)
```

### Issues

Enable issue templates:
1. Settings → Features → Issues (✅)
2. Create `.github/ISSUE_TEMPLATE/bug_report.md`
3. Create `.github/ISSUE_TEMPLATE/feature_request.md`

### Discussions

Enable for community Q&A:
- Settings → Features → Discussions (✅)

---

## 🤝 Contributing Guidelines

Create `CONTRIBUTING.md`:

```markdown
# Contributing to RentAFruit

We love your input! We want to make contributing as easy as possible.

## Development Process

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Code Style

- Use TypeScript for all new code
- Follow existing code style
- Write meaningful commit messages
- Add comments for complex logic

## Pull Request Process

1. Update README.md with details of changes
2. Update CHANGELOG.md
3. The PR will be merged once approved by maintainers

## Report Bugs

Use GitHub Issues with the bug report template.

## Suggest Features

Use GitHub Issues with the feature request template.
```

---

## 🚀 Continuous Integration (Optional)

### GitHub Actions Workflow

Create `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install pnpm
        run: npm install -g pnpm
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Build
        run: pnpm build
      
      - name: Type check (if configured)
        run: pnpm type-check || echo "Type check not configured"
```

---

## 📊 GitHub Stats Badges

Add to README.md:

```markdown
![Stars](https://img.shields.io/github/stars/yourusername/rentafruit?style=social)
![Forks](https://img.shields.io/github/forks/yourusername/rentafruit?style=social)
![Issues](https://img.shields.io/github/issues/yourusername/rentafruit)
![License](https://img.shields.io/github/license/yourusername/rentafruit)
![Last Commit](https://img.shields.io/github/last-commit/yourusername/rentafruit)
```

---

## ✅ Final Checklist

Before making repository public:

- [ ] All sensitive data removed (.env files ignored)
- [ ] README.md complete with screenshots
- [ ] LICENSE file added
- [ ] .gitignore configured
- [ ] Repository description set
- [ ] Topics added
- [ ] Social preview image uploaded
- [ ] All links in README work
- [ ] Code builds successfully
- [ ] Deployment works

---

## 🎉 Share Your Project!

Once ready, share on:
- Reddit: r/reactjs, r/webdev
- Twitter/X with #React #WebDev #Gaming
- Dev.to blog post
- Hacker News (Show HN:)
- Product Hunt

---

**Your project is now ready for the world! 🚀**
