# Quarto Website Setup Guide for GitHub Pages

This guide documents how to create and publish a Quarto website on GitHub Pages.

## Prerequisites

- Quarto installed ([download here](https://quarto.org/docs/get-started/))
- Git installed
- GitHub account

## Step 1: Create a GitHub Repository

1. Go to GitHub and create a new repository
2. Name it `<username>.github.io` (e.g., `edreiyu.github.io`)
3. Initialize it (with or without README)
4. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/<username>/<username>.github.io.git
   cd <username>.github.io
   ```

## Step 2: Create Quarto Website Files

### Create `_quarto.yml` (main configuration):
```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Your Website Title"
  navbar:
    left:
      - href: index.qmd
        text: Home
      - about.qmd

format:
  html:
    theme:
      - cosmo
      - brand
    css: styles.css
    toc: true
```

**Key configuration:**
- `output-dir: docs` - GitHub Pages will serve from this folder
- `type: website` - Tells Quarto this is a website project

### Create `index.qmd` (home page):
```markdown
---
title: "Your Website Title"
---

# Welcome to My Website

This is the home page content.

## About This Site

Add your content here using Markdown.
```

### Create `about.qmd` (about page):
```markdown
---
title: "About"
---

## About Me

Add information about yourself here.
```

### Create `styles.css` (optional custom styles):
```css
/* Add custom CSS here */
```

## Step 3: Add `.nojekyll` File

Create an empty `.nojekyll` file in the root directory:
```bash
touch .nojekyll
```

**Why?** This tells GitHub Pages not to process your site with Jekyll, which is important for Quarto sites.

## Step 4: Build the Website

Run Quarto to render your website:
```bash
quarto render
```

This will create all HTML files in the `docs/` directory.

## Step 5: Commit and Push to GitHub

```bash
git add .
git commit -m "Initial Quarto website setup"
git push origin main
```

## Step 6: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (in the left sidebar)
3. Under **Source**, select:
   - Branch: `main`
   - Folder: `/docs`
4. Click **Save**

## Step 7: Access Your Website

After a few minutes, your website will be available at:
```
https://<username>.github.io
```

## Making Updates

Whenever you want to update your website:

1. Edit your `.qmd` files
2. Run `quarto render` to rebuild
3. Commit and push changes:
   ```bash
   git add .
   git commit -m "Update content"
   git push origin main
   ```

## Tips

- **Preview locally**: Run `quarto preview` to see changes before publishing
- **Add pages**: Create new `.qmd` files and add them to `_quarto.yml` navbar
- **Themes**: Explore other [Quarto themes](https://quarto.org/docs/output-formats/html-themes.html)
- **Advanced features**: Add blog posts, custom layouts, and more using [Quarto documentation](https://quarto.org/docs/websites/)

## Common Issues

### Site not updating?
- Make sure you ran `quarto render` before pushing
- Check GitHub Actions tab for build errors
- Clear browser cache

### 404 errors?
- Verify GitHub Pages is set to serve from `/docs` folder
- Ensure `.nojekyll` file exists
- Check that `docs/` folder is committed to git

### Styling looks broken?
- Check that `site_libs/` folder is in `docs/` directory
- Verify all files in `docs/` are committed

## Project Structure

```
your-repo/
├── .nojekyll           # Prevents Jekyll processing
├── _quarto.yml         # Main configuration
├── index.qmd           # Home page
├── about.qmd           # About page
├── styles.css          # Custom CSS
└── docs/               # Generated HTML (published to GitHub Pages)
    ├── .nojekyll
    ├── index.html
    ├── about.html
    ├── site_libs/
    └── ...
```

## Additional Resources

- [Quarto Websites](https://quarto.org/docs/websites/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Quarto Publishing Guide](https://quarto.org/docs/publishing/github-pages.html)
