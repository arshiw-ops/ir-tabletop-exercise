# GitHub Pages Deployment Guide

This guide explains how to deploy the Incident Response Table Top Exercise to GitHub Pages for your team.

## Prerequisites

- A GitHub account
- Git installed on your local machine
- Node.js and pnpm installed (for building locally)

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and sign in to your account
2. Click the **+** icon in the top right and select **New repository**
3. Name your repository (e.g., `ir-tabletop-exercise`)
4. Choose **Public** (so your team can access it)
5. Do NOT initialize with README, .gitignore, or license (we'll add these)
6. Click **Create repository**

## Step 2: Push Code to GitHub

### Option A: Using Command Line (Recommended)

```bash
# Navigate to the project directory
cd ir-tabletop-exercise

# Initialize git if not already done
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Incident Response Table Top Exercise"

# Add remote repository (replace YOUR_USERNAME and YOUR_REPO)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Option B: Using GitHub Desktop

1. Open GitHub Desktop
2. Click **File** → **New Repository**
3. Select the local path to your project
4. Click **Create Repository**
5. Click **Publish repository** to push to GitHub

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. Scroll down to **Pages** section in the left sidebar
4. Under **Source**, select **Deploy from a branch**
5. Select **main** branch and **/root** folder
6. Click **Save**

## Step 4: Configure for GitHub Pages Deployment

The application is configured to work with GitHub Pages. The build process creates static files in the `dist/public` directory that GitHub Pages will serve.

### Important: Update Base URL (if using a subdirectory)

If your repository is named something other than your username (e.g., `https://username.github.io/ir-tabletop-exercise`), you need to update the Vite configuration:

1. Open `vite.config.ts` (or create it if it doesn't exist)
2. Add or update the base configuration:

```typescript
export default defineConfig({
  base: '/ir-tabletop-exercise/',
  // ... rest of config
})
```

Replace `ir-tabletop-exercise` with your actual repository name.

## Step 5: Deploy

### Automatic Deployment with GitHub Actions (Recommended)

Create a `.github/workflows/deploy.yml` file:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
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
        
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist/public
```

Then:
1. Commit and push this file to GitHub
2. Go to your repository **Settings** → **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Select **gh-pages** branch and **/ (root)** folder
5. Save

### Manual Deployment

If you prefer to deploy manually:

```bash
# Build the application
pnpm build

# The static files are now in dist/public
# You can deploy these files to GitHub Pages using:
# - GitHub Desktop
# - git subtree
# - Or any other deployment method
```

## Step 6: Access Your Application

After deployment completes (usually within 1-2 minutes):

- **If using username.github.io**: `https://username.github.io/ir-tabletop-exercise`
- **If using a custom domain**: Configure in GitHub Pages settings

Your team can now access the application at this URL!

## Troubleshooting

### Application loads but styles/images are broken

**Solution**: Update the base URL in `vite.config.ts` to match your repository structure.

### GitHub Pages not updating after push

**Solution**: 
1. Check the **Actions** tab in your repository to see if the build succeeded
2. Wait 1-2 minutes for deployment to complete
3. Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)

### 404 errors when navigating

**Solution**: This is a client-side routing issue. The application uses client-side routing, so all routes should work. If you see 404s:
1. Check that the base URL is correctly configured
2. Ensure the `dist/public` folder is being deployed

## Updating the Application

To update the application with new scenarios or quiz questions:

1. Make changes to the code locally
2. Test with `pnpm dev`
3. Commit changes: `git add . && git commit -m "Update: description of changes"`
4. Push to GitHub: `git push origin main`
5. GitHub Actions will automatically build and deploy

## Team Access

Share the deployed URL with your team. They can:
- Access the application from any browser
- Complete scenarios and take quizzes
- Progress is saved locally in their browser (no server needed)
- No login required

## Notes

- **Progress Storage**: User progress is saved in browser localStorage. Each user's progress is independent.
- **No Backend**: This is a static application with no backend server, so it's lightweight and fast.
- **Offline Support**: Once loaded, the application can work offline (progress won't sync across devices).
- **Custom Domain**: To use a custom domain, configure it in GitHub Pages settings.

## Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Vite Deployment Guide](https://vitejs.dev/guide/static-deploy.html#github-pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

## Support

For issues or questions about the application itself, refer to the README.md file.
