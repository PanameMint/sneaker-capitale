# Sneaker Capitale — Setup Guide

## What's in here
- `_config.yml` — site settings (title, theme)
- `index.md` — homepage
- `about.md` — about page
- `_posts/` — every article/news/release-date post goes here as one Markdown file each
- `Gemfile` — only needed if you ever want to preview the site on your own computer; not needed for GitHub Pages

## Getting this live (no coding required)

1. **Create a GitHub account** at github.com (free).
2. **Create a new repository** named exactly `sneakercapitale.github.io` — wait, actually name it `sneaker-capitale` (any name is fine since we'll use a custom domain).
3. Upload every file in this folder into that repository (drag and drop into GitHub's web uploader works fine — keep the `_posts` folder structure intact).
4. In the repo, go to **Settings → Pages**, and set the source to the `main` branch. GitHub will build and publish the site automatically — you'll get a free `https://yourusername.github.io/sneaker-capitale/` URL within a minute or two.
5. Once you've bought your domain, come back to **Settings → Pages** and add it as a "custom domain" — I'll walk you through the DNS records when you get there.

## Publishing a new article
1. In GitHub, open the `_posts` folder.
2. Click "Add file" → "Create new file".
3. Name it `YYYY-MM-DD-your-title.md` (the date matters — Jekyll uses it to sort posts).
4. Copy the format from an existing post (the `---` block at the top, then your text below).
5. Commit the file — the site rebuilds and publishes automatically.

Send me the article text and I'll format it into a ready-to-paste post each time.
