# Deployment Guide

This guide explains how to deploy the Celstomp documentation to various hosting platforms.

## Quick Deploy

### GitHub Pages (Recommended)

1. **Create `docs` folder in main repo:**
```bash
# From celstomp_mdbook directory
cp -r book/* /home/immalloy/Documents/celstomp_v1/docs/
```

2. **Commit to repository:**
```bash
cd /home/immalloy/Documents/celstomp_v1
git add docs/
git commit -m "Add documentation site"
git push
```

3. **Enable GitHub Pages:**
- Go to repository Settings
- Navigate to Pages section
- Select "Deploy from a branch"
- Choose branch: `main` (or `master`)
- Select folder: `/docs`
- Click Save

4. **Access your site:**
- URL: `https://ginyoa.github.io/celstomp_v1/`
- May take a few minutes to deploy

### Netlify

1. **Build the site:**
```bash
cd /home/immalloy/Documents/celstomp_mdbook
mdbook build
```

2. **Deploy:**
- Go to [netlify.com](https://netlify.com)
- Drag and drop the `book/` folder
- Or connect GitHub repository

3. **Configure:**
- Build command: `mdbook build`
- Publish directory: `book`

### Vercel

1. **Install Vercel CLI:**
```bash
npm i -g vercel
```

2. **Deploy:**
```bash
cd /home/immalloy/Documents/celstomp_mdbook
vercel --prod
```

Or connect repository in Vercel dashboard.

## Manual Deployment

### Any Static Host

The `book/` directory contains a complete static website:

```
book/
├── index.html          # Homepage
├── *.html              # All documentation pages
├── css/                # Stylesheets
├── fonts/              # Fonts
├── community/          # Community pages
├── concepts/           # Concepts pages
├── development/        # Development pages
├── guides/             # Guides pages
├── reference/          # Reference pages
└── searchindex.js      # Search functionality
```

Simply upload all contents of `book/` to your web server.

### FTP/SFTP

```bash
# Example using rsync
rsync -avz book/ user@yourserver:/var/www/celstomp-docs/
```

### AWS S3

```bash
# Sync to S3 bucket
aws s3 sync book/ s3://your-bucket-name --delete

# Make public (if needed)
aws s3api put-bucket-acl --bucket your-bucket-name --acl public-read
```

## Automated Deployment

### GitHub Actions

Create `.github/workflows/docs.yml` in the main repo:

```yaml
name: Deploy Documentation

on:
  push:
    branches: [ main ]
    paths:
      - 'docs/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup mdBook
      uses: peaceiris/actions-mdbook@v1
      with:
        mdbook-version: 'latest'
    
    - name: Build
      run: cd celstomp_mdbook && mdbook build
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./celstomp_mdbook/book
```

### Local Build Script

Create `build-docs.sh`:

```bash
#!/bin/bash
set -e

echo "Building documentation..."
cd /home/immalloy/Documents/celstomp_mdbook
mdbook build

echo "Copying to main repo..."
rm -rf /home/immalloy/Documents/celstomp_v1/docs
cp -r book /home/immalloy/Documents/celstomp_v1/docs

echo "Committing changes..."
cd /home/immalloy/Documents/celstomp_v1
git add docs/
git commit -m "Update documentation"
git push

echo "Done!"
```

Make executable:
```bash
chmod +x build-docs.sh
```

## Custom Domain

### GitHub Pages with Custom Domain

1. **Add CNAME file:**
```bash
echo "docs.celstomp.com" > book/CNAME
```

2. **Configure DNS:**
- Add CNAME record: `docs` → `ginyoa.github.io`
- Or A records to GitHub Pages IPs

3. **Enable in Settings:**
- Repository Settings → Pages
- Enter custom domain
- Enable HTTPS

## Verification

### Check Build

```bash
cd /home/immalloy/Documents/celstomp_mdbook
mdbook build

# Check for errors
ls -la book/index.html
```

### Test Locally

```bash
mdbook serve
# Open http://localhost:3000
```

### Validate Links

Install link checker:
```bash
cargo install mdbook-linkcheck
```

Add to `book.toml`:
```toml
[output.linkcheck]
```

Run check:
```bash
mdbook build
```

## Maintenance

### Updating Documentation

1. Edit files in `src/` directory
2. Test locally: `mdbook serve`
3. Build: `mdbook build`
4. Deploy using method above

### Versioning

For versioned docs:

```bash
# Build specific version
mdbook build
cp -r book /path/to/site/v1.0/

# Build latest
mdbook build
cp -r book /path/to/site/latest/
```

### Analytics (Optional)

Add to `book.toml`:
```toml
[output.html]
additional-js = ["analytics.js"]
```

Create `src/analytics.js`:
```javascript
// Your analytics code here
```

## Troubleshooting

### Build Fails

1. Check mdbook version: `mdbook --version`
2. Validate `book.toml` syntax
3. Check all referenced files exist
4. Look for errors in output

### 404 Errors

1. Check all pages in `SUMMARY.md`
2. Verify internal links
3. Ensure base URL is correct

### Styling Issues

1. Check `custom.css` is included in `book.toml`
2. Verify CSS syntax
3. Clear browser cache

## Support

For deployment issues:
- Check [mdBook documentation](https://rust-lang.github.io/mdBook/)
- Review hosting provider docs
- Open an issue on GitHub

## See Also

- [mdBook Guide](https://rust-lang.github.io/mdBook/)
- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Netlify Docs](https://docs.netlify.com/)
